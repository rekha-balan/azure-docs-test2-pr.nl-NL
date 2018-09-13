---
title: SQL syntax and SQL query for DocumentDB | Microsoft Docs
description: Learn about SQL syntax, database concepts, and SQL queries for DocumentDB, a NoSQL database. SQL can used as a JSON query language in DocumentDB.
keywords: sql syntax,sql query, sql queries, json query language, database concepts and sql queries, aggregate functions
services: documentdb
documentationcenter: ''
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/08/2017
ms.author: arramac
ms.openlocfilehash: 131113fad176bfac67f37dda3d525daba8dd4b96
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548949"
---
# <a name="sql-query-and-sql-syntax-in-documentdb"></a><span data-ttu-id="39387-105">SQL query and SQL syntax in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="39387-105">SQL query and SQL syntax in DocumentDB</span></span>
<span data-ttu-id="39387-106">Microsoft Azure DocumentDB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span><span class="sxs-lookup"><span data-stu-id="39387-106">Microsoft Azure DocumentDB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="39387-107">DocumentDB is truly schema-free.</span><span class="sxs-lookup"><span data-stu-id="39387-107">DocumentDB is truly schema-free.</span></span> <span data-ttu-id="39387-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span><span class="sxs-lookup"><span data-stu-id="39387-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="39387-109">While designing the query language for DocumentDB we had two goals in mind:</span><span class="sxs-lookup"><span data-stu-id="39387-109">While designing the query language for DocumentDB we had two goals in mind:</span></span>

* <span data-ttu-id="39387-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="39387-111">SQL is one of the most familiar and popular query languages.</span><span class="sxs-lookup"><span data-stu-id="39387-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="39387-112">DocumentDB SQL provides a formal programming model for rich queries over JSON documents.</span><span class="sxs-lookup"><span data-stu-id="39387-112">DocumentDB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="39387-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span><span class="sxs-lookup"><span data-stu-id="39387-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="39387-114">The DocumentDB SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span><span class="sxs-lookup"><span data-stu-id="39387-114">The DocumentDB SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="39387-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user defined functions (UDFs) written entirely in JavaScript, among other features.</span><span class="sxs-lookup"><span data-stu-id="39387-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="39387-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span><span class="sxs-lookup"><span data-stu-id="39387-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="39387-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows DocumentDB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out DocumentDB and run SQL queries against our dataset.</span><span class="sxs-lookup"><span data-stu-id="39387-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows DocumentDB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out DocumentDB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="39387-118">Then, return to this article, where we'll start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span><span class="sxs-lookup"><span data-stu-id="39387-118">Then, return to this article, where we'll start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <a id="GettingStarted"></a><span data-ttu-id="39387-119">Getting started with SQL commands in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="39387-119">Getting started with SQL commands in DocumentDB</span></span>
<span data-ttu-id="39387-120">To see DocumentDB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span><span class="sxs-lookup"><span data-stu-id="39387-120">To see DocumentDB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="39387-121">Consider these two JSON documents about two families.</span><span class="sxs-lookup"><span data-stu-id="39387-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="39387-122">Note that with DocumentDB, we do not need to create any schemas or secondary indices explicitly.</span><span class="sxs-lookup"><span data-stu-id="39387-122">Note that with DocumentDB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="39387-123">We simply need to insert the JSON documents to a DocumentDB collection and subsequently query.</span><span class="sxs-lookup"><span data-stu-id="39387-123">We simply need to insert the JSON documents to a DocumentDB collection and subsequently query.</span></span> <span data-ttu-id="39387-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address and registration information.</span><span class="sxs-lookup"><span data-stu-id="39387-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address and registration information.</span></span> <span data-ttu-id="39387-125">The document has strings, numbers, booleans, arrays and nested properties.</span><span class="sxs-lookup"><span data-stu-id="39387-125">The document has strings, numbers, booleans, arrays and nested properties.</span></span> 

<span data-ttu-id="39387-126">**Document**</span><span class="sxs-lookup"><span data-stu-id="39387-126">**Document**</span></span>  

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

<span data-ttu-id="39387-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span><span class="sxs-lookup"><span data-stu-id="39387-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="39387-128">**Document**</span><span class="sxs-lookup"><span data-stu-id="39387-128">**Document**</span></span>  

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

<span data-ttu-id="39387-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB SQL.</span></span> <span data-ttu-id="39387-130">For example, the following query will return the documents where the id field matches `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="39387-130">For example, the following query will return the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="39387-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span><span class="sxs-lookup"><span data-stu-id="39387-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="39387-132">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-133">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-133">**Results**</span></span>

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


<span data-ttu-id="39387-134">Now consider the case where we need to reformat the JSON output in a different shape.</span><span class="sxs-lookup"><span data-stu-id="39387-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="39387-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span><span class="sxs-lookup"><span data-stu-id="39387-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="39387-136">In this case, "NY, NY" matches.</span><span class="sxs-lookup"><span data-stu-id="39387-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="39387-137">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="39387-138">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="39387-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span><span class="sxs-lookup"><span data-stu-id="39387-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="39387-140">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="39387-141">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="39387-142">We would like to draw attention to a few noteworthy aspects of the DocumentDB query language through the examples we've seen so far:</span><span class="sxs-lookup"><span data-stu-id="39387-142">We would like to draw attention to a few noteworthy aspects of the DocumentDB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="39387-143">Since DocumentDB SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span><span class="sxs-lookup"><span data-stu-id="39387-143">Since DocumentDB SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="39387-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="39387-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="39387-145">The structured query language works with schema-less data.</span><span class="sxs-lookup"><span data-stu-id="39387-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="39387-146">Therefore, the type system needs to be bound dynamically.</span><span class="sxs-lookup"><span data-stu-id="39387-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="39387-147">The same expression could yield different types on different documents.</span><span class="sxs-lookup"><span data-stu-id="39387-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="39387-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span><span class="sxs-lookup"><span data-stu-id="39387-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="39387-149">DocumentDB only supports strict JSON documents.</span><span class="sxs-lookup"><span data-stu-id="39387-149">DocumentDB only supports strict JSON documents.</span></span> <span data-ttu-id="39387-150">This means the type system and expressions are restricted to deal only with JSON types.</span><span class="sxs-lookup"><span data-stu-id="39387-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="39387-151">Please refer to the [JSON specification](http://www.json.org/) for more details.</span><span class="sxs-lookup"><span data-stu-id="39387-151">Please refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="39387-152">A DocumentDB collection is a schema-free container of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="39387-152">A DocumentDB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="39387-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span><span class="sxs-lookup"><span data-stu-id="39387-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="39387-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span><span class="sxs-lookup"><span data-stu-id="39387-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <a id="Indexing"></a> <span data-ttu-id="39387-155">DocumentDB indexing</span><span class="sxs-lookup"><span data-stu-id="39387-155">DocumentDB indexing</span></span>
<span data-ttu-id="39387-156">Before we get into the DocumentDB SQL syntax, it is worth exploring the indexing design in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="39387-156">Before we get into the DocumentDB SQL syntax, it is worth exploring the indexing design in DocumentDB.</span></span> 

