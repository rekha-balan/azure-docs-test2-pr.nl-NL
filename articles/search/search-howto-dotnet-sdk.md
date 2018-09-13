---
title: How to use Azure Search from a .NET Application | Microsoft Docs
description: How to use Azure Search from a .NET Application
services: search
documentationcenter: ''
author: brjohnstmsft
manager: pablocas
editor: ''
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 11/30/2016
ms.author: brjohnst
ms.openlocfilehash: 50e03b7a3af6f88c9ceb3241d60b9414bbe42d16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671987"
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="447c8-103">How to use Azure Search from a .NET Application</span><span class="sxs-lookup"><span data-stu-id="447c8-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="447c8-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="447c8-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="447c8-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span><span class="sxs-lookup"><span data-stu-id="447c8-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="447c8-106">What's in the Azure Search SDK</span><span class="sxs-lookup"><span data-stu-id="447c8-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="447c8-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="447c8-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="447c8-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span><span class="sxs-lookup"><span data-stu-id="447c8-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="447c8-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span><span class="sxs-lookup"><span data-stu-id="447c8-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="447c8-110">These classes are organized into the following namespaces:</span><span class="sxs-lookup"><span data-stu-id="447c8-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="447c8-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="447c8-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="447c8-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="447c8-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="447c8-113">The current version of the Azure Search .NET SDK is now generally available.</span><span class="sxs-lookup"><span data-stu-id="447c8-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="447c8-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="447c8-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="447c8-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="447c8-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="447c8-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span><span class="sxs-lookup"><span data-stu-id="447c8-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="447c8-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="447c8-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="447c8-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span><span class="sxs-lookup"><span data-stu-id="447c8-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="447c8-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="447c8-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="447c8-120">Upgrading to the latest version of the SDK</span><span class="sxs-lookup"><span data-stu-id="447c8-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="447c8-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span><span class="sxs-lookup"><span data-stu-id="447c8-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="447c8-122">Requirements for the SDK</span><span class="sxs-lookup"><span data-stu-id="447c8-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="447c8-123">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="447c8-123">Visual Studio 2015.</span></span>
2. <span data-ttu-id="447c8-124">Your own Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="447c8-124">Your own Azure Search service.</span></span> <span data-ttu-id="447c8-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span><span class="sxs-lookup"><span data-stu-id="447c8-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="447c8-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span><span class="sxs-lookup"><span data-stu-id="447c8-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="447c8-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="447c8-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="447c8-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="447c8-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="447c8-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.5, .NET Core, as well as apps compatible with [Portable Class Library (PCL) Profile 111](https://docs.microsoft.com/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="447c8-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.5, .NET Core, as well as apps compatible with [Portable Class Library (PCL) Profile 111](https://docs.microsoft.com/dotnet/articles/standard/library).</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="447c8-130">Core scenarios</span><span class="sxs-lookup"><span data-stu-id="447c8-130">Core scenarios</span></span>
<span data-ttu-id="447c8-131">There are several things you'll need to do in your search application.</span><span class="sxs-lookup"><span data-stu-id="447c8-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="447c8-132">In this tutorial, we'll cover these core scenarios:</span><span class="sxs-lookup"><span data-stu-id="447c8-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="447c8-133">Creating an index</span><span class="sxs-lookup"><span data-stu-id="447c8-133">Creating an index</span></span>
* <span data-ttu-id="447c8-134">Populating the index with documents</span><span class="sxs-lookup"><span data-stu-id="447c8-134">Populating the index with documents</span></span>
* <span data-ttu-id="447c8-135">Searching for documents using full-text search and filters</span><span class="sxs-lookup"><span data-stu-id="447c8-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="447c8-136">The sample code that follows illustrates each of these.</span><span class="sxs-lookup"><span data-stu-id="447c8-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="447c8-137">Feel free to use the code snippets in your own application.</span><span class="sxs-lookup"><span data-stu-id="447c8-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="447c8-138">Overview</span><span class="sxs-lookup"><span data-stu-id="447c8-138">Overview</span></span>
<span data-ttu-id="447c8-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span><span class="sxs-lookup"><span data-stu-id="447c8-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="447c8-140">Here is the main program, showing the overall flow:</span><span class="sxs-lookup"><span data-stu-id="447c8-140">Here is the main program, showing the overall flow:</span></span>

    // This sample shows how to delete, create, upload documents and query an index
    static void Main(string[] args)
    {
        SearchServiceClient serviceClient = CreateSearchServiceClient();

        Console.WriteLine("{0}", "Deleting index...\n");
        DeleteHotelsIndexIfExists(serviceClient);

        Console.WriteLine("{0}", "Creating index...\n");
        CreateHotelsIndex(serviceClient);

        ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

        Console.WriteLine("{0}", "Uploading documents...\n");
        UploadDocuments(indexClient);

        ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

        RunQueries(indexClientForQueries);

        Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
        Console.ReadKey();
    }

<span data-ttu-id="447c8-141">We'll walk through this step by step.</span><span class="sxs-lookup"><span data-stu-id="447c8-141">We'll walk through this step by step.</span></span> <span data-ttu-id="447c8-142">First we need to create a new `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="447c8-142">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="447c8-143">This object allows you to manage indexes.</span><span class="sxs-lookup"><span data-stu-id="447c8-143">This object allows you to manage indexes.</span></span> <span data-ttu-id="447c8-144">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span><span class="sxs-lookup"><span data-stu-id="447c8-144">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span>

    private static SearchServiceClient CreateSearchServiceClient()
    {
        string searchServiceName = "myservice";
        string adminApiKey = "Put your API admin key here";

        SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
        return serviceClient;
    }

> [!NOTE]
> <span data-ttu-id="447c8-145">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="447c8-145">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="447c8-146">If this happens to you, double-check our API key.</span><span class="sxs-lookup"><span data-stu-id="447c8-146">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="447c8-147">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span><span class="sxs-lookup"><span data-stu-id="447c8-147">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="447c8-148">We will walk through these methods a little later.</span><span class="sxs-lookup"><span data-stu-id="447c8-148">We will walk through these methods a little later.</span></span>

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

<span data-ttu-id="447c8-149">Next, the index needs to be populated.</span><span class="sxs-lookup"><span data-stu-id="447c8-149">Next, the index needs to be populated.</span></span> <span data-ttu-id="447c8-150">To do this, we will need a `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="447c8-150">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="447c8-151">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="447c8-151">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="447c8-152">We use the latter for convenience.</span><span class="sxs-lookup"><span data-stu-id="447c8-152">We use the latter for convenience.</span></span>

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

> [!NOTE]
> <span data-ttu-id="447c8-153">In a typical search application, index management and population is handled by a separate component from search queries.</span><span class="sxs-lookup"><span data-stu-id="447c8-153">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="447c8-154">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="447c8-154">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="447c8-155">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="447c8-155">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="447c8-156">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span><span class="sxs-lookup"><span data-stu-id="447c8-156">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="447c8-157">This is consistent with the principle of least privilege and will help to make your application more secure.</span><span class="sxs-lookup"><span data-stu-id="447c8-157">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="447c8-158">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="447c8-158">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="447c8-159">Now that we have a `SearchIndexClient`, we can populate the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-159">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="447c8-160">This is done by another method that we will walk through later.</span><span class="sxs-lookup"><span data-stu-id="447c8-160">This is done by another method that we will walk through later.</span></span>

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

<span data-ttu-id="447c8-161">Finally, we execute a few search queries and display the results.</span><span class="sxs-lookup"><span data-stu-id="447c8-161">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="447c8-162">This time we use a different `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="447c8-162">This time we use a different `SearchIndexClient`:</span></span>

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

    RunQueries(indexClientForQueries);

<span data-ttu-id="447c8-163">We will take a closer look at the `RunQueries` method later.</span><span class="sxs-lookup"><span data-stu-id="447c8-163">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="447c8-164">Here is the code to create the new `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="447c8-164">Here is the code to create the new `SearchIndexClient`:</span></span>

    private static SearchIndexClient CreateSearchIndexClient()
    {
        string searchServiceName = "myservice";
        string queryApiKey = "Put one of your API query keys here";

        SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
        return indexClient;
    }

<span data-ttu-id="447c8-165">This time we use a query key since we do not need write access to the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-165">This time we use a query key since we do not need write access to the index.</span></span>

<span data-ttu-id="447c8-166">If you run this application with a valid service name and API keys, the output should look like this:</span><span class="sxs-lookup"><span data-stu-id="447c8-166">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="447c8-167">The full source code of the application is provided at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="447c8-167">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="447c8-168">Next, we will take a closer look at each of the methods called by `Main`.</span><span class="sxs-lookup"><span data-stu-id="447c8-168">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="447c8-169">Creating an index</span><span class="sxs-lookup"><span data-stu-id="447c8-169">Creating an index</span></span>
<span data-ttu-id="447c8-170">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span><span class="sxs-lookup"><span data-stu-id="447c8-170">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="447c8-171">That is done by the following method:</span><span class="sxs-lookup"><span data-stu-id="447c8-171">That is done by the following method:</span></span>

    private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
    {
        if (serviceClient.Indexes.Exists("hotels"))
        {
            serviceClient.Indexes.Delete("hotels");
        }
    }

<span data-ttu-id="447c8-172">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span><span class="sxs-lookup"><span data-stu-id="447c8-172">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-173">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span><span class="sxs-lookup"><span data-stu-id="447c8-173">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="447c8-174">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span><span class="sxs-lookup"><span data-stu-id="447c8-174">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="447c8-175">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span><span class="sxs-lookup"><span data-stu-id="447c8-175">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="447c8-176">Next, `Main` creates a new "hotels" index by calling this method:</span><span class="sxs-lookup"><span data-stu-id="447c8-176">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

    private static void CreateHotelsIndex(SearchServiceClient serviceClient)
    {
        var definition = new Index()
        {
            Name = "hotels",
            Fields = FieldBuilder.BuildForType<Hotel>()
        };

        serviceClient.Indexes.Create(definition);
    }

<span data-ttu-id="447c8-177">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span><span class="sxs-lookup"><span data-stu-id="447c8-177">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="447c8-178">Each field has a name, data type, and several attributes that define its search behavior.</span><span class="sxs-lookup"><span data-stu-id="447c8-178">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="447c8-179">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span><span class="sxs-lookup"><span data-stu-id="447c8-179">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="447c8-180">We'll take a closer look at the `Hotel` class later on.</span><span class="sxs-lookup"><span data-stu-id="447c8-180">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-181">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span><span class="sxs-lookup"><span data-stu-id="447c8-181">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="447c8-182">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span><span class="sxs-lookup"><span data-stu-id="447c8-182">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="447c8-183">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span><span class="sxs-lookup"><span data-stu-id="447c8-183">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="447c8-184">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="447c8-184">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="447c8-185">Populating the index</span><span class="sxs-lookup"><span data-stu-id="447c8-185">Populating the index</span></span>
<span data-ttu-id="447c8-186">The next step in `Main` is to populate the newly-created index.</span><span class="sxs-lookup"><span data-stu-id="447c8-186">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="447c8-187">This is done in the following method:</span><span class="sxs-lookup"><span data-stu-id="447c8-187">This is done in the following method:</span></span>

    private static void UploadDocuments(ISearchIndexClient indexClient)
    {
        var hotels = new Hotel[]
        {
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
            },
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
            },
            new Hotel() 
            { 
                HotelId = "3", 
                BaseRate = 129.99,
                Description = "Close to town hall and the river"
            }
        };

        var batch = IndexBatch.Upload(hotels);

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
    }

