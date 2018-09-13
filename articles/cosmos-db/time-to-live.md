---
title: Expire data in Azure Cosmos DB with time to live | Microsoft Docs
description: With TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the system after a period of time.
services: cosmos-db
keywords: time to live
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 08/29/2017
ms.author: sngun
ms.openlocfilehash: 2cae74224a9d59939175ac7e43d4d6b183ca3933
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967913"
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="d7685-104">Expire data in Azure Cosmos DB collections automatically with time to live</span><span class="sxs-lookup"><span data-stu-id="d7685-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="d7685-105">Applications can produce and store vast amounts of data.</span><span class="sxs-lookup"><span data-stu-id="d7685-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="d7685-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span><span class="sxs-lookup"><span data-stu-id="d7685-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="d7685-107">Once the data becomes surplus to the needs of the application, it is safe to purge this data and reduce the storage needs of an application.</span><span class="sxs-lookup"><span data-stu-id="d7685-107">Once the data becomes surplus to the needs of the application, it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="d7685-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span><span class="sxs-lookup"><span data-stu-id="d7685-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="d7685-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span><span class="sxs-lookup"><span data-stu-id="d7685-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="d7685-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span><span class="sxs-lookup"><span data-stu-id="d7685-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="d7685-111">Time to live in Azure Cosmos DB uses an offset against when the document was last modified.</span><span class="sxs-lookup"><span data-stu-id="d7685-111">Time to live in Azure Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="d7685-112">To do this it uses the `_ts` field, which exists on every document.</span><span class="sxs-lookup"><span data-stu-id="d7685-112">To do this it uses the `_ts` field, which exists on every document.</span></span> <span data-ttu-id="d7685-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span><span class="sxs-lookup"><span data-stu-id="d7685-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="d7685-114">The `_ts` field is updated every time a document is modified.</span><span class="sxs-lookup"><span data-stu-id="d7685-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="d7685-115">TTL behavior</span><span class="sxs-lookup"><span data-stu-id="d7685-115">TTL behavior</span></span>
<span data-ttu-id="d7685-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span><span class="sxs-lookup"><span data-stu-id="d7685-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="d7685-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span><span class="sxs-lookup"><span data-stu-id="d7685-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="d7685-118">DefaultTTL for the collection</span><span class="sxs-lookup"><span data-stu-id="d7685-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="d7685-119">If missing (or set to null), documents are not deleted automatically.</span><span class="sxs-lookup"><span data-stu-id="d7685-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="d7685-120">If present and the value is set to "-1" = infinite – documents don’t expire by default</span><span class="sxs-lookup"><span data-stu-id="d7685-120">If present and the value is set to "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="d7685-121">If present and the value is set to some number ("n") – documents expire "n" seconds after last modification</span><span class="sxs-lookup"><span data-stu-id="d7685-121">If present and the value is set to some number ("n") – documents expire "n" seconds after last modification</span></span>
2. <span data-ttu-id="d7685-122">TTL for the documents:</span><span class="sxs-lookup"><span data-stu-id="d7685-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="d7685-123">Property is applicable only if DefaultTTL is present for the parent collection.</span><span class="sxs-lookup"><span data-stu-id="d7685-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="d7685-124">Overrides the DefaultTTL value for the parent collection.</span><span class="sxs-lookup"><span data-stu-id="d7685-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="d7685-125">As soon as the document has expired (`ttl` + `_ts` <= current server time), the document is marked as "expired."</span><span class="sxs-lookup"><span data-stu-id="d7685-125">As soon as the document has expired (`ttl` + `_ts` <= current server time), the document is marked as "expired."</span></span> <span data-ttu-id="d7685-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span><span class="sxs-lookup"><span data-stu-id="d7685-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="d7685-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span><span class="sxs-lookup"><span data-stu-id="d7685-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="d7685-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span><span class="sxs-lookup"><span data-stu-id="d7685-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="d7685-129">The above logic can be shown in the following matrix:</span><span class="sxs-lookup"><span data-stu-id="d7685-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="d7685-130">DefaultTTL missing/not set on the collection</span><span class="sxs-lookup"><span data-stu-id="d7685-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="d7685-131">DefaultTTL = -1 on collection</span><span class="sxs-lookup"><span data-stu-id="d7685-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="d7685-132">DefaultTTL = n' on collection</span><span class="sxs-lookup"><span data-stu-id="d7685-132">DefaultTTL = n' on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="d7685-133">TTL Missing on document</span><span class="sxs-lookup"><span data-stu-id="d7685-133">TTL Missing on document</span></span> |<span data-ttu-id="d7685-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span><span class="sxs-lookup"><span data-stu-id="d7685-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="d7685-135">No documents in this collection will expire.</span><span class="sxs-lookup"><span data-stu-id="d7685-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="d7685-136">The documents in this collection will expire when interval n' elapses.</span><span class="sxs-lookup"><span data-stu-id="d7685-136">The documents in this collection will expire when interval n' elapses.</span></span> |
| <span data-ttu-id="d7685-137">TTL = -1 on document</span><span class="sxs-lookup"><span data-stu-id="d7685-137">TTL = -1 on document</span></span> |<span data-ttu-id="d7685-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span><span class="sxs-lookup"><span data-stu-id="d7685-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="d7685-139">TTL on a document is uninterpreted by the system.</span><span class="sxs-lookup"><span data-stu-id="d7685-139">TTL on a document is uninterpreted by the system.</span></span> |<span data-ttu-id="d7685-140">No documents in this collection will expire.</span><span class="sxs-lookup"><span data-stu-id="d7685-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="d7685-141">The document with TTL=-1 in this collection will never expire.</span><span class="sxs-lookup"><span data-stu-id="d7685-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="d7685-142">All other documents will expire after n' interval.</span><span class="sxs-lookup"><span data-stu-id="d7685-142">All other documents will expire after n' interval.</span></span> |
| <span data-ttu-id="d7685-143">TTL = n on document</span><span class="sxs-lookup"><span data-stu-id="d7685-143">TTL = n on document</span></span> |<span data-ttu-id="d7685-144">Nothing to override at the document level.</span><span class="sxs-lookup"><span data-stu-id="d7685-144">Nothing to override at the document level.</span></span> <span data-ttu-id="d7685-145">TTL on a document is uninterpreted by the system.</span><span class="sxs-lookup"><span data-stu-id="d7685-145">TTL on a document is uninterpreted by the system.</span></span> |<span data-ttu-id="d7685-146">The document with TTL = n will expire after interval n, in seconds.</span><span class="sxs-lookup"><span data-stu-id="d7685-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="d7685-147">Other documents will inherit interval of -1 and never expire.</span><span class="sxs-lookup"><span data-stu-id="d7685-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="d7685-148">The document with TTL = n will expire after interval n, in seconds.</span><span class="sxs-lookup"><span data-stu-id="d7685-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="d7685-149">Other documents will inherit n' interval from the collection.</span><span class="sxs-lookup"><span data-stu-id="d7685-149">Other documents will inherit n' interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="d7685-150">Configuring TTL</span><span class="sxs-lookup"><span data-stu-id="d7685-150">Configuring TTL</span></span>
<span data-ttu-id="d7685-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span><span class="sxs-lookup"><span data-stu-id="d7685-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span> <span data-ttu-id="d7685-152">TTL can be set programmatically or by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7685-152">TTL can be set programmatically or by using the Azure portal.</span></span> <span data-ttu-id="d7685-153">Use the following steps to configure TTL from Azure portal:</span><span class="sxs-lookup"><span data-stu-id="d7685-153">Use the following steps to configure TTL from Azure portal:</span></span>

