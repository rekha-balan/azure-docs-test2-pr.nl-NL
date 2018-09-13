---
title: Create an index (.NET API - Azure Search) | Microsoft Docs
description: Create an index in code using the Azure Search .NET SDK.
author: brjohnstmsft
manager: jlembicz
tags: azure-portal
services: search
ms.service: search
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7e7d1f8110d8470fe7596633563529f397c5551e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44785205"
---
# <a name="create-an-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="14f0c-103">Create an Azure Search index using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="14f0c-103">Create an Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Overview](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

<span data-ttu-id="14f0c-108">This article will walk you through the process of creating an Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="14f0c-108">This article will walk you through the process of creating an Azure Search [index](https://docs.microsoft.com/rest/api/searchservice/Create-Index) using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="14f0c-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14f0c-109">Before following this guide and creating an index, you should have already [created an Azure Search service](search-create-service-portal.md).</span></span>

> [!NOTE]
> All sample code in this article is written in C#. You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto). You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.


## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="14f0c-113">Identify your Azure Search service's admin api-key</span><span class="sxs-lookup"><span data-stu-id="14f0c-113">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="14f0c-114">Now that you have provisioned an Azure Search service, you are almost ready to issue requests against your service endpoint using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="14f0c-114">Now that you have provisioned an Azure Search service, you are almost ready to issue requests against your service endpoint using the .NET SDK.</span></span> <span data-ttu-id="14f0c-115">First, you will need to obtain one of the admin api-keys that was generated for the search service you provisioned.</span><span class="sxs-lookup"><span data-stu-id="14f0c-115">First, you will need to obtain one of the admin api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="14f0c-116">The .NET SDK will send this api-key on every request to your service.</span><span class="sxs-lookup"><span data-stu-id="14f0c-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="14f0c-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span><span class="sxs-lookup"><span data-stu-id="14f0c-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="14f0c-118">To find your service's api-keys, sign in to the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="14f0c-118">To find your service's api-keys, sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="14f0c-119">Go to your Azure Search service's blade</span><span class="sxs-lookup"><span data-stu-id="14f0c-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="14f0c-120">Click on the "Keys" icon</span><span class="sxs-lookup"><span data-stu-id="14f0c-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="14f0c-121">Your service will have *admin keys* and *query keys*.</span><span class="sxs-lookup"><span data-stu-id="14f0c-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="14f0c-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span><span class="sxs-lookup"><span data-stu-id="14f0c-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="14f0c-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="14f0c-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="14f0c-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span><span class="sxs-lookup"><span data-stu-id="14f0c-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="14f0c-125">For the purposes of creating an index, you can use either your primary or secondary admin key.</span><span class="sxs-lookup"><span data-stu-id="14f0c-125">For the purposes of creating an index, you can use either your primary or secondary admin key.</span></span>

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-the-searchserviceclient-class"></a><span data-ttu-id="14f0c-126">Create an instance of the SearchServiceClient class</span><span class="sxs-lookup"><span data-stu-id="14f0c-126">Create an instance of the SearchServiceClient class</span></span>
<span data-ttu-id="14f0c-127">To start using the Azure Search .NET SDK, you will need to create an instance of the `SearchServiceClient` class.</span><span class="sxs-lookup"><span data-stu-id="14f0c-127">To start using the Azure Search .NET SDK, you will need to create an instance of the `SearchServiceClient` class.</span></span> <span data-ttu-id="14f0c-128">This class has several constructors.</span><span class="sxs-lookup"><span data-stu-id="14f0c-128">This class has several constructors.</span></span> <span data-ttu-id="14f0c-129">The one you want takes your search service name and a `SearchCredentials` object as parameters.</span><span class="sxs-lookup"><span data-stu-id="14f0c-129">The one you want takes your search service name and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="14f0c-130">`SearchCredentials` wraps your api-key.</span><span class="sxs-lookup"><span data-stu-id="14f0c-130">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="14f0c-131">The code below creates a new `SearchServiceClient` using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="14f0c-131">The code below creates a new `SearchServiceClient` using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

<span data-ttu-id="14f0c-132">`SearchServiceClient` has an `Indexes` property.</span><span class="sxs-lookup"><span data-stu-id="14f0c-132">`SearchServiceClient` has an `Indexes` property.</span></span> <span data-ttu-id="14f0c-133">This property provides all the methods you need to create, list, update, or delete Azure Search indexes.</span><span class="sxs-lookup"><span data-stu-id="14f0c-133">This property provides all the methods you need to create, list, update, or delete Azure Search indexes.</span></span>

> [!NOTE]
> The `SearchServiceClient` class manages connections to your search service. In order to avoid opening too many connections, you should try to share a single instance of `SearchServiceClient` in your application if possible. Its methods are thread-safe to enable such sharing.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a><span data-ttu-id="14f0c-137">Define your Azure Search index</span><span class="sxs-lookup"><span data-stu-id="14f0c-137">Define your Azure Search index</span></span>
<span data-ttu-id="14f0c-138">A single call to the `Indexes.Create` method will create your index.</span><span class="sxs-lookup"><span data-stu-id="14f0c-138">A single call to the `Indexes.Create` method will create your index.</span></span> <span data-ttu-id="14f0c-139">This method takes as a parameter an `Index` object that defines your Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="14f0c-139">This method takes as a parameter an `Index` object that defines your Azure Search index.</span></span> <span data-ttu-id="14f0c-140">You need to create an `Index` object and initialize it as follows:</span><span class="sxs-lookup"><span data-stu-id="14f0c-140">You need to create an `Index` object and initialize it as follows:</span></span>

1. <span data-ttu-id="14f0c-141">Set the `Name` property of the `Index` object to the name of your index.</span><span class="sxs-lookup"><span data-stu-id="14f0c-141">Set the `Name` property of the `Index` object to the name of your index.</span></span>
2. <span data-ttu-id="14f0c-142">Set the `Fields` property of the `Index` object to an array of `Field` objects.</span><span class="sxs-lookup"><span data-stu-id="14f0c-142">Set the `Fields` property of the `Index` object to an array of `Field` objects.</span></span> <span data-ttu-id="14f0c-143">The easiest way to create the `Field` objects is by calling the `FieldBuilder.BuildForType` method, passing a model class for the type parameter.</span><span class="sxs-lookup"><span data-stu-id="14f0c-143">The easiest way to create the `Field` objects is by calling the `FieldBuilder.BuildForType` method, passing a model class for the type parameter.</span></span> <span data-ttu-id="14f0c-144">A model class has properties that map to the fields of your index.</span><span class="sxs-lookup"><span data-stu-id="14f0c-144">A model class has properties that map to the fields of your index.</span></span> <span data-ttu-id="14f0c-145">This allows you to bind documents from your search index to instances of your model class.</span><span class="sxs-lookup"><span data-stu-id="14f0c-145">This allows you to bind documents from your search index to instances of your model class.</span></span>

> [!NOTE]
> If you don't plan to use a model class, you can still define your index by creating `Field` objects directly. You can provide the name of the field to the constructor, along with the data type (or analyzer for string fields). You can also set other properties like `IsSearchable`, `IsFilterable`, etc.
>
>

<span data-ttu-id="14f0c-149">It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [appropriate properties](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span><span class="sxs-lookup"><span data-stu-id="14f0c-149">It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [appropriate properties](https://docs.microsoft.com/rest/api/searchservice/Create-Index).</span></span> <span data-ttu-id="14f0c-150">These properties control which search features (filtering, faceting, sorting full-text search, etc.) apply to which fields.</span><span class="sxs-lookup"><span data-stu-id="14f0c-150">These properties control which search features (filtering, faceting, sorting full-text search, etc.) apply to which fields.</span></span> <span data-ttu-id="14f0c-151">For any property you do not explicitly set, the `Field` class defaults to disabling the corresponding search feature unless you specifically enable it.</span><span class="sxs-lookup"><span data-stu-id="14f0c-151">For any property you do not explicitly set, the `Field` class defaults to disabling the corresponding search feature unless you specifically enable it.</span></span>

<span data-ttu-id="14f0c-152">For our example, we've named our index "hotels" and defined our fields using a model class.</span><span class="sxs-lookup"><span data-stu-id="14f0c-152">For our example, we've named our index "hotels" and defined our fields using a model class.</span></span> <span data-ttu-id="14f0c-153">Each property of the model class has attributes which determine the search-related behaviors of the corresponding index field.</span><span class="sxs-lookup"><span data-stu-id="14f0c-153">Each property of the model class has attributes which determine the search-related behaviors of the corresponding index field.</span></span> <span data-ttu-id="14f0c-154">The model class is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="14f0c-154">The model class is defined as follows:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

<span data-ttu-id="14f0c-155">We have carefully chosen the attributes for each property based on how we think they will be used in an application.</span><span class="sxs-lookup"><span data-stu-id="14f0c-155">We have carefully chosen the attributes for each property based on how we think they will be used in an application.</span></span> <span data-ttu-id="14f0c-156">For example, it is likely that people searching for hotels will be interested in keyword matches on the `description` field, so we enable full-text search for that field by adding the `IsSearchable` attribute to the `Description` property.</span><span class="sxs-lookup"><span data-stu-id="14f0c-156">For example, it is likely that people searching for hotels will be interested in keyword matches on the `description` field, so we enable full-text search for that field by adding the `IsSearchable` attribute to the `Description` property.</span></span>

<span data-ttu-id="14f0c-157">Please note that exactly one field in your index of type `string` must be the designated as the *key* field by adding the `Key` attribute (see `HotelId` in the above example).</span><span class="sxs-lookup"><span data-stu-id="14f0c-157">Please note that exactly one field in your index of type `string` must be the designated as the *key* field by adding the `Key` attribute (see `HotelId` in the above example).</span></span>

<span data-ttu-id="14f0c-158">The index definition above uses a language analyzer for the `description_fr` field because it is intended to store French text.</span><span class="sxs-lookup"><span data-stu-id="14f0c-158">The index definition above uses a language analyzer for the `description_fr` field because it is intended to store French text.</span></span> <span data-ttu-id="14f0c-159">See [the Language support topic](https://docs.microsoft.com/rest/api/searchservice/Language-support) as well as the corresponding [blog post](https://azure.microsoft.com/blog/language-support-in-azure-search/) for more information about language analyzers.</span><span class="sxs-lookup"><span data-stu-id="14f0c-159">See [the Language support topic](https://docs.microsoft.com/rest/api/searchservice/Language-support) as well as the corresponding [blog post](https://azure.microsoft.com/blog/language-support-in-azure-search/) for more information about language analyzers.</span></span>

> [!NOTE]
> By default, the name of each property in your model class is used as the name of the corresponding field in the index. If you want to map all property names to camel-case field names, mark the class with the `SerializePropertyNamesAsCamelCase` attribute. If you want to map to a different name, you can use the `JsonProperty` attribute like the `DescriptionFr` property above. The `JsonProperty` attribute takes precedence over the `SerializePropertyNamesAsCamelCase` attribute.
> 
> 

<span data-ttu-id="14f0c-164">Now that we've defined a model class, we can create an index definition very easily:</span><span class="sxs-lookup"><span data-stu-id="14f0c-164">Now that we've defined a model class, we can create an index definition very easily:</span></span>

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-the-index"></a><span data-ttu-id="14f0c-165">Create the index</span><span class="sxs-lookup"><span data-stu-id="14f0c-165">Create the index</span></span>
<span data-ttu-id="14f0c-166">Now that you have an initialized `Index` object, you can create the index simply by calling `Indexes.Create` on your `SearchServiceClient` object:</span><span class="sxs-lookup"><span data-stu-id="14f0c-166">Now that you have an initialized `Index` object, you can create the index simply by calling `Indexes.Create` on your `SearchServiceClient` object:</span></span>

```csharp
serviceClient.Indexes.Create(definition);
```

<span data-ttu-id="14f0c-167">For a successful request, the method will return normally.</span><span class="sxs-lookup"><span data-stu-id="14f0c-167">For a successful request, the method will return normally.</span></span> <span data-ttu-id="14f0c-168">If there is a problem with the request such as an invalid parameter, the method will throw `CloudException`.</span><span class="sxs-lookup"><span data-stu-id="14f0c-168">If there is a problem with the request such as an invalid parameter, the method will throw `CloudException`.</span></span>

<span data-ttu-id="14f0c-169">When you're done with an index and want to delete it, just call the `Indexes.Delete` method on your `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="14f0c-169">When you're done with an index and want to delete it, just call the `Indexes.Delete` method on your `SearchServiceClient`.</span></span> <span data-ttu-id="14f0c-170">For example, this is how we would delete the "hotels" index:</span><span class="sxs-lookup"><span data-stu-id="14f0c-170">For example, this is how we would delete the "hotels" index:</span></span>

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity. We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive. For example, in the examples above you could use `CreateAsync` and `DeleteAsync` instead of `Create` and `Delete`.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="14f0c-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="14f0c-174">Next steps</span></span>
<span data-ttu-id="14f0c-175">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span><span class="sxs-lookup"><span data-stu-id="14f0c-175">After creating an Azure Search index, you will be ready to [upload your content into the index](search-what-is-data-import.md) so you can start searching your data.</span></span>