<span data-ttu-id="447c8-188">This method has four parts.</span><span class="sxs-lookup"><span data-stu-id="447c8-188">This method has four parts.</span></span> <span data-ttu-id="447c8-189">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-189">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="447c8-190">This data is hard-coded for simplicity.</span><span class="sxs-lookup"><span data-stu-id="447c8-190">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="447c8-191">In your own application, your data will likely come from an external data source such as a SQL database.</span><span class="sxs-lookup"><span data-stu-id="447c8-191">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="447c8-192">The second part creates an `IndexBatch` containing the documents.</span><span class="sxs-lookup"><span data-stu-id="447c8-192">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="447c8-193">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="447c8-193">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="447c8-194">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span><span class="sxs-lookup"><span data-stu-id="447c8-194">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-195">In this example, we are just uploading documents.</span><span class="sxs-lookup"><span data-stu-id="447c8-195">In this example, we are just uploading documents.</span></span> <span data-ttu-id="447c8-196">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span><span class="sxs-lookup"><span data-stu-id="447c8-196">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="447c8-197">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span><span class="sxs-lookup"><span data-stu-id="447c8-197">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="447c8-198">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span><span class="sxs-lookup"><span data-stu-id="447c8-198">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="447c8-199">The third part of this method is a catch block that handles an important error case for indexing.</span><span class="sxs-lookup"><span data-stu-id="447c8-199">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="447c8-200">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="447c8-200">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="447c8-201">This can happen if you are indexing documents while your service is under heavy load.</span><span class="sxs-lookup"><span data-stu-id="447c8-201">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="447c8-202">**We strongly recommend explicitly handling this case in your code.**</span><span class="sxs-lookup"><span data-stu-id="447c8-202">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="447c8-203">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span><span class="sxs-lookup"><span data-stu-id="447c8-203">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-204">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span><span class="sxs-lookup"><span data-stu-id="447c8-204">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="447c8-205">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="447c8-205">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="447c8-206">Finally, the `UploadDocuments` method delays for two seconds.</span><span class="sxs-lookup"><span data-stu-id="447c8-206">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="447c8-207">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span><span class="sxs-lookup"><span data-stu-id="447c8-207">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="447c8-208">Delays like this are typically only necessary in demos, tests, and sample applications.</span><span class="sxs-lookup"><span data-stu-id="447c8-208">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="447c8-209">How the .NET SDK handles documents</span><span class="sxs-lookup"><span data-stu-id="447c8-209">How the .NET SDK handles documents</span></span>
<span data-ttu-id="447c8-210">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-210">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="447c8-211">To help answer that question, let's look at the `Hotel` class:</span><span class="sxs-lookup"><span data-stu-id="447c8-211">To help answer that question, let's look at the `Hotel` class:</span></span>

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