1. <span data-ttu-id="d7685-154">Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d7685-154">Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your Azure Cosmos DB account.</span></span>  

2. <span data-ttu-id="d7685-155">Navigate to the collection you want to set the TTL value, Open the **Scale & Settings** pane.</span><span class="sxs-lookup"><span data-stu-id="d7685-155">Navigate to the collection you want to set the TTL value, Open the **Scale & Settings** pane.</span></span> <span data-ttu-id="d7685-156">You can see that the Time to Live is by default set to **off**.</span><span class="sxs-lookup"><span data-stu-id="d7685-156">You can see that the Time to Live is by default set to **off**.</span></span> <span data-ttu-id="d7685-157">You can change it to **on (no default)** or **on**.</span><span class="sxs-lookup"><span data-stu-id="d7685-157">You can change it to **on (no default)** or **on**.</span></span>

   <span data-ttu-id="d7685-158">**off** - Documents are not deleted automatically.</span><span class="sxs-lookup"><span data-stu-id="d7685-158">**off** - Documents are not deleted automatically.</span></span>  
   <span data-ttu-id="d7685-159">**on (no default)** - This option sets the TTL value to "-1" (infinite) which means documents don’t expire by default.</span><span class="sxs-lookup"><span data-stu-id="d7685-159">**on (no default)** - This option sets the TTL value to "-1" (infinite) which means documents don’t expire by default.</span></span>  
   <span data-ttu-id="d7685-160">**on** - Documents expire "n" seconds after last modification.</span><span class="sxs-lookup"><span data-stu-id="d7685-160">**on** - Documents expire "n" seconds after last modification.</span></span>  

   ![Set time to live](./media/time-to-live/set-ttl-in-portal.png)

