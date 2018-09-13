---
title: SQL queries for Azure Cosmos DB | Microsoft Docs
description: Learn about SQL syntax, database concepts, and SQL queries for Azure Cosmos DB. SQL can used as a JSON query language in Azure Cosmos DB.
keywords: sql syntax,sql query, sql queries, json query language, database concepts and sql queries, aggregate functions
services: cosmos-db
author: LalithaMV
manager: kfile
editor: monicar
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: na
ms.topic: conceptual
ms.date: 08/10/2018
ms.author: laviswa
ms.openlocfilehash: 766a2a9a2b71d9cd013f26b843d413d7603ab1fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866246"
---
# <a name="query-azure-cosmos-db-data-with-sql-queries"></a><span data-ttu-id="b62c5-105">Query Azure Cosmos DB data with SQL queries</span><span class="sxs-lookup"><span data-stu-id="b62c5-105">Query Azure Cosmos DB data with SQL queries</span></span>

<span data-ttu-id="b62c5-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language on SQL API accounts.</span><span class="sxs-lookup"><span data-stu-id="b62c5-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language on SQL API accounts.</span></span> <span data-ttu-id="b62c5-107">While designing the query language for Azure Cosmos DB, the following two goals are considered:</span><span class="sxs-lookup"><span data-stu-id="b62c5-107">While designing the query language for Azure Cosmos DB, the following two goals are considered:</span></span>

* <span data-ttu-id="b62c5-108">Instead of inventing a new query language, we made Azure Cosmos DB to support SQL, one of the most familiar and popular query languages.</span><span class="sxs-lookup"><span data-stu-id="b62c5-108">Instead of inventing a new query language, we made Azure Cosmos DB to support SQL, one of the most familiar and popular query languages.</span></span> <span data-ttu-id="b62c5-109">Azure Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span><span class="sxs-lookup"><span data-stu-id="b62c5-109">Azure Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>  

* <span data-ttu-id="b62c5-110">Azure Cosmos DB uses JavaScript's programming model as the foundation for the query language.</span><span class="sxs-lookup"><span data-stu-id="b62c5-110">Azure Cosmos DB uses JavaScript's programming model as the foundation for the query language.</span></span> <span data-ttu-id="b62c5-111">The SQL API is rooted in JavaScript's type system, expression evaluation, and function invocation.</span><span class="sxs-lookup"><span data-stu-id="b62c5-111">The SQL API is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="b62c5-112">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span><span class="sxs-lookup"><span data-stu-id="b62c5-112">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="b62c5-113">This article walks you through some examples SQL queries by using simple JSON documents.</span><span class="sxs-lookup"><span data-stu-id="b62c5-113">This article walks you through some examples SQL queries by using simple JSON documents.</span></span> <span data-ttu-id="b62c5-114">To learn about Azure Cosmos DB SQL language syntax, see [SQL syntax reference](sql-api-sql-query-reference.md) article.</span><span class="sxs-lookup"><span data-stu-id="b62c5-114">To learn about Azure Cosmos DB SQL language syntax, see [SQL syntax reference](sql-api-sql-query-reference.md) article.</span></span> 

## <a id="GettingStarted"></a><span data-ttu-id="b62c5-115">Get started with SQL commands</span><span class="sxs-lookup"><span data-stu-id="b62c5-115">Get started with SQL commands</span></span>
<span data-ttu-id="b62c5-116">Let's create two simple JSON documents and query against that data.</span><span class="sxs-lookup"><span data-stu-id="b62c5-116">Let's create two simple JSON documents and query against that data.</span></span> <span data-ttu-id="b62c5-117">Consider two JSON documents about families, insert these JSON documents into a collection and subsequently query the data.</span><span class="sxs-lookup"><span data-stu-id="b62c5-117">Consider two JSON documents about families, insert these JSON documents into a collection and subsequently query the data.</span></span> <span data-ttu-id="b62c5-118">Here we have a simple JSON document for the Andersen and Wakefield families, the parents, children (and their pets), address, and registration information.</span><span class="sxs-lookup"><span data-stu-id="b62c5-118">Here we have a simple JSON document for the Andersen and Wakefield families, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="b62c5-119">The document has strings, numbers, Booleans, arrays, and nested properties.</span><span class="sxs-lookup"><span data-stu-id="b62c5-119">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="b62c5-120">**Document1**</span><span class="sxs-lookup"><span data-stu-id="b62c5-120">**Document1**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="b62c5-121">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-121">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="b62c5-122">**Document2**</span><span class="sxs-lookup"><span data-stu-id="b62c5-122">**Document2**</span></span>  

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

<span data-ttu-id="b62c5-123">Now let's try a few queries against this data to understand some of the key aspects of Azure Cosmos DB's SQL query language.</span><span class="sxs-lookup"><span data-stu-id="b62c5-123">Now let's try a few queries against this data to understand some of the key aspects of Azure Cosmos DB's SQL query language.</span></span> 

<span data-ttu-id="b62c5-124">**Query1**: For example, the following query returns the documents where the id field matches `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-124">**Query1**: For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="b62c5-125">Since it's a `SELECT *`, the output of the query is the complete JSON document, to learn about the syntax, see [SELECT statement](sql-api-sql-query-reference.md#select-query):</span><span class="sxs-lookup"><span data-stu-id="b62c5-125">Since it's a `SELECT *`, the output of the query is the complete JSON document, to learn about the syntax, see [SELECT statement](sql-api-sql-query-reference.md#select-query):</span></span>

```sql
    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-126">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-126">**Results**</span></span>

```json
    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]
```

<span data-ttu-id="b62c5-127">**Query2** : Now consider the case where we need to reformat the JSON output in a different shape.</span><span class="sxs-lookup"><span data-stu-id="b62c5-127">**Query2** : Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="b62c5-128">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span><span class="sxs-lookup"><span data-stu-id="b62c5-128">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="b62c5-129">In this case, "NY, NY" matches.</span><span class="sxs-lookup"><span data-stu-id="b62c5-129">In this case, "NY, NY" matches.</span></span>   

```sql
    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state
```

<span data-ttu-id="b62c5-130">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-130">**Results**</span></span>

```json
    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]
```

<span data-ttu-id="b62c5-131">**Query3**: This query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span><span class="sxs-lookup"><span data-stu-id="b62c5-131">**Query3**: This query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

```sql
    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC
```

<span data-ttu-id="b62c5-132">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-132">**Results**</span></span>

```json
    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]
```

<span data-ttu-id="b62c5-133">Following are few aspects of the Cosmos DB query language through the examples you've seen so far:</span><span class="sxs-lookup"><span data-stu-id="b62c5-133">Following are few aspects of the Cosmos DB query language through the examples you've seen so far:</span></span>  

* <span data-ttu-id="b62c5-134">Since SQL API works on JSON values, it deals with tree shaped entities instead of rows and columns.</span><span class="sxs-lookup"><span data-stu-id="b62c5-134">Since SQL API works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="b62c5-135">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-135">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   

* <span data-ttu-id="b62c5-136">The structured query language works with schema-less data.</span><span class="sxs-lookup"><span data-stu-id="b62c5-136">The structured query language works with schema-less data.</span></span> <span data-ttu-id="b62c5-137">Therefore, the type system needs to be bound dynamically.</span><span class="sxs-lookup"><span data-stu-id="b62c5-137">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="b62c5-138">The same expression could yield different types on different documents.</span><span class="sxs-lookup"><span data-stu-id="b62c5-138">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="b62c5-139">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span><span class="sxs-lookup"><span data-stu-id="b62c5-139">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  

* <span data-ttu-id="b62c5-140">Azure Cosmos DB supports strict JSON documents only.</span><span class="sxs-lookup"><span data-stu-id="b62c5-140">Azure Cosmos DB supports strict JSON documents only.</span></span> <span data-ttu-id="b62c5-141">This means the type system and expressions are restricted to deal only with JSON types.</span><span class="sxs-lookup"><span data-stu-id="b62c5-141">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="b62c5-142">Refer to the [JSON specification](http://www.json.org/) for more details.</span><span class="sxs-lookup"><span data-stu-id="b62c5-142">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  

* <span data-ttu-id="b62c5-143">A Cosmos DB collection is a schema-free container of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="b62c5-143">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="b62c5-144">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span><span class="sxs-lookup"><span data-stu-id="b62c5-144">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="b62c5-145">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span><span class="sxs-lookup"><span data-stu-id="b62c5-145">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <a id="SelectClause"></a><span data-ttu-id="b62c5-146">Select clause</span><span class="sxs-lookup"><span data-stu-id="b62c5-146">Select clause</span></span>

<span data-ttu-id="b62c5-147">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span><span class="sxs-lookup"><span data-stu-id="b62c5-147">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="b62c5-148">Typically, for each query, the source in the FROM clause is enumerated.</span><span class="sxs-lookup"><span data-stu-id="b62c5-148">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="b62c5-149">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="b62c5-149">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="b62c5-150">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span><span class="sxs-lookup"><span data-stu-id="b62c5-150">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span> <span data-ttu-id="b62c5-151">To learn about the syntax, see [SELECT syntax](sql-api-sql-query-reference.md#bk_select_query).</span><span class="sxs-lookup"><span data-stu-id="b62c5-151">To learn about the syntax, see [SELECT syntax](sql-api-sql-query-reference.md#bk_select_query).</span></span>

<span data-ttu-id="b62c5-152">The following example shows a typical SELECT query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-152">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="b62c5-153">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-153">**Query**</span></span>

```sql
    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-154">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-154">**Results**</span></span>

```json
    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]
```

### <a name="nested-properties"></a><span data-ttu-id="b62c5-155">Nested properties</span><span class="sxs-lookup"><span data-stu-id="b62c5-155">Nested properties</span></span>
<span data-ttu-id="b62c5-156">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-156">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="b62c5-157">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-157">**Query**</span></span>

```sql
    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-158">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-158">**Results**</span></span>

```json
    [{
      "state": "WA", 
      "city": "seattle"
    }]
```

<span data-ttu-id="b62c5-159">Projection also supports JSON expressions as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b62c5-159">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="b62c5-160">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-160">**Query**</span></span>

```sql
    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-161">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-161">**Results**</span></span>

```json
    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]
```

<span data-ttu-id="b62c5-162">Let's look at the role of `$1` here.</span><span class="sxs-lookup"><span data-stu-id="b62c5-162">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="b62c5-163">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-163">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="b62c5-164">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-164">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="b62c5-165">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-165">**Query**</span></span>

```sql
    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-166">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-166">**Results**</span></span>

```json
    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]
```

## <a id="FromClause"></a><span data-ttu-id="b62c5-167">FROM clause</span><span class="sxs-lookup"><span data-stu-id="b62c5-167">FROM clause</span></span>

