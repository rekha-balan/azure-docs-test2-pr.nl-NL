---
title: Expire data in DocumentDB with time to live | Microsoft Docs
description: With TTL, Microsoft Azure DocumentDB provides the ability to have documents automatically purged from the system after a period of time.
services: documentdb
documentationcenter: ''
keywords: time to live
author: arramac
manager: jhubbard
editor: ''
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: documentdb
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: arramac
ms.openlocfilehash: c97ebc7164f92371fd2f7de0ffa97f929682ef58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661223"
---
# <a name="expire-data-in-documentdb-collections-automatically-with-time-to-live"></a><span data-ttu-id="710cb-104">Expire data in DocumentDB collections automatically with time to live</span><span class="sxs-lookup"><span data-stu-id="710cb-104">Expire data in DocumentDB collections automatically with time to live</span></span>
<span data-ttu-id="710cb-105">Applications can produce and store vast amounts of data.</span><span class="sxs-lookup"><span data-stu-id="710cb-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="710cb-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span><span class="sxs-lookup"><span data-stu-id="710cb-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="710cb-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span><span class="sxs-lookup"><span data-stu-id="710cb-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="710cb-108">With "time to live" or TTL, Microsoft Azure DocumentDB provides the ability to have documents automatically purged from the database after a period of time.</span><span class="sxs-lookup"><span data-stu-id="710cb-108">With "time to live" or TTL, Microsoft Azure DocumentDB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="710cb-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span><span class="sxs-lookup"><span data-stu-id="710cb-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="710cb-110">Once TTL is set, either as a collection default or at a document level, DocumentDB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span><span class="sxs-lookup"><span data-stu-id="710cb-110">Once TTL is set, either as a collection default or at a document level, DocumentDB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="710cb-111">Time to live in DocumentDB uses an offset against when the document was last modified.</span><span class="sxs-lookup"><span data-stu-id="710cb-111">Time to live in DocumentDB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="710cb-112">To do this it uses the `_ts` field which exists on every document.</span><span class="sxs-lookup"><span data-stu-id="710cb-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="710cb-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span><span class="sxs-lookup"><span data-stu-id="710cb-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="710cb-114">The `_ts` field is updated every time a document is modified.</span><span class="sxs-lookup"><span data-stu-id="710cb-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="710cb-115">TTL behavior</span><span class="sxs-lookup"><span data-stu-id="710cb-115">TTL behavior</span></span>
<span data-ttu-id="710cb-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span><span class="sxs-lookup"><span data-stu-id="710cb-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="710cb-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span><span class="sxs-lookup"><span data-stu-id="710cb-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="710cb-118">DefaultTTL for the collection</span><span class="sxs-lookup"><span data-stu-id="710cb-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="710cb-119">If missing (or set to null), documents are not deleted automatically.</span><span class="sxs-lookup"><span data-stu-id="710cb-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="710cb-120">If present and the value is "-1" = infinite – documents don’t expire by default</span><span class="sxs-lookup"><span data-stu-id="710cb-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="710cb-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span><span class="sxs-lookup"><span data-stu-id="710cb-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="710cb-122">TTL for the documents:</span><span class="sxs-lookup"><span data-stu-id="710cb-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="710cb-123">Property is applicable only if DefaultTTL is present for the parent collection.</span><span class="sxs-lookup"><span data-stu-id="710cb-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="710cb-124">Overrides the DefaultTTL value for the parent collection.</span><span class="sxs-lookup"><span data-stu-id="710cb-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="710cb-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span><span class="sxs-lookup"><span data-stu-id="710cb-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="710cb-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span><span class="sxs-lookup"><span data-stu-id="710cb-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="710cb-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span><span class="sxs-lookup"><span data-stu-id="710cb-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="710cb-128">This does not consume any [Request Units (RUs)](documentdb-request-units.md) from the collection budget.</span><span class="sxs-lookup"><span data-stu-id="710cb-128">This does not consume any [Request Units (RUs)](documentdb-request-units.md) from the collection budget.</span></span>

