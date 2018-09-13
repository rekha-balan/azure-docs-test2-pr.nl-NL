---
title: List Azure Storage resources with the Storage Client Library for C++ | Microsoft Docs
description: Learn how to use the listing APIs in Microsoft Azure Storage Client Library for C++ to enumerate containers, blobs, queues, tables, and entities.
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: 4a4ac7938989f821c092379aff3085f5e440d1c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554308"
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="c8983-103">List Azure Storage resources in C++</span><span class="sxs-lookup"><span data-stu-id="c8983-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="c8983-104">Listing operations are key to many development scenarios with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c8983-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="c8983-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span><span class="sxs-lookup"><span data-stu-id="c8983-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="c8983-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="c8983-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="c8983-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c8983-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="c8983-108">This article addresses the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="c8983-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="c8983-109">List containers in an account</span><span class="sxs-lookup"><span data-stu-id="c8983-109">List containers in an account</span></span>
* <span data-ttu-id="c8983-110">List blobs in a container or virtual blob directory</span><span class="sxs-lookup"><span data-stu-id="c8983-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="c8983-111">List queues in an account</span><span class="sxs-lookup"><span data-stu-id="c8983-111">List queues in an account</span></span>
* <span data-ttu-id="c8983-112">List tables in an account</span><span class="sxs-lookup"><span data-stu-id="c8983-112">List tables in an account</span></span>
* <span data-ttu-id="c8983-113">Query entities in a table</span><span class="sxs-lookup"><span data-stu-id="c8983-113">Query entities in a table</span></span>