<span data-ttu-id="447c8-212">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span><span class="sxs-lookup"><span data-stu-id="447c8-212">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="447c8-213">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span><span class="sxs-lookup"><span data-stu-id="447c8-213">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="447c8-214">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span><span class="sxs-lookup"><span data-stu-id="447c8-214">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-215">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span><span class="sxs-lookup"><span data-stu-id="447c8-215">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="447c8-216">You can customize this serialization if needed.</span><span class="sxs-lookup"><span data-stu-id="447c8-216">You can customize this serialization if needed.</span></span> <span data-ttu-id="447c8-217">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="447c8-217">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="447c8-218">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span><span class="sxs-lookup"><span data-stu-id="447c8-218">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="447c8-219">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="447c8-219">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="447c8-220">The `FieldBuilder` class uses these to construct field definitions for the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-220">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="447c8-221">The third important thing about the `Hotel` class are the data types of the public properties.</span><span class="sxs-lookup"><span data-stu-id="447c8-221">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="447c8-222">The .NET types of  these properties map to their equivalent field types in the index definition.</span><span class="sxs-lookup"><span data-stu-id="447c8-222">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="447c8-223">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="447c8-223">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="447c8-224">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="447c8-224">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="447c8-225">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span><span class="sxs-lookup"><span data-stu-id="447c8-225">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="447c8-226">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span><span class="sxs-lookup"><span data-stu-id="447c8-226">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-227">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span><span class="sxs-lookup"><span data-stu-id="447c8-227">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="447c8-228">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span><span class="sxs-lookup"><span data-stu-id="447c8-228">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="447c8-229">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span><span class="sxs-lookup"><span data-stu-id="447c8-229">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="447c8-230">Only the latter are used in the sample code in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="447c8-230">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="447c8-231">The `Document` class inherits from `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="447c8-231">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="447c8-232">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="447c8-232">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="447c8-233">**Why you should use nullable data types**</span><span class="sxs-lookup"><span data-stu-id="447c8-233">**Why you should use nullable data types**</span></span>

