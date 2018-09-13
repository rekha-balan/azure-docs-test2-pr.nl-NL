---
title: 'Azure Cosmos DB: SQL syntax query reference | Microsoft Docs'
description: Reference documentation for the Azure Cosmos DB SQL query language.
services: cosmos-db
author: LalithaMV
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: na
ms.topic: reference
ms.date: 08/19/2018
ms.author: laviswa
ms.openlocfilehash: 33614628926e53354db14886530d7ca44da61f0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865895"
---
# <a name="azure-cosmos-db-sql-syntax-reference"></a><span data-ttu-id="29937-103">Azure Cosmos DB SQL syntax reference</span><span class="sxs-lookup"><span data-stu-id="29937-103">Azure Cosmos DB SQL syntax reference</span></span>

<span data-ttu-id="29937-104">Azure Cosmos DB supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span><span class="sxs-lookup"><span data-stu-id="29937-104">Azure Cosmos DB supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="29937-105">This article provides reference/syntax documentation for the SQL query language, which is compatible with SQL API accounts.</span><span class="sxs-lookup"><span data-stu-id="29937-105">This article provides reference/syntax documentation for the SQL query language, which is compatible with SQL API accounts.</span></span> <span data-ttu-id="29937-106">For a walkthrough of the SQL queries with sample data see [query Azure Cosmos DB data](sql-api-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="29937-106">For a walkthrough of the SQL queries with sample data see [query Azure Cosmos DB data](sql-api-sql-query.md).</span></span>  
  
<span data-ttu-id="29937-107">Visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span><span class="sxs-lookup"><span data-stu-id="29937-107">Visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="29937-108">SELECT query</span><span class="sxs-lookup"><span data-stu-id="29937-108">SELECT query</span></span>  
<span data-ttu-id="29937-109">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span><span class="sxs-lookup"><span data-stu-id="29937-109">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="29937-110">Typically, for each query, the source in the FROM clause is enumerated.</span><span class="sxs-lookup"><span data-stu-id="29937-110">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="29937-111">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="29937-111">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="29937-112">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span><span class="sxs-lookup"><span data-stu-id="29937-112">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span> <span data-ttu-id="29937-113">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span><span class="sxs-lookup"><span data-stu-id="29937-113">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span> <span data-ttu-id="29937-114">For examples, see [SELECT query examples](sql-api-sql-query.md#SelectClause)</span><span class="sxs-lookup"><span data-stu-id="29937-114">For examples, see [SELECT query examples](sql-api-sql-query.md#SelectClause)</span></span>
  
<span data-ttu-id="29937-115">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-115">**Syntax**</span></span>  
  
```sql
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="29937-116">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-116">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-117">See following sections for details on each clause:</span><span class="sxs-lookup"><span data-stu-id="29937-117">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="29937-118">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="29937-118">SELECT clause</span></span>](#bk_select_query)    
-   [<span data-ttu-id="29937-119">FROM clause</span><span class="sxs-lookup"><span data-stu-id="29937-119">FROM clause</span></span>](#bk_from_clause)    
-   [<span data-ttu-id="29937-120">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="29937-120">WHERE clause</span></span>](#bk_where_clause)    
-   [<span data-ttu-id="29937-121">ORDER BY clause</span><span class="sxs-lookup"><span data-stu-id="29937-121">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="29937-122">The clauses in the SELECT statement must be ordered as shown above.</span><span class="sxs-lookup"><span data-stu-id="29937-122">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="29937-123">Any one of the optional clauses can be omitted.</span><span class="sxs-lookup"><span data-stu-id="29937-123">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="29937-124">But when optional clauses are used, they must appear in the right order.</span><span class="sxs-lookup"><span data-stu-id="29937-124">But when optional clauses are used, they must appear in the right order.</span></span>  
  
### <a name="logical-processing-order-of-the-select-statement"></a><span data-ttu-id="29937-125">Logical Processing Order of the SELECT statement</span><span class="sxs-lookup"><span data-stu-id="29937-125">Logical Processing Order of the SELECT statement</span></span>  
  
<span data-ttu-id="29937-126">The order in which clauses are processed is:</span><span class="sxs-lookup"><span data-stu-id="29937-126">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="29937-127">FROM clause</span><span class="sxs-lookup"><span data-stu-id="29937-127">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="29937-128">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="29937-128">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="29937-129">ORDER BY clause</span><span class="sxs-lookup"><span data-stu-id="29937-129">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="29937-130">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="29937-130">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="29937-131">Note that this is different from the order in which they appear in the syntax.</span><span class="sxs-lookup"><span data-stu-id="29937-131">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="29937-132">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span><span class="sxs-lookup"><span data-stu-id="29937-132">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="29937-133">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span><span class="sxs-lookup"><span data-stu-id="29937-133">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

### <a name="whitespace-characters-and-comments"></a><span data-ttu-id="29937-134">Whitespace characters and comments</span><span class="sxs-lookup"><span data-stu-id="29937-134">Whitespace characters and comments</span></span>  

<span data-ttu-id="29937-135">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span><span class="sxs-lookup"><span data-stu-id="29937-135">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="29937-136">The query language supports T-SQL style comments like</span><span class="sxs-lookup"><span data-stu-id="29937-136">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="29937-137">SQL Statement `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="29937-137">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="29937-138">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span><span class="sxs-lookup"><span data-stu-id="29937-138">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="29937-139">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span><span class="sxs-lookup"><span data-stu-id="29937-139">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <a name="bk_select_query"></a> <span data-ttu-id="29937-140">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="29937-140">SELECT clause</span></span>  
<span data-ttu-id="29937-141">The clauses in the SELECT statement must be ordered as shown above.</span><span class="sxs-lookup"><span data-stu-id="29937-141">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="29937-142">Any one of the optional clauses can be omitted.</span><span class="sxs-lookup"><span data-stu-id="29937-142">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="29937-143">But when optional clauses are used, they must appear in the right order.</span><span class="sxs-lookup"><span data-stu-id="29937-143">But when optional clauses are used, they must appear in the right order.</span></span> <span data-ttu-id="29937-144">For examples, see [SELECT query examples](sql-api-sql-query.md#SelectClause)</span><span class="sxs-lookup"><span data-stu-id="29937-144">For examples, see [SELECT query examples](sql-api-sql-query.md#SelectClause)</span></span>

<span data-ttu-id="29937-145">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-145">**Syntax**</span></span>  

```sql
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="29937-146">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-146">**Arguments**</span></span>  
  
- `<select_specification>`  

  <span data-ttu-id="29937-147">Properties or value to be selected for the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-147">Properties or value to be selected for the result set.</span></span>  
  
- `'*'`  

  <span data-ttu-id="29937-148">Specifies that the value should be retrieved without making any changes.</span><span class="sxs-lookup"><span data-stu-id="29937-148">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="29937-149">Specifically if the processed value is an object, all properties will be retrieved.</span><span class="sxs-lookup"><span data-stu-id="29937-149">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
- `<object_property_list>`  
  
  <span data-ttu-id="29937-150">Specifies the list of properties to be retrieved.</span><span class="sxs-lookup"><span data-stu-id="29937-150">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="29937-151">Each returned value will be an object with the properties specified.</span><span class="sxs-lookup"><span data-stu-id="29937-151">Each returned value will be an object with the properties specified.</span></span>  
  
- `VALUE`  

  <span data-ttu-id="29937-152">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span><span class="sxs-lookup"><span data-stu-id="29937-152">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="29937-153">This, unlike `<property_list>` does not wrap the projected value in an object.</span><span class="sxs-lookup"><span data-stu-id="29937-153">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
- `<scalar_expression>`  

  <span data-ttu-id="29937-154">Expression representing the value to be computed.</span><span class="sxs-lookup"><span data-stu-id="29937-154">Expression representing the value to be computed.</span></span> <span data-ttu-id="29937-155">See [Scalar expressions](#bk_scalar_expressions) section for details.</span><span class="sxs-lookup"><span data-stu-id="29937-155">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="29937-156">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-156">**Remarks**</span></span>  
  
<span data-ttu-id="29937-157">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span><span class="sxs-lookup"><span data-stu-id="29937-157">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="29937-158">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span><span class="sxs-lookup"><span data-stu-id="29937-158">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="29937-159">SELECT \* is only valid if FROM clause is specified and introduced only a single input source.</span><span class="sxs-lookup"><span data-stu-id="29937-159">SELECT \* is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="29937-160">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span><span class="sxs-lookup"><span data-stu-id="29937-160">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1. `SELECT * FROM ... AS from_alias ...`  
  
   <span data-ttu-id="29937-161">is equivalent to:</span><span class="sxs-lookup"><span data-stu-id="29937-161">is equivalent to:</span></span>  
  
   `SELECT from_alias FROM ... AS from_alias ...`  
  
2. `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
   <span data-ttu-id="29937-162">is equivalent to:</span><span class="sxs-lookup"><span data-stu-id="29937-162">is equivalent to:</span></span>  
  
   `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="29937-163">**See Also**</span><span class="sxs-lookup"><span data-stu-id="29937-163">**See Also**</span></span>  
  
[<span data-ttu-id="29937-164">Scalar expressions</span><span class="sxs-lookup"><span data-stu-id="29937-164">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="29937-165">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="29937-165">SELECT clause</span></span>](#bk_select_query)  
  
##  <a name="bk_from_clause"></a> <span data-ttu-id="29937-166">FROM clause</span><span class="sxs-lookup"><span data-stu-id="29937-166">FROM clause</span></span>  
<span data-ttu-id="29937-167">Specifies the source or joined sources.</span><span class="sxs-lookup"><span data-stu-id="29937-167">Specifies the source or joined sources.</span></span> <span data-ttu-id="29937-168">The FROM clause is optional unless the source is filtered or projected later in the query.</span><span class="sxs-lookup"><span data-stu-id="29937-168">The FROM clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="29937-169">The purpose of this clause is to specify the data source upon which the query must operate.</span><span class="sxs-lookup"><span data-stu-id="29937-169">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="29937-170">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span><span class="sxs-lookup"><span data-stu-id="29937-170">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> <span data-ttu-id="29937-171">If this clause is not specified, other clauses will still be executed as if FROM clause provided a single document.</span><span class="sxs-lookup"><span data-stu-id="29937-171">If this clause is not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span> <span data-ttu-id="29937-172">For examples, see [FROM clause examples](sql-api-sql-query.md#FromClause)</span><span class="sxs-lookup"><span data-stu-id="29937-172">For examples, see [FROM clause examples](sql-api-sql-query.md#FromClause)</span></span>
  
<span data-ttu-id="29937-173">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-173">**Syntax**</span></span>  
  
```sql  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="29937-174">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-174">**Arguments**</span></span>  
  
- `<from_source>`  
  
  <span data-ttu-id="29937-175">Specifies a data source, with or without an alias.</span><span class="sxs-lookup"><span data-stu-id="29937-175">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="29937-176">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span><span class="sxs-lookup"><span data-stu-id="29937-176">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
  -  <span data-ttu-id="29937-177">If the expression is a collection_name, then collection_name will be used as an alias.</span><span class="sxs-lookup"><span data-stu-id="29937-177">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
  -  <span data-ttu-id="29937-178">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span><span class="sxs-lookup"><span data-stu-id="29937-178">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="29937-179">If the expression is a collection_name, then collection_name will be used as an alias.</span><span class="sxs-lookup"><span data-stu-id="29937-179">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
- <span data-ttu-id="29937-180">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="29937-180">AS `input_alias`</span></span>  
  
  <span data-ttu-id="29937-181">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span><span class="sxs-lookup"><span data-stu-id="29937-181">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
- <span data-ttu-id="29937-182">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="29937-182">`input_alias` IN</span></span>  
  
  <span data-ttu-id="29937-183">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span><span class="sxs-lookup"><span data-stu-id="29937-183">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="29937-184">Any value returned by underlying collection expression that is not an array is ignored.</span><span class="sxs-lookup"><span data-stu-id="29937-184">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
- `<collection_expression>`  
  
  <span data-ttu-id="29937-185">Specifies the collection expression to be used to retrieve the documents.</span><span class="sxs-lookup"><span data-stu-id="29937-185">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
- `ROOT`  
  
  <span data-ttu-id="29937-186">Specifies that document should be retrieved from the default, currently connected collection.</span><span class="sxs-lookup"><span data-stu-id="29937-186">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
- `collection_name`  
  
  <span data-ttu-id="29937-187">Specifies that document should be retrieved from the provided collection.</span><span class="sxs-lookup"><span data-stu-id="29937-187">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="29937-188">The name of the collection must match the name of the collection currently connected to.</span><span class="sxs-lookup"><span data-stu-id="29937-188">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
- `input_alias`  
  
  <span data-ttu-id="29937-189">Specifies that document should be retrieved from the other source defined by the provided alias.</span><span class="sxs-lookup"><span data-stu-id="29937-189">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
- `<collection_expression> '.' property_`  
  
  <span data-ttu-id="29937-190">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span><span class="sxs-lookup"><span data-stu-id="29937-190">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
- `<collection_expression> '[' "property_name" | array_index ']'`  
  
  <span data-ttu-id="29937-191">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span><span class="sxs-lookup"><span data-stu-id="29937-191">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="29937-192">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-192">**Remarks**</span></span>  
  
<span data-ttu-id="29937-193">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span><span class="sxs-lookup"><span data-stu-id="29937-193">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="29937-194">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="29937-194">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="29937-195">However, the latter syntax can be used if a property name contains a non-identifier characters.</span><span class="sxs-lookup"><span data-stu-id="29937-195">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
### <a name="handling-missing-properties-missing-array-elements-and-undefined-values"></a><span data-ttu-id="29937-196">handling missing properties, missing array elements, and undefined values</span><span class="sxs-lookup"><span data-stu-id="29937-196">handling missing properties, missing array elements, and undefined values</span></span>
  
<span data-ttu-id="29937-197">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span><span class="sxs-lookup"><span data-stu-id="29937-197">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
### <a name="collection-expression-context-scoping"></a><span data-ttu-id="29937-198">Collection expression context scoping</span><span class="sxs-lookup"><span data-stu-id="29937-198">Collection expression context scoping</span></span>  
  
<span data-ttu-id="29937-199">A collection expression may be collection-scoped or document-scoped:</span><span class="sxs-lookup"><span data-stu-id="29937-199">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="29937-200">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="29937-200">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="29937-201">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span><span class="sxs-lookup"><span data-stu-id="29937-201">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="29937-202">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span><span class="sxs-lookup"><span data-stu-id="29937-202">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="29937-203">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span><span class="sxs-lookup"><span data-stu-id="29937-203">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="29937-204">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span><span class="sxs-lookup"><span data-stu-id="29937-204">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
### <a name="joins"></a><span data-ttu-id="29937-205">Joins</span><span class="sxs-lookup"><span data-stu-id="29937-205">Joins</span></span> 
  
<span data-ttu-id="29937-206">In the current release, Azure Cosmos DB supports inner joins.</span><span class="sxs-lookup"><span data-stu-id="29937-206">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="29937-207">Additional join capabilities are forthcoming.</span><span class="sxs-lookup"><span data-stu-id="29937-207">Additional join capabilities are forthcoming.</span></span> 

<span data-ttu-id="29937-208">Inner joins result in a complete cross product of the sets participating in the join.</span><span class="sxs-lookup"><span data-stu-id="29937-208">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="29937-209">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span><span class="sxs-lookup"><span data-stu-id="29937-209">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span> <span data-ttu-id="29937-210">For examples, see [JOIN keyword examples](sql-api-sql-query.md#Joins)</span><span class="sxs-lookup"><span data-stu-id="29937-210">For examples, see [JOIN keyword examples](sql-api-sql-query.md#Joins)</span></span>
  
<span data-ttu-id="29937-211">The evaluation of the join depends on the context scope of the participating sets:</span><span class="sxs-lookup"><span data-stu-id="29937-211">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="29937-212">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span><span class="sxs-lookup"><span data-stu-id="29937-212">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="29937-213">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span><span class="sxs-lookup"><span data-stu-id="29937-213">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="29937-214">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span><span class="sxs-lookup"><span data-stu-id="29937-214">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
### <a name="examples-of-joins"></a><span data-ttu-id="29937-215">Examples of joins</span><span class="sxs-lookup"><span data-stu-id="29937-215">Examples of joins</span></span>  
  
<span data-ttu-id="29937-216">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="29937-216">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="29937-217">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="29937-217">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="29937-218">This FROM clause returns a set of N-tuples (tuple with N values).</span><span class="sxs-lookup"><span data-stu-id="29937-218">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="29937-219">Each tuple has values produced by iterating all collection aliases over their respective sets.</span><span class="sxs-lookup"><span data-stu-id="29937-219">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="29937-220">**Example 1** - 2 sources</span><span class="sxs-lookup"><span data-stu-id="29937-220">**Example 1** - 2 sources</span></span>  
  
- <span data-ttu-id="29937-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="29937-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="29937-222">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span><span class="sxs-lookup"><span data-stu-id="29937-222">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="29937-223">{1, 2} for `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="29937-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="29937-224">{3} for `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="29937-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="29937-225">{4, 5} for `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="29937-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="29937-226">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span><span class="sxs-lookup"><span data-stu-id="29937-226">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="29937-227">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="29937-227">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="29937-228">**Example 2** - 3 sources</span><span class="sxs-lookup"><span data-stu-id="29937-228">**Example 2** - 3 sources</span></span>  
  
- <span data-ttu-id="29937-229">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="29937-229">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="29937-230">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span><span class="sxs-lookup"><span data-stu-id="29937-230">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="29937-231">{1, 2} for `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="29937-231">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="29937-232">{3} for `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="29937-232">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="29937-233">{4, 5} for `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="29937-233">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="29937-234">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span><span class="sxs-lookup"><span data-stu-id="29937-234">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="29937-235">{100, 200} for `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="29937-235">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="29937-236">{300} for `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="29937-236">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="29937-237">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span><span class="sxs-lookup"><span data-stu-id="29937-237">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="29937-238">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="29937-238">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="29937-239">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="29937-239">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
  > [!NOTE]
  > <span data-ttu-id="29937-240">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span><span class="sxs-lookup"><span data-stu-id="29937-240">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="29937-241">**Example 3** - 3 sources</span><span class="sxs-lookup"><span data-stu-id="29937-241">**Example 3** - 3 sources</span></span>  
  
- <span data-ttu-id="29937-242">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="29937-242">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="29937-243">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="29937-243">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="29937-244">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span><span class="sxs-lookup"><span data-stu-id="29937-244">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="29937-245">{1, 2} for `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="29937-245">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="29937-246">{3} for `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="29937-246">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="29937-247">{4, 5} for `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="29937-247">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="29937-248">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span><span class="sxs-lookup"><span data-stu-id="29937-248">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="29937-249">{100, 200} for `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="29937-249">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="29937-250">{300} for `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="29937-250">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="29937-251">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span><span class="sxs-lookup"><span data-stu-id="29937-251">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="29937-252">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="29937-252">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="29937-253">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="29937-253">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
  > [!NOTE]
  > <span data-ttu-id="29937-254">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="29937-254">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="29937-255">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span><span class="sxs-lookup"><span data-stu-id="29937-255">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="29937-256">**See also**</span><span class="sxs-lookup"><span data-stu-id="29937-256">**See also**</span></span>  
  
 [<span data-ttu-id="29937-257">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="29937-257">SELECT clause</span></span>](#bk_select_query)  
  
##  <a name="bk_where_clause"></a> <span data-ttu-id="29937-258">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="29937-258">WHERE clause</span></span>  
 <span data-ttu-id="29937-259">Specifies the search condition for the documents returned by the query.</span><span class="sxs-lookup"><span data-stu-id="29937-259">Specifies the search condition for the documents returned by the query.</span></span> <span data-ttu-id="29937-260">For examples, see [WHERE clause examples](sql-api-sql-query.md#WhereClause)</span><span class="sxs-lookup"><span data-stu-id="29937-260">For examples, see [WHERE clause examples](sql-api-sql-query.md#WhereClause)</span></span>
  
 <span data-ttu-id="29937-261">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-261">**Syntax**</span></span>  
  
```sql  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="29937-262">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-262">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="29937-263">Specifies the condition to be met for the documents to be returned.</span><span class="sxs-lookup"><span data-stu-id="29937-263">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="29937-264">Expression representing the value to be computed.</span><span class="sxs-lookup"><span data-stu-id="29937-264">Expression representing the value to be computed.</span></span> <span data-ttu-id="29937-265">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span><span class="sxs-lookup"><span data-stu-id="29937-265">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="29937-266">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-266">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-267">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span><span class="sxs-lookup"><span data-stu-id="29937-267">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="29937-268">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span><span class="sxs-lookup"><span data-stu-id="29937-268">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <a name="bk_orderby_clause"></a> <span data-ttu-id="29937-269">ORDER BY clause</span><span class="sxs-lookup"><span data-stu-id="29937-269">ORDER BY clause</span></span>  
 <span data-ttu-id="29937-270">Specifies the sorting order for results returned by the query.</span><span class="sxs-lookup"><span data-stu-id="29937-270">Specifies the sorting order for results returned by the query.</span></span> <span data-ttu-id="29937-271">For examples, see [ORDER BY clause examples](sql-api-sql-query.md#OrderByClause)</span><span class="sxs-lookup"><span data-stu-id="29937-271">For examples, see [ORDER BY clause examples](sql-api-sql-query.md#OrderByClause)</span></span>
  
 <span data-ttu-id="29937-272">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-272">**Syntax**</span></span>  
  
```sql  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="29937-273">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-273">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="29937-274">Specifies a property or expression on which to sort the query result set.</span><span class="sxs-lookup"><span data-stu-id="29937-274">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="29937-275">A sort column can be specified as a name or column alias.</span><span class="sxs-lookup"><span data-stu-id="29937-275">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="29937-276">Multiple sort columns can be specified.</span><span class="sxs-lookup"><span data-stu-id="29937-276">Multiple sort columns can be specified.</span></span> <span data-ttu-id="29937-277">Column names must be unique.</span><span class="sxs-lookup"><span data-stu-id="29937-277">Column names must be unique.</span></span> <span data-ttu-id="29937-278">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span><span class="sxs-lookup"><span data-stu-id="29937-278">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="29937-279">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span><span class="sxs-lookup"><span data-stu-id="29937-279">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="29937-280">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span><span class="sxs-lookup"><span data-stu-id="29937-280">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="29937-281">Specifies a single property or expression on which to sort the query result set.</span><span class="sxs-lookup"><span data-stu-id="29937-281">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="29937-282">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span><span class="sxs-lookup"><span data-stu-id="29937-282">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="29937-283">Specifies that the values in the specified column should be sorted in ascending or descending order.</span><span class="sxs-lookup"><span data-stu-id="29937-283">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="29937-284">ASC sorts from the lowest value to highest value.</span><span class="sxs-lookup"><span data-stu-id="29937-284">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="29937-285">DESC sorts from highest value to lowest value.</span><span class="sxs-lookup"><span data-stu-id="29937-285">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="29937-286">ASC is the default sort order.</span><span class="sxs-lookup"><span data-stu-id="29937-286">ASC is the default sort order.</span></span> <span data-ttu-id="29937-287">Null values are treated as the lowest possible values.</span><span class="sxs-lookup"><span data-stu-id="29937-287">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="29937-288">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-288">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-289">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span><span class="sxs-lookup"><span data-stu-id="29937-289">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="29937-290">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span><span class="sxs-lookup"><span data-stu-id="29937-290">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="29937-291">Refer to the indexing policy documentation for more details.</span><span class="sxs-lookup"><span data-stu-id="29937-291">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <a name="bk_scalar_expressions"></a> <span data-ttu-id="29937-292">Scalar expressions</span><span class="sxs-lookup"><span data-stu-id="29937-292">Scalar expressions</span></span>  
 <span data-ttu-id="29937-293">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span><span class="sxs-lookup"><span data-stu-id="29937-293">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="29937-294">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span><span class="sxs-lookup"><span data-stu-id="29937-294">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="29937-295">Simple expressions can be combined into complex expressions using operators.</span><span class="sxs-lookup"><span data-stu-id="29937-295">Simple expressions can be combined into complex expressions using operators.</span></span> <span data-ttu-id="29937-296">For examples, see [scalar expressions examples](sql-api-sql-query.md#scalar-expressions)</span><span class="sxs-lookup"><span data-stu-id="29937-296">For examples, see [scalar expressions examples](sql-api-sql-query.md#scalar-expressions)</span></span>
  
 <span data-ttu-id="29937-297">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span><span class="sxs-lookup"><span data-stu-id="29937-297">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="29937-298">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-298">**Syntax**</span></span>  
  
```sql  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="29937-299">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-299">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="29937-300">Represents a constant value.</span><span class="sxs-lookup"><span data-stu-id="29937-300">Represents a constant value.</span></span> <span data-ttu-id="29937-301">See [Constants](#bk_constants) section for details.</span><span class="sxs-lookup"><span data-stu-id="29937-301">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="29937-302">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span><span class="sxs-lookup"><span data-stu-id="29937-302">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="29937-303">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span><span class="sxs-lookup"><span data-stu-id="29937-303">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="29937-304">Represents a value of the property of an object.</span><span class="sxs-lookup"><span data-stu-id="29937-304">Represents a value of the property of an object.</span></span> <span data-ttu-id="29937-305">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span><span class="sxs-lookup"><span data-stu-id="29937-305">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="29937-306">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span><span class="sxs-lookup"><span data-stu-id="29937-306">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="29937-307">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span><span class="sxs-lookup"><span data-stu-id="29937-307">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="29937-308">Represents an operator that is applied to a single value.</span><span class="sxs-lookup"><span data-stu-id="29937-308">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="29937-309">See [Operators](#bk_operators) section for details.</span><span class="sxs-lookup"><span data-stu-id="29937-309">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="29937-310">Represents an operator that is applied to two values.</span><span class="sxs-lookup"><span data-stu-id="29937-310">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="29937-311">See [Operators](#bk_operators) section for details.</span><span class="sxs-lookup"><span data-stu-id="29937-311">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="29937-312">Represents a value defined by a result of a function call.</span><span class="sxs-lookup"><span data-stu-id="29937-312">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="29937-313">Name of the user defined scalar function.</span><span class="sxs-lookup"><span data-stu-id="29937-313">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="29937-314">Name of the built-in scalar function.</span><span class="sxs-lookup"><span data-stu-id="29937-314">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="29937-315">Represents a value obtained by creating a new object with specified properties and their values.</span><span class="sxs-lookup"><span data-stu-id="29937-315">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="29937-316">Represents a value obtained by creating a new array with specified values as elements</span><span class="sxs-lookup"><span data-stu-id="29937-316">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="29937-317">Represents a value of the specified parameter name.</span><span class="sxs-lookup"><span data-stu-id="29937-317">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="29937-318">Parameter names must have a single \@ as the first character.</span><span class="sxs-lookup"><span data-stu-id="29937-318">Parameter names must have a single \@ as the first character.</span></span>  
  
 <span data-ttu-id="29937-319">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-319">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-320">When calling a built-in or user defined scalar function all arguments must be defined.</span><span class="sxs-lookup"><span data-stu-id="29937-320">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="29937-321">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-321">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="29937-322">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span><span class="sxs-lookup"><span data-stu-id="29937-322">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="29937-323">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span><span class="sxs-lookup"><span data-stu-id="29937-323">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="29937-324">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span><span class="sxs-lookup"><span data-stu-id="29937-324">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <a name="bk_operators"></a> <span data-ttu-id="29937-325">Operators</span><span class="sxs-lookup"><span data-stu-id="29937-325">Operators</span></span>  
 <span data-ttu-id="29937-326">This section describes the supported operators.</span><span class="sxs-lookup"><span data-stu-id="29937-326">This section describes the supported operators.</span></span> <span data-ttu-id="29937-327">Each operator can be assigned to exactly one category.</span><span class="sxs-lookup"><span data-stu-id="29937-327">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="29937-328">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span><span class="sxs-lookup"><span data-stu-id="29937-328">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="29937-329">**Operator categories:**</span><span class="sxs-lookup"><span data-stu-id="29937-329">**Operator categories:**</span></span>  
  
|<span data-ttu-id="29937-330">**Category**</span><span class="sxs-lookup"><span data-stu-id="29937-330">**Category**</span></span>|<span data-ttu-id="29937-331">**Details**</span><span class="sxs-lookup"><span data-stu-id="29937-331">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="29937-332">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="29937-332">**arithmetic**</span></span>|<span data-ttu-id="29937-333">Operator expects input(s) to be Number(s).</span><span class="sxs-lookup"><span data-stu-id="29937-333">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="29937-334">Output is also a Number.</span><span class="sxs-lookup"><span data-stu-id="29937-334">Output is also a Number.</span></span> <span data-ttu-id="29937-335">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span><span class="sxs-lookup"><span data-stu-id="29937-335">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="29937-336">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="29937-336">**bitwise**</span></span>|<span data-ttu-id="29937-337">Operator expects input(s) to be 32-bit signed integer Number(s).</span><span class="sxs-lookup"><span data-stu-id="29937-337">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="29937-338">Output is also 32-bit signed integer Number.</span><span class="sxs-lookup"><span data-stu-id="29937-338">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="29937-339">Any non-integer value will be rounded.</span><span class="sxs-lookup"><span data-stu-id="29937-339">Any non-integer value will be rounded.</span></span> <span data-ttu-id="29937-340">Positive value will be rounded down, negative values rounded up.</span><span class="sxs-lookup"><span data-stu-id="29937-340">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="29937-341">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span><span class="sxs-lookup"><span data-stu-id="29937-341">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="29937-342">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span><span class="sxs-lookup"><span data-stu-id="29937-342">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="29937-343">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span><span class="sxs-lookup"><span data-stu-id="29937-343">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="29937-344">**logical**</span><span class="sxs-lookup"><span data-stu-id="29937-344">**logical**</span></span>|<span data-ttu-id="29937-345">Operator expects input(s) to be Boolean(s).</span><span class="sxs-lookup"><span data-stu-id="29937-345">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="29937-346">Output is also a Boolean.</span><span class="sxs-lookup"><span data-stu-id="29937-346">Output is also a Boolean.</span></span><br /><span data-ttu-id="29937-347">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span><span class="sxs-lookup"><span data-stu-id="29937-347">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="29937-348">**comparison**</span><span class="sxs-lookup"><span data-stu-id="29937-348">**comparison**</span></span>|<span data-ttu-id="29937-349">Operator expects input(s) to have the same type and not be undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-349">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="29937-350">Output is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="29937-350">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="29937-351">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span><span class="sxs-lookup"><span data-stu-id="29937-351">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="29937-352">See **Ordering of values for comparison** table for value ordering details.</span><span class="sxs-lookup"><span data-stu-id="29937-352">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="29937-353">**string**</span><span class="sxs-lookup"><span data-stu-id="29937-353">**string**</span></span>|<span data-ttu-id="29937-354">Operator expects input(s) to be String(s).</span><span class="sxs-lookup"><span data-stu-id="29937-354">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="29937-355">Output is also a String.</span><span class="sxs-lookup"><span data-stu-id="29937-355">Output is also a String.</span></span><br /><span data-ttu-id="29937-356">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span><span class="sxs-lookup"><span data-stu-id="29937-356">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="29937-357">**Unary operators:**</span><span class="sxs-lookup"><span data-stu-id="29937-357">**Unary operators:**</span></span>  
  
|<span data-ttu-id="29937-358">**Name**</span><span class="sxs-lookup"><span data-stu-id="29937-358">**Name**</span></span>|<span data-ttu-id="29937-359">**Operator**</span><span class="sxs-lookup"><span data-stu-id="29937-359">**Operator**</span></span>|<span data-ttu-id="29937-360">**Details**</span><span class="sxs-lookup"><span data-stu-id="29937-360">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="29937-361">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="29937-361">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="29937-362">Returns the number value.</span><span class="sxs-lookup"><span data-stu-id="29937-362">Returns the number value.</span></span><br /><br /> <span data-ttu-id="29937-363">Bitwise negation.</span><span class="sxs-lookup"><span data-stu-id="29937-363">Bitwise negation.</span></span> <span data-ttu-id="29937-364">Returns negated number value.</span><span class="sxs-lookup"><span data-stu-id="29937-364">Returns negated number value.</span></span>|  
|<span data-ttu-id="29937-365">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="29937-365">**bitwise**</span></span>|~|<span data-ttu-id="29937-366">Ones' complement.</span><span class="sxs-lookup"><span data-stu-id="29937-366">Ones' complement.</span></span> <span data-ttu-id="29937-367">Returns a complement of a number value.</span><span class="sxs-lookup"><span data-stu-id="29937-367">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="29937-368">**Logical**</span><span class="sxs-lookup"><span data-stu-id="29937-368">**Logical**</span></span>|<span data-ttu-id="29937-369">**NOT**</span><span class="sxs-lookup"><span data-stu-id="29937-369">**NOT**</span></span>|<span data-ttu-id="29937-370">Negation.</span><span class="sxs-lookup"><span data-stu-id="29937-370">Negation.</span></span> <span data-ttu-id="29937-371">Returns negated Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-371">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="29937-372">**Binary operators:**</span><span class="sxs-lookup"><span data-stu-id="29937-372">**Binary operators:**</span></span>  
  
|<span data-ttu-id="29937-373">**Name**</span><span class="sxs-lookup"><span data-stu-id="29937-373">**Name**</span></span>|<span data-ttu-id="29937-374">**Operator**</span><span class="sxs-lookup"><span data-stu-id="29937-374">**Operator**</span></span>|<span data-ttu-id="29937-375">**Details**</span><span class="sxs-lookup"><span data-stu-id="29937-375">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="29937-376">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="29937-376">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="29937-377">Addition.</span><span class="sxs-lookup"><span data-stu-id="29937-377">Addition.</span></span><br /><br /> <span data-ttu-id="29937-378">Subtraction.</span><span class="sxs-lookup"><span data-stu-id="29937-378">Subtraction.</span></span><br /><br /> <span data-ttu-id="29937-379">Multiplication.</span><span class="sxs-lookup"><span data-stu-id="29937-379">Multiplication.</span></span><br /><br /> <span data-ttu-id="29937-380">Division.</span><span class="sxs-lookup"><span data-stu-id="29937-380">Division.</span></span><br /><br /> <span data-ttu-id="29937-381">Modulation.</span><span class="sxs-lookup"><span data-stu-id="29937-381">Modulation.</span></span>|  
|<span data-ttu-id="29937-382">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="29937-382">**bitwise**</span></span>|<span data-ttu-id="29937-383">&#124;</span><span class="sxs-lookup"><span data-stu-id="29937-383">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="29937-384">Bitwise OR.</span><span class="sxs-lookup"><span data-stu-id="29937-384">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="29937-385">Bitwise AND.</span><span class="sxs-lookup"><span data-stu-id="29937-385">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="29937-386">Bitwise XOR.</span><span class="sxs-lookup"><span data-stu-id="29937-386">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="29937-387">Left Shift.</span><span class="sxs-lookup"><span data-stu-id="29937-387">Left Shift.</span></span><br /><br /> <span data-ttu-id="29937-388">Right Shift.</span><span class="sxs-lookup"><span data-stu-id="29937-388">Right Shift.</span></span><br /><br /> <span data-ttu-id="29937-389">Zero-fill Right Shift.</span><span class="sxs-lookup"><span data-stu-id="29937-389">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="29937-390">**logical**</span><span class="sxs-lookup"><span data-stu-id="29937-390">**logical**</span></span>|<span data-ttu-id="29937-391">**AND**</span><span class="sxs-lookup"><span data-stu-id="29937-391">**AND**</span></span><br /><br /> <span data-ttu-id="29937-392">**OR**</span><span class="sxs-lookup"><span data-stu-id="29937-392">**OR**</span></span>|<span data-ttu-id="29937-393">Logical conjunction.</span><span class="sxs-lookup"><span data-stu-id="29937-393">Logical conjunction.</span></span> <span data-ttu-id="29937-394">Returns **true** if both arguments are **true**, returns **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-394">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-395">Logical conjunction.</span><span class="sxs-lookup"><span data-stu-id="29937-395">Logical conjunction.</span></span> <span data-ttu-id="29937-396">Returns **true** if both arguments are **true**, returns **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-396">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="29937-397">**comparison**</span><span class="sxs-lookup"><span data-stu-id="29937-397">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="29937-398">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="29937-398">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="29937-399">**??**</span><span class="sxs-lookup"><span data-stu-id="29937-399">**??**</span></span>|<span data-ttu-id="29937-400">Equals.</span><span class="sxs-lookup"><span data-stu-id="29937-400">Equals.</span></span> <span data-ttu-id="29937-401">Returns **true** if arguments are equal, returns **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-401">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-402">Not equal to.</span><span class="sxs-lookup"><span data-stu-id="29937-402">Not equal to.</span></span> <span data-ttu-id="29937-403">Returns **true** if arguments are not equal, returns **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-403">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-404">Greater Than.</span><span class="sxs-lookup"><span data-stu-id="29937-404">Greater Than.</span></span> <span data-ttu-id="29937-405">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-405">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-406">Greater Than or Equal To.</span><span class="sxs-lookup"><span data-stu-id="29937-406">Greater Than or Equal To.</span></span> <span data-ttu-id="29937-407">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-407">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-408">Less Than.</span><span class="sxs-lookup"><span data-stu-id="29937-408">Less Than.</span></span> <span data-ttu-id="29937-409">Returns **true** if first argument is less than the second one, return **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-409">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-410">Less Than or Equal To.</span><span class="sxs-lookup"><span data-stu-id="29937-410">Less Than or Equal To.</span></span> <span data-ttu-id="29937-411">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-411">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="29937-412">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="29937-412">Coalesce.</span></span> <span data-ttu-id="29937-413">Returns the second argument if the first argument is an **undefined** value.</span><span class="sxs-lookup"><span data-stu-id="29937-413">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="29937-414">**String**</span><span class="sxs-lookup"><span data-stu-id="29937-414">**String**</span></span>|<span data-ttu-id="29937-415">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="29937-415">**&#124;&#124;**</span></span>|<span data-ttu-id="29937-416">Concatenation.</span><span class="sxs-lookup"><span data-stu-id="29937-416">Concatenation.</span></span> <span data-ttu-id="29937-417">Returns a concatenation of both arguments.</span><span class="sxs-lookup"><span data-stu-id="29937-417">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="29937-418">**Ternary operators:**</span><span class="sxs-lookup"><span data-stu-id="29937-418">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="29937-419">Ternary operator</span><span class="sxs-lookup"><span data-stu-id="29937-419">Ternary operator</span></span>|<span data-ttu-id="29937-420">?</span><span class="sxs-lookup"><span data-stu-id="29937-420">?</span></span>|<span data-ttu-id="29937-421">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span><span class="sxs-lookup"><span data-stu-id="29937-421">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="29937-422">**Ordering of values for comparison**</span><span class="sxs-lookup"><span data-stu-id="29937-422">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="29937-423">**Type**</span><span class="sxs-lookup"><span data-stu-id="29937-423">**Type**</span></span>|<span data-ttu-id="29937-424">**Values order**</span><span class="sxs-lookup"><span data-stu-id="29937-424">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="29937-425">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="29937-425">**Undefined**</span></span>|<span data-ttu-id="29937-426">Not comparable.</span><span class="sxs-lookup"><span data-stu-id="29937-426">Not comparable.</span></span>|  
|<span data-ttu-id="29937-427">**Null**</span><span class="sxs-lookup"><span data-stu-id="29937-427">**Null**</span></span>|<span data-ttu-id="29937-428">Single value: **null**</span><span class="sxs-lookup"><span data-stu-id="29937-428">Single value: **null**</span></span>|  
|<span data-ttu-id="29937-429">**Number**</span><span class="sxs-lookup"><span data-stu-id="29937-429">**Number**</span></span>|<span data-ttu-id="29937-430">Natural real number.</span><span class="sxs-lookup"><span data-stu-id="29937-430">Natural real number.</span></span><br /><br /> <span data-ttu-id="29937-431">Negative Infinity value is smaller than any other Number value.</span><span class="sxs-lookup"><span data-stu-id="29937-431">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="29937-432">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span><span class="sxs-lookup"><span data-stu-id="29937-432">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="29937-433">Comparing with **NaN** will result in **undefined** value.</span><span class="sxs-lookup"><span data-stu-id="29937-433">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="29937-434">**String**</span><span class="sxs-lookup"><span data-stu-id="29937-434">**String**</span></span>|<span data-ttu-id="29937-435">Lexicographical order.</span><span class="sxs-lookup"><span data-stu-id="29937-435">Lexicographical order.</span></span>|  
|<span data-ttu-id="29937-436">**Array**</span><span class="sxs-lookup"><span data-stu-id="29937-436">**Array**</span></span>|<span data-ttu-id="29937-437">No ordering, but equitable.</span><span class="sxs-lookup"><span data-stu-id="29937-437">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="29937-438">**Object**</span><span class="sxs-lookup"><span data-stu-id="29937-438">**Object**</span></span>|<span data-ttu-id="29937-439">No ordering, but equitable.</span><span class="sxs-lookup"><span data-stu-id="29937-439">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="29937-440">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-440">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-441">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span><span class="sxs-lookup"><span data-stu-id="29937-441">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="29937-442">In order to support efficient execution of queries, most of the operators have strict type requirements.</span><span class="sxs-lookup"><span data-stu-id="29937-442">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="29937-443">Also operators by themselves do not perform implicit conversions.</span><span class="sxs-lookup"><span data-stu-id="29937-443">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="29937-444">This means that a query like: SELECT \* FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span><span class="sxs-lookup"><span data-stu-id="29937-444">This means that a query like: SELECT \* FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="29937-445">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-445">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="29937-446">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span><span class="sxs-lookup"><span data-stu-id="29937-446">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="29937-447">This is different from how JavaScript evaluates operators on values of different types.</span><span class="sxs-lookup"><span data-stu-id="29937-447">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="29937-448">**Arrays and objects equality and comparison**</span><span class="sxs-lookup"><span data-stu-id="29937-448">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="29937-449">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span><span class="sxs-lookup"><span data-stu-id="29937-449">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="29937-450">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span><span class="sxs-lookup"><span data-stu-id="29937-450">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="29937-451">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span><span class="sxs-lookup"><span data-stu-id="29937-451">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="29937-452">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-452">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="29937-453">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span><span class="sxs-lookup"><span data-stu-id="29937-453">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="29937-454">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-454">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <a name="bk_constants"></a> <span data-ttu-id="29937-455">Constants</span><span class="sxs-lookup"><span data-stu-id="29937-455">Constants</span></span>  
 <span data-ttu-id="29937-456">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span><span class="sxs-lookup"><span data-stu-id="29937-456">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="29937-457">The format of a constant depends on the data type of the value it represents.</span><span class="sxs-lookup"><span data-stu-id="29937-457">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="29937-458">**Supported scalar data types:**</span><span class="sxs-lookup"><span data-stu-id="29937-458">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="29937-459">**Type**</span><span class="sxs-lookup"><span data-stu-id="29937-459">**Type**</span></span>|<span data-ttu-id="29937-460">**Values order**</span><span class="sxs-lookup"><span data-stu-id="29937-460">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="29937-461">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="29937-461">**Undefined**</span></span>|<span data-ttu-id="29937-462">Single value: **undefined**</span><span class="sxs-lookup"><span data-stu-id="29937-462">Single value: **undefined**</span></span>|  
|<span data-ttu-id="29937-463">**Null**</span><span class="sxs-lookup"><span data-stu-id="29937-463">**Null**</span></span>|<span data-ttu-id="29937-464">Single value: **null**</span><span class="sxs-lookup"><span data-stu-id="29937-464">Single value: **null**</span></span>|  
|<span data-ttu-id="29937-465">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="29937-465">**Boolean**</span></span>|<span data-ttu-id="29937-466">Values: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="29937-466">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="29937-467">**Number**</span><span class="sxs-lookup"><span data-stu-id="29937-467">**Number**</span></span>|<span data-ttu-id="29937-468">A double-precision floating-point number, IEEE 754 standard.</span><span class="sxs-lookup"><span data-stu-id="29937-468">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="29937-469">**String**</span><span class="sxs-lookup"><span data-stu-id="29937-469">**String**</span></span>|<span data-ttu-id="29937-470">A sequence of zero or more Unicode characters.</span><span class="sxs-lookup"><span data-stu-id="29937-470">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="29937-471">Strings must be enclosed in single or double quotes.</span><span class="sxs-lookup"><span data-stu-id="29937-471">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="29937-472">**Array**</span><span class="sxs-lookup"><span data-stu-id="29937-472">**Array**</span></span>|<span data-ttu-id="29937-473">A sequence of zero or more elements.</span><span class="sxs-lookup"><span data-stu-id="29937-473">A sequence of zero or more elements.</span></span> <span data-ttu-id="29937-474">Each element can be a value of any scalar data type, except Undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-474">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="29937-475">**Object**</span><span class="sxs-lookup"><span data-stu-id="29937-475">**Object**</span></span>|<span data-ttu-id="29937-476">An unordered set of zero or more name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="29937-476">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="29937-477">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="29937-477">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="29937-478">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-478">**Syntax**</span></span>  
  
```sql  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="29937-479">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-479">**Arguments**</span></span>  
  
* `<undefined_constant>; undefined`  
  
  <span data-ttu-id="29937-480">Represents undefined value of type Undefined.</span><span class="sxs-lookup"><span data-stu-id="29937-480">Represents undefined value of type Undefined.</span></span>  
  
* `<null_constant>; null`  
  
  <span data-ttu-id="29937-481">Represents **null** value of type **Null**.</span><span class="sxs-lookup"><span data-stu-id="29937-481">Represents **null** value of type **Null**.</span></span>  
  
* `<boolean_constant>`  
  
  <span data-ttu-id="29937-482">Represents constant of type Boolean.</span><span class="sxs-lookup"><span data-stu-id="29937-482">Represents constant of type Boolean.</span></span>  
  
* `false`  
  
  <span data-ttu-id="29937-483">Represents **false** value of type Boolean.</span><span class="sxs-lookup"><span data-stu-id="29937-483">Represents **false** value of type Boolean.</span></span>  
  
* `true`  
  
  <span data-ttu-id="29937-484">Represents **true** value of type Boolean.</span><span class="sxs-lookup"><span data-stu-id="29937-484">Represents **true** value of type Boolean.</span></span>  
  
* `<number_constant>`  
  
  <span data-ttu-id="29937-485">Represents a constant.</span><span class="sxs-lookup"><span data-stu-id="29937-485">Represents a constant.</span></span>  
  
* `decimal_literal`  
  
  <span data-ttu-id="29937-486">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span><span class="sxs-lookup"><span data-stu-id="29937-486">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
* `hexadecimal_literal`  
  
  <span data-ttu-id="29937-487">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="29937-487">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
* `<string_constant>`  
  
  <span data-ttu-id="29937-488">Represents a constant of type String.</span><span class="sxs-lookup"><span data-stu-id="29937-488">Represents a constant of type String.</span></span>  
  
* `string _literal`  
  
  <span data-ttu-id="29937-489">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span><span class="sxs-lookup"><span data-stu-id="29937-489">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="29937-490">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span><span class="sxs-lookup"><span data-stu-id="29937-490">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="29937-491">Following escape sequences are allowed:</span><span class="sxs-lookup"><span data-stu-id="29937-491">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="29937-492">**Escape sequence**</span><span class="sxs-lookup"><span data-stu-id="29937-492">**Escape sequence**</span></span>|<span data-ttu-id="29937-493">**Description**</span><span class="sxs-lookup"><span data-stu-id="29937-493">**Description**</span></span>|<span data-ttu-id="29937-494">**Unicode character**</span><span class="sxs-lookup"><span data-stu-id="29937-494">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="29937-495">\\'</span><span class="sxs-lookup"><span data-stu-id="29937-495">\\'</span></span>|<span data-ttu-id="29937-496">apostrophe (')</span><span class="sxs-lookup"><span data-stu-id="29937-496">apostrophe (')</span></span>|<span data-ttu-id="29937-497">U+0027</span><span class="sxs-lookup"><span data-stu-id="29937-497">U+0027</span></span>|  
|<span data-ttu-id="29937-498">\\"</span><span class="sxs-lookup"><span data-stu-id="29937-498">\\"</span></span>|<span data-ttu-id="29937-499">quotation mark (")</span><span class="sxs-lookup"><span data-stu-id="29937-499">quotation mark (")</span></span>|<span data-ttu-id="29937-500">U+0022</span><span class="sxs-lookup"><span data-stu-id="29937-500">U+0022</span></span>|  
|<span data-ttu-id="29937-501">\\\|reverse solidus (\\)</span><span class="sxs-lookup"><span data-stu-id="29937-501">\\\|reverse solidus (\\)</span></span>|<span data-ttu-id="29937-502">U+005C</span><span class="sxs-lookup"><span data-stu-id="29937-502">U+005C</span></span>|  
|\\/|<span data-ttu-id="29937-503">solidus (/)</span><span class="sxs-lookup"><span data-stu-id="29937-503">solidus (/)</span></span>|<span data-ttu-id="29937-504">U+002F</span><span class="sxs-lookup"><span data-stu-id="29937-504">U+002F</span></span>|  
|<span data-ttu-id="29937-505">\b</span><span class="sxs-lookup"><span data-stu-id="29937-505">\b</span></span>|<span data-ttu-id="29937-506">backspace</span><span class="sxs-lookup"><span data-stu-id="29937-506">backspace</span></span>|<span data-ttu-id="29937-507">U+0008</span><span class="sxs-lookup"><span data-stu-id="29937-507">U+0008</span></span>|  
|<span data-ttu-id="29937-508">\f</span><span class="sxs-lookup"><span data-stu-id="29937-508">\f</span></span>|<span data-ttu-id="29937-509">form feed</span><span class="sxs-lookup"><span data-stu-id="29937-509">form feed</span></span>|<span data-ttu-id="29937-510">U+000C</span><span class="sxs-lookup"><span data-stu-id="29937-510">U+000C</span></span>|  
|<span data-ttu-id="29937-511">\n</span><span class="sxs-lookup"><span data-stu-id="29937-511">\n</span></span>|<span data-ttu-id="29937-512">line feed</span><span class="sxs-lookup"><span data-stu-id="29937-512">line feed</span></span>|<span data-ttu-id="29937-513">U+000A</span><span class="sxs-lookup"><span data-stu-id="29937-513">U+000A</span></span>|  
|<span data-ttu-id="29937-514">\r</span><span class="sxs-lookup"><span data-stu-id="29937-514">\r</span></span>|<span data-ttu-id="29937-515">carriage return</span><span class="sxs-lookup"><span data-stu-id="29937-515">carriage return</span></span>|<span data-ttu-id="29937-516">U+000D</span><span class="sxs-lookup"><span data-stu-id="29937-516">U+000D</span></span>|  
|<span data-ttu-id="29937-517">\t</span><span class="sxs-lookup"><span data-stu-id="29937-517">\t</span></span>|<span data-ttu-id="29937-518">tab</span><span class="sxs-lookup"><span data-stu-id="29937-518">tab</span></span>|<span data-ttu-id="29937-519">U+0009</span><span class="sxs-lookup"><span data-stu-id="29937-519">U+0009</span></span>|  
|<span data-ttu-id="29937-520">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="29937-520">\uXXXX</span></span>|<span data-ttu-id="29937-521">A Unicode character defined by 4 hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="29937-521">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="29937-522">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="29937-522">U+XXXX</span></span>|  
  
##  <a name="bk_query_perf_guidelines"></a> <span data-ttu-id="29937-523">Query performance guidelines</span><span class="sxs-lookup"><span data-stu-id="29937-523">Query performance guidelines</span></span>  
 <span data-ttu-id="29937-524">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span><span class="sxs-lookup"><span data-stu-id="29937-524">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="29937-525">The following filters will be considered for index lookup:</span><span class="sxs-lookup"><span data-stu-id="29937-525">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="29937-526">Use equality operator ( = ) with a document path expression and a constant.</span><span class="sxs-lookup"><span data-stu-id="29937-526">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="29937-527">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span><span class="sxs-lookup"><span data-stu-id="29937-527">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="29937-528">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span><span class="sxs-lookup"><span data-stu-id="29937-528">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="29937-529">**Document path expression**</span><span class="sxs-lookup"><span data-stu-id="29937-529">**Document path expression**</span></span>  
  
 <span data-ttu-id="29937-530">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span><span class="sxs-lookup"><span data-stu-id="29937-530">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="29937-531">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span><span class="sxs-lookup"><span data-stu-id="29937-531">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="29937-532">For an expression to be considered a document path expression, it should:</span><span class="sxs-lookup"><span data-stu-id="29937-532">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="29937-533">Reference the collection root directly.</span><span class="sxs-lookup"><span data-stu-id="29937-533">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="29937-534">Reference property or constant array indexer of some document path expression</span><span class="sxs-lookup"><span data-stu-id="29937-534">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="29937-535">Reference an alias, which represents some document path expression.</span><span class="sxs-lookup"><span data-stu-id="29937-535">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="29937-536">**Syntax conventions**</span><span class="sxs-lookup"><span data-stu-id="29937-536">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="29937-537">The following table describes the conventions used to describe syntax in the following SQL reference.</span><span class="sxs-lookup"><span data-stu-id="29937-537">The following table describes the conventions used to describe syntax in the following SQL reference.</span></span>  
  
    |<span data-ttu-id="29937-538">**Convention**</span><span class="sxs-lookup"><span data-stu-id="29937-538">**Convention**</span></span>|<span data-ttu-id="29937-539">**Used for**</span><span class="sxs-lookup"><span data-stu-id="29937-539">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="29937-540">UPPERCASE</span><span class="sxs-lookup"><span data-stu-id="29937-540">UPPERCASE</span></span>|<span data-ttu-id="29937-541">Case-insensitive keywords.</span><span class="sxs-lookup"><span data-stu-id="29937-541">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="29937-542">lowercase</span><span class="sxs-lookup"><span data-stu-id="29937-542">lowercase</span></span>|<span data-ttu-id="29937-543">Case-sensitive keywords.</span><span class="sxs-lookup"><span data-stu-id="29937-543">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="29937-544">\<nonterminal></span><span class="sxs-lookup"><span data-stu-id="29937-544">\<nonterminal></span></span>|<span data-ttu-id="29937-545">Nonterminal, defined separately.</span><span class="sxs-lookup"><span data-stu-id="29937-545">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="29937-546">\<nonterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="29937-546">\<nonterminal> ::=</span></span>|<span data-ttu-id="29937-547">Syntax definition of the nonterminal.</span><span class="sxs-lookup"><span data-stu-id="29937-547">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="29937-548">other_terminal</span><span class="sxs-lookup"><span data-stu-id="29937-548">other_terminal</span></span>|<span data-ttu-id="29937-549">Terminal (token), described in detail in words.</span><span class="sxs-lookup"><span data-stu-id="29937-549">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="29937-550">identifier</span><span class="sxs-lookup"><span data-stu-id="29937-550">identifier</span></span>|<span data-ttu-id="29937-551">Identifier.</span><span class="sxs-lookup"><span data-stu-id="29937-551">Identifier.</span></span> <span data-ttu-id="29937-552">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span><span class="sxs-lookup"><span data-stu-id="29937-552">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="29937-553">"string"</span><span class="sxs-lookup"><span data-stu-id="29937-553">"string"</span></span>|<span data-ttu-id="29937-554">Quoted string.</span><span class="sxs-lookup"><span data-stu-id="29937-554">Quoted string.</span></span> <span data-ttu-id="29937-555">Allows any valid string.</span><span class="sxs-lookup"><span data-stu-id="29937-555">Allows any valid string.</span></span> <span data-ttu-id="29937-556">See description of a string_literal.</span><span class="sxs-lookup"><span data-stu-id="29937-556">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="29937-557">'symbol'</span><span class="sxs-lookup"><span data-stu-id="29937-557">'symbol'</span></span>|<span data-ttu-id="29937-558">Literal symbol which is part of the syntax.</span><span class="sxs-lookup"><span data-stu-id="29937-558">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="29937-559">&#124; (vertical bar)</span><span class="sxs-lookup"><span data-stu-id="29937-559">&#124; (vertical bar)</span></span>|<span data-ttu-id="29937-560">Alternatives for syntax items.</span><span class="sxs-lookup"><span data-stu-id="29937-560">Alternatives for syntax items.</span></span> <span data-ttu-id="29937-561">You can use only one of the items specified.</span><span class="sxs-lookup"><span data-stu-id="29937-561">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="29937-562">[ ] /(brackets)</span><span class="sxs-lookup"><span data-stu-id="29937-562">[ ] /(brackets)</span></span>|<span data-ttu-id="29937-563">Brackets enclose one or more optional items.</span><span class="sxs-lookup"><span data-stu-id="29937-563">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="29937-564">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="29937-564">[ ,...n ]</span></span>|<span data-ttu-id="29937-565">Indicates the preceding item can be repeated n number of times.</span><span class="sxs-lookup"><span data-stu-id="29937-565">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="29937-566">The occurrences are separated by commas.</span><span class="sxs-lookup"><span data-stu-id="29937-566">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="29937-567">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="29937-567">[ ...n ]</span></span>|<span data-ttu-id="29937-568">Indicates the preceding item can be repeated n number of times.</span><span class="sxs-lookup"><span data-stu-id="29937-568">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="29937-569">The occurrences are separated by blanks.</span><span class="sxs-lookup"><span data-stu-id="29937-569">The occurrences are separated by blanks.</span></span>|  
  
##  <a name="bk_built_in_functions"></a> <span data-ttu-id="29937-570">Built-in functions</span><span class="sxs-lookup"><span data-stu-id="29937-570">Built-in functions</span></span>  
 <span data-ttu-id="29937-571">Azure Cosmos DB provides many built-in SQL functions.</span><span class="sxs-lookup"><span data-stu-id="29937-571">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="29937-572">The categories of built-in functions are listed below.</span><span class="sxs-lookup"><span data-stu-id="29937-572">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="29937-573">Function</span><span class="sxs-lookup"><span data-stu-id="29937-573">Function</span></span>|<span data-ttu-id="29937-574">Description</span><span class="sxs-lookup"><span data-stu-id="29937-574">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="29937-575">Mathematical functions</span><span class="sxs-lookup"><span data-stu-id="29937-575">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="29937-576">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span><span class="sxs-lookup"><span data-stu-id="29937-576">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="29937-577">Type checking functions</span><span class="sxs-lookup"><span data-stu-id="29937-577">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="29937-578">The type checking functions allow you to check the type of an expression within SQL queries.</span><span class="sxs-lookup"><span data-stu-id="29937-578">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="29937-579">String functions</span><span class="sxs-lookup"><span data-stu-id="29937-579">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="29937-580">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-580">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="29937-581">Array functions</span><span class="sxs-lookup"><span data-stu-id="29937-581">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="29937-582">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span><span class="sxs-lookup"><span data-stu-id="29937-582">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="29937-583">Spatial functions</span><span class="sxs-lookup"><span data-stu-id="29937-583">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="29937-584">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-584">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <a name="bk_mathematical_functions"></a> <span data-ttu-id="29937-585">Mathematical functions</span><span class="sxs-lookup"><span data-stu-id="29937-585">Mathematical functions</span></span>  
 <span data-ttu-id="29937-586">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span><span class="sxs-lookup"><span data-stu-id="29937-586">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="29937-587">ABS</span><span class="sxs-lookup"><span data-stu-id="29937-587">ABS</span></span>](#bk_abs)|[<span data-ttu-id="29937-588">ACOS</span><span class="sxs-lookup"><span data-stu-id="29937-588">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="29937-589">ASIN</span><span class="sxs-lookup"><span data-stu-id="29937-589">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="29937-590">ATAN</span><span class="sxs-lookup"><span data-stu-id="29937-590">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="29937-591">ATN2</span><span class="sxs-lookup"><span data-stu-id="29937-591">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="29937-592">CEILING</span><span class="sxs-lookup"><span data-stu-id="29937-592">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="29937-593">COS</span><span class="sxs-lookup"><span data-stu-id="29937-593">COS</span></span>](#bk_cos)|[<span data-ttu-id="29937-594">COT</span><span class="sxs-lookup"><span data-stu-id="29937-594">COT</span></span>](#bk_cot)|[<span data-ttu-id="29937-595">DEGREES</span><span class="sxs-lookup"><span data-stu-id="29937-595">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="29937-596">EXP</span><span class="sxs-lookup"><span data-stu-id="29937-596">EXP</span></span>](#bk_exp)|[<span data-ttu-id="29937-597">FLOOR</span><span class="sxs-lookup"><span data-stu-id="29937-597">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="29937-598">LOG</span><span class="sxs-lookup"><span data-stu-id="29937-598">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="29937-599">LOG10</span><span class="sxs-lookup"><span data-stu-id="29937-599">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="29937-600">PI</span><span class="sxs-lookup"><span data-stu-id="29937-600">PI</span></span>](#bk_pi)|[<span data-ttu-id="29937-601">POWER</span><span class="sxs-lookup"><span data-stu-id="29937-601">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="29937-602">RADIANS</span><span class="sxs-lookup"><span data-stu-id="29937-602">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="29937-603">ROUND</span><span class="sxs-lookup"><span data-stu-id="29937-603">ROUND</span></span>](#bk_round)|[<span data-ttu-id="29937-604">SIN</span><span class="sxs-lookup"><span data-stu-id="29937-604">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="29937-605">SQRT</span><span class="sxs-lookup"><span data-stu-id="29937-605">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="29937-606">SQUARE</span><span class="sxs-lookup"><span data-stu-id="29937-606">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="29937-607">SIGN</span><span class="sxs-lookup"><span data-stu-id="29937-607">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="29937-608">TAN</span><span class="sxs-lookup"><span data-stu-id="29937-608">TAN</span></span>](#bk_tan)|[<span data-ttu-id="29937-609">TRUNC</span><span class="sxs-lookup"><span data-stu-id="29937-609">TRUNC</span></span>](#bk_trunc)||  
  
####  <a name="bk_abs"></a> <span data-ttu-id="29937-610">ABS</span><span class="sxs-lookup"><span data-stu-id="29937-610">ABS</span></span>  
 <span data-ttu-id="29937-611">Returns the absolute (positive) value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-611">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-612">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-612">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-613">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-613">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-614">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-614">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-615">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-615">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-616">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-616">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-617">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-617">**Examples**</span></span>  
  
 <span data-ttu-id="29937-618">The following example shows the results of using the ABS function on three different numbers.</span><span class="sxs-lookup"><span data-stu-id="29937-618">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="29937-619">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-619">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> <span data-ttu-id="29937-620">ACOS</span><span class="sxs-lookup"><span data-stu-id="29937-620">ACOS</span></span>  
 <span data-ttu-id="29937-621">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span><span class="sxs-lookup"><span data-stu-id="29937-621">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="29937-622">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-622">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-623">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-624">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-625">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-625">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-626">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-627">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-627">**Examples**</span></span>  
  
 <span data-ttu-id="29937-628">The following example returns the ACOS of -1.</span><span class="sxs-lookup"><span data-stu-id="29937-628">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="29937-629">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-629">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> <span data-ttu-id="29937-630">ASIN</span><span class="sxs-lookup"><span data-stu-id="29937-630">ASIN</span></span>  
 <span data-ttu-id="29937-631">Returns the angle, in radians, whose sine is the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-631">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="29937-632">This is also called arcsine.</span><span class="sxs-lookup"><span data-stu-id="29937-632">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="29937-633">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-633">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-634">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-635">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-636">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-636">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-637">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-638">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-638">**Examples**</span></span>  
  
 <span data-ttu-id="29937-639">The following example returns the ASIN of -1.</span><span class="sxs-lookup"><span data-stu-id="29937-639">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="29937-640">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-640">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> <span data-ttu-id="29937-641">ATAN</span><span class="sxs-lookup"><span data-stu-id="29937-641">ATAN</span></span>  
 <span data-ttu-id="29937-642">Returns the angle, in radians, whose tangent is the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-642">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="29937-643">This is also called arctangent.</span><span class="sxs-lookup"><span data-stu-id="29937-643">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="29937-644">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-644">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-645">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-645">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-646">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-646">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-647">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-647">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-648">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-648">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-649">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-649">**Examples**</span></span>  
  
 <span data-ttu-id="29937-650">The following example returns the ATAN of the specified value.</span><span class="sxs-lookup"><span data-stu-id="29937-650">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="29937-651">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-651">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> <span data-ttu-id="29937-652">ATN2</span><span class="sxs-lookup"><span data-stu-id="29937-652">ATN2</span></span>  
 <span data-ttu-id="29937-653">Returns the principal value of the arc tangent of y/x, expressed in radians.</span><span class="sxs-lookup"><span data-stu-id="29937-653">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="29937-654">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-654">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="29937-655">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-655">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-656">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-656">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-657">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-657">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-658">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-658">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-659">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-659">**Examples**</span></span>  
  
 <span data-ttu-id="29937-660">The following example calculates the ATN2 for the specified x and y components.</span><span class="sxs-lookup"><span data-stu-id="29937-660">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="29937-661">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-661">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> <span data-ttu-id="29937-662">CEILING</span><span class="sxs-lookup"><span data-stu-id="29937-662">CEILING</span></span>  
 <span data-ttu-id="29937-663">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-663">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-664">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-664">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-665">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-665">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-666">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-666">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-667">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-667">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-668">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-668">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-669">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-669">**Examples**</span></span>  
  
 <span data-ttu-id="29937-670">The following example shows positive numeric, negative, and zero values with the CEILING function.</span><span class="sxs-lookup"><span data-stu-id="29937-670">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="29937-671">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-671">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> <span data-ttu-id="29937-672">COS</span><span class="sxs-lookup"><span data-stu-id="29937-672">COS</span></span>  
 <span data-ttu-id="29937-673">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="29937-673">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="29937-674">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-674">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-675">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-675">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-676">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-676">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-677">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-677">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-678">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-678">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-679">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-679">**Examples**</span></span>  
  
 <span data-ttu-id="29937-680">The following example calculates the COS of the specified angle.</span><span class="sxs-lookup"><span data-stu-id="29937-680">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="29937-681">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-681">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> <span data-ttu-id="29937-682">COT</span><span class="sxs-lookup"><span data-stu-id="29937-682">COT</span></span>  
 <span data-ttu-id="29937-683">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-683">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-684">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-684">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-685">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-685">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-686">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-686">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-687">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-687">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-688">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-688">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-689">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-689">**Examples**</span></span>  
  
 <span data-ttu-id="29937-690">The following example calculates the COT of the specified angle.</span><span class="sxs-lookup"><span data-stu-id="29937-690">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="29937-691">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-691">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> <span data-ttu-id="29937-692">DEGREES</span><span class="sxs-lookup"><span data-stu-id="29937-692">DEGREES</span></span>  
 <span data-ttu-id="29937-693">Returns the corresponding angle in degrees for an angle specified in radians.</span><span class="sxs-lookup"><span data-stu-id="29937-693">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="29937-694">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-694">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-695">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-695">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-696">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-696">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-697">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-697">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-698">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-698">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-699">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-699">**Examples**</span></span>  
  
 <span data-ttu-id="29937-700">The following example returns the number of degrees in an angle of PI/2 radians.</span><span class="sxs-lookup"><span data-stu-id="29937-700">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="29937-701">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-701">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> <span data-ttu-id="29937-702">FLOOR</span><span class="sxs-lookup"><span data-stu-id="29937-702">FLOOR</span></span>  
 <span data-ttu-id="29937-703">Returns the largest integer less than or equal to the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-703">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-704">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-704">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-705">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-705">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-706">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-706">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-707">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-707">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-708">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-708">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-709">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-709">**Examples**</span></span>  
  
 <span data-ttu-id="29937-710">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span><span class="sxs-lookup"><span data-stu-id="29937-710">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="29937-711">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-711">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> <span data-ttu-id="29937-712">EXP</span><span class="sxs-lookup"><span data-stu-id="29937-712">EXP</span></span>  
 <span data-ttu-id="29937-713">Returns the exponential value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-713">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-714">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-714">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-715">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-715">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-716">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-716">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-717">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-717">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-718">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-718">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-719">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-719">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-720">The constant **e** (2.718281…), is the base of natural logarithms.</span><span class="sxs-lookup"><span data-stu-id="29937-720">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="29937-721">The exponent of a number is the constant **e** raised to the power of the number.</span><span class="sxs-lookup"><span data-stu-id="29937-721">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="29937-722">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="29937-722">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="29937-723">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="29937-723">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="29937-724">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="29937-724">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="29937-725">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-725">**Examples**</span></span>  
  
 <span data-ttu-id="29937-726">The following example declares a variable and returns the exponential value of the specified variable (10).</span><span class="sxs-lookup"><span data-stu-id="29937-726">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="29937-727">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-727">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="29937-728">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span><span class="sxs-lookup"><span data-stu-id="29937-728">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="29937-729">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span><span class="sxs-lookup"><span data-stu-id="29937-729">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="29937-730">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-730">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> <span data-ttu-id="29937-731">LOG</span><span class="sxs-lookup"><span data-stu-id="29937-731">LOG</span></span>  
 <span data-ttu-id="29937-732">Returns the natural logarithm of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-732">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-733">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-733">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="29937-734">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-734">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-735">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-735">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="29937-736">Optional numeric argument that sets the base for the logarithm.</span><span class="sxs-lookup"><span data-stu-id="29937-736">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="29937-737">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-737">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-738">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-738">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-739">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-739">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-740">By default, LOG() returns the natural logarithm.</span><span class="sxs-lookup"><span data-stu-id="29937-740">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="29937-741">You can change the base of the logarithm to another value by using the optional base parameter.</span><span class="sxs-lookup"><span data-stu-id="29937-741">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="29937-742">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span><span class="sxs-lookup"><span data-stu-id="29937-742">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="29937-743">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span><span class="sxs-lookup"><span data-stu-id="29937-743">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="29937-744">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span><span class="sxs-lookup"><span data-stu-id="29937-744">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="29937-745">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-745">**Examples**</span></span>  
  
 <span data-ttu-id="29937-746">The following example declares a variable and returns the logarithm value of the specified variable (10).</span><span class="sxs-lookup"><span data-stu-id="29937-746">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="29937-747">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-747">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="29937-748">The following example calculates the LOG for the exponent of a number.</span><span class="sxs-lookup"><span data-stu-id="29937-748">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="29937-749">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-749">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> <span data-ttu-id="29937-750">LOG10</span><span class="sxs-lookup"><span data-stu-id="29937-750">LOG10</span></span>  
 <span data-ttu-id="29937-751">Returns the base-10 logarithm of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-751">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-752">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-752">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-753">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-753">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-754">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-754">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-755">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-755">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-756">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-756">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-757">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="29937-757">**Remarks**</span></span>  
  
 <span data-ttu-id="29937-758">The LOG10 and POWER functions are inversely related to one another.</span><span class="sxs-lookup"><span data-stu-id="29937-758">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="29937-759">For example, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="29937-759">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="29937-760">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-760">**Examples**</span></span>  
  
 <span data-ttu-id="29937-761">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span><span class="sxs-lookup"><span data-stu-id="29937-761">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="29937-762">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-762">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> <span data-ttu-id="29937-763">PI</span><span class="sxs-lookup"><span data-stu-id="29937-763">PI</span></span>  
 <span data-ttu-id="29937-764">Returns the constant value of PI.</span><span class="sxs-lookup"><span data-stu-id="29937-764">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="29937-765">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-765">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="29937-766">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-766">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-767">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-767">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-768">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-768">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-769">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-770">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-770">**Examples**</span></span>  
  
 <span data-ttu-id="29937-771">The following example returns the value of PI.</span><span class="sxs-lookup"><span data-stu-id="29937-771">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="29937-772">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-772">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> <span data-ttu-id="29937-773">POWER</span><span class="sxs-lookup"><span data-stu-id="29937-773">POWER</span></span>  
 <span data-ttu-id="29937-774">Returns the value of the specified expression to the specified power.</span><span class="sxs-lookup"><span data-stu-id="29937-774">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="29937-775">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-775">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="29937-776">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-777">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-777">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="29937-778">Is the power to which to raise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="29937-778">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="29937-779">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-779">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-780">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-780">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-781">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-781">**Examples**</span></span>  
  
 <span data-ttu-id="29937-782">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span><span class="sxs-lookup"><span data-stu-id="29937-782">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="29937-783">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-783">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> <span data-ttu-id="29937-784">RADIANS</span><span class="sxs-lookup"><span data-stu-id="29937-784">RADIANS</span></span>  
 <span data-ttu-id="29937-785">Returns radians when a numeric expression, in degrees, is entered.</span><span class="sxs-lookup"><span data-stu-id="29937-785">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="29937-786">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-786">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-787">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-787">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-788">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-788">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-789">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-789">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-790">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-790">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-791">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-791">**Examples**</span></span>  
  
 <span data-ttu-id="29937-792">The following example takes a few angles as input and returns their corresponding radian values.</span><span class="sxs-lookup"><span data-stu-id="29937-792">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="29937-793">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-793">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> <span data-ttu-id="29937-794">ROUND</span><span class="sxs-lookup"><span data-stu-id="29937-794">ROUND</span></span>  
 <span data-ttu-id="29937-795">Returns a numeric value, rounded to the closest integer value.</span><span class="sxs-lookup"><span data-stu-id="29937-795">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="29937-796">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-796">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-797">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-797">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-798">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-798">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-799">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-799">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-800">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-800">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-801">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-801">**Examples**</span></span>  
  
 <span data-ttu-id="29937-802">The following example rounds the following positive and negative numbers to the nearest integer.</span><span class="sxs-lookup"><span data-stu-id="29937-802">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="29937-803">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-803">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> <span data-ttu-id="29937-804">SIGN</span><span class="sxs-lookup"><span data-stu-id="29937-804">SIGN</span></span>  
 <span data-ttu-id="29937-805">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-805">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="29937-806">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-806">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-807">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-807">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-808">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-808">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-809">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-809">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-810">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-810">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-811">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-811">**Examples**</span></span>  
  
 <span data-ttu-id="29937-812">The following example returns the SIGN values of numbers from -2 to 2.</span><span class="sxs-lookup"><span data-stu-id="29937-812">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="29937-813">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-813">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> <span data-ttu-id="29937-814">SIN</span><span class="sxs-lookup"><span data-stu-id="29937-814">SIN</span></span>  
 <span data-ttu-id="29937-815">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="29937-815">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="29937-816">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-816">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-817">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-817">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-818">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-818">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-819">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-819">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-820">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-820">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-821">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-821">**Examples**</span></span>  
  
 <span data-ttu-id="29937-822">The following example calculates the SIN of the specified angle.</span><span class="sxs-lookup"><span data-stu-id="29937-822">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="29937-823">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-823">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> <span data-ttu-id="29937-824">SQRT</span><span class="sxs-lookup"><span data-stu-id="29937-824">SQRT</span></span>  
 <span data-ttu-id="29937-825">Returns the square root of the specified numeric value.</span><span class="sxs-lookup"><span data-stu-id="29937-825">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="29937-826">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-826">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-827">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-827">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-828">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-828">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-829">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-829">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-830">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-830">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-831">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-831">**Examples**</span></span>  
  
 <span data-ttu-id="29937-832">The following example returns the square roots of numbers 1-3.</span><span class="sxs-lookup"><span data-stu-id="29937-832">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="29937-833">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-833">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> <span data-ttu-id="29937-834">SQUARE</span><span class="sxs-lookup"><span data-stu-id="29937-834">SQUARE</span></span>  
 <span data-ttu-id="29937-835">Returns the square of the specified numeric value.</span><span class="sxs-lookup"><span data-stu-id="29937-835">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="29937-836">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-836">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-837">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-837">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-838">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-838">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-839">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-839">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-840">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-840">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-841">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-841">**Examples**</span></span>  
  
 <span data-ttu-id="29937-842">The following example returns the squares of numbers 1-3.</span><span class="sxs-lookup"><span data-stu-id="29937-842">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="29937-843">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-843">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> <span data-ttu-id="29937-844">TAN</span><span class="sxs-lookup"><span data-stu-id="29937-844">TAN</span></span>  
 <span data-ttu-id="29937-845">Returns the tangent of the specified angle, in radians, in the specified expression.</span><span class="sxs-lookup"><span data-stu-id="29937-845">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="29937-846">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-846">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-847">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-847">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-848">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-848">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-849">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-849">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-850">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-850">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-851">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-851">**Examples**</span></span>  
  
 <span data-ttu-id="29937-852">The following example calculates the tangent of PI()/2.</span><span class="sxs-lookup"><span data-stu-id="29937-852">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="29937-853">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-853">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a> <span data-ttu-id="29937-854">TRUNC</span><span class="sxs-lookup"><span data-stu-id="29937-854">TRUNC</span></span>  
 <span data-ttu-id="29937-855">Returns a numeric value, truncated to the closest integer value.</span><span class="sxs-lookup"><span data-stu-id="29937-855">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="29937-856">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-856">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="29937-857">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-857">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="29937-858">Is a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-858">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-859">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-859">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-860">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-860">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-861">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-861">**Examples**</span></span>  
  
 <span data-ttu-id="29937-862">The following example truncates the following positive and negative numbers to the nearest integer value.</span><span class="sxs-lookup"><span data-stu-id="29937-862">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="29937-863">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-863">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a> <span data-ttu-id="29937-864">Type checking functions</span><span class="sxs-lookup"><span data-stu-id="29937-864">Type checking functions</span></span>  
 <span data-ttu-id="29937-865">The following functions support type checking against input values, and each return a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-865">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="29937-866">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="29937-866">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="29937-867">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="29937-867">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="29937-868">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="29937-868">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="29937-869">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="29937-869">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="29937-870">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="29937-870">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="29937-871">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="29937-871">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="29937-872">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="29937-872">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="29937-873">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="29937-873">IS_STRING</span></span>](#bk_is_string)||  
  
####  <a name="bk_is_array"></a> <span data-ttu-id="29937-874">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="29937-874">IS_ARRAY</span></span>  
 <span data-ttu-id="29937-875">Returns a Boolean value indicating if the type of the specified expression is an array.</span><span class="sxs-lookup"><span data-stu-id="29937-875">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="29937-876">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-876">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="29937-877">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-877">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-878">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-878">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-879">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-879">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-880">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-880">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-881">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-881">**Examples**</span></span>  
  
 <span data-ttu-id="29937-882">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span><span class="sxs-lookup"><span data-stu-id="29937-882">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-883">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-883">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a> <span data-ttu-id="29937-884">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="29937-884">IS_BOOL</span></span>  
 <span data-ttu-id="29937-885">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="29937-885">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="29937-886">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-886">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="29937-887">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-887">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-888">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-888">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-889">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-889">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-890">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-890">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-891">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-891">**Examples**</span></span>  
  
 <span data-ttu-id="29937-892">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span><span class="sxs-lookup"><span data-stu-id="29937-892">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-893">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-893">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a> <span data-ttu-id="29937-894">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="29937-894">IS_DEFINED</span></span>  
 <span data-ttu-id="29937-895">Returns a Boolean indicating if the property has been assigned a value.</span><span class="sxs-lookup"><span data-stu-id="29937-895">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="29937-896">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-896">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="29937-897">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-898">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-899">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-899">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-900">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-901">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-901">**Examples**</span></span>  
  
 <span data-ttu-id="29937-902">The following example checks for the presence of a property within the specified JSON document.</span><span class="sxs-lookup"><span data-stu-id="29937-902">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="29937-903">The first returns true since "a" is present, but the second returns false since "b" is absent.</span><span class="sxs-lookup"><span data-stu-id="29937-903">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="29937-904">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-904">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a> <span data-ttu-id="29937-905">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="29937-905">IS_NULL</span></span>  
 <span data-ttu-id="29937-906">Returns a Boolean value indicating if the type of the specified expression is null.</span><span class="sxs-lookup"><span data-stu-id="29937-906">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="29937-907">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-907">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="29937-908">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-908">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-909">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-909">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-910">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-910">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-911">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-911">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-912">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-912">**Examples**</span></span>  
  
 <span data-ttu-id="29937-913">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span><span class="sxs-lookup"><span data-stu-id="29937-913">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-914">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-914">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a> <span data-ttu-id="29937-915">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="29937-915">IS_NUMBER</span></span>  
 <span data-ttu-id="29937-916">Returns a Boolean value indicating if the type of the specified expression is a number.</span><span class="sxs-lookup"><span data-stu-id="29937-916">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="29937-917">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-917">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="29937-918">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-918">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-919">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-919">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-920">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-920">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-921">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-921">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-922">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-922">**Examples**</span></span>  
  
 <span data-ttu-id="29937-923">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span><span class="sxs-lookup"><span data-stu-id="29937-923">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-924">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-924">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a> <span data-ttu-id="29937-925">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="29937-925">IS_OBJECT</span></span>  
 <span data-ttu-id="29937-926">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="29937-926">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="29937-927">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-927">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="29937-928">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-928">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-929">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-929">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-930">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-930">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-931">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-931">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-932">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-932">**Examples**</span></span>  
  
 <span data-ttu-id="29937-933">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span><span class="sxs-lookup"><span data-stu-id="29937-933">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-934">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-934">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a> <span data-ttu-id="29937-935">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="29937-935">IS_PRIMITIVE</span></span>  
 <span data-ttu-id="29937-936">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span><span class="sxs-lookup"><span data-stu-id="29937-936">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="29937-937">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-937">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="29937-938">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-938">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-939">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-939">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-940">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-940">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-941">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-941">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-942">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-942">**Examples**</span></span>  
  
 <span data-ttu-id="29937-943">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span><span class="sxs-lookup"><span data-stu-id="29937-943">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-944">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-944">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> <span data-ttu-id="29937-945">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="29937-945">IS_STRING</span></span>  
 <span data-ttu-id="29937-946">Returns a Boolean value indicating if the type of the specified expression is a string.</span><span class="sxs-lookup"><span data-stu-id="29937-946">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="29937-947">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-947">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="29937-948">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-948">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="29937-949">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-949">Is any valid expression.</span></span>  
  
 <span data-ttu-id="29937-950">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-950">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-951">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-951">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-952">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-952">**Examples**</span></span>  
  
 <span data-ttu-id="29937-953">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span><span class="sxs-lookup"><span data-stu-id="29937-953">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="29937-954">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-954">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> <span data-ttu-id="29937-955">String functions</span><span class="sxs-lookup"><span data-stu-id="29937-955">String functions</span></span>  
 <span data-ttu-id="29937-956">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-956">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="29937-957">CONCAT</span><span class="sxs-lookup"><span data-stu-id="29937-957">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="29937-958">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="29937-958">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="29937-959">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="29937-959">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="29937-960">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="29937-960">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="29937-961">LEFT</span><span class="sxs-lookup"><span data-stu-id="29937-961">LEFT</span></span>](#bk_left)|[<span data-ttu-id="29937-962">LENGTH</span><span class="sxs-lookup"><span data-stu-id="29937-962">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="29937-963">LOWER</span><span class="sxs-lookup"><span data-stu-id="29937-963">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="29937-964">LTRIM</span><span class="sxs-lookup"><span data-stu-id="29937-964">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="29937-965">REPLACE</span><span class="sxs-lookup"><span data-stu-id="29937-965">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="29937-966">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="29937-966">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="29937-967">REVERSE</span><span class="sxs-lookup"><span data-stu-id="29937-967">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="29937-968">RIGHT</span><span class="sxs-lookup"><span data-stu-id="29937-968">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="29937-969">RTRIM</span><span class="sxs-lookup"><span data-stu-id="29937-969">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="29937-970">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="29937-970">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="29937-971">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="29937-971">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="29937-972">ToString</span><span class="sxs-lookup"><span data-stu-id="29937-972">ToString</span></span>](#bk_tostring)|[<span data-ttu-id="29937-973">TRIM</span><span class="sxs-lookup"><span data-stu-id="29937-973">TRIM</span></span>](#bk_trim)|[<span data-ttu-id="29937-974">UPPER</span><span class="sxs-lookup"><span data-stu-id="29937-974">UPPER</span></span>](#bk_upper)||| 
  
####  <a name="bk_concat"></a> <span data-ttu-id="29937-975">CONCAT</span><span class="sxs-lookup"><span data-stu-id="29937-975">CONCAT</span></span>  
 <span data-ttu-id="29937-976">Returns a string that is the result of concatenating two or more string values.</span><span class="sxs-lookup"><span data-stu-id="29937-976">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="29937-977">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-977">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="29937-978">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-978">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-979">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-979">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-980">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-980">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-981">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-981">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-982">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-982">**Examples**</span></span>  
  
 <span data-ttu-id="29937-983">The following example returns the concatenated string of the specified values.</span><span class="sxs-lookup"><span data-stu-id="29937-983">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="29937-984">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-984">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> <span data-ttu-id="29937-985">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="29937-985">CONTAINS</span></span>  
 <span data-ttu-id="29937-986">Returns a Boolean indicating whether the first string expression contains the second.</span><span class="sxs-lookup"><span data-stu-id="29937-986">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="29937-987">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-987">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="29937-988">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-988">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-989">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-989">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-990">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-990">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-991">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-991">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-992">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-992">**Examples**</span></span>  
  
 <span data-ttu-id="29937-993">The following example checks if "abc" contains "ab" and contains "d".</span><span class="sxs-lookup"><span data-stu-id="29937-993">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="29937-994">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-994">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> <span data-ttu-id="29937-995">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="29937-995">ENDSWITH</span></span>  
 <span data-ttu-id="29937-996">Returns a Boolean indicating whether the first string expression ends with the second.</span><span class="sxs-lookup"><span data-stu-id="29937-996">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="29937-997">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-997">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="29937-998">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-998">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-999">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-999">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1000">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1000">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1001">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1001">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-1002">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1002">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1003">The following example returns the "abc" ends with "b" and "bc".</span><span class="sxs-lookup"><span data-stu-id="29937-1003">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="29937-1004">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1004">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a> <span data-ttu-id="29937-1005">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="29937-1005">INDEX_OF</span></span>  
 <span data-ttu-id="29937-1006">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="29937-1006">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="29937-1007">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1007">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="29937-1008">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1008">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1009">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1009">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1010">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1010">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1011">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1011">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1012">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1012">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1013">The following example returns the index of various substrings inside "abc".</span><span class="sxs-lookup"><span data-stu-id="29937-1013">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="29937-1014">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1014">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> <span data-ttu-id="29937-1015">LEFT</span><span class="sxs-lookup"><span data-stu-id="29937-1015">LEFT</span></span>  
 <span data-ttu-id="29937-1016">Returns the left part of a string with the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="29937-1016">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="29937-1017">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1017">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="29937-1018">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1018">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1019">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1019">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="29937-1020">Is any valid numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1020">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1021">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1021">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1022">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1022">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1023">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1023">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1024">The following example returns the left part of "abc" for various length values.</span><span class="sxs-lookup"><span data-stu-id="29937-1024">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="29937-1025">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1025">Here is the result set.</span></span>  
  
```  
[{"$1": "a", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> <span data-ttu-id="29937-1026">LENGTH</span><span class="sxs-lookup"><span data-stu-id="29937-1026">LENGTH</span></span>  
 <span data-ttu-id="29937-1027">Returns the number of characters of the specified string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1027">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="29937-1028">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1028">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1029">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1029">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1030">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1030">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1031">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1031">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1032">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1032">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1033">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1033">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1034">The following example returns the length of a string.</span><span class="sxs-lookup"><span data-stu-id="29937-1034">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="29937-1035">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1035">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> <span data-ttu-id="29937-1036">LOWER</span><span class="sxs-lookup"><span data-stu-id="29937-1036">LOWER</span></span>  
 <span data-ttu-id="29937-1037">Returns a string expression after converting uppercase character data to lowercase.</span><span class="sxs-lookup"><span data-stu-id="29937-1037">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="29937-1038">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1038">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1039">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1039">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1040">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1040">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1041">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1041">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1042">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1042">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1043">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1043">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1044">The following example shows how to use LOWER in a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1044">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="29937-1045">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1045">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> <span data-ttu-id="29937-1046">LTRIM</span><span class="sxs-lookup"><span data-stu-id="29937-1046">LTRIM</span></span>  
 <span data-ttu-id="29937-1047">Returns a string expression after it removes leading blanks.</span><span class="sxs-lookup"><span data-stu-id="29937-1047">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="29937-1048">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1048">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1049">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1049">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1050">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1050">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1051">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1051">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1052">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1052">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1053">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1053">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1054">The following example shows how to use LTRIM inside a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1054">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="29937-1055">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1055">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> <span data-ttu-id="29937-1056">REPLACE</span><span class="sxs-lookup"><span data-stu-id="29937-1056">REPLACE</span></span>  
 <span data-ttu-id="29937-1057">Replaces all occurrences of a specified string value with another string value.</span><span class="sxs-lookup"><span data-stu-id="29937-1057">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="29937-1058">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1058">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="29937-1059">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1059">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1060">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1060">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1061">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1061">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1062">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1062">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1063">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1063">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1064">The following example shows how to use REPLACE in a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1064">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="29937-1065">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1065">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> <span data-ttu-id="29937-1066">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="29937-1066">REPLICATE</span></span>  
 <span data-ttu-id="29937-1067">Repeats a string value a specified number of times.</span><span class="sxs-lookup"><span data-stu-id="29937-1067">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="29937-1068">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1068">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="29937-1069">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1069">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1070">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1070">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="29937-1071">Is any valid numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1071">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1072">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1072">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1073">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1073">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1074">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1074">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1075">The following example shows how to use REPLICATE in a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1075">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="29937-1076">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1076">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> <span data-ttu-id="29937-1077">REVERSE</span><span class="sxs-lookup"><span data-stu-id="29937-1077">REVERSE</span></span>  
 <span data-ttu-id="29937-1078">Returns the reverse order of a string value.</span><span class="sxs-lookup"><span data-stu-id="29937-1078">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="29937-1079">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1079">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1080">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1080">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1081">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1081">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1082">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1082">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1083">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1083">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1084">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1084">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1085">The following example shows how to use REVERSE in a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1085">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="29937-1086">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1086">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> <span data-ttu-id="29937-1087">RIGHT</span><span class="sxs-lookup"><span data-stu-id="29937-1087">RIGHT</span></span>  
 <span data-ttu-id="29937-1088">Returns the right part of a string with the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="29937-1088">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="29937-1089">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1089">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="29937-1090">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1090">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1091">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1091">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="29937-1092">Is any valid numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1092">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1093">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1093">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1094">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1094">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1095">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1095">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1096">The following example returns the right part of "abc" for various length values.</span><span class="sxs-lookup"><span data-stu-id="29937-1096">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="29937-1097">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1097">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> <span data-ttu-id="29937-1098">RTRIM</span><span class="sxs-lookup"><span data-stu-id="29937-1098">RTRIM</span></span>  
 <span data-ttu-id="29937-1099">Returns a string expression after it removes trailing blanks.</span><span class="sxs-lookup"><span data-stu-id="29937-1099">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="29937-1100">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1100">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1101">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1101">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1102">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1102">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1103">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1103">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1104">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1104">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1105">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1105">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1106">The following example shows how to use RTRIM inside a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1106">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="29937-1107">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1107">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> <span data-ttu-id="29937-1108">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="29937-1108">STARTSWITH</span></span>  
 <span data-ttu-id="29937-1109">Returns a Boolean indicating whether the first string expression starts with the second.</span><span class="sxs-lookup"><span data-stu-id="29937-1109">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="29937-1110">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1110">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="29937-1111">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1111">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1112">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1112">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1113">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1113">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1114">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1114">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-1115">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1115">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1116">The following example checks if the string "abc" begins with "b" and "a".</span><span class="sxs-lookup"><span data-stu-id="29937-1116">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="29937-1117">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1117">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> <span data-ttu-id="29937-1118">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="29937-1118">SUBSTRING</span></span>  
 <span data-ttu-id="29937-1119">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span><span class="sxs-lookup"><span data-stu-id="29937-1119">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="29937-1120">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1120">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="29937-1121">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1121">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1122">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1122">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="29937-1123">Is any valid numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1123">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1124">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1124">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1125">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1125">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1126">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1126">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1127">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span><span class="sxs-lookup"><span data-stu-id="29937-1127">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="29937-1128">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1128">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
####  <a name="bk_tostring"></a> <span data-ttu-id="29937-1129">ToString</span><span class="sxs-lookup"><span data-stu-id="29937-1129">ToString</span></span>  
 <span data-ttu-id="29937-1130">Returns a string representation of scalar expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1130">Returns a string representation of scalar expression.</span></span> 
  
 <span data-ttu-id="29937-1131">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1131">**Syntax**</span></span>  
  
```  
ToString(<expr>)
```  
  
 <span data-ttu-id="29937-1132">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1132">**Arguments**</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="29937-1133">Is any valid scalar expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1133">Is any valid scalar expression.</span></span>  
  
 <span data-ttu-id="29937-1134">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1134">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1135">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1135">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1136">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1136">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1137">The following example shows how ToString behaves across different types.</span><span class="sxs-lookup"><span data-stu-id="29937-1137">The following example shows how ToString behaves across different types.</span></span>   
  
```  
SELECT ToString(1.0000), ToString("Hello World"), ToString(NaN), ToString(Infinity),
ToString(IS_STRING(ToString(undefined))), IS_STRING(ToString(0.1234), ToString(false), ToString(undefined))
```  
  
 <span data-ttu-id="29937-1138">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1138">Here is the result set.</span></span>  
  
```  
[{"$1": "1", "$2": "Hello World", "$3": "NaN", "$4": "Infinity", "$5": "false", "$6": true, "$7": "false"}]  
```  
 <span data-ttu-id="29937-1139">Given the following input:</span><span class="sxs-lookup"><span data-stu-id="29937-1139">Given the following input:</span></span>
```  
{"Products":[{"ProductID":1,"Weight":4,"WeightUnits":"lb"},{"ProductID":2,"Weight":32,"WeightUnits":"kg"},{"ProductID":3,"Weight":400,"WeightUnits":"g"},{"ProductID":4,"Weight":8999,"WeightUnits":"mg"}]}
```    
 <span data-ttu-id="29937-1140">The following example shows how ToString can be used with other string functions like CONCAT.</span><span class="sxs-lookup"><span data-stu-id="29937-1140">The following example shows how ToString can be used with other string functions like CONCAT.</span></span>   
 
```  
SELECT 
CONCAT(ToString(p.Weight), p.WeightUnits) 
FROM p in c.Products 
```  

 <span data-ttu-id="29937-1141">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1141">Here is the result set.</span></span>  
  
```  
[{"$1":"4lb" },
 {"$1":"32kg"},
 {"$1":"400g" },
 {"$1":"8999mg" }]

```  
<span data-ttu-id="29937-1142">Given the following input.</span><span class="sxs-lookup"><span data-stu-id="29937-1142">Given the following input.</span></span>
```
{"id":"08259","description":"Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX","nutrients":[{"id":"305","description":"Caffeine","units":"mg"},{"id":"306","description":"Cholesterol, HDL","nutritionValue":30,"units":"mg"},{"id":"307","description":"Sodium, NA","nutritionValue":612,"units":"mg"},{"id":"308","description":"Protein, ABP","nutritionValue":60,"units":"mg"},{"id":"309","description":"Zinc, ZN","nutritionValue":null,"units":"mg"}]}
```
 <span data-ttu-id="29937-1143">The following example shows how ToString can be used with other string functions like REPLACE.</span><span class="sxs-lookup"><span data-stu-id="29937-1143">The following example shows how ToString can be used with other string functions like REPLACE.</span></span>   
```
SELECT 
    n.id AS nutrientID,
    REPLACE(ToString(n.nutritionValue), "6", "9") AS nutritionVal
FROM food 
JOIN n IN food.nutrients
```
 <span data-ttu-id="29937-1144">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1144">Here is the result set.</span></span>  
 ```
[{"nutrientID":"305"},
{"nutrientID":"306","nutritionVal":"30"},
{"nutrientID":"307","nutritionVal":"912"},
{"nutrientID":"308","nutritionVal":"90"},
{"nutrientID":"309","nutritionVal":"null"}]
 ``` 
 
####  <a name="bk_trim"></a> <span data-ttu-id="29937-1145">TRIM</span><span class="sxs-lookup"><span data-stu-id="29937-1145">TRIM</span></span>  
 <span data-ttu-id="29937-1146">Returns a string expression after it removes leading and trailing blanks.</span><span class="sxs-lookup"><span data-stu-id="29937-1146">Returns a string expression after it removes leading and trailing blanks.</span></span>  
  
 <span data-ttu-id="29937-1147">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1147">**Syntax**</span></span>  
  
```  
TRIM(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1148">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1148">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1149">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1149">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1150">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1150">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1151">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1151">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1152">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1152">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1153">The following example shows how to use TRIM inside a query.</span><span class="sxs-lookup"><span data-stu-id="29937-1153">The following example shows how to use TRIM inside a query.</span></span>  
  
```  
SELECT TRIM("   abc"), TRIM("   abc   "), TRIM("abc   "), TRIM("abc")   
```  
  
 <span data-ttu-id="29937-1154">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1154">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc", "$4": "abc"}]  
``` 
####  <a name="bk_upper"></a> <span data-ttu-id="29937-1155">UPPER</span><span class="sxs-lookup"><span data-stu-id="29937-1155">UPPER</span></span>  
 <span data-ttu-id="29937-1156">Returns a string expression after converting lowercase character data to uppercase.</span><span class="sxs-lookup"><span data-stu-id="29937-1156">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="29937-1157">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1157">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="29937-1158">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1158">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="29937-1159">Is any valid string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1159">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="29937-1160">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1160">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1161">Returns a string expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1161">Returns a string expression.</span></span>  
  
 <span data-ttu-id="29937-1162">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1162">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1163">The following example shows how to use UPPER in a query</span><span class="sxs-lookup"><span data-stu-id="29937-1163">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="29937-1164">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1164">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> <span data-ttu-id="29937-1165">Array functions</span><span class="sxs-lookup"><span data-stu-id="29937-1165">Array functions</span></span>  
 <span data-ttu-id="29937-1166">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span><span class="sxs-lookup"><span data-stu-id="29937-1166">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="29937-1167">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="29937-1167">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="29937-1168">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="29937-1168">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="29937-1169">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="29937-1169">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="29937-1170">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="29937-1170">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a> <span data-ttu-id="29937-1171">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="29937-1171">ARRAY_CONCAT</span></span>  
 <span data-ttu-id="29937-1172">Returns an array that is the result of concatenating two or more array values.</span><span class="sxs-lookup"><span data-stu-id="29937-1172">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="29937-1173">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1173">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="29937-1174">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1174">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="29937-1175">Is any valid array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1175">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="29937-1176">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1176">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1177">Returns an array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1177">Returns an array expression.</span></span>  
  
 <span data-ttu-id="29937-1178">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1178">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1179">The following example how to concatenate two arrays.</span><span class="sxs-lookup"><span data-stu-id="29937-1179">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="29937-1180">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1180">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a> <span data-ttu-id="29937-1181">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="29937-1181">ARRAY_CONTAINS</span></span>  
<span data-ttu-id="29937-1182">Returns a Boolean indicating whether the array contains the specified value.</span><span class="sxs-lookup"><span data-stu-id="29937-1182">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="29937-1183">Can specify if the match is full or partial.</span><span class="sxs-lookup"><span data-stu-id="29937-1183">Can specify if the match is full or partial.</span></span> 

 <span data-ttu-id="29937-1184">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1184">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr> [, bool_expr])  
```  
  
 <span data-ttu-id="29937-1185">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1185">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="29937-1186">Is any valid array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1186">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="29937-1187">Is any valid expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1187">Is any valid expression.</span></span>  

-   `bool_expr`  
  
     <span data-ttu-id="29937-1188">Is any boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1188">Is any boolean expression.</span></span>       
  
 <span data-ttu-id="29937-1189">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1189">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1190">Returns a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-1190">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="29937-1191">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1191">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1192">The following example how to check for membership in an array using ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="29937-1192">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="29937-1193">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1193">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  

 <span data-ttu-id="29937-1194">The following example how to check for a partial match of a JSON in an array using ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="29937-1194">The following example how to check for a partial match of a JSON in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT  
    ARRAY_CONTAINS([{"name": "apples", "fresh": true}, {"name": "strawberries", "fresh": true}], {"name": "apples"}, true), 
    ARRAY_CONTAINS([{"name": "apples", "fresh": true}, {"name": "strawberries", "fresh": true}], {"name": "apples"}),
    ARRAY_CONTAINS([{"name": "apples", "fresh": true}, {"name": "strawberries", "fresh": true}], {"name": "mangoes"}, true) 
```  
  
 <span data-ttu-id="29937-1195">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1195">Here is the result set.</span></span>  
  
```  
[{
  "$1": true,
  "$2": false,
  "$3": false
}] 
```  
  
####  <a name="bk_array_length"></a> <span data-ttu-id="29937-1196">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="29937-1196">ARRAY_LENGTH</span></span>  
 <span data-ttu-id="29937-1197">Returns the number of elements of the specified array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1197">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="29937-1198">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1198">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="29937-1199">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1199">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="29937-1200">Is any valid array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1200">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="29937-1201">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1201">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1202">Returns a numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1202">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1203">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1203">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1204">The following example how to get the length of an array using ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="29937-1204">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="29937-1205">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1205">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a> <span data-ttu-id="29937-1206">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="29937-1206">ARRAY_SLICE</span></span>  
 <span data-ttu-id="29937-1207">Returns part of an array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1207">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="29937-1208">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1208">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="29937-1209">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1209">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="29937-1210">Is any valid array expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1210">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="29937-1211">Is any valid numeric expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1211">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="29937-1212">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1212">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1213">Returns a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-1213">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="29937-1214">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1214">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1215">The following example how to get a part of an array using ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="29937-1215">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="29937-1216">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1216">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> <span data-ttu-id="29937-1217">Spatial functions</span><span class="sxs-lookup"><span data-stu-id="29937-1217">Spatial functions</span></span>  
 <span data-ttu-id="29937-1218">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-1218">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="29937-1219">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="29937-1219">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="29937-1220">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="29937-1220">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="29937-1221">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="29937-1221">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="29937-1222">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="29937-1222">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="29937-1223">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="29937-1223">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> <span data-ttu-id="29937-1224">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="29937-1224">ST_DISTANCE</span></span>  
 <span data-ttu-id="29937-1225">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span><span class="sxs-lookup"><span data-stu-id="29937-1225">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="29937-1226">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1226">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="29937-1227">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1227">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1228">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1228">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="29937-1229">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1229">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1230">Returns a numeric expression containing the distance.</span><span class="sxs-lookup"><span data-stu-id="29937-1230">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="29937-1231">This is expressed in meters for the default reference system.</span><span class="sxs-lookup"><span data-stu-id="29937-1231">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="29937-1232">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1232">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1233">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span><span class="sxs-lookup"><span data-stu-id="29937-1233">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="29937-1234">.</span><span class="sxs-lookup"><span data-stu-id="29937-1234">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="29937-1235">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1235">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> <span data-ttu-id="29937-1236">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="29937-1236">ST_WITHIN</span></span>  
 <span data-ttu-id="29937-1237">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span><span class="sxs-lookup"><span data-stu-id="29937-1237">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="29937-1238">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1238">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="29937-1239">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1239">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1240">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1240">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1241">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1241">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="29937-1242">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1242">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1243">Returns a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-1243">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="29937-1244">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1244">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1245">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="29937-1245">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="29937-1246">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1246">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a> <span data-ttu-id="29937-1247">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="29937-1247">ST_INTERSECTS</span></span>  
 <span data-ttu-id="29937-1248">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span><span class="sxs-lookup"><span data-stu-id="29937-1248">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="29937-1249">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1249">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="29937-1250">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1250">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1251">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1251">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1252">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1252">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="29937-1253">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1253">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1254">Returns a Boolean value.</span><span class="sxs-lookup"><span data-stu-id="29937-1254">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="29937-1255">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1255">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1256">The following example shows how to find all areas that intersects with the given polygon.</span><span class="sxs-lookup"><span data-stu-id="29937-1256">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="29937-1257">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1257">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> <span data-ttu-id="29937-1258">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="29937-1258">ST_ISVALID</span></span>  
 <span data-ttu-id="29937-1259">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span><span class="sxs-lookup"><span data-stu-id="29937-1259">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="29937-1260">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1260">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="29937-1261">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1261">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1262">Is any valid GeoJSON Point, Polygon, or LineString expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1262">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="29937-1263">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1263">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1264">Returns a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1264">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="29937-1265">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1265">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1266">The following example shows how to check if a point is valid using ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="29937-1266">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="29937-1267">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span><span class="sxs-lookup"><span data-stu-id="29937-1267">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="29937-1268">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span><span class="sxs-lookup"><span data-stu-id="29937-1268">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="29937-1269">Points within a polygon must be specified in counter-clockwise order.</span><span class="sxs-lookup"><span data-stu-id="29937-1269">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="29937-1270">A polygon specified in clockwise order represents the inverse of the region within it.</span><span class="sxs-lookup"><span data-stu-id="29937-1270">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="29937-1271">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1271">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> <span data-ttu-id="29937-1272">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="29937-1272">ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="29937-1273">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span><span class="sxs-lookup"><span data-stu-id="29937-1273">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="29937-1274">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="29937-1274">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="29937-1275">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="29937-1275">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="29937-1276">Is any valid GeoJSON point or polygon expression.</span><span class="sxs-lookup"><span data-stu-id="29937-1276">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="29937-1277">**Return Types**</span><span class="sxs-lookup"><span data-stu-id="29937-1277">**Return Types**</span></span>  
  
 <span data-ttu-id="29937-1278">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span><span class="sxs-lookup"><span data-stu-id="29937-1278">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="29937-1279">**Examples**</span><span class="sxs-lookup"><span data-stu-id="29937-1279">**Examples**</span></span>  
  
 <span data-ttu-id="29937-1280">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="29937-1280">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="29937-1281">Here is the result set.</span><span class="sxs-lookup"><span data-stu-id="29937-1281">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="29937-1282">Next steps</span><span class="sxs-lookup"><span data-stu-id="29937-1282">Next steps</span></span>  
 <span data-ttu-id="29937-1283">[SQL syntax and SQL query for Azure Cosmos DB](sql-api-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="29937-1283">[SQL syntax and SQL query for Azure Cosmos DB](sql-api-sql-query.md) </span></span>  
 [<span data-ttu-id="29937-1284">Azure Cosmos DB documentation</span><span class="sxs-lookup"><span data-stu-id="29937-1284">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/azure/cosmos-db/)  
  
  
