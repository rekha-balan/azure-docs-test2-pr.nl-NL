---
title: Regional failover in Azure Cosmos DB | Microsoft Docs
description: Learn about how manual and automatic failover works with Azure Cosmos DB.
services: cosmos-db
author: kanshiG
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 03/27/2018
ms.author: govindk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 697be3a1eb07b2f2650f3dd94fd835b9431aec6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870105"
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a><span data-ttu-id="d1850-103">Automatic regional failover for business continuity in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d1850-103">Automatic regional failover for business continuity in Azure Cosmos DB</span></span>
<span data-ttu-id="d1850-104">Azure Cosmos DB simplifies the global distribution of data by offering fully managed, [multi-region database accounts](distribute-data-globally.md) that provide clear tradeoffs between consistency, availability, and performance, all with corresponding guarantees.</span><span class="sxs-lookup"><span data-stu-id="d1850-104">Azure Cosmos DB simplifies the global distribution of data by offering fully managed, [multi-region database accounts](distribute-data-globally.md) that provide clear tradeoffs between consistency, availability, and performance, all with corresponding guarantees.</span></span> <span data-ttu-id="d1850-105">Cosmos DB accounts offer high availability, single digit ms latencies, [well-defined consistency levels](consistency-levels.md), transparent regional failover with multi-homing APIs, and the ability to elastically scale throughput and storage across the globe.</span><span class="sxs-lookup"><span data-stu-id="d1850-105">Cosmos DB accounts offer high availability, single digit ms latencies, [well-defined consistency levels](consistency-levels.md), transparent regional failover with multi-homing APIs, and the ability to elastically scale throughput and storage across the globe.</span></span> 

<span data-ttu-id="d1850-106">Cosmos DB supports both explicit and policy driven failovers that allow you to control the end-to-end system behavior in the event of failures.</span><span class="sxs-lookup"><span data-stu-id="d1850-106">Cosmos DB supports both explicit and policy driven failovers that allow you to control the end-to-end system behavior in the event of failures.</span></span> <span data-ttu-id="d1850-107">In this article, we look at:</span><span class="sxs-lookup"><span data-stu-id="d1850-107">In this article, we look at:</span></span>

* <span data-ttu-id="d1850-108">How do manual failovers work in Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d1850-108">How do manual failovers work in Cosmos DB?</span></span>
* <span data-ttu-id="d1850-109">How do automatic failovers work in Cosmos DB and what happens when a data center goes down?</span><span class="sxs-lookup"><span data-stu-id="d1850-109">How do automatic failovers work in Cosmos DB and what happens when a data center goes down?</span></span>
* <span data-ttu-id="d1850-110">How can you use manual failovers in application architectures?</span><span class="sxs-lookup"><span data-stu-id="d1850-110">How can you use manual failovers in application architectures?</span></span>

<span data-ttu-id="d1850-111">You can also learn about regional failovers in this video by Azure Cosmos DB Program Manager Andrew Liu, which demonstrates the global distribution features including regional failover.</span><span class="sxs-lookup"><span data-stu-id="d1850-111">You can also learn about regional failovers in this video by Azure Cosmos DB Program Manager Andrew Liu, which demonstrates the global distribution features including regional failover.</span></span>