## <a name="enabling-ttl"></a><span data-ttu-id="d7685-162">Enabling TTL</span><span class="sxs-lookup"><span data-stu-id="d7685-162">Enabling TTL</span></span>
<span data-ttu-id="d7685-163">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span><span class="sxs-lookup"><span data-stu-id="d7685-163">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="d7685-164">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span><span class="sxs-lookup"><span data-stu-id="d7685-164">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="d7685-165">Configuring default TTL on a collection</span><span class="sxs-lookup"><span data-stu-id="d7685-165">Configuring default TTL on a collection</span></span>
<span data-ttu-id="d7685-166">You are able to configure a default time to live at a collection level.</span><span class="sxs-lookup"><span data-stu-id="d7685-166">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="d7685-167">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="d7685-167">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="d7685-168">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span><span class="sxs-lookup"><span data-stu-id="d7685-168">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="d7685-169">Setting TTL on a document</span><span class="sxs-lookup"><span data-stu-id="d7685-169">Setting TTL on a document</span></span>
<span data-ttu-id="d7685-170">In addition to setting a default TTL on a collection, you can set specific TTL at a document level.</span><span class="sxs-lookup"><span data-stu-id="d7685-170">In addition to setting a default TTL on a collection, you can set specific TTL at a document level.</span></span> <span data-ttu-id="d7685-171">Doing this will override the default of the collection.</span><span class="sxs-lookup"><span data-stu-id="d7685-171">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="d7685-172">To set the TTL on a document, you need to provide a non-zero positive number, which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="d7685-172">To set the TTL on a document, you need to provide a non-zero positive number, which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="d7685-173">If a document has no TTL field, then the default of the collection will apply.</span><span class="sxs-lookup"><span data-stu-id="d7685-173">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="d7685-174">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span><span class="sxs-lookup"><span data-stu-id="d7685-174">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="d7685-175">Here's a snippet showing how to set the TTL expiration on a document:</span><span class="sxs-lookup"><span data-stu-id="d7685-175">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="d7685-176">Extending TTL on an existing document</span><span class="sxs-lookup"><span data-stu-id="d7685-176">Extending TTL on an existing document</span></span>
<span data-ttu-id="d7685-177">You can reset the TTL on a document by doing any write operation on the document.</span><span class="sxs-lookup"><span data-stu-id="d7685-177">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="d7685-178">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span><span class="sxs-lookup"><span data-stu-id="d7685-178">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="d7685-179">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span><span class="sxs-lookup"><span data-stu-id="d7685-179">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(readDocument);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="d7685-180">Removing TTL from a document</span><span class="sxs-lookup"><span data-stu-id="d7685-180">Removing TTL from a document</span></span>
<span data-ttu-id="d7685-181">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span><span class="sxs-lookup"><span data-stu-id="d7685-181">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="d7685-182">When the TTL field is removed from the document, the default of the collection will be applied.</span><span class="sxs-lookup"><span data-stu-id="d7685-182">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="d7685-183">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span><span class="sxs-lookup"><span data-stu-id="d7685-183">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(readDocument);

## <a name="disabling-ttl"></a><span data-ttu-id="d7685-184">Disabling TTL</span><span class="sxs-lookup"><span data-stu-id="d7685-184">Disabling TTL</span></span>
<span data-ttu-id="d7685-185">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span><span class="sxs-lookup"><span data-stu-id="d7685-185">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="d7685-186">Deleting this property is different from setting it to -1.</span><span class="sxs-lookup"><span data-stu-id="d7685-186">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="d7685-187">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span><span class="sxs-lookup"><span data-stu-id="d7685-187">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="d7685-188">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span><span class="sxs-lookup"><span data-stu-id="d7685-188">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);

