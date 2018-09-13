---
title: Create an Azure Search index using the .NET SDK | Microsoft Docs
description: Create an index in code using the Azure Search .NET SDK.
services: search
documentationcenter: ''
author: brjohnstmsft
manager: jhubbard
editor: ''
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 3a5131323f438109d94137cb4f577054ec13227f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662222"
---
# <a name="create-an-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="17f60-103">Create an Azure Search index using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="17f60-103">Create an Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Overview](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

<span data-ttu-id="17f60-108">This article will walk you through the process of creating an Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="17f60-108">This article will walk you through the process of creating an Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="17f60-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17f60-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span></span>

<span data-ttu-id="17f60-110">Note that all sample code in this article is written in C#.</span><span class="sxs-lookup"><span data-stu-id="17f60-110">Note that all sample code in this article is written in C#.</span></span> <span data-ttu-id="17f60-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="17f60-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="17f60-112">Identify your Azure Search service's admin api-key</span><span class="sxs-lookup"><span data-stu-id="17f60-112">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="17f60-113">Now that you have provisioned an Azure Search service, you are almost ready to issue requests against your service endpoint using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="17f60-113">Now that you have provisioned an Azure Search service, you are almost ready to issue requests against your service endpoint using the .NET SDK.</span></span> <span data-ttu-id="17f60-114">First, you will need to obtain one of the admin api-keys that was generated for the search service you provisioned.</span><span class="sxs-lookup"><span data-stu-id="17f60-114">First, you will need to obtain one of the admin api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="17f60-115">The .NET SDK will send this api-key on every request to your service.</span><span class="sxs-lookup"><span data-stu-id="17f60-115">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="17f60-116">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span><span class="sxs-lookup"><span data-stu-id="17f60-116">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="17f60-117">To find your service's api-keys, sign in to the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="17f60-117">To find your service's api-keys, sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="17f60-118">Go to your Azure Search service's blade</span><span class="sxs-lookup"><span data-stu-id="17f60-118">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="17f60-119">Click on the "Keys" icon</span><span class="sxs-lookup"><span data-stu-id="17f60-119">Click on the "Keys" icon</span></span>

<span data-ttu-id="17f60-120">Your service will have *admin keys* and *query keys*.</span><span class="sxs-lookup"><span data-stu-id="17f60-120">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="17f60-121">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span><span class="sxs-lookup"><span data-stu-id="17f60-121">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="17f60-122">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="17f60-122">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="17f60-123">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span><span class="sxs-lookup"><span data-stu-id="17f60-123">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="17f60-124">For the purposes of creating an index, you can use either your primary or secondary admin key.</span><span class="sxs-lookup"><span data-stu-id="17f60-124">For the purposes of creating an index, you can use either your primary or secondary admin key.</span></span>

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-the-searchserviceclient-class"></a><span data-ttu-id="17f60-125">Create an instance of the SearchServiceClient class</span><span class="sxs-lookup"><span data-stu-id="17f60-125">Create an instance of the SearchServiceClient class</span></span>
<span data-ttu-id="17f60-126">To start using the Azure Search .NET SDK, you will need to create an instance of the `SearchServiceClient` class.</span><span class="sxs-lookup"><span data-stu-id="17f60-126">To start using the Azure Search .NET SDK, you will need to create an instance of the `SearchServiceClient` class.</span></span> <span data-ttu-id="17f60-127">This class has several constructors.</span><span class="sxs-lookup"><span data-stu-id="17f60-127">This class has several constructors.</span></span> <span data-ttu-id="17f60-128">The one you want takes your search service name and a `SearchCredentials` object as parameters.</span><span class="sxs-lookup"><span data-stu-id="17f60-128">The one you want takes your search service name and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="17f60-129">`SearchCredentials` wraps your api-key.</span><span class="sxs-lookup"><span data-stu-id="17f60-129">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="17f60-130">The code below creates a new `SearchServiceClient` using values for the search service name and api-key that are stored in the application's config file (`app.config` or `web.config`):</span><span class="sxs-lookup"><span data-stu-id="17f60-130">The code below creates a new `SearchServiceClient` using values for the search service name and api-key that are stored in the application's config file (`app.config` or `web.config`):</span></span>

```csharp
string searchServiceName = ConfigurationManager.AppSettings["SearchServiceName"];
string adminApiKey = ConfigurationManager.AppSettings["SearchServiceAdminApiKey"];

SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
```