>[!VIDEO https://www.youtube.com/embed/1D06yjTVxt8]
>

## <a id="ConfigureMultiRegionApplications"></a><span data-ttu-id="d1850-112">Configuring multi-region applications</span><span class="sxs-lookup"><span data-stu-id="d1850-112">Configuring multi-region applications</span></span>
<span data-ttu-id="d1850-113">Before we dive into failover modes, we look at how you can configure an application to take advantage of multi-region availability and be resilient in the face of regional failovers.</span><span class="sxs-lookup"><span data-stu-id="d1850-113">Before we dive into failover modes, we look at how you can configure an application to take advantage of multi-region availability and be resilient in the face of regional failovers.</span></span>

* <span data-ttu-id="d1850-114">First, deploy your application in multiple regions</span><span class="sxs-lookup"><span data-stu-id="d1850-114">First, deploy your application in multiple regions</span></span>
* <span data-ttu-id="d1850-115">To ensure low latency access from every region your application is deployed, configure the corresponding [preferred regions list](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) for each region via one of the supported SDKs.</span><span class="sxs-lookup"><span data-stu-id="d1850-115">To ensure low latency access from every region your application is deployed, configure the corresponding [preferred regions list](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) for each region via one of the supported SDKs.</span></span>

<span data-ttu-id="d1850-116">The following snippet shows how to initialize a multi-region application.</span><span class="sxs-lookup"><span data-stu-id="d1850-116">The following snippet shows how to initialize a multi-region application.</span></span> <span data-ttu-id="d1850-117">Here, the Azure Cosmos DB account `contoso.documents.azure.com` is configured with two regions - West US and North Europe.</span><span class="sxs-lookup"><span data-stu-id="d1850-117">Here, the Azure Cosmos DB account `contoso.documents.azure.com` is configured with two regions - West US and North Europe.</span></span> 

* <span data-ttu-id="d1850-118">The application is deployed in the West US region (using Azure App Services for example)</span><span class="sxs-lookup"><span data-stu-id="d1850-118">The application is deployed in the West US region (using Azure App Services for example)</span></span> 
* <span data-ttu-id="d1850-119">Configured with `West US` as the first preferred region for low latency reads</span><span class="sxs-lookup"><span data-stu-id="d1850-119">Configured with `West US` as the first preferred region for low latency reads</span></span>
* <span data-ttu-id="d1850-120">Configured with `North Europe` as the second preferred region (for high availability during regional failures)</span><span class="sxs-lookup"><span data-stu-id="d1850-120">Configured with `North Europe` as the second preferred region (for high availability during regional failures)</span></span>

<span data-ttu-id="d1850-121">In the SQL API, this configuration looks like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="d1850-121">In the SQL API, this configuration looks like the following snippet:</span></span>

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "<Fill your Cosmos DB account's AuthorizationKey>",
    usConnectionPolicy);
