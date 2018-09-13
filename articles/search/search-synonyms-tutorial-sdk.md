---
title: Synonyms C# tutorial in Azure Search | Microsoft Docs
description: In this tutorial, add the synonyms feature to an index in Azure Search.
manager: cgronlun
author: HeidiSteen
services: search
ms.service: search
ms.topic: tutorial
ms.date: 07/10/2018
ms.author: heidist
ms.openlocfilehash: 8340c4dc2a855911073905a3aea93e19fc7b520d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774481"
---
# <a name="tutorial-add-synonyms-for-azure-search-in-c"></a><span data-ttu-id="3fd13-103">Tutorial: Add synonyms for Azure Search in C#</span><span class="sxs-lookup"><span data-stu-id="3fd13-103">Tutorial: Add synonyms for Azure Search in C#</span></span>

<span data-ttu-id="3fd13-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span><span class="sxs-lookup"><span data-stu-id="3fd13-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="3fd13-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span><span class="sxs-lookup"><span data-stu-id="3fd13-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span> 

<span data-ttu-id="3fd13-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span><span class="sxs-lookup"><span data-stu-id="3fd13-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="3fd13-107">This tutorial covers essential steps for adding and using synonyms with an existing index.</span><span class="sxs-lookup"><span data-stu-id="3fd13-107">This tutorial covers essential steps for adding and using synonyms with an existing index.</span></span> <span data-ttu-id="3fd13-108">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="3fd13-108">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3fd13-109">Enable synonyms by creating and posting mapping rules</span><span class="sxs-lookup"><span data-stu-id="3fd13-109">Enable synonyms by creating and posting mapping rules</span></span> 
> * <span data-ttu-id="3fd13-110">Reference a synonym map in a query string</span><span class="sxs-lookup"><span data-stu-id="3fd13-110">Reference a synonym map in a query string</span></span>