<span data-ttu-id="b62c5-168">The FROM <from_specification> clause is optional unless the source is filtered or projected later in the query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-168">The FROM <from_specification> clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="b62c5-169">To learn about the syntax, see [FROM syntax](sql-api-sql-query-reference.md#bk_from_clause).</span><span class="sxs-lookup"><span data-stu-id="b62c5-169">To learn about the syntax, see [FROM syntax](sql-api-sql-query-reference.md#bk_from_clause).</span></span> <span data-ttu-id="b62c5-170">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span><span class="sxs-lookup"><span data-stu-id="b62c5-170">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="b62c5-171">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span><span class="sxs-lookup"><span data-stu-id="b62c5-171">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="b62c5-172">The following list contains the rules that are enforced per query:</span><span class="sxs-lookup"><span data-stu-id="b62c5-172">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="b62c5-173">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-173">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="b62c5-174">Here `f` is the equivalent of `Families`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-174">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="b62c5-175">`AS` is an optional keyword to alias the identifier.</span><span class="sxs-lookup"><span data-stu-id="b62c5-175">`AS` is an optional keyword to alias the identifier.</span></span>  

* <span data-ttu-id="b62c5-176">Once aliased, the original source cannot be bound.</span><span class="sxs-lookup"><span data-stu-id="b62c5-176">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="b62c5-177">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span><span class="sxs-lookup"><span data-stu-id="b62c5-177">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>  

* <span data-ttu-id="b62c5-178">All properties that need to be referenced must be fully qualified.</span><span class="sxs-lookup"><span data-stu-id="b62c5-178">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="b62c5-179">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span><span class="sxs-lookup"><span data-stu-id="b62c5-179">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="b62c5-180">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span><span class="sxs-lookup"><span data-stu-id="b62c5-180">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="get-subdocuments-using-from-clause"></a><span data-ttu-id="b62c5-181">Get Subdocuments using FROM clause</span><span class="sxs-lookup"><span data-stu-id="b62c5-181">Get Subdocuments using FROM clause</span></span>

<span data-ttu-id="b62c5-182">The source can also be reduced to a smaller subset.</span><span class="sxs-lookup"><span data-stu-id="b62c5-182">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="b62c5-183">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b62c5-183">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="b62c5-184">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-184">**Query**</span></span>

```sql
    SELECT * 
    FROM Families.children
```

<span data-ttu-id="b62c5-185">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-185">**Results**</span></span>  

```json
    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]
```

<span data-ttu-id="b62c5-186">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-186">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="b62c5-187">If some families don’t have an `address.state` value, they are excluded in the query result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-187">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="b62c5-188">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-188">**Query**</span></span>

```sql
    SELECT * 
    FROM Families.address.state
```

<span data-ttu-id="b62c5-189">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-189">**Results**</span></span>

```json
    [
      "WA", 
      "NY"
    ]
```

## <a id="WhereClause"></a><span data-ttu-id="b62c5-190">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="b62c5-190">WHERE clause</span></span>
<span data-ttu-id="b62c5-191">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span><span class="sxs-lookup"><span data-stu-id="b62c5-191">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="b62c5-192">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-192">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="b62c5-193">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-193">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="b62c5-194">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-194">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> <span data-ttu-id="b62c5-195">To learn about the syntax, see [WHERE syntax](sql-api-sql-query-reference.md#bk_where_clause).</span><span class="sxs-lookup"><span data-stu-id="b62c5-195">To learn about the syntax, see [WHERE syntax](sql-api-sql-query-reference.md#bk_where_clause).</span></span>

<span data-ttu-id="b62c5-196">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-196">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="b62c5-197">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span><span class="sxs-lookup"><span data-stu-id="b62c5-197">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="b62c5-198">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-198">**Query**</span></span>

```sql
    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-199">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-199">**Results**</span></span>

```json
    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]
```

<span data-ttu-id="b62c5-200">The previous example showed a simple equality query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-200">The previous example showed a simple equality query.</span></span> <span data-ttu-id="b62c5-201">The SQL API also supports a variety of scalar expressions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-201">The SQL API also supports a variety of scalar expressions.</span></span> <span data-ttu-id="b62c5-202">The most commonly used are binary and unary expressions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-202">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="b62c5-203">Property references from the source JSON object are also valid expressions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-203">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="b62c5-204">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span><span class="sxs-lookup"><span data-stu-id="b62c5-204">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

|<span data-ttu-id="b62c5-205">**Operator type**</span><span class="sxs-lookup"><span data-stu-id="b62c5-205">**Operator type**</span></span>  |<span data-ttu-id="b62c5-206">**Values**</span><span class="sxs-lookup"><span data-stu-id="b62c5-206">**Values**</span></span>  |
|---------|---------|
|<span data-ttu-id="b62c5-207">Arithmetic</span><span class="sxs-lookup"><span data-stu-id="b62c5-207">Arithmetic</span></span>    |   <span data-ttu-id="b62c5-208">+,-,\*,/,%</span><span class="sxs-lookup"><span data-stu-id="b62c5-208">+,-,\*,/,%</span></span>   |
|<span data-ttu-id="b62c5-209">Bitwise</span><span class="sxs-lookup"><span data-stu-id="b62c5-209">Bitwise</span></span>  |   |<span data-ttu-id="b62c5-210">, &, ^, <<, >>, >>> (zero-fill right shift)</span><span class="sxs-lookup"><span data-stu-id="b62c5-210">, &, ^, <<, >>, >>> (zero-fill right shift)</span></span>      |
|<span data-ttu-id="b62c5-211">Logical</span><span class="sxs-lookup"><span data-stu-id="b62c5-211">Logical</span></span>   |   <span data-ttu-id="b62c5-212">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="b62c5-212">AND, OR, NOT</span></span>      |
|<span data-ttu-id="b62c5-213">Comparison</span><span class="sxs-lookup"><span data-stu-id="b62c5-213">Comparison</span></span>   |    <span data-ttu-id="b62c5-214">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="b62c5-214">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span>     |
|<span data-ttu-id="b62c5-215">String</span><span class="sxs-lookup"><span data-stu-id="b62c5-215">String</span></span>  |  || <span data-ttu-id="b62c5-216">(concatenate)</span><span class="sxs-lookup"><span data-stu-id="b62c5-216">(concatenate)</span></span>       |

<span data-ttu-id="b62c5-217">Let’s take a look at some queries using binary operators.</span><span class="sxs-lookup"><span data-stu-id="b62c5-217">Let’s take a look at some queries using binary operators.</span></span>

```sql
    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5
```

<span data-ttu-id="b62c5-218">The unary operators +,-, ~, and NOT are also supported, and can be used inside queries as shown in the following examples:</span><span class="sxs-lookup"><span data-stu-id="b62c5-218">The unary operators +,-, ~, and NOT are also supported, and can be used inside queries as shown in the following examples:</span></span>

```sql
    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5
```

<span data-ttu-id="b62c5-219">In addition to binary and unary operators, property references are also allowed.</span><span class="sxs-lookup"><span data-stu-id="b62c5-219">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="b62c5-220">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-220">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="b62c5-221">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-221">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="b62c5-222">Equality and comparison operators</span><span class="sxs-lookup"><span data-stu-id="b62c5-222">Equality and comparison operators</span></span>
<span data-ttu-id="b62c5-223">The following table shows the result of equality comparisons in the SQL API between any two JSON types.</span><span class="sxs-lookup"><span data-stu-id="b62c5-223">The following table shows the result of equality comparisons in the SQL API between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-224">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-224">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-225">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-225">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-226">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-226">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-227">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-227">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-228">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-228">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-229">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-229">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-230">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-230">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="b62c5-231">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-231">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-232">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-232">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-233">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-233">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-234">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-234">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-235">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-235">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-236">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-236">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-237">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-237">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-238">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-238">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-239">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-240">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-240">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-241">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="b62c5-242">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-242">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-245">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-246">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-246">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-247">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-248">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-248">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-250">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="b62c5-251">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-251">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-253">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-254">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-254">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-255">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-256">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-256">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-257">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-257">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-259">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="b62c5-260">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-260">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-261">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-262">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-262">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-263">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-264">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-264">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-265">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-266">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-266">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-268">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="b62c5-269">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-269">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-270">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-270">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-271">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-272">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-272">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-274">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-275">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-275">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-277">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="b62c5-278">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-278">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-279">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="b62c5-280">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-280">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="b62c5-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-283">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-284">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-284">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-285">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="b62c5-286">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-286">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="b62c5-287">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="b62c5-287">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="b62c5-288">For other comparison operators such as >, >=, !=, <, and <=, the following rules apply:</span><span class="sxs-lookup"><span data-stu-id="b62c5-288">For other comparison operators such as >, >=, !=, <, and <=, the following rules apply:</span></span>   

* <span data-ttu-id="b62c5-289">Comparison across types results in Undefined.</span><span class="sxs-lookup"><span data-stu-id="b62c5-289">Comparison across types results in Undefined.</span></span>  
* <span data-ttu-id="b62c5-290">Comparison between two objects or two arrays results in Undefined.</span><span class="sxs-lookup"><span data-stu-id="b62c5-290">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="b62c5-291">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span><span class="sxs-lookup"><span data-stu-id="b62c5-291">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

## <a name="between-keyword"></a><span data-ttu-id="b62c5-292">BETWEEN keyword</span><span class="sxs-lookup"><span data-stu-id="b62c5-292">BETWEEN keyword</span></span>
<span data-ttu-id="b62c5-293">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="b62c5-293">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="b62c5-294">BETWEEN can be used against strings or numbers.</span><span class="sxs-lookup"><span data-stu-id="b62c5-294">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="b62c5-295">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span><span class="sxs-lookup"><span data-stu-id="b62c5-295">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

```sql
    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5
```

<span data-ttu-id="b62c5-296">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span><span class="sxs-lookup"><span data-stu-id="b62c5-296">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

```sql
    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c