<span data-ttu-id="447c8-234">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span><span class="sxs-lookup"><span data-stu-id="447c8-234">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="447c8-235">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span><span class="sxs-lookup"><span data-stu-id="447c8-235">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="447c8-236">Neither the SDK nor the Azure Search service will help you to enforce this.</span><span class="sxs-lookup"><span data-stu-id="447c8-236">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="447c8-237">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="447c8-237">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="447c8-238">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span><span class="sxs-lookup"><span data-stu-id="447c8-238">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="447c8-239">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span><span class="sxs-lookup"><span data-stu-id="447c8-239">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="447c8-240">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span><span class="sxs-lookup"><span data-stu-id="447c8-240">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="447c8-241">Custom Serialization with JSON.NET</span><span class="sxs-lookup"><span data-stu-id="447c8-241">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="447c8-242">The SDK uses JSON.NET for serializing and deserializing documents.</span><span class="sxs-lookup"><span data-stu-id="447c8-242">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="447c8-243">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span><span class="sxs-lookup"><span data-stu-id="447c8-243">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="447c8-244">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span><span class="sxs-lookup"><span data-stu-id="447c8-244">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="447c8-245">For example, with custom serialization you can:</span><span class="sxs-lookup"><span data-stu-id="447c8-245">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="447c8-246">Include or exclude certain properties of your model class from being stored as document fields.</span><span class="sxs-lookup"><span data-stu-id="447c8-246">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="447c8-247">Map between property names in your code and field names in your index.</span><span class="sxs-lookup"><span data-stu-id="447c8-247">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="447c8-248">Create custom attributes that can be used for mapping properties to document fields.</span><span class="sxs-lookup"><span data-stu-id="447c8-248">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="447c8-249">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span><span class="sxs-lookup"><span data-stu-id="447c8-249">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="447c8-250">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="447c8-250">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="447c8-251">It contains classes that are used by the custom serialization tests.</span><span class="sxs-lookup"><span data-stu-id="447c8-251">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="447c8-252">Searching for documents in the index</span><span class="sxs-lookup"><span data-stu-id="447c8-252">Searching for documents in the index</span></span>
<span data-ttu-id="447c8-253">The last step in the sample application is to search for some documents in the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-253">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="447c8-254">The following method does this:</span><span class="sxs-lookup"><span data-stu-id="447c8-254">The following method does this:</span></span>

    private static void RunQueries(ISearchIndexClient indexClient)
    {
        SearchParameters parameters;
        DocumentSearchResult<Hotel> results;
    
        Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");
    
        parameters =
            new SearchParameters()
            {
                Select = new[] { "hotelName" }
            };
    
        results = indexClient.Documents.Search<Hotel>("budget", parameters);
    
        WriteDocuments(results);
    
        Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
        Console.WriteLine("and return the hotelId and description:\n");
    
        parameters =
            new SearchParameters()
            {
                Filter = "baseRate lt 150",
                Select = new[] { "hotelId", "description" }
            };
    
        results = indexClient.Documents.Search<Hotel>("*", parameters);
    
        WriteDocuments(results);
    
        Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
        Console.Write("in descending order, take the top two results, and show only hotelName and ");
        Console.WriteLine("lastRenovationDate:\n");
    
        parameters =
            new SearchParameters()
            {
                OrderBy = new[] { "lastRenovationDate desc" },
                Select = new[] { "hotelName", "lastRenovationDate" },
                Top = 2
            };
    
        results = indexClient.Documents.Search<Hotel>("*", parameters);
    
        WriteDocuments(results);
    
        Console.WriteLine("Search the entire index for the term 'motel':\n");
    
        parameters = new SearchParameters();
        results = indexClient.Documents.Search<Hotel>("motel", parameters);
    
        WriteDocuments(results);
    }

