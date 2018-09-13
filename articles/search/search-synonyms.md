<properties
   pageTitle="Synonyms in Azure Search (preview) | Microsoft Docs"
   description="Preliminary documentation for the Synonyms (preview) feature, exposed in the Azure Search REST API."
   services="search"
   documentationCenter=""
   authors="mhko"
   manager="pablocas"
   editor=""/>

<tags
   ms.service="search"
   ms.devlang="rest-api"
   ms.workload="search"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.date="07/07/2016"
   ms.author="nateko"/>

# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="63cc2-103">Synonyms in Azure Search (preview)</span><span class="sxs-lookup"><span data-stu-id="63cc2-103">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="63cc2-104">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span><span class="sxs-lookup"><span data-stu-id="63cc2-104">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="63cc2-105">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span><span class="sxs-lookup"><span data-stu-id="63cc2-105">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="63cc2-106">In Azure Search, synonym expansion is done at query time.</span><span class="sxs-lookup"><span data-stu-id="63cc2-106">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="63cc2-107">You can add synonym maps to a service with no disruption to existing operations.</span><span class="sxs-lookup"><span data-stu-id="63cc2-107">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="63cc2-108">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span><span class="sxs-lookup"><span data-stu-id="63cc2-108">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="63cc2-109">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="63cc2-109">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="63cc2-110">Feature availability</span><span class="sxs-lookup"><span data-stu-id="63cc2-110">Feature availability</span></span>

<span data-ttu-id="63cc2-111">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="63cc2-111">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="63cc2-112">There is no Azure portal support at this time.</span><span class="sxs-lookup"><span data-stu-id="63cc2-112">There is no Azure portal support at this time.</span></span> <span data-ttu-id="63cc2-113">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span><span class="sxs-lookup"><span data-stu-id="63cc2-113">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="63cc2-114">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span><span class="sxs-lookup"><span data-stu-id="63cc2-114">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="63cc2-115">How to use synonyms in Azure search</span><span class="sxs-lookup"><span data-stu-id="63cc2-115">How to use synonyms in Azure search</span></span>

<span data-ttu-id="63cc2-116">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span><span class="sxs-lookup"><span data-stu-id="63cc2-116">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="63cc2-117">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span><span class="sxs-lookup"><span data-stu-id="63cc2-117">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="63cc2-118">Synonym maps and indexes are maintained independently.</span><span class="sxs-lookup"><span data-stu-id="63cc2-118">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="63cc2-119">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span><span class="sxs-lookup"><span data-stu-id="63cc2-119">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="63cc2-120">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span><span class="sxs-lookup"><span data-stu-id="63cc2-120">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="63cc2-121">Updating even a single entry requires a reload.</span><span class="sxs-lookup"><span data-stu-id="63cc2-121">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="63cc2-122">Incorporating synonyms into your search application is a two-step process:</span><span class="sxs-lookup"><span data-stu-id="63cc2-122">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="63cc2-123">Add a synonym map to your search service through the APIs below.</span><span class="sxs-lookup"><span data-stu-id="63cc2-123">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="63cc2-124">Configure a searchable field to use the synonym map in the index definition.</span><span class="sxs-lookup"><span data-stu-id="63cc2-124">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="63cc2-125">SynonymMaps Resource APIs</span><span class="sxs-lookup"><span data-stu-id="63cc2-125">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="63cc2-126">Add or update a synonym map under your service, using POST or PUT.</span><span class="sxs-lookup"><span data-stu-id="63cc2-126">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="63cc2-127">Synonym maps are uploaded to the service via POST or PUT.</span><span class="sxs-lookup"><span data-stu-id="63cc2-127">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="63cc2-128">Each rule must be delimited by the new line character ('\n').</span><span class="sxs-lookup"><span data-stu-id="63cc2-128">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="63cc2-129">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span><span class="sxs-lookup"><span data-stu-id="63cc2-129">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="63cc2-130">Each rule can have up to 20 expansions.</span><span class="sxs-lookup"><span data-stu-id="63cc2-130">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="63cc2-131">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span><span class="sxs-lookup"><span data-stu-id="63cc2-131">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="63cc2-132">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="63cc2-132">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="63cc2-133">You can create a new synonym map using HTTP POST, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="63cc2-133">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="63cc2-134">Alternatively, you can use PUT and specify the synonym map name on the URI.</span><span class="sxs-lookup"><span data-stu-id="63cc2-134">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="63cc2-135">If the synonym map does not exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="63cc2-135">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="63cc2-136">Apache Solr synonym format</span><span class="sxs-lookup"><span data-stu-id="63cc2-136">Apache Solr synonym format</span></span>

