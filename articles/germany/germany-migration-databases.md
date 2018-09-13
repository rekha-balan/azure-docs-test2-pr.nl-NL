---
title: Migration of database resources from Azure Germany to global Azure
description: This article provides help for migrating database resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 6f5cccc41ca6430eb417539e09582bd25a615bab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865528"
---
# <a name="migration-of-database-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="8f474-103">Migration of database resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="8f474-103">Migration of database resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="8f474-104">This article will provide you some help for the migration of Azure Database resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="8f474-104">This article will provide you some help for the migration of Azure Database resources from Azure Germany to global Azure.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="8f474-105">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8f474-105">Azure SQL Database</span></span>

<span data-ttu-id="8f474-106">To migrate Azure SQL databases, you can use (for smaller workloads) the export function to create a BACPAC file.</span><span class="sxs-lookup"><span data-stu-id="8f474-106">To migrate Azure SQL databases, you can use (for smaller workloads) the export function to create a BACPAC file.</span></span> <span data-ttu-id="8f474-107">BaACPAC file is a compressed (zip'ed) file with metadata and data from the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="8f474-107">BaACPAC file is a compressed (zip'ed) file with metadata and data from the SQL Server database.</span></span> <span data-ttu-id="8f474-108">Once created, you can copy it to the target environment (for example with AzCopy) and use the import function to rebuild the database.</span><span class="sxs-lookup"><span data-stu-id="8f474-108">Once created, you can copy it to the target environment (for example with AzCopy) and use the import function to rebuild the database.</span></span> <span data-ttu-id="8f474-109">Be aware of the following considerations (see more in the links provided below):</span><span class="sxs-lookup"><span data-stu-id="8f474-109">Be aware of the following considerations (see more in the links provided below):</span></span>

- <span data-ttu-id="8f474-110">For an export to be transactionally consistent, make sure either</span><span class="sxs-lookup"><span data-stu-id="8f474-110">For an export to be transactionally consistent, make sure either</span></span>
  - <span data-ttu-id="8f474-111">no write activity is occurring during the export, or</span><span class="sxs-lookup"><span data-stu-id="8f474-111">no write activity is occurring during the export, or</span></span>
  - <span data-ttu-id="8f474-112">you're exporting from a transactionally consistent copy of your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="8f474-112">you're exporting from a transactionally consistent copy of your Azure SQL database.</span></span>
- <span data-ttu-id="8f474-113">For export to blob storage, the BACPAC file is limited to 200 GB.</span><span class="sxs-lookup"><span data-stu-id="8f474-113">For export to blob storage, the BACPAC file is limited to 200 GB.</span></span> <span data-ttu-id="8f474-114">For a larger BACPAC file, export to local storage.</span><span class="sxs-lookup"><span data-stu-id="8f474-114">For a larger BACPAC file, export to local storage.</span></span>
- <span data-ttu-id="8f474-115">If the export operation from Azure SQL Database takes longer than 20 hours, it may be canceled.</span><span class="sxs-lookup"><span data-stu-id="8f474-115">If the export operation from Azure SQL Database takes longer than 20 hours, it may be canceled.</span></span> <span data-ttu-id="8f474-116">Look for hints how to increase performance in the links below.</span><span class="sxs-lookup"><span data-stu-id="8f474-116">Look for hints how to increase performance in the links below.</span></span>

> [!NOTE]
> <span data-ttu-id="8f474-117">The connection string will change since the DNS name of the server will change.</span><span class="sxs-lookup"><span data-stu-id="8f474-117">The connection string will change since the DNS name of the server will change.</span></span>

### <a name="next-steps"></a><span data-ttu-id="8f474-118">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8f474-118">Next Steps</span></span>

- [<span data-ttu-id="8f474-119">Export DB to Bacpac file</span><span class="sxs-lookup"><span data-stu-id="8f474-119">Export DB to Bacpac file</span></span>](../sql-database/sql-database-export.md)
- [<span data-ttu-id="8f474-120">Import Bacpac file to a DB</span><span class="sxs-lookup"><span data-stu-id="8f474-120">Import Bacpac file to a DB</span></span>](../sql-database/sql-database-import.md)

### <a name="references"></a><span data-ttu-id="8f474-121">References</span><span class="sxs-lookup"><span data-stu-id="8f474-121">References</span></span>