<span data-ttu-id="447c8-255">Each time it executes a query, this method first creates a new `SearchParameters` object.</span><span class="sxs-lookup"><span data-stu-id="447c8-255">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="447c8-256">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span><span class="sxs-lookup"><span data-stu-id="447c8-256">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="447c8-257">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span><span class="sxs-lookup"><span data-stu-id="447c8-257">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="447c8-258">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="447c8-258">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="447c8-259">The next step is to actually execute the search query.</span><span class="sxs-lookup"><span data-stu-id="447c8-259">The next step is to actually execute the search query.</span></span> <span data-ttu-id="447c8-260">This is done using the `Documents.Search` method.</span><span class="sxs-lookup"><span data-stu-id="447c8-260">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="447c8-261">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span><span class="sxs-lookup"><span data-stu-id="447c8-261">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="447c8-262">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="447c8-262">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="447c8-263">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="447c8-263">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="447c8-264">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span><span class="sxs-lookup"><span data-stu-id="447c8-264">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

    private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
    {
        foreach (SearchResult<Hotel> result in searchResults.Results)
        {
            Console.WriteLine(result.Document);
        }

        Console.WriteLine();
    }

<span data-ttu-id="447c8-265">Let's take a closer look at each of the queries in turn.</span><span class="sxs-lookup"><span data-stu-id="447c8-265">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="447c8-266">Here is the code to execute the first query:</span><span class="sxs-lookup"><span data-stu-id="447c8-266">Here is the code to execute the first query:</span></span>

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