<span data-ttu-id="c8983-114">Each of these methods is shown using different overloads for different scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8983-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="c8983-115">Asynchronous versus synchronous</span><span class="sxs-lookup"><span data-stu-id="c8983-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="c8983-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="c8983-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="c8983-117">For example:</span><span class="sxs-lookup"><span data-stu-id="c8983-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="c8983-118">Synchronous operations wrap the corresponding asynchronous operations:</span><span class="sxs-lookup"><span data-stu-id="c8983-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="c8983-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span><span class="sxs-lookup"><span data-stu-id="c8983-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="c8983-120">Segmented listing</span><span class="sxs-lookup"><span data-stu-id="c8983-120">Segmented listing</span></span>
<span data-ttu-id="c8983-121">The scale of cloud storage requires segmented listing.</span><span class="sxs-lookup"><span data-stu-id="c8983-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="c8983-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span><span class="sxs-lookup"><span data-stu-id="c8983-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="c8983-123">These are not theoretical numbers, but real customer usage cases.</span><span class="sxs-lookup"><span data-stu-id="c8983-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="c8983-124">It is therefore impractical to list all objects in a single response.</span><span class="sxs-lookup"><span data-stu-id="c8983-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="c8983-125">Instead, you can list objects using paging.</span><span class="sxs-lookup"><span data-stu-id="c8983-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="c8983-126">Each of the listing APIs has a *segmented* overload.</span><span class="sxs-lookup"><span data-stu-id="c8983-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="c8983-127">The response for a segmented listing operation includes:</span><span class="sxs-lookup"><span data-stu-id="c8983-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="c8983-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span><span class="sxs-lookup"><span data-stu-id="c8983-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="c8983-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span><span class="sxs-lookup"><span data-stu-id="c8983-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="c8983-130">When there are no more results to return, the continuation token is null.</span><span class="sxs-lookup"><span data-stu-id="c8983-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="c8983-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span><span class="sxs-lookup"><span data-stu-id="c8983-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="c8983-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="c8983-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="c8983-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span><span class="sxs-lookup"><span data-stu-id="c8983-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="c8983-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span><span class="sxs-lookup"><span data-stu-id="c8983-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="c8983-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span><span class="sxs-lookup"><span data-stu-id="c8983-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="c8983-136">One reason might be that the query could not complete in five seconds.</span><span class="sxs-lookup"><span data-stu-id="c8983-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="c8983-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span><span class="sxs-lookup"><span data-stu-id="c8983-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="c8983-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span><span class="sxs-lookup"><span data-stu-id="c8983-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="c8983-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span><span class="sxs-lookup"><span data-stu-id="c8983-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="c8983-140">Greedy listing</span><span class="sxs-lookup"><span data-stu-id="c8983-140">Greedy listing</span></span>
<span data-ttu-id="c8983-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="c8983-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="c8983-142">These methods were implemented as wrappers of segmented APIs.</span><span class="sxs-lookup"><span data-stu-id="c8983-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="c8983-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span><span class="sxs-lookup"><span data-stu-id="c8983-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="c8983-144">This approach might work when the storage account or table contains a small number of objects.</span><span class="sxs-lookup"><span data-stu-id="c8983-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="c8983-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span><span class="sxs-lookup"><span data-stu-id="c8983-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="c8983-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span><span class="sxs-lookup"><span data-stu-id="c8983-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="c8983-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span><span class="sxs-lookup"><span data-stu-id="c8983-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="c8983-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span><span class="sxs-lookup"><span data-stu-id="c8983-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="c8983-149">If your code is calling these greedy APIs:</span><span class="sxs-lookup"><span data-stu-id="c8983-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="c8983-150">Then you should modify your code to use the segmented listing APIs:</span><span class="sxs-lookup"><span data-stu-id="c8983-150">Then you should modify your code to use the segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="c8983-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span><span class="sxs-lookup"><span data-stu-id="c8983-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="c8983-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span><span class="sxs-lookup"><span data-stu-id="c8983-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="c8983-153">Lazy listing</span><span class="sxs-lookup"><span data-stu-id="c8983-153">Lazy listing</span></span>
<span data-ttu-id="c8983-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span><span class="sxs-lookup"><span data-stu-id="c8983-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="c8983-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span><span class="sxs-lookup"><span data-stu-id="c8983-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="c8983-156">In C++, the iterator-based template also provides a similar approach.</span><span class="sxs-lookup"><span data-stu-id="c8983-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="c8983-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span><span class="sxs-lookup"><span data-stu-id="c8983-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="c8983-158">A typical code snippet that uses the lazy listing pattern might look like this:</span><span class="sxs-lookup"><span data-stu-id="c8983-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="c8983-159">Note that lazy listing is only available in synchronous mode.</span><span class="sxs-lookup"><span data-stu-id="c8983-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="c8983-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span><span class="sxs-lookup"><span data-stu-id="c8983-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="c8983-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span><span class="sxs-lookup"><span data-stu-id="c8983-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="c8983-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span><span class="sxs-lookup"><span data-stu-id="c8983-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="c8983-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="c8983-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c8983-164">Conclusion</span><span class="sxs-lookup"><span data-stu-id="c8983-164">Conclusion</span></span>
<span data-ttu-id="c8983-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span><span class="sxs-lookup"><span data-stu-id="c8983-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="c8983-166">To summarize:</span><span class="sxs-lookup"><span data-stu-id="c8983-166">To summarize:</span></span>

* <span data-ttu-id="c8983-167">Async APIs are strongly recommended under multiple threading scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8983-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="c8983-168">Segmented listing is recommended for most scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8983-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="c8983-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8983-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="c8983-170">Greedy listing is not recommended and has been removed from the library.</span><span class="sxs-lookup"><span data-stu-id="c8983-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8983-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8983-171">Next steps</span></span>
<span data-ttu-id="c8983-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="c8983-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="c8983-173">How to use Blob Storage from C++</span><span class="sxs-lookup"><span data-stu-id="c8983-173">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="c8983-174">How to use Table Storage from C++</span><span class="sxs-lookup"><span data-stu-id="c8983-174">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="c8983-175">How to use Queue Storage from C++</span><span class="sxs-lookup"><span data-stu-id="c8983-175">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="c8983-176">Azure Storage Client Library for C++ API documentation.</span><span class="sxs-lookup"><span data-stu-id="c8983-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="c8983-177">Azure Storage Team Blog</span><span class="sxs-lookup"><span data-stu-id="c8983-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="c8983-178">Azure Storage Documentation</span><span class="sxs-lookup"><span data-stu-id="c8983-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