```

<span data-ttu-id="d1850-122">The application is also deployed in the North Europe region with the order of preferred regions reversed.</span><span class="sxs-lookup"><span data-stu-id="d1850-122">The application is also deployed in the North Europe region with the order of preferred regions reversed.</span></span> <span data-ttu-id="d1850-123">That is, the North Europe region is specified first for low latency reads.</span><span class="sxs-lookup"><span data-stu-id="d1850-123">That is, the North Europe region is specified first for low latency reads.</span></span> <span data-ttu-id="d1850-124">Then, the West US region is specified as the second preferred region for high availability during regional failures.</span><span class="sxs-lookup"><span data-stu-id="d1850-124">Then, the West US region is specified as the second preferred region for high availability during regional failures.</span></span>

<span data-ttu-id="d1850-125">The following architecture diagram shows a multi-region application deployment where Cosmos DB and the application are configured to be available in four Azure geographic regions.</span><span class="sxs-lookup"><span data-stu-id="d1850-125">The following architecture diagram shows a multi-region application deployment where Cosmos DB and the application are configured to be available in four Azure geographic regions.</span></span>  

![Globally distributed application deployment with Azure Cosmos DB](./media/regional-failover/app-deployment.png)

<span data-ttu-id="d1850-127">Now, let's look at how the Cosmos DB service handles regional failures via automatic failovers.</span><span class="sxs-lookup"><span data-stu-id="d1850-127">Now, let's look at how the Cosmos DB service handles regional failures via automatic failovers.</span></span> 

## <a id="AutomaticFailovers"></a><span data-ttu-id="d1850-128">Automatic Failovers</span><span class="sxs-lookup"><span data-stu-id="d1850-128">Automatic Failovers</span></span>
<span data-ttu-id="d1850-129">In the rare event of an Azure regional outage or data center outage, Cosmos DB automatically triggers failovers of all Cosmos DB accounts with a presence in the affected region.</span><span class="sxs-lookup"><span data-stu-id="d1850-129">In the rare event of an Azure regional outage or data center outage, Cosmos DB automatically triggers failovers of all Cosmos DB accounts with a presence in the affected region.</span></span> 

<span data-ttu-id="d1850-130">**What happens if a read region has an outage?**</span><span class="sxs-lookup"><span data-stu-id="d1850-130">**What happens if a read region has an outage?**</span></span>

<span data-ttu-id="d1850-131">Cosmos DB accounts with a read region in one of the affected regions are automatically disconnected from their write region and marked offline.</span><span class="sxs-lookup"><span data-stu-id="d1850-131">Cosmos DB accounts with a read region in one of the affected regions are automatically disconnected from their write region and marked offline.</span></span> <span data-ttu-id="d1850-132">The Cosmos DB SDKs implement a regional discovery protocol that allows them to automatically detect when a region is available and redirect read calls to the next available region in the preferred region list.</span><span class="sxs-lookup"><span data-stu-id="d1850-132">The Cosmos DB SDKs implement a regional discovery protocol that allows them to automatically detect when a region is available and redirect read calls to the next available region in the preferred region list.</span></span> <span data-ttu-id="d1850-133">If none of the regions in the preferred region list is available, calls automatically fall back to the current write region.</span><span class="sxs-lookup"><span data-stu-id="d1850-133">If none of the regions in the preferred region list is available, calls automatically fall back to the current write region.</span></span> <span data-ttu-id="d1850-134">No changes are required in your application code to handle regional failovers.</span><span class="sxs-lookup"><span data-stu-id="d1850-134">No changes are required in your application code to handle regional failovers.</span></span> <span data-ttu-id="d1850-135">During this entire process, consistency guarantees continue to be honored by Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d1850-135">During this entire process, consistency guarantees continue to be honored by Cosmos DB.</span></span>

![Read region failures in Azure Cosmos DB](./media/regional-failover/read-region-failures.png)

<span data-ttu-id="d1850-137">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span><span class="sxs-lookup"><span data-stu-id="d1850-137">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span></span> <span data-ttu-id="d1850-138">Cosmos DB accounts that had a read region in the affected region will then automatically sync with current write region and turn online.</span><span class="sxs-lookup"><span data-stu-id="d1850-138">Cosmos DB accounts that had a read region in the affected region will then automatically sync with current write region and turn online.</span></span> <span data-ttu-id="d1850-139">The Cosmos DB SDKs discover the availability of the new region and evaluate whether the region should be selected as the current read region based on the preferred region list configured by the application.</span><span class="sxs-lookup"><span data-stu-id="d1850-139">The Cosmos DB SDKs discover the availability of the new region and evaluate whether the region should be selected as the current read region based on the preferred region list configured by the application.</span></span> <span data-ttu-id="d1850-140">Subsequent reads are redirected to the recovered region without requiring any changes to your application code.</span><span class="sxs-lookup"><span data-stu-id="d1850-140">Subsequent reads are redirected to the recovered region without requiring any changes to your application code.</span></span>

<span data-ttu-id="d1850-141">**What happens if a write region has an outage?**</span><span class="sxs-lookup"><span data-stu-id="d1850-141">**What happens if a write region has an outage?**</span></span>

<span data-ttu-id="d1850-142">If the affected region is the current write region and automatic failover is enabled for the Azure Cosmos DB account, then the region is automatically marked as offline.</span><span class="sxs-lookup"><span data-stu-id="d1850-142">If the affected region is the current write region and automatic failover is enabled for the Azure Cosmos DB account, then the region is automatically marked as offline.</span></span> <span data-ttu-id="d1850-143">Then, an alternative region is promoted as the write region for the affected Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d1850-143">Then, an alternative region is promoted as the write region for the affected Azure Cosmos DB account.</span></span> <span data-ttu-id="d1850-144">You can enable automatic failover and fully control the region selection order for your Azure Cosmos DB accounts via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange).</span><span class="sxs-lookup"><span data-stu-id="d1850-144">You can enable automatic failover and fully control the region selection order for your Azure Cosmos DB accounts via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange).</span></span> 

![Failover priorities for Azure Cosmos DB](./media/regional-failover/failover-priorities.png)

<span data-ttu-id="d1850-146">During automatic failovers, Azure Cosmos DB automatically chooses the next write region for a given Azure Cosmos DB account based on the specified priority order.</span><span class="sxs-lookup"><span data-stu-id="d1850-146">During automatic failovers, Azure Cosmos DB automatically chooses the next write region for a given Azure Cosmos DB account based on the specified priority order.</span></span> <span data-ttu-id="d1850-147">Applications can use the WriteEndpoint property of DocumentClient class to detect the change in write region.</span><span class="sxs-lookup"><span data-stu-id="d1850-147">Applications can use the WriteEndpoint property of DocumentClient class to detect the change in write region.</span></span>

![Write region failures in Azure Cosmos DB](./media/regional-failover/write-region-failures.png)

<span data-ttu-id="d1850-149">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span><span class="sxs-lookup"><span data-stu-id="d1850-149">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span></span> 

* <span data-ttu-id="d1850-150">Data present in the previous write region that was not replicated to read regions during the outage is published as a conflict feed.</span><span class="sxs-lookup"><span data-stu-id="d1850-150">Data present in the previous write region that was not replicated to read regions during the outage is published as a conflict feed.</span></span> <span data-ttu-id="d1850-151">Applications can read the conflict feed, resolve the conflicts based on application specific logic, and write the updated data back to the Azure Cosmos DB account as appropriate.</span><span class="sxs-lookup"><span data-stu-id="d1850-151">Applications can read the conflict feed, resolve the conflicts based on application specific logic, and write the updated data back to the Azure Cosmos DB account as appropriate.</span></span> 
* <span data-ttu-id="d1850-152">The previous write region is recreated as a read region and brought back online automatically.</span><span class="sxs-lookup"><span data-stu-id="d1850-152">The previous write region is recreated as a read region and brought back online automatically.</span></span> 
* <span data-ttu-id="d1850-153">You can reconfigure read region that was brought back online automatically as the write region by performing a manual failover via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="d1850-153">You can reconfigure read region that was brought back online automatically as the write region by performing a manual failover via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span>

<span data-ttu-id="d1850-154">The following code snippet illustrates how to process conflicts after the affected region recovers from the outage.</span><span class="sxs-lookup"><span data-stu-id="d1850-154">The following code snippet illustrates how to process conflicts after the affected region recovers from the outage.</span></span>

```cs
string conflictsFeedContinuationToken = null;
do
{
    FeedResponse<Conflict> conflictsFeed = client.ReadConflictFeedAsync(collectionLink,
        new FeedOptions { RequestContinuation = conflictsFeedContinuationToken }).Result;

    foreach (Conflict conflict in conflictsFeed)
    {
        Document doc = conflict.GetResource<Document>();
        Console.WriteLine("Conflict record ResourceId = {0} ResourceType= {1}", conflict.ResourceId, conflict.ResourceType);

        // Perform application specific logic to process the conflict record / resource
    }

    conflictsFeedContinuationToken = conflictsFeed.ResponseContinuation;
} while (conflictsFeedContinuationToken != null);
```

## <a id="ManualFailovers"></a><span data-ttu-id="d1850-155">Manual Failovers</span><span class="sxs-lookup"><span data-stu-id="d1850-155">Manual Failovers</span></span>

<span data-ttu-id="d1850-156">In addition to automatic failovers, the current write region of a given Cosmos DB account can be manually changed dynamically to one of the existing read regions.</span><span class="sxs-lookup"><span data-stu-id="d1850-156">In addition to automatic failovers, the current write region of a given Cosmos DB account can be manually changed dynamically to one of the existing read regions.</span></span> <span data-ttu-id="d1850-157">Manual failovers can be initiated via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="d1850-157">Manual failovers can be initiated via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span> 

<span data-ttu-id="d1850-158">Manual failovers ensure **zero data loss** and **zero availability** loss and gracefully transfer write status from the old write region to the new one for the specified Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d1850-158">Manual failovers ensure **zero data loss** and **zero availability** loss and gracefully transfer write status from the old write region to the new one for the specified Cosmos DB account.</span></span> <span data-ttu-id="d1850-159">Like in automatic failovers, the Cosmos DB SDK automatically handles write region changes during manual failovers and ensures that calls are automatically redirected to the new write region.</span><span class="sxs-lookup"><span data-stu-id="d1850-159">Like in automatic failovers, the Cosmos DB SDK automatically handles write region changes during manual failovers and ensures that calls are automatically redirected to the new write region.</span></span> <span data-ttu-id="d1850-160">No code or configuration changes are required in your application to manage failovers.</span><span class="sxs-lookup"><span data-stu-id="d1850-160">No code or configuration changes are required in your application to manage failovers.</span></span> 

![Manual failovers in Azure Cosmos DB](./media/regional-failover/manual-failovers.png)

<span data-ttu-id="d1850-162">Some of the common scenarios where manual failover can be useful are:</span><span class="sxs-lookup"><span data-stu-id="d1850-162">Some of the common scenarios where manual failover can be useful are:</span></span>

<span data-ttu-id="d1850-163">**Follow the clock model**: If your applications have predictable traffic patterns based on the time of the day, you can periodically change the write status to the most active geographic region based on time of the day.</span><span class="sxs-lookup"><span data-stu-id="d1850-163">**Follow the clock model**: If your applications have predictable traffic patterns based on the time of the day, you can periodically change the write status to the most active geographic region based on time of the day.</span></span>

<span data-ttu-id="d1850-164">**Service update**: Certain globally distributed application deployment may involve rerouting traffic to different region via traffic manager during their planned service update.</span><span class="sxs-lookup"><span data-stu-id="d1850-164">**Service update**: Certain globally distributed application deployment may involve rerouting traffic to different region via traffic manager during their planned service update.</span></span> <span data-ttu-id="d1850-165">Such application deployment now can use manual failover to keep the write status to the region where there is going to be active traffic during the service update window.</span><span class="sxs-lookup"><span data-stu-id="d1850-165">Such application deployment now can use manual failover to keep the write status to the region where there is going to be active traffic during the service update window.</span></span>

<span data-ttu-id="d1850-166">**Business Continuity and Disaster Recovery (BCDR) and High Availability and Disaster Recovery (HADR) drills**: Most enterprise applications include business continuity tests as part of their development and release process.</span><span class="sxs-lookup"><span data-stu-id="d1850-166">**Business Continuity and Disaster Recovery (BCDR) and High Availability and Disaster Recovery (HADR) drills**: Most enterprise applications include business continuity tests as part of their development and release process.</span></span> <span data-ttu-id="d1850-167">BCDR and HADR testing is often an important step in compliance certifications and guaranteeing service availability in the case of regional outages.</span><span class="sxs-lookup"><span data-stu-id="d1850-167">BCDR and HADR testing is often an important step in compliance certifications and guaranteeing service availability in the case of regional outages.</span></span> <span data-ttu-id="d1850-168">You can test the BCDR readiness of your applications that use Cosmos DB for storage by triggering a manual failover of your Cosmos DB account and/or adding and removing a region dynamically.</span><span class="sxs-lookup"><span data-stu-id="d1850-168">You can test the BCDR readiness of your applications that use Cosmos DB for storage by triggering a manual failover of your Cosmos DB account and/or adding and removing a region dynamically.</span></span>

<span data-ttu-id="d1850-169">In this article, we reviewed how manual and automatic failovers work in Cosmos DB, and how you can configure your Cosmos DB accounts and applications to be globally available.</span><span class="sxs-lookup"><span data-stu-id="d1850-169">In this article, we reviewed how manual and automatic failovers work in Cosmos DB, and how you can configure your Cosmos DB accounts and applications to be globally available.</span></span> <span data-ttu-id="d1850-170">By using Cosmos DB's global replication support, you can improve end-to-end latency and ensure that they are highly available even in the event of region failures.</span><span class="sxs-lookup"><span data-stu-id="d1850-170">By using Cosmos DB's global replication support, you can improve end-to-end latency and ensure that they are highly available even in the event of region failures.</span></span> 

## <a id="NextSteps"></a><span data-ttu-id="d1850-171">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d1850-171">Next Steps</span></span>
* <span data-ttu-id="d1850-172">Learn about how Cosmos DB supports [global distribution](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="d1850-172">Learn about how Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="d1850-173">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="d1850-173">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="d1850-174">Develop with multiple regions using Azure Cosmos DB's [SQL API](tutorial-global-distribution-sql-api.md)</span><span class="sxs-lookup"><span data-stu-id="d1850-174">Develop with multiple regions using Azure Cosmos DB's [SQL API](tutorial-global-distribution-sql-api.md)</span></span>
* <span data-ttu-id="d1850-175">Learn how to build [Multi-region writer architectures](multi-region-writers.md) with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d1850-175">Learn how to build [Multi-region writer architectures](multi-region-writers.md) with Azure Cosmos DB</span></span>

