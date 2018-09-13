---
title: Lucene query examples for Azure Search | Microsoft Docs
description: Lucene query syntax for fuzzy search, proximity search, term boosting, regular expression search, and wildcard searches in an Azure Search service.
author: HeidiSteen
manager: cgronlun
tags: Lucene query analyzer syntax
services: search
ms.service: search
ms.topic: conceptual
ms.date: 08/09/2018
ms.author: heidist
ms.openlocfilehash: b5a3e2eac218ba2aa6958ffc56bd59f5b513cf48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810432"
---
# <a name="lucene-syntax-query-examples-for-building-advanced-queries-in-azure-search"></a><span data-ttu-id="0071d-103">Lucene syntax query examples for building advanced queries in Azure Search</span><span class="sxs-lookup"><span data-stu-id="0071d-103">Lucene syntax query examples for building advanced queries in Azure Search</span></span>
<span data-ttu-id="0071d-104">When constructing queries for Azure Search, you can replace the default [simple query parser](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) with the more expansive [Lucene Query Parser in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) to formulate specialized and advanced query definitions.</span><span class="sxs-lookup"><span data-stu-id="0071d-104">When constructing queries for Azure Search, you can replace the default [simple query parser](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) with the more expansive [Lucene Query Parser in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) to formulate specialized and advanced query definitions.</span></span> 

<span data-ttu-id="0071d-105">The Lucene Query Parser supports complex query constructs, such as field-scoped queries, fuzzy and prefix wildcard search, proximity search, term boosting, and regular expression search.</span><span class="sxs-lookup"><span data-stu-id="0071d-105">The Lucene Query Parser supports complex query constructs, such as field-scoped queries, fuzzy and prefix wildcard search, proximity search, term boosting, and regular expression search.</span></span> <span data-ttu-id="0071d-106">The additional power comes with additional processing requirements so you should expect a slightly longer execution time.</span><span class="sxs-lookup"><span data-stu-id="0071d-106">The additional power comes with additional processing requirements so you should expect a slightly longer execution time.</span></span> <span data-ttu-id="0071d-107">In this article, you can step through examples demonstrating query operations available when using the full syntax.</span><span class="sxs-lookup"><span data-stu-id="0071d-107">In this article, you can step through examples demonstrating query operations available when using the full syntax.</span></span>

> [!Note]
> <span data-ttu-id="0071d-108">Many of the specialized query constructions enabled through the full Lucene query syntax are not [text-analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), which can be surprising if you expect stemming or lemmatization.</span><span class="sxs-lookup"><span data-stu-id="0071d-108">Many of the specialized query constructions enabled through the full Lucene query syntax are not [text-analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), which can be surprising if you expect stemming or lemmatization.</span></span> <span data-ttu-id="0071d-109">Lexical analysis is only performed on complete terms (a term query or phrase query).</span><span class="sxs-lookup"><span data-stu-id="0071d-109">Lexical analysis is only performed on complete terms (a term query or phrase query).</span></span> <span data-ttu-id="0071d-110">Query types with incomplete terms (prefix query, wildcard query, regex query, fuzzy query) are added directly to the query tree, bypassing the analysis stage.</span><span class="sxs-lookup"><span data-stu-id="0071d-110">Query types with incomplete terms (prefix query, wildcard query, regex query, fuzzy query) are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="0071d-111">The only transformation performed on incomplete query terms is lowercasing.</span><span class="sxs-lookup"><span data-stu-id="0071d-111">The only transformation performed on incomplete query terms is lowercasing.</span></span> 
>

## <a name="formulate-requests-in-postman"></a><span data-ttu-id="0071d-112">Formulate requests in Postman</span><span class="sxs-lookup"><span data-stu-id="0071d-112">Formulate requests in Postman</span></span>