<span data-ttu-id="710cb-129">The above logic can be shown in the following matrix:</span><span class="sxs-lookup"><span data-stu-id="710cb-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="710cb-130">DefaultTTL missing/not set on the collection</span><span class="sxs-lookup"><span data-stu-id="710cb-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="710cb-131">DefaultTTL = -1 on collection</span><span class="sxs-lookup"><span data-stu-id="710cb-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="710cb-132">DefaultTTL = "n" on collection</span><span class="sxs-lookup"><span data-stu-id="710cb-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="710cb-133">TTL Missing on document</span><span class="sxs-lookup"><span data-stu-id="710cb-133">TTL Missing on document</span></span> |<span data-ttu-id="710cb-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span><span class="sxs-lookup"><span data-stu-id="710cb-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="710cb-135">No documents in this collection will expire.</span><span class="sxs-lookup"><span data-stu-id="710cb-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="710cb-136">The documents in this collection will expire when interval n elapses.</span><span class="sxs-lookup"><span data-stu-id="710cb-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="710cb-137">TTL = -1 on document</span><span class="sxs-lookup"><span data-stu-id="710cb-137">TTL = -1 on document</span></span> |<span data-ttu-id="710cb-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span><span class="sxs-lookup"><span data-stu-id="710cb-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="710cb-139">TTL on a document is un-interpreted by the system.</span><span class="sxs-lookup"><span data-stu-id="710cb-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="710cb-140">No documents in this collection will expire.</span><span class="sxs-lookup"><span data-stu-id="710cb-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="710cb-141">The document with TTL=-1 in this collection will never expire.</span><span class="sxs-lookup"><span data-stu-id="710cb-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="710cb-142">All other documents will expire after "n" interval.</span><span class="sxs-lookup"><span data-stu-id="710cb-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="710cb-143">TTL = n on document</span><span class="sxs-lookup"><span data-stu-id="710cb-143">TTL = n on document</span></span> |<span data-ttu-id="710cb-144">Nothing to override at the document level.</span><span class="sxs-lookup"><span data-stu-id="710cb-144">Nothing to override at the document level.</span></span> <span data-ttu-id="710cb-145">TTL on a document in un-interpreted by the system.</span><span class="sxs-lookup"><span data-stu-id="710cb-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="710cb-146">The document with TTL = n will expire after interval n, in seconds.</span><span class="sxs-lookup"><span data-stu-id="710cb-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="710cb-147">Other documents will inherit interval of -1 and never expire.</span><span class="sxs-lookup"><span data-stu-id="710cb-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="710cb-148">The document with TTL = n will expire after interval n, in seconds.</span><span class="sxs-lookup"><span data-stu-id="710cb-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="710cb-149">Other documents will inherit "n" interval from the collection.</span><span class="sxs-lookup"><span data-stu-id="710cb-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="710cb-150">Configuring TTL</span><span class="sxs-lookup"><span data-stu-id="710cb-150">Configuring TTL</span></span>
<span data-ttu-id="710cb-151">By default, time to live is disabled by default in all DocumentDB collections and on all documents.</span><span class="sxs-lookup"><span data-stu-id="710cb-151">By default, time to live is disabled by default in all DocumentDB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="710cb-152">Enabling TTL</span><span class="sxs-lookup"><span data-stu-id="710cb-152">Enabling TTL</span></span>
<span data-ttu-id="710cb-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span><span class="sxs-lookup"><span data-stu-id="710cb-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="710cb-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the DocumentDB service should monitor this collection for documents that have overridden this default.</span><span class="sxs-lookup"><span data-stu-id="710cb-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the DocumentDB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="710cb-155">Configuring default TTL on a collection</span><span class="sxs-lookup"><span data-stu-id="710cb-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="710cb-156">You are able to configure a default time to live at a collection level.</span><span class="sxs-lookup"><span data-stu-id="710cb-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="710cb-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="710cb-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="710cb-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span><span class="sxs-lookup"><span data-stu-id="710cb-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="710cb-159">Setting TTL on a document</span><span class="sxs-lookup"><span data-stu-id="710cb-159">Setting TTL on a document</span></span>
<span data-ttu-id="710cb-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span><span class="sxs-lookup"><span data-stu-id="710cb-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="710cb-161">Doing this will override the default of the collection.</span><span class="sxs-lookup"><span data-stu-id="710cb-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="710cb-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="710cb-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="710cb-163">If a document has no TTL field, then the default of the collection will apply.</span><span class="sxs-lookup"><span data-stu-id="710cb-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="710cb-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span><span class="sxs-lookup"><span data-stu-id="710cb-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="710cb-165">Here's a snippet showing how to set the TTL expiration on a document:</span><span class="sxs-lookup"><span data-stu-id="710cb-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

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


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="710cb-166">Extending TTL on an existing document</span><span class="sxs-lookup"><span data-stu-id="710cb-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="710cb-167">You can reset the TTL on a document by doing any write operation on the document.</span><span class="sxs-lookup"><span data-stu-id="710cb-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="710cb-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span><span class="sxs-lookup"><span data-stu-id="710cb-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="710cb-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span><span class="sxs-lookup"><span data-stu-id="710cb-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="710cb-170">Removing TTL from a document</span><span class="sxs-lookup"><span data-stu-id="710cb-170">Removing TTL from a document</span></span>
<span data-ttu-id="710cb-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span><span class="sxs-lookup"><span data-stu-id="710cb-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="710cb-172">When the TTL field is removed from the document, the default of the collection will be applied.</span><span class="sxs-lookup"><span data-stu-id="710cb-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="710cb-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span><span class="sxs-lookup"><span data-stu-id="710cb-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="710cb-174">Disabling TTL</span><span class="sxs-lookup"><span data-stu-id="710cb-174">Disabling TTL</span></span>
<span data-ttu-id="710cb-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span><span class="sxs-lookup"><span data-stu-id="710cb-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="710cb-176">Deleting this property is different from setting it to -1.</span><span class="sxs-lookup"><span data-stu-id="710cb-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="710cb-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span><span class="sxs-lookup"><span data-stu-id="710cb-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="710cb-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span><span class="sxs-lookup"><span data-stu-id="710cb-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="710cb-179">FAQ</span><span class="sxs-lookup"><span data-stu-id="710cb-179">FAQ</span></span>
<span data-ttu-id="710cb-180">**What will TTL cost me?**</span><span class="sxs-lookup"><span data-stu-id="710cb-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="710cb-181">There is no additional cost to setting a TTL on a document.</span><span class="sxs-lookup"><span data-stu-id="710cb-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="710cb-182">**How long will it take to delete my document once the TTL is up?**</span><span class="sxs-lookup"><span data-stu-id="710cb-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="710cb-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span><span class="sxs-lookup"><span data-stu-id="710cb-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="710cb-184">**Will TTL on a document have any impact on RU charges?**</span><span class="sxs-lookup"><span data-stu-id="710cb-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="710cb-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="710cb-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in DocumentDB.</span></span>