```

<span data-ttu-id="b62c5-297">The main difference between using BETWEEN in the SQL API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span><span class="sxs-lookup"><span data-stu-id="b62c5-297">The main difference between using BETWEEN in the SQL API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="b62c5-298">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span><span class="sxs-lookup"><span data-stu-id="b62c5-298">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="b62c5-299">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span><span class="sxs-lookup"><span data-stu-id="b62c5-299">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="b62c5-300">Logical (AND, OR and NOT) operators</span><span class="sxs-lookup"><span data-stu-id="b62c5-300">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="b62c5-301">Logical operators operate on Boolean values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-301">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="b62c5-302">The logical truth tables for these operators are shown in the following tables.</span><span class="sxs-lookup"><span data-stu-id="b62c5-302">The logical truth tables for these operators are shown in the following tables.</span></span>

<span data-ttu-id="b62c5-303">**OR operator**</span><span class="sxs-lookup"><span data-stu-id="b62c5-303">**OR operator**</span></span>

| <span data-ttu-id="b62c5-304">OR</span><span class="sxs-lookup"><span data-stu-id="b62c5-304">OR</span></span> | <span data-ttu-id="b62c5-305">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-305">True</span></span> | <span data-ttu-id="b62c5-306">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-306">False</span></span> | <span data-ttu-id="b62c5-307">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-307">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b62c5-308">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-308">True</span></span> |<span data-ttu-id="b62c5-309">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-309">True</span></span> |<span data-ttu-id="b62c5-310">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-310">True</span></span> |<span data-ttu-id="b62c5-311">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-311">True</span></span> |
| <span data-ttu-id="b62c5-312">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-312">False</span></span> |<span data-ttu-id="b62c5-313">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-313">True</span></span> |<span data-ttu-id="b62c5-314">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-314">False</span></span> |<span data-ttu-id="b62c5-315">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-315">Undefined</span></span> |
| <span data-ttu-id="b62c5-316">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-316">Undefined</span></span> |<span data-ttu-id="b62c5-317">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-317">True</span></span> |<span data-ttu-id="b62c5-318">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-318">Undefined</span></span> |<span data-ttu-id="b62c5-319">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-319">Undefined</span></span> |

<span data-ttu-id="b62c5-320">**AND operator**</span><span class="sxs-lookup"><span data-stu-id="b62c5-320">**AND operator**</span></span>

| <span data-ttu-id="b62c5-321">AND</span><span class="sxs-lookup"><span data-stu-id="b62c5-321">AND</span></span> | <span data-ttu-id="b62c5-322">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-322">True</span></span> | <span data-ttu-id="b62c5-323">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-323">False</span></span> | <span data-ttu-id="b62c5-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-324">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b62c5-325">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-325">True</span></span> |<span data-ttu-id="b62c5-326">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-326">True</span></span> |<span data-ttu-id="b62c5-327">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-327">False</span></span> |<span data-ttu-id="b62c5-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-328">Undefined</span></span> |
| <span data-ttu-id="b62c5-329">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-329">False</span></span> |<span data-ttu-id="b62c5-330">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-330">False</span></span> |<span data-ttu-id="b62c5-331">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-331">False</span></span> |<span data-ttu-id="b62c5-332">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-332">False</span></span> |
| <span data-ttu-id="b62c5-333">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-333">Undefined</span></span> |<span data-ttu-id="b62c5-334">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-334">Undefined</span></span> |<span data-ttu-id="b62c5-335">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-335">False</span></span> |<span data-ttu-id="b62c5-336">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-336">Undefined</span></span> |

<span data-ttu-id="b62c5-337">**NOT operator**</span><span class="sxs-lookup"><span data-stu-id="b62c5-337">**NOT operator**</span></span>

| <span data-ttu-id="b62c5-338">NOT</span><span class="sxs-lookup"><span data-stu-id="b62c5-338">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="b62c5-339">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-339">True</span></span> |<span data-ttu-id="b62c5-340">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-340">False</span></span> |
| <span data-ttu-id="b62c5-341">False</span><span class="sxs-lookup"><span data-stu-id="b62c5-341">False</span></span> |<span data-ttu-id="b62c5-342">True</span><span class="sxs-lookup"><span data-stu-id="b62c5-342">True</span></span> |
| <span data-ttu-id="b62c5-343">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-343">Undefined</span></span> |<span data-ttu-id="b62c5-344">Undefined</span><span class="sxs-lookup"><span data-stu-id="b62c5-344">Undefined</span></span> |

## <a name="in-keyword"></a><span data-ttu-id="b62c5-345">IN keyword</span><span class="sxs-lookup"><span data-stu-id="b62c5-345">IN keyword</span></span>

<span data-ttu-id="b62c5-346">The IN keyword can be used to check whether a specified value matches any value in a list.</span><span class="sxs-lookup"><span data-stu-id="b62c5-346">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="b62c5-347">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="b62c5-347">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

```sql
    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')
```

<span data-ttu-id="b62c5-348">This example returns all documents where the state is any of the specified values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-348">This example returns all documents where the state is any of the specified values.</span></span>

```sql
    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")
```

## <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="b62c5-349">Ternary (?) and Coalesce (??) operators</span><span class="sxs-lookup"><span data-stu-id="b62c5-349">Ternary (?) and Coalesce (??) operators</span></span>

<span data-ttu-id="b62c5-350">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b62c5-350">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> <span data-ttu-id="b62c5-351">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span><span class="sxs-lookup"><span data-stu-id="b62c5-351">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="b62c5-352">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span><span class="sxs-lookup"><span data-stu-id="b62c5-352">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

```sql
     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c
```

<span data-ttu-id="b62c5-353">You can also nest the calls to the operator like in the query below.</span><span class="sxs-lookup"><span data-stu-id="b62c5-353">You can also nest the calls to the operator like in the query below.</span></span>

```sql
    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c
```

<span data-ttu-id="b62c5-354">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span><span class="sxs-lookup"><span data-stu-id="b62c5-354">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="b62c5-355">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="b62c5-355">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="b62c5-356">is defined) in a document.</span><span class="sxs-lookup"><span data-stu-id="b62c5-356">is defined) in a document.</span></span> <span data-ttu-id="b62c5-357">This is useful when querying against semi-structured or data of mixed types.</span><span class="sxs-lookup"><span data-stu-id="b62c5-357">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="b62c5-358">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span><span class="sxs-lookup"><span data-stu-id="b62c5-358">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

```sql
    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f
```

## <a id="EscapingReservedKeywords"></a><span data-ttu-id="b62c5-359">Quoted property accessor</span><span class="sxs-lookup"><span data-stu-id="b62c5-359">Quoted property accessor</span></span>
<span data-ttu-id="b62c5-360">You can also access properties using the quoted property operator `[]`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-360">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="b62c5-361">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span><span class="sxs-lookup"><span data-stu-id="b62c5-361">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="b62c5-362">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span><span class="sxs-lookup"><span data-stu-id="b62c5-362">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

```sql
    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"
```

## <a name="aliasing"></a><span data-ttu-id="b62c5-363">Aliasing</span><span class="sxs-lookup"><span data-stu-id="b62c5-363">Aliasing</span></span>

<span data-ttu-id="b62c5-364">Now let's extend the example above with explicit aliasing of values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-364">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="b62c5-365">AS is the keyword used for aliasing.</span><span class="sxs-lookup"><span data-stu-id="b62c5-365">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="b62c5-366">It's optional as shown while projecting the second value as `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-366">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="b62c5-367">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-367">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="b62c5-368">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-368">**Query**</span></span>
```sql
    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-369">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-369">**Results**</span></span>

```json
    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]
```

## <a name="scalar-expressions"></a><span data-ttu-id="b62c5-370">Scalar expressions</span><span class="sxs-lookup"><span data-stu-id="b62c5-370">Scalar expressions</span></span>
<span data-ttu-id="b62c5-371">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-371">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="b62c5-372">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-372">**Query**</span></span>

```sql
    SELECT "Hello World"
```

<span data-ttu-id="b62c5-373">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-373">**Results**</span></span>

```json
    [{
      "$1": "Hello World"
    }]
```

<span data-ttu-id="b62c5-374">Here's a more complex example that uses a scalar expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-374">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="b62c5-375">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-375">**Query**</span></span>

```sql
    SELECT ((2 + 11 % 7)-2)/3    
```

<span data-ttu-id="b62c5-376">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-376">**Results**</span></span>

```json
    [{
      "$1": 1.33333
    }]
```

<span data-ttu-id="b62c5-377">In the following example, the result of the scalar expression is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="b62c5-377">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="b62c5-378">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-378">**Query**</span></span>

```sql
    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    
```

<span data-ttu-id="b62c5-379">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-379">**Results**</span></span>

```json
    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]
```

## <a name="object-and-array-creation"></a><span data-ttu-id="b62c5-380">Object and array creation</span><span class="sxs-lookup"><span data-stu-id="b62c5-380">Object and array creation</span></span>
<span data-ttu-id="b62c5-381">Another key feature of the SQL API is array/object creation.</span><span class="sxs-lookup"><span data-stu-id="b62c5-381">Another key feature of the SQL API is array/object creation.</span></span> <span data-ttu-id="b62c5-382">In the previous example, note that we created a new JSON object.</span><span class="sxs-lookup"><span data-stu-id="b62c5-382">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="b62c5-383">Similarly, one can also construct arrays as shown in the following examples:</span><span class="sxs-lookup"><span data-stu-id="b62c5-383">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="b62c5-384">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-384">**Query**</span></span>

```sql
    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    
```

<span data-ttu-id="b62c5-385">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-385">**Results**</span></span>  

```json
    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]
```

## <a id="ValueKeyword"></a><span data-ttu-id="b62c5-386">VALUE keyword</span><span class="sxs-lookup"><span data-stu-id="b62c5-386">VALUE keyword</span></span>
<span data-ttu-id="b62c5-387">The **VALUE** keyword provides a way to return JSON value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-387">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="b62c5-388">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-388">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="b62c5-389">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-389">**Query**</span></span>

```sql
    SELECT VALUE "Hello World"
```

<span data-ttu-id="b62c5-390">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-390">**Results**</span></span>

```json
    [
      "Hello World"
    ]
```

<span data-ttu-id="b62c5-391">The following query returns the JSON value without the `"address"` label in the results.</span><span class="sxs-lookup"><span data-stu-id="b62c5-391">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="b62c5-392">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-392">**Query**</span></span>

```sql
    SELECT VALUE f.address
    FROM Families f    
```

<span data-ttu-id="b62c5-393">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-393">**Results**</span></span>  

```json
    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]
```

<span data-ttu-id="b62c5-394">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span><span class="sxs-lookup"><span data-stu-id="b62c5-394">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="b62c5-395">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-395">**Query**</span></span>

```sql
    SELECT VALUE f.address.state
    FROM Families f    
```

<span data-ttu-id="b62c5-396">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-396">**Results**</span></span>

```json
    [
      "WA",
      "NY"
    ]
```

## <a name="-operator"></a><span data-ttu-id="b62c5-397">\* Operator</span><span class="sxs-lookup"><span data-stu-id="b62c5-397">\* Operator</span></span>
<span data-ttu-id="b62c5-398">The special operator (\*) is supported to project the document as-is.</span><span class="sxs-lookup"><span data-stu-id="b62c5-398">The special operator (\*) is supported to project the document as-is.</span></span> <span data-ttu-id="b62c5-399">When used, it must be the only projected field.</span><span class="sxs-lookup"><span data-stu-id="b62c5-399">When used, it must be the only projected field.</span></span> <span data-ttu-id="b62c5-400">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span><span class="sxs-lookup"><span data-stu-id="b62c5-400">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="b62c5-401">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-401">**Query**</span></span>

```sql
    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"
```

<span data-ttu-id="b62c5-402">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-402">**Results**</span></span>

```json
    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]
```

## <a id="TopKeyword"></a><span data-ttu-id="b62c5-403">TOP Operator</span><span class="sxs-lookup"><span data-stu-id="b62c5-403">TOP Operator</span></span>
<span data-ttu-id="b62c5-404">The TOP keyword can be used to limit the number of values from a query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-404">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="b62c5-405">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span><span class="sxs-lookup"><span data-stu-id="b62c5-405">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="b62c5-406">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span><span class="sxs-lookup"><span data-stu-id="b62c5-406">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="b62c5-407">This is the only way to predictably indicate which rows are affected by TOP.</span><span class="sxs-lookup"><span data-stu-id="b62c5-407">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="b62c5-408">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-408">**Query**</span></span>

```sql
    SELECT TOP 1 * 
    FROM Families f 