<span data-ttu-id="0071d-113">The following examples leverage a NYC Jobs search index consisting of jobs available based on a dataset provided by the [City of New York OpenData](https://opendata.cityofnewyork.us/) initiative.</span><span class="sxs-lookup"><span data-stu-id="0071d-113">The following examples leverage a NYC Jobs search index consisting of jobs available based on a dataset provided by the [City of New York OpenData](https://opendata.cityofnewyork.us/) initiative.</span></span> <span data-ttu-id="0071d-114">This data should not be considered current or complete.</span><span class="sxs-lookup"><span data-stu-id="0071d-114">This data should not be considered current or complete.</span></span> <span data-ttu-id="0071d-115">The index is on a sandbox service provided by Microsoft, which means you do not need an Azure subscription or Azure Search to try these queries.</span><span class="sxs-lookup"><span data-stu-id="0071d-115">The index is on a sandbox service provided by Microsoft, which means you do not need an Azure subscription or Azure Search to try these queries.</span></span>

<span data-ttu-id="0071d-116">What you do need is Postman or an equivalent tool for issuing HTTP request on GET.</span><span class="sxs-lookup"><span data-stu-id="0071d-116">What you do need is Postman or an equivalent tool for issuing HTTP request on GET.</span></span> <span data-ttu-id="0071d-117">For more information, see [Explore with REST clients](search-fiddler.md).</span><span class="sxs-lookup"><span data-stu-id="0071d-117">For more information, see [Explore with REST clients](search-fiddler.md).</span></span>

### <a name="set-the-request-header"></a><span data-ttu-id="0071d-118">Set the request header</span><span class="sxs-lookup"><span data-stu-id="0071d-118">Set the request header</span></span>

1. <span data-ttu-id="0071d-119">In the request header, set **Content-Type** to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="0071d-119">In the request header, set **Content-Type** to `application/json`.</span></span>

2. <span data-ttu-id="0071d-120">Add an **api-key**, and set it to this string: `252044BE3886FE4A8E3BAA4F595114BB`.</span><span class="sxs-lookup"><span data-stu-id="0071d-120">Add an **api-key**, and set it to this string: `252044BE3886FE4A8E3BAA4F595114BB`.</span></span> <span data-ttu-id="0071d-121">This is a query key for the sandbox search service hosting the NYC Jobs index.</span><span class="sxs-lookup"><span data-stu-id="0071d-121">This is a query key for the sandbox search service hosting the NYC Jobs index.</span></span>

<span data-ttu-id="0071d-122">After you specify the request header, you can reuse it for all of the queries in this article, swapping out only the **search=** string.</span><span class="sxs-lookup"><span data-stu-id="0071d-122">After you specify the request header, you can reuse it for all of the queries in this article, swapping out only the **search=** string.</span></span> 

  ![Postman request header](media/search-query-lucene-examples/postman-header.png)

### <a name="set-the-request-url"></a><span data-ttu-id="0071d-124">Set the request URL</span><span class="sxs-lookup"><span data-stu-id="0071d-124">Set the request URL</span></span>

<span data-ttu-id="0071d-125">Request is a GET command paired with a URL containing the Azure Search endpoint and search string.</span><span class="sxs-lookup"><span data-stu-id="0071d-125">Request is a GET command paired with a URL containing the Azure Search endpoint and search string.</span></span>

  ![Postman request header](media/search-query-lucene-examples/postman-basic-url-request-elements.png)

<span data-ttu-id="0071d-127">URL composition has the following elements:</span><span class="sxs-lookup"><span data-stu-id="0071d-127">URL composition has the following elements:</span></span>

+ <span data-ttu-id="0071d-128">**`https://azs-playground.search.windows.net/`** is a sandbox search service maintained by the Azure Search development team.</span><span class="sxs-lookup"><span data-stu-id="0071d-128">**`https://azs-playground.search.windows.net/`** is a sandbox search service maintained by the Azure Search development team.</span></span> 
+ <span data-ttu-id="0071d-129">**`indexes/nycjobs/`** is the NYC Jobs index in the indexes collection of that service.</span><span class="sxs-lookup"><span data-stu-id="0071d-129">**`indexes/nycjobs/`** is the NYC Jobs index in the indexes collection of that service.</span></span> <span data-ttu-id="0071d-130">Both the service name and index are required on the request.</span><span class="sxs-lookup"><span data-stu-id="0071d-130">Both the service name and index are required on the request.</span></span>
+ <span data-ttu-id="0071d-131">**`docs`** is the documents collection containing all searchable content.</span><span class="sxs-lookup"><span data-stu-id="0071d-131">**`docs`** is the documents collection containing all searchable content.</span></span> <span data-ttu-id="0071d-132">The query api-key provided in the request header only works on read operations targeting the documents collection.</span><span class="sxs-lookup"><span data-stu-id="0071d-132">The query api-key provided in the request header only works on read operations targeting the documents collection.</span></span>
+ <span data-ttu-id="0071d-133">**`api-version=2017-11-11`** sets the api-version, which is a required parameter on every request.</span><span class="sxs-lookup"><span data-stu-id="0071d-133">**`api-version=2017-11-11`** sets the api-version, which is a required parameter on every request.</span></span>
+ <span data-ttu-id="0071d-134">**`search=*`** is the query string, which in the initial query is null, returning the first 50 results (by default).</span><span class="sxs-lookup"><span data-stu-id="0071d-134">**`search=*`** is the query string, which in the initial query is null, returning the first 50 results (by default).</span></span>

## <a name="send-your-first-query"></a><span data-ttu-id="0071d-135">Send your first query</span><span class="sxs-lookup"><span data-stu-id="0071d-135">Send your first query</span></span>

<span data-ttu-id="0071d-136">As a verification step, paste the following request into GET and click **Send**.</span><span class="sxs-lookup"><span data-stu-id="0071d-136">As a verification step, paste the following request into GET and click **Send**.</span></span> <span data-ttu-id="0071d-137">Results are returned as verbose JSON documents.</span><span class="sxs-lookup"><span data-stu-id="0071d-137">Results are returned as verbose JSON documents.</span></span> <span data-ttu-id="0071d-138">You can copy-paste this URL in first example below.</span><span class="sxs-lookup"><span data-stu-id="0071d-138">You can copy-paste this URL in first example below.</span></span>

  ```http
  https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&search=*
  ```

<span data-ttu-id="0071d-139">The query string, **`search=*`**, is an unspecified search equivalent to null or empty search.</span><span class="sxs-lookup"><span data-stu-id="0071d-139">The query string, **`search=*`**, is an unspecified search equivalent to null or empty search.</span></span> <span data-ttu-id="0071d-140">It's not especially useful, but it is the simplest search you can do.</span><span class="sxs-lookup"><span data-stu-id="0071d-140">It's not especially useful, but it is the simplest search you can do.</span></span>

<span data-ttu-id="0071d-141">Optionally, you can add **`$count=true`** to the URL to return a count of the documents matching the search criteria.</span><span class="sxs-lookup"><span data-stu-id="0071d-141">Optionally, you can add **`$count=true`** to the URL to return a count of the documents matching the search criteria.</span></span> <span data-ttu-id="0071d-142">On an empty search string, this is all the documents in the index (about 2800 in the case of NYC Jobs).</span><span class="sxs-lookup"><span data-stu-id="0071d-142">On an empty search string, this is all the documents in the index (about 2800 in the case of NYC Jobs).</span></span>

## <a name="how-to-invoke-full-lucene-parsing"></a><span data-ttu-id="0071d-143">How to invoke full Lucene parsing</span><span class="sxs-lookup"><span data-stu-id="0071d-143">How to invoke full Lucene parsing</span></span>

<span data-ttu-id="0071d-144">Add **queryType=full** to invoke the full query syntax, overriding the default simple query syntax.</span><span class="sxs-lookup"><span data-stu-id="0071d-144">Add **queryType=full** to invoke the full query syntax, overriding the default simple query syntax.</span></span> 

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&queryType=full&search=*
```

<span data-ttu-id="0071d-145">All of the examples in this article specify the **queryType=full** search parameter, indicating that the full syntax is handled by the Lucene Query Parser.</span><span class="sxs-lookup"><span data-stu-id="0071d-145">All of the examples in this article specify the **queryType=full** search parameter, indicating that the full syntax is handled by the Lucene Query Parser.</span></span> 

## <a name="example-1-field-scoped-query"></a><span data-ttu-id="0071d-146">Example 1: Field-scoped query</span><span class="sxs-lookup"><span data-stu-id="0071d-146">Example 1: Field-scoped query</span></span>

<span data-ttu-id="0071d-147">This first example is not parser-specific, but we lead with it to introduce the first fundamental query concept: containment.</span><span class="sxs-lookup"><span data-stu-id="0071d-147">This first example is not parser-specific, but we lead with it to introduce the first fundamental query concept: containment.</span></span> <span data-ttu-id="0071d-148">This example scopes query execution and the response to just a few specific fields.</span><span class="sxs-lookup"><span data-stu-id="0071d-148">This example scopes query execution and the response to just a few specific fields.</span></span> <span data-ttu-id="0071d-149">Knowing how to structure a readable JSON response is important when your tool is Postman or Search explorer.</span><span class="sxs-lookup"><span data-stu-id="0071d-149">Knowing how to structure a readable JSON response is important when your tool is Postman or Search explorer.</span></span> 

<span data-ttu-id="0071d-150">For brevity, the query targets only the *business_title* field and specifies only business titles are returned.</span><span class="sxs-lookup"><span data-stu-id="0071d-150">For brevity, the query targets only the *business_title* field and specifies only business titles are returned.</span></span> <span data-ttu-id="0071d-151">The syntax is **searchFields** to restrict query execution to just the business_title field, and **select** to specify which fields are included in the response.</span><span class="sxs-lookup"><span data-stu-id="0071d-151">The syntax is **searchFields** to restrict query execution to just the business_title field, and **select** to specify which fields are included in the response.</span></span>

```http
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&search=*
```

<span data-ttu-id="0071d-152">Response for this query should look similar to the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="0071d-152">Response for this query should look similar to the following screenshot.</span></span>

  ![Postman sample response](media/search-query-lucene-examples/postman-sample-results.png)

<span data-ttu-id="0071d-154">You might have noticed the search score in the response.</span><span class="sxs-lookup"><span data-stu-id="0071d-154">You might have noticed the search score in the response.</span></span> <span data-ttu-id="0071d-155">Uniform scores of 1 occur when there is no rank, either because the search was not full text search, or because no criteria was applied.</span><span class="sxs-lookup"><span data-stu-id="0071d-155">Uniform scores of 1 occur when there is no rank, either because the search was not full text search, or because no criteria was applied.</span></span> <span data-ttu-id="0071d-156">For null search with no criteria, rows come back in arbitrary order.</span><span class="sxs-lookup"><span data-stu-id="0071d-156">For null search with no criteria, rows come back in arbitrary order.</span></span> <span data-ttu-id="0071d-157">When you include actual criteria, you will see search scores evolve into meaningful values.</span><span class="sxs-lookup"><span data-stu-id="0071d-157">When you include actual criteria, you will see search scores evolve into meaningful values.</span></span>

## <a name="example-2-intra-field-filtering"></a><span data-ttu-id="0071d-158">Example 2: Intra-field filtering</span><span class="sxs-lookup"><span data-stu-id="0071d-158">Example 2: Intra-field filtering</span></span>

<span data-ttu-id="0071d-159">Full Lucene syntax supports expressions within a field.</span><span class="sxs-lookup"><span data-stu-id="0071d-159">Full Lucene syntax supports expressions within a field.</span></span> <span data-ttu-id="0071d-160">This query searches for business titles with the term senior in them, but not junior:</span><span class="sxs-lookup"><span data-stu-id="0071d-160">This query searches for business titles with the term senior in them, but not junior:</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:senior+NOT+junior
```

  ![Postman sample response](media/search-query-lucene-examples/intrafieldfilter.png)

<span data-ttu-id="0071d-162">By specifying a **fieldname:searchterm** construction, you can define a fielded query operation, where the field is a single word, and the search term is also a single word or a phrase, optionally with Boolean operators.</span><span class="sxs-lookup"><span data-stu-id="0071d-162">By specifying a **fieldname:searchterm** construction, you can define a fielded query operation, where the field is a single word, and the search term is also a single word or a phrase, optionally with Boolean operators.</span></span> <span data-ttu-id="0071d-163">Some examples include the following:</span><span class="sxs-lookup"><span data-stu-id="0071d-163">Some examples include the following:</span></span>

* <span data-ttu-id="0071d-164">business_title:(senior NOT junior)</span><span class="sxs-lookup"><span data-stu-id="0071d-164">business_title:(senior NOT junior)</span></span>
* <span data-ttu-id="0071d-165">state:("New York" AND "New Jersey")</span><span class="sxs-lookup"><span data-stu-id="0071d-165">state:("New York" AND "New Jersey")</span></span>

<span data-ttu-id="0071d-166">Be sure to put multiple strings within quotation marks if you want both strings to be evaluated as a single entity, as in this case searching for two distinct cities in the location field.</span><span class="sxs-lookup"><span data-stu-id="0071d-166">Be sure to put multiple strings within quotation marks if you want both strings to be evaluated as a single entity, as in this case searching for two distinct cities in the location field.</span></span> <span data-ttu-id="0071d-167">Also, ensure the operator is capitalized as you see with NOT and AND.</span><span class="sxs-lookup"><span data-stu-id="0071d-167">Also, ensure the operator is capitalized as you see with NOT and AND.</span></span>

<span data-ttu-id="0071d-168">The field specified in **fieldname:searchterm** must be a searchable field.</span><span class="sxs-lookup"><span data-stu-id="0071d-168">The field specified in **fieldname:searchterm** must be a searchable field.</span></span> <span data-ttu-id="0071d-169">See [Create Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) for details on how index attributes are used in field definitions.</span><span class="sxs-lookup"><span data-stu-id="0071d-169">See [Create Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) for details on how index attributes are used in field definitions.</span></span>

## <a name="example-3-fuzzy-search"></a><span data-ttu-id="0071d-170">Example 3: Fuzzy search</span><span class="sxs-lookup"><span data-stu-id="0071d-170">Example 3: Fuzzy search</span></span>

<span data-ttu-id="0071d-171">Full Lucene syntax also supports fuzzy search, matching on terms that have a similar construction.</span><span class="sxs-lookup"><span data-stu-id="0071d-171">Full Lucene syntax also supports fuzzy search, matching on terms that have a similar construction.</span></span> <span data-ttu-id="0071d-172">To do a fuzzy search, append the tilde `~` symbol at the end of a single word with an optional parameter, a value between 0 and 2, that specifies the edit distance.</span><span class="sxs-lookup"><span data-stu-id="0071d-172">To do a fuzzy search, append the tilde `~` symbol at the end of a single word with an optional parameter, a value between 0 and 2, that specifies the edit distance.</span></span> <span data-ttu-id="0071d-173">For example, `blue~` or `blue~1` would return blue, blues, and glue.</span><span class="sxs-lookup"><span data-stu-id="0071d-173">For example, `blue~` or `blue~1` would return blue, blues, and glue.</span></span>

<span data-ttu-id="0071d-174">This query searches for jobs with the term "associate" (deliberately misspelled):</span><span class="sxs-lookup"><span data-stu-id="0071d-174">This query searches for jobs with the term "associate" (deliberately misspelled):</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:asosiate~
```
  ![Fuzzy search response](media/search-query-lucene-examples/fuzzysearch.png)

<span data-ttu-id="0071d-176">Per [Lucene documentation](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), fuzzy searches are based on [Damerau-Levenshtein Distance](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).</span><span class="sxs-lookup"><span data-stu-id="0071d-176">Per [Lucene documentation](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), fuzzy searches are based on [Damerau-Levenshtein Distance](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).</span></span>

> [!Note]
> <span data-ttu-id="0071d-177">Fuzzy queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis).</span><span class="sxs-lookup"><span data-stu-id="0071d-177">Fuzzy queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis).</span></span> <span data-ttu-id="0071d-178">Query types with incomplete terms (prefix query, wildcard query, regex query, fuzzy query) are added directly to the query tree, bypassing the analysis stage.</span><span class="sxs-lookup"><span data-stu-id="0071d-178">Query types with incomplete terms (prefix query, wildcard query, regex query, fuzzy query) are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="0071d-179">The only transformation performed on incomplete query terms is lowercasing.</span><span class="sxs-lookup"><span data-stu-id="0071d-179">The only transformation performed on incomplete query terms is lowercasing.</span></span>
>

## <a name="example-4-proximity-search"></a><span data-ttu-id="0071d-180">Example 4: Proximity search</span><span class="sxs-lookup"><span data-stu-id="0071d-180">Example 4: Proximity search</span></span>
<span data-ttu-id="0071d-181">Proximity searches are used to find terms that are near each other in a document.</span><span class="sxs-lookup"><span data-stu-id="0071d-181">Proximity searches are used to find terms that are near each other in a document.</span></span> <span data-ttu-id="0071d-182">Insert a tilde "~" symbol at the end of a phrase followed by the number of words that create the proximity boundary.</span><span class="sxs-lookup"><span data-stu-id="0071d-182">Insert a tilde "~" symbol at the end of a phrase followed by the number of words that create the proximity boundary.</span></span> <span data-ttu-id="0071d-183">For example, "hotel airport"~5 will find the terms hotel and airport within 5 words of each other in a document.</span><span class="sxs-lookup"><span data-stu-id="0071d-183">For example, "hotel airport"~5 will find the terms hotel and airport within 5 words of each other in a document.</span></span>

<span data-ttu-id="0071d-184">In this query, for jobs with the term "senior analyst" where it is separated by no more than one word:</span><span class="sxs-lookup"><span data-stu-id="0071d-184">In this query, for jobs with the term "senior analyst" where it is separated by no more than one word:</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:%22senior%20analyst%22~1
```
  ![Proximity query](media/search-query-lucene-examples/proximity-before.png)

<span data-ttu-id="0071d-186">Try it again removing the words between the term "senior analyst".</span><span class="sxs-lookup"><span data-stu-id="0071d-186">Try it again removing the words between the term "senior analyst".</span></span> <span data-ttu-id="0071d-187">Notice that 8 documents are returned for this query as opposed to 10 for the previous query.</span><span class="sxs-lookup"><span data-stu-id="0071d-187">Notice that 8 documents are returned for this query as opposed to 10 for the previous query.</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:%22senior%20analyst%22~0
```

## <a name="example-5-term-boosting"></a><span data-ttu-id="0071d-188">Example 5: Term boosting</span><span class="sxs-lookup"><span data-stu-id="0071d-188">Example 5: Term boosting</span></span>
<span data-ttu-id="0071d-189">Term boosting refers to ranking a document higher if it contains the boosted term, relative to documents that do not contain the term.</span><span class="sxs-lookup"><span data-stu-id="0071d-189">Term boosting refers to ranking a document higher if it contains the boosted term, relative to documents that do not contain the term.</span></span> <span data-ttu-id="0071d-190">To boost a term, use the caret, "^", symbol with a boost factor (a number) at the end of the term you are searching.</span><span class="sxs-lookup"><span data-stu-id="0071d-190">To boost a term, use the caret, "^", symbol with a boost factor (a number) at the end of the term you are searching.</span></span> 

<span data-ttu-id="0071d-191">In this "before" query, search for jobs with the term *computer analyst* and notice there are no results with both words *computer* and *analyst*, yet *computer* jobs are at the top of the results.</span><span class="sxs-lookup"><span data-stu-id="0071d-191">In this "before" query, search for jobs with the term *computer analyst* and notice there are no results with both words *computer* and *analyst*, yet *computer* jobs are at the top of the results.</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:computer%20analyst
```
  ![Term boosting before](media/search-query-lucene-examples/termboostingbefore.png)

<span data-ttu-id="0071d-193">In the "after" query, repeat the search, this time boosting results with the term *analyst* over the term *computer* if both words do not exist.</span><span class="sxs-lookup"><span data-stu-id="0071d-193">In the "after" query, repeat the search, this time boosting results with the term *analyst* over the term *computer* if both words do not exist.</span></span> 

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:computer%20analyst%5e2
```
<span data-ttu-id="0071d-194">A more human readable version of the above query is `search=business_title:computer analyst^2`.</span><span class="sxs-lookup"><span data-stu-id="0071d-194">A more human readable version of the above query is `search=business_title:computer analyst^2`.</span></span> <span data-ttu-id="0071d-195">For a workable query, `^2` is encoded as `%5E2`, which is harder to see.</span><span class="sxs-lookup"><span data-stu-id="0071d-195">For a workable query, `^2` is encoded as `%5E2`, which is harder to see.</span></span>

  ![Term boosting after](media/search-query-lucene-examples/termboostingafter.png)

<span data-ttu-id="0071d-197">Term boosting differs from scoring profiles in that scoring profiles boost certain fields, rather than specific terms.</span><span class="sxs-lookup"><span data-stu-id="0071d-197">Term boosting differs from scoring profiles in that scoring profiles boost certain fields, rather than specific terms.</span></span> <span data-ttu-id="0071d-198">The following example helps illustrate the differences.</span><span class="sxs-lookup"><span data-stu-id="0071d-198">The following example helps illustrate the differences.</span></span>

<span data-ttu-id="0071d-199">Consider a scoring profile that boosts matches in a certain field, such as **genre** in the musicstoreindex example.</span><span class="sxs-lookup"><span data-stu-id="0071d-199">Consider a scoring profile that boosts matches in a certain field, such as **genre** in the musicstoreindex example.</span></span> <span data-ttu-id="0071d-200">Term boosting could be used to further boost certain search terms higher than others.</span><span class="sxs-lookup"><span data-stu-id="0071d-200">Term boosting could be used to further boost certain search terms higher than others.</span></span> <span data-ttu-id="0071d-201">For example, "rock^2 electronic" will boost documents that contain the search terms in the **genre** field higher than other searchable fields in the index.</span><span class="sxs-lookup"><span data-stu-id="0071d-201">For example, "rock^2 electronic" will boost documents that contain the search terms in the **genre** field higher than other searchable fields in the index.</span></span> <span data-ttu-id="0071d-202">Furthermore, documents that contain the search term "rock" will be ranked higher than the other search term "electronic" as a result of the term boost value (2).</span><span class="sxs-lookup"><span data-stu-id="0071d-202">Furthermore, documents that contain the search term "rock" will be ranked higher than the other search term "electronic" as a result of the term boost value (2).</span></span>

<span data-ttu-id="0071d-203">When setting the factor level, the higher the boost factor, the more relevant the term will be relative to other search terms.</span><span class="sxs-lookup"><span data-stu-id="0071d-203">When setting the factor level, the higher the boost factor, the more relevant the term will be relative to other search terms.</span></span> <span data-ttu-id="0071d-204">By default, the boost factor is 1.</span><span class="sxs-lookup"><span data-stu-id="0071d-204">By default, the boost factor is 1.</span></span> <span data-ttu-id="0071d-205">Although the boost factor must be positive, it can be less than 1 (for example, 0.2).</span><span class="sxs-lookup"><span data-stu-id="0071d-205">Although the boost factor must be positive, it can be less than 1 (for example, 0.2).</span></span>


## <a name="example-6-regex"></a><span data-ttu-id="0071d-206">Example 6: Regex</span><span class="sxs-lookup"><span data-stu-id="0071d-206">Example 6: Regex</span></span>

<span data-ttu-id="0071d-207">A regular expression search finds a match based on the contents between forward slashes "/", as documented in the [RegExp class](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).</span><span class="sxs-lookup"><span data-stu-id="0071d-207">A regular expression search finds a match based on the contents between forward slashes "/", as documented in the [RegExp class](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).</span></span>

<span data-ttu-id="0071d-208">In this query, search for jobs with either the term Senior or Junior: \`search=business_title:/(Sen|Jun)ior/\`\`.</span><span class="sxs-lookup"><span data-stu-id="0071d-208">In this query, search for jobs with either the term Senior or Junior: \`search=business_title:/(Sen|Jun)ior/\`\`.</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:/(Sen|Jun)ior/
```

  ![Regex query](media/search-query-lucene-examples/regex.png)

> [!Note]
> <span data-ttu-id="0071d-210">Regex queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis).</span><span class="sxs-lookup"><span data-stu-id="0071d-210">Regex queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis).</span></span> <span data-ttu-id="0071d-211">The only transformation performed on incomplete query terms is lowercasing.</span><span class="sxs-lookup"><span data-stu-id="0071d-211">The only transformation performed on incomplete query terms is lowercasing.</span></span>
>

