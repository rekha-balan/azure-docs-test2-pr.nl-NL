---
title: Import data for use with the Azure Cosmos DB Table API | Microsoft Docs
description: Learn how import data to use with the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: na
ms.topic: tutorial
ms.date: 11/28/2017
ms.author: sngun
ms.openlocfilehash: 905815259707116759e0b980690fac108ab81c7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866014"
---
# <a name="migrate-your-data-to-azure-cosmos-db-table-api-account"></a><span data-ttu-id="e1a95-103">Migrate your data to Azure Cosmos DB Table API account</span><span class="sxs-lookup"><span data-stu-id="e1a95-103">Migrate your data to Azure Cosmos DB Table API account</span></span>

<span data-ttu-id="e1a95-104">This tutorial provides instructions on importing data for use with the Azure Cosmos DB [Table API](table-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1a95-104">This tutorial provides instructions on importing data for use with the Azure Cosmos DB [Table API](table-introduction.md).</span></span> <span data-ttu-id="e1a95-105">If you have data stored in Azure Table storage, you can use either the Data Migration Tool or AzCopy to import your data to Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="e1a95-105">If you have data stored in Azure Table storage, you can use either the Data Migration Tool or AzCopy to import your data to Azure Cosmos DB Table API.</span></span> <span data-ttu-id="e1a95-106">If you have data stored in an Azure Cosmos DB Table API (preview) account, you must use the Data Migration tool to migrate your data.</span><span class="sxs-lookup"><span data-stu-id="e1a95-106">If you have data stored in an Azure Cosmos DB Table API (preview) account, you must use the Data Migration tool to migrate your data.</span></span> 

<span data-ttu-id="e1a95-107">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="e1a95-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1a95-108">Importing data with the Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="e1a95-108">Importing data with the Data Migration tool</span></span>
> * <span data-ttu-id="e1a95-109">Importing data with AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1a95-109">Importing data with AzCopy</span></span>
> * <span data-ttu-id="e1a95-110">Migrating from Table API (preview) to Table API</span><span class="sxs-lookup"><span data-stu-id="e1a95-110">Migrating from Table API (preview) to Table API</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e1a95-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1a95-111">Prerequisites</span></span>

* <span data-ttu-id="e1a95-112">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for an individual container or a set of containers.</span><span class="sxs-lookup"><span data-stu-id="e1a95-112">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for an individual container or a set of containers.</span></span> <span data-ttu-id="e1a95-113">Be sure to increase the throughput for larger data migrations.</span><span class="sxs-lookup"><span data-stu-id="e1a95-113">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="e1a95-114">After you've completed the migration, decrease the throughput to save costs.</span><span class="sxs-lookup"><span data-stu-id="e1a95-114">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="e1a95-115">For more information about increasing throughput in the Azure portal, see Performance levels and pricing tiers in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e1a95-115">For more information about increasing throughput in the Azure portal, see Performance levels and pricing tiers in Azure Cosmos DB.</span></span>

## <a name="data-migration-tool"></a><span data-ttu-id="e1a95-116">Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="e1a95-116">Data Migration tool</span></span>

<span data-ttu-id="e1a95-117">The command-line Azure Cosmos DB Data Migration tool (dt.exe) can be used to import your existing Azure Table storage data to a Table API GA account, or migrate data from a Table API (preview) account into a Table API GA account.</span><span class="sxs-lookup"><span data-stu-id="e1a95-117">The command-line Azure Cosmos DB Data Migration tool (dt.exe) can be used to import your existing Azure Table storage data to a Table API GA account, or migrate data from a Table API (preview) account into a Table API GA account.</span></span> <span data-ttu-id="e1a95-118">Other sources are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="e1a95-118">Other sources are not currently supported.</span></span> <span data-ttu-id="e1a95-119">The UI based Data Migration tool (dtui.exe) is not currently supported for Table API accounts.</span><span class="sxs-lookup"><span data-stu-id="e1a95-119">The UI based Data Migration tool (dtui.exe) is not currently supported for Table API accounts.</span></span> 

<span data-ttu-id="e1a95-120">To perform a migration of table data, complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="e1a95-120">To perform a migration of table data, complete the following tasks:</span></span>

1. <span data-ttu-id="e1a95-121">Download the migration tool from [GitHub](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="e1a95-121">Download the migration tool from [GitHub](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>
2. <span data-ttu-id="e1a95-122">Run `dt.exe` using the command-line arguments for your scenario.</span><span class="sxs-lookup"><span data-stu-id="e1a95-122">Run `dt.exe` using the command-line arguments for your scenario.</span></span> <span data-ttu-id="e1a95-123">`dt.exe` takes a command in the following format:</span><span class="sxs-lookup"><span data-stu-id="e1a95-123">`dt.exe` takes a command in the following format:</span></span>

   ```bash
    dt.exe [/<option>:<value>] /s:<source-name> [/s.<source-option>:<value>] /t:<target-name> [/t.<target-option>:<value>] 
```

<span data-ttu-id="e1a95-124">Options for the command are:</span><span class="sxs-lookup"><span data-stu-id="e1a95-124">Options for the command are:</span></span>

    /ErrorLog: Optional. Name of the CSV file to redirect data transfer failures
    /OverwriteErrorLog: Optional. Overwrite error log file
    /ProgressUpdateInterval: Optional, default is 00:00:01. Time interval to refresh on-screen data transfer progress
    /ErrorDetails: Optional, default is None. Specifies that detailed error information should be displayed for the following errors: None, Critical, All

### <a name="command-line-source-settings"></a><span data-ttu-id="e1a95-125">Command-line source settings</span><span class="sxs-lookup"><span data-stu-id="e1a95-125">Command-line source settings</span></span>

<span data-ttu-id="e1a95-126">Use the following source options when defining Azure Table Storage or Table API preview as the source of the migration.</span><span class="sxs-lookup"><span data-stu-id="e1a95-126">Use the following source options when defining Azure Table Storage or Table API preview as the source of the migration.</span></span>

    /s:AzureTable: Reads data from Azure Table storage
    /s.ConnectionString: Connection string for the table endpoint. This can be retrieved from the Azure portal
    /s.LocationMode: Optional, default is PrimaryOnly. Specifies which location mode to use when connecting to Azure Table storage: PrimaryOnly, PrimaryThenSecondary, SecondaryOnly, SecondaryThenPrimary
    /s.Table: Name of the Azure Table
    /s.InternalFields: Set to All for table migration as RowKey and PartitionKey are required for import.
    /s.Filter: Optional. Filter string to apply
    /s.Projection: Optional. List of columns to select

<span data-ttu-id="e1a95-127">To retrieve the source connection string when importing from Azure Table storage, open the Azure portal and click **Storage accounts** > **Account** > **Access keys**, and then use the copy button to copy the **Connection string**.</span><span class="sxs-lookup"><span data-stu-id="e1a95-127">To retrieve the source connection string when importing from Azure Table storage, open the Azure portal and click **Storage accounts** > **Account** > **Access keys**, and then use the copy button to copy the **Connection string**.</span></span>

![Screenshot of HBase source options](./media/table-import/storage-table-access-key.png)

<span data-ttu-id="e1a95-129">To retrieve the source connection string when importing from an Azure Cosmos DB Table API (preview) account, open the Azure portal, click **Azure Cosmos DB** > **Account** > **Connection String** and use the copy button to copy the **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="e1a95-129">To retrieve the source connection string when importing from an Azure Cosmos DB Table API (preview) account, open the Azure portal, click **Azure Cosmos DB** > **Account** > **Connection String** and use the copy button to copy the **Connection String**.</span></span>

![Screenshot of HBase source options](./media/table-import/cosmos-connection-string.png)

[<span data-ttu-id="e1a95-131">Sample Azure Table Storage command</span><span class="sxs-lookup"><span data-stu-id="e1a95-131">Sample Azure Table Storage command</span></span>](#azure-table-storage)

[<span data-ttu-id="e1a95-132">Sample Azure Cosmos DB Table API (preview) command</span><span class="sxs-lookup"><span data-stu-id="e1a95-132">Sample Azure Cosmos DB Table API (preview) command</span></span>](#table-api-preview)

### <a name="command-line-target-settings"></a><span data-ttu-id="e1a95-133">Command-line target settings</span><span class="sxs-lookup"><span data-stu-id="e1a95-133">Command-line target settings</span></span>

<span data-ttu-id="e1a95-134">Use the following target options when defining Azure Cosmos DB Table API as the target of the migration.</span><span class="sxs-lookup"><span data-stu-id="e1a95-134">Use the following target options when defining Azure Cosmos DB Table API as the target of the migration.</span></span>

    /t:TableAPIBulk: Uploads data into Azure CosmosDB Table in batches
    /t.ConnectionString: Connection string for the table endpoint
    /t.TableName: Specifies the name of the table to write to
    /t.Overwrite: Optional, default is false. Specifies if existing values should be overwritten
    /t.MaxInputBufferSize: Optional, default is 1GB. Approximate estimate of input bytes to buffer before flushing data to sink
    /t.Throughput: Optional, service defaults if not specified. Specifies throughput to configure for table
    /t.MaxBatchSize: Optional, default is 2MB. Specify the batch size in bytes

<a id="azure-table-storage"></a>
### <a name="sample-command-source-is-azure-table-storage"></a><span data-ttu-id="e1a95-135">Sample command: Source is Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="e1a95-135">Sample command: Source is Azure Table storage</span></span>

<span data-ttu-id="e1a95-136">Here is a command-line sample showing how to import from Azure Table storage to Table API:</span><span class="sxs-lookup"><span data-stu-id="e1a95-136">Here is a command-line sample showing how to import from Azure Table storage to Table API:</span></span>

```
dt /s:AzureTable /s.ConnectionString:DefaultEndpointsProtocol=https;AccountName=<Azure Table storage account name>;AccountKey=<Account Key>;EndpointSuffix=core.windows.net /s.Table:<Table name> /t:TableAPIBulk /t.ConnectionString:DefaultEndpointsProtocol=https;AccountName=<Azure Cosmos DB account name>;AccountKey=<Azure Cosmos DB account key>;TableEndpoint=https://<Account name>.table.cosmosdb.azure.com:443 /t.TableName:<Table name> /t.Overwrite
```
<a id="table-api-preview"></a>
### <a name="sample-command-source-is-azure-cosmos-db-table-api-preview"></a><span data-ttu-id="e1a95-137">Sample command: Source is Azure Cosmos DB Table API (preview)</span><span class="sxs-lookup"><span data-stu-id="e1a95-137">Sample command: Source is Azure Cosmos DB Table API (preview)</span></span>

<span data-ttu-id="e1a95-138">Here is a command-line sample to import from Table API preview to Table API GA:</span><span class="sxs-lookup"><span data-stu-id="e1a95-138">Here is a command-line sample to import from Table API preview to Table API GA:</span></span>

```
dt /s:AzureTable /s.ConnectionString:DefaultEndpointsProtocol=https;AccountName=<Table API preview account name>;AccountKey=<Table API preview account key>;TableEndpoint=https://<Account Name>.documents.azure.com; /s.Table:<Table name> /t:TableAPIBulk /t.ConnectionString:DefaultEndpointsProtocol=https;AccountName=<Azure Cosmos DB account name>;AccountKey=<Azure Cosmos DB account key>;TableEndpoint=https://<Account name>.table.cosmosdb.azure.com:443 /t.TableName:<Table name> /t.Overwrite
```

## <a name="migrate-data-by-using-azcopy"></a><span data-ttu-id="e1a95-139">Migrate data by using AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1a95-139">Migrate data by using AzCopy</span></span>

<span data-ttu-id="e1a95-140">Using the AzCopy command-line utility is the other option for migrating data from Azure Table storage to the Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="e1a95-140">Using the AzCopy command-line utility is the other option for migrating data from Azure Table storage to the Azure Cosmos DB Table API.</span></span> <span data-ttu-id="e1a95-141">To use AzCopy, you first export your data as described in [Export data from Table storage](../storage/common/storage-use-azcopy.md#export-data-from-table-storage), then import the data to Azure Cosmos DB as described in [Azure Cosmos DB Table API](../storage/common/storage-use-azcopy.md#import-data-into-table-storage).</span><span class="sxs-lookup"><span data-stu-id="e1a95-141">To use AzCopy, you first export your data as described in [Export data from Table storage](../storage/common/storage-use-azcopy.md#export-data-from-table-storage), then import the data to Azure Cosmos DB as described in [Azure Cosmos DB Table API](../storage/common/storage-use-azcopy.md#import-data-into-table-storage).</span></span>

<span data-ttu-id="e1a95-142">When performing the import into Azure Cosmos DB, refer to the following sample.</span><span class="sxs-lookup"><span data-stu-id="e1a95-142">When performing the import into Azure Cosmos DB, refer to the following sample.</span></span> <span data-ttu-id="e1a95-143">Note that the /Dest value uses cosmosdb, not core.</span><span class="sxs-lookup"><span data-stu-id="e1a95-143">Note that the /Dest value uses cosmosdb, not core.</span></span>

<span data-ttu-id="e1a95-144">Example import command:</span><span class="sxs-lookup"><span data-stu-id="e1a95-144">Example import command:</span></span>

```
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.cosmosdb.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

## <a name="migrate-from-table-api-preview-to-table-api"></a><span data-ttu-id="e1a95-145">Migrate from Table API (preview) to Table API</span><span class="sxs-lookup"><span data-stu-id="e1a95-145">Migrate from Table API (preview) to Table API</span></span>

> [!WARNING]
> <span data-ttu-id="e1a95-146">If you want to immediately enjoy the benefits of the generally available tables then please migrate your existing preview tables as specified in this section, otherwise we will be performing auto-migrations for existing preview customers in the coming weeks, note however that auto-migrated preview tables will have certain restrictions to them that newly created tables will not.</span><span class="sxs-lookup"><span data-stu-id="e1a95-146">If you want to immediately enjoy the benefits of the generally available tables then please migrate your existing preview tables as specified in this section, otherwise we will be performing auto-migrations for existing preview customers in the coming weeks, note however that auto-migrated preview tables will have certain restrictions to them that newly created tables will not.</span></span>
> 

<span data-ttu-id="e1a95-147">The Table API is now generally available (GA).</span><span class="sxs-lookup"><span data-stu-id="e1a95-147">The Table API is now generally available (GA).</span></span> <span data-ttu-id="e1a95-148">There are differences between the preview and GA versions of tables both in the code that runs in the cloud as well as in code that runs at the client.</span><span class="sxs-lookup"><span data-stu-id="e1a95-148">There are differences between the preview and GA versions of tables both in the code that runs in the cloud as well as in code that runs at the client.</span></span> <span data-ttu-id="e1a95-149">Therefore it is not advised to try to mix a preview SDK client with a GA Table API account, and vice versa.</span><span class="sxs-lookup"><span data-stu-id="e1a95-149">Therefore it is not advised to try to mix a preview SDK client with a GA Table API account, and vice versa.</span></span> <span data-ttu-id="e1a95-150">Table API preview customers who want to continue to use their existing tables but in a production environment need to migrate from the preview to the GA environment, or wait for auto-migration.</span><span class="sxs-lookup"><span data-stu-id="e1a95-150">Table API preview customers who want to continue to use their existing tables but in a production environment need to migrate from the preview to the GA environment, or wait for auto-migration.</span></span> <span data-ttu-id="e1a95-151">If you wait for auto-migration, you will be notified of the restrictions on the migrated tables.</span><span class="sxs-lookup"><span data-stu-id="e1a95-151">If you wait for auto-migration, you will be notified of the restrictions on the migrated tables.</span></span> <span data-ttu-id="e1a95-152">After migration, you will be able to create new tables on your existing account without restrictions (only migrated tables will have restrictions).</span><span class="sxs-lookup"><span data-stu-id="e1a95-152">After migration, you will be able to create new tables on your existing account without restrictions (only migrated tables will have restrictions).</span></span>

<span data-ttu-id="e1a95-153">To migrate from Table API (preview) to the generally available Table API:</span><span class="sxs-lookup"><span data-stu-id="e1a95-153">To migrate from Table API (preview) to the generally available Table API:</span></span>

1. <span data-ttu-id="e1a95-154">Create a new Azure Cosmos DB account and set its API type to Azure Table as described in [Create a database account](create-table-dotnet.md#create-a-database-account).</span><span class="sxs-lookup"><span data-stu-id="e1a95-154">Create a new Azure Cosmos DB account and set its API type to Azure Table as described in [Create a database account](create-table-dotnet.md#create-a-database-account).</span></span>

2. <span data-ttu-id="e1a95-155">Change clients to use a GA release of the [Table API SDKs](table-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e1a95-155">Change clients to use a GA release of the [Table API SDKs](table-sdk-dotnet.md).</span></span>

3. <span data-ttu-id="e1a95-156">Migrate the client data from preview tables to GA tables by using the Data Migration tool.</span><span class="sxs-lookup"><span data-stu-id="e1a95-156">Migrate the client data from preview tables to GA tables by using the Data Migration tool.</span></span> <span data-ttu-id="e1a95-157">Instructions on using the data migration tool for this purpose are described in [Data Migration tool](#data-migration-tool).</span><span class="sxs-lookup"><span data-stu-id="e1a95-157">Instructions on using the data migration tool for this purpose are described in [Data Migration tool](#data-migration-tool).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e1a95-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1a95-158">Next steps</span></span>

<span data-ttu-id="e1a95-159">In this tutorial you learned how to:</span><span class="sxs-lookup"><span data-stu-id="e1a95-159">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1a95-160">Import data with the Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="e1a95-160">Import data with the Data Migration tool</span></span>
> * <span data-ttu-id="e1a95-161">Import data with AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1a95-161">Import data with AzCopy</span></span>
> * <span data-ttu-id="e1a95-162">Migrate from Table API (preview) to Table API</span><span class="sxs-lookup"><span data-stu-id="e1a95-162">Migrate from Table API (preview) to Table API</span></span>

<span data-ttu-id="e1a95-163">You can now proceed to the next tutorial and learn how to query data using the Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="e1a95-163">You can now proceed to the next tutorial and learn how to query data using the Azure Cosmos DB Table API.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="e1a95-164">How to query data?</span><span class="sxs-lookup"><span data-stu-id="e1a95-164">How to query data?</span></span>](../cosmos-db/tutorial-query-table.md)