<span data-ttu-id="710cb-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span><span class="sxs-lookup"><span data-stu-id="710cb-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="710cb-187">TTL applies to the entire document.</span><span class="sxs-lookup"><span data-stu-id="710cb-187">TTL applies to the entire document.</span></span> <span data-ttu-id="710cb-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span><span class="sxs-lookup"><span data-stu-id="710cb-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="710cb-189">**Does the TTL feature have any specific indexing requirements?**</span><span class="sxs-lookup"><span data-stu-id="710cb-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="710cb-190">Yes.</span><span class="sxs-lookup"><span data-stu-id="710cb-190">Yes.</span></span> <span data-ttu-id="710cb-191">The collection must have [indexing policy set](documentdb-indexing-policies.md) to either Consistent or Lazy.</span><span class="sxs-lookup"><span data-stu-id="710cb-191">The collection must have [indexing policy set](documentdb-indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="710cb-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span><span class="sxs-lookup"><span data-stu-id="710cb-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="710cb-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="710cb-193">Next steps</span></span>
<span data-ttu-id="710cb-194">To learn more about Azure DocumentDB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/documentdb/) page.</span><span class="sxs-lookup"><span data-stu-id="710cb-194">To learn more about Azure DocumentDB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/documentdb/) page.</span></span>

