---
title: Synonyms preview tutorial in Azure Search | Microsoft Docs
description: Add the synonyms preview feature to an index in Azure Search.
services: search
manager: jhubbard
documentationcenter: ''
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662979"
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="70429-103">Synonym (preview) C# tutorial for Azure Search</span><span class="sxs-lookup"><span data-stu-id="70429-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="70429-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span><span class="sxs-lookup"><span data-stu-id="70429-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="70429-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span><span class="sxs-lookup"><span data-stu-id="70429-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="70429-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span><span class="sxs-lookup"><span data-stu-id="70429-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="70429-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span><span class="sxs-lookup"><span data-stu-id="70429-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="70429-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span><span class="sxs-lookup"><span data-stu-id="70429-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="70429-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="70429-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="70429-110">There is no Azure portal support at this time.</span><span class="sxs-lookup"><span data-stu-id="70429-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="70429-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span><span class="sxs-lookup"><span data-stu-id="70429-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70429-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="70429-112">Prerequisites</span></span>

<span data-ttu-id="70429-113">Tutorial requirements include the following:</span><span class="sxs-lookup"><span data-stu-id="70429-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="70429-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70429-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="70429-115">Azure Search service</span><span class="sxs-lookup"><span data-stu-id="70429-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="70429-116">Preview version of Microsoft.Azure.Search .NET library</span><span class="sxs-lookup"><span data-stu-id="70429-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="70429-117">How to use Azure Search from a .NET Application</span><span class="sxs-lookup"><span data-stu-id="70429-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="70429-118">Overview</span><span class="sxs-lookup"><span data-stu-id="70429-118">Overview</span></span>

<span data-ttu-id="70429-119">Before-and-after queries demonstrate the value of synonyms.</span><span class="sxs-lookup"><span data-stu-id="70429-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="70429-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span><span class="sxs-lookup"><span data-stu-id="70429-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="70429-121">The sample application creates a small index named "hotels" populated with two documents.</span><span class="sxs-lookup"><span data-stu-id="70429-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="70429-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span><span class="sxs-lookup"><span data-stu-id="70429-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="70429-123">The code below demonstrates the overall flow.</span><span class="sxs-lookup"><span data-stu-id="70429-123">The code below demonstrates the overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="70429-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="70429-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="70429-125">"Before" queries</span><span class="sxs-lookup"><span data-stu-id="70429-125">"Before" queries</span></span>

<span data-ttu-id="70429-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span><span class="sxs-lookup"><span data-stu-id="70429-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="70429-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="70429-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="70429-128">Enable synonyms</span><span class="sxs-lookup"><span data-stu-id="70429-128">Enable synonyms</span></span>

<span data-ttu-id="70429-129">Enabling synonyms is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="70429-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="70429-130">We first define and upload synonym rules and then configure fields to use them.</span><span class="sxs-lookup"><span data-stu-id="70429-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="70429-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="70429-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="70429-132">Add a synonym map to your search service.</span><span class="sxs-lookup"><span data-stu-id="70429-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="70429-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span><span class="sxs-lookup"><span data-stu-id="70429-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="70429-134">A synonym map must conform to the open source standard `solr` format.</span><span class="sxs-lookup"><span data-stu-id="70429-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="70429-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="70429-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="70429-136">Configure searchable fields to use the synonym map in the index definition.</span><span class="sxs-lookup"><span data-stu-id="70429-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="70429-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span><span class="sxs-lookup"><span data-stu-id="70429-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="70429-138">When you add a synonym map, index rebuilds are not required.</span><span class="sxs-lookup"><span data-stu-id="70429-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="70429-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span><span class="sxs-lookup"><span data-stu-id="70429-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="70429-140">The addition of new attributes has no impact on index availability.</span><span class="sxs-lookup"><span data-stu-id="70429-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="70429-141">The same applies in disabling synonyms for a field.</span><span class="sxs-lookup"><span data-stu-id="70429-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="70429-142">You can simply set the `synonymMaps` property to an empty list.</span><span class="sxs-lookup"><span data-stu-id="70429-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="70429-143">"After" queries</span><span class="sxs-lookup"><span data-stu-id="70429-143">"After" queries</span></span>

<span data-ttu-id="70429-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span><span class="sxs-lookup"><span data-stu-id="70429-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="70429-145">The first query finds the document from the rule `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="70429-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="70429-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span><span class="sxs-lookup"><span data-stu-id="70429-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="70429-147">Adding synonyms completely changes the search experience.</span><span class="sxs-lookup"><span data-stu-id="70429-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="70429-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span><span class="sxs-lookup"><span data-stu-id="70429-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="70429-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span><span class="sxs-lookup"><span data-stu-id="70429-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="70429-150">Sample application source code</span><span class="sxs-lookup"><span data-stu-id="70429-150">Sample application source code</span></span>
<span data-ttu-id="70429-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="70429-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70429-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="70429-152">Next steps</span></span>

* <span data-ttu-id="70429-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="70429-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="70429-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="70429-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="70429-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="70429-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
