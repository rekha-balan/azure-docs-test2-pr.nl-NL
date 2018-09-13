---
title: Full text search engine (Lucene) architecture in Azure Search | Microsoft Docs
description: Explanation of Lucene query processing and document retrieval concepts for full text search, as related to Azure Search.
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: ''
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: 00c1ca3f4251698d97747966fb219028e412639d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661327"
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="752b4-103">How full text search works in Azure Search</span><span class="sxs-lookup"><span data-stu-id="752b4-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="752b4-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="752b4-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="752b4-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span><span class="sxs-lookup"><span data-stu-id="752b4-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="752b4-106">In these situations, having a background in the four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes to query parameters or index configuration that will deliver the desired outcome.</span><span class="sxs-lookup"><span data-stu-id="752b4-106">In these situations, having a background in the four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes to query parameters or index configuration that will deliver the desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="752b4-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span><span class="sxs-lookup"><span data-stu-id="752b4-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="752b4-108">We selectively expose and extend Lucene functionality to enable the scenarios important to Azure Search.</span><span class="sxs-lookup"><span data-stu-id="752b4-108">We selectively expose and extend Lucene functionality to enable the scenarios important to Azure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="752b4-109">Architecture overview and diagram</span><span class="sxs-lookup"><span data-stu-id="752b4-109">Architecture overview and diagram</span></span>

<span data-ttu-id="752b4-110">Processing a full text search query starts with parsing the query text to extract search terms.</span><span class="sxs-lookup"><span data-stu-id="752b4-110">Processing a full text search query starts with parsing the query text to extract search terms.</span></span> <span data-ttu-id="752b4-111">The search engine uses an index to retrieve documents with matching terms.</span><span class="sxs-lookup"><span data-stu-id="752b4-111">The search engine uses an index to retrieve documents with matching terms.</span></span> <span data-ttu-id="752b4-112">Individual query terms are sometimes broken down and reconstituted into new forms to cast a broader net over what could be considered as a potential match.</span><span class="sxs-lookup"><span data-stu-id="752b4-112">Individual query terms are sometimes broken down and reconstituted into new forms to cast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="752b4-113">A result set is then sorted by a relevance score assigned to each individual matching document.</span><span class="sxs-lookup"><span data-stu-id="752b4-113">A result set is then sorted by a relevance score assigned to each individual matching document.</span></span> <span data-ttu-id="752b4-114">Those at the top of the ranked list are returned to the calling application.</span><span class="sxs-lookup"><span data-stu-id="752b4-114">Those at the top of the ranked list are returned to the calling application.</span></span>

<span data-ttu-id="752b4-115">Restated, query execution has four stages:</span><span class="sxs-lookup"><span data-stu-id="752b4-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="752b4-116">Query parsing</span><span class="sxs-lookup"><span data-stu-id="752b4-116">Query parsing</span></span> 
2. <span data-ttu-id="752b4-117">Lexical analysis</span><span class="sxs-lookup"><span data-stu-id="752b4-117">Lexical analysis</span></span> 
3. <span data-ttu-id="752b4-118">Document retrieval</span><span class="sxs-lookup"><span data-stu-id="752b4-118">Document retrieval</span></span> 
4. <span data-ttu-id="752b4-119">Scoring</span><span class="sxs-lookup"><span data-stu-id="752b4-119">Scoring</span></span> 

<span data-ttu-id="752b4-120">The diagram below illustrates the components used to process a search request.</span><span class="sxs-lookup"><span data-stu-id="752b4-120">The diagram below illustrates the components used to process a search request.</span></span> 

 ![Lucene query architecture diagram in Azure Search][1]


| <span data-ttu-id="752b4-122">Key components</span><span class="sxs-lookup"><span data-stu-id="752b4-122">Key components</span></span> | <span data-ttu-id="752b4-123">Functional description</span><span class="sxs-lookup"><span data-stu-id="752b4-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="752b4-124">**Query parsers**</span><span class="sxs-lookup"><span data-stu-id="752b4-124">**Query parsers**</span></span> | <span data-ttu-id="752b4-125">Separate query terms from query operators and create the query structure (a query tree) to be sent to the search engine.</span><span class="sxs-lookup"><span data-stu-id="752b4-125">Separate query terms from query operators and create the query structure (a query tree) to be sent to the search engine.</span></span> |
|<span data-ttu-id="752b4-126">**Analyzers**</span><span class="sxs-lookup"><span data-stu-id="752b4-126">**Analyzers**</span></span> | <span data-ttu-id="752b4-127">Perform lexical analysis on query terms.</span><span class="sxs-lookup"><span data-stu-id="752b4-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="752b4-128">This process can involve transforming, removing, or expanding of query terms.</span><span class="sxs-lookup"><span data-stu-id="752b4-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="752b4-129">**Index**</span><span class="sxs-lookup"><span data-stu-id="752b4-129">**Index**</span></span> | <span data-ttu-id="752b4-130">An efficient data structure used to store and organize searchable terms extracted from indexed documents.</span><span class="sxs-lookup"><span data-stu-id="752b4-130">An efficient data structure used to store and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="752b4-131">**Search engine**</span><span class="sxs-lookup"><span data-stu-id="752b4-131">**Search engine**</span></span> | <span data-ttu-id="752b4-132">Retrieves and scores matching documents based on the contents of the inverted index.</span><span class="sxs-lookup"><span data-stu-id="752b4-132">Retrieves and scores matching documents based on the contents of the inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="752b4-133">Anatomy of a search request</span><span class="sxs-lookup"><span data-stu-id="752b4-133">Anatomy of a search request</span></span>

