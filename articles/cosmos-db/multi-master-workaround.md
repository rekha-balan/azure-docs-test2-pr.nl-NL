---
title: Perform multi-region writes and reads by choosing the right partitioning key | Microsoft Docs
description: Learn about how to design application architectures with local reads and writes across multiple geographic regions with Azure Cosmos DB by choosing a partition key.
services: cosmos-db
author: rimman
manager: kfile
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: conceptual
ms.date: 06/6/2018
ms.author: rimman
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d38b7cd7d1f28f706e94782602926abc8fc11e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864761"
---
# <a name="perform-multi-region-writes-and-reads-by-choosing-the-right-partitioning-key"></a><span data-ttu-id="3f470-103">Perform multi-region writes and reads by choosing the right partitioning key</span><span class="sxs-lookup"><span data-stu-id="3f470-103">Perform multi-region writes and reads by choosing the right partitioning key</span></span>

<span data-ttu-id="3f470-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span><span class="sxs-lookup"><span data-stu-id="3f470-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="3f470-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span><span class="sxs-lookup"><span data-stu-id="3f470-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="3f470-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span><span class="sxs-lookup"><span data-stu-id="3f470-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="3f470-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f470-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <a id="ExampleScenario"></a><span data-ttu-id="3f470-108">Content Publishing - an example scenario</span><span class="sxs-lookup"><span data-stu-id="3f470-108">Content Publishing - an example scenario</span></span>
<span data-ttu-id="3f470-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f470-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="3f470-110">Consider a content publishing platform built on Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f470-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="3f470-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span><span class="sxs-lookup"><span data-stu-id="3f470-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="3f470-112">Both authors and subscribers are spread over the world</span><span class="sxs-lookup"><span data-stu-id="3f470-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="3f470-113">Authors must publish (write) articles to their local (closest) region</span><span class="sxs-lookup"><span data-stu-id="3f470-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="3f470-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span><span class="sxs-lookup"><span data-stu-id="3f470-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="3f470-115">Subscribers should get a notification when new articles are published.</span><span class="sxs-lookup"><span data-stu-id="3f470-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="3f470-116">Subscribers must be able to read articles from their local region.</span><span class="sxs-lookup"><span data-stu-id="3f470-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="3f470-117">They should also be able to add reviews to these articles.</span><span class="sxs-lookup"><span data-stu-id="3f470-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="3f470-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span><span class="sxs-lookup"><span data-stu-id="3f470-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="3f470-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span><span class="sxs-lookup"><span data-stu-id="3f470-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="3f470-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span><span class="sxs-lookup"><span data-stu-id="3f470-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="3f470-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span><span class="sxs-lookup"><span data-stu-id="3f470-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="3f470-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="3f470-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <a id="ModelingNotifications"></a><span data-ttu-id="3f470-123">Modeling notifications</span><span class="sxs-lookup"><span data-stu-id="3f470-123">Modeling notifications</span></span>
<span data-ttu-id="3f470-124">Notifications are data feeds specific to a user.</span><span class="sxs-lookup"><span data-stu-id="3f470-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="3f470-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span><span class="sxs-lookup"><span data-stu-id="3f470-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="3f470-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span><span class="sxs-lookup"><span data-stu-id="3f470-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="3f470-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span><span class="sxs-lookup"><span data-stu-id="3f470-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <a id="ModelingSubscriptions"></a><span data-ttu-id="3f470-128">Modeling subscriptions</span><span class="sxs-lookup"><span data-stu-id="3f470-128">Modeling subscriptions</span></span>
<span data-ttu-id="3f470-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span><span class="sxs-lookup"><span data-stu-id="3f470-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="3f470-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span><span class="sxs-lookup"><span data-stu-id="3f470-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <a id="ModelingArticles"></a><span data-ttu-id="3f470-131">Modeling articles</span><span class="sxs-lookup"><span data-stu-id="3f470-131">Modeling articles</span></span>
<span data-ttu-id="3f470-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="3f470-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="3f470-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="3f470-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <a id="ModelingReviews"></a><span data-ttu-id="3f470-134">Modeling reviews</span><span class="sxs-lookup"><span data-stu-id="3f470-134">Modeling reviews</span></span>
<span data-ttu-id="3f470-135">Like articles, reviews are mostly written and read in the context of article.</span><span class="sxs-lookup"><span data-stu-id="3f470-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="3f470-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span><span class="sxs-lookup"><span data-stu-id="3f470-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <a id="DataAccessMethods"></a><span data-ttu-id="3f470-137">Data access layer methods</span><span class="sxs-lookup"><span data-stu-id="3f470-137">Data access layer methods</span></span>
<span data-ttu-id="3f470-138">Now let's look at the main data access methods we need to implement.</span><span class="sxs-lookup"><span data-stu-id="3f470-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="3f470-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span><span class="sxs-lookup"><span data-stu-id="3f470-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a><span data-ttu-id="3f470-140">Azure Cosmos DB account configuration</span><span class="sxs-lookup"><span data-stu-id="3f470-140">Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="3f470-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span><span class="sxs-lookup"><span data-stu-id="3f470-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="3f470-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span><span class="sxs-lookup"><span data-stu-id="3f470-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="3f470-143">For example, with two regions, here's a setup for multi-region writes:</span><span class="sxs-lookup"><span data-stu-id="3f470-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="3f470-144">Account Name</span><span class="sxs-lookup"><span data-stu-id="3f470-144">Account Name</span></span> | <span data-ttu-id="3f470-145">Write Region</span><span class="sxs-lookup"><span data-stu-id="3f470-145">Write Region</span></span> | <span data-ttu-id="3f470-146">Read Region</span><span class="sxs-lookup"><span data-stu-id="3f470-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="3f470-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span><span class="sxs-lookup"><span data-stu-id="3f470-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure Cosmos DB multi-master architecture](./media/multi-master-workaround/multi-master.png)