- [<span data-ttu-id="8f474-122">Azure SQL Database documentation</span><span class="sxs-lookup"><span data-stu-id="8f474-122">Azure SQL Database documentation</span></span>](https://docs.microsoft.com/azure/sql-database/)







## <a name="sql-data-warehouse"></a><span data-ttu-id="8f474-123">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8f474-123">SQL Data Warehouse</span></span>

<span data-ttu-id="8f474-124">There are no special migration options for SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f474-124">There are no special migration options for SQL Data Warehouse.</span></span> <span data-ttu-id="8f474-125">Follow the instructions under [Azure SQL Database](#azure-sql-database).</span><span class="sxs-lookup"><span data-stu-id="8f474-125">Follow the instructions under [Azure SQL Database](#azure-sql-database).</span></span>







## <a name="azure-cosmos-db"></a><span data-ttu-id="8f474-126">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f474-126">Azure Cosmos DB</span></span>

<span data-ttu-id="8f474-127">With the Azure Cosmos DB Data Migration tool, you can easily migrate data to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f474-127">With the Azure Cosmos DB Data Migration tool, you can easily migrate data to Azure Cosmos DB.</span></span> <span data-ttu-id="8f474-128">The Azure Cosmos DB Data Migration tool is an open source solution that imports data to Azure Cosmos DB from different sources.</span><span class="sxs-lookup"><span data-stu-id="8f474-128">The Azure Cosmos DB Data Migration tool is an open source solution that imports data to Azure Cosmos DB from different sources.</span></span>

<span data-ttu-id="8f474-129">The tool is available as a graphical interface tool or as command-line tool.</span><span class="sxs-lookup"><span data-stu-id="8f474-129">The tool is available as a graphical interface tool or as command-line tool.</span></span> <span data-ttu-id="8f474-130">The source code is available in the GitHub repository for [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool), and a compiled version is available on the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=46436).</span><span class="sxs-lookup"><span data-stu-id="8f474-130">The source code is available in the GitHub repository for [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool), and a compiled version is available on the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=46436).</span></span>

<span data-ttu-id="8f474-131">The recommended steps are:</span><span class="sxs-lookup"><span data-stu-id="8f474-131">The recommended steps are:</span></span>

- <span data-ttu-id="8f474-132">Perform a review of application uptime requirements and account configurations to recommend the right action plan.</span><span class="sxs-lookup"><span data-stu-id="8f474-132">Perform a review of application uptime requirements and account configurations to recommend the right action plan.</span></span>
- <span data-ttu-id="8f474-133">Follow the steps to clone the account configurations from Azure Germany to the new region by running the tool</span><span class="sxs-lookup"><span data-stu-id="8f474-133">Follow the steps to clone the account configurations from Azure Germany to the new region by running the tool</span></span>
- <span data-ttu-id="8f474-134">If a maintenance window is possible, follow the steps to copy data from source to destination by running the tool</span><span class="sxs-lookup"><span data-stu-id="8f474-134">If a maintenance window is possible, follow the steps to copy data from source to destination by running the tool</span></span>
- <span data-ttu-id="8f474-135">If a maintenance window isn't possible, follow the steps to copy data from source to destination by running the tool and process that we recommend</span><span class="sxs-lookup"><span data-stu-id="8f474-135">If a maintenance window isn't possible, follow the steps to copy data from source to destination by running the tool and process that we recommend</span></span>
  - <span data-ttu-id="8f474-136">Make changes to read/write in application with config driven approach</span><span class="sxs-lookup"><span data-stu-id="8f474-136">Make changes to read/write in application with config driven approach</span></span>
  - <span data-ttu-id="8f474-137">Perform first-time sync</span><span class="sxs-lookup"><span data-stu-id="8f474-137">Perform first-time sync</span></span>
  - <span data-ttu-id="8f474-138">Setup incremental sync/catch up with change feed</span><span class="sxs-lookup"><span data-stu-id="8f474-138">Setup incremental sync/catch up with change feed</span></span>
  - <span data-ttu-id="8f474-139">Point reads to new account and validate application</span><span class="sxs-lookup"><span data-stu-id="8f474-139">Point reads to new account and validate application</span></span>
  - <span data-ttu-id="8f474-140">Stop writes to old account, validate change feed is caught up, then point writes to new accounts</span><span class="sxs-lookup"><span data-stu-id="8f474-140">Stop writes to old account, validate change feed is caught up, then point writes to new accounts</span></span>
  - <span data-ttu-id="8f474-141">Stop tool, and delete old account</span><span class="sxs-lookup"><span data-stu-id="8f474-141">Stop tool, and delete old account</span></span>
- <span data-ttu-id="8f474-142">Follow the steps to run the tool to validate that data is consistent across the old and new accounts.</span><span class="sxs-lookup"><span data-stu-id="8f474-142">Follow the steps to run the tool to validate that data is consistent across the old and new accounts.</span></span>


### <a name="references"></a><span data-ttu-id="8f474-143">References</span><span class="sxs-lookup"><span data-stu-id="8f474-143">References</span></span>