<span data-ttu-id="447c8-267">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span><span class="sxs-lookup"><span data-stu-id="447c8-267">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="447c8-268">Here are the results:</span><span class="sxs-lookup"><span data-stu-id="447c8-268">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="447c8-269">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span><span class="sxs-lookup"><span data-stu-id="447c8-269">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

<span data-ttu-id="447c8-270">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span><span class="sxs-lookup"><span data-stu-id="447c8-270">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="447c8-271">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="447c8-271">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="447c8-272">Here are the results of the query:</span><span class="sxs-lookup"><span data-stu-id="447c8-272">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="447c8-273">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span><span class="sxs-lookup"><span data-stu-id="447c8-273">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="447c8-274">Here is the code:</span><span class="sxs-lookup"><span data-stu-id="447c8-274">Here is the code:</span></span> 

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };
    
    results = indexClient.Documents.Search<Hotel>("*", parameters);
    
    WriteDocuments(results);

<span data-ttu-id="447c8-275">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="447c8-275">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="447c8-276">We also set `Top` to 2 to ensure we only get the top two documents.</span><span class="sxs-lookup"><span data-stu-id="447c8-276">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="447c8-277">As before, we set `Select` to specify which fields should be returned.</span><span class="sxs-lookup"><span data-stu-id="447c8-277">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="447c8-278">Here are the results:</span><span class="sxs-lookup"><span data-stu-id="447c8-278">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="447c8-279">Finally, we want to find all hotels that match the word "motel":</span><span class="sxs-lookup"><span data-stu-id="447c8-279">Finally, we want to find all hotels that match the word "motel":</span></span>

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);

<span data-ttu-id="447c8-280">And here are the results, which include all fields since we did not specify the `Select` property:</span><span class="sxs-lookup"><span data-stu-id="447c8-280">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="447c8-281">This step completes the tutorial, but don't stop here.</span><span class="sxs-lookup"><span data-stu-id="447c8-281">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="447c8-282">**Next steps** provides additional resources for learning more about Azure Search.</span><span class="sxs-lookup"><span data-stu-id="447c8-282">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="447c8-283">Sample application source code</span><span class="sxs-lookup"><span data-stu-id="447c8-283">Sample application source code</span></span>
<span data-ttu-id="447c8-284">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="447c8-284">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

## <a name="next-steps"></a><span data-ttu-id="447c8-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="447c8-285">Next steps</span></span>
* <span data-ttu-id="447c8-286">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="447c8-286">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="447c8-287">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="447c8-287">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="447c8-288">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span><span class="sxs-lookup"><span data-stu-id="447c8-288">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="447c8-289">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="447c8-289">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