<span data-ttu-id="17f60-131">`SearchServiceClient` has an `Indexes` property.</span><span class="sxs-lookup"><span data-stu-id="17f60-131">`SearchServiceClient` has an `Indexes` property.</span></span> <span data-ttu-id="17f60-132">This property provides all the methods you need to create, list, update, or delete Azure Search indexes.</span><span class="sxs-lookup"><span data-stu-id="17f60-132">This property provides all the methods you need to create, list, update, or delete Azure Search indexes.</span></span>

> [!NOTE]
> The `SearchServiceClient` class manages connections to your search service. In order to avoid opening too many connections, you should try to share a single instance of `SearchServiceClient` in your application if possible. Its methods are thread-safe to enable such sharing.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a><span data-ttu-id="17f60-136">Define your Azure Search index</span><span class="sxs-lookup"><span data-stu-id="17f60-136">Define your Azure Search index</span></span>
<span data-ttu-id="17f60-137">A single call to the `Indexes.Create` method will create your index.</span><span class="sxs-lookup"><span data-stu-id="17f60-137">A single call to the `Indexes.Create` method will create your index.</span></span> <span data-ttu-id="17f60-138">This method takes as a parameter an `Index` object that defines your Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="17f60-138">This method takes as a parameter an `Index` object that defines your Azure Search index.</span></span> <span data-ttu-id="17f60-139">You need to create an `Index` object and initialize it as follows:</span><span class="sxs-lookup"><span data-stu-id="17f60-139">You need to create an `Index` object and initialize it as follows:</span></span>

1. <span data-ttu-id="17f60-140">Set the `Name` property of the `Index` object to the name of your index.</span><span class="sxs-lookup"><span data-stu-id="17f60-140">Set the `Name` property of the `Index` object to the name of your index.</span></span>
2. <span data-ttu-id="17f60-141">Set the `Fields` property of the `Index` object to an array of `Field` objects.</span><span class="sxs-lookup"><span data-stu-id="17f60-141">Set the `Fields` property of the `Index` object to an array of `Field` objects.</span></span> <span data-ttu-id="17f60-142">The easiest way to create the `Field` objects is by calling the `FieldBuilder.BuildForType` method, passing a model class for the type parameter.</span><span class="sxs-lookup"><span data-stu-id="17f60-142">The easiest way to create the `Field` objects is by calling the `FieldBuilder.BuildForType` method, passing a model class for the type parameter.</span></span> <span data-ttu-id="17f60-143">A model class has properties that map to the fields of your index.</span><span class="sxs-lookup"><span data-stu-id="17f60-143">A model class has properties that map to the fields of your index.</span></span> <span data-ttu-id="17f60-144">This allows you to bind documents from your search index to instances of your model class.</span><span class="sxs-lookup"><span data-stu-id="17f60-144">This allows you to bind documents from your search index to instances of your model class.</span></span>

> [!NOTE]
> If you don't plan to use a model class, you can still define your index by creating `Field` objects directly. You can provide the name of the field to the constructor, along with the data type (or analyzer for string fields). You can also set other properties like `IsSearchable`, `IsFilterable`, etc.
>
>