<span data-ttu-id="3fd13-111">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span><span class="sxs-lookup"><span data-stu-id="3fd13-111">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="3fd13-112">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span><span class="sxs-lookup"><span data-stu-id="3fd13-112">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="3fd13-113">Synonyms are supported in the latest API and SDK versions (api-version=2017-11-11, SDK version 5.0.0).</span><span class="sxs-lookup"><span data-stu-id="3fd13-113">Synonyms are supported in the latest API and SDK versions (api-version=2017-11-11, SDK version 5.0.0).</span></span> <span data-ttu-id="3fd13-114">There is no Azure portal support at this time.</span><span class="sxs-lookup"><span data-stu-id="3fd13-114">There is no Azure portal support at this time.</span></span> <span data-ttu-id="3fd13-115">If Azure portal support for synonyms would be useful to you, please provide your feedback on the [UserVoice](https://feedback.azure.com/forums/263029-azure-search)</span><span class="sxs-lookup"><span data-stu-id="3fd13-115">If Azure portal support for synonyms would be useful to you, please provide your feedback on the [UserVoice](https://feedback.azure.com/forums/263029-azure-search)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fd13-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3fd13-116">Prerequisites</span></span>

<span data-ttu-id="3fd13-117">Tutorial requirements include the following:</span><span class="sxs-lookup"><span data-stu-id="3fd13-117">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="3fd13-118">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fd13-118">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="3fd13-119">Azure Search service</span><span class="sxs-lookup"><span data-stu-id="3fd13-119">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="3fd13-120">Microsoft.Azure.Search .NET library</span><span class="sxs-lookup"><span data-stu-id="3fd13-120">Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk)
* [<span data-ttu-id="3fd13-121">How to use Azure Search from a .NET Application</span><span class="sxs-lookup"><span data-stu-id="3fd13-121">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="3fd13-122">Overview</span><span class="sxs-lookup"><span data-stu-id="3fd13-122">Overview</span></span>

<span data-ttu-id="3fd13-123">Before-and-after queries demonstrate the value of synonyms.</span><span class="sxs-lookup"><span data-stu-id="3fd13-123">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="3fd13-124">In this tutorial, use a sample application that executes queries and returns results on a sample index.</span><span class="sxs-lookup"><span data-stu-id="3fd13-124">In this tutorial, use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="3fd13-125">The sample application creates a small index named "hotels" populated with two documents.</span><span class="sxs-lookup"><span data-stu-id="3fd13-125">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="3fd13-126">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span><span class="sxs-lookup"><span data-stu-id="3fd13-126">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="3fd13-127">The code below demonstrates the overall flow.</span><span class="sxs-lookup"><span data-stu-id="3fd13-127">The code below demonstrates the overall flow.</span></span>

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
<span data-ttu-id="3fd13-128">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="3fd13-128">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="3fd13-129">"Before" queries</span><span class="sxs-lookup"><span data-stu-id="3fd13-129">"Before" queries</span></span>

<span data-ttu-id="3fd13-130">In `RunQueriesWithNonExistentTermsInIndex`, issue search queries with "five star", "internet", and "economy AND hotel".</span><span class="sxs-lookup"><span data-stu-id="3fd13-130">In `RunQueriesWithNonExistentTermsInIndex`, issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
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
<span data-ttu-id="3fd13-131">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="3fd13-131">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="3fd13-132">Enable synonyms</span><span class="sxs-lookup"><span data-stu-id="3fd13-132">Enable synonyms</span></span>

<span data-ttu-id="3fd13-133">Enabling synonyms is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="3fd13-133">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="3fd13-134">We first define and upload synonym rules and then configure fields to use them.</span><span class="sxs-lookup"><span data-stu-id="3fd13-134">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="3fd13-135">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="3fd13-135">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="3fd13-136">Add a synonym map to your search service.</span><span class="sxs-lookup"><span data-stu-id="3fd13-136">Add a synonym map to your search service.</span></span> <span data-ttu-id="3fd13-137">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span><span class="sxs-lookup"><span data-stu-id="3fd13-137">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
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
<span data-ttu-id="3fd13-138">A synonym map must conform to the open source standard `solr` format.</span><span class="sxs-lookup"><span data-stu-id="3fd13-138">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="3fd13-139">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="3fd13-139">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="3fd13-140">Configure searchable fields to use the synonym map in the index definition.</span><span class="sxs-lookup"><span data-stu-id="3fd13-140">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="3fd13-141">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span><span class="sxs-lookup"><span data-stu-id="3fd13-141">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="3fd13-142">When you add a synonym map, index rebuilds are not required.</span><span class="sxs-lookup"><span data-stu-id="3fd13-142">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="3fd13-143">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span><span class="sxs-lookup"><span data-stu-id="3fd13-143">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="3fd13-144">The addition of new attributes has no impact on index availability.</span><span class="sxs-lookup"><span data-stu-id="3fd13-144">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="3fd13-145">The same applies in disabling synonyms for a field.</span><span class="sxs-lookup"><span data-stu-id="3fd13-145">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="3fd13-146">You can simply set the `synonymMaps` property to an empty list.</span><span class="sxs-lookup"><span data-stu-id="3fd13-146">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="3fd13-147">"After" queries</span><span class="sxs-lookup"><span data-stu-id="3fd13-147">"After" queries</span></span>

<span data-ttu-id="3fd13-148">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span><span class="sxs-lookup"><span data-stu-id="3fd13-148">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="3fd13-149">The first query finds the document from the rule `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="3fd13-149">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="3fd13-150">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span><span class="sxs-lookup"><span data-stu-id="3fd13-150">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="3fd13-151">Adding synonyms completely changes the search experience.</span><span class="sxs-lookup"><span data-stu-id="3fd13-151">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="3fd13-152">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span><span class="sxs-lookup"><span data-stu-id="3fd13-152">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="3fd13-153">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span><span class="sxs-lookup"><span data-stu-id="3fd13-153">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="3fd13-154">Sample application source code</span><span class="sxs-lookup"><span data-stu-id="3fd13-154">Sample application source code</span></span>
<span data-ttu-id="3fd13-155">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="3fd13-155">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="3fd13-156">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3fd13-156">Clean up resources</span></span>

<span data-ttu-id="3fd13-157">The fastest way to clean up after a tutorial is by deleting the resource group containing the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="3fd13-157">The fastest way to clean up after a tutorial is by deleting the resource group containing the Azure Search service.</span></span> <span data-ttu-id="3fd13-158">You can delete the resource group now to permanently delete everything in it.</span><span class="sxs-lookup"><span data-stu-id="3fd13-158">You can delete the resource group now to permanently delete everything in it.</span></span> <span data-ttu-id="3fd13-159">In the portal, the resource group name is on the Overview page of Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="3fd13-159">In the portal, the resource group name is on the Overview page of Azure Search service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fd13-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fd13-160">Next steps</span></span>

<span data-ttu-id="3fd13-161">This tutorial demonstrated the [Synonyms REST API](https://aka.ms/rgm6rq) in C# code to create and post mapping rules and then call the synonym map on a query.</span><span class="sxs-lookup"><span data-stu-id="3fd13-161">This tutorial demonstrated the [Synonyms REST API](https://aka.ms/rgm6rq) in C# code to create and post mapping rules and then call the synonym map on a query.</span></span> <span data-ttu-id="3fd13-162">Additional information can be found in the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/) reference documentation.</span><span class="sxs-lookup"><span data-stu-id="3fd13-162">Additional information can be found in the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/) reference documentation.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fd13-163">How to use synonyms in Azure Search</span><span class="sxs-lookup"><span data-stu-id="3fd13-163">How to use synonyms in Azure Search</span></span>](search-synonyms.md)