- [<span data-ttu-id="8f474-144">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f474-144">Azure Cosmos DB</span></span>](../cosmos-db/introduction.md)
- [<span data-ttu-id="8f474-145">Import data to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f474-145">Import data to Azure Cosmos DB</span></span>](../cosmos-db/import-data.md)








## <a name="redis-cache"></a><span data-ttu-id="8f474-146">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="8f474-146">Redis Cache</span></span>

<span data-ttu-id="8f474-147">There are a few options to migrate to global Azure, depending on the requirements you have.</span><span class="sxs-lookup"><span data-stu-id="8f474-147">There are a few options to migrate to global Azure, depending on the requirements you have.</span></span>

### <a name="option-1-data-loss-ok-create-new-instance"></a><span data-ttu-id="8f474-148">Option 1: Data Loss ok, create new instance</span><span class="sxs-lookup"><span data-stu-id="8f474-148">Option 1: Data Loss ok, create new instance</span></span>

<span data-ttu-id="8f474-149">This approach makes most sense when</span><span class="sxs-lookup"><span data-stu-id="8f474-149">This approach makes most sense when</span></span>

- <span data-ttu-id="8f474-150">you're using Redis as a transient data cache and</span><span class="sxs-lookup"><span data-stu-id="8f474-150">you're using Redis as a transient data cache and</span></span>
- <span data-ttu-id="8f474-151">your application will repopulate the cache data automatically in the new region.</span><span class="sxs-lookup"><span data-stu-id="8f474-151">your application will repopulate the cache data automatically in the new region.</span></span>

<span data-ttu-id="8f474-152">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8f474-152">Follow these steps:</span></span>

- <span data-ttu-id="8f474-153">Create a new Redis instance in the new target region.</span><span class="sxs-lookup"><span data-stu-id="8f474-153">Create a new Redis instance in the new target region.</span></span>
- <span data-ttu-id="8f474-154">Update your application to use the new instance in new region.</span><span class="sxs-lookup"><span data-stu-id="8f474-154">Update your application to use the new instance in new region.</span></span>
- <span data-ttu-id="8f474-155">Delete old Redis instance in source region.</span><span class="sxs-lookup"><span data-stu-id="8f474-155">Delete old Redis instance in source region.</span></span>

### <a name="option-2-copy-data-from-source-instance-to-target-instance"></a><span data-ttu-id="8f474-156">Option 2: Copy data from Source instance to Target instance</span><span class="sxs-lookup"><span data-stu-id="8f474-156">Option 2: Copy data from Source instance to Target instance</span></span>

<span data-ttu-id="8f474-157">A member of the Azure Redis team wrote an open-source tool that copies data from one Redis instance to another without requiring Import or Export functionality.</span><span class="sxs-lookup"><span data-stu-id="8f474-157">A member of the Azure Redis team wrote an open-source tool that copies data from one Redis instance to another without requiring Import or Export functionality.</span></span>

- <span data-ttu-id="8f474-158">Create a VM in the source region.</span><span class="sxs-lookup"><span data-stu-id="8f474-158">Create a VM in the source region.</span></span> <span data-ttu-id="8f474-159">If your data set in Redis is large, make sure to select a relatively powerful VM size to minimize copying time.</span><span class="sxs-lookup"><span data-stu-id="8f474-159">If your data set in Redis is large, make sure to select a relatively powerful VM size to minimize copying time.</span></span>
- <span data-ttu-id="8f474-160">Create new Redis instance in target region.</span><span class="sxs-lookup"><span data-stu-id="8f474-160">Create new Redis instance in target region.</span></span>
- <span data-ttu-id="8f474-161">Flush data from the **target** instance (make sure **NOT** to flush from the **source** instance.</span><span class="sxs-lookup"><span data-stu-id="8f474-161">Flush data from the **target** instance (make sure **NOT** to flush from the **source** instance.</span></span> <span data-ttu-id="8f474-162">Flushing is required because the copy tool **doesn't overwrite** existing keys in the target location.</span><span class="sxs-lookup"><span data-stu-id="8f474-162">Flushing is required because the copy tool **doesn't overwrite** existing keys in the target location.</span></span>
- <span data-ttu-id="8f474-163">Use a tool like the following to automatically copy data from source Redis instance to target Redis instance: [Source](https://github.com/deepakverma/redis-copy), [Download](https://github.com/deepakverma/redis-copy/releases/download/alpha/Release.zip).</span><span class="sxs-lookup"><span data-stu-id="8f474-163">Use a tool like the following to automatically copy data from source Redis instance to target Redis instance: [Source](https://github.com/deepakverma/redis-copy), [Download](https://github.com/deepakverma/redis-copy/releases/download/alpha/Release.zip).</span></span>

> [!NOTE]
> <span data-ttu-id="8f474-164">This process can take a long time, depending on the size of your data set.</span><span class="sxs-lookup"><span data-stu-id="8f474-164">This process can take a long time, depending on the size of your data set.</span></span>

### <a name="option-3-export-from-source-instance-import-into-destination-instance"></a><span data-ttu-id="8f474-165">Option 3: Export from source instance, import into destination instance</span><span class="sxs-lookup"><span data-stu-id="8f474-165">Option 3: Export from source instance, import into destination instance</span></span>

<span data-ttu-id="8f474-166">This approach takes advantage of features only available in the Premium tier.</span><span class="sxs-lookup"><span data-stu-id="8f474-166">This approach takes advantage of features only available in the Premium tier.</span></span>

- <span data-ttu-id="8f474-167">Create a new Premium tier Redis instance in the target region.</span><span class="sxs-lookup"><span data-stu-id="8f474-167">Create a new Premium tier Redis instance in the target region.</span></span> <span data-ttu-id="8f474-168">Use the same size as the source Redis instance.</span><span class="sxs-lookup"><span data-stu-id="8f474-168">Use the same size as the source Redis instance.</span></span>
- <span data-ttu-id="8f474-169">[Export data from source cache](../redis-cache/cache-how-to-import-export-data.md) or use the [Export-AzureRmRedisCache PowerShell cmdlet](/powershell/module/azurerm.rediscache/export-azurermrediscache?view=azurermps-6.4.0).</span><span class="sxs-lookup"><span data-stu-id="8f474-169">[Export data from source cache](../redis-cache/cache-how-to-import-export-data.md) or use the [Export-AzureRmRedisCache PowerShell cmdlet](/powershell/module/azurerm.rediscache/export-azurermrediscache?view=azurermps-6.4.0).</span></span>

> [!NOTE]
> <span data-ttu-id="8f474-170">The export storage account must be in the same region as the cache instance.</span><span class="sxs-lookup"><span data-stu-id="8f474-170">The export storage account must be in the same region as the cache instance.</span></span>

- <span data-ttu-id="8f474-171">Copy exported blobs to a storage account in destination region (for example by using AzCopy)</span><span class="sxs-lookup"><span data-stu-id="8f474-171">Copy exported blobs to a storage account in destination region (for example by using AzCopy)</span></span>
- <span data-ttu-id="8f474-172">[Import data into destination cache](../redis-cache/cache-how-to-import-export-data.md) or use the [Import-AzureRmRedisCAche PowerShell cmdlet](/powershell/module/azurerm.rediscache/import-azurermrediscache?view=azurermps-6.4.0).</span><span class="sxs-lookup"><span data-stu-id="8f474-172">[Import data into destination cache](../redis-cache/cache-how-to-import-export-data.md) or use the [Import-AzureRmRedisCAche PowerShell cmdlet](/powershell/module/azurerm.rediscache/import-azurermrediscache?view=azurermps-6.4.0).</span></span>
- <span data-ttu-id="8f474-173">Reconfigure your application to use the target Redis instance.</span><span class="sxs-lookup"><span data-stu-id="8f474-173">Reconfigure your application to use the target Redis instance.</span></span>

### <a name="option-4-write-data-to-two-redis-instances-read-from-one-instance"></a><span data-ttu-id="8f474-174">Option 4: Write data to two Redis instances, read from one instance</span><span class="sxs-lookup"><span data-stu-id="8f474-174">Option 4: Write data to two Redis instances, read from one instance</span></span>

<span data-ttu-id="8f474-175">For this approach, you need to modify your application.</span><span class="sxs-lookup"><span data-stu-id="8f474-175">For this approach, you need to modify your application.</span></span> <span data-ttu-id="8f474-176">It needs to write data to more than one cache instances while reading from one of the cache instances.</span><span class="sxs-lookup"><span data-stu-id="8f474-176">It needs to write data to more than one cache instances while reading from one of the cache instances.</span></span> <span data-ttu-id="8f474-177">This approach makes sense if the data stored in Redis</span><span class="sxs-lookup"><span data-stu-id="8f474-177">This approach makes sense if the data stored in Redis</span></span>
- <span data-ttu-id="8f474-178">is refreshed on a regular basis,</span><span class="sxs-lookup"><span data-stu-id="8f474-178">is refreshed on a regular basis,</span></span> 
- <span data-ttu-id="8f474-179">all data is written to the target Redis instance, and</span><span class="sxs-lookup"><span data-stu-id="8f474-179">all data is written to the target Redis instance, and</span></span>
- <span data-ttu-id="8f474-180">you have enough time for all data to be refreshed.</span><span class="sxs-lookup"><span data-stu-id="8f474-180">you have enough time for all data to be refreshed.</span></span>

### <a name="references"></a><span data-ttu-id="8f474-181">References</span><span class="sxs-lookup"><span data-stu-id="8f474-181">References</span></span>

- [<span data-ttu-id="8f474-182">Overview Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="8f474-182">Overview Azure Redis Cache</span></span>](../redis-cache/cache-overview.md)