```

<span data-ttu-id="b62c5-409">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-409">**Results**</span></span>

```json
    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]
```

<span data-ttu-id="b62c5-410">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-410">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="b62c5-411">For more details, please see parameterized queries below.</span><span class="sxs-lookup"><span data-stu-id="b62c5-411">For more details, please see parameterized queries below.</span></span>

## <a id="Aggregates"></a><span data-ttu-id="b62c5-412">Aggregate Functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-412">Aggregate Functions</span></span>
<span data-ttu-id="b62c5-413">You can also perform aggregations in the `SELECT` clause.</span><span class="sxs-lookup"><span data-stu-id="b62c5-413">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="b62c5-414">Aggregate functions perform a calculation on a set of values and return a single value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-414">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="b62c5-415">For example, the following query returns the count of family documents within the collection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-415">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="b62c5-416">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-416">**Query**</span></span>

```sql
    SELECT COUNT(1) 
    FROM Families f 
```

<span data-ttu-id="b62c5-417">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-417">**Results**</span></span>

```json
    [{
        "$1": 2
    }]
```

<span data-ttu-id="b62c5-418">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span><span class="sxs-lookup"><span data-stu-id="b62c5-418">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="b62c5-419">For example, the following query returns the count of values as a single number:</span><span class="sxs-lookup"><span data-stu-id="b62c5-419">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="b62c5-420">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-420">**Query**</span></span>

```sql
    SELECT VALUE COUNT(1) 
    FROM Families f 
```

<span data-ttu-id="b62c5-421">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-421">**Results**</span></span>

```json
    [ 2 ]
```

<span data-ttu-id="b62c5-422">You can also perform aggregates in combination with filters.</span><span class="sxs-lookup"><span data-stu-id="b62c5-422">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="b62c5-423">For example, the following query returns the count of documents with the address in the state of Washington.</span><span class="sxs-lookup"><span data-stu-id="b62c5-423">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="b62c5-424">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-424">**Query**</span></span>

```sql
    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 
```

<span data-ttu-id="b62c5-425">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-425">**Results**</span></span>

```json
    [ 1 ]
```

<span data-ttu-id="b62c5-426">The following table shows the list of supported aggregate functions in the SQL API.</span><span class="sxs-lookup"><span data-stu-id="b62c5-426">The following table shows the list of supported aggregate functions in the SQL API.</span></span> <span data-ttu-id="b62c5-427">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span><span class="sxs-lookup"><span data-stu-id="b62c5-427">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="b62c5-428">Usage</span><span class="sxs-lookup"><span data-stu-id="b62c5-428">Usage</span></span> | <span data-ttu-id="b62c5-429">Description</span><span class="sxs-lookup"><span data-stu-id="b62c5-429">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="b62c5-430">COUNT</span><span class="sxs-lookup"><span data-stu-id="b62c5-430">COUNT</span></span> | <span data-ttu-id="b62c5-431">Returns the number of items in the expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-431">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="b62c5-432">SUM</span><span class="sxs-lookup"><span data-stu-id="b62c5-432">SUM</span></span>   | <span data-ttu-id="b62c5-433">Returns the sum of all the values in the expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-433">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="b62c5-434">MIN</span><span class="sxs-lookup"><span data-stu-id="b62c5-434">MIN</span></span>   | <span data-ttu-id="b62c5-435">Returns the minimum value in the expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-435">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="b62c5-436">MAX</span><span class="sxs-lookup"><span data-stu-id="b62c5-436">MAX</span></span>   | <span data-ttu-id="b62c5-437">Returns the maximum value in the expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-437">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="b62c5-438">AVG</span><span class="sxs-lookup"><span data-stu-id="b62c5-438">AVG</span></span>   | <span data-ttu-id="b62c5-439">Returns the average of the values in the expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-439">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="b62c5-440">Aggregates can also be performed over the results of an array iteration.</span><span class="sxs-lookup"><span data-stu-id="b62c5-440">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="b62c5-441">For more information, see [Array Iteration in Queries](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="b62c5-441">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="b62c5-442">When using the Azure portal's Data Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span><span class="sxs-lookup"><span data-stu-id="b62c5-442">When using the Azure portal's Data Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="b62c5-443">The SDKs produces a single cumulative value across all pages.</span><span class="sxs-lookup"><span data-stu-id="b62c5-443">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="b62c5-444">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span><span class="sxs-lookup"><span data-stu-id="b62c5-444">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <a id="OrderByClause"></a><span data-ttu-id="b62c5-445">ORDER BY clause</span><span class="sxs-lookup"><span data-stu-id="b62c5-445">ORDER BY clause</span></span>
<span data-ttu-id="b62c5-446">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span><span class="sxs-lookup"><span data-stu-id="b62c5-446">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="b62c5-447">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span><span class="sxs-lookup"><span data-stu-id="b62c5-447">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="b62c5-448">For example, here's a query that retrieves families in order of the resident city's name.</span><span class="sxs-lookup"><span data-stu-id="b62c5-448">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="b62c5-449">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-449">**Query**</span></span>

```sql
    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city
```

<span data-ttu-id="b62c5-450">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-450">**Results**</span></span>

```json
    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]
```

<span data-ttu-id="b62c5-451">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span><span class="sxs-lookup"><span data-stu-id="b62c5-451">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="b62c5-452">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-452">**Query**</span></span>

```sql
    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC
```

<span data-ttu-id="b62c5-453">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-453">**Results**</span></span>

```json
    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]
```

## <a id="Advanced"></a><span data-ttu-id="b62c5-454">Advanced database concepts and SQL queries</span><span class="sxs-lookup"><span data-stu-id="b62c5-454">Advanced database concepts and SQL queries</span></span>

### <a id="Iteration"></a><span data-ttu-id="b62c5-455">Iteration</span><span class="sxs-lookup"><span data-stu-id="b62c5-455">Iteration</span></span>
<span data-ttu-id="b62c5-456">A new construct was added via the **IN** keyword in the SQL API to provide support for iterating over JSON arrays.</span><span class="sxs-lookup"><span data-stu-id="b62c5-456">A new construct was added via the **IN** keyword in the SQL API to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="b62c5-457">The FROM source provides support for iteration.</span><span class="sxs-lookup"><span data-stu-id="b62c5-457">The FROM source provides support for iteration.</span></span> <span data-ttu-id="b62c5-458">Let's start with the following example:</span><span class="sxs-lookup"><span data-stu-id="b62c5-458">Let's start with the following example:</span></span>

<span data-ttu-id="b62c5-459">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-459">**Query**</span></span>

```sql
    SELECT * 
    FROM Families.children
```

<span data-ttu-id="b62c5-460">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-460">**Results**</span></span>  

```json
    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]
```

<span data-ttu-id="b62c5-461">Now let's look at another query that performs iteration over children in the collection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-461">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="b62c5-462">Note the difference in the output array.</span><span class="sxs-lookup"><span data-stu-id="b62c5-462">Note the difference in the output array.</span></span> <span data-ttu-id="b62c5-463">This example splits `children` and flattens the results into a single array.</span><span class="sxs-lookup"><span data-stu-id="b62c5-463">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="b62c5-464">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-464">**Query**</span></span>

```sql
    SELECT * 
    FROM c IN Families.children
```

<span data-ttu-id="b62c5-465">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-465">**Results**</span></span>  

```json
    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]
```

<span data-ttu-id="b62c5-466">This can be further used to filter on each individual entry of the array as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b62c5-466">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="b62c5-467">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-467">**Query**</span></span>

```sql
    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8
```

<span data-ttu-id="b62c5-468">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-468">**Results**</span></span>  

```json
    [{
      "givenName": "Lisa"
    }]
```

<span data-ttu-id="b62c5-469">You can also perform aggregation over the result of array iteration.</span><span class="sxs-lookup"><span data-stu-id="b62c5-469">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="b62c5-470">For example, the following query counts the number of children among all families.</span><span class="sxs-lookup"><span data-stu-id="b62c5-470">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="b62c5-471">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-471">**Query**</span></span>

```sql
    SELECT COUNT(child) 
    FROM child IN Families.children
```

<span data-ttu-id="b62c5-472">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-472">**Results**</span></span>  

```json
    [
      { 
        "$1": 3
      }
    ]
```

### <a id="Joins"></a><span data-ttu-id="b62c5-473">Joins</span><span class="sxs-lookup"><span data-stu-id="b62c5-473">Joins</span></span>
<span data-ttu-id="b62c5-474">In a relational database, the need to join across tables is important.</span><span class="sxs-lookup"><span data-stu-id="b62c5-474">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="b62c5-475">It's the logical corollary to designing normalized schemas.</span><span class="sxs-lookup"><span data-stu-id="b62c5-475">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="b62c5-476">Contrary to this, the SQL API deals with the denormalized data model of schema-free documents.</span><span class="sxs-lookup"><span data-stu-id="b62c5-476">Contrary to this, the SQL API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="b62c5-477">This is the logical equivalent of a "self-join".</span><span class="sxs-lookup"><span data-stu-id="b62c5-477">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="b62c5-478">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="b62c5-478">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="b62c5-479">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span><span class="sxs-lookup"><span data-stu-id="b62c5-479">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="b62c5-480">Each tuple has values produced by iterating all collection aliases over their respective sets.</span><span class="sxs-lookup"><span data-stu-id="b62c5-480">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="b62c5-481">In other words, this is a full cross product of the sets participating in the join.</span><span class="sxs-lookup"><span data-stu-id="b62c5-481">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="b62c5-482">The following examples show how the JOIN clause works.</span><span class="sxs-lookup"><span data-stu-id="b62c5-482">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="b62c5-483">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span><span class="sxs-lookup"><span data-stu-id="b62c5-483">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="b62c5-484">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-484">**Query**</span></span>

```sql
    SELECT f.id
    FROM Families f
    JOIN f.NonExistent
```

<span data-ttu-id="b62c5-485">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-485">**Results**</span></span>  

```json
    [{
    }]
```

<span data-ttu-id="b62c5-486">In the following example, the join is between the document root and the `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="b62c5-486">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="b62c5-487">It's a cross product between two JSON objects.</span><span class="sxs-lookup"><span data-stu-id="b62c5-487">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="b62c5-488">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span><span class="sxs-lookup"><span data-stu-id="b62c5-488">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="b62c5-489">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span><span class="sxs-lookup"><span data-stu-id="b62c5-489">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="b62c5-490">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-490">**Query**</span></span>

```sql
    SELECT f.id
    FROM Families f
    JOIN f.children
```

<span data-ttu-id="b62c5-491">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-491">**Results**</span></span>

```json
    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]
```

<span data-ttu-id="b62c5-492">The following example shows a more conventional join:</span><span class="sxs-lookup"><span data-stu-id="b62c5-492">The following example shows a more conventional join:</span></span>

<span data-ttu-id="b62c5-493">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-493">**Query**</span></span>

