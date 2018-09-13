---
title: Import and Export data in Azure Redis Cache | Microsoft Docs
description: Learn how to import and export data to and from blob storage with your premium Azure Redis Cache instances
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: sdanie
ms.openlocfilehash: 9fb019b6f2e7cbbbffec394866ec8685172c54ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552676"
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="968cc-103">Import and Export data in Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="968cc-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="968cc-104">Import/Export is an Azure Redis Cache data management operation, which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a blob in an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="968cc-104">Import/Export is an Azure Redis Cache data management operation, which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="968cc-105">**Export** - you can export your Azure Redis Cache RDB snapshots to a Page Blob.</span><span class="sxs-lookup"><span data-stu-id="968cc-105">**Export** - you can export your Azure Redis Cache RDB snapshots to a Page Blob.</span></span>
- <span data-ttu-id="968cc-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span><span class="sxs-lookup"><span data-stu-id="968cc-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="968cc-107">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span><span class="sxs-lookup"><span data-stu-id="968cc-107">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="968cc-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides the answers to commonly asked questions.</span><span class="sxs-lookup"><span data-stu-id="968cc-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides the answers to commonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="968cc-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span><span class="sxs-lookup"><span data-stu-id="968cc-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="968cc-110">Import</span><span class="sxs-lookup"><span data-stu-id="968cc-110">Import</span></span>
<span data-ttu-id="968cc-111">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span><span class="sxs-lookup"><span data-stu-id="968cc-111">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="968cc-112">Importing data is an easy way to create a cache with pre-populated data.</span><span class="sxs-lookup"><span data-stu-id="968cc-112">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="968cc-113">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span><span class="sxs-lookup"><span data-stu-id="968cc-113">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="968cc-114">Before beginning the import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in the same region and subscription as your Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="968cc-114">Before beginning the import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in the same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="968cc-115">For more information, see [Get started with Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="968cc-115">For more information, see [Get started with Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="968cc-116">If you exported your RDB file using the [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span><span class="sxs-lookup"><span data-stu-id="968cc-116">If you exported your RDB file using the [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="968cc-117">To import one or more exported cache blobs, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Import data** from the **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="968cc-117">To import one or more exported cache blobs, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Import data** from the **Resource menu**.</span></span>

    ![Import data][cache-import-data]
2. <span data-ttu-id="968cc-119">Click **Choose Blob(s)** and select the storage account that contains the data to import.</span><span class="sxs-lookup"><span data-stu-id="968cc-119">Click **Choose Blob(s)** and select the storage account that contains the data to import.</span></span>

    ![Choose storage account][cache-import-choose-storage-account]
3. <span data-ttu-id="968cc-121">Click the container that contains the data to import.</span><span class="sxs-lookup"><span data-stu-id="968cc-121">Click the container that contains the data to import.</span></span>

    ![Choose container][cache-import-choose-container]
4. <span data-ttu-id="968cc-123">Select one or more blobs to import by clicking the area to the left of the blob name, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="968cc-123">Select one or more blobs to import by clicking the area to the left of the blob name, and then click **Select**.</span></span>

    ![Choose blobs][cache-import-choose-blobs]
5. <span data-ttu-id="968cc-125">Click **Import** to begin the import process.</span><span class="sxs-lookup"><span data-stu-id="968cc-125">Click **Import** to begin the import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="968cc-126">The cache is not accessible by cache clients during the import process, and any existing data in the cache is deleted.</span><span class="sxs-lookup"><span data-stu-id="968cc-126">The cache is not accessible by cache clients during the import process, and any existing data in the cache is deleted.</span></span>
   >
   >

    ![Import][cache-import-blobs]

    <span data-ttu-id="968cc-128">You can monitor the progress of the import operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="968cc-128">You can monitor the progress of the import operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Import progress][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="968cc-130">Export</span><span class="sxs-lookup"><span data-stu-id="968cc-130">Export</span></span>
<span data-ttu-id="968cc-131">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span><span class="sxs-lookup"><span data-stu-id="968cc-131">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span></span> <span data-ttu-id="968cc-132">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span><span class="sxs-lookup"><span data-stu-id="968cc-132">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="968cc-133">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span><span class="sxs-lookup"><span data-stu-id="968cc-133">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="968cc-134">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span><span class="sxs-lookup"><span data-stu-id="968cc-134">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

1. <span data-ttu-id="968cc-135">To export the current contents of the cache to storage, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Export data** from the **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="968cc-135">To export the current contents of the cache to storage, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Export data** from the **Resource menu**.</span></span>

    ![Choose storage container][cache-export-data-choose-storage-container]
2. <span data-ttu-id="968cc-137">Click **Choose Storage Container** and select the desired storage account.</span><span class="sxs-lookup"><span data-stu-id="968cc-137">Click **Choose Storage Container** and select the desired storage account.</span></span> <span data-ttu-id="968cc-138">The storage account must be in the same subscription and region as your cache.</span><span class="sxs-lookup"><span data-stu-id="968cc-138">The storage account must be in the same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="968cc-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span><span class="sxs-lookup"><span data-stu-id="968cc-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Storage account][cache-export-data-choose-account]
3. <span data-ttu-id="968cc-141">Choose the desired blob container and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="968cc-141">Choose the desired blob container and click **Select**.</span></span> <span data-ttu-id="968cc-142">To use new a container, click **Add Container** to add it first and then select it from the list.</span><span class="sxs-lookup"><span data-stu-id="968cc-142">To use new a container, click **Add Container** to add it first and then select it from the list.</span></span>

    ![Choose storage container][cache-export-data-container]
4. <span data-ttu-id="968cc-144">Type a **Blob name prefix** and click **Export** to start the export process.</span><span class="sxs-lookup"><span data-stu-id="968cc-144">Type a **Blob name prefix** and click **Export** to start the export process.</span></span> <span data-ttu-id="968cc-145">The blob name prefix is used to prefix the names of files generated by this export operation.</span><span class="sxs-lookup"><span data-stu-id="968cc-145">The blob name prefix is used to prefix the names of files generated by this export operation.</span></span>

    ![Export][cache-export-data]

    <span data-ttu-id="968cc-147">You can monitor the progress of the export operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="968cc-147">You can monitor the progress of the export operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Export data complete][cache-export-data-export-complete]

    <span data-ttu-id="968cc-149">Caches remain available for use during the export process.</span><span class="sxs-lookup"><span data-stu-id="968cc-149">Caches remain available for use during the export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="968cc-150">Import/Export FAQ</span><span class="sxs-lookup"><span data-stu-id="968cc-150">Import/Export FAQ</span></span>
<span data-ttu-id="968cc-151">This section contains frequently asked questions about the Import/Export feature.</span><span class="sxs-lookup"><span data-stu-id="968cc-151">This section contains frequently asked questions about the Import/Export feature.</span></span>

* [<span data-ttu-id="968cc-152">What pricing tiers can use Import/Export?</span><span class="sxs-lookup"><span data-stu-id="968cc-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="968cc-153">Can I import data from any Redis server?</span><span class="sxs-lookup"><span data-stu-id="968cc-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="968cc-154">What RDB versions can I import?</span><span class="sxs-lookup"><span data-stu-id="968cc-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="968cc-155">Is my cache available during an Import/Export operation?</span><span class="sxs-lookup"><span data-stu-id="968cc-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="968cc-156">Can I use Import/Export with Redis cluster?</span><span class="sxs-lookup"><span data-stu-id="968cc-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="968cc-157">How does Import/Export work with a custom databases setting?</span><span class="sxs-lookup"><span data-stu-id="968cc-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="968cc-158">How is Import/Export different from Redis persistence?</span><span class="sxs-lookup"><span data-stu-id="968cc-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="968cc-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span><span class="sxs-lookup"><span data-stu-id="968cc-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="968cc-160">I received a timeout error during my Import/Export operation. What does it mean?</span><span class="sxs-lookup"><span data-stu-id="968cc-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation.-what-does-it-mean)
* [<span data-ttu-id="968cc-161">I got an error when exporting my data to Azure Blob Storage. What happened?</span><span class="sxs-lookup"><span data-stu-id="968cc-161">I got an error when exporting my data to Azure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage.-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="968cc-162">What pricing tiers can use Import/Export?</span><span class="sxs-lookup"><span data-stu-id="968cc-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="968cc-163">Import/Export is available only in the premium pricing tier.</span><span class="sxs-lookup"><span data-stu-id="968cc-163">Import/Export is available only in the premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="968cc-164">Can I import data from any Redis server?</span><span class="sxs-lookup"><span data-stu-id="968cc-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="968cc-165">Yes, in addition to importing data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="968cc-165">Yes, in addition to importing data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="968cc-166">To do this, upload the RDB file from the desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="968cc-166">To do this, upload the RDB file from the desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="968cc-167">For example, you may want to export the data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span><span class="sxs-lookup"><span data-stu-id="968cc-167">For example, you may want to export the data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="968cc-168">To successfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, the page blob size must be aligned on a 512 byte boundary.</span><span class="sxs-lookup"><span data-stu-id="968cc-168">To successfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, the page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="968cc-169">For sample code to perform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span><span class="sxs-lookup"><span data-stu-id="968cc-169">For sample code to perform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="968cc-170">What RDB versions can I import?</span><span class="sxs-lookup"><span data-stu-id="968cc-170">What RDB versions can I import?</span></span>

<span data-ttu-id="968cc-171">Azure Redis Cache supports RDB import up through RDB version 7.</span><span class="sxs-lookup"><span data-stu-id="968cc-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="968cc-172">Is my cache available during an Import/Export operation?</span><span class="sxs-lookup"><span data-stu-id="968cc-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="968cc-173">**Export** - Caches remain available and you can continue to use your cache during an export operation.</span><span class="sxs-lookup"><span data-stu-id="968cc-173">**Export** - Caches remain available and you can continue to use your cache during an export operation.</span></span>
* <span data-ttu-id="968cc-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when the import operation completes.</span><span class="sxs-lookup"><span data-stu-id="968cc-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when the import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="968cc-175">Can I use Import/Export with Redis cluster?</span><span class="sxs-lookup"><span data-stu-id="968cc-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="968cc-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span><span class="sxs-lookup"><span data-stu-id="968cc-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="968cc-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span><span class="sxs-lookup"><span data-stu-id="968cc-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="968cc-178">When clustered cache data is imported, the keys are redistributed among the shards of the cluster.</span><span class="sxs-lookup"><span data-stu-id="968cc-178">When clustered cache data is imported, the keys are redistributed among the shards of the cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="968cc-179">How does Import/Export work with a custom databases setting?</span><span class="sxs-lookup"><span data-stu-id="968cc-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="968cc-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for the `databases` setting during cache creation.</span><span class="sxs-lookup"><span data-stu-id="968cc-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="968cc-181">When importing to a pricing tier with a lower `databases` limit than the tier from which you exported:</span><span class="sxs-lookup"><span data-stu-id="968cc-181">When importing to a pricing tier with a lower `databases` limit than the tier from which you exported:</span></span>
  * <span data-ttu-id="968cc-182">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span><span class="sxs-lookup"><span data-stu-id="968cc-182">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="968cc-183">If you are using a custom number of `databases` that falls within the limits for the tier to which you are importing, no data is lost.</span><span class="sxs-lookup"><span data-stu-id="968cc-183">If you are using a custom number of `databases` that falls within the limits for the tier to which you are importing, no data is lost.</span></span>
  * <span data-ttu-id="968cc-184">If your exported data contained data in a database that exceeds the limits of the new tier, the data from those higher databases is not imported.</span><span class="sxs-lookup"><span data-stu-id="968cc-184">If your exported data contained data in a database that exceeds the limits of the new tier, the data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="968cc-185">How is Import/Export different from Redis persistence?</span><span class="sxs-lookup"><span data-stu-id="968cc-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="968cc-186">Azure Redis Cache persistence allows you to persist data stored in Redis to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="968cc-186">Azure Redis Cache persistence allows you to persist data stored in Redis to Azure Storage.</span></span> <span data-ttu-id="968cc-187">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span><span class="sxs-lookup"><span data-stu-id="968cc-187">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="968cc-188">If a catastrophic event occurs that disables both the primary and replica cache, the cache data is restored automatically using the most recent snapshot.</span><span class="sxs-lookup"><span data-stu-id="968cc-188">If a catastrophic event occurs that disables both the primary and replica cache, the cache data is restored automatically using the most recent snapshot.</span></span> <span data-ttu-id="968cc-189">For more information, see [How to configure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="968cc-189">For more information, see [How to configure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="968cc-190">Import/ Export allows you to bring data into or export from Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="968cc-190">Import/ Export allows you to bring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="968cc-191">It does not configure backup and restore using Redis persistence.</span><span class="sxs-lookup"><span data-stu-id="968cc-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="968cc-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span><span class="sxs-lookup"><span data-stu-id="968cc-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="968cc-193">Yes, for PowerShell instructions see [To import a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [To export a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="968cc-193">Yes, for PowerShell instructions see [To import a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [To export a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="968cc-194">I received a timeout error during my Import/Export operation.</span><span class="sxs-lookup"><span data-stu-id="968cc-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="968cc-195">What does it mean?</span><span class="sxs-lookup"><span data-stu-id="968cc-195">What does it mean?</span></span>
<span data-ttu-id="968cc-196">If you remain on the **Import data** or **Export data** blade for longer than 15 minutes before initiating the operation, you receive an error with an error message similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="968cc-196">If you remain on the **Import data** or **Export data** blade for longer than 15 minutes before initiating the operation, you receive an error with an error message similar to the following example:</span></span>

    The request to import data into cache 'contoso55' failed with status 'error' and error 'One of the SAS URIs provided could not be used for the following reason: The SAS token end time (se) must be at least 1 hour from now and the start time (st), if given, must be at least 15 minutes in the past.

<span data-ttu-id="968cc-197">To resolve this, initiate the import or export operation before 15 minutes has elapsed.</span><span class="sxs-lookup"><span data-stu-id="968cc-197">To resolve this, initiate the import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened"></a><span data-ttu-id="968cc-198">I got an error when exporting my data to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="968cc-198">I got an error when exporting my data to Azure Blob Storage.</span></span> <span data-ttu-id="968cc-199">What happened?</span><span class="sxs-lookup"><span data-stu-id="968cc-199">What happened?</span></span>
<span data-ttu-id="968cc-200">Export works only with RDB files stored as page blobs.</span><span class="sxs-lookup"><span data-stu-id="968cc-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="968cc-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span><span class="sxs-lookup"><span data-stu-id="968cc-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="968cc-202">For more information, see [Blob storage accounts](../storage/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="968cc-202">For more information, see [Blob storage accounts](../storage/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="968cc-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="968cc-203">Next steps</span></span>
<span data-ttu-id="968cc-204">Learn how to use more premium cache features.</span><span class="sxs-lookup"><span data-stu-id="968cc-204">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="968cc-205">Introduction to the Azure Redis Cache Premium tier</span><span class="sxs-lookup"><span data-stu-id="968cc-205">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-import-export-data/cache-import-data-import-complete.png