<span data-ttu-id="3f470-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span><span class="sxs-lookup"><span data-stu-id="3f470-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="3f470-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span><span class="sxs-lookup"><span data-stu-id="3f470-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="3f470-151">Reads are performed by reading from both accounts to get the global view of data.</span><span class="sxs-lookup"><span data-stu-id="3f470-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="3f470-152">This approach can be extended to as many regions as required.</span><span class="sxs-lookup"><span data-stu-id="3f470-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="3f470-153">For example, here's a setup with three geographic regions:</span><span class="sxs-lookup"><span data-stu-id="3f470-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="3f470-154">Account Name</span><span class="sxs-lookup"><span data-stu-id="3f470-154">Account Name</span></span> | <span data-ttu-id="3f470-155">Write Region</span><span class="sxs-lookup"><span data-stu-id="3f470-155">Write Region</span></span> | <span data-ttu-id="3f470-156">Read Region 1</span><span class="sxs-lookup"><span data-stu-id="3f470-156">Read Region 1</span></span> | <span data-ttu-id="3f470-157">Read Region 2</span><span class="sxs-lookup"><span data-stu-id="3f470-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a><span data-ttu-id="3f470-158">Data access layer implementation</span><span class="sxs-lookup"><span data-stu-id="3f470-158">Data access layer implementation</span></span>
<span data-ttu-id="3f470-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span><span class="sxs-lookup"><span data-stu-id="3f470-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="3f470-160">The DAL must implement the following steps:</span><span class="sxs-lookup"><span data-stu-id="3f470-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="3f470-161">Create multiple instances of `DocumentClient` for each account.</span><span class="sxs-lookup"><span data-stu-id="3f470-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="3f470-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span><span class="sxs-lookup"><span data-stu-id="3f470-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="3f470-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span><span class="sxs-lookup"><span data-stu-id="3f470-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="3f470-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span><span class="sxs-lookup"><span data-stu-id="3f470-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="3f470-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span><span class="sxs-lookup"><span data-stu-id="3f470-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="3f470-166">With the preceding setup, the data access methods can be implemented.</span><span class="sxs-lookup"><span data-stu-id="3f470-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="3f470-167">Write operations forward the write to the corresponding `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="3f470-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="3f470-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="3f470-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="3f470-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3f470-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <a id="NextSteps"></a><span data-ttu-id="3f470-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f470-170">Next steps</span></span>
<span data-ttu-id="3f470-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span><span class="sxs-lookup"><span data-stu-id="3f470-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="3f470-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="3f470-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="3f470-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3f470-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="3f470-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="3f470-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="3f470-175">Develop with multiple regions using the [Azure Cosmos DB - SQL API](tutorial-global-distribution-sql-api.md)</span><span class="sxs-lookup"><span data-stu-id="3f470-175">Develop with multiple regions using the [Azure Cosmos DB - SQL API](tutorial-global-distribution-sql-api.md)</span></span>
* <span data-ttu-id="3f470-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="3f470-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="3f470-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="3f470-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