<span data-ttu-id="752b4-134">A search request is a complete specification of what should be returned in a result set.</span><span class="sxs-lookup"><span data-stu-id="752b4-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="752b4-135">In simplest form, it is an empty query with no criteria of any kind.</span><span class="sxs-lookup"><span data-stu-id="752b4-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="752b4-136">A more realistic example includes parameters, several query terms, perhaps scoped to certain fields, with possibly a filter expression and ordering rules.</span><span class="sxs-lookup"><span data-stu-id="752b4-136">A more realistic example includes parameters, several query terms, perhaps scoped to certain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="752b4-137">The following example is a search request you might send to Azure Search using the [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="752b4-137">The following example is a search request you might send to Azure Search using the [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

<span data-ttu-id="752b4-138">For this request, the search engine does the following:</span><span class="sxs-lookup"><span data-stu-id="752b4-138">For this request, the search engine does the following:</span></span>

1. <span data-ttu-id="752b4-139">Filters out documents where the price is at least $60 and less than $300.</span><span class="sxs-lookup"><span data-stu-id="752b4-139">Filters out documents where the price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="752b4-140">Executes the query.</span><span class="sxs-lookup"><span data-stu-id="752b4-140">Executes the query.</span></span> <span data-ttu-id="752b4-141">In this example, the search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in the example allows us to explain how analyzers handle it).</span><span class="sxs-lookup"><span data-stu-id="752b4-141">In this example, the search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in the example allows us to explain how analyzers handle it).</span></span> <span data-ttu-id="752b4-142">For this query, the search engine scans the description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on the term "spacious", or on terms that start with the prefix "air-condition".</span><span class="sxs-lookup"><span data-stu-id="752b4-142">For this query, the search engine scans the description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on the term "spacious", or on terms that start with the prefix "air-condition".</span></span> <span data-ttu-id="752b4-143">The `searchMode` parameter is used to match on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span><span class="sxs-lookup"><span data-stu-id="752b4-143">The `searchMode` parameter is used to match on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="752b4-144">Orders the resulting set of hotels by proximity to a given geography location, and then returned to the calling application.</span><span class="sxs-lookup"><span data-stu-id="752b4-144">Orders the resulting set of hotels by proximity to a given geography location, and then returned to the calling application.</span></span> 

<span data-ttu-id="752b4-145">The majority of this article is about processing of the *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="752b4-145">The majority of this article is about processing of the *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="752b4-146">Filtering and ordering are out of scope.</span><span class="sxs-lookup"><span data-stu-id="752b4-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="752b4-147">For more information, see the [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="752b4-147">For more information, see the [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="752b4-148">Stage 1: Query parsing</span><span class="sxs-lookup"><span data-stu-id="752b4-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="752b4-149">As noted, the query string is the first line of the request:</span><span class="sxs-lookup"><span data-stu-id="752b4-149">As noted, the query string is the first line of the request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="752b4-150">The query parser separates operators (such as `*` and `+` in the example) from search terms, and deconstructs the search query into *subqueries* of a supported type:</span><span class="sxs-lookup"><span data-stu-id="752b4-150">The query parser separates operators (such as `*` and `+` in the example) from search terms, and deconstructs the search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="752b4-151">*term query* for standalone terms (like spacious)</span><span class="sxs-lookup"><span data-stu-id="752b4-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="752b4-152">*phrase query* for quoted terms (like ocean view)</span><span class="sxs-lookup"><span data-stu-id="752b4-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="752b4-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span><span class="sxs-lookup"><span data-stu-id="752b4-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="752b4-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="752b4-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="752b4-155">Operators associated with a subquery determine whether the query "must be" or "should be" satisfied in order for a document to be considered a match.</span><span class="sxs-lookup"><span data-stu-id="752b4-155">Operators associated with a subquery determine whether the query "must be" or "should be" satisfied in order for a document to be considered a match.</span></span> <span data-ttu-id="752b4-156">For example, `+"Ocean view"` is "must" due to the `+` operator.</span><span class="sxs-lookup"><span data-stu-id="752b4-156">For example, `+"Ocean view"` is "must" due to the `+` operator.</span></span> 