<span data-ttu-id="39387-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span><span class="sxs-lookup"><span data-stu-id="39387-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="39387-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span><span class="sxs-lookup"><span data-stu-id="39387-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="39387-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span><span class="sxs-lookup"><span data-stu-id="39387-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="39387-160">Therefore, when we designed the DocumentDB indexing subsystem, we set the following goals:</span><span class="sxs-lookup"><span data-stu-id="39387-160">Therefore, when we designed the DocumentDB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="39387-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span><span class="sxs-lookup"><span data-stu-id="39387-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="39387-162">Support for efficient, rich hierarchical, and relational queries: The index supports the DocumentDB query language efficiently, including support for hierarchical and relational projections.</span><span class="sxs-lookup"><span data-stu-id="39387-162">Support for efficient, rich hierarchical, and relational queries: The index supports the DocumentDB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="39387-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span><span class="sxs-lookup"><span data-stu-id="39387-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="39387-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span><span class="sxs-lookup"><span data-stu-id="39387-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="39387-165">Support for multi-tenancy: Given the reservation based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span><span class="sxs-lookup"><span data-stu-id="39387-165">Support for multi-tenancy: Given the reservation based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="39387-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span><span class="sxs-lookup"><span data-stu-id="39387-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="39387-167">This is crucial because DocumentDB allows the developer to make cost based tradeoffs between index overhead in relation to the query performance.</span><span class="sxs-lookup"><span data-stu-id="39387-167">This is crucial because DocumentDB allows the developer to make cost based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="39387-168">Refer to the [DocumentDB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span><span class="sxs-lookup"><span data-stu-id="39387-168">Refer to the [DocumentDB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="39387-169">Let’s now get into the details of the DocumentDB SQL syntax.</span><span class="sxs-lookup"><span data-stu-id="39387-169">Let’s now get into the details of the DocumentDB SQL syntax.</span></span>

## <a id="Basics"></a><span data-ttu-id="39387-170">Basics of a DocumentDB SQL query</span><span class="sxs-lookup"><span data-stu-id="39387-170">Basics of a DocumentDB SQL query</span></span>
<span data-ttu-id="39387-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span><span class="sxs-lookup"><span data-stu-id="39387-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="39387-172">Typically, for each query, the source in the FROM clause is enumerated.</span><span class="sxs-lookup"><span data-stu-id="39387-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="39387-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="39387-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="39387-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span><span class="sxs-lookup"><span data-stu-id="39387-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a><span data-ttu-id="39387-175">FROM clause</span><span class="sxs-lookup"><span data-stu-id="39387-175">FROM clause</span></span>
<span data-ttu-id="39387-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span><span class="sxs-lookup"><span data-stu-id="39387-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="39387-177">The purpose of this clause is to specify the data source upon which the query must operate.</span><span class="sxs-lookup"><span data-stu-id="39387-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="39387-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span><span class="sxs-lookup"><span data-stu-id="39387-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="39387-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span><span class="sxs-lookup"><span data-stu-id="39387-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="39387-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span><span class="sxs-lookup"><span data-stu-id="39387-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="39387-181">The following list contains the rules that are enforced per query:</span><span class="sxs-lookup"><span data-stu-id="39387-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="39387-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="39387-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="39387-183">Here `f` is the equivalent of `Families`.</span><span class="sxs-lookup"><span data-stu-id="39387-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="39387-184">`AS` is an optional keyword to alias the identifier.</span><span class="sxs-lookup"><span data-stu-id="39387-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="39387-185">Note that once aliased, the original source cannot be bound.</span><span class="sxs-lookup"><span data-stu-id="39387-185">Note that once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="39387-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span><span class="sxs-lookup"><span data-stu-id="39387-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="39387-187">All properties that need to be referenced must be fully qualified.</span><span class="sxs-lookup"><span data-stu-id="39387-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="39387-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span><span class="sxs-lookup"><span data-stu-id="39387-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="39387-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span><span class="sxs-lookup"><span data-stu-id="39387-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="sub-documents"></a><span data-ttu-id="39387-190">Sub-documents</span><span class="sxs-lookup"><span data-stu-id="39387-190">Sub-documents</span></span>
<span data-ttu-id="39387-191">The source can also be reduced to a smaller subset.</span><span class="sxs-lookup"><span data-stu-id="39387-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="39387-192">For instance, to enumerating only a sub-tree in each document, the sub-root could then become the source, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="39387-192">For instance, to enumerating only a sub-tree in each document, the sub-root could then become the source, as shown in the following example.</span></span>

<span data-ttu-id="39387-193">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="39387-194">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-194">**Results**</span></span>  

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

<span data-ttu-id="39387-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="39387-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example.</span></span> <span data-ttu-id="39387-196">Any valid JSON value (not undefined) that can be found in the source will be considered for inclusion in the result of the query.</span><span class="sxs-lookup"><span data-stu-id="39387-196">Any valid JSON value (not undefined) that can be found in the source will be considered for inclusion in the result of the query.</span></span> <span data-ttu-id="39387-197">If some families don’t have an `address.state` value, they will be excluded in the query result.</span><span class="sxs-lookup"><span data-stu-id="39387-197">If some families don’t have an `address.state` value, they will be excluded in the query result.</span></span>

<span data-ttu-id="39387-198">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-198">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="39387-199">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-199">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a><span data-ttu-id="39387-200">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="39387-200">WHERE clause</span></span>
<span data-ttu-id="39387-201">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span><span class="sxs-lookup"><span data-stu-id="39387-201">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="39387-202">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span><span class="sxs-lookup"><span data-stu-id="39387-202">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="39387-203">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span><span class="sxs-lookup"><span data-stu-id="39387-203">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="39387-204">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span><span class="sxs-lookup"><span data-stu-id="39387-204">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="39387-205">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="39387-205">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="39387-206">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span><span class="sxs-lookup"><span data-stu-id="39387-206">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="39387-207">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-207">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-208">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-208">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="39387-209">The previous example showed a simple equality query.</span><span class="sxs-lookup"><span data-stu-id="39387-209">The previous example showed a simple equality query.</span></span> <span data-ttu-id="39387-210">DocumentDB SQL also supports a variety of scalar expressions.</span><span class="sxs-lookup"><span data-stu-id="39387-210">DocumentDB SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="39387-211">The most commonly used are binary and unary expressions.</span><span class="sxs-lookup"><span data-stu-id="39387-211">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="39387-212">Property references from the source JSON object are also valid expressions.</span><span class="sxs-lookup"><span data-stu-id="39387-212">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="39387-213">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span><span class="sxs-lookup"><span data-stu-id="39387-213">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="39387-214">Arithmetic</span><span class="sxs-lookup"><span data-stu-id="39387-214">Arithmetic</span></span></td>    
<td><span data-ttu-id="39387-215">+,-,\*,/,%</span><span class="sxs-lookup"><span data-stu-id="39387-215">+,-,\*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="39387-216">Bitwise</span><span class="sxs-lookup"><span data-stu-id="39387-216">Bitwise</span></span></td>    
<td><span data-ttu-id="39387-217">|, &, ^, <<, >>, >>> (zero-fill right shift)</span><span class="sxs-lookup"><span data-stu-id="39387-217">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="39387-218">Logical</span><span class="sxs-lookup"><span data-stu-id="39387-218">Logical</span></span></td>
<td><span data-ttu-id="39387-219">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="39387-219">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="39387-220">Comparison</span><span class="sxs-lookup"><span data-stu-id="39387-220">Comparison</span></span></td>    
<td><span data-ttu-id="39387-221">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="39387-221">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="39387-222">String</span><span class="sxs-lookup"><span data-stu-id="39387-222">String</span></span></td>    
<td><span data-ttu-id="39387-223">|| (concatenate)</span><span class="sxs-lookup"><span data-stu-id="39387-223">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="39387-224">Let’s take a look at some queries using binary operators.</span><span class="sxs-lookup"><span data-stu-id="39387-224">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="39387-225">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="39387-225">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="39387-226">In addition to binary and unary operators, property references are also allowed.</span><span class="sxs-lookup"><span data-stu-id="39387-226">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="39387-227">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span><span class="sxs-lookup"><span data-stu-id="39387-227">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="39387-228">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span><span class="sxs-lookup"><span data-stu-id="39387-228">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="39387-229">Equality and comparison operators</span><span class="sxs-lookup"><span data-stu-id="39387-229">Equality and comparison operators</span></span>
<span data-ttu-id="39387-230">The following table shows the result of equality comparisons in DocumentDB SQL between any two JSON types.</span><span class="sxs-lookup"><span data-stu-id="39387-230">The following table shows the result of equality comparisons in DocumentDB SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="39387-231">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-231">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-232">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-232">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-233">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-233">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-234">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-234">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-235">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-235">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-236">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-236">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-237">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-237">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="39387-238">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-238">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-239">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-239">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-245">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-246">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-246">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-247">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-247">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-248">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-248">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="39387-249">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-249">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-253">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-254">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-254">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-255">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-255">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-256">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-257">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-257">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="39387-258">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-258">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-261">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-262">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-262">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-263">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-263">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-265">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-266">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-266">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="39387-267">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-267">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-269">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-270">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-270">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-271">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-271">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-274">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-275">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-275">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="39387-276">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-276">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-277">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-278">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-278">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-279">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-279">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-283">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-284">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-284">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="39387-285">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-285">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-286">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-286">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="39387-287">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-287">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="39387-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-292">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="39387-293">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-293">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="39387-294">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="39387-294">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="39387-295">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span><span class="sxs-lookup"><span data-stu-id="39387-295">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="39387-296">Comparison across types results in Undefined.</span><span class="sxs-lookup"><span data-stu-id="39387-296">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="39387-297">Comparison between two objects or two arrays results in Undefined.</span><span class="sxs-lookup"><span data-stu-id="39387-297">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="39387-298">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span><span class="sxs-lookup"><span data-stu-id="39387-298">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="39387-299">BETWEEN keyword</span><span class="sxs-lookup"><span data-stu-id="39387-299">BETWEEN keyword</span></span>
<span data-ttu-id="39387-300">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-300">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="39387-301">BETWEEN can be used against strings or numbers.</span><span class="sxs-lookup"><span data-stu-id="39387-301">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="39387-302">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span><span class="sxs-lookup"><span data-stu-id="39387-302">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="39387-303">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span><span class="sxs-lookup"><span data-stu-id="39387-303">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="39387-304">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span><span class="sxs-lookup"><span data-stu-id="39387-304">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="39387-305">The main difference between using BETWEEN in DocumentDB and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span><span class="sxs-lookup"><span data-stu-id="39387-305">The main difference between using BETWEEN in DocumentDB and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="39387-306">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span><span class="sxs-lookup"><span data-stu-id="39387-306">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="39387-307">Logical (AND, OR and NOT) operators</span><span class="sxs-lookup"><span data-stu-id="39387-307">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="39387-308">Logical operators operate on Boolean values.</span><span class="sxs-lookup"><span data-stu-id="39387-308">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="39387-309">The logical truth tables for these operators are shown in the following tables.</span><span class="sxs-lookup"><span data-stu-id="39387-309">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="39387-310">OR</span><span class="sxs-lookup"><span data-stu-id="39387-310">OR</span></span> | <span data-ttu-id="39387-311">True</span><span class="sxs-lookup"><span data-stu-id="39387-311">True</span></span> | <span data-ttu-id="39387-312">False</span><span class="sxs-lookup"><span data-stu-id="39387-312">False</span></span> | <span data-ttu-id="39387-313">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-313">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39387-314">True</span><span class="sxs-lookup"><span data-stu-id="39387-314">True</span></span> |<span data-ttu-id="39387-315">True</span><span class="sxs-lookup"><span data-stu-id="39387-315">True</span></span> |<span data-ttu-id="39387-316">True</span><span class="sxs-lookup"><span data-stu-id="39387-316">True</span></span> |<span data-ttu-id="39387-317">True</span><span class="sxs-lookup"><span data-stu-id="39387-317">True</span></span> |
| <span data-ttu-id="39387-318">False</span><span class="sxs-lookup"><span data-stu-id="39387-318">False</span></span> |<span data-ttu-id="39387-319">True</span><span class="sxs-lookup"><span data-stu-id="39387-319">True</span></span> |<span data-ttu-id="39387-320">False</span><span class="sxs-lookup"><span data-stu-id="39387-320">False</span></span> |<span data-ttu-id="39387-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-321">Undefined</span></span> |
| <span data-ttu-id="39387-322">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-322">Undefined</span></span> |<span data-ttu-id="39387-323">True</span><span class="sxs-lookup"><span data-stu-id="39387-323">True</span></span> |<span data-ttu-id="39387-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-324">Undefined</span></span> |<span data-ttu-id="39387-325">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-325">Undefined</span></span> |

| <span data-ttu-id="39387-326">AND</span><span class="sxs-lookup"><span data-stu-id="39387-326">AND</span></span> | <span data-ttu-id="39387-327">True</span><span class="sxs-lookup"><span data-stu-id="39387-327">True</span></span> | <span data-ttu-id="39387-328">False</span><span class="sxs-lookup"><span data-stu-id="39387-328">False</span></span> | <span data-ttu-id="39387-329">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-329">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39387-330">True</span><span class="sxs-lookup"><span data-stu-id="39387-330">True</span></span> |<span data-ttu-id="39387-331">True</span><span class="sxs-lookup"><span data-stu-id="39387-331">True</span></span> |<span data-ttu-id="39387-332">False</span><span class="sxs-lookup"><span data-stu-id="39387-332">False</span></span> |<span data-ttu-id="39387-333">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-333">Undefined</span></span> |
| <span data-ttu-id="39387-334">False</span><span class="sxs-lookup"><span data-stu-id="39387-334">False</span></span> |<span data-ttu-id="39387-335">False</span><span class="sxs-lookup"><span data-stu-id="39387-335">False</span></span> |<span data-ttu-id="39387-336">False</span><span class="sxs-lookup"><span data-stu-id="39387-336">False</span></span> |<span data-ttu-id="39387-337">False</span><span class="sxs-lookup"><span data-stu-id="39387-337">False</span></span> |
| <span data-ttu-id="39387-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-338">Undefined</span></span> |<span data-ttu-id="39387-339">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-339">Undefined</span></span> |<span data-ttu-id="39387-340">False</span><span class="sxs-lookup"><span data-stu-id="39387-340">False</span></span> |<span data-ttu-id="39387-341">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-341">Undefined</span></span> |

| <span data-ttu-id="39387-342">NOT</span><span class="sxs-lookup"><span data-stu-id="39387-342">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="39387-343">True</span><span class="sxs-lookup"><span data-stu-id="39387-343">True</span></span> |<span data-ttu-id="39387-344">False</span><span class="sxs-lookup"><span data-stu-id="39387-344">False</span></span> |
| <span data-ttu-id="39387-345">False</span><span class="sxs-lookup"><span data-stu-id="39387-345">False</span></span> |<span data-ttu-id="39387-346">True</span><span class="sxs-lookup"><span data-stu-id="39387-346">True</span></span> |
| <span data-ttu-id="39387-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-347">Undefined</span></span> |<span data-ttu-id="39387-348">Undefined</span><span class="sxs-lookup"><span data-stu-id="39387-348">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="39387-349">IN keyword</span><span class="sxs-lookup"><span data-stu-id="39387-349">IN keyword</span></span>
<span data-ttu-id="39387-350">The IN keyword can be used to check whether a specified value matches any value in a list.</span><span class="sxs-lookup"><span data-stu-id="39387-350">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="39387-351">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="39387-351">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="39387-352">This example returns all documents where the state is any of the specified values.</span><span class="sxs-lookup"><span data-stu-id="39387-352">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="39387-353">Ternary (?) and Coalesce (??) operators</span><span class="sxs-lookup"><span data-stu-id="39387-353">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="39387-354">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="39387-354">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="39387-355">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span><span class="sxs-lookup"><span data-stu-id="39387-355">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="39387-356">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span><span class="sxs-lookup"><span data-stu-id="39387-356">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="39387-357">You can also nest the calls to the operator like in the query below.</span><span class="sxs-lookup"><span data-stu-id="39387-357">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="39387-358">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents will be excluded in the query results.</span><span class="sxs-lookup"><span data-stu-id="39387-358">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents will be excluded in the query results.</span></span>

<span data-ttu-id="39387-359">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="39387-359">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="39387-360">is defined) in a document.</span><span class="sxs-lookup"><span data-stu-id="39387-360">is defined) in a document.</span></span> <span data-ttu-id="39387-361">This is useful when querying against semi-structured or data of mixed types.</span><span class="sxs-lookup"><span data-stu-id="39387-361">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="39387-362">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span><span class="sxs-lookup"><span data-stu-id="39387-362">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a><span data-ttu-id="39387-363">Quoted property accessor</span><span class="sxs-lookup"><span data-stu-id="39387-363">Quoted property accessor</span></span>
<span data-ttu-id="39387-364">You can also access properties using the quoted property operator `[]`.</span><span class="sxs-lookup"><span data-stu-id="39387-364">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="39387-365">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span><span class="sxs-lookup"><span data-stu-id="39387-365">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="39387-366">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span><span class="sxs-lookup"><span data-stu-id="39387-366">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a><span data-ttu-id="39387-367">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="39387-367">SELECT clause</span></span>
<span data-ttu-id="39387-368">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values will be retrieved from the query, just like in ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-368">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values will be retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="39387-369">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span><span class="sxs-lookup"><span data-stu-id="39387-369">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="39387-370">The following example shows a typical SELECT query.</span><span class="sxs-lookup"><span data-stu-id="39387-370">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="39387-371">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-371">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-372">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-372">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="39387-373">Nested properties</span><span class="sxs-lookup"><span data-stu-id="39387-373">Nested properties</span></span>
<span data-ttu-id="39387-374">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="39387-374">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="39387-375">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-375">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-376">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-376">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="39387-377">Projection also supports JSON expressions as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="39387-377">Projection also supports JSON expressions as shown in the following example.</span></span>

