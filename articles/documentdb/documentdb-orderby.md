---
redirect_url: https://azure.microsoft.com/services/documentdb/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 0ca716857733290fad4278e3be5059408bb75393
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552185"
---
# <a name="sorting-documentdb-data-using-order-by"></a><span data-ttu-id="02c0a-101">Sorting DocumentDB data using Order By</span><span class="sxs-lookup"><span data-stu-id="02c0a-101">Sorting DocumentDB data using Order By</span></span>
<span data-ttu-id="02c0a-102">Microsoft Azure DocumentDB supports querying documents using SQL over JSON documents.</span><span class="sxs-lookup"><span data-stu-id="02c0a-102">Microsoft Azure DocumentDB supports querying documents using SQL over JSON documents.</span></span> <span data-ttu-id="02c0a-103">Query results can be ordered using the ORDER BY clause in SQL query statements.</span><span class="sxs-lookup"><span data-stu-id="02c0a-103">Query results can be ordered using the ORDER BY clause in SQL query statements.</span></span>

<span data-ttu-id="02c0a-104">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="02c0a-104">After reading this article, you'll be able to answer the following questions:</span></span> 

* <span data-ttu-id="02c0a-105">How do I query with Order By?</span><span class="sxs-lookup"><span data-stu-id="02c0a-105">How do I query with Order By?</span></span>
* <span data-ttu-id="02c0a-106">How do I configure an indexing policy for Order By?</span><span class="sxs-lookup"><span data-stu-id="02c0a-106">How do I configure an indexing policy for Order By?</span></span>
* <span data-ttu-id="02c0a-107">What's coming next?</span><span class="sxs-lookup"><span data-stu-id="02c0a-107">What's coming next?</span></span>