<span data-ttu-id="17f60-148">It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [appropriate properties](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span><span class="sxs-lookup"><span data-stu-id="17f60-148">It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [appropriate properties](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span></span> <span data-ttu-id="17f60-149">These properties control which search features (filtering, faceting, sorting full-text search, etc.) apply to which fields.</span><span class="sxs-lookup"><span data-stu-id="17f60-149">These properties control which search features (filtering, faceting, sorting full-text search, etc.) apply to which fields.</span></span> <span data-ttu-id="17f60-150">For any property you do not explicitly set, the `Field` class defaults to disabling the corresponding search feature unless you specifically enable it.</span><span class="sxs-lookup"><span data-stu-id="17f60-150">For any property you do not explicitly set, the `Field` class defaults to disabling the corresponding search feature unless you specifically enable it.</span></span>

<span data-ttu-id="17f60-151">For our example, we've named our index "hotels" and defined our fields using a model class.</span><span class="sxs-lookup"><span data-stu-id="17f60-151">For our example, we've named our index "hotels" and defined our fields using a model class.</span></span> <span data-ttu-id="17f60-152">Each property of the model class has attributes which determine the search-related behaviors of the corresponding index field.</span><span class="sxs-lookup"><span data-stu-id="17f60-152">Each property of the model class has attributes which determine the search-related behaviors of the corresponding index field.</span></span> <span data-ttu-id="17f60-153">The model class is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="17f60-153">The model class is defined as follows:</span></span>

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

<span data-ttu-id="17f60-154">We have carefully chosen the attributes for each property based on how we think they will be used in an application.</span><span class="sxs-lookup"><span data-stu-id="17f60-154">We have carefully chosen the attributes for each property based on how we think they will be used in an application.</span></span> <span data-ttu-id="17f60-155">For example, it is likely that people searching for hotels will be interested in keyword matches on the `description` field, so we enable full-text search for that field by adding the `IsSearchable` attribute to the `Description` property.</span><span class="sxs-lookup"><span data-stu-id="17f60-155">For example, it is likely that people searching for hotels will be interested in keyword matches on the `description` field, so we enable full-text search for that field by adding the `IsSearchable` attribute to the `Description` property.</span></span>

<span data-ttu-id="17f60-156">Please note that exactly one field in your index of type `string` must be the designated as the *key* field by adding the `Key` attribute (see `HotelId` in the above example).</span><span class="sxs-lookup"><span data-stu-id="17f60-156">Please note that exactly one field in your index of type `string` must be the designated as the *key* field by adding the `Key` attribute (see `HotelId` in the above example).</span></span>

<span data-ttu-id="17f60-157">The index definition above uses a language analyzer for the `description_fr` field because it is intended to store French text.</span><span class="sxs-lookup"><span data-stu-id="17f60-157">The index definition above uses a language analyzer for the `description_fr` field because it is intended to store French text.</span></span> <span data-ttu-id="17f60-158">See [the Language support topic](https://docs.microsoft.com/rest/api/searchservice/Language-support) as well as the corresponding [blog post](https://azure.microsoft.com/blog/language-support-in-azure-search/) for more information about language analyzers.</span><span class="sxs-lookup"><span data-stu-id="17f60-158">See [the Language support topic](https://docs.microsoft.com/rest/api/searchservice/Language-support) as well as the corresponding [blog post](https://azure.microsoft.com/blog/language-support-in-azure-search/) for more information about language analyzers.</span></span>

> [!NOTE]
> By default, the name of each property in your model class is used as the name of the corresponding field in the index. If you want to map all property names to camel-case field names, mark the class with the `SerializePropertyNamesAsCamelCase` attribute. If you want to map to a different name, you can use the `JsonProperty` attribute like the `DescriptionFr` property above. The `JsonProperty` attribute takes precedence over the `SerializePropertyNamesAsCamelCase` attribute.
> 
> 

<span data-ttu-id="17f60-163">Now that we've defined a model class, we can create an index definition very easily:</span><span class="sxs-lookup"><span data-stu-id="17f60-163">Now that we've defined a model class, we can create an index definition very easily:</span></span>

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-the-index"></a><span data-ttu-id="17f60-164">Create the index</span><span class="sxs-lookup"><span data-stu-id="17f60-164">Create the index</span></span>
<span data-ttu-id="17f60-165">Now that you have an initialized `Index` object, you can create the index simply by calling `Indexes.Create` on your `SearchServiceClient` object:</span><span class="sxs-lookup"><span data-stu-id="17f60-165">Now that you have an initialized `Index` object, you can create the index simply by calling `Indexes.Create` on your `SearchServiceClient` object:</span></span>

```csharp
serviceClient.Indexes.Create(definition);
```

<span data-ttu-id="17f60-166">For a successful request, the method will return normally.</span><span class="sxs-lookup"><span data-stu-id="17f60-166">For a successful request, the method will return normally.</span></span> <span data-ttu-id="17f60-167">If there is a problem with the request such as an invalid parameter, the method will throw `CloudException`.</span><span class="sxs-lookup"><span data-stu-id="17f60-167">If there is a problem with the request such as an invalid parameter, the method will throw `CloudException`.</span></span>

<span data-ttu-id="17f60-168">When you're done with an index and want to delete it, just call the `Indexes.Delete` method on your `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="17f60-168">When you're done with an index and want to delete it, just call the `Indexes.Delete` method on your `SearchServiceClient`.</span></span> <span data-ttu-id="17f60-169">For example, this is how we would delete the "hotels" index:</span><span class="sxs-lookup"><span data-stu-id="17f60-169">For example, this is how we would delete the "hotels" index:</span></span>

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity. We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive. For example, in the examples above you could use `CreateAsync` and `DeleteAsync` instead of `Create` and `Delete`.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="17f60-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="17f60-173">Next steps</span></span>
<span data-ttu-id="17f60-174">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span><span class="sxs-lookup"><span data-stu-id="17f60-174">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span></span>