## <a name="example-7-wildcard-search"></a><span data-ttu-id="0071d-212">Example 7: Wildcard search</span><span class="sxs-lookup"><span data-stu-id="0071d-212">Example 7: Wildcard search</span></span>
<span data-ttu-id="0071d-213">You can use generally recognized syntax for multiple (\*) or single (?) character wildcard searches.</span><span class="sxs-lookup"><span data-stu-id="0071d-213">You can use generally recognized syntax for multiple (\*) or single (?) character wildcard searches.</span></span> <span data-ttu-id="0071d-214">Note the Lucene query parser supports the use of these symbols with a single term, and not a phrase.</span><span class="sxs-lookup"><span data-stu-id="0071d-214">Note the Lucene query parser supports the use of these symbols with a single term, and not a phrase.</span></span>

<span data-ttu-id="0071d-215">In this query, search for jobs that contain the prefix 'prog' which would include business titles with the terms programming and programmer in it.</span><span class="sxs-lookup"><span data-stu-id="0071d-215">In this query, search for jobs that contain the prefix 'prog' which would include business titles with the terms programming and programmer in it.</span></span> <span data-ttu-id="0071d-216">You cannot use a \* or ?</span><span class="sxs-lookup"><span data-stu-id="0071d-216">You cannot use a \* or ?</span></span> <span data-ttu-id="0071d-217">symbol as the first character of a search.</span><span class="sxs-lookup"><span data-stu-id="0071d-217">symbol as the first character of a search.</span></span>

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:prog*
```
  ![Wildcard query](media/search-query-lucene-examples/wildcard.png)

> [!Note]
> <span data-ttu-id="0071d-219">Wildcard queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis).</span><span class="sxs-lookup"><span data-stu-id="0071d-219">Wildcard queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis).</span></span> <span data-ttu-id="0071d-220">The only transformation performed on incomplete query terms is lowercasing.</span><span class="sxs-lookup"><span data-stu-id="0071d-220">The only transformation performed on incomplete query terms is lowercasing.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="0071d-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="0071d-221">Next steps</span></span>
<span data-ttu-id="0071d-222">Try specifying the Lucene Query Parser in your code.</span><span class="sxs-lookup"><span data-stu-id="0071d-222">Try specifying the Lucene Query Parser in your code.</span></span> <span data-ttu-id="0071d-223">The following links explain how to set up search queries for both .NET and the REST API.</span><span class="sxs-lookup"><span data-stu-id="0071d-223">The following links explain how to set up search queries for both .NET and the REST API.</span></span> <span data-ttu-id="0071d-224">The links use the default simple syntax so you will need to apply what you learned from this article to specify the **queryType**.</span><span class="sxs-lookup"><span data-stu-id="0071d-224">The links use the default simple syntax so you will need to apply what you learned from this article to specify the **queryType**.</span></span>

* [<span data-ttu-id="0071d-225">Query your Azure Search Index using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0071d-225">Query your Azure Search Index using the .NET SDK</span></span>](search-query-dotnet.md)
* [<span data-ttu-id="0071d-226">Query your Azure Search Index using the REST API</span><span class="sxs-lookup"><span data-stu-id="0071d-226">Query your Azure Search Index using the REST API</span></span>](search-query-rest-api.md)

<span data-ttu-id="0071d-227">Additional syntax reference, query architecture, and examples can be found in the following links:</span><span class="sxs-lookup"><span data-stu-id="0071d-227">Additional syntax reference, query architecture, and examples can be found in the following links:</span></span>

+ [<span data-ttu-id="0071d-228">Simple syntax query examples</span><span class="sxs-lookup"><span data-stu-id="0071d-228">Simple syntax query examples</span></span>](search-query-simple-examples.md)
+ [<span data-ttu-id="0071d-229">How full text search works in Azure Search</span><span class="sxs-lookup"><span data-stu-id="0071d-229">How full text search works in Azure Search</span></span>](search-lucene-query-architecture.md)
+ [<span data-ttu-id="0071d-230">Simple query syntax</span><span class="sxs-lookup"><span data-stu-id="0071d-230">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)
+ [<span data-ttu-id="0071d-231">Full Lucene query syntax</span><span class="sxs-lookup"><span data-stu-id="0071d-231">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)