<span data-ttu-id="02c0a-108">[Samples](#samples) and an [FAQ](#faq) are also provided.</span><span class="sxs-lookup"><span data-stu-id="02c0a-108">[Samples](#samples) and an [FAQ](#faq) are also provided.</span></span>

<span data-ttu-id="02c0a-109">For a complete reference on SQL querying, see the [DocumentDB Query tutorial](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="02c0a-109">For a complete reference on SQL querying, see the [DocumentDB Query tutorial](documentdb-sql-query.md).</span></span>

## <a name="how-to-query-with-order-by"></a><span data-ttu-id="02c0a-110">How to Query with Order By</span><span class="sxs-lookup"><span data-stu-id="02c0a-110">How to Query with Order By</span></span>
<span data-ttu-id="02c0a-111">Like in ANSI-SQL, you can now include an optional Order By clause in SQL statements when querying DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="02c0a-111">Like in ANSI-SQL, you can now include an optional Order By clause in SQL statements when querying DocumentDB.</span></span> <span data-ttu-id="02c0a-112">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span><span class="sxs-lookup"><span data-stu-id="02c0a-112">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span> 

### <a name="ordering-using-sql"></a><span data-ttu-id="02c0a-113">Ordering using SQL</span><span class="sxs-lookup"><span data-stu-id="02c0a-113">Ordering using SQL</span></span>
<span data-ttu-id="02c0a-114">For example here's a query to retrieve the top 10 books in descending order of their titles.</span><span class="sxs-lookup"><span data-stu-id="02c0a-114">For example here's a query to retrieve the top 10 books in descending order of their titles.</span></span> 

    SELECT TOP 10 * 
    FROM Books 
    ORDER BY Books.Title DESC

### <a name="ordering-using-sql-with-filtering"></a><span data-ttu-id="02c0a-115">Ordering using SQL with Filtering</span><span class="sxs-lookup"><span data-stu-id="02c0a-115">Ordering using SQL with Filtering</span></span>
<span data-ttu-id="02c0a-116">You can order using any nested property within documents like Books.ShippingDetails.Weight, and you can specify additional filters in the WHERE clause in combination with Order By like in this example:</span><span class="sxs-lookup"><span data-stu-id="02c0a-116">You can order using any nested property within documents like Books.ShippingDetails.Weight, and you can specify additional filters in the WHERE clause in combination with Order By like in this example:</span></span>

    SELECT * 
    FROM Books 
    WHERE Books.SalePrice > 4000
    ORDER BY Books.ShippingDetails.Weight

### <a name="ordering-using-the-linq-provider-for-net"></a><span data-ttu-id="02c0a-117">Ordering using the LINQ Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="02c0a-117">Ordering using the LINQ Provider for .NET</span></span>
<span data-ttu-id="02c0a-118">Using the .NET SDK version 1.2.0 and higher, you can also use the OrderBy() or OrderByDescending() clause within LINQ queries like in this example:</span><span class="sxs-lookup"><span data-stu-id="02c0a-118">Using the .NET SDK version 1.2.0 and higher, you can also use the OrderBy() or OrderByDescending() clause within LINQ queries like in this example:</span></span>

    foreach (Book book in client.CreateDocumentQuery<Book>(UriFactory.CreateDocumentCollectionUri("db", "books"))
        .OrderBy(b => b.PublishTimestamp)
        .Take(100))
    {
        // Iterate through books
    }

<span data-ttu-id="02c0a-119">DocumentDB supports ordering with a single numeric, string or Boolean property per query, with additional query types coming soon.</span><span class="sxs-lookup"><span data-stu-id="02c0a-119">DocumentDB supports ordering with a single numeric, string or Boolean property per query, with additional query types coming soon.</span></span> <span data-ttu-id="02c0a-120">Please see [What's coming next](#Whats_coming_next) for more details.</span><span class="sxs-lookup"><span data-stu-id="02c0a-120">Please see [What's coming next](#Whats_coming_next) for more details.</span></span>

## <a name="configure-an-indexing-policy-for-order-by"></a><span data-ttu-id="02c0a-121">Configure an indexing policy for Order By</span><span class="sxs-lookup"><span data-stu-id="02c0a-121">Configure an indexing policy for Order By</span></span>
<span data-ttu-id="02c0a-122">Recall that DocumentDB supports two kinds of indexes (Hash and Range), which can be set for specific paths/properties, data types (strings/numbers) and at different precision values (either maximum precision or a fixed precision value).</span><span class="sxs-lookup"><span data-stu-id="02c0a-122">Recall that DocumentDB supports two kinds of indexes (Hash and Range), which can be set for specific paths/properties, data types (strings/numbers) and at different precision values (either maximum precision or a fixed precision value).</span></span> <span data-ttu-id="02c0a-123">Since DocumentDB uses Hash indexing as default, you must create a new collection with a custom indexing policy with Range on numbers, strings or both, in order to use Order By.</span><span class="sxs-lookup"><span data-stu-id="02c0a-123">Since DocumentDB uses Hash indexing as default, you must create a new collection with a custom indexing policy with Range on numbers, strings or both, in order to use Order By.</span></span> 

> [!NOTE]
> <span data-ttu-id="02c0a-124">String range indexes were introduced on July 7, 2015 with REST API version 2015-06-03.</span><span class="sxs-lookup"><span data-stu-id="02c0a-124">String range indexes were introduced on July 7, 2015 with REST API version 2015-06-03.</span></span> <span data-ttu-id="02c0a-125">In order to create policies for Order By against strings, you must use SDK version 1.2.0 of the .NET SDK, or version 1.1.0 of the Python, Node.js or Java SDK.</span><span class="sxs-lookup"><span data-stu-id="02c0a-125">In order to create policies for Order By against strings, you must use SDK version 1.2.0 of the .NET SDK, or version 1.1.0 of the Python, Node.js or Java SDK.</span></span>
> 
> <span data-ttu-id="02c0a-126">Prior to REST API version 2015-06-03, the default collection indexing policy was Hash for both strings and numbers.</span><span class="sxs-lookup"><span data-stu-id="02c0a-126">Prior to REST API version 2015-06-03, the default collection indexing policy was Hash for both strings and numbers.</span></span> <span data-ttu-id="02c0a-127">This has been changed to Hash for strings, and Range for numbers.</span><span class="sxs-lookup"><span data-stu-id="02c0a-127">This has been changed to Hash for strings, and Range for numbers.</span></span> 
> 
> 

<span data-ttu-id="02c0a-128">For more details see [DocumentDB indexing policies](documentdb-indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="02c0a-128">For more details see [DocumentDB indexing policies](documentdb-indexing-policies.md).</span></span>

### <a name="indexing-for-order-by-against-all-properties"></a><span data-ttu-id="02c0a-129">Indexing for Order By against all properties</span><span class="sxs-lookup"><span data-stu-id="02c0a-129">Indexing for Order By against all properties</span></span>
<span data-ttu-id="02c0a-130">Here's how you can create a collection with "All Range" indexing for Order By against any/all numeric or string properties that appear within JSON documents within it.</span><span class="sxs-lookup"><span data-stu-id="02c0a-130">Here's how you can create a collection with "All Range" indexing for Order By against any/all numeric or string properties that appear within JSON documents within it.</span></span> <span data-ttu-id="02c0a-131">Here we override the default index type for string values to Range, and at the maximum precision (-1).</span><span class="sxs-lookup"><span data-stu-id="02c0a-131">Here we override the default index type for string values to Range, and at the maximum precision (-1).</span></span>

    DocumentCollection books = new DocumentCollection();
    books.Id = "books";
    books.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), books);  

> [!NOTE]
> <span data-ttu-id="02c0a-132">Note that Order By only will return results of the data types (String and Number) that are indexed with a RangeIndex.</span><span class="sxs-lookup"><span data-stu-id="02c0a-132">Note that Order By only will return results of the data types (String and Number) that are indexed with a RangeIndex.</span></span> <span data-ttu-id="02c0a-133">For example, if you have the default indexing policy which only has RangeIndex on numbers, an Order By against a path with string values will return no documents.</span><span class="sxs-lookup"><span data-stu-id="02c0a-133">For example, if you have the default indexing policy which only has RangeIndex on numbers, an Order By against a path with string values will return no documents.</span></span>
> 
> 

### <a name="indexing-for-order-by-for-a-single-property"></a><span data-ttu-id="02c0a-134">Indexing for Order By for a single property</span><span class="sxs-lookup"><span data-stu-id="02c0a-134">Indexing for Order By for a single property</span></span>
<span data-ttu-id="02c0a-135">Here's how you can create a collection with indexing for Order By against just the Title property, which is a string.</span><span class="sxs-lookup"><span data-stu-id="02c0a-135">Here's how you can create a collection with indexing for Order By against just the Title property, which is a string.</span></span> <span data-ttu-id="02c0a-136">There are two paths, one for the Title property ("/Title/?") with Range indexing, and the other for every other property with the default indexing scheme, which is Hash for strings and Range for numbers.</span><span class="sxs-lookup"><span data-stu-id="02c0a-136">There are two paths, one for the Title property ("/Title/?") with Range indexing, and the other for every other property with the default indexing scheme, which is Hash for strings and Range for numbers.</span></span>                    

    booksCollection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = -1 } } 
            });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), booksCollection);  