```sql
    SELECT f.id
    FROM Families f
    JOIN c IN f.children 
```

<span data-ttu-id="b62c5-494">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-494">**Results**</span></span>

```json
    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]
```

<span data-ttu-id="b62c5-495">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span><span class="sxs-lookup"><span data-stu-id="b62c5-495">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="b62c5-496">So, the flow in this case is as follows:</span><span class="sxs-lookup"><span data-stu-id="b62c5-496">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="b62c5-497">Expand each child element **c** in the array.</span><span class="sxs-lookup"><span data-stu-id="b62c5-497">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="b62c5-498">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span><span class="sxs-lookup"><span data-stu-id="b62c5-498">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="b62c5-499">Finally, project the root object **f** name property alone.</span><span class="sxs-lookup"><span data-stu-id="b62c5-499">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="b62c5-500">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span><span class="sxs-lookup"><span data-stu-id="b62c5-500">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="b62c5-501">The second document (`WakefieldFamily`) contains two children.</span><span class="sxs-lookup"><span data-stu-id="b62c5-501">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="b62c5-502">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span><span class="sxs-lookup"><span data-stu-id="b62c5-502">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="b62c5-503">The root fields in both these documents are the same, just as you would expect in a cross product.</span><span class="sxs-lookup"><span data-stu-id="b62c5-503">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="b62c5-504">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span><span class="sxs-lookup"><span data-stu-id="b62c5-504">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="b62c5-505">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span><span class="sxs-lookup"><span data-stu-id="b62c5-505">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="b62c5-506">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-506">**Query**</span></span>

```sql
    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
```

<span data-ttu-id="b62c5-507">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-507">**Results**</span></span>

```json
    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]
```

<span data-ttu-id="b62c5-508">This example is a natural extension of the preceding example, and performs a double join.</span><span class="sxs-lookup"><span data-stu-id="b62c5-508">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="b62c5-509">So, the cross product can be viewed as the following pseudo-code:</span><span class="sxs-lookup"><span data-stu-id="b62c5-509">So, the cross product can be viewed as the following pseudo-code:</span></span>

```
    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }
```

<span data-ttu-id="b62c5-510">`AndersenFamily` has one child who has one pet.</span><span class="sxs-lookup"><span data-stu-id="b62c5-510">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="b62c5-511">So, the cross product yields one row (1\*1\*1) from this family.</span><span class="sxs-lookup"><span data-stu-id="b62c5-511">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="b62c5-512">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span><span class="sxs-lookup"><span data-stu-id="b62c5-512">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="b62c5-513">Jesse has two pets though.</span><span class="sxs-lookup"><span data-stu-id="b62c5-513">Jesse has two pets though.</span></span> <span data-ttu-id="b62c5-514">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span><span class="sxs-lookup"><span data-stu-id="b62c5-514">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="b62c5-515">In the next example, there is an additional filter on `pet`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-515">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="b62c5-516">This excludes all the tuples where the pet name is not "Shadow".</span><span class="sxs-lookup"><span data-stu-id="b62c5-516">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="b62c5-517">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span><span class="sxs-lookup"><span data-stu-id="b62c5-517">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="b62c5-518">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-518">**Query**</span></span>

```sql
    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"
```

<span data-ttu-id="b62c5-519">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-519">**Results**</span></span>

```json
    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]
```

## <a id="JavaScriptIntegration"></a><span data-ttu-id="b62c5-520">JavaScript integration</span><span class="sxs-lookup"><span data-stu-id="b62c5-520">JavaScript integration</span></span>
<span data-ttu-id="b62c5-521">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="b62c5-521">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="b62c5-522">This allows for both:</span><span class="sxs-lookup"><span data-stu-id="b62c5-522">This allows for both:</span></span>

* <span data-ttu-id="b62c5-523">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span><span class="sxs-lookup"><span data-stu-id="b62c5-523">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="b62c5-524">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-524">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="b62c5-525">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span><span class="sxs-lookup"><span data-stu-id="b62c5-525">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <a id="UserDefinedFunctions"></a><span data-ttu-id="b62c5-526">User-Defined Functions (UDFs)</span><span class="sxs-lookup"><span data-stu-id="b62c5-526">User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="b62c5-527">Along with the types already defined in this article, the SQL API provides support for User Defined Functions (UDF).</span><span class="sxs-lookup"><span data-stu-id="b62c5-527">Along with the types already defined in this article, the SQL API provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="b62c5-528">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span><span class="sxs-lookup"><span data-stu-id="b62c5-528">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="b62c5-529">Each of these arguments is checked for being legal JSON values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-529">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="b62c5-530">The SQL syntax is extended to support custom application logic using these User-Defined Functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-530">The SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="b62c5-531">UDFs can be registered with SQL API and then be referenced as part of a SQL query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-531">UDFs can be registered with SQL API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="b62c5-532">In fact, the UDFs are exquisitely designed to be invoked by queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-532">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="b62c5-533">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span><span class="sxs-lookup"><span data-stu-id="b62c5-533">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="b62c5-534">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="b62c5-534">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="b62c5-535">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span><span class="sxs-lookup"><span data-stu-id="b62c5-535">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="b62c5-536">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-536">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

```javascript
       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  
```

<span data-ttu-id="b62c5-537">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-537">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="b62c5-538">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span><span class="sxs-lookup"><span data-stu-id="b62c5-538">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="b62c5-539">We can now use this UDF in a query in a projection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-539">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="b62c5-540">UDFs must be qualified with the case-sensitive prefix "udf."</span><span class="sxs-lookup"><span data-stu-id="b62c5-540">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="b62c5-541">when called from within queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-541">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="b62c5-542">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span><span class="sxs-lookup"><span data-stu-id="b62c5-542">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="b62c5-543">prefix like SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="b62c5-543">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="b62c5-544">This calling pattern has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="b62c5-544">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="b62c5-545">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-545">**Query**</span></span>

```sql
    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families
```

<span data-ttu-id="b62c5-546">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-546">**Results**</span></span>

```json
    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]
```

<span data-ttu-id="b62c5-547">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span><span class="sxs-lookup"><span data-stu-id="b62c5-547">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="b62c5-548">prefix:</span><span class="sxs-lookup"><span data-stu-id="b62c5-548">prefix:</span></span>

<span data-ttu-id="b62c5-549">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-549">**Query**</span></span>

```sql
    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")
```

<span data-ttu-id="b62c5-550">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-550">**Results**</span></span>

```json
    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]
```

<span data-ttu-id="b62c5-551">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span><span class="sxs-lookup"><span data-stu-id="b62c5-551">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="b62c5-552">To expand on the power of UDFs, let's look at another example with conditional logic:</span><span class="sxs-lookup"><span data-stu-id="b62c5-552">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

```javascript
       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);
```

<span data-ttu-id="b62c5-553">Below is an example that exercises the UDF.</span><span class="sxs-lookup"><span data-stu-id="b62c5-553">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="b62c5-554">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-554">**Query**</span></span>

```sql
    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    
```

<span data-ttu-id="b62c5-555">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-555">**Results**</span></span>

```json
     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]
```

<span data-ttu-id="b62c5-556">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the SQL API to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span><span class="sxs-lookup"><span data-stu-id="b62c5-556">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the SQL API to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="b62c5-557">The SQL API provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span><span class="sxs-lookup"><span data-stu-id="b62c5-557">The SQL API provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="b62c5-558">The result is incorporated in the overall execution pipeline seamlessly.</span><span class="sxs-lookup"><span data-stu-id="b62c5-558">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="b62c5-559">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span><span class="sxs-lookup"><span data-stu-id="b62c5-559">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="b62c5-560">Similarly if the result of the UDF is undefined, it's not included in the result.</span><span class="sxs-lookup"><span data-stu-id="b62c5-560">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="b62c5-561">In summary, UDFs are great tools to do complex business logic as part of the query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-561">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="b62c5-562">Operator evaluation</span><span class="sxs-lookup"><span data-stu-id="b62c5-562">Operator evaluation</span></span>
<span data-ttu-id="b62c5-563">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span><span class="sxs-lookup"><span data-stu-id="b62c5-563">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="b62c5-564">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span><span class="sxs-lookup"><span data-stu-id="b62c5-564">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="b62c5-565">In the SQL API, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span><span class="sxs-lookup"><span data-stu-id="b62c5-565">In the SQL API, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="b62c5-566">In order to efficiently execute queries, most of the operators have strict type requirements.</span><span class="sxs-lookup"><span data-stu-id="b62c5-566">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="b62c5-567">The SQL API doesn't perform implicit conversions, unlike JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b62c5-567">The SQL API doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="b62c5-568">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span><span class="sxs-lookup"><span data-stu-id="b62c5-568">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="b62c5-569">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span><span class="sxs-lookup"><span data-stu-id="b62c5-569">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="b62c5-570">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span><span class="sxs-lookup"><span data-stu-id="b62c5-570">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="b62c5-571">This choice is crucial for efficient index matching in the SQL API.</span><span class="sxs-lookup"><span data-stu-id="b62c5-571">This choice is crucial for efficient index matching in the SQL API.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="b62c5-572">Parameterized SQL queries</span><span class="sxs-lookup"><span data-stu-id="b62c5-572">Parameterized SQL queries</span></span>
<span data-ttu-id="b62c5-573">Cosmos DB supports queries with parameters expressed with the familiar \@ notation.</span><span class="sxs-lookup"><span data-stu-id="b62c5-573">Cosmos DB supports queries with parameters expressed with the familiar \@ notation.</span></span> <span data-ttu-id="b62c5-574">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-574">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="b62c5-575">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span><span class="sxs-lookup"><span data-stu-id="b62c5-575">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

```sql
    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState
```

<span data-ttu-id="b62c5-576">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span><span class="sxs-lookup"><span data-stu-id="b62c5-576">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

```sql
    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }
```

<span data-ttu-id="b62c5-577">The argument to TOP can be set using parameterized queries like shown below.</span><span class="sxs-lookup"><span data-stu-id="b62c5-577">The argument to TOP can be set using parameterized queries like shown below.</span></span>

```sql
    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }
```