<span data-ttu-id="63cc2-137">The Solr format supports equivalent and explicit synonym mappings.</span><span class="sxs-lookup"><span data-stu-id="63cc2-137">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="63cc2-138">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="63cc2-138">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="63cc2-139">Below is a sample rule for equivalent synonyms.</span><span class="sxs-lookup"><span data-stu-id="63cc2-139">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="63cc2-140">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span><span class="sxs-lookup"><span data-stu-id="63cc2-140">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="63cc2-141">Explicit mapping is denoted by an arrow "=>".</span><span class="sxs-lookup"><span data-stu-id="63cc2-141">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="63cc2-142">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span><span class="sxs-lookup"><span data-stu-id="63cc2-142">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="63cc2-143">Given the rule below, search queries "Washington", "Wash."</span><span class="sxs-lookup"><span data-stu-id="63cc2-143">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="63cc2-144">or "WA" will all be rewritten to "WA".</span><span class="sxs-lookup"><span data-stu-id="63cc2-144">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="63cc2-145">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span><span class="sxs-lookup"><span data-stu-id="63cc2-145">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="63cc2-146">List synonym maps under your service.</span><span class="sxs-lookup"><span data-stu-id="63cc2-146">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="63cc2-147">Get a synonym map under your service.</span><span class="sxs-lookup"><span data-stu-id="63cc2-147">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="63cc2-148">Delete a synonyms map under your service.</span><span class="sxs-lookup"><span data-stu-id="63cc2-148">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="63cc2-149">Configure a searchable field to use the synonym map in the index definition.</span><span class="sxs-lookup"><span data-stu-id="63cc2-149">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="63cc2-150">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span><span class="sxs-lookup"><span data-stu-id="63cc2-150">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="63cc2-151">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span><span class="sxs-lookup"><span data-stu-id="63cc2-151">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="63cc2-152">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span><span class="sxs-lookup"><span data-stu-id="63cc2-152">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="63cc2-153">In this preview, you can only have one synonym map per field.</span><span class="sxs-lookup"><span data-stu-id="63cc2-153">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="63cc2-154">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="63cc2-154">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="63cc2-155">Impact of synonyms on other search features</span><span class="sxs-lookup"><span data-stu-id="63cc2-155">Impact of synonyms on other search features</span></span>

<span data-ttu-id="63cc2-156">The synonyms feature rewrites the original query with synonyms with the OR operator.</span><span class="sxs-lookup"><span data-stu-id="63cc2-156">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="63cc2-157">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span><span class="sxs-lookup"><span data-stu-id="63cc2-157">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="63cc2-158">Synonym feature applies to search queries and does not apply to filters or facets.</span><span class="sxs-lookup"><span data-stu-id="63cc2-158">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="63cc2-159">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span><span class="sxs-lookup"><span data-stu-id="63cc2-159">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="63cc2-160">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span><span class="sxs-lookup"><span data-stu-id="63cc2-160">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="63cc2-161">Tips for building a synonym map</span><span class="sxs-lookup"><span data-stu-id="63cc2-161">Tips for building a synonym map</span></span>

- <span data-ttu-id="63cc2-162">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span><span class="sxs-lookup"><span data-stu-id="63cc2-162">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="63cc2-163">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span><span class="sxs-lookup"><span data-stu-id="63cc2-163">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="63cc2-164">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="63cc2-164">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="63cc2-165">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span><span class="sxs-lookup"><span data-stu-id="63cc2-165">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="63cc2-166">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span><span class="sxs-lookup"><span data-stu-id="63cc2-166">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="63cc2-167">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span><span class="sxs-lookup"><span data-stu-id="63cc2-167">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="63cc2-168">Currently, a field can only use one of them.</span><span class="sxs-lookup"><span data-stu-id="63cc2-168">Currently, a field can only use one of them.</span></span> <span data-ttu-id="63cc2-169">You can update a field's synonymMaps property at any time.</span><span class="sxs-lookup"><span data-stu-id="63cc2-169">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63cc2-170">Next Steps</span><span class="sxs-lookup"><span data-stu-id="63cc2-170">Next Steps</span></span>

- <span data-ttu-id="63cc2-171">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span><span class="sxs-lookup"><span data-stu-id="63cc2-171">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="63cc2-172">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span><span class="sxs-lookup"><span data-stu-id="63cc2-172">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="63cc2-173">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span><span class="sxs-lookup"><span data-stu-id="63cc2-173">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