<a id="ttl-and-index-interaction"></a> 
## <a name="ttl-and-index-interaction"></a><span data-ttu-id="d7685-189">TTL and index interaction</span><span class="sxs-lookup"><span data-stu-id="d7685-189">TTL and index interaction</span></span>
<span data-ttu-id="d7685-190">Adding or changing the TTL setting on a collection changes the underlying index.</span><span class="sxs-lookup"><span data-stu-id="d7685-190">Adding or changing the TTL setting on a collection changes the underlying index.</span></span> <span data-ttu-id="d7685-191">When the TTL value is changed from Off to On, the collection is reindexed.</span><span class="sxs-lookup"><span data-stu-id="d7685-191">When the TTL value is changed from Off to On, the collection is reindexed.</span></span> <span data-ttu-id="d7685-192">When making changes to the indexing policy when the indexing mode is consistent, users will not notice a change to the index.</span><span class="sxs-lookup"><span data-stu-id="d7685-192">When making changes to the indexing policy when the indexing mode is consistent, users will not notice a change to the index.</span></span> <span data-ttu-id="d7685-193">When the indexing mode is set to lazy, the index is always catching up and if the TTL value is changed, the index is recreated from scratch.</span><span class="sxs-lookup"><span data-stu-id="d7685-193">When the indexing mode is set to lazy, the index is always catching up and if the TTL value is changed, the index is recreated from scratch.</span></span> <span data-ttu-id="d7685-194">When the TTL value is changed and the index mode is set to lazy, queries done during the index rebuild do not return complete or correct results.</span><span class="sxs-lookup"><span data-stu-id="d7685-194">When the TTL value is changed and the index mode is set to lazy, queries done during the index rebuild do not return complete or correct results.</span></span>

<span data-ttu-id="d7685-195">If you need exact data returned, do not change the TTL value when the indexing mode is set to lazy.</span><span class="sxs-lookup"><span data-stu-id="d7685-195">If you need exact data returned, do not change the TTL value when the indexing mode is set to lazy.</span></span> <span data-ttu-id="d7685-196">Ideally consistent index should be chosen to ensure consistent query results.</span><span class="sxs-lookup"><span data-stu-id="d7685-196">Ideally consistent index should be chosen to ensure consistent query results.</span></span> 

## <a name="faq"></a><span data-ttu-id="d7685-197">FAQ</span><span class="sxs-lookup"><span data-stu-id="d7685-197">FAQ</span></span>
<span data-ttu-id="d7685-198">**What will TTL cost me?**</span><span class="sxs-lookup"><span data-stu-id="d7685-198">**What will TTL cost me?**</span></span>

<span data-ttu-id="d7685-199">There is no additional cost to setting a TTL on a document.</span><span class="sxs-lookup"><span data-stu-id="d7685-199">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="d7685-200">**How long will it take to delete my document once the TTL is up?**</span><span class="sxs-lookup"><span data-stu-id="d7685-200">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="d7685-201">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span><span class="sxs-lookup"><span data-stu-id="d7685-201">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="d7685-202">**Will TTL on a document have any impact on RU charges?**</span><span class="sxs-lookup"><span data-stu-id="d7685-202">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="d7685-203">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d7685-203">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="d7685-204">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span><span class="sxs-lookup"><span data-stu-id="d7685-204">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="d7685-205">TTL applies to the entire document.</span><span class="sxs-lookup"><span data-stu-id="d7685-205">TTL applies to the entire document.</span></span> <span data-ttu-id="d7685-206">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document into a separate "linked" document and then use TTL on that extracted document.</span><span class="sxs-lookup"><span data-stu-id="d7685-206">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document into a separate "linked" document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="d7685-207">**Does the TTL feature have any specific indexing requirements?**</span><span class="sxs-lookup"><span data-stu-id="d7685-207">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="d7685-208">Yes.</span><span class="sxs-lookup"><span data-stu-id="d7685-208">Yes.</span></span> <span data-ttu-id="d7685-209">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span><span class="sxs-lookup"><span data-stu-id="d7685-209">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="d7685-210">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span><span class="sxs-lookup"><span data-stu-id="d7685-210">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7685-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7685-211">Next steps</span></span>
<span data-ttu-id="d7685-212">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span><span class="sxs-lookup"><span data-stu-id="d7685-212">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