<span data-ttu-id="752b4-157">The query parser restructures the subqueries into a *query tree* (an internal structure representing the query) it passes on to the search engine.</span><span class="sxs-lookup"><span data-stu-id="752b4-157">The query parser restructures the subqueries into a *query tree* (an internal structure representing the query) it passes on to the search engine.</span></span> <span data-ttu-id="752b4-158">In the first stage of query parsing, the query tree looks like this.</span><span class="sxs-lookup"><span data-stu-id="752b4-158">In the first stage of query parsing, the query tree looks like this.</span></span>  

 ![Boolean query searchmode any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="752b4-160">Supported parsers: Simple and Full Lucene</span><span class="sxs-lookup"><span data-stu-id="752b4-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="752b4-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span><span class="sxs-lookup"><span data-stu-id="752b4-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="752b4-162">By setting the `queryType` parameter with your search request, you tell the query parser which query language you choose so that it knows how to interpret the operators and syntax.</span><span class="sxs-lookup"><span data-stu-id="752b4-162">By setting the `queryType` parameter with your search request, you tell the query parser which query language you choose so that it knows how to interpret the operators and syntax.</span></span> <span data-ttu-id="752b4-163">The [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable to interpret user input as-is without client-side processing.</span><span class="sxs-lookup"><span data-stu-id="752b4-163">The [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable to interpret user input as-is without client-side processing.</span></span> <span data-ttu-id="752b4-164">It supports query operators familiar from web search engines.</span><span class="sxs-lookup"><span data-stu-id="752b4-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="752b4-165">The [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends the default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span><span class="sxs-lookup"><span data-stu-id="752b4-165">The [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends the default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="752b4-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span><span class="sxs-lookup"><span data-stu-id="752b4-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="752b4-167">The example request in this article uses the Full Lucene query language.</span><span class="sxs-lookup"><span data-stu-id="752b4-167">The example request in this article uses the Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-the-parser"></a><span data-ttu-id="752b4-168">Impact of searchMode on the parser</span><span class="sxs-lookup"><span data-stu-id="752b4-168">Impact of searchMode on the parser</span></span> 

<span data-ttu-id="752b4-169">Another search request parameter that affects parsing is the `searchMode` parameter.</span><span class="sxs-lookup"><span data-stu-id="752b4-169">Another search request parameter that affects parsing is the `searchMode` parameter.</span></span> <span data-ttu-id="752b4-170">It controls the default operator for Boolean queries: any (default) or all.</span><span class="sxs-lookup"><span data-stu-id="752b4-170">It controls the default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="752b4-171">When `searchMode=any`, which is the default, the space delimiter between spacious and air-condition is OR (`||`), making the sample query text equivalent to:</span><span class="sxs-lookup"><span data-stu-id="752b4-171">When `searchMode=any`, which is the default, the space delimiter between spacious and air-condition is OR (`||`), making the sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="752b4-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (the term *must* match).</span><span class="sxs-lookup"><span data-stu-id="752b4-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (the term *must* match).</span></span> <span data-ttu-id="752b4-173">Less obvious is how to interpret the remaining terms: spacious and air-condition.</span><span class="sxs-lookup"><span data-stu-id="752b4-173">Less obvious is how to interpret the remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="752b4-174">Should the search engine find matches on ocean view *and* spacious *and* air-condition?</span><span class="sxs-lookup"><span data-stu-id="752b4-174">Should the search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="752b4-175">Or should it find ocean view plus *either one* of the remaining terms?</span><span class="sxs-lookup"><span data-stu-id="752b4-175">Or should it find ocean view plus *either one* of the remaining terms?</span></span> 

<span data-ttu-id="752b4-176">By default (`searchMode=any`), the search engine assumes the broader interpretation.</span><span class="sxs-lookup"><span data-stu-id="752b4-176">By default (`searchMode=any`), the search engine assumes the broader interpretation.</span></span> <span data-ttu-id="752b4-177">Either field *should* be matched, reflecting "or" semantics.</span><span class="sxs-lookup"><span data-stu-id="752b4-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="752b4-178">The initial query tree illustrated previously, with the two "should" operations, shows the default.</span><span class="sxs-lookup"><span data-stu-id="752b4-178">The initial query tree illustrated previously, with the two "should" operations, shows the default.</span></span>  

<span data-ttu-id="752b4-179">Suppose that we now set `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="752b4-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="752b4-180">In this case, the space is interpreted as an "and" operation.</span><span class="sxs-lookup"><span data-stu-id="752b4-180">In this case, the space is interpreted as an "and" operation.</span></span> <span data-ttu-id="752b4-181">Each of the remaining terms must both be present in the document to qualify as a match.</span><span class="sxs-lookup"><span data-stu-id="752b4-181">Each of the remaining terms must both be present in the document to qualify as a match.</span></span> <span data-ttu-id="752b4-182">The resulting sample query would be interpreted as follows:</span><span class="sxs-lookup"><span data-stu-id="752b4-182">The resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="752b4-183">A modified query tree for this query would be as follows, where a matching document is the intersection of all three subqueries:</span><span class="sxs-lookup"><span data-stu-id="752b4-183">A modified query tree for this query would be as follows, where a matching document is the intersection of all three subqueries:</span></span> 

 ![Boolean query searchmode all][3]

> [!Note] 
> <span data-ttu-id="752b4-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span><span class="sxs-lookup"><span data-stu-id="752b4-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="752b4-186">Users who are likely to include operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span><span class="sxs-lookup"><span data-stu-id="752b4-186">Users who are likely to include operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="752b4-187">For more about the interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="752b4-187">For more about the interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="752b4-188">Stage 2: Lexical analysis</span><span class="sxs-lookup"><span data-stu-id="752b4-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="752b4-189">Lexical analyzers process *term queries* and *phrase queries* after the query tree is structured.</span><span class="sxs-lookup"><span data-stu-id="752b4-189">Lexical analyzers process *term queries* and *phrase queries* after the query tree is structured.</span></span> <span data-ttu-id="752b4-190">An analyzer accepts the text inputs given to it by the parser, processes the text, and then sends back tokenized terms to be incorporated into the query tree.</span><span class="sxs-lookup"><span data-stu-id="752b4-190">An analyzer accepts the text inputs given to it by the parser, processes the text, and then sends back tokenized terms to be incorporated into the query tree.</span></span> 

<span data-ttu-id="752b4-191">The most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific to a given language:</span><span class="sxs-lookup"><span data-stu-id="752b4-191">The most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific to a given language:</span></span> 

* <span data-ttu-id="752b4-192">Reducing a query term to the root form of a word</span><span class="sxs-lookup"><span data-stu-id="752b4-192">Reducing a query term to the root form of a word</span></span> 
* <span data-ttu-id="752b4-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span><span class="sxs-lookup"><span data-stu-id="752b4-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="752b4-194">Breaking a composite word into component parts</span><span class="sxs-lookup"><span data-stu-id="752b4-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="752b4-195">Lower casing an upper case word</span><span class="sxs-lookup"><span data-stu-id="752b4-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="752b4-196">All of these operations tend to erase differences between the text input provided by the user and the terms stored in the index.</span><span class="sxs-lookup"><span data-stu-id="752b4-196">All of these operations tend to erase differences between the text input provided by the user and the terms stored in the index.</span></span> <span data-ttu-id="752b4-197">Such operations go beyond text processing and require in-depth knowledge of the language itself.</span><span class="sxs-lookup"><span data-stu-id="752b4-197">Such operations go beyond text processing and require in-depth knowledge of the language itself.</span></span> <span data-ttu-id="752b4-198">To add this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span><span class="sxs-lookup"><span data-stu-id="752b4-198">To add this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="752b4-199">Analysis requirements can range from minimal to elaborate depending on your scenario.</span><span class="sxs-lookup"><span data-stu-id="752b4-199">Analysis requirements can range from minimal to elaborate depending on your scenario.</span></span> <span data-ttu-id="752b4-200">You can control complexity of lexical analysis by the selecting one of the predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="752b4-200">You can control complexity of lexical analysis by the selecting one of the predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="752b4-201">Analyzers are scoped to searchable fields and are specified as part of a field definition.</span><span class="sxs-lookup"><span data-stu-id="752b4-201">Analyzers are scoped to searchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="752b4-202">This allows you to vary lexical analysis on a per-field basis.</span><span class="sxs-lookup"><span data-stu-id="752b4-202">This allows you to vary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="752b4-203">Unspecified, the *standard* Lucene analyzer is used.</span><span class="sxs-lookup"><span data-stu-id="752b4-203">Unspecified, the *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="752b4-204">In our example, prior to analysis, the initial query tree has the term "Spacious," with an uppercase "S" and a comma that the query parser interprets as a part of the query term (a comma is not considered a query language operator).</span><span class="sxs-lookup"><span data-stu-id="752b4-204">In our example, prior to analysis, the initial query tree has the term "Spacious," with an uppercase "S" and a comma that the query parser interprets as a part of the query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="752b4-205">When the default analyzer processes the term, it will lowercase "ocean view" and "spacious", and remove the comma character.</span><span class="sxs-lookup"><span data-stu-id="752b4-205">When the default analyzer processes the term, it will lowercase "ocean view" and "spacious", and remove the comma character.</span></span> <span data-ttu-id="752b4-206">The modified query tree will look as follows:</span><span class="sxs-lookup"><span data-stu-id="752b4-206">The modified query tree will look as follows:</span></span> 

 ![Boolean query with analyzed terms][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="752b4-208">Testing analyzer behaviors</span><span class="sxs-lookup"><span data-stu-id="752b4-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="752b4-209">The behavior of an analyzer can be tested using the [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="752b4-209">The behavior of an analyzer can be tested using the [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="752b4-210">Provide the text you want to analyze to see what terms given analyzer will generate.</span><span class="sxs-lookup"><span data-stu-id="752b4-210">Provide the text you want to analyze to see what terms given analyzer will generate.</span></span> <span data-ttu-id="752b4-211">For example, to see how the standard analyzer would process the text "air-condition", you can issue the following request:</span><span class="sxs-lookup"><span data-stu-id="752b4-211">For example, to see how the standard analyzer would process the text "air-condition", you can issue the following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="752b4-212">The standard analyzer breaks the input text into the following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span><span class="sxs-lookup"><span data-stu-id="752b4-212">The standard analyzer breaks the input text into the following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-to-lexical-analysis"></a><span data-ttu-id="752b4-213">Exceptions to lexical analysis</span><span class="sxs-lookup"><span data-stu-id="752b4-213">Exceptions to lexical analysis</span></span> 

<span data-ttu-id="752b4-214">Lexical analysis applies only to query types that require complete terms – either a term query or a phrase query.</span><span class="sxs-lookup"><span data-stu-id="752b4-214">Lexical analysis applies only to query types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="752b4-215">It doesn’t apply to query types with incomplete terms – prefix query, wildcard query, regex query – or to a fuzzy query.</span><span class="sxs-lookup"><span data-stu-id="752b4-215">It doesn’t apply to query types with incomplete terms – prefix query, wildcard query, regex query – or to a fuzzy query.</span></span> <span data-ttu-id="752b4-216">Those query types, including the prefix query with term *air-condition\** in our example, are added directly to the query tree, bypassing the analysis stage.</span><span class="sxs-lookup"><span data-stu-id="752b4-216">Those query types, including the prefix query with term *air-condition\** in our example, are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="752b4-217">The only transformation performed on query terms of those types is lowercasing.</span><span class="sxs-lookup"><span data-stu-id="752b4-217">The only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="752b4-218">Stage 3: Document retrieval</span><span class="sxs-lookup"><span data-stu-id="752b4-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="752b4-219">Document retrieval refers to finding documents with matching terms in the index.</span><span class="sxs-lookup"><span data-stu-id="752b4-219">Document retrieval refers to finding documents with matching terms in the index.</span></span> <span data-ttu-id="752b4-220">This stage is understood best through an example.</span><span class="sxs-lookup"><span data-stu-id="752b4-220">This stage is understood best through an example.</span></span> <span data-ttu-id="752b4-221">Let's start with a hotels index having the following simple schema:</span><span class="sxs-lookup"><span data-stu-id="752b4-221">Let's start with a hotels index having the following simple schema:</span></span> 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

<span data-ttu-id="752b4-222">Further assume that this index contains the following four documents:</span><span class="sxs-lookup"><span data-stu-id="752b4-222">Further assume that this index contains the following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance to the beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on the north shore of the island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

<span data-ttu-id="752b4-223">**How terms are indexed**</span><span class="sxs-lookup"><span data-stu-id="752b4-223">**How terms are indexed**</span></span>

<span data-ttu-id="752b4-224">To understand retrieval, it helps to know a few basics about indexing.</span><span class="sxs-lookup"><span data-stu-id="752b4-224">To understand retrieval, it helps to know a few basics about indexing.</span></span> <span data-ttu-id="752b4-225">The unit of storage is an inverted index, one for each searchable field.</span><span class="sxs-lookup"><span data-stu-id="752b4-225">The unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="752b4-226">Within an inverted index is a sorted list of all terms from all documents.</span><span class="sxs-lookup"><span data-stu-id="752b4-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="752b4-227">Each term maps to the list of documents in which it occurs, as evident in the example below.</span><span class="sxs-lookup"><span data-stu-id="752b4-227">Each term maps to the list of documents in which it occurs, as evident in the example below.</span></span>

<span data-ttu-id="752b4-228">To produce the terms in an inverted index, the search engine performs lexical analysis over the content of documents, similar to what happens during query processing.</span><span class="sxs-lookup"><span data-stu-id="752b4-228">To produce the terms in an inverted index, the search engine performs lexical analysis over the content of documents, similar to what happens during query processing.</span></span> <span data-ttu-id="752b4-229">Text inputs are passed to an analyzer, lower-cased, stripped of punctuation, and so forth, depending on the analyzer configuration.</span><span class="sxs-lookup"><span data-stu-id="752b4-229">Text inputs are passed to an analyzer, lower-cased, stripped of punctuation, and so forth, depending on the analyzer configuration.</span></span> <span data-ttu-id="752b4-230">It's common, but not required, to use the same analyzers for search and indexing operations so that query terms look more like terms inside the index.</span><span class="sxs-lookup"><span data-stu-id="752b4-230">It's common, but not required, to use the same analyzers for search and indexing operations so that query terms look more like terms inside the index.</span></span>

> [!Note]
> <span data-ttu-id="752b4-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span><span class="sxs-lookup"><span data-stu-id="752b4-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="752b4-232">If unspecified, the analyzer set with the `analyzer` property is used for both indexing and searching.</span><span class="sxs-lookup"><span data-stu-id="752b4-232">If unspecified, the analyzer set with the `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="752b4-233">**Inverted index for example documents**</span><span class="sxs-lookup"><span data-stu-id="752b4-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="752b4-234">Returning to our example, for the **title** field, the inverted index looks like this:</span><span class="sxs-lookup"><span data-stu-id="752b4-234">Returning to our example, for the **title** field, the inverted index looks like this:</span></span>

| <span data-ttu-id="752b4-235">Term</span><span class="sxs-lookup"><span data-stu-id="752b4-235">Term</span></span> | <span data-ttu-id="752b4-236">Document list</span><span class="sxs-lookup"><span data-stu-id="752b4-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="752b4-237">atman</span><span class="sxs-lookup"><span data-stu-id="752b4-237">atman</span></span> | <span data-ttu-id="752b4-238">1</span><span class="sxs-lookup"><span data-stu-id="752b4-238">1</span></span> |
| <span data-ttu-id="752b4-239">beach</span><span class="sxs-lookup"><span data-stu-id="752b4-239">beach</span></span> | <span data-ttu-id="752b4-240">2</span><span class="sxs-lookup"><span data-stu-id="752b4-240">2</span></span> |
| <span data-ttu-id="752b4-241">hotel</span><span class="sxs-lookup"><span data-stu-id="752b4-241">hotel</span></span> | <span data-ttu-id="752b4-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="752b4-242">1, 3</span></span> |
| <span data-ttu-id="752b4-243">ocean</span><span class="sxs-lookup"><span data-stu-id="752b4-243">ocean</span></span> | <span data-ttu-id="752b4-244">4</span><span class="sxs-lookup"><span data-stu-id="752b4-244">4</span></span>  |
| <span data-ttu-id="752b4-245">playa</span><span class="sxs-lookup"><span data-stu-id="752b4-245">playa</span></span> | <span data-ttu-id="752b4-246">3</span><span class="sxs-lookup"><span data-stu-id="752b4-246">3</span></span> |
| <span data-ttu-id="752b4-247">resort</span><span class="sxs-lookup"><span data-stu-id="752b4-247">resort</span></span> | <span data-ttu-id="752b4-248">3</span><span class="sxs-lookup"><span data-stu-id="752b4-248">3</span></span> |
| <span data-ttu-id="752b4-249">retreat</span><span class="sxs-lookup"><span data-stu-id="752b4-249">retreat</span></span> | <span data-ttu-id="752b4-250">4</span><span class="sxs-lookup"><span data-stu-id="752b4-250">4</span></span> |

<span data-ttu-id="752b4-251">In the title field, only *hotel* shows up in two documents: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="752b4-251">In the title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="752b4-252">For the **description** field, the index is as follows:</span><span class="sxs-lookup"><span data-stu-id="752b4-252">For the **description** field, the index is as follows:</span></span>

| <span data-ttu-id="752b4-253">Term</span><span class="sxs-lookup"><span data-stu-id="752b4-253">Term</span></span> | <span data-ttu-id="752b4-254">Document list</span><span class="sxs-lookup"><span data-stu-id="752b4-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="752b4-255">air</span><span class="sxs-lookup"><span data-stu-id="752b4-255">air</span></span> | <span data-ttu-id="752b4-256">3</span><span class="sxs-lookup"><span data-stu-id="752b4-256">3</span></span>
| <span data-ttu-id="752b4-257">and</span><span class="sxs-lookup"><span data-stu-id="752b4-257">and</span></span> | <span data-ttu-id="752b4-258">4</span><span class="sxs-lookup"><span data-stu-id="752b4-258">4</span></span>
| <span data-ttu-id="752b4-259">beach</span><span class="sxs-lookup"><span data-stu-id="752b4-259">beach</span></span> | <span data-ttu-id="752b4-260">1</span><span class="sxs-lookup"><span data-stu-id="752b4-260">1</span></span>
| <span data-ttu-id="752b4-261">conditioned</span><span class="sxs-lookup"><span data-stu-id="752b4-261">conditioned</span></span> | <span data-ttu-id="752b4-262">3</span><span class="sxs-lookup"><span data-stu-id="752b4-262">3</span></span>
| <span data-ttu-id="752b4-263">comfortable</span><span class="sxs-lookup"><span data-stu-id="752b4-263">comfortable</span></span> | <span data-ttu-id="752b4-264">3</span><span class="sxs-lookup"><span data-stu-id="752b4-264">3</span></span>
| <span data-ttu-id="752b4-265">distance</span><span class="sxs-lookup"><span data-stu-id="752b4-265">distance</span></span> | <span data-ttu-id="752b4-266">1</span><span class="sxs-lookup"><span data-stu-id="752b4-266">1</span></span>
| <span data-ttu-id="752b4-267">island</span><span class="sxs-lookup"><span data-stu-id="752b4-267">island</span></span> | <span data-ttu-id="752b4-268">2</span><span class="sxs-lookup"><span data-stu-id="752b4-268">2</span></span>
| <span data-ttu-id="752b4-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="752b4-269">kauaʻi</span></span> | <span data-ttu-id="752b4-270">2</span><span class="sxs-lookup"><span data-stu-id="752b4-270">2</span></span>
| <span data-ttu-id="752b4-271">located</span><span class="sxs-lookup"><span data-stu-id="752b4-271">located</span></span> | <span data-ttu-id="752b4-272">2</span><span class="sxs-lookup"><span data-stu-id="752b4-272">2</span></span>
| <span data-ttu-id="752b4-273">north</span><span class="sxs-lookup"><span data-stu-id="752b4-273">north</span></span> | <span data-ttu-id="752b4-274">2</span><span class="sxs-lookup"><span data-stu-id="752b4-274">2</span></span>
| <span data-ttu-id="752b4-275">ocean</span><span class="sxs-lookup"><span data-stu-id="752b4-275">ocean</span></span> | <span data-ttu-id="752b4-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="752b4-276">1, 2, 3</span></span>
| <span data-ttu-id="752b4-277">of</span><span class="sxs-lookup"><span data-stu-id="752b4-277">of</span></span> | <span data-ttu-id="752b4-278">2</span><span class="sxs-lookup"><span data-stu-id="752b4-278">2</span></span>
| <span data-ttu-id="752b4-279">on</span><span class="sxs-lookup"><span data-stu-id="752b4-279">on</span></span> |<span data-ttu-id="752b4-280">2</span><span class="sxs-lookup"><span data-stu-id="752b4-280">2</span></span>
| <span data-ttu-id="752b4-281">quiet</span><span class="sxs-lookup"><span data-stu-id="752b4-281">quiet</span></span> | <span data-ttu-id="752b4-282">4</span><span class="sxs-lookup"><span data-stu-id="752b4-282">4</span></span>
| <span data-ttu-id="752b4-283">rooms</span><span class="sxs-lookup"><span data-stu-id="752b4-283">rooms</span></span>  | <span data-ttu-id="752b4-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="752b4-284">1, 3</span></span>
| <span data-ttu-id="752b4-285">secluded</span><span class="sxs-lookup"><span data-stu-id="752b4-285">secluded</span></span> | <span data-ttu-id="752b4-286">4</span><span class="sxs-lookup"><span data-stu-id="752b4-286">4</span></span>
| <span data-ttu-id="752b4-287">shore</span><span class="sxs-lookup"><span data-stu-id="752b4-287">shore</span></span> | <span data-ttu-id="752b4-288">2</span><span class="sxs-lookup"><span data-stu-id="752b4-288">2</span></span>
| <span data-ttu-id="752b4-289">spacious</span><span class="sxs-lookup"><span data-stu-id="752b4-289">spacious</span></span> | <span data-ttu-id="752b4-290">1</span><span class="sxs-lookup"><span data-stu-id="752b4-290">1</span></span>
| <span data-ttu-id="752b4-291">the</span><span class="sxs-lookup"><span data-stu-id="752b4-291">the</span></span> | <span data-ttu-id="752b4-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="752b4-292">1, 2</span></span>
| <span data-ttu-id="752b4-293">to</span><span class="sxs-lookup"><span data-stu-id="752b4-293">to</span></span> | <span data-ttu-id="752b4-294">1</span><span class="sxs-lookup"><span data-stu-id="752b4-294">1</span></span>
| <span data-ttu-id="752b4-295">view</span><span class="sxs-lookup"><span data-stu-id="752b4-295">view</span></span> | <span data-ttu-id="752b4-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="752b4-296">1, 2, 3</span></span>
| <span data-ttu-id="752b4-297">walking</span><span class="sxs-lookup"><span data-stu-id="752b4-297">walking</span></span> | <span data-ttu-id="752b4-298">1</span><span class="sxs-lookup"><span data-stu-id="752b4-298">1</span></span>
| <span data-ttu-id="752b4-299">with</span><span class="sxs-lookup"><span data-stu-id="752b4-299">with</span></span> | <span data-ttu-id="752b4-300">3</span><span class="sxs-lookup"><span data-stu-id="752b4-300">3</span></span>


<span data-ttu-id="752b4-301">**Matching query terms against indexed terms**</span><span class="sxs-lookup"><span data-stu-id="752b4-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="752b4-302">Given the inverted indices above, let’s return to the sample query and see how matching documents are found for our example query.</span><span class="sxs-lookup"><span data-stu-id="752b4-302">Given the inverted indices above, let’s return to the sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="752b4-303">Recall that the final query tree looks like this:</span><span class="sxs-lookup"><span data-stu-id="752b4-303">Recall that the final query tree looks like this:</span></span> 

 ![Boolean query with analyzed terms][4]

<span data-ttu-id="752b4-305">During query execution, individual queries are executed against the searchable fields independently.</span><span class="sxs-lookup"><span data-stu-id="752b4-305">During query execution, individual queries are executed against the searchable fields independently.</span></span> 

+ <span data-ttu-id="752b4-306">The TermQuery, "spacious", matches document 1 (Hotel Atman).</span><span class="sxs-lookup"><span data-stu-id="752b4-306">The TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="752b4-307">The PrefixQuery, "air-condition\*", doesn't match any documents.</span><span class="sxs-lookup"><span data-stu-id="752b4-307">The PrefixQuery, "air-condition\*", doesn't match any documents.</span></span> 

  <span data-ttu-id="752b4-308">This is a behavior that sometimes confuses developers.</span><span class="sxs-lookup"><span data-stu-id="752b4-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="752b4-309">Although the term air-conditioned exists in the document, it is split into two terms by the default analyzer.</span><span class="sxs-lookup"><span data-stu-id="752b4-309">Although the term air-conditioned exists in the document, it is split into two terms by the default analyzer.</span></span> <span data-ttu-id="752b4-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span><span class="sxs-lookup"><span data-stu-id="752b4-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="752b4-311">Therefore terms with prefix "air-condition" are looked up in the inverted index and not found.</span><span class="sxs-lookup"><span data-stu-id="752b4-311">Therefore terms with prefix "air-condition" are looked up in the inverted index and not found.</span></span>

+ <span data-ttu-id="752b4-312">The PhraseQuery, "ocean view", looks up the terms "ocean" and "view" and checks the proximity of terms in the original document.</span><span class="sxs-lookup"><span data-stu-id="752b4-312">The PhraseQuery, "ocean view", looks up the terms "ocean" and "view" and checks the proximity of terms in the original document.</span></span> <span data-ttu-id="752b4-313">Documents 1, 2 and 3 match this query in the description field.</span><span class="sxs-lookup"><span data-stu-id="752b4-313">Documents 1, 2 and 3 match this query in the description field.</span></span> <span data-ttu-id="752b4-314">Notice document 4 has the term ocean in the title but isn’t considered a match, as we're looking for the "ocean view" phrase rather than individual words.</span><span class="sxs-lookup"><span data-stu-id="752b4-314">Notice document 4 has the term ocean in the title but isn’t considered a match, as we're looking for the "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="752b4-315">A search query is executed independently against all searchable fields in the Azure Search index unless you limit the fields set with the `searchFields` parameter, as illustrated in the example search request.</span><span class="sxs-lookup"><span data-stu-id="752b4-315">A search query is executed independently against all searchable fields in the Azure Search index unless you limit the fields set with the `searchFields` parameter, as illustrated in the example search request.</span></span> <span data-ttu-id="752b4-316">Documents that match in any of the selected fields are returned.</span><span class="sxs-lookup"><span data-stu-id="752b4-316">Documents that match in any of the selected fields are returned.</span></span> 

<span data-ttu-id="752b4-317">On the whole, for the query in question, the documents that match are 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="752b4-317">On the whole, for the query in question, the documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="752b4-318">Stage 4: Scoring</span><span class="sxs-lookup"><span data-stu-id="752b4-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="752b4-319">Every document in a search result set is assigned a relevance score.</span><span class="sxs-lookup"><span data-stu-id="752b4-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="752b4-320">The function of the relevance score is to rank higher those documents that best answer a user question as expressed by the search query.</span><span class="sxs-lookup"><span data-stu-id="752b4-320">The function of the relevance score is to rank higher those documents that best answer a user question as expressed by the search query.</span></span> <span data-ttu-id="752b4-321">The score is computed based on statistical properties of terms that matched.</span><span class="sxs-lookup"><span data-stu-id="752b4-321">The score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="752b4-322">At the core of the scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="752b4-322">At the core of the scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="752b4-323">In queries containing rare and common terms, TF/IDF promotes results containing the rare term.</span><span class="sxs-lookup"><span data-stu-id="752b4-323">In queries containing rare and common terms, TF/IDF promotes results containing the rare term.</span></span> <span data-ttu-id="752b4-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched the query *the president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span><span class="sxs-lookup"><span data-stu-id="752b4-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched the query *the president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="752b4-325">Scoring example</span><span class="sxs-lookup"><span data-stu-id="752b4-325">Scoring example</span></span>

<span data-ttu-id="752b4-326">Recall the three documents that matched our example query:</span><span class="sxs-lookup"><span data-stu-id="752b4-326">Recall the three documents that matched our example query:</span></span>
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance to the beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on the north shore of the island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="752b4-327">Document 1 matched the query best because both the term *spacious* and the required phrase *ocean view* occur in the description field.</span><span class="sxs-lookup"><span data-stu-id="752b4-327">Document 1 matched the query best because both the term *spacious* and the required phrase *ocean view* occur in the description field.</span></span> <span data-ttu-id="752b4-328">The next two documents match only the phrase *ocean view*.</span><span class="sxs-lookup"><span data-stu-id="752b4-328">The next two documents match only the phrase *ocean view*.</span></span> <span data-ttu-id="752b4-329">It might be surprising that the relevance score for document 2 and 3 is different even though they matched the query in the same way.</span><span class="sxs-lookup"><span data-stu-id="752b4-329">It might be surprising that the relevance score for document 2 and 3 is different even though they matched the query in the same way.</span></span> <span data-ttu-id="752b4-330">It's because the scoring formula has more components than just TF/IDF.</span><span class="sxs-lookup"><span data-stu-id="752b4-330">It's because the scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="752b4-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span><span class="sxs-lookup"><span data-stu-id="752b4-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="752b4-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) to understand how field length and other factors can influence the relevance score.</span><span class="sxs-lookup"><span data-stu-id="752b4-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) to understand how field length and other factors can influence the relevance score.</span></span>

<span data-ttu-id="752b4-333">Some query types (wildcard, prefix, regex) always contribute a constant score to the overall document score.</span><span class="sxs-lookup"><span data-stu-id="752b4-333">Some query types (wildcard, prefix, regex) always contribute a constant score to the overall document score.</span></span> <span data-ttu-id="752b4-334">This allows matches found through query expansion to be included in the results, but without affecting the ranking.</span><span class="sxs-lookup"><span data-stu-id="752b4-334">This allows matches found through query expansion to be included in the results, but without affecting the ranking.</span></span> 

<span data-ttu-id="752b4-335">An example illustrates why this matters.</span><span class="sxs-lookup"><span data-stu-id="752b4-335">An example illustrates why this matters.</span></span> <span data-ttu-id="752b4-336">Wildcard searches, including prefix searches, are ambiguous by definition because the input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour\*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span><span class="sxs-lookup"><span data-stu-id="752b4-336">Wildcard searches, including prefix searches, are ambiguous by definition because the input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour\*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="752b4-337">Given the nature of these results, there is no way to reasonably infer which terms are more valuable than others.</span><span class="sxs-lookup"><span data-stu-id="752b4-337">Given the nature of these results, there is no way to reasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="752b4-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span><span class="sxs-lookup"><span data-stu-id="752b4-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="752b4-339">In a multi-part search request that includes partial and complete terms, results from the partial input are incorporated with a constant score to avoid bias towards potentially unexpected matches.</span><span class="sxs-lookup"><span data-stu-id="752b4-339">In a multi-part search request that includes partial and complete terms, results from the partial input are incorporated with a constant score to avoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="752b4-340">Score tuning</span><span class="sxs-lookup"><span data-stu-id="752b4-340">Score tuning</span></span>

<span data-ttu-id="752b4-341">There are two ways to tune relevance scores in Azure Search:</span><span class="sxs-lookup"><span data-stu-id="752b4-341">There are two ways to tune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="752b4-342">**Scoring profiles** promote documents in the ranked list of results based on a set of rules.</span><span class="sxs-lookup"><span data-stu-id="752b4-342">**Scoring profiles** promote documents in the ranked list of results based on a set of rules.</span></span> <span data-ttu-id="752b4-343">In our example, we could consider documents that matched in the title field more relevant than documents that matched in the description field.</span><span class="sxs-lookup"><span data-stu-id="752b4-343">In our example, we could consider documents that matched in the title field more relevant than documents that matched in the description field.</span></span> <span data-ttu-id="752b4-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span><span class="sxs-lookup"><span data-stu-id="752b4-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="752b4-345">Learn more how to [add Scoring Profiles to a search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="752b4-345">Learn more how to [add Scoring Profiles to a search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="752b4-346">**Term boosting** (available only in the Full Lucene query syntax) provides a boosting operator `^` that can be applied to any part of the query tree.</span><span class="sxs-lookup"><span data-stu-id="752b4-346">**Term boosting** (available only in the Full Lucene query syntax) provides a boosting operator `^` that can be applied to any part of the query tree.</span></span> <span data-ttu-id="752b4-347">In our example, instead of searching on the prefix *air-condition*\*, one could search for either the exact term *air-condition* or the prefix, but documents that match on the exact term are ranked higher by applying boost to the term query: \*air-condition^2||air-condition\*\*.</span><span class="sxs-lookup"><span data-stu-id="752b4-347">In our example, instead of searching on the prefix *air-condition*\*, one could search for either the exact term *air-condition* or the prefix, but documents that match on the exact term are ranked higher by applying boost to the term query: \*air-condition^2||air-condition\*\*.</span></span> <span data-ttu-id="752b4-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="752b4-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="752b4-349">Scoring in a distributed index</span><span class="sxs-lookup"><span data-stu-id="752b4-349">Scoring in a distributed index</span></span>

<span data-ttu-id="752b4-350">All indexes in Azure Search are automatically split into multiple shards, allowing us to quickly distribute the index among multiple nodes during service scale up or scale down.</span><span class="sxs-lookup"><span data-stu-id="752b4-350">All indexes in Azure Search are automatically split into multiple shards, allowing us to quickly distribute the index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="752b4-351">When a search request is issued, it’s issued against each shard independently.</span><span class="sxs-lookup"><span data-stu-id="752b4-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="752b4-352">The results from each shard are then merged and ordered by score (if no other ordering is defined).</span><span class="sxs-lookup"><span data-stu-id="752b4-352">The results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="752b4-353">It is important to know that the scoring function weights query term frequency against its inverse document frequency in all documents within the shard, not across all shards!</span><span class="sxs-lookup"><span data-stu-id="752b4-353">It is important to know that the scoring function weights query term frequency against its inverse document frequency in all documents within the shard, not across all shards!</span></span>

<span data-ttu-id="752b4-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span><span class="sxs-lookup"><span data-stu-id="752b4-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="752b4-355">Fortunately, such differences tend to disappear as the number of documents in the index grows due to more even term distribution.</span><span class="sxs-lookup"><span data-stu-id="752b4-355">Fortunately, such differences tend to disappear as the number of documents in the index grows due to more even term distribution.</span></span> <span data-ttu-id="752b4-356">It’s not possible to assume on which shard any given document will be placed.</span><span class="sxs-lookup"><span data-stu-id="752b4-356">It’s not possible to assume on which shard any given document will be placed.</span></span> <span data-ttu-id="752b4-357">However, assuming a document key doesn't change, it will always be assigned to the same shard.</span><span class="sxs-lookup"><span data-stu-id="752b4-357">However, assuming a document key doesn't change, it will always be assigned to the same shard.</span></span>

<span data-ttu-id="752b4-358">In general, document score is not the best attribute for ordering documents if order stability is important.</span><span class="sxs-lookup"><span data-stu-id="752b4-358">In general, document score is not the best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="752b4-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of the same query.</span><span class="sxs-lookup"><span data-stu-id="752b4-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of the same query.</span></span> <span data-ttu-id="752b4-360">Document score should only give a general sense of document relevance relative to other documents in the results set.</span><span class="sxs-lookup"><span data-stu-id="752b4-360">Document score should only give a general sense of document relevance relative to other documents in the results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="752b4-361">Conclusion</span><span class="sxs-lookup"><span data-stu-id="752b4-361">Conclusion</span></span>

<span data-ttu-id="752b4-362">The success of internet search engines has raised expectations for full text search over private data.</span><span class="sxs-lookup"><span data-stu-id="752b4-362">The success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="752b4-363">For almost any kind of search experience, we now expect the engine to understand our intent, even when terms are misspelled or incomplete.</span><span class="sxs-lookup"><span data-stu-id="752b4-363">For almost any kind of search experience, we now expect the engine to understand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="752b4-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span><span class="sxs-lookup"><span data-stu-id="752b4-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="752b4-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach to processing in ways that distill, expand, and transform query terms to deliver a relevant result.</span><span class="sxs-lookup"><span data-stu-id="752b4-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach to processing in ways that distill, expand, and transform query terms to deliver a relevant result.</span></span> <span data-ttu-id="752b4-366">Given the inherent complexities, there are a lot of factors that can affect the outcome of a query.</span><span class="sxs-lookup"><span data-stu-id="752b4-366">Given the inherent complexities, there are a lot of factors that can affect the outcome of a query.</span></span> <span data-ttu-id="752b4-367">For this reason, investing the time to understand the mechanics of full text search offers tangible benefits when trying to work through unexpected results.</span><span class="sxs-lookup"><span data-stu-id="752b4-367">For this reason, investing the time to understand the mechanics of full text search offers tangible benefits when trying to work through unexpected results.</span></span>  

<span data-ttu-id="752b4-368">This article explored full text search in the context of Azure Search.</span><span class="sxs-lookup"><span data-stu-id="752b4-368">This article explored full text search in the context of Azure Search.</span></span> <span data-ttu-id="752b4-369">We hope it gives you sufficient background to recognize potential causes and resolutions for addressing common query problems.</span><span class="sxs-lookup"><span data-stu-id="752b4-369">We hope it gives you sufficient background to recognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="752b4-370">Next steps</span><span class="sxs-lookup"><span data-stu-id="752b4-370">Next steps</span></span>

+ <span data-ttu-id="752b4-371">Build the sample index, try out different queries and review results.</span><span class="sxs-lookup"><span data-stu-id="752b4-371">Build the sample index, try out different queries and review results.</span></span> <span data-ttu-id="752b4-372">For instructions, see [Build and query an index in the portal](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="752b4-372">For instructions, see [Build and query an index in the portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="752b4-373">Try additional query syntax from the [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in the portal.</span><span class="sxs-lookup"><span data-stu-id="752b4-373">Try additional query syntax from the [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in the portal.</span></span>

+ <span data-ttu-id="752b4-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want to tune ranking in your search application.</span><span class="sxs-lookup"><span data-stu-id="752b4-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want to tune ranking in your search application.</span></span>

+ <span data-ttu-id="752b4-375">Learn how to apply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="752b4-375">Learn how to apply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="752b4-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span><span class="sxs-lookup"><span data-stu-id="752b4-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

## <a name="see-also"></a><span data-ttu-id="752b4-377">See also</span><span class="sxs-lookup"><span data-stu-id="752b4-377">See also</span></span>

[<span data-ttu-id="752b4-378">Search Documents REST API</span><span class="sxs-lookup"><span data-stu-id="752b4-378">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="752b4-379">Simple query syntax</span><span class="sxs-lookup"><span data-stu-id="752b4-379">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="752b4-380">Full Lucene query syntax</span><span class="sxs-lookup"><span data-stu-id="752b4-380">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="752b4-381">Handle search results</span><span class="sxs-lookup"><span data-stu-id="752b4-381">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-lucene-query-architecture/architecture-diagram2.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-lucene-query-architecture/azsearch-queryparsing-should2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-lucene-query-architecture/azsearch-queryparsing-must2.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-lucene-query-architecture/azsearch-queryparsing-spacious2.png




