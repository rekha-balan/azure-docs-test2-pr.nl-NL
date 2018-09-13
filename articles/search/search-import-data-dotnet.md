---
title: Data upload in Azure Search using the .NET SDK | Microsoft Docs
description: Learn how to upload data to an index in Azure Search using the .NET SDK.
services: search
documentationcenter: ''
author: brjohnstmsft
manager: jhubbard
editor: ''
tags: ''
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 3c8f30583ebcb5b4e4182bd2770079882c088c50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662228"
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="94080-103">Upload data to Azure Search using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="94080-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Overview](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="94080-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="94080-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="94080-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="94080-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="94080-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="94080-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

<span data-ttu-id="94080-110">Note that all sample code in this article is written in C#.</span><span class="sxs-lookup"><span data-stu-id="94080-110">Note that all sample code in this article is written in C#.</span></span> <span data-ttu-id="94080-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="94080-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span>

<span data-ttu-id="94080-112">In order to push documents into your index using the .NET SDK, you will need to:</span><span class="sxs-lookup"><span data-stu-id="94080-112">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="94080-113">Create a `SearchIndexClient` object to connect to your search index.</span><span class="sxs-lookup"><span data-stu-id="94080-113">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="94080-114">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span><span class="sxs-lookup"><span data-stu-id="94080-114">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="94080-115">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span><span class="sxs-lookup"><span data-stu-id="94080-115">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="94080-116">Create an instance of the SearchIndexClient class</span><span class="sxs-lookup"><span data-stu-id="94080-116">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="94080-117">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span><span class="sxs-lookup"><span data-stu-id="94080-117">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="94080-118">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span><span class="sxs-lookup"><span data-stu-id="94080-118">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="94080-119">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="94080-119">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> In a typical search application, index management and population is handled by a separate component from search queries. `Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`. It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`. However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key. This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure. You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

<span data-ttu-id="94080-126">`SearchIndexClient` has a `Documents` property.</span><span class="sxs-lookup"><span data-stu-id="94080-126">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="94080-127">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span><span class="sxs-lookup"><span data-stu-id="94080-127">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="94080-128">Decide which indexing action to use</span><span class="sxs-lookup"><span data-stu-id="94080-128">Decide which indexing action to use</span></span>
<span data-ttu-id="94080-129">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span><span class="sxs-lookup"><span data-stu-id="94080-129">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="94080-130">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span><span class="sxs-lookup"><span data-stu-id="94080-130">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="94080-131">Depending on which of the below actions you choose, only certain fields must be included for each document:</span><span class="sxs-lookup"><span data-stu-id="94080-131">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="94080-132">Action</span><span class="sxs-lookup"><span data-stu-id="94080-132">Action</span></span> | <span data-ttu-id="94080-133">Description</span><span class="sxs-lookup"><span data-stu-id="94080-133">Description</span></span> | <span data-ttu-id="94080-134">Necessary fields for each document</span><span class="sxs-lookup"><span data-stu-id="94080-134">Necessary fields for each document</span></span> | <span data-ttu-id="94080-135">Notes</span><span class="sxs-lookup"><span data-stu-id="94080-135">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="94080-136">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span><span class="sxs-lookup"><span data-stu-id="94080-136">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="94080-137">key, plus any other fields you wish to define</span><span class="sxs-lookup"><span data-stu-id="94080-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="94080-138">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span><span class="sxs-lookup"><span data-stu-id="94080-138">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="94080-139">This occurs even when the field was previously set to a non-null value.</span><span class="sxs-lookup"><span data-stu-id="94080-139">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="94080-140">Updates an existing document with the specified fields.</span><span class="sxs-lookup"><span data-stu-id="94080-140">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="94080-141">If the document does not exist in the index, the merge will fail.</span><span class="sxs-lookup"><span data-stu-id="94080-141">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="94080-142">key, plus any other fields you wish to define</span><span class="sxs-lookup"><span data-stu-id="94080-142">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="94080-143">Any field you specify in a merge will replace the existing field in the document.</span><span class="sxs-lookup"><span data-stu-id="94080-143">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="94080-144">This includes fields of type `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="94080-144">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="94080-145">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="94080-145">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="94080-146">It will not be `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="94080-146">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="94080-147">This action behaves like `Merge` if a document with the given key already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="94080-147">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="94080-148">If the document does not exist, it behaves like `Upload` with a new document.</span><span class="sxs-lookup"><span data-stu-id="94080-148">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="94080-149">key, plus any other fields you wish to define</span><span class="sxs-lookup"><span data-stu-id="94080-149">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="94080-150">Removes the specified document from the index.</span><span class="sxs-lookup"><span data-stu-id="94080-150">Removes the specified document from the index.</span></span> |<span data-ttu-id="94080-151">key only</span><span class="sxs-lookup"><span data-stu-id="94080-151">key only</span></span> |<span data-ttu-id="94080-152">Any fields you specify other than the key field will be ignored.</span><span class="sxs-lookup"><span data-stu-id="94080-152">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="94080-153">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span><span class="sxs-lookup"><span data-stu-id="94080-153">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="94080-154">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span><span class="sxs-lookup"><span data-stu-id="94080-154">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="94080-155">Construct your IndexBatch</span><span class="sxs-lookup"><span data-stu-id="94080-155">Construct your IndexBatch</span></span>
<span data-ttu-id="94080-156">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="94080-156">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="94080-157">The example below shows how to create a batch with a few different actions.</span><span class="sxs-lookup"><span data-stu-id="94080-157">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="94080-158">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span><span class="sxs-lookup"><span data-stu-id="94080-158">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="94080-159">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span><span class="sxs-lookup"><span data-stu-id="94080-159">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="94080-160">Assume that this example "hotels" index is already populated with a number of documents.</span><span class="sxs-lookup"><span data-stu-id="94080-160">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="94080-161">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span><span class="sxs-lookup"><span data-stu-id="94080-161">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="94080-162">Also, note that you can only include up to 1000 documents in a single indexing request.</span><span class="sxs-lookup"><span data-stu-id="94080-162">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> In this example, we are applying different actions to different documents. If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`. For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`. These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="94080-167">Import data to the index</span><span class="sxs-lookup"><span data-stu-id="94080-167">Import data to the index</span></span>
<span data-ttu-id="94080-168">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span><span class="sxs-lookup"><span data-stu-id="94080-168">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="94080-169">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span><span class="sxs-lookup"><span data-stu-id="94080-169">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="94080-170">Note the `try`/`catch` surrounding the call to the `Index` method.</span><span class="sxs-lookup"><span data-stu-id="94080-170">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="94080-171">The catch block handles an important error case for indexing.</span><span class="sxs-lookup"><span data-stu-id="94080-171">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="94080-172">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="94080-172">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="94080-173">This can happen if you are indexing documents while your service is under heavy load.</span><span class="sxs-lookup"><span data-stu-id="94080-173">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="94080-174">**We strongly recommend explicitly handling this case in your code.**</span><span class="sxs-lookup"><span data-stu-id="94080-174">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="94080-175">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span><span class="sxs-lookup"><span data-stu-id="94080-175">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="94080-176">Finally, the code in the example above delays for two seconds.</span><span class="sxs-lookup"><span data-stu-id="94080-176">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="94080-177">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span><span class="sxs-lookup"><span data-stu-id="94080-177">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="94080-178">Delays like this are typically only necessary in demos, tests, and sample applications.</span><span class="sxs-lookup"><span data-stu-id="94080-178">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="94080-179">How the .NET SDK handles documents</span><span class="sxs-lookup"><span data-stu-id="94080-179">How the .NET SDK handles documents</span></span>
<span data-ttu-id="94080-180">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span><span class="sxs-lookup"><span data-stu-id="94080-180">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="94080-181">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="94080-181">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="94080-182">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span><span class="sxs-lookup"><span data-stu-id="94080-182">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="94080-183">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span><span class="sxs-lookup"><span data-stu-id="94080-183">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="94080-184">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span><span class="sxs-lookup"><span data-stu-id="94080-184">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON. You can customize this serialization if needed. You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.
> 
> 

<span data-ttu-id="94080-189">The second important thing about the `Hotel` class are the data types of the public properties.</span><span class="sxs-lookup"><span data-stu-id="94080-189">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="94080-190">The .NET types of these properties map to their equivalent field types in the index definition.</span><span class="sxs-lookup"><span data-stu-id="94080-190">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="94080-191">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="94080-191">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="94080-192">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span><span class="sxs-lookup"><span data-stu-id="94080-192">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="94080-193">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="94080-193">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="94080-194">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="94080-194">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values. This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes. All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter. Only the latter are used in the sample code in this article.
> 
> 

<span data-ttu-id="94080-199">**Why you should use nullable data types**</span><span class="sxs-lookup"><span data-stu-id="94080-199">**Why you should use nullable data types**</span></span>

<span data-ttu-id="94080-200">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span><span class="sxs-lookup"><span data-stu-id="94080-200">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="94080-201">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span><span class="sxs-lookup"><span data-stu-id="94080-201">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="94080-202">Neither the SDK nor the Azure Search service will help you to enforce this.</span><span class="sxs-lookup"><span data-stu-id="94080-202">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="94080-203">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="94080-203">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="94080-204">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span><span class="sxs-lookup"><span data-stu-id="94080-204">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="94080-205">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span><span class="sxs-lookup"><span data-stu-id="94080-205">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="94080-206">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span><span class="sxs-lookup"><span data-stu-id="94080-206">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94080-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="94080-207">Next steps</span></span>
<span data-ttu-id="94080-208">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span><span class="sxs-lookup"><span data-stu-id="94080-208">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="94080-209">See [Query Your Azure Search Index](search-query-overview.md) for details.</span><span class="sxs-lookup"><span data-stu-id="94080-209">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