<span data-ttu-id="39387-378">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-378">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-379">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-379">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="39387-380">Let's look at the role of `$1` here.</span><span class="sxs-lookup"><span data-stu-id="39387-380">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="39387-381">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span><span class="sxs-lookup"><span data-stu-id="39387-381">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="39387-382">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="39387-382">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="39387-383">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-383">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-384">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-384">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="39387-385">Aliasing</span><span class="sxs-lookup"><span data-stu-id="39387-385">Aliasing</span></span>
<span data-ttu-id="39387-386">Now let's extend the example above with explicit aliasing of values.</span><span class="sxs-lookup"><span data-stu-id="39387-386">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="39387-387">AS is the keyword used for aliasing.</span><span class="sxs-lookup"><span data-stu-id="39387-387">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="39387-388">Note that it's optional as shown while projecting the second value as `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="39387-388">Note that it's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="39387-389">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span><span class="sxs-lookup"><span data-stu-id="39387-389">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="39387-390">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-390">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-391">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-391">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="39387-392">Scalar expressions</span><span class="sxs-lookup"><span data-stu-id="39387-392">Scalar expressions</span></span>
<span data-ttu-id="39387-393">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span><span class="sxs-lookup"><span data-stu-id="39387-393">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="39387-394">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-394">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="39387-395">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-395">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="39387-396">Here's a more complex example that uses a scalar expression.</span><span class="sxs-lookup"><span data-stu-id="39387-396">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="39387-397">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-397">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="39387-398">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-398">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="39387-399">In the following example, the result of the scalar expression is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="39387-399">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="39387-400">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-400">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="39387-401">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-401">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="39387-402">Object and array creation</span><span class="sxs-lookup"><span data-stu-id="39387-402">Object and array creation</span></span>
<span data-ttu-id="39387-403">Another key feature of DocumentDB SQL is array/object creation.</span><span class="sxs-lookup"><span data-stu-id="39387-403">Another key feature of DocumentDB SQL is array/object creation.</span></span> <span data-ttu-id="39387-404">In the previous example, note that we created a new JSON object.</span><span class="sxs-lookup"><span data-stu-id="39387-404">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="39387-405">Similarly, one can also construct arrays as shown in the following examples.</span><span class="sxs-lookup"><span data-stu-id="39387-405">Similarly, one can also construct arrays as shown in the following examples.</span></span>

<span data-ttu-id="39387-406">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-406">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="39387-407">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-407">**Results**</span></span>  

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

### <a id="ValueKeyword"></a><span data-ttu-id="39387-408">VALUE keyword</span><span class="sxs-lookup"><span data-stu-id="39387-408">VALUE keyword</span></span>
<span data-ttu-id="39387-409">The **VALUE** keyword provides a way to return JSON value.</span><span class="sxs-lookup"><span data-stu-id="39387-409">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="39387-410">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="39387-410">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="39387-411">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-411">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="39387-412">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-412">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="39387-413">The following query returns the JSON value without the `"address"` label in the results.</span><span class="sxs-lookup"><span data-stu-id="39387-413">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="39387-414">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-414">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="39387-415">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-415">**Results**</span></span>  

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

<span data-ttu-id="39387-416">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span><span class="sxs-lookup"><span data-stu-id="39387-416">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="39387-417">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-417">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="39387-418">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-418">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="39387-419">\* Operator</span><span class="sxs-lookup"><span data-stu-id="39387-419">\* Operator</span></span>
<span data-ttu-id="39387-420">The special operator (\*) is supported to project the document as-is.</span><span class="sxs-lookup"><span data-stu-id="39387-420">The special operator (\*) is supported to project the document as-is.</span></span> <span data-ttu-id="39387-421">When used, it must be the only projected field.</span><span class="sxs-lookup"><span data-stu-id="39387-421">When used, it must be the only projected field.</span></span> <span data-ttu-id="39387-422">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span><span class="sxs-lookup"><span data-stu-id="39387-422">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="39387-423">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-423">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="39387-424">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-424">**Results**</span></span>

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

### <a id="TopKeyword"></a><span data-ttu-id="39387-425">TOP Operator</span><span class="sxs-lookup"><span data-stu-id="39387-425">TOP Operator</span></span>
<span data-ttu-id="39387-426">The TOP keyword can be used to limit the number of values from a query.</span><span class="sxs-lookup"><span data-stu-id="39387-426">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="39387-427">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span><span class="sxs-lookup"><span data-stu-id="39387-427">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="39387-428">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span><span class="sxs-lookup"><span data-stu-id="39387-428">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="39387-429">This is the only way to predictably indicate which rows are affected by TOP.</span><span class="sxs-lookup"><span data-stu-id="39387-429">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="39387-430">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-430">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="39387-431">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-431">**Results**</span></span>

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

<span data-ttu-id="39387-432">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span><span class="sxs-lookup"><span data-stu-id="39387-432">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="39387-433">For more details, please see parameterized queries below.</span><span class="sxs-lookup"><span data-stu-id="39387-433">For more details, please see parameterized queries below.</span></span>

### <a id="Aggregates"></a><span data-ttu-id="39387-434">Aggregate Functions</span><span class="sxs-lookup"><span data-stu-id="39387-434">Aggregate Functions</span></span>
<span data-ttu-id="39387-435">You can also perform aggregations in the `SELECT` clause.</span><span class="sxs-lookup"><span data-stu-id="39387-435">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="39387-436">Aggregate functions perform a calculation on a set of values and return a single value.</span><span class="sxs-lookup"><span data-stu-id="39387-436">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="39387-437">For example, the following query returns the count of family documents within the collection.</span><span class="sxs-lookup"><span data-stu-id="39387-437">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="39387-438">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-438">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="39387-439">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-439">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="39387-440">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span><span class="sxs-lookup"><span data-stu-id="39387-440">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="39387-441">For example, the following query returns the count of values as a single number:</span><span class="sxs-lookup"><span data-stu-id="39387-441">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="39387-442">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-442">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="39387-443">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-443">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="39387-444">You can also perform aggregates in combination with filters.</span><span class="sxs-lookup"><span data-stu-id="39387-444">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="39387-445">For example, the following query returns the count of documents with the address in the state of Washington.</span><span class="sxs-lookup"><span data-stu-id="39387-445">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="39387-446">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-446">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="39387-447">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-447">**Results**</span></span>

    [{
        "$1": 1
    }]

<span data-ttu-id="39387-448">The following tables shows the list of supported aggregate functions in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="39387-448">The following tables shows the list of supported aggregate functions in DocumentDB.</span></span> <span data-ttu-id="39387-449">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span><span class="sxs-lookup"><span data-stu-id="39387-449">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="39387-450">Usage</span><span class="sxs-lookup"><span data-stu-id="39387-450">Usage</span></span> | <span data-ttu-id="39387-451">Description</span><span class="sxs-lookup"><span data-stu-id="39387-451">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="39387-452">COUNT</span><span class="sxs-lookup"><span data-stu-id="39387-452">COUNT</span></span> | <span data-ttu-id="39387-453">Returns the number of items in the expression.</span><span class="sxs-lookup"><span data-stu-id="39387-453">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="39387-454">SUM</span><span class="sxs-lookup"><span data-stu-id="39387-454">SUM</span></span>   | <span data-ttu-id="39387-455">Returns the sum of all the values in the expression.</span><span class="sxs-lookup"><span data-stu-id="39387-455">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="39387-456">MIN</span><span class="sxs-lookup"><span data-stu-id="39387-456">MIN</span></span>   | <span data-ttu-id="39387-457">Returns the minimum value in the expression.</span><span class="sxs-lookup"><span data-stu-id="39387-457">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="39387-458">MAX</span><span class="sxs-lookup"><span data-stu-id="39387-458">MAX</span></span>   | <span data-ttu-id="39387-459">Returns the maximum value in the expression.</span><span class="sxs-lookup"><span data-stu-id="39387-459">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="39387-460">AVG</span><span class="sxs-lookup"><span data-stu-id="39387-460">AVG</span></span>   | <span data-ttu-id="39387-461">Returns the average of the values in the expression.</span><span class="sxs-lookup"><span data-stu-id="39387-461">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="39387-462">Aggregates can also be performed over the results of an array iteration.</span><span class="sxs-lookup"><span data-stu-id="39387-462">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="39387-463">For more details, see [Array Iteration in Queries](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="39387-463">For more details, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="39387-464">When using the Azure Portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span><span class="sxs-lookup"><span data-stu-id="39387-464">When using the Azure Portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="39387-465">The SDKs will produce a single cumulative value across all pages.</span><span class="sxs-lookup"><span data-stu-id="39387-465">The SDKs will produce a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="39387-466">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span><span class="sxs-lookup"><span data-stu-id="39387-466">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <a id="OrderByClause"></a><span data-ttu-id="39387-467">ORDER BY clause</span><span class="sxs-lookup"><span data-stu-id="39387-467">ORDER BY clause</span></span>
<span data-ttu-id="39387-468">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span><span class="sxs-lookup"><span data-stu-id="39387-468">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="39387-469">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span><span class="sxs-lookup"><span data-stu-id="39387-469">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="39387-470">For example, here's a query that retrieves families in order of the resident city's name.</span><span class="sxs-lookup"><span data-stu-id="39387-470">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="39387-471">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-471">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="39387-472">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-472">**Results**</span></span>

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

<span data-ttu-id="39387-473">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span><span class="sxs-lookup"><span data-stu-id="39387-473">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="39387-474">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-474">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="39387-475">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-475">**Results**</span></span>

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

## <a id="Advanced"></a><span data-ttu-id="39387-476">Advanced database concepts and SQL queries</span><span class="sxs-lookup"><span data-stu-id="39387-476">Advanced database concepts and SQL queries</span></span>

### <a id="Iteration"></a><span data-ttu-id="39387-477">Iteration</span><span class="sxs-lookup"><span data-stu-id="39387-477">Iteration</span></span>
<span data-ttu-id="39387-478">A new construct was added via the **IN** keyword in DocumentDB SQL to provide support for iterating over JSON arrays.</span><span class="sxs-lookup"><span data-stu-id="39387-478">A new construct was added via the **IN** keyword in DocumentDB SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="39387-479">The FROM source provides support for iteration.</span><span class="sxs-lookup"><span data-stu-id="39387-479">The FROM source provides support for iteration.</span></span> <span data-ttu-id="39387-480">Let's start with the following example:</span><span class="sxs-lookup"><span data-stu-id="39387-480">Let's start with the following example:</span></span>

<span data-ttu-id="39387-481">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-481">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="39387-482">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-482">**Results**</span></span>  

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

<span data-ttu-id="39387-483">Now let's look at another query that performs iteration over children in the collection.</span><span class="sxs-lookup"><span data-stu-id="39387-483">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="39387-484">Note the difference in the output array.</span><span class="sxs-lookup"><span data-stu-id="39387-484">Note the difference in the output array.</span></span> <span data-ttu-id="39387-485">This example splits `children` and flattens the results into a single array.</span><span class="sxs-lookup"><span data-stu-id="39387-485">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="39387-486">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-486">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="39387-487">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-487">**Results**</span></span>  

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

<span data-ttu-id="39387-488">This can be further used to filter on each individual entry of the array as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="39387-488">This can be further used to filter on each individual entry of the array as shown in the following example.</span></span>

<span data-ttu-id="39387-489">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-489">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="39387-490">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-490">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="39387-491">You can also perform aggregation over the result of array iteration.</span><span class="sxs-lookup"><span data-stu-id="39387-491">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="39387-492">For example, the following query counts the number of children among all families.</span><span class="sxs-lookup"><span data-stu-id="39387-492">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="39387-493">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-493">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="39387-494">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-494">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a><span data-ttu-id="39387-495">Joins</span><span class="sxs-lookup"><span data-stu-id="39387-495">Joins</span></span>
<span data-ttu-id="39387-496">In a relational database, the need to join across tables is very important.</span><span class="sxs-lookup"><span data-stu-id="39387-496">In a relational database, the need to join across tables is very important.</span></span> <span data-ttu-id="39387-497">It's the logical corollary to designing normalized schemas.</span><span class="sxs-lookup"><span data-stu-id="39387-497">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="39387-498">Contrary to this, DocumentDB deals with the denormalized data model of schema-free documents.</span><span class="sxs-lookup"><span data-stu-id="39387-498">Contrary to this, DocumentDB deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="39387-499">This is the logical equivalent of a "self-join".</span><span class="sxs-lookup"><span data-stu-id="39387-499">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="39387-500">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="39387-500">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="39387-501">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span><span class="sxs-lookup"><span data-stu-id="39387-501">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="39387-502">Each tuple has values produced by iterating all collection aliases over their respective sets.</span><span class="sxs-lookup"><span data-stu-id="39387-502">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="39387-503">In other words, this is a full cross product of the sets participating in the join.</span><span class="sxs-lookup"><span data-stu-id="39387-503">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="39387-504">The following examples show how the JOIN clause works.</span><span class="sxs-lookup"><span data-stu-id="39387-504">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="39387-505">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span><span class="sxs-lookup"><span data-stu-id="39387-505">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="39387-506">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-506">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="39387-507">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-507">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="39387-508">In the following example, the join is between the document root and the `children` sub-root.</span><span class="sxs-lookup"><span data-stu-id="39387-508">In the following example, the join is between the document root and the `children` sub-root.</span></span> <span data-ttu-id="39387-509">It's a cross product between two JSON objects.</span><span class="sxs-lookup"><span data-stu-id="39387-509">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="39387-510">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span><span class="sxs-lookup"><span data-stu-id="39387-510">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="39387-511">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span><span class="sxs-lookup"><span data-stu-id="39387-511">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="39387-512">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-512">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="39387-513">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-513">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="39387-514">The following example shows a more conventional join:</span><span class="sxs-lookup"><span data-stu-id="39387-514">The following example shows a more conventional join:</span></span>

<span data-ttu-id="39387-515">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-515">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="39387-516">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-516">**Results**</span></span>

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



<span data-ttu-id="39387-517">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span><span class="sxs-lookup"><span data-stu-id="39387-517">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="39387-518">So, the flow in this case is as follows:</span><span class="sxs-lookup"><span data-stu-id="39387-518">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="39387-519">Expand each child element **c** in the array.</span><span class="sxs-lookup"><span data-stu-id="39387-519">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="39387-520">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span><span class="sxs-lookup"><span data-stu-id="39387-520">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="39387-521">Finally, project the root object **f** name property alone.</span><span class="sxs-lookup"><span data-stu-id="39387-521">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="39387-522">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span><span class="sxs-lookup"><span data-stu-id="39387-522">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="39387-523">The second document (`WakefieldFamily`) contains two children.</span><span class="sxs-lookup"><span data-stu-id="39387-523">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="39387-524">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span><span class="sxs-lookup"><span data-stu-id="39387-524">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="39387-525">Note that the root fields in both these documents will be same, just as you would expect in a cross product.</span><span class="sxs-lookup"><span data-stu-id="39387-525">Note that the root fields in both these documents will be same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="39387-526">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span><span class="sxs-lookup"><span data-stu-id="39387-526">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="39387-527">Furthermore, as we will see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span><span class="sxs-lookup"><span data-stu-id="39387-527">Furthermore, as we will see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="39387-528">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-528">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="39387-529">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-529">**Results**</span></span>

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



<span data-ttu-id="39387-530">This example is a natural extension of the preceding example, and performs a double join.</span><span class="sxs-lookup"><span data-stu-id="39387-530">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="39387-531">So, the cross product can be viewed as the following pseudo-code.</span><span class="sxs-lookup"><span data-stu-id="39387-531">So, the cross product can be viewed as the following pseudo-code.</span></span>

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

<span data-ttu-id="39387-532">`AndersenFamily` has one child who has one pet.</span><span class="sxs-lookup"><span data-stu-id="39387-532">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="39387-533">So, the cross product yields one row (1*1*1) from this family.</span><span class="sxs-lookup"><span data-stu-id="39387-533">So, the cross product yields one row (1*1*1) from this family.</span></span> <span data-ttu-id="39387-534">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span><span class="sxs-lookup"><span data-stu-id="39387-534">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="39387-535">Jesse has 2 pets though.</span><span class="sxs-lookup"><span data-stu-id="39387-535">Jesse has 2 pets though.</span></span> <span data-ttu-id="39387-536">Hence the cross product yields 1*1*2 = 2 rows from this family.</span><span class="sxs-lookup"><span data-stu-id="39387-536">Hence the cross product yields 1*1*2 = 2 rows from this family.</span></span>

<span data-ttu-id="39387-537">In the next example, there is an additional filter on `pet`.</span><span class="sxs-lookup"><span data-stu-id="39387-537">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="39387-538">This excludes all the tuples where the pet name is not "Shadow".</span><span class="sxs-lookup"><span data-stu-id="39387-538">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="39387-539">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span><span class="sxs-lookup"><span data-stu-id="39387-539">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="39387-540">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-540">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="39387-541">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-541">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a><span data-ttu-id="39387-542">JavaScript integration</span><span class="sxs-lookup"><span data-stu-id="39387-542">JavaScript integration</span></span>
<span data-ttu-id="39387-543">DocumentDB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="39387-543">DocumentDB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="39387-544">This allows for both:</span><span class="sxs-lookup"><span data-stu-id="39387-544">This allows for both:</span></span>

* <span data-ttu-id="39387-545">Ability to do high performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span><span class="sxs-lookup"><span data-stu-id="39387-545">Ability to do high performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="39387-546">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span><span class="sxs-lookup"><span data-stu-id="39387-546">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="39387-547">For more details about DocumentDB support for JavaScript integration, please refer to the JavaScript server side programmability documentation.</span><span class="sxs-lookup"><span data-stu-id="39387-547">For more details about DocumentDB support for JavaScript integration, please refer to the JavaScript server side programmability documentation.</span></span>

### <a id="UserDefinedFunctions"></a><span data-ttu-id="39387-548">User Defined Functions (UDFs)</span><span class="sxs-lookup"><span data-stu-id="39387-548">User Defined Functions (UDFs)</span></span>
<span data-ttu-id="39387-549">Along with the types already defined in this article, DocumentDB SQL provides support for User Defined Functions (UDF).</span><span class="sxs-lookup"><span data-stu-id="39387-549">Along with the types already defined in this article, DocumentDB SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="39387-550">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span><span class="sxs-lookup"><span data-stu-id="39387-550">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="39387-551">Each of these arguments are checked for being legal JSON values.</span><span class="sxs-lookup"><span data-stu-id="39387-551">Each of these arguments are checked for being legal JSON values.</span></span>  

<span data-ttu-id="39387-552">The DocumentDB SQL syntax is extended to support custom application logic using these User Defined Functions.</span><span class="sxs-lookup"><span data-stu-id="39387-552">The DocumentDB SQL syntax is extended to support custom application logic using these User Defined Functions.</span></span> <span data-ttu-id="39387-553">UDFs can be registered with DocumentDB and then be referenced as part of a SQL query.</span><span class="sxs-lookup"><span data-stu-id="39387-553">UDFs can be registered with DocumentDB and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="39387-554">In fact, the UDFs are exquisitely designed to be invoked by queries.</span><span class="sxs-lookup"><span data-stu-id="39387-554">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="39387-555">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span><span class="sxs-lookup"><span data-stu-id="39387-555">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="39387-556">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="39387-556">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="39387-557">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span><span class="sxs-lookup"><span data-stu-id="39387-557">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="39387-558">Below is an example of how a UDF can be registered at the DocumentDB database, specifically under a document collection.</span><span class="sxs-lookup"><span data-stu-id="39387-558">Below is an example of how a UDF can be registered at the DocumentDB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="39387-559">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="39387-559">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="39387-560">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span><span class="sxs-lookup"><span data-stu-id="39387-560">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="39387-561">We can now use this UDF in a query in a projection.</span><span class="sxs-lookup"><span data-stu-id="39387-561">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="39387-562">UDFs must be qualified with the case-sensitive prefix "udf."</span><span class="sxs-lookup"><span data-stu-id="39387-562">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="39387-563">when called from within queries.</span><span class="sxs-lookup"><span data-stu-id="39387-563">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="39387-564">Prior to 3/17/2015, DocumentDB supported UDF calls without the "udf."</span><span class="sxs-lookup"><span data-stu-id="39387-564">Prior to 3/17/2015, DocumentDB supported UDF calls without the "udf."</span></span> <span data-ttu-id="39387-565">prefix like SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="39387-565">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="39387-566">This calling pattern has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="39387-566">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="39387-567">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-567">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="39387-568">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-568">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="39387-569">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span><span class="sxs-lookup"><span data-stu-id="39387-569">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="39387-570">prefix :</span><span class="sxs-lookup"><span data-stu-id="39387-570">prefix :</span></span>

<span data-ttu-id="39387-571">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-571">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="39387-572">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-572">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="39387-573">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span><span class="sxs-lookup"><span data-stu-id="39387-573">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="39387-574">To expand on the power of UDFs, let's look at another example with conditional logic:</span><span class="sxs-lookup"><span data-stu-id="39387-574">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="39387-575">Below is an example that exercises the UDF.</span><span class="sxs-lookup"><span data-stu-id="39387-575">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="39387-576">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-576">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="39387-577">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-577">**Results**</span></span>

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


<span data-ttu-id="39387-578">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span><span class="sxs-lookup"><span data-stu-id="39387-578">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="39387-579">DocumentDB SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span><span class="sxs-lookup"><span data-stu-id="39387-579">DocumentDB SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="39387-580">The result is incorporated in the overall execution pipeline seamlessly.</span><span class="sxs-lookup"><span data-stu-id="39387-580">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="39387-581">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span><span class="sxs-lookup"><span data-stu-id="39387-581">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="39387-582">Similarly if the result of the UDF is undefined, it's not included in the result.</span><span class="sxs-lookup"><span data-stu-id="39387-582">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="39387-583">In summary, UDFs are great tools to do complex business logic as part of the query.</span><span class="sxs-lookup"><span data-stu-id="39387-583">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="39387-584">Operator evaluation</span><span class="sxs-lookup"><span data-stu-id="39387-584">Operator evaluation</span></span>
<span data-ttu-id="39387-585">DocumentDB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span><span class="sxs-lookup"><span data-stu-id="39387-585">DocumentDB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="39387-586">While DocumentDB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span><span class="sxs-lookup"><span data-stu-id="39387-586">While DocumentDB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="39387-587">In DocumentDB SQL, unlike in traditional SQL, the types of values are often not known until the values are actually retrieved from database.</span><span class="sxs-lookup"><span data-stu-id="39387-587">In DocumentDB SQL, unlike in traditional SQL, the types of values are often not known until the values are actually retrieved from database.</span></span> <span data-ttu-id="39387-588">In order to efficiently execute queries, most of the operators have strict type requirements.</span><span class="sxs-lookup"><span data-stu-id="39387-588">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="39387-589">DocumentDB SQL doesn't perform implicit conversions, unlike JavaScript.</span><span class="sxs-lookup"><span data-stu-id="39387-589">DocumentDB SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="39387-590">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents which contain an Age property whose value is 21.</span><span class="sxs-lookup"><span data-stu-id="39387-590">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents which contain an Age property whose value is 21.</span></span> <span data-ttu-id="39387-591">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span><span class="sxs-lookup"><span data-stu-id="39387-591">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="39387-592">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span><span class="sxs-lookup"><span data-stu-id="39387-592">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="39387-593">This choice is crucial for efficient index matching in DocumentDB SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-593">This choice is crucial for efficient index matching in DocumentDB SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="39387-594">Parameterized SQL queries</span><span class="sxs-lookup"><span data-stu-id="39387-594">Parameterized SQL queries</span></span>
<span data-ttu-id="39387-595">DocumentDB supports queries with parameters expressed with the familiar @ notation.</span><span class="sxs-lookup"><span data-stu-id="39387-595">DocumentDB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="39387-596">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span><span class="sxs-lookup"><span data-stu-id="39387-596">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="39387-597">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span><span class="sxs-lookup"><span data-stu-id="39387-597">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="39387-598">This request can then be sent to DocumentDB as a parameterized JSON query like shown below.</span><span class="sxs-lookup"><span data-stu-id="39387-598">This request can then be sent to DocumentDB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="39387-599">The argument to TOP can be set using parameterized queries like shown below.</span><span class="sxs-lookup"><span data-stu-id="39387-599">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="39387-600">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span><span class="sxs-lookup"><span data-stu-id="39387-600">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="39387-601">Also since DocumentDB is schema-less, parameters are not validated against any type.</span><span class="sxs-lookup"><span data-stu-id="39387-601">Also since DocumentDB is schema-less, parameters are not validated against any type.</span></span>

## <a id="BuiltinFunctions"></a><span data-ttu-id="39387-602">Built-in functions</span><span class="sxs-lookup"><span data-stu-id="39387-602">Built-in functions</span></span>
<span data-ttu-id="39387-603">DocumentDB also supports a number of built-in functions for common operations, that can be used inside queries like user defined functions (UDFs).</span><span class="sxs-lookup"><span data-stu-id="39387-603">DocumentDB also supports a number of built-in functions for common operations, that can be used inside queries like user defined functions (UDFs).</span></span>

| <span data-ttu-id="39387-604">Function group</span><span class="sxs-lookup"><span data-stu-id="39387-604">Function group</span></span>          | <span data-ttu-id="39387-605">Operations</span><span class="sxs-lookup"><span data-stu-id="39387-605">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="39387-606">Mathematical functions</span><span class="sxs-lookup"><span data-stu-id="39387-606">Mathematical functions</span></span>  | <span data-ttu-id="39387-607">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span><span class="sxs-lookup"><span data-stu-id="39387-607">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="39387-608">Type checking functions</span><span class="sxs-lookup"><span data-stu-id="39387-608">Type checking functions</span></span> | <span data-ttu-id="39387-609">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="39387-609">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="39387-610">String functions</span><span class="sxs-lookup"><span data-stu-id="39387-610">String functions</span></span>        | <span data-ttu-id="39387-611">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span><span class="sxs-lookup"><span data-stu-id="39387-611">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="39387-612">Array functions</span><span class="sxs-lookup"><span data-stu-id="39387-612">Array functions</span></span>         | <span data-ttu-id="39387-613">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="39387-613">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="39387-614">Spatial functions</span><span class="sxs-lookup"><span data-stu-id="39387-614">Spatial functions</span></span>       | <span data-ttu-id="39387-615">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="39387-615">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="39387-616">If you’re currently using a user defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span><span class="sxs-lookup"><span data-stu-id="39387-616">If you’re currently using a user defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="39387-617">Mathematical functions</span><span class="sxs-lookup"><span data-stu-id="39387-617">Mathematical functions</span></span>
<span data-ttu-id="39387-618">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span><span class="sxs-lookup"><span data-stu-id="39387-618">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="39387-619">Here’s a table of supported built-in mathematical functions.</span><span class="sxs-lookup"><span data-stu-id="39387-619">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="39387-620">Usage</span><span class="sxs-lookup"><span data-stu-id="39387-620">Usage</span></span> | <span data-ttu-id="39387-621">Description</span><span class="sxs-lookup"><span data-stu-id="39387-621">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="39387-622">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="39387-622">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="39387-623">Returns the absolute (positive) value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-623">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-624">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-624">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="39387-625">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-625">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-626">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-626">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="39387-627">Returns the largest integer less than or equal to the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-627">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-628">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-628">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="39387-629">Returns the exponent of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-629">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="39387-630">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="39387-630">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="39387-631">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span><span class="sxs-lookup"><span data-stu-id="39387-631">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="39387-632">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-632">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="39387-633">Returns the base-10 logarithmic value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-633">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-634">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-634">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="39387-635">Returns a numeric value, rounded to the closest integer value.</span><span class="sxs-lookup"><span data-stu-id="39387-635">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="39387-636">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-636">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="39387-637">Returns a numeric value, truncated to the closest integer value.</span><span class="sxs-lookup"><span data-stu-id="39387-637">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="39387-638">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-638">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="39387-639">Returns the square root of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-639">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-640">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-640">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="39387-641">Returns the square of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-641">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-642">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-642">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="39387-643">Returns the power of the specified numeric expression to the value specifed.</span><span class="sxs-lookup"><span data-stu-id="39387-643">Returns the power of the specified numeric expression to the value specifed.</span></span> |
| [<span data-ttu-id="39387-644">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-644">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="39387-645">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-645">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-646">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-646">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="39387-647">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span><span class="sxs-lookup"><span data-stu-id="39387-647">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="39387-648">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-648">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="39387-649">Returns the angle, in radians, whose sine is the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-649">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="39387-650">This is also called arcsine.</span><span class="sxs-lookup"><span data-stu-id="39387-650">This is also called arcsine.</span></span> |
| [<span data-ttu-id="39387-651">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-651">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="39387-652">Returns the angle, in radians, whose tangent is the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-652">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="39387-653">This is also called arctangent.</span><span class="sxs-lookup"><span data-stu-id="39387-653">This is also called arctangent.</span></span> |
| [<span data-ttu-id="39387-654">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-654">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="39387-655">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span><span class="sxs-lookup"><span data-stu-id="39387-655">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="39387-656">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-656">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="39387-657">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="39387-657">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="39387-658">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-658">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="39387-659">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="39387-659">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="39387-660">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-660">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="39387-661">Returns the corresponding angle in degrees for an angle specified in radians.</span><span class="sxs-lookup"><span data-stu-id="39387-661">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="39387-662">PI ()</span><span class="sxs-lookup"><span data-stu-id="39387-662">PI ()</span></span>](#bk_pi) | <span data-ttu-id="39387-663">Returns the constant value of PI.</span><span class="sxs-lookup"><span data-stu-id="39387-663">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="39387-664">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-664">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="39387-665">Returns radians when a numeric expression, in degrees, is entered.</span><span class="sxs-lookup"><span data-stu-id="39387-665">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="39387-666">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-666">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="39387-667">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="39387-667">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="39387-668">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-668">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="39387-669">Returns the tangent of the input expression, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="39387-669">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="39387-670">For example, you can now run queries like the following:</span><span class="sxs-lookup"><span data-stu-id="39387-670">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="39387-671">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-671">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="39387-672">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-672">**Results**</span></span>

    [4]

<span data-ttu-id="39387-673">The main difference between DocumentDB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span><span class="sxs-lookup"><span data-stu-id="39387-673">The main difference between DocumentDB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="39387-674">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span><span class="sxs-lookup"><span data-stu-id="39387-674">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="39387-675">Type checking functions</span><span class="sxs-lookup"><span data-stu-id="39387-675">Type checking functions</span></span>
<span data-ttu-id="39387-676">The type checking functions allow you to check the type of an expression within SQL queries.</span><span class="sxs-lookup"><span data-stu-id="39387-676">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="39387-677">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span><span class="sxs-lookup"><span data-stu-id="39387-677">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="39387-678">Here’s a table of supported built-in type checking functions.</span><span class="sxs-lookup"><span data-stu-id="39387-678">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="39387-679"><strong>Usage</strong></span><span class="sxs-lookup"><span data-stu-id="39387-679"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="39387-680"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="39387-680"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-681"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-681"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-682">Returns a Boolean indicating if the type of the value is an array.</span><span class="sxs-lookup"><span data-stu-id="39387-682">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-683"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-683"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-684">Returns a Boolean indicating if the type of the value is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="39387-684">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-685"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-685"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-686">Returns a Boolean indicating if the type of the value is null.</span><span class="sxs-lookup"><span data-stu-id="39387-686">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-687"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-687"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-688">Returns a Boolean indicating if the type of the value is a number.</span><span class="sxs-lookup"><span data-stu-id="39387-688">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-689"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-689"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-690">Returns a Boolean indicating if the type of the value is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="39387-690">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-691"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-691"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-692">Returns a Boolean indicating if the type of the value is a string.</span><span class="sxs-lookup"><span data-stu-id="39387-692">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-693"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-693"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-694">Returns a Boolean indicating if the property has been assigned a value.</span><span class="sxs-lookup"><span data-stu-id="39387-694">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-695"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="39387-695"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="39387-696">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span><span class="sxs-lookup"><span data-stu-id="39387-696">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="39387-697">Using these functions, you can now run queries like the following:</span><span class="sxs-lookup"><span data-stu-id="39387-697">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="39387-698">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-698">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="39387-699">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-699">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="39387-700">String functions</span><span class="sxs-lookup"><span data-stu-id="39387-700">String functions</span></span>
<span data-ttu-id="39387-701">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span><span class="sxs-lookup"><span data-stu-id="39387-701">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="39387-702">Here's a table of built-in string functions:</span><span class="sxs-lookup"><span data-stu-id="39387-702">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="39387-703">Usage</span><span class="sxs-lookup"><span data-stu-id="39387-703">Usage</span></span> | <span data-ttu-id="39387-704">Description</span><span class="sxs-lookup"><span data-stu-id="39387-704">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="39387-705">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-705">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="39387-706">Returns the number of characters of the specified string expression</span><span class="sxs-lookup"><span data-stu-id="39387-706">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="39387-707">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="39387-707">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="39387-708">Returns a string that is the result of concatenating two or more string values.</span><span class="sxs-lookup"><span data-stu-id="39387-708">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="39387-709">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-709">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="39387-710">Returns part of a string expression.</span><span class="sxs-lookup"><span data-stu-id="39387-710">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="39387-711">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-711">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="39387-712">Returns a Boolean indicating whether the first string expression ends with the second</span><span class="sxs-lookup"><span data-stu-id="39387-712">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="39387-713">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-713">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="39387-714">Returns a Boolean indicating whether the first string expression ends with the second</span><span class="sxs-lookup"><span data-stu-id="39387-714">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="39387-715">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-715">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="39387-716">Returns a Boolean indicating whether the first string expression contains the second.</span><span class="sxs-lookup"><span data-stu-id="39387-716">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="39387-717">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-717">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="39387-718">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="39387-718">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="39387-719">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-719">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="39387-720">Returns the left part of a string with the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="39387-720">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="39387-721">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-721">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="39387-722">Returns the right part of a string with the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="39387-722">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="39387-723">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-723">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="39387-724">Returns a string expression after it removes leading blanks.</span><span class="sxs-lookup"><span data-stu-id="39387-724">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="39387-725">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-725">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="39387-726">Returns a string expression after truncating all trailing blanks.</span><span class="sxs-lookup"><span data-stu-id="39387-726">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="39387-727">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-727">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="39387-728">Returns a string expression after converting uppercase character data to lowercase.</span><span class="sxs-lookup"><span data-stu-id="39387-728">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="39387-729">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-729">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="39387-730">Returns a string expression after converting lowercase character data to uppercase.</span><span class="sxs-lookup"><span data-stu-id="39387-730">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="39387-731">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-731">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="39387-732">Replaces all occurrences of a specified string value with another string value.</span><span class="sxs-lookup"><span data-stu-id="39387-732">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="39387-733">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-733">REPLICATE (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replicate) |<span data-ttu-id="39387-734">Repeats a string value a specified number of times.</span><span class="sxs-lookup"><span data-stu-id="39387-734">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="39387-735">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-735">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="39387-736">Returns the reverse order of a string value.</span><span class="sxs-lookup"><span data-stu-id="39387-736">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="39387-737">Using these functions, you can now run queries like the following.</span><span class="sxs-lookup"><span data-stu-id="39387-737">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="39387-738">For example, you can return the family name in uppercase as follows:</span><span class="sxs-lookup"><span data-stu-id="39387-738">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="39387-739">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-739">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="39387-740">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-740">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="39387-741">Or concatenate strings like in this example:</span><span class="sxs-lookup"><span data-stu-id="39387-741">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="39387-742">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-742">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="39387-743">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-743">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="39387-744">String functions can also be used in the WHERE clause to filter results, like in the following example:</span><span class="sxs-lookup"><span data-stu-id="39387-744">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="39387-745">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-745">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="39387-746">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-746">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="39387-747">Array functions</span><span class="sxs-lookup"><span data-stu-id="39387-747">Array functions</span></span>
<span data-ttu-id="39387-748">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span><span class="sxs-lookup"><span data-stu-id="39387-748">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="39387-749">Here's a table of built-in array functions:</span><span class="sxs-lookup"><span data-stu-id="39387-749">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="39387-750">Usage</span><span class="sxs-lookup"><span data-stu-id="39387-750">Usage</span></span> | <span data-ttu-id="39387-751">Description</span><span class="sxs-lookup"><span data-stu-id="39387-751">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="39387-752">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-752">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="39387-753">Returns the number of elements of the specified array expression.</span><span class="sxs-lookup"><span data-stu-id="39387-753">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="39387-754">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="39387-754">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="39387-755">Returns an array that is the result of concatenating two or more array values.</span><span class="sxs-lookup"><span data-stu-id="39387-755">Returns an array that is the result of concatenating two or more array values.</span></span> |
| [<span data-ttu-id="39387-756">ARRAY_CONTAINS (arr_expr, expr)</span><span class="sxs-lookup"><span data-stu-id="39387-756">ARRAY_CONTAINS (arr_expr, expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |<span data-ttu-id="39387-757">Returns a Boolean indicating whether the array contains the specified value.</span><span class="sxs-lookup"><span data-stu-id="39387-757">Returns a Boolean indicating whether the array contains the specified value.</span></span> |
| <span data-ttu-id="39387-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="39387-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="39387-759">Returns part of an array expression.</span><span class="sxs-lookup"><span data-stu-id="39387-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="39387-760">Array functions can be used to manipulate arrays within JSON.</span><span class="sxs-lookup"><span data-stu-id="39387-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="39387-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="39387-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="39387-762">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="39387-763">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="39387-764">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span><span class="sxs-lookup"><span data-stu-id="39387-764">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="39387-765">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-765">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="39387-766">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-766">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="39387-767">Spatial functions</span><span class="sxs-lookup"><span data-stu-id="39387-767">Spatial functions</span></span>
<span data-ttu-id="39387-768">DocumentDB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span><span class="sxs-lookup"><span data-stu-id="39387-768">DocumentDB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="39387-769"><strong>Usage</strong></span><span class="sxs-lookup"><span data-stu-id="39387-769"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="39387-770"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="39387-770"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-771">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-771">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="39387-772">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span><span class="sxs-lookup"><span data-stu-id="39387-772">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-773">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-773">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="39387-774">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span><span class="sxs-lookup"><span data-stu-id="39387-774">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-775">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="39387-775">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="39387-776">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="39387-776">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-777">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="39387-777">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="39387-778">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span><span class="sxs-lookup"><span data-stu-id="39387-778">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="39387-779">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="39387-779">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="39387-780">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span><span class="sxs-lookup"><span data-stu-id="39387-780">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="39387-781">Spatial functions can be used to perform proximity queries against spatial data.</span><span class="sxs-lookup"><span data-stu-id="39387-781">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="39387-782">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span><span class="sxs-lookup"><span data-stu-id="39387-782">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="39387-783">**Query**</span><span class="sxs-lookup"><span data-stu-id="39387-783">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="39387-784">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-784">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="39387-785">For more details on geospatial support in DocumentDB, please see [Working with geospatial data in Azure DocumentDB](documentdb-geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="39387-785">For more details on geospatial support in DocumentDB, please see [Working with geospatial data in Azure DocumentDB](documentdb-geospatial.md).</span></span> <span data-ttu-id="39387-786">That wraps up spatial functions, and the SQL syntax for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="39387-786">That wraps up spatial functions, and the SQL syntax for DocumentDB.</span></span> <span data-ttu-id="39387-787">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span><span class="sxs-lookup"><span data-stu-id="39387-787">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <a id="Linq"></a><span data-ttu-id="39387-788">LINQ to DocumentDB SQL</span><span class="sxs-lookup"><span data-stu-id="39387-788">LINQ to DocumentDB SQL</span></span>
<span data-ttu-id="39387-789">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span><span class="sxs-lookup"><span data-stu-id="39387-789">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="39387-790">DocumentDB provides a client side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to DocumentDB queries.</span><span class="sxs-lookup"><span data-stu-id="39387-790">DocumentDB provides a client side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to DocumentDB queries.</span></span> 

<span data-ttu-id="39387-791">The picture below shows the architecture of supporting LINQ queries using DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="39387-791">The picture below shows the architecture of supporting LINQ queries using DocumentDB.</span></span>  <span data-ttu-id="39387-792">Using the DocumentDB client, developers can create an **IQueryable** object that directly queries the DocumentDB query provider, which then translates the LINQ query into a DocumentDB query.</span><span class="sxs-lookup"><span data-stu-id="39387-792">Using the DocumentDB client, developers can create an **IQueryable** object that directly queries the DocumentDB query provider, which then translates the LINQ query into a DocumentDB query.</span></span> <span data-ttu-id="39387-793">The query is then passed to the DocumentDB server to retrieve a set of results in JSON format.</span><span class="sxs-lookup"><span data-stu-id="39387-793">The query is then passed to the DocumentDB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="39387-794">The returned results are deserialized into a stream of .NET objects on the client side.</span><span class="sxs-lookup"><span data-stu-id="39387-794">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Architecture of supporting LINQ queries using DocumentDB - SQL syntax, JSON query language, database concepts and SQL queries][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="39387-796">.NET and JSON mapping</span><span class="sxs-lookup"><span data-stu-id="39387-796">.NET and JSON mapping</span></span>
<span data-ttu-id="39387-797">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span><span class="sxs-lookup"><span data-stu-id="39387-797">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="39387-798">Consider the following example.</span><span class="sxs-lookup"><span data-stu-id="39387-798">Consider the following example.</span></span> <span data-ttu-id="39387-799">The Family object created is mapped to the JSON document as shown below.</span><span class="sxs-lookup"><span data-stu-id="39387-799">The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="39387-800">And vice versa, the JSON document is mapped back to a .NET object.</span><span class="sxs-lookup"><span data-stu-id="39387-800">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="39387-801">**C# Class**</span><span class="sxs-lookup"><span data-stu-id="39387-801">**C# Class**</span></span>

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


<span data-ttu-id="39387-802">**JSON**</span><span class="sxs-lookup"><span data-stu-id="39387-802">**JSON**</span></span>  

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



### <a name="linq-to-sql-translation"></a><span data-ttu-id="39387-803">LINQ to SQL translation</span><span class="sxs-lookup"><span data-stu-id="39387-803">LINQ to SQL translation</span></span>
<span data-ttu-id="39387-804">The DocumentDB query provider performs a best effort mapping from a LINQ query into a DocumentDB SQL query.</span><span class="sxs-lookup"><span data-stu-id="39387-804">The DocumentDB query provider performs a best effort mapping from a LINQ query into a DocumentDB SQL query.</span></span> <span data-ttu-id="39387-805">In the following description, we assume the reader has a basic familiarity of LINQ.</span><span class="sxs-lookup"><span data-stu-id="39387-805">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="39387-806">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span><span class="sxs-lookup"><span data-stu-id="39387-806">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="39387-807">Only these JSON types are supported.</span><span class="sxs-lookup"><span data-stu-id="39387-807">Only these JSON types are supported.</span></span> <span data-ttu-id="39387-808">The following scalar expressions are supported.</span><span class="sxs-lookup"><span data-stu-id="39387-808">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="39387-809">Constant values – these includes constant values of the primitive data types at the time the query is evaluated.</span><span class="sxs-lookup"><span data-stu-id="39387-809">Constant values – these includes constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="39387-810">Property/array index expressions – these expressions refer to the property of an object or an array element.</span><span class="sxs-lookup"><span data-stu-id="39387-810">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="39387-811">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span><span class="sxs-lookup"><span data-stu-id="39387-811">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="39387-812">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span><span class="sxs-lookup"><span data-stu-id="39387-812">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="39387-813">For the complete list, refer to the SQL specification.</span><span class="sxs-lookup"><span data-stu-id="39387-813">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="39387-814">2 \* family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="39387-814">2 \* family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="39387-815">String comparison expression - these include comparing a string value to some constant string value.</span><span class="sxs-lookup"><span data-stu-id="39387-815">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="39387-816">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span><span class="sxs-lookup"><span data-stu-id="39387-816">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="39387-817">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span><span class="sxs-lookup"><span data-stu-id="39387-817">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="39387-818">These values can be nested.</span><span class="sxs-lookup"><span data-stu-id="39387-818">These values can be nested.</span></span>
  
     <span data-ttu-id="39387-819">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with 2 fields</span><span class="sxs-lookup"><span data-stu-id="39387-819">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with 2 fields</span></span>              
     <span data-ttu-id="39387-820">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="39387-820">new int[] { 3, child.grade, 5 };</span></span>

### <a id="SupportedLinqOperators"></a><span data-ttu-id="39387-821">List of supported LINQ operators</span><span class="sxs-lookup"><span data-stu-id="39387-821">List of supported LINQ operators</span></span>
<span data-ttu-id="39387-822">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="39387-822">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="39387-823">**Select**: Projections translate to the SQL SELECT including object construction</span><span class="sxs-lookup"><span data-stu-id="39387-823">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="39387-824">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span><span class="sxs-lookup"><span data-stu-id="39387-824">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="39387-825">to the SQL operators</span><span class="sxs-lookup"><span data-stu-id="39387-825">to the SQL operators</span></span>
* <span data-ttu-id="39387-826">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span><span class="sxs-lookup"><span data-stu-id="39387-826">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="39387-827">Can be used to chain/nest expressions to filter on array elements</span><span class="sxs-lookup"><span data-stu-id="39387-827">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="39387-828">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span><span class="sxs-lookup"><span data-stu-id="39387-828">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="39387-829">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="39387-829">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="39387-830">**CompareTo**: Translates to range comparisons.</span><span class="sxs-lookup"><span data-stu-id="39387-830">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="39387-831">Commonly used for strings since they’re not comparable in .NET</span><span class="sxs-lookup"><span data-stu-id="39387-831">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="39387-832">**Take**: Translates to the SQL TOP for limiting results from a query</span><span class="sxs-lookup"><span data-stu-id="39387-832">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="39387-833">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="39387-833">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="39387-834">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="39387-834">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="39387-835">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="39387-835">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="39387-836">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span><span class="sxs-lookup"><span data-stu-id="39387-836">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="39387-837">**User Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user defined function.</span><span class="sxs-lookup"><span data-stu-id="39387-837">**User Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user defined function.</span></span>
* <span data-ttu-id="39387-838">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span><span class="sxs-lookup"><span data-stu-id="39387-838">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="39387-839">Can translate Contains to String CONTAINS, ARRAY_CONTAINS or the SQL IN depending on context.</span><span class="sxs-lookup"><span data-stu-id="39387-839">Can translate Contains to String CONTAINS, ARRAY_CONTAINS or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="39387-840">SQL query operators</span><span class="sxs-lookup"><span data-stu-id="39387-840">SQL query operators</span></span>
<span data-ttu-id="39387-841">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to DocumentDB queries.</span><span class="sxs-lookup"><span data-stu-id="39387-841">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to DocumentDB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="39387-842">Select Operator</span><span class="sxs-lookup"><span data-stu-id="39387-842">Select Operator</span></span>
<span data-ttu-id="39387-843">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span><span class="sxs-lookup"><span data-stu-id="39387-843">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="39387-844">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-844">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="39387-845">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-845">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="39387-846">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-846">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="39387-847">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-847">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="39387-848">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-848">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="39387-849">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-849">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="39387-850">SelectMany operator</span><span class="sxs-lookup"><span data-stu-id="39387-850">SelectMany operator</span></span>
<span data-ttu-id="39387-851">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span><span class="sxs-lookup"><span data-stu-id="39387-851">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="39387-852">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-852">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="39387-853">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-853">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="39387-854">Where operator</span><span class="sxs-lookup"><span data-stu-id="39387-854">Where operator</span></span>
<span data-ttu-id="39387-855">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression which returns a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="39387-855">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression which returns a Boolean value.</span></span>

<span data-ttu-id="39387-856">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-856">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="39387-857">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-857">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="39387-858">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-858">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="39387-859">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-859">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="39387-860">Composite SQL queries</span><span class="sxs-lookup"><span data-stu-id="39387-860">Composite SQL queries</span></span>
<span data-ttu-id="39387-861">The above operators can be composed to form more powerful queries.</span><span class="sxs-lookup"><span data-stu-id="39387-861">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="39387-862">Since DocumentDB supports nested collections, the composition can either be concatenated or nested.</span><span class="sxs-lookup"><span data-stu-id="39387-862">Since DocumentDB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="39387-863">Concatenation</span><span class="sxs-lookup"><span data-stu-id="39387-863">Concatenation</span></span>
<span data-ttu-id="39387-864">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="39387-864">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="39387-865">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span><span class="sxs-lookup"><span data-stu-id="39387-865">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="39387-866">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-866">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="39387-867">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-867">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="39387-868">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-868">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="39387-869">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-869">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="39387-870">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-870">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="39387-871">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-871">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="39387-872">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-872">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="39387-873">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-873">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="39387-874">Nesting</span><span class="sxs-lookup"><span data-stu-id="39387-874">Nesting</span></span>
<span data-ttu-id="39387-875">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span><span class="sxs-lookup"><span data-stu-id="39387-875">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="39387-876">In a nested query, the inner query is applied to each element of the outer collection.</span><span class="sxs-lookup"><span data-stu-id="39387-876">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="39387-877">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span><span class="sxs-lookup"><span data-stu-id="39387-877">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="39387-878">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-878">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="39387-879">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-879">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="39387-880">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-880">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="39387-881">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-881">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="39387-882">**LINQ lambda expression**</span><span class="sxs-lookup"><span data-stu-id="39387-882">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="39387-883">**SQL**</span><span class="sxs-lookup"><span data-stu-id="39387-883">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a><span data-ttu-id="39387-884">Executing SQL queries</span><span class="sxs-lookup"><span data-stu-id="39387-884">Executing SQL queries</span></span>
<span data-ttu-id="39387-885">DocumentDB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span><span class="sxs-lookup"><span data-stu-id="39387-885">DocumentDB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="39387-886">Additionally, DocumentDB offers programming libraries for several popular languages like .NET, Node.js, JavaScript and Python.</span><span class="sxs-lookup"><span data-stu-id="39387-886">Additionally, DocumentDB offers programming libraries for several popular languages like .NET, Node.js, JavaScript and Python.</span></span> <span data-ttu-id="39387-887">The REST API and the various libraries all support querying through SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-887">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="39387-888">The .NET SDK supports LINQ querying in addition to SQL.</span><span class="sxs-lookup"><span data-stu-id="39387-888">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="39387-889">The following examples show how to create a query and submit it against a DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="39387-889">The following examples show how to create a query and submit it against a DocumentDB database account.</span></span>

### <a id="RestAPI"></a><span data-ttu-id="39387-890">REST API</span><span class="sxs-lookup"><span data-stu-id="39387-890">REST API</span></span>
<span data-ttu-id="39387-891">DocumentDB offers an open RESTful programming model over HTTP.</span><span class="sxs-lookup"><span data-stu-id="39387-891">DocumentDB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="39387-892">Database accounts can be provisioned using an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="39387-892">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="39387-893">The DocumentDB resource model consists of a sets of resources under a database account, each  of which is addressable using a logical and stable URI.</span><span class="sxs-lookup"><span data-stu-id="39387-893">The DocumentDB resource model consists of a sets of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="39387-894">A set of resources is referred to as a feed in this document.</span><span class="sxs-lookup"><span data-stu-id="39387-894">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="39387-895">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span><span class="sxs-lookup"><span data-stu-id="39387-895">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="39387-896">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST and DELETE with their standard interpretation.</span><span class="sxs-lookup"><span data-stu-id="39387-896">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST and DELETE with their standard interpretation.</span></span> <span data-ttu-id="39387-897">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a DocumentDB query.</span><span class="sxs-lookup"><span data-stu-id="39387-897">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a DocumentDB query.</span></span> <span data-ttu-id="39387-898">Queries are always read only operations with no side-effects.</span><span class="sxs-lookup"><span data-stu-id="39387-898">Queries are always read only operations with no side-effects.</span></span>

<span data-ttu-id="39387-899">The following examples show a POST for a DocumentDB query made against a collection containing the two sample documents we've reviewed so far.</span><span class="sxs-lookup"><span data-stu-id="39387-899">The following examples show a POST for a DocumentDB query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="39387-900">The query has a simple filter on the JSON name property.</span><span class="sxs-lookup"><span data-stu-id="39387-900">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="39387-901">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span><span class="sxs-lookup"><span data-stu-id="39387-901">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="39387-902">**Request**</span><span class="sxs-lookup"><span data-stu-id="39387-902">**Request**</span></span>

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


<span data-ttu-id="39387-903">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-903">**Results**</span></span>

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


<span data-ttu-id="39387-904">The second example shows a more complex query that returns multiple results from the join.</span><span class="sxs-lookup"><span data-stu-id="39387-904">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="39387-905">**Request**</span><span class="sxs-lookup"><span data-stu-id="39387-905">**Request**</span></span>

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


<span data-ttu-id="39387-906">**Results**</span><span class="sxs-lookup"><span data-stu-id="39387-906">**Results**</span></span>

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


<span data-ttu-id="39387-907">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span><span class="sxs-lookup"><span data-stu-id="39387-907">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="39387-908">Clients can paginate results by including the header in subsequent results.</span><span class="sxs-lookup"><span data-stu-id="39387-908">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="39387-909">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span><span class="sxs-lookup"><span data-stu-id="39387-909">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="39387-910">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span><span class="sxs-lookup"><span data-stu-id="39387-910">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="39387-911">The clients must perform a second level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span><span class="sxs-lookup"><span data-stu-id="39387-911">The clients must perform a second level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="39387-912">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span><span class="sxs-lookup"><span data-stu-id="39387-912">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="39387-913">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span><span class="sxs-lookup"><span data-stu-id="39387-913">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="39387-914">Note that the queried collection's indexing policy can also influence the consistency of query results.</span><span class="sxs-lookup"><span data-stu-id="39387-914">Note that the queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="39387-915">With the default indexing policy settings, for collections the index is always current with the document contents and query results will match the consistency chosen for data.</span><span class="sxs-lookup"><span data-stu-id="39387-915">With the default indexing policy settings, for collections the index is always current with the document contents and query results will match the consistency chosen for data.</span></span> <span data-ttu-id="39387-916">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span><span class="sxs-lookup"><span data-stu-id="39387-916">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="39387-917">For more information, refer to [DocumentDB Consistency Levels][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="39387-917">For more information, refer to [DocumentDB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="39387-918">If the configured indexing policy on the collection cannot support the specified query, the DocumentDB server returns 400 "Bad Request".</span><span class="sxs-lookup"><span data-stu-id="39387-918">If the configured indexing policy on the collection cannot support the specified query, the DocumentDB server returns 400 "Bad Request".</span></span> <span data-ttu-id="39387-919">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span><span class="sxs-lookup"><span data-stu-id="39387-919">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="39387-920">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span><span class="sxs-lookup"><span data-stu-id="39387-920">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

### <a id="DotNetSdk"></a><span data-ttu-id="39387-921">C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="39387-921">C# (.NET) SDK</span></span>
<span data-ttu-id="39387-922">The .NET SDK supports both LINQ and SQL querying.</span><span class="sxs-lookup"><span data-stu-id="39387-922">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="39387-923">The following example shows how to perform the simple filter query introduced earlier in this document.</span><span class="sxs-lookup"><span data-stu-id="39387-923">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="39387-924">This sample compares two properties for equality within each document and uses anonymous projections.</span><span class="sxs-lookup"><span data-stu-id="39387-924">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="39387-925">The next sample shows joins, expressed through LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="39387-925">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="39387-926">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span><span class="sxs-lookup"><span data-stu-id="39387-926">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="39387-927">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span><span class="sxs-lookup"><span data-stu-id="39387-927">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="39387-928">The number of pages can be controlled using the `MaxItemCount` setting.</span><span class="sxs-lookup"><span data-stu-id="39387-928">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="39387-929">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="39387-929">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="39387-930">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span><span class="sxs-lookup"><span data-stu-id="39387-930">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="39387-931">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though DocumentDB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="39387-931">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though DocumentDB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="39387-932">Refer to [DocumentDB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span><span class="sxs-lookup"><span data-stu-id="39387-932">Refer to [DocumentDB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="39387-933">In order to perform aggregation queries, you need SDKs 1.12.0 or above.</span><span class="sxs-lookup"><span data-stu-id="39387-933">In order to perform aggregation queries, you need SDKs 1.12.0 or above.</span></span> <span data-ttu-id="39387-934">LINQ support for aggregation functions is not supported but will be available in .NET SDK 1.13.0.</span><span class="sxs-lookup"><span data-stu-id="39387-934">LINQ support for aggregation functions is not supported but will be available in .NET SDK 1.13.0.</span></span>
>

### <a id="JavaScriptServerSideApi"></a><span data-ttu-id="39387-935">JavaScript server-side API</span><span class="sxs-lookup"><span data-stu-id="39387-935">JavaScript server-side API</span></span>
<span data-ttu-id="39387-936">DocumentDB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="39387-936">DocumentDB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="39387-937">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span><span class="sxs-lookup"><span data-stu-id="39387-937">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="39387-938">These operations are wrapped in ambient ACID transactions.</span><span class="sxs-lookup"><span data-stu-id="39387-938">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="39387-939">The following example show how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="39387-939">The following example show how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

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

## <a id="References"></a><span data-ttu-id="39387-940">References</span><span class="sxs-lookup"><span data-stu-id="39387-940">References</span></span>
1. <span data-ttu-id="39387-941">[Introduction to Azure DocumentDB][introduction]</span><span class="sxs-lookup"><span data-stu-id="39387-941">[Introduction to Azure DocumentDB][introduction]</span></span>
2. [<span data-ttu-id="39387-942">DocumentDB SQL specification</span><span class="sxs-lookup"><span data-stu-id="39387-942">DocumentDB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="39387-943">DocumentDB .NET samples</span><span class="sxs-lookup"><span data-stu-id="39387-943">DocumentDB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="39387-944">[DocumentDB Consistency Levels][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="39387-944">[DocumentDB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="39387-945">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="39387-945">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="39387-946">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="39387-946">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="39387-947">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="39387-947">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="39387-948">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="39387-948">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="39387-949">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="39387-949">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="39387-950">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="39387-950">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="39387-951">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="39387-951">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="39387-952">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="39387-952">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="39387-953">G.</span><span class="sxs-lookup"><span data-stu-id="39387-953">G.</span></span> <span data-ttu-id="39387-954">Graefe.</span><span class="sxs-lookup"><span data-stu-id="39387-954">Graefe.</span></span> <span data-ttu-id="39387-955">The Cascades framework for query optimization.</span><span class="sxs-lookup"><span data-stu-id="39387-955">The Cascades framework for query optimization.</span></span> <span data-ttu-id="39387-956">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="39387-956">IEEE Data Eng.</span></span> <span data-ttu-id="39387-957">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="39387-957">Bull., 18(3): 1995.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-sql-query/sql-query1.png
[introduction]: documentdb-introduction.md
[consistency-levels]: documentdb-consistency-levels.md