## <a name="samples"></a><span data-ttu-id="02c0a-137">Samples</span><span class="sxs-lookup"><span data-stu-id="02c0a-137">Samples</span></span>
<span data-ttu-id="02c0a-138">Take a look at this [GitHub samples project](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/Queries) that demonstrates how to use Order By, including creating indexing policies and paging using Order By.</span><span class="sxs-lookup"><span data-stu-id="02c0a-138">Take a look at this [GitHub samples project](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/Queries) that demonstrates how to use Order By, including creating indexing policies and paging using Order By.</span></span> <span data-ttu-id="02c0a-139">The samples are open source and we encourage you to submit pull requests with contributions that could benefit other DocumentDB developers.</span><span class="sxs-lookup"><span data-stu-id="02c0a-139">The samples are open source and we encourage you to submit pull requests with contributions that could benefit other DocumentDB developers.</span></span> <span data-ttu-id="02c0a-140">Please refer to the [Contribution guidelines](https://github.com/Azure/azure-documentdb-net/blob/master/Contributing.md) for guidance on how to contribute.</span><span class="sxs-lookup"><span data-stu-id="02c0a-140">Please refer to the [Contribution guidelines](https://github.com/Azure/azure-documentdb-net/blob/master/Contributing.md) for guidance on how to contribute.</span></span>  

## <a name="faq"></a><span data-ttu-id="02c0a-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="02c0a-141">FAQ</span></span>
<span data-ttu-id="02c0a-142">**What is the expected Request Unit (RU) consumption of Order By queries?**</span><span class="sxs-lookup"><span data-stu-id="02c0a-142">**What is the expected Request Unit (RU) consumption of Order By queries?**</span></span>

<span data-ttu-id="02c0a-143">Since Order By utilizes the DocumentDB index for lookups, the number of request units consumed by Order By queries will be similar to the equivalent queries without Order By.</span><span class="sxs-lookup"><span data-stu-id="02c0a-143">Since Order By utilizes the DocumentDB index for lookups, the number of request units consumed by Order By queries will be similar to the equivalent queries without Order By.</span></span> <span data-ttu-id="02c0a-144">Like any other operation on DocumentDB, the number of request units depends on the sizes/shapes of documents as well as the complexity of the query.</span><span class="sxs-lookup"><span data-stu-id="02c0a-144">Like any other operation on DocumentDB, the number of request units depends on the sizes/shapes of documents as well as the complexity of the query.</span></span> 

<span data-ttu-id="02c0a-145">**What is the expected indexing overhead for Order By?**</span><span class="sxs-lookup"><span data-stu-id="02c0a-145">**What is the expected indexing overhead for Order By?**</span></span>

<span data-ttu-id="02c0a-146">The indexing storage overhead will be proportionate to the number of properties.</span><span class="sxs-lookup"><span data-stu-id="02c0a-146">The indexing storage overhead will be proportionate to the number of properties.</span></span> <span data-ttu-id="02c0a-147">In the worst case scenario, the index overhead will be 100% of the data.</span><span class="sxs-lookup"><span data-stu-id="02c0a-147">In the worst case scenario, the index overhead will be 100% of the data.</span></span> <span data-ttu-id="02c0a-148">There is no difference in throughput (Request Units) overhead between Range/Order By indexing and the default Hash indexing.</span><span class="sxs-lookup"><span data-stu-id="02c0a-148">There is no difference in throughput (Request Units) overhead between Range/Order By indexing and the default Hash indexing.</span></span>

<span data-ttu-id="02c0a-149">**How do I query my existing data in DocumentDB using Order By?**</span><span class="sxs-lookup"><span data-stu-id="02c0a-149">**How do I query my existing data in DocumentDB using Order By?**</span></span>

<span data-ttu-id="02c0a-150">In order to sort query results using Order By, you must modify the indexing policy of the collection to use a Range index type against the property used to sort.</span><span class="sxs-lookup"><span data-stu-id="02c0a-150">In order to sort query results using Order By, you must modify the indexing policy of the collection to use a Range index type against the property used to sort.</span></span> <span data-ttu-id="02c0a-151">See [Modifying Indexing Policy](documentdb-indexing-policies.md#modifying-the-indexing-policy-of-a-collection).</span><span class="sxs-lookup"><span data-stu-id="02c0a-151">See [Modifying Indexing Policy](documentdb-indexing-policies.md#modifying-the-indexing-policy-of-a-collection).</span></span> 

<span data-ttu-id="02c0a-152">**What are the current limitations of Order By?**</span><span class="sxs-lookup"><span data-stu-id="02c0a-152">**What are the current limitations of Order By?**</span></span>

<span data-ttu-id="02c0a-153">Order By can be specified only against a property, either numeric or String when it is range indexed with the Maximum Precision (-1).</span><span class="sxs-lookup"><span data-stu-id="02c0a-153">Order By can be specified only against a property, either numeric or String when it is range indexed with the Maximum Precision (-1).</span></span>

<span data-ttu-id="02c0a-154">You cannot perform the following:</span><span class="sxs-lookup"><span data-stu-id="02c0a-154">You cannot perform the following:</span></span>

* <span data-ttu-id="02c0a-155">Order By with internal string properties like id, _rid, and _self (coming soon).</span><span class="sxs-lookup"><span data-stu-id="02c0a-155">Order By with internal string properties like id, _rid, and _self (coming soon).</span></span>
* <span data-ttu-id="02c0a-156">Order By with properties derived from the result of an intra-document join (coming soon).</span><span class="sxs-lookup"><span data-stu-id="02c0a-156">Order By with properties derived from the result of an intra-document join (coming soon).</span></span>
* <span data-ttu-id="02c0a-157">Order By multiple properties (coming soon).</span><span class="sxs-lookup"><span data-stu-id="02c0a-157">Order By multiple properties (coming soon).</span></span>
* <span data-ttu-id="02c0a-158">Order By with queries on databases, collections, users, permissions or attachments (coming soon).</span><span class="sxs-lookup"><span data-stu-id="02c0a-158">Order By with queries on databases, collections, users, permissions or attachments (coming soon).</span></span>
* <span data-ttu-id="02c0a-159">Order By with computed properties e.g. the result of an expression or a UDF/built-in function.</span><span class="sxs-lookup"><span data-stu-id="02c0a-159">Order By with computed properties e.g. the result of an expression or a UDF/built-in function.</span></span>

<span data-ttu-id="02c0a-160">Order By is not currently supported for cross-partition queries when using Query Explorer in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02c0a-160">Order By is not currently supported for cross-partition queries when using Query Explorer in the Azure portal.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="02c0a-161">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="02c0a-161">Troubleshooting</span></span>
<span data-ttu-id="02c0a-162">If you receive an error that Order By is not supported, check to ensure that you're using a version of the [SDK](documentdb-sdk-dotnet.md) that supports Order By.</span><span class="sxs-lookup"><span data-stu-id="02c0a-162">If you receive an error that Order By is not supported, check to ensure that you're using a version of the [SDK](documentdb-sdk-dotnet.md) that supports Order By.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="02c0a-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="02c0a-163">Next steps</span></span>
<span data-ttu-id="02c0a-164">Fork the [GitHub samples project](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/Queries) and start ordering your data!</span><span class="sxs-lookup"><span data-stu-id="02c0a-164">Fork the [GitHub samples project](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/Queries) and start ordering your data!</span></span> 

## <a name="references"></a><span data-ttu-id="02c0a-165">References</span><span class="sxs-lookup"><span data-stu-id="02c0a-165">References</span></span>
* [<span data-ttu-id="02c0a-166">DocumentDB Query Reference</span><span class="sxs-lookup"><span data-stu-id="02c0a-166">DocumentDB Query Reference</span></span>](documentdb-sql-query.md)
* [<span data-ttu-id="02c0a-167">DocumentDB Indexing Policy Reference</span><span class="sxs-lookup"><span data-stu-id="02c0a-167">DocumentDB Indexing Policy Reference</span></span>](documentdb-indexing-policies.md)
* [<span data-ttu-id="02c0a-168">DocumentDB SQL Reference</span><span class="sxs-lookup"><span data-stu-id="02c0a-168">DocumentDB SQL Reference</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
* [<span data-ttu-id="02c0a-169">DocumentDB Order By Samples</span><span class="sxs-lookup"><span data-stu-id="02c0a-169">DocumentDB Order By Samples</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/Queries)