<span data-ttu-id="b62c5-578">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span><span class="sxs-lookup"><span data-stu-id="b62c5-578">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="b62c5-579">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span><span class="sxs-lookup"><span data-stu-id="b62c5-579">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <a id="BuiltinFunctions"></a><span data-ttu-id="b62c5-580">Built-in functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-580">Built-in functions</span></span>
<span data-ttu-id="b62c5-581">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span><span class="sxs-lookup"><span data-stu-id="b62c5-581">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="b62c5-582">Function group</span><span class="sxs-lookup"><span data-stu-id="b62c5-582">Function group</span></span>          | <span data-ttu-id="b62c5-583">Operations</span><span class="sxs-lookup"><span data-stu-id="b62c5-583">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b62c5-584">Mathematical functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-584">Mathematical functions</span></span>  | <span data-ttu-id="b62c5-585">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span><span class="sxs-lookup"><span data-stu-id="b62c5-585">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="b62c5-586">Type checking functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-586">Type checking functions</span></span> | <span data-ttu-id="b62c5-587">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="b62c5-587">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="b62c5-588">String functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-588">String functions</span></span>        | <span data-ttu-id="b62c5-589">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span><span class="sxs-lookup"><span data-stu-id="b62c5-589">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="b62c5-590">Array functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-590">Array functions</span></span>         | <span data-ttu-id="b62c5-591">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="b62c5-591">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="b62c5-592">Spatial functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-592">Spatial functions</span></span>       | <span data-ttu-id="b62c5-593">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="b62c5-593">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="b62c5-594">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span><span class="sxs-lookup"><span data-stu-id="b62c5-594">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="b62c5-595">Mathematical functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-595">Mathematical functions</span></span>
<span data-ttu-id="b62c5-596">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-596">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="b62c5-597">Here’s a table of supported built-in mathematical functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-597">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="b62c5-598">Usage</span><span class="sxs-lookup"><span data-stu-id="b62c5-598">Usage</span></span> | <span data-ttu-id="b62c5-599">Description</span><span class="sxs-lookup"><span data-stu-id="b62c5-599">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b62c5-600">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="b62c5-600">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="b62c5-601">Returns the absolute (positive) value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-601">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-602">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-602">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="b62c5-603">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-603">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-604">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-604">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="b62c5-605">Returns the largest integer less than or equal to the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-605">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-606">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-606">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="b62c5-607">Returns the exponent of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-607">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="b62c5-608">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="b62c5-608">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="b62c5-609">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span><span class="sxs-lookup"><span data-stu-id="b62c5-609">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="b62c5-610">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-610">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="b62c5-611">Returns the base-10 logarithmic value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-611">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-612">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-612">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="b62c5-613">Returns a numeric value, rounded to the closest integer value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-613">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="b62c5-614">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-614">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="b62c5-615">Returns a numeric value, truncated to the closest integer value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-615">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="b62c5-616">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-616">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="b62c5-617">Returns the square root of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-617">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-618">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-618">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="b62c5-619">Returns the square of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-619">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-620">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-620">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="b62c5-621">Returns the power of the specified numeric expression to the value specified.</span><span class="sxs-lookup"><span data-stu-id="b62c5-621">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="b62c5-622">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-622">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="b62c5-623">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-623">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-624">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-624">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="b62c5-625">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span><span class="sxs-lookup"><span data-stu-id="b62c5-625">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="b62c5-626">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-626">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="b62c5-627">Returns the angle, in radians, whose sine is the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-627">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="b62c5-628">This is also called arcsine.</span><span class="sxs-lookup"><span data-stu-id="b62c5-628">This is also called arcsine.</span></span> |
| [<span data-ttu-id="b62c5-629">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-629">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="b62c5-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="b62c5-631">This is also called arctangent.</span><span class="sxs-lookup"><span data-stu-id="b62c5-631">This is also called arctangent.</span></span> |
| [<span data-ttu-id="b62c5-632">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-632">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="b62c5-633">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-633">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="b62c5-634">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-634">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="b62c5-635">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-635">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="b62c5-636">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-636">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="b62c5-637">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-637">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="b62c5-638">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-638">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="b62c5-639">Returns the corresponding angle in degrees for an angle specified in radians.</span><span class="sxs-lookup"><span data-stu-id="b62c5-639">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="b62c5-640">PI ()</span><span class="sxs-lookup"><span data-stu-id="b62c5-640">PI ()</span></span>](#bk_pi) | <span data-ttu-id="b62c5-641">Returns the constant value of PI.</span><span class="sxs-lookup"><span data-stu-id="b62c5-641">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="b62c5-642">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-642">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="b62c5-643">Returns radians when a numeric expression, in degrees, is entered.</span><span class="sxs-lookup"><span data-stu-id="b62c5-643">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="b62c5-644">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-644">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="b62c5-645">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-645">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="b62c5-646">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-646">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="b62c5-647">Returns the tangent of the input expression, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-647">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="b62c5-648">For example, you can now run queries like the following:</span><span class="sxs-lookup"><span data-stu-id="b62c5-648">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="b62c5-649">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-649">**Query**</span></span>

```sql
    SELECT VALUE ABS(-4)
```

<span data-ttu-id="b62c5-650">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-650">**Results**</span></span>

```json
    [4]
```
<span data-ttu-id="b62c5-651">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span><span class="sxs-lookup"><span data-stu-id="b62c5-651">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="b62c5-652">For example, if you have a document where the Size property is missing, or has a non-numeric value like "unknown", then the document is skipped over, instead of returning an error.</span><span class="sxs-lookup"><span data-stu-id="b62c5-652">For example, if you have a document where the Size property is missing, or has a non-numeric value like "unknown", then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="b62c5-653">Type checking functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-653">Type checking functions</span></span>
<span data-ttu-id="b62c5-654">The type checking functions allow you to check the type of an expression within SQL queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-654">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="b62c5-655">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span><span class="sxs-lookup"><span data-stu-id="b62c5-655">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="b62c5-656">Here’s a table of supported built-in type checking functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-656">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="b62c5-657"><strong>Usage</strong></span><span class="sxs-lookup"><span data-stu-id="b62c5-657"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="b62c5-658"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="b62c5-658"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-659"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-659"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-660">Returns a Boolean indicating if the type of the value is an array.</span><span class="sxs-lookup"><span data-stu-id="b62c5-660">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-661"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-661"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-662">Returns a Boolean indicating if the type of the value is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="b62c5-662">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-663"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-663"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-664">Returns a Boolean indicating if the type of the value is null.</span><span class="sxs-lookup"><span data-stu-id="b62c5-664">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-665"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-665"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-666">Returns a Boolean indicating if the type of the value is a number.</span><span class="sxs-lookup"><span data-stu-id="b62c5-666">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-667"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-667"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-668">Returns a Boolean indicating if the type of the value is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="b62c5-668">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-669"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-669"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-670">Returns a Boolean indicating if the type of the value is a string.</span><span class="sxs-lookup"><span data-stu-id="b62c5-670">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-671"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-671"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-672">Returns a Boolean indicating if the property has been assigned a value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-672">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-673"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="b62c5-673"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="b62c5-674">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span><span class="sxs-lookup"><span data-stu-id="b62c5-674">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="b62c5-675">Using these functions, you can now run queries like the following:</span><span class="sxs-lookup"><span data-stu-id="b62c5-675">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="b62c5-676">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-676">**Query**</span></span>

```sql
    SELECT VALUE IS_NUMBER(-4)
```

<span data-ttu-id="b62c5-677">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-677">**Results**</span></span>

```json
    [true]
```

### <a name="string-functions"></a><span data-ttu-id="b62c5-678">String functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-678">String functions</span></span>
<span data-ttu-id="b62c5-679">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-679">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="b62c5-680">Here's a table of built-in string functions:</span><span class="sxs-lookup"><span data-stu-id="b62c5-680">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="b62c5-681">Usage</span><span class="sxs-lookup"><span data-stu-id="b62c5-681">Usage</span></span> | <span data-ttu-id="b62c5-682">Description</span><span class="sxs-lookup"><span data-stu-id="b62c5-682">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="b62c5-683">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-683">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="b62c5-684">Returns the number of characters of the specified string expression</span><span class="sxs-lookup"><span data-stu-id="b62c5-684">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="b62c5-685">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="b62c5-685">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="b62c5-686">Returns a string that is the result of concatenating two or more string values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-686">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="b62c5-687">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-687">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="b62c5-688">Returns part of a string expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-688">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="b62c5-689">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-689">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="b62c5-690">Returns a Boolean indicating whether the first string expression starts with the second</span><span class="sxs-lookup"><span data-stu-id="b62c5-690">Returns a Boolean indicating whether the first string expression starts with the second</span></span> |
| [<span data-ttu-id="b62c5-691">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-691">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="b62c5-692">Returns a Boolean indicating whether the first string expression ends with the second</span><span class="sxs-lookup"><span data-stu-id="b62c5-692">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="b62c5-693">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-693">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="b62c5-694">Returns a Boolean indicating whether the first string expression contains the second.</span><span class="sxs-lookup"><span data-stu-id="b62c5-694">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="b62c5-695">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-695">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="b62c5-696">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="b62c5-696">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="b62c5-697">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-697">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="b62c5-698">Returns the left part of a string with the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="b62c5-698">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="b62c5-699">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-699">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="b62c5-700">Returns the right part of a string with the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="b62c5-700">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="b62c5-701">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-701">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="b62c5-702">Returns a string expression after it removes leading blanks.</span><span class="sxs-lookup"><span data-stu-id="b62c5-702">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="b62c5-703">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-703">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="b62c5-704">Returns a string expression after truncating all trailing blanks.</span><span class="sxs-lookup"><span data-stu-id="b62c5-704">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="b62c5-705">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-705">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="b62c5-706">Returns a string expression after converting uppercase character data to lowercase.</span><span class="sxs-lookup"><span data-stu-id="b62c5-706">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="b62c5-707">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-707">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="b62c5-708">Returns a string expression after converting lowercase character data to uppercase.</span><span class="sxs-lookup"><span data-stu-id="b62c5-708">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="b62c5-709">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-709">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="b62c5-710">Replaces all occurrences of a specified string value with another string value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-710">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="b62c5-711">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-711">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/sql-api-sql-query-reference#bk_replicate) |<span data-ttu-id="b62c5-712">Repeats a string value a specified number of times.</span><span class="sxs-lookup"><span data-stu-id="b62c5-712">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="b62c5-713">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-713">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="b62c5-714">Returns the reverse order of a string value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-714">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="b62c5-715">Using these functions, you can now run queries like the following.</span><span class="sxs-lookup"><span data-stu-id="b62c5-715">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="b62c5-716">For example, you can return the family name in uppercase as follows:</span><span class="sxs-lookup"><span data-stu-id="b62c5-716">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="b62c5-717">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-717">**Query**</span></span>

```sql
    SELECT VALUE UPPER(Families.id)
    FROM Families
```

<span data-ttu-id="b62c5-718">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-718">**Results**</span></span>

```json
    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]
```

<span data-ttu-id="b62c5-719">Or concatenate strings like in this example:</span><span class="sxs-lookup"><span data-stu-id="b62c5-719">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="b62c5-720">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-720">**Query**</span></span>

```sql
    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families
```

<span data-ttu-id="b62c5-721">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-721">**Results**</span></span>

```json
    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]
```

<span data-ttu-id="b62c5-722">String functions can also be used in the WHERE clause to filter results, like in the following example:</span><span class="sxs-lookup"><span data-stu-id="b62c5-722">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="b62c5-723">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-723">**Query**</span></span>

```sql
    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")
```

<span data-ttu-id="b62c5-724">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-724">**Results**</span></span>

```json
    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]
```

### <a name="array-functions"></a><span data-ttu-id="b62c5-725">Array functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-725">Array functions</span></span>
<span data-ttu-id="b62c5-726">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-726">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="b62c5-727">Here's a table of built-in array functions:</span><span class="sxs-lookup"><span data-stu-id="b62c5-727">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="b62c5-728">Usage</span><span class="sxs-lookup"><span data-stu-id="b62c5-728">Usage</span></span> | <span data-ttu-id="b62c5-729">Description</span><span class="sxs-lookup"><span data-stu-id="b62c5-729">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="b62c5-730">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-730">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="b62c5-731">Returns the number of elements of the specified array expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-731">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="b62c5-732">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="b62c5-732">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="b62c5-733">Returns an array that is the result of concatenating two or more array values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-733">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="b62c5-734">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="b62c5-734">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="b62c5-735">Returns a Boolean indicating whether the array contains the specified value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-735">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="b62c5-736">Can specify if the match is full or partial.</span><span class="sxs-lookup"><span data-stu-id="b62c5-736">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="b62c5-737">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="b62c5-737">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="b62c5-738">Returns part of an array expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-738">Returns part of an array expression.</span></span> |

<span data-ttu-id="b62c5-739">Array functions can be used to manipulate arrays within JSON.</span><span class="sxs-lookup"><span data-stu-id="b62c5-739">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="b62c5-740">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="b62c5-740">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="b62c5-741">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-741">**Query**</span></span>

```sql
    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })
```

<span data-ttu-id="b62c5-742">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-742">**Results**</span></span>

```json
    [{
      "id": "WakefieldFamily"
    }]
```

<span data-ttu-id="b62c5-743">You can specify a partial fragment for matching elements within the array.</span><span class="sxs-lookup"><span data-stu-id="b62c5-743">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="b62c5-744">The following query finds all parents with the `givenName` of `Robin`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-744">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="b62c5-745">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-745">**Query**</span></span>

```sql
    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)
```

<span data-ttu-id="b62c5-746">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-746">**Results**</span></span>

```json
    [{
      "id": "WakefieldFamily"
    }]
```

<span data-ttu-id="b62c5-747">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span><span class="sxs-lookup"><span data-stu-id="b62c5-747">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="b62c5-748">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-748">**Query**</span></span>

```sql
    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 
```

<span data-ttu-id="b62c5-749">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-749">**Results**</span></span>

```json
    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]
```

### <a name="spatial-functions"></a><span data-ttu-id="b62c5-750">Spatial functions</span><span class="sxs-lookup"><span data-stu-id="b62c5-750">Spatial functions</span></span>
<span data-ttu-id="b62c5-751">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span><span class="sxs-lookup"><span data-stu-id="b62c5-751">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="b62c5-752"><strong>Usage</strong></span><span class="sxs-lookup"><span data-stu-id="b62c5-752"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="b62c5-753"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="b62c5-753"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-754">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-754">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="b62c5-755">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-755">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-756">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-756">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="b62c5-757">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span><span class="sxs-lookup"><span data-stu-id="b62c5-757">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-758">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="b62c5-758">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="b62c5-759">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="b62c5-759">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-760">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="b62c5-760">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="b62c5-761">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span><span class="sxs-lookup"><span data-stu-id="b62c5-761">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b62c5-762">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="b62c5-762">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="b62c5-763">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-763">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="b62c5-764">Spatial functions can be used to perform proximity queries against spatial data.</span><span class="sxs-lookup"><span data-stu-id="b62c5-764">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="b62c5-765">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span><span class="sxs-lookup"><span data-stu-id="b62c5-765">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="b62c5-766">**Query**</span><span class="sxs-lookup"><span data-stu-id="b62c5-766">**Query**</span></span>

```sql
    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000
```

<span data-ttu-id="b62c5-767">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-767">**Results**</span></span>

```json
    [{
      "id": "WakefieldFamily"
    }]
```

<span data-ttu-id="b62c5-768">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="b62c5-768">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="b62c5-769">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b62c5-769">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="b62c5-770">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span><span class="sxs-lookup"><span data-stu-id="b62c5-770">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <a id="Linq"></a><span data-ttu-id="b62c5-771">LINQ to SQL API</span><span class="sxs-lookup"><span data-stu-id="b62c5-771">LINQ to SQL API</span></span>
<span data-ttu-id="b62c5-772">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span><span class="sxs-lookup"><span data-stu-id="b62c5-772">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="b62c5-773">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-773">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="b62c5-774">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b62c5-774">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="b62c5-775">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-775">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="b62c5-776">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span><span class="sxs-lookup"><span data-stu-id="b62c5-776">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="b62c5-777">The returned results are deserialized into a stream of .NET objects on the client side.</span><span class="sxs-lookup"><span data-stu-id="b62c5-777">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Architecture of supporting LINQ queries using the SQL API - SQL syntax, JSON query language, database concepts, and SQL queries][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="b62c5-779">.NET and JSON mapping</span><span class="sxs-lookup"><span data-stu-id="b62c5-779">.NET and JSON mapping</span></span>
<span data-ttu-id="b62c5-780">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span><span class="sxs-lookup"><span data-stu-id="b62c5-780">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="b62c5-781">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span><span class="sxs-lookup"><span data-stu-id="b62c5-781">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="b62c5-782">And vice versa, the JSON document is mapped back to a .NET object.</span><span class="sxs-lookup"><span data-stu-id="b62c5-782">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="b62c5-783">**C# Class**</span><span class="sxs-lookup"><span data-stu-id="b62c5-783">**C# Class**</span></span>

```csharp
    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };
```

<span data-ttu-id="b62c5-784">**JSON**</span><span class="sxs-lookup"><span data-stu-id="b62c5-784">**JSON**</span></span>  

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
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };
```


### <a name="linq-to-sql-translation"></a><span data-ttu-id="b62c5-785">LINQ to SQL translation</span><span class="sxs-lookup"><span data-stu-id="b62c5-785">LINQ to SQL translation</span></span>
<span data-ttu-id="b62c5-786">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-786">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="b62c5-787">In the following description, we assume the reader has a basic familiarity of LINQ.</span><span class="sxs-lookup"><span data-stu-id="b62c5-787">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="b62c5-788">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span><span class="sxs-lookup"><span data-stu-id="b62c5-788">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="b62c5-789">Only these JSON types are supported.</span><span class="sxs-lookup"><span data-stu-id="b62c5-789">Only these JSON types are supported.</span></span> <span data-ttu-id="b62c5-790">The following scalar expressions are supported.</span><span class="sxs-lookup"><span data-stu-id="b62c5-790">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="b62c5-791">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span><span class="sxs-lookup"><span data-stu-id="b62c5-791">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="b62c5-792">Property/array index expressions – these expressions refer to the property of an object or an array element.</span><span class="sxs-lookup"><span data-stu-id="b62c5-792">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="b62c5-793">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span><span class="sxs-lookup"><span data-stu-id="b62c5-793">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="b62c5-794">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span><span class="sxs-lookup"><span data-stu-id="b62c5-794">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="b62c5-795">For the complete list, refer to the SQL specification.</span><span class="sxs-lookup"><span data-stu-id="b62c5-795">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="b62c5-796">2 \* family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="b62c5-796">2 \* family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="b62c5-797">String comparison expression - these include comparing a string value to some constant string value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-797">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="b62c5-798">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span><span class="sxs-lookup"><span data-stu-id="b62c5-798">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="b62c5-799">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span><span class="sxs-lookup"><span data-stu-id="b62c5-799">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="b62c5-800">These values can be nested.</span><span class="sxs-lookup"><span data-stu-id="b62c5-800">These values can be nested.</span></span>
  
     <span data-ttu-id="b62c5-801">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span><span class="sxs-lookup"><span data-stu-id="b62c5-801">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="b62c5-802">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="b62c5-802">new int[] { 3, child.grade, 5 };</span></span>

### <a id="SupportedLinqOperators"></a><span data-ttu-id="b62c5-803">List of supported LINQ operators</span><span class="sxs-lookup"><span data-stu-id="b62c5-803">List of supported LINQ operators</span></span>
<span data-ttu-id="b62c5-804">Here is a list of supported LINQ operators in the LINQ provider included with the SQL .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b62c5-804">Here is a list of supported LINQ operators in the LINQ provider included with the SQL .NET SDK.</span></span>

* <span data-ttu-id="b62c5-805">**Select**: Projections translate to the SQL SELECT including object construction</span><span class="sxs-lookup"><span data-stu-id="b62c5-805">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="b62c5-806">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span><span class="sxs-lookup"><span data-stu-id="b62c5-806">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="b62c5-807">to the SQL operators</span><span class="sxs-lookup"><span data-stu-id="b62c5-807">to the SQL operators</span></span>
* <span data-ttu-id="b62c5-808">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span><span class="sxs-lookup"><span data-stu-id="b62c5-808">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="b62c5-809">Can be used to chain/nest expressions to filter on array elements</span><span class="sxs-lookup"><span data-stu-id="b62c5-809">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="b62c5-810">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span><span class="sxs-lookup"><span data-stu-id="b62c5-810">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="b62c5-811">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="b62c5-811">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="b62c5-812">**CompareTo**: Translates to range comparisons.</span><span class="sxs-lookup"><span data-stu-id="b62c5-812">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="b62c5-813">Commonly used for strings since they’re not comparable in .NET</span><span class="sxs-lookup"><span data-stu-id="b62c5-813">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="b62c5-814">**Take**: Translates to the SQL TOP for limiting results from a query</span><span class="sxs-lookup"><span data-stu-id="b62c5-814">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="b62c5-815">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-815">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="b62c5-816">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-816">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="b62c5-817">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-817">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="b62c5-818">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-818">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="b62c5-819">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span><span class="sxs-lookup"><span data-stu-id="b62c5-819">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="b62c5-820">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span><span class="sxs-lookup"><span data-stu-id="b62c5-820">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="b62c5-821">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span><span class="sxs-lookup"><span data-stu-id="b62c5-821">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="b62c5-822">SQL query operators</span><span class="sxs-lookup"><span data-stu-id="b62c5-822">SQL query operators</span></span>
<span data-ttu-id="b62c5-823">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-823">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="b62c5-824">Select Operator</span><span class="sxs-lookup"><span data-stu-id="b62c5-824">Select Operator</span></span>
<span data-ttu-id="b62c5-825">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span><span class="sxs-lookup"><span data-stu-id="b62c5-825">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="b62c5-826">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-826">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="b62c5-827">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-827">**SQL**</span></span> 

```sql
    SELECT VALUE f.parents[0].familyName
    FROM Families f
```

<span data-ttu-id="b62c5-828">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-828">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="b62c5-829">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-829">**SQL**</span></span> 

```sql
    SELECT VALUE f.children[0].grade + c
    FROM Families f 
```


<span data-ttu-id="b62c5-830">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-830">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="b62c5-831">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-831">**SQL**</span></span> 

```sql
    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f
```


#### <a name="selectmany-operator"></a><span data-ttu-id="b62c5-832">SelectMany operator</span><span class="sxs-lookup"><span data-stu-id="b62c5-832">SelectMany operator</span></span>
<span data-ttu-id="b62c5-833">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span><span class="sxs-lookup"><span data-stu-id="b62c5-833">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="b62c5-834">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-834">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="b62c5-835">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-835">**SQL**</span></span> 

```sql
    SELECT VALUE child
    FROM child IN Families.children
```

#### <a name="where-operator"></a><span data-ttu-id="b62c5-836">Where operator</span><span class="sxs-lookup"><span data-stu-id="b62c5-836">Where operator</span></span>
<span data-ttu-id="b62c5-837">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="b62c5-837">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="b62c5-838">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-838">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="b62c5-839">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-839">**SQL**</span></span> 

```sql
    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 
```

<span data-ttu-id="b62c5-840">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-840">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="b62c5-841">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-841">**SQL**</span></span> 

```sql
    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3
```

### <a name="composite-sql-queries"></a><span data-ttu-id="b62c5-842">Composite SQL queries</span><span class="sxs-lookup"><span data-stu-id="b62c5-842">Composite SQL queries</span></span>
<span data-ttu-id="b62c5-843">The above operators can be composed to form more powerful queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-843">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="b62c5-844">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span><span class="sxs-lookup"><span data-stu-id="b62c5-844">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="b62c5-845">Concatenation</span><span class="sxs-lookup"><span data-stu-id="b62c5-845">Concatenation</span></span>
<span data-ttu-id="b62c5-846">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-846">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="b62c5-847">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span><span class="sxs-lookup"><span data-stu-id="b62c5-847">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="b62c5-848">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-848">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="b62c5-849">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-849">**SQL**</span></span>

```sql
    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
```

<span data-ttu-id="b62c5-850">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-850">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="b62c5-851">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-851">**SQL**</span></span> 

```sql
    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3
```


<span data-ttu-id="b62c5-852">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-852">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="b62c5-853">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-853">**SQL**</span></span> 

```sql
    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)
```

<span data-ttu-id="b62c5-854">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-854">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="b62c5-855">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-855">**SQL**</span></span> 

```sql
    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"
```


#### <a name="nesting"></a><span data-ttu-id="b62c5-856">Nesting</span><span class="sxs-lookup"><span data-stu-id="b62c5-856">Nesting</span></span>
<span data-ttu-id="b62c5-857">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span><span class="sxs-lookup"><span data-stu-id="b62c5-857">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="b62c5-858">In a nested query, the inner query is applied to each element of the outer collection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-858">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="b62c5-859">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span><span class="sxs-lookup"><span data-stu-id="b62c5-859">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="b62c5-860">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-860">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="b62c5-861">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-861">**SQL**</span></span> 

```sql
    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents
```

<span data-ttu-id="b62c5-862">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-862">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="b62c5-863">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-863">**SQL**</span></span> 

```sql
    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"
```


<span data-ttu-id="b62c5-864">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="b62c5-864">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="b62c5-865">**SQL**</span><span class="sxs-lookup"><span data-stu-id="b62c5-865">**SQL**</span></span> 

```sql
    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName
```

## <a id="ExecutingSqlQueries"></a><span data-ttu-id="b62c5-866">Execute SQL queries</span><span class="sxs-lookup"><span data-stu-id="b62c5-866">Execute SQL queries</span></span>
<span data-ttu-id="b62c5-867">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span><span class="sxs-lookup"><span data-stu-id="b62c5-867">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="b62c5-868">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span><span class="sxs-lookup"><span data-stu-id="b62c5-868">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="b62c5-869">The REST API and the various libraries all support querying through SQL.</span><span class="sxs-lookup"><span data-stu-id="b62c5-869">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="b62c5-870">The .NET SDK supports LINQ querying in addition to SQL.</span><span class="sxs-lookup"><span data-stu-id="b62c5-870">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="b62c5-871">The following examples show how to create a query and submit it against a Cosmos DB database account.</span><span class="sxs-lookup"><span data-stu-id="b62c5-871">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <a id="RestAPI"></a><span data-ttu-id="b62c5-872">REST API</span><span class="sxs-lookup"><span data-stu-id="b62c5-872">REST API</span></span>
<span data-ttu-id="b62c5-873">Cosmos DB offers an open RESTful programming model over HTTP.</span><span class="sxs-lookup"><span data-stu-id="b62c5-873">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="b62c5-874">Database accounts can be provisioned using an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b62c5-874">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="b62c5-875">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span><span class="sxs-lookup"><span data-stu-id="b62c5-875">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="b62c5-876">A set of resources is referred to as a feed in this document.</span><span class="sxs-lookup"><span data-stu-id="b62c5-876">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="b62c5-877">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span><span class="sxs-lookup"><span data-stu-id="b62c5-877">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="b62c5-878">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span><span class="sxs-lookup"><span data-stu-id="b62c5-878">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="b62c5-879">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-879">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="b62c5-880">Queries are always read-only operations with no side-effects.</span><span class="sxs-lookup"><span data-stu-id="b62c5-880">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="b62c5-881">The following examples show a POST for a SQL API query made against a collection containing the two sample documents we've reviewed so far.</span><span class="sxs-lookup"><span data-stu-id="b62c5-881">The following examples show a POST for a SQL API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="b62c5-882">The query has a simple filter on the JSON name property.</span><span class="sxs-lookup"><span data-stu-id="b62c5-882">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="b62c5-883">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span><span class="sxs-lookup"><span data-stu-id="b62c5-883">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="b62c5-884">**Request**</span><span class="sxs-lookup"><span data-stu-id="b62c5-884">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="b62c5-885">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-885">**Results**</span></span>

```
    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }
```

<span data-ttu-id="b62c5-886">The second example shows a more complex query that returns multiple results from the join.</span><span class="sxs-lookup"><span data-stu-id="b62c5-886">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="b62c5-887">**Request**</span><span class="sxs-lookup"><span data-stu-id="b62c5-887">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="b62c5-888">**Results**</span><span class="sxs-lookup"><span data-stu-id="b62c5-888">**Results**</span></span>

```
    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }
```

<span data-ttu-id="b62c5-889">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span><span class="sxs-lookup"><span data-stu-id="b62c5-889">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="b62c5-890">Clients can paginate results by including the header in subsequent results.</span><span class="sxs-lookup"><span data-stu-id="b62c5-890">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="b62c5-891">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span><span class="sxs-lookup"><span data-stu-id="b62c5-891">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="b62c5-892">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span><span class="sxs-lookup"><span data-stu-id="b62c5-892">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="b62c5-893">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span><span class="sxs-lookup"><span data-stu-id="b62c5-893">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="b62c5-894">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span><span class="sxs-lookup"><span data-stu-id="b62c5-894">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="b62c5-895">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span><span class="sxs-lookup"><span data-stu-id="b62c5-895">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="b62c5-896">The queried collection's indexing policy can also influence the consistency of query results.</span><span class="sxs-lookup"><span data-stu-id="b62c5-896">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="b62c5-897">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span><span class="sxs-lookup"><span data-stu-id="b62c5-897">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="b62c5-898">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span><span class="sxs-lookup"><span data-stu-id="b62c5-898">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="b62c5-899">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="b62c5-899">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="b62c5-900">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span><span class="sxs-lookup"><span data-stu-id="b62c5-900">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="b62c5-901">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span><span class="sxs-lookup"><span data-stu-id="b62c5-901">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="b62c5-902">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span><span class="sxs-lookup"><span data-stu-id="b62c5-902">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="b62c5-903">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-903">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="b62c5-904">For more information, see [SQL query metrics for Azure Cosmos DB](sql-api-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b62c5-904">For more information, see [SQL query metrics for Azure Cosmos DB](sql-api-sql-query-metrics.md).</span></span>

### <a id="DotNetSdk"></a><span data-ttu-id="b62c5-905">C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="b62c5-905">C# (.NET) SDK</span></span>
<span data-ttu-id="b62c5-906">The .NET SDK supports both LINQ and SQL querying.</span><span class="sxs-lookup"><span data-stu-id="b62c5-906">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="b62c5-907">The following example shows how to perform the simple filter query introduced earlier in this document.</span><span class="sxs-lookup"><span data-stu-id="b62c5-907">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="b62c5-908">This sample compares two properties for equality within each document and uses anonymous projections.</span><span class="sxs-lookup"><span data-stu-id="b62c5-908">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="b62c5-909">The next sample shows joins, expressed through LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="b62c5-909">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="b62c5-910">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span><span class="sxs-lookup"><span data-stu-id="b62c5-910">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="b62c5-911">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span><span class="sxs-lookup"><span data-stu-id="b62c5-911">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="b62c5-912">The number of pages can be controlled using the `MaxItemCount` setting.</span><span class="sxs-lookup"><span data-stu-id="b62c5-912">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="b62c5-913">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="b62c5-913">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="b62c5-914">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span><span class="sxs-lookup"><span data-stu-id="b62c5-914">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="b62c5-915">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-915">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="b62c5-916">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span><span class="sxs-lookup"><span data-stu-id="b62c5-916">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <a id="JavaScriptServerSideApi"></a><span data-ttu-id="b62c5-917">JavaScript server-side API</span><span class="sxs-lookup"><span data-stu-id="b62c5-917">JavaScript server-side API</span></span>
<span data-ttu-id="b62c5-918">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="b62c5-918">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="b62c5-919">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span><span class="sxs-lookup"><span data-stu-id="b62c5-919">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="b62c5-920">These operations are wrapped in ambient ACID transactions.</span><span class="sxs-lookup"><span data-stu-id="b62c5-920">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="b62c5-921">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="b62c5-921">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a><span data-ttu-id="b62c5-922">References</span><span class="sxs-lookup"><span data-stu-id="b62c5-922">References</span></span>
1. <span data-ttu-id="b62c5-923">[Introduction to Azure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="b62c5-923">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="b62c5-924">Azure Cosmos DB SQL specification</span><span class="sxs-lookup"><span data-stu-id="b62c5-924">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="b62c5-925">Azure Cosmos DB .NET samples</span><span class="sxs-lookup"><span data-stu-id="b62c5-925">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="b62c5-926">[Azure Cosmos DB Consistency Levels][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="b62c5-926">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="b62c5-927">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="b62c5-927">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="b62c5-928">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="b62c5-928">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="b62c5-929">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="b62c5-929">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="b62c5-930">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="b62c5-930">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="b62c5-931">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="b62c5-931">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="b62c5-932">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="b62c5-932">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="b62c5-933">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="b62c5-933">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="b62c5-934">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="b62c5-934">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="b62c5-935">G.</span><span class="sxs-lookup"><span data-stu-id="b62c5-935">G.</span></span> <span data-ttu-id="b62c5-936">Graefe.</span><span class="sxs-lookup"><span data-stu-id="b62c5-936">Graefe.</span></span> <span data-ttu-id="b62c5-937">The Cascades framework for query optimization.</span><span class="sxs-lookup"><span data-stu-id="b62c5-937">The Cascades framework for query optimization.</span></span> <span data-ttu-id="b62c5-938">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="b62c5-938">IEEE Data Eng.</span></span> <span data-ttu-id="b62c5-939">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="b62c5-939">Bull., 18(3): 1995.</span></span>

[1]: ./media/sql-api-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md
