---
title: Database migration tool for Azure Cosmos DB | Microsoft Docs
description: Learn how to use the open-source Azure Cosmos DB data migration tools to import data to Azure Cosmos DB from various sources including MongoDB, SQL Server, Table storage, Amazon DynamoDB, CSV, and JSON files. CSV to JSON conversion.
keywords: csv to json, database migration tools, convert csv to json
services: cosmos-db
author: deborahc
manager: kfile
editor: monicar
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.date: 03/30/2018
ms.author: dech
ms.custom: mvc
ms.openlocfilehash: a40009c174d674e0344b31a2a2b49c5929b95792
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856935"
---
# <a name="use-data-migration-tool-to-migrate-your-data-to-azure-cosmos-db"></a><span data-ttu-id="dd562-105">Use Data migration tool to migrate your data to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="dd562-105">Use Data migration tool to migrate your data to Azure Cosmos DB</span></span> 

<span data-ttu-id="dd562-106">This tutorial provides instructions on using the Azure Cosmos DB Data Migration tool, which can import data from various sources into Azure Cosmos DB collections and tables.</span><span class="sxs-lookup"><span data-stu-id="dd562-106">This tutorial provides instructions on using the Azure Cosmos DB Data Migration tool, which can import data from various sources into Azure Cosmos DB collections and tables.</span></span> <span data-ttu-id="dd562-107">You can import from JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB, and even Azure Cosmos DB SQL API collections, and you migrate that data to collections and tables for use with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd562-107">You can import from JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB, and even Azure Cosmos DB SQL API collections, and you migrate that data to collections and tables for use with Azure Cosmos DB.</span></span> <span data-ttu-id="dd562-108">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the SQL API.</span><span class="sxs-lookup"><span data-stu-id="dd562-108">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the SQL API.</span></span>

<span data-ttu-id="dd562-109">Which API are you going to use with Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="dd562-109">Which API are you going to use with Azure Cosmos DB?</span></span> 

* <span data-ttu-id="dd562-110">**[SQL API](documentdb-introduction.md)** - You can use any of the source options provided in the Data Migration tool to import data.</span><span class="sxs-lookup"><span data-stu-id="dd562-110">**[SQL API](documentdb-introduction.md)** - You can use any of the source options provided in the Data Migration tool to import data.</span></span>
* <span data-ttu-id="dd562-111">**[Table API](table-introduction.md)** - You can use the Data Migration tool or AzCopy to import data.</span><span class="sxs-lookup"><span data-stu-id="dd562-111">**[Table API](table-introduction.md)** - You can use the Data Migration tool or AzCopy to import data.</span></span> <span data-ttu-id="dd562-112">See [Import data for use with the Azure Cosmos DB Table API](table-import.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="dd562-112">See [Import data for use with the Azure Cosmos DB Table API](table-import.md) for more information.</span></span>
* <span data-ttu-id="dd562-113">**[MongoDB API](mongodb-introduction.md)** - The Data Migration tool does not currently support Azure Cosmos DB MongoDB API either as a source or as a target.</span><span class="sxs-lookup"><span data-stu-id="dd562-113">**[MongoDB API](mongodb-introduction.md)** - The Data Migration tool does not currently support Azure Cosmos DB MongoDB API either as a source or as a target.</span></span> <span data-ttu-id="dd562-114">If you want to migrate the data in or out of MongoDB API collections in Azure Cosmos DB, refer to [Azure Cosmos DB: How to migrate data for the MongoDB API](mongodb-migrate.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="dd562-114">If you want to migrate the data in or out of MongoDB API collections in Azure Cosmos DB, refer to [Azure Cosmos DB: How to migrate data for the MongoDB API](mongodb-migrate.md) for instructions.</span></span> <span data-ttu-id="dd562-115">You can still use the Data Migration tool to export data from MongoDB to Azure Cosmos DB SQL API collections for use with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="dd562-115">You can still use the Data Migration tool to export data from MongoDB to Azure Cosmos DB SQL API collections for use with the SQL API.</span></span> 
* <span data-ttu-id="dd562-116">**[Gremlin API](graph-introduction.md)** - The Data Migration tool is not a supported import tool for Gremlin API accounts at this time.</span><span class="sxs-lookup"><span data-stu-id="dd562-116">**[Gremlin API](graph-introduction.md)** - The Data Migration tool is not a supported import tool for Gremlin API accounts at this time.</span></span> 

<span data-ttu-id="dd562-117">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="dd562-117">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd562-118">Installing the Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="dd562-118">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="dd562-119">Importing data from different data sources</span><span class="sxs-lookup"><span data-stu-id="dd562-119">Importing data from different data sources</span></span>
> * <span data-ttu-id="dd562-120">Exporting from Azure Cosmos DB to JSON</span><span class="sxs-lookup"><span data-stu-id="dd562-120">Exporting from Azure Cosmos DB to JSON</span></span>

## <a id="Prerequisites"></a><span data-ttu-id="dd562-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd562-121">Prerequisites</span></span>
<span data-ttu-id="dd562-122">Before following the instructions in this article, ensure that you have the following installed:</span><span class="sxs-lookup"><span data-stu-id="dd562-122">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="dd562-123">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span><span class="sxs-lookup"><span data-stu-id="dd562-123">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

* <span data-ttu-id="dd562-124">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for an individual collection or a set of collections.</span><span class="sxs-lookup"><span data-stu-id="dd562-124">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for an individual collection or a set of collections.</span></span> <span data-ttu-id="dd562-125">Be sure to increase the throughput for larger data migrations.</span><span class="sxs-lookup"><span data-stu-id="dd562-125">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="dd562-126">After you've completed the migration, decrease the throughput to save costs.</span><span class="sxs-lookup"><span data-stu-id="dd562-126">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="dd562-127">For more information about increasing throughput in the Azure portal, see Performance levels and pricing tiers in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd562-127">For more information about increasing throughput in the Azure portal, see Performance levels and pricing tiers in Azure Cosmos DB.</span></span>

## <a id="Overviewl"></a><span data-ttu-id="dd562-128">Overview</span><span class="sxs-lookup"><span data-stu-id="dd562-128">Overview</span></span>
<span data-ttu-id="dd562-129">The Data Migration tool is an open-source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span><span class="sxs-lookup"><span data-stu-id="dd562-129">The Data Migration tool is an open-source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="dd562-130">JSON files</span><span class="sxs-lookup"><span data-stu-id="dd562-130">JSON files</span></span>
* <span data-ttu-id="dd562-131">MongoDB</span><span class="sxs-lookup"><span data-stu-id="dd562-131">MongoDB</span></span>
* <span data-ttu-id="dd562-132">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dd562-132">SQL Server</span></span>
* <span data-ttu-id="dd562-133">CSV files</span><span class="sxs-lookup"><span data-stu-id="dd562-133">CSV files</span></span>
* <span data-ttu-id="dd562-134">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="dd562-134">Azure Table storage</span></span>
* <span data-ttu-id="dd562-135">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="dd562-135">Amazon DynamoDB</span></span>
* <span data-ttu-id="dd562-136">HBase</span><span class="sxs-lookup"><span data-stu-id="dd562-136">HBase</span></span>
* <span data-ttu-id="dd562-137">Azure Cosmos DB collections</span><span class="sxs-lookup"><span data-stu-id="dd562-137">Azure Cosmos DB collections</span></span>

<span data-ttu-id="dd562-138">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command-line (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="dd562-138">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command-line (dt.exe).</span></span> <span data-ttu-id="dd562-139">In fact, there is an option to output the associated command after setting up an import through the UI.</span><span class="sxs-lookup"><span data-stu-id="dd562-139">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="dd562-140">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span><span class="sxs-lookup"><span data-stu-id="dd562-140">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="dd562-141">Keep reading to learn more about source options, sample commands to import from each source, target options, and viewing import results.</span><span class="sxs-lookup"><span data-stu-id="dd562-141">Keep reading to learn more about source options, sample commands to import from each source, target options, and viewing import results.</span></span>

## <a id="Install"></a><span data-ttu-id="dd562-142">Installation</span><span class="sxs-lookup"><span data-stu-id="dd562-142">Installation</span></span>
<span data-ttu-id="dd562-143">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="dd562-143">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span> <span data-ttu-id="dd562-144">You can download and compile the solution locally, or [download a pre-compiled binary](https://cosmosdbportalstorage.blob.core.windows.net/datamigrationtool/2018.02.28-1.8.1/dt-1.8.1.zip), then run either:</span><span class="sxs-lookup"><span data-stu-id="dd562-144">You can download and compile the solution locally, or [download a pre-compiled binary](https://cosmosdbportalstorage.blob.core.windows.net/datamigrationtool/2018.02.28-1.8.1/dt-1.8.1.zip), then run either:</span></span>

* <span data-ttu-id="dd562-145">**Dtui.exe**: Graphical interface version of the tool</span><span class="sxs-lookup"><span data-stu-id="dd562-145">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="dd562-146">**Dt.exe**: Command-line version of the tool</span><span class="sxs-lookup"><span data-stu-id="dd562-146">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="select-data-source"></a><span data-ttu-id="dd562-147">Select data source</span><span class="sxs-lookup"><span data-stu-id="dd562-147">Select data source</span></span>

<span data-ttu-id="dd562-148">Once you've installed the tool, it's time to import your data.</span><span class="sxs-lookup"><span data-stu-id="dd562-148">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="dd562-149">What kind of data do you want to import?</span><span class="sxs-lookup"><span data-stu-id="dd562-149">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="dd562-150">JSON files</span><span class="sxs-lookup"><span data-stu-id="dd562-150">JSON files</span></span>](#JSON)
* [<span data-ttu-id="dd562-151">MongoDB</span><span class="sxs-lookup"><span data-stu-id="dd562-151">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="dd562-152">MongoDB Export files</span><span class="sxs-lookup"><span data-stu-id="dd562-152">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="dd562-153">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dd562-153">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="dd562-154">CSV files</span><span class="sxs-lookup"><span data-stu-id="dd562-154">CSV files</span></span>](#CSV)
* [<span data-ttu-id="dd562-155">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="dd562-155">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="dd562-156">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="dd562-156">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="dd562-157">Blob</span><span class="sxs-lookup"><span data-stu-id="dd562-157">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="dd562-158">Azure Cosmos DB collections</span><span class="sxs-lookup"><span data-stu-id="dd562-158">Azure Cosmos DB collections</span></span>](#SQLSource)
* [<span data-ttu-id="dd562-159">HBase</span><span class="sxs-lookup"><span data-stu-id="dd562-159">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="dd562-160">Azure Cosmos DB bulk import</span><span class="sxs-lookup"><span data-stu-id="dd562-160">Azure Cosmos DB bulk import</span></span>](#SQLBulkTarget)
* [<span data-ttu-id="dd562-161">Azure Cosmos DB sequential record import</span><span class="sxs-lookup"><span data-stu-id="dd562-161">Azure Cosmos DB sequential record import</span></span>](#SQLSeqTarget)


## <a id="JSON"></a><span data-ttu-id="dd562-162">Import JSON files</span><span class="sxs-lookup"><span data-stu-id="dd562-162">Import JSON files</span></span>
<span data-ttu-id="dd562-163">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="dd562-163">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="dd562-164">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span><span class="sxs-lookup"><span data-stu-id="dd562-164">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Screenshot of JSON file source options - Database migration tools](./media/import-data/jsonsource.png)

<span data-ttu-id="dd562-166">Here are some command-line samples to import JSON files:</span><span class="sxs-lookup"><span data-stu-id="dd562-166">Here are some command-line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a><span data-ttu-id="dd562-167">Import from MongoDB</span><span class="sxs-lookup"><span data-stu-id="dd562-167">Import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd562-168">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-168">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="dd562-169">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span><span class="sxs-lookup"><span data-stu-id="dd562-169">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Screenshot of MongoDB source options](./media/import-data/mongodbsource.png)

<span data-ttu-id="dd562-171">The connection string is in the standard MongoDB format:</span><span class="sxs-lookup"><span data-stu-id="dd562-171">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="dd562-172">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-172">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-173">Enter the name of the collection from which data will be imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-173">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="dd562-174">You may optionally specify or provide a file for a query (for example, {pop: {$gt:5000}} ) and/or projection (for example, {loc:0} ) to both filter and shape the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-174">You may optionally specify or provide a file for a query (for example, {pop: {$gt:5000}} ) and/or projection (for example, {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="dd562-175">Here are some command-line samples to import from MongoDB:</span><span class="sxs-lookup"><span data-stu-id="dd562-175">Here are some command-line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a><span data-ttu-id="dd562-176">Import MongoDB export files</span><span class="sxs-lookup"><span data-stu-id="dd562-176">Import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd562-177">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-177">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="dd562-178">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span><span class="sxs-lookup"><span data-stu-id="dd562-178">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Screenshot of MongoDB export source options](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="dd562-180">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span><span class="sxs-lookup"><span data-stu-id="dd562-180">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="dd562-181">Here is a command-line sample to import from MongoDB export JSON files:</span><span class="sxs-lookup"><span data-stu-id="dd562-181">Here is a command-line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a><span data-ttu-id="dd562-182">Import from SQL Server</span><span class="sxs-lookup"><span data-stu-id="dd562-182">Import from SQL Server</span></span>
<span data-ttu-id="dd562-183">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span><span class="sxs-lookup"><span data-stu-id="dd562-183">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="dd562-184">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span><span class="sxs-lookup"><span data-stu-id="dd562-184">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Screenshot of SQL source options - database migration tools](./media/import-data/sqlexportsource.png)

<span data-ttu-id="dd562-186">The format of the connection string is the standard SQL connection string format.</span><span class="sxs-lookup"><span data-stu-id="dd562-186">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="dd562-187">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-187">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-188">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span><span class="sxs-lookup"><span data-stu-id="dd562-188">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="dd562-189">Consider the following SQL query:</span><span class="sxs-lookup"><span data-stu-id="dd562-189">Consider the following SQL query:</span></span>

<span data-ttu-id="dd562-190">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="dd562-190">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="dd562-191">Which returns the following (partial) results:</span><span class="sxs-lookup"><span data-stu-id="dd562-191">Which returns the following (partial) results:</span></span>

![Screenshot of SQL query results](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="dd562-193">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="dd562-193">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="dd562-194">By specifying a nesting separator of '.', the import tool creates Address and Address.Location subdocuments during the import.</span><span class="sxs-lookup"><span data-stu-id="dd562-194">By specifying a nesting separator of '.', the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="dd562-195">Here is an example of a resulting document in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="dd562-195">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="dd562-196">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="dd562-196">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="dd562-197">Here are some command-line samples to import from SQL Server:</span><span class="sxs-lookup"><span data-stu-id="dd562-197">Here are some command-line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a><span data-ttu-id="dd562-198">Import CSV files and convert CSV to JSON</span><span class="sxs-lookup"><span data-stu-id="dd562-198">Import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="dd562-199">The CSV file source importer option enables you to import one or more CSV files.</span><span class="sxs-lookup"><span data-stu-id="dd562-199">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="dd562-200">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span><span class="sxs-lookup"><span data-stu-id="dd562-200">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Screenshot of CSV source options - CSV to JSON](media/import-data/csvsource.png)

<span data-ttu-id="dd562-202">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span><span class="sxs-lookup"><span data-stu-id="dd562-202">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="dd562-203">Consider the following CSV header row and data rows:</span><span class="sxs-lookup"><span data-stu-id="dd562-203">Consider the following CSV header row and data rows:</span></span>

![Screenshot of CSV sample records - CSV to JSON](./media/import-data/csvsample.png)

<span data-ttu-id="dd562-205">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="dd562-205">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="dd562-206">By specifying a nesting separator of '.', the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span><span class="sxs-lookup"><span data-stu-id="dd562-206">By specifying a nesting separator of '.', the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="dd562-207">Here is an example of a resulting document in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="dd562-207">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="dd562-208">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="dd562-208">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="dd562-209">The import tool attempts to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span><span class="sxs-lookup"><span data-stu-id="dd562-209">The import tool attempts to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="dd562-210">Types are identified in the following order: number, datetime, boolean.</span><span class="sxs-lookup"><span data-stu-id="dd562-210">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="dd562-211">There are two other things to note about CSV import:</span><span class="sxs-lookup"><span data-stu-id="dd562-211">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="dd562-212">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span><span class="sxs-lookup"><span data-stu-id="dd562-212">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="dd562-213">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command-line option.</span><span class="sxs-lookup"><span data-stu-id="dd562-213">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command-line option.</span></span>
2. <span data-ttu-id="dd562-214">By default, an unquoted null is treated as a null value.</span><span class="sxs-lookup"><span data-stu-id="dd562-214">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="dd562-215">This behavior can be overridden (that is, treat an unquoted null as a "null" string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command-line option.</span><span class="sxs-lookup"><span data-stu-id="dd562-215">This behavior can be overridden (that is, treat an unquoted null as a "null" string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command-line option.</span></span>

<span data-ttu-id="dd562-216">Here is a command-line sample for CSV import:</span><span class="sxs-lookup"><span data-stu-id="dd562-216">Here is a command-line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a><span data-ttu-id="dd562-217">Import from Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="dd562-217">Import from Azure Table storage</span></span>
<span data-ttu-id="dd562-218">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table.</span><span class="sxs-lookup"><span data-stu-id="dd562-218">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table.</span></span> <span data-ttu-id="dd562-219">Optionally, you can filter the table entities to be imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-219">Optionally, you can filter the table entities to be imported.</span></span> 

<span data-ttu-id="dd562-220">Data imported from Azure Table Storage can be output to Azure Cosmos DB tables and entities, for use with the Table API, or to collections and documents, for use with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="dd562-220">Data imported from Azure Table Storage can be output to Azure Cosmos DB tables and entities, for use with the Table API, or to collections and documents, for use with the SQL API.</span></span> <span data-ttu-id="dd562-221">However; Table API is only available as a target in the command-line utility, you cannot export to Table API by using the Data Migration tool user interface.</span><span class="sxs-lookup"><span data-stu-id="dd562-221">However; Table API is only available as a target in the command-line utility, you cannot export to Table API by using the Data Migration tool user interface.</span></span> <span data-ttu-id="dd562-222">For more information, see [Import data for use with the Azure Cosmos DB Table API](table-import.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-222">For more information, see [Import data for use with the Azure Cosmos DB Table API](table-import.md).</span></span> 

![Screenshot of Azure Table storage source options](./media/import-data/azuretablesource.png)

<span data-ttu-id="dd562-224">The format of the Azure Table storage connection string is:</span><span class="sxs-lookup"><span data-stu-id="dd562-224">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="dd562-225">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-225">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-226">Enter the name of the Azure table from to import from.</span><span class="sxs-lookup"><span data-stu-id="dd562-226">Enter the name of the Azure table from to import from.</span></span> <span data-ttu-id="dd562-227">You may optionally specify a [filter](../vs-azure-tools-table-designer-construct-filter-strings.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-227">You may optionally specify a [filter](../vs-azure-tools-table-designer-construct-filter-strings.md).</span></span>

<span data-ttu-id="dd562-228">The Azure Table storage source importer option has the following additional options:</span><span class="sxs-lookup"><span data-stu-id="dd562-228">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="dd562-229">Include Internal Fields</span><span class="sxs-lookup"><span data-stu-id="dd562-229">Include Internal Fields</span></span>
   1. <span data-ttu-id="dd562-230">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span><span class="sxs-lookup"><span data-stu-id="dd562-230">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="dd562-231">None - Exclude all internal fields</span><span class="sxs-lookup"><span data-stu-id="dd562-231">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="dd562-232">RowKey - Only include the RowKey field</span><span class="sxs-lookup"><span data-stu-id="dd562-232">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="dd562-233">Select Columns</span><span class="sxs-lookup"><span data-stu-id="dd562-233">Select Columns</span></span>
   1. <span data-ttu-id="dd562-234">Azure Table storage filters do not support projections.</span><span class="sxs-lookup"><span data-stu-id="dd562-234">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="dd562-235">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span><span class="sxs-lookup"><span data-stu-id="dd562-235">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="dd562-236">All other entity properties are ignored.</span><span class="sxs-lookup"><span data-stu-id="dd562-236">All other entity properties are ignored.</span></span>

<span data-ttu-id="dd562-237">Here is a command-line sample to import from Azure Table storage:</span><span class="sxs-lookup"><span data-stu-id="dd562-237">Here is a command-line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a><span data-ttu-id="dd562-238">Import from Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="dd562-238">Import from Amazon DynamoDB</span></span>
<span data-ttu-id="dd562-239">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-239">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="dd562-240">Several templates are provided so that setting up an import is as easy as possible.</span><span class="sxs-lookup"><span data-stu-id="dd562-240">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Screenshot of Amazon DynamoDB source options - database migration tools](./media/import-data/dynamodbsource1.png)

![Screenshot of Amazon DynamoDB source options - database migration tools](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="dd562-243">The format of the Amazon DynamoDB connection string is:</span><span class="sxs-lookup"><span data-stu-id="dd562-243">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="dd562-244">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-244">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-245">Here is a command-line sample to import from Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="dd562-245">Here is a command-line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a><span data-ttu-id="dd562-246">Import from Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="dd562-246">Import from Azure Blob storage</span></span>
<span data-ttu-id="dd562-247">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="dd562-247">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="dd562-248">After specifying a Blob container URL and Account Key, provide a regular expression to select the file(s) to import.</span><span class="sxs-lookup"><span data-stu-id="dd562-248">After specifying a Blob container URL and Account Key, provide a regular expression to select the file(s) to import.</span></span>

![Screenshot of Blob file source options](./media/import-data/blobsource.png)

<span data-ttu-id="dd562-250">Here is command-line sample to import JSON files from Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="dd562-250">Here is command-line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="SQLSource"></a><span data-ttu-id="dd562-251">Import from a SQL API collection</span><span class="sxs-lookup"><span data-stu-id="dd562-251">Import from a SQL API collection</span></span>
<span data-ttu-id="dd562-252">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span><span class="sxs-lookup"><span data-stu-id="dd562-252">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Screenshot of Azure Cosmos DB source options](./media/import-data/documentdbsource.png)

<span data-ttu-id="dd562-254">The format of the Azure Cosmos DB connection string is:</span><span class="sxs-lookup"><span data-stu-id="dd562-254">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="dd562-255">The Azure Cosmos DB account connection string can be retrieved from the Keys page of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span><span class="sxs-lookup"><span data-stu-id="dd562-255">The Azure Cosmos DB account connection string can be retrieved from the Keys page of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="dd562-256">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-256">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-257">To import from a single Azure Cosmos DB collection, enter the name of the collection to import data from.</span><span class="sxs-lookup"><span data-stu-id="dd562-257">To import from a single Azure Cosmos DB collection, enter the name of the collection to import data from.</span></span> <span data-ttu-id="dd562-258">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (for example, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="dd562-258">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (for example, collection01 | collection02 | collection03).</span></span> <span data-ttu-id="dd562-259">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-259">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="dd562-260">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span><span class="sxs-lookup"><span data-stu-id="dd562-260">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="dd562-261">The Azure Cosmos DB source importer option has the following advanced options:</span><span class="sxs-lookup"><span data-stu-id="dd562-261">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="dd562-262">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (for example, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="dd562-262">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (for example, _rid, _ts).</span></span>
2. <span data-ttu-id="dd562-263">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="dd562-263">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span></span>
3. <span data-ttu-id="dd562-264">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="dd562-264">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span></span>
4. <span data-ttu-id="dd562-265">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd562-265">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="dd562-266">The available choices are DirectTcp, DirectHttps, and Gateway.</span><span class="sxs-lookup"><span data-stu-id="dd562-266">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="dd562-267">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span><span class="sxs-lookup"><span data-stu-id="dd562-267">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot of Azure Cosmos DB source advanced options](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="dd562-269">The import tool defaults to connection mode DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="dd562-269">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="dd562-270">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span><span class="sxs-lookup"><span data-stu-id="dd562-270">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="dd562-271">Here are some command-line samples to import from Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="dd562-271">Here are some command-line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:DocumentDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:DocumentDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:DocumentDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="dd562-272">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-272">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="dd562-273">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="dd562-273">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <a id="HBaseSource"></a><span data-ttu-id="dd562-274">Import from HBase</span><span class="sxs-lookup"><span data-stu-id="dd562-274">Import from HBase</span></span>
<span data-ttu-id="dd562-275">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span><span class="sxs-lookup"><span data-stu-id="dd562-275">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="dd562-276">Several templates are provided so that setting up an import is as easy as possible.</span><span class="sxs-lookup"><span data-stu-id="dd562-276">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Screenshot of HBase source options](./media/import-data/hbasesource1.png)

![Screenshot of HBase source options](./media/import-data/hbasesource2.png)

<span data-ttu-id="dd562-279">The format of the HBase Stargate connection string is:</span><span class="sxs-lookup"><span data-stu-id="dd562-279">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="dd562-280">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-280">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-281">Here is a command-line sample to import from HBase:</span><span class="sxs-lookup"><span data-stu-id="dd562-281">Here is a command-line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="SQLBulkTarget"></a><span data-ttu-id="dd562-282">Import to the SQL API (Bulk Import)</span><span class="sxs-lookup"><span data-stu-id="dd562-282">Import to the SQL API (Bulk Import)</span></span>
<span data-ttu-id="dd562-283">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span><span class="sxs-lookup"><span data-stu-id="dd562-283">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="dd562-284">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span><span class="sxs-lookup"><span data-stu-id="dd562-284">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="dd562-285">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-285">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="dd562-286">The tool creates, executes, and then deletes the stored procedure from the target collection(s).</span><span class="sxs-lookup"><span data-stu-id="dd562-286">The tool creates, executes, and then deletes the stored procedure from the target collection(s).</span></span>  

![Screenshot of Azure Cosmos DB bulk options](./media/import-data/documentdbbulk.png)

<span data-ttu-id="dd562-288">The format of the Azure Cosmos DB connection string is:</span><span class="sxs-lookup"><span data-stu-id="dd562-288">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="dd562-289">The Azure Cosmos DB account connection string can be retrieved from the Keys page of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span><span class="sxs-lookup"><span data-stu-id="dd562-289">The Azure Cosmos DB account connection string can be retrieved from the Keys page of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="dd562-290">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-290">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-291">To import to a single collection, enter the name of the collection to import data from and click the Add button.</span><span class="sxs-lookup"><span data-stu-id="dd562-291">To import to a single collection, enter the name of the collection to import data from and click the Add button.</span></span> <span data-ttu-id="dd562-292">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="dd562-292">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="dd562-293">When specifying multiple collections via the aforementioned syntax, keep the following guidelines in mind:</span><span class="sxs-lookup"><span data-stu-id="dd562-293">When specifying multiple collections via the aforementioned syntax, keep the following guidelines in mind:</span></span>

1. <span data-ttu-id="dd562-294">Only integer range name patterns are supported.</span><span class="sxs-lookup"><span data-stu-id="dd562-294">Only integer range name patterns are supported.</span></span> <span data-ttu-id="dd562-295">For example, specifying collection[0-3] creates the following collections: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="dd562-295">For example, specifying collection[0-3] creates the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="dd562-296">You can use an abbreviated syntax: collection[3] creates the same set of collections mentioned in step 1.</span><span class="sxs-lookup"><span data-stu-id="dd562-296">You can use an abbreviated syntax: collection[3] creates the same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="dd562-297">More than one substitution can be provided.</span><span class="sxs-lookup"><span data-stu-id="dd562-297">More than one substitution can be provided.</span></span> <span data-ttu-id="dd562-298">For example, collection[0-1] [0-9] generates 20 collection names with leading zeros (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="dd562-298">For example, collection[0-1] [0-9] generates 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="dd562-299">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span><span class="sxs-lookup"><span data-stu-id="dd562-299">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="dd562-300">For best import performance, choose a higher throughput.</span><span class="sxs-lookup"><span data-stu-id="dd562-300">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="dd562-301">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-301">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd562-302">The performance throughput setting only applies to collection creation.</span><span class="sxs-lookup"><span data-stu-id="dd562-302">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="dd562-303">If the specified collection already exists, its throughput is not be modified.</span><span class="sxs-lookup"><span data-stu-id="dd562-303">If the specified collection already exists, its throughput is not be modified.</span></span>
> 
> 

<span data-ttu-id="dd562-304">When importing to multiple collections, the import tool supports hash-based sharding.</span><span class="sxs-lookup"><span data-stu-id="dd562-304">When importing to multiple collections, the import tool supports hash-based sharding.</span></span> <span data-ttu-id="dd562-305">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents are sharded randomly across the target collections).</span><span class="sxs-lookup"><span data-stu-id="dd562-305">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents are sharded randomly across the target collections).</span></span>

<span data-ttu-id="dd562-306">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (if documents do not contain this property, then the import tool generates a GUID as the id property value).</span><span class="sxs-lookup"><span data-stu-id="dd562-306">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (if documents do not contain this property, then the import tool generates a GUID as the id property value).</span></span>

<span data-ttu-id="dd562-307">There are a number of advanced options available during import.</span><span class="sxs-lookup"><span data-stu-id="dd562-307">There are a number of advanced options available during import.</span></span> <span data-ttu-id="dd562-308">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span><span class="sxs-lookup"><span data-stu-id="dd562-308">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Screenshot of Azure Cosmos DB bulk insert sproc option](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="dd562-310">Additionally, when importing date types (for example, from SQL Server or MongoDB), you can choose between three import options:</span><span class="sxs-lookup"><span data-stu-id="dd562-310">Additionally, when importing date types (for example, from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot of Azure Cosmos DB date time import options](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="dd562-312">String: Persist as a string value</span><span class="sxs-lookup"><span data-stu-id="dd562-312">String: Persist as a string value</span></span>
* <span data-ttu-id="dd562-313">Epoch: Persist as an Epoch number value</span><span class="sxs-lookup"><span data-stu-id="dd562-313">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="dd562-314">Both: Persist both string and Epoch number values.</span><span class="sxs-lookup"><span data-stu-id="dd562-314">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="dd562-315">This option creates a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="dd562-315">This option creates a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="dd562-316">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span><span class="sxs-lookup"><span data-stu-id="dd562-316">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="dd562-317">Batch Size: The tool defaults to a batch size of 50.</span><span class="sxs-lookup"><span data-stu-id="dd562-317">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="dd562-318">If the documents to be imported are large, consider lowering the batch size.</span><span class="sxs-lookup"><span data-stu-id="dd562-318">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="dd562-319">Conversely, if the documents to be imported are small, consider raising the batch size.</span><span class="sxs-lookup"><span data-stu-id="dd562-319">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="dd562-320">Max Script Size (bytes): The tool defaults to a max script size of 512 KB.</span><span class="sxs-lookup"><span data-stu-id="dd562-320">Max Script Size (bytes): The tool defaults to a max script size of 512 KB.</span></span>
3. <span data-ttu-id="dd562-321">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span><span class="sxs-lookup"><span data-stu-id="dd562-321">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="dd562-322">Documents missing a unique id field are not imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-322">Documents missing a unique id field are not imported.</span></span>
4. <span data-ttu-id="dd562-323">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span><span class="sxs-lookup"><span data-stu-id="dd562-323">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="dd562-324">Selecting this option allows overwriting existing documents with matching ids.</span><span class="sxs-lookup"><span data-stu-id="dd562-324">Selecting this option allows overwriting existing documents with matching ids.</span></span> <span data-ttu-id="dd562-325">This feature is useful for scheduled data migrations that update existing documents.</span><span class="sxs-lookup"><span data-stu-id="dd562-325">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="dd562-326">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="dd562-326">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span></span>
6. <span data-ttu-id="dd562-327">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="dd562-327">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span></span>
7. <span data-ttu-id="dd562-328">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd562-328">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="dd562-329">The available choices are DirectTcp, DirectHttps, and Gateway.</span><span class="sxs-lookup"><span data-stu-id="dd562-329">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="dd562-330">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span><span class="sxs-lookup"><span data-stu-id="dd562-330">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot of Azure Cosmos DB bulk import advanced options](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="dd562-332">The import tool defaults to connection mode DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="dd562-332">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="dd562-333">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span><span class="sxs-lookup"><span data-stu-id="dd562-333">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <a id="SQLSeqTarget"></a><span data-ttu-id="dd562-334">Import to the SQL API (Sequential Record Import)</span><span class="sxs-lookup"><span data-stu-id="dd562-334">Import to the SQL API (Sequential Record Import)</span></span>
<span data-ttu-id="dd562-335">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span><span class="sxs-lookup"><span data-stu-id="dd562-335">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="dd562-336">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span><span class="sxs-lookup"><span data-stu-id="dd562-336">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="dd562-337">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span><span class="sxs-lookup"><span data-stu-id="dd562-337">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="dd562-338">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-338">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Screenshot of Azure Cosmos DB sequential record import options](./media/import-data/documentdbsequential.png)

<span data-ttu-id="dd562-340">The format of the Azure Cosmos DB connection string is:</span><span class="sxs-lookup"><span data-stu-id="dd562-340">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="dd562-341">The Azure Cosmos DB account connection string can be retrieved from the Keys page of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span><span class="sxs-lookup"><span data-stu-id="dd562-341">The Azure Cosmos DB account connection string can be retrieved from the Keys page of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="dd562-342">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span><span class="sxs-lookup"><span data-stu-id="dd562-342">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="dd562-343">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span><span class="sxs-lookup"><span data-stu-id="dd562-343">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="dd562-344">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="dd562-344">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="dd562-345">When specifying multiple collections via the aforementioned syntax, keep the following guidelines in mind:</span><span class="sxs-lookup"><span data-stu-id="dd562-345">When specifying multiple collections via the aforementioned syntax, keep the following guidelines in mind:</span></span>

1. <span data-ttu-id="dd562-346">Only integer range name patterns are supported.</span><span class="sxs-lookup"><span data-stu-id="dd562-346">Only integer range name patterns are supported.</span></span> <span data-ttu-id="dd562-347">For example, specifying collection[0-3] creates the following collections: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="dd562-347">For example, specifying collection[0-3] creates the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="dd562-348">You can use an abbreviated syntax: collection[3] creates the same set of collections mentioned in step 1.</span><span class="sxs-lookup"><span data-stu-id="dd562-348">You can use an abbreviated syntax: collection[3] creates the same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="dd562-349">More than one substitution can be provided.</span><span class="sxs-lookup"><span data-stu-id="dd562-349">More than one substitution can be provided.</span></span> <span data-ttu-id="dd562-350">For example, collection[0-1] [0-9] creates 20 collection names with leading zeros (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="dd562-350">For example, collection[0-1] [0-9] creates 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="dd562-351">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span><span class="sxs-lookup"><span data-stu-id="dd562-351">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="dd562-352">For best import performance, choose a higher throughput.</span><span class="sxs-lookup"><span data-stu-id="dd562-352">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="dd562-353">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-353">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="dd562-354">Any import to collections with throughput >10,000 RUs require a partition key.</span><span class="sxs-lookup"><span data-stu-id="dd562-354">Any import to collections with throughput >10,000 RUs require a partition key.</span></span> <span data-ttu-id="dd562-355">If you choose to have more than 250,000 RUs, you need to file a request in the portal to have your account increased.</span><span class="sxs-lookup"><span data-stu-id="dd562-355">If you choose to have more than 250,000 RUs, you need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="dd562-356">The throughput setting only applies to collection or database creation.</span><span class="sxs-lookup"><span data-stu-id="dd562-356">The throughput setting only applies to collection or database creation.</span></span> <span data-ttu-id="dd562-357">If the specified collection already exists, its throughput will not be modified.</span><span class="sxs-lookup"><span data-stu-id="dd562-357">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="dd562-358">When importing to multiple collections, the import tool supports hash-based sharding.</span><span class="sxs-lookup"><span data-stu-id="dd562-358">When importing to multiple collections, the import tool supports hash-based sharding.</span></span> <span data-ttu-id="dd562-359">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents are sharded randomly across the target collections).</span><span class="sxs-lookup"><span data-stu-id="dd562-359">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents are sharded randomly across the target collections).</span></span>

<span data-ttu-id="dd562-360">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (if documents do not contain this property, then the import tool generates a GUID as the id property value).</span><span class="sxs-lookup"><span data-stu-id="dd562-360">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (if documents do not contain this property, then the import tool generates a GUID as the id property value).</span></span>

<span data-ttu-id="dd562-361">There are a number of advanced options available during import.</span><span class="sxs-lookup"><span data-stu-id="dd562-361">There are a number of advanced options available during import.</span></span> <span data-ttu-id="dd562-362">First, when importing date types (for example, from SQL Server or MongoDB), you can choose between three import options:</span><span class="sxs-lookup"><span data-stu-id="dd562-362">First, when importing date types (for example, from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot of Azure Cosmos DB date time import options](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="dd562-364">String: Persist as a string value</span><span class="sxs-lookup"><span data-stu-id="dd562-364">String: Persist as a string value</span></span>
* <span data-ttu-id="dd562-365">Epoch: Persist as an Epoch number value</span><span class="sxs-lookup"><span data-stu-id="dd562-365">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="dd562-366">Both: Persist both string and Epoch number values.</span><span class="sxs-lookup"><span data-stu-id="dd562-366">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="dd562-367">This option creates a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="dd562-367">This option creates a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="dd562-368">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span><span class="sxs-lookup"><span data-stu-id="dd562-368">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="dd562-369">Number of Parallel Requests: The tool defaults to two parallel requests.</span><span class="sxs-lookup"><span data-stu-id="dd562-369">Number of Parallel Requests: The tool defaults to two parallel requests.</span></span> <span data-ttu-id="dd562-370">If the documents to be imported are small, consider raising the number of parallel requests.</span><span class="sxs-lookup"><span data-stu-id="dd562-370">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="dd562-371">If this number is raised too much, the import may experience rate limiting.</span><span class="sxs-lookup"><span data-stu-id="dd562-371">If this number is raised too much, the import may experience rate limiting.</span></span>
2. <span data-ttu-id="dd562-372">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span><span class="sxs-lookup"><span data-stu-id="dd562-372">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="dd562-373">Documents missing a unique id field are not imported.</span><span class="sxs-lookup"><span data-stu-id="dd562-373">Documents missing a unique id field are not imported.</span></span>
3. <span data-ttu-id="dd562-374">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span><span class="sxs-lookup"><span data-stu-id="dd562-374">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="dd562-375">Selecting this option allows overwriting existing documents with matching ids.</span><span class="sxs-lookup"><span data-stu-id="dd562-375">Selecting this option allows overwriting existing documents with matching ids.</span></span> <span data-ttu-id="dd562-376">This feature is useful for scheduled data migrations that update existing documents.</span><span class="sxs-lookup"><span data-stu-id="dd562-376">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="dd562-377">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="dd562-377">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span></span>
5. <span data-ttu-id="dd562-378">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="dd562-378">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (for example, network connectivity interruption).</span></span>
6. <span data-ttu-id="dd562-379">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd562-379">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="dd562-380">The available choices are DirectTcp, DirectHttps, and Gateway.</span><span class="sxs-lookup"><span data-stu-id="dd562-380">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="dd562-381">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span><span class="sxs-lookup"><span data-stu-id="dd562-381">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot of Azure Cosmos DB sequential record import advanced options](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="dd562-383">The import tool defaults to connection mode DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="dd562-383">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="dd562-384">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span><span class="sxs-lookup"><span data-stu-id="dd562-384">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <a id="IndexingPolicy"></a><span data-ttu-id="dd562-385">Specify an indexing policy</span><span class="sxs-lookup"><span data-stu-id="dd562-385">Specify an indexing policy</span></span>
<span data-ttu-id="dd562-386">When you allow the migration tool to create Azure Cosmos DB SQL API collections during import, you can specify the indexing policy of the collections.</span><span class="sxs-lookup"><span data-stu-id="dd562-386">When you allow the migration tool to create Azure Cosmos DB SQL API collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="dd562-387">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span><span class="sxs-lookup"><span data-stu-id="dd562-387">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Screenshot of Azure Cosmos DB Indexing Policy advanced options](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="dd562-389">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right-clicking in the indexing policy textbox).</span><span class="sxs-lookup"><span data-stu-id="dd562-389">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right-clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="dd562-390">The policy templates the tool provides are:</span><span class="sxs-lookup"><span data-stu-id="dd562-390">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="dd562-391">Default.</span><span class="sxs-lookup"><span data-stu-id="dd562-391">Default.</span></span> <span data-ttu-id="dd562-392">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span><span class="sxs-lookup"><span data-stu-id="dd562-392">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="dd562-393">This policy has a lower index storage overhead than Range.</span><span class="sxs-lookup"><span data-stu-id="dd562-393">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="dd562-394">Range.</span><span class="sxs-lookup"><span data-stu-id="dd562-394">Range.</span></span> <span data-ttu-id="dd562-395">This policy is best when you’re using ORDER BY, range, and equality queries on both numbers and strings.</span><span class="sxs-lookup"><span data-stu-id="dd562-395">This policy is best when you’re using ORDER BY, range, and equality queries on both numbers and strings.</span></span> <span data-ttu-id="dd562-396">This policy has a higher index storage overhead than Default or Hash.</span><span class="sxs-lookup"><span data-stu-id="dd562-396">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Screenshot of Azure Cosmos DB Indexing Policy advanced options](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="dd562-398">If you do not specify an indexing policy, then the default policy is applied.</span><span class="sxs-lookup"><span data-stu-id="dd562-398">If you do not specify an indexing policy, then the default policy is applied.</span></span> <span data-ttu-id="dd562-399">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="dd562-399">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="dd562-400">Export to JSON file</span><span class="sxs-lookup"><span data-stu-id="dd562-400">Export to JSON file</span></span>
<span data-ttu-id="dd562-401">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="dd562-401">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="dd562-402">The tool handles the export for you, or you can choose to view the resulting migration command and run the command yourself.</span><span class="sxs-lookup"><span data-stu-id="dd562-402">The tool handles the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="dd562-403">The resulting JSON file may be stored locally or in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="dd562-403">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Screenshot of Azure Cosmos DB JSON local file export option](./media/import-data/jsontarget.png)

![Screenshot of Azure Cosmos DB JSON Azure Blob storage export option](./media/import-data/jsontarget2.png)

<span data-ttu-id="dd562-406">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span><span class="sxs-lookup"><span data-stu-id="dd562-406">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="dd562-407">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="dd562-407">Advanced configuration</span></span>
<span data-ttu-id="dd562-408">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span><span class="sxs-lookup"><span data-stu-id="dd562-408">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="dd562-409">The following rules apply to this page:</span><span class="sxs-lookup"><span data-stu-id="dd562-409">The following rules apply to this page:</span></span>

1. <span data-ttu-id="dd562-410">If a file name is not provided, then all errors are returned on the Results page.</span><span class="sxs-lookup"><span data-stu-id="dd562-410">If a file name is not provided, then all errors are returned on the Results page.</span></span>
2. <span data-ttu-id="dd562-411">If a file name is provided without a directory, then the file is created (or overwritten) in the current environment directory.</span><span class="sxs-lookup"><span data-stu-id="dd562-411">If a file name is provided without a directory, then the file is created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="dd562-412">If you select an existing file, then the file is overwritten, there is no append option.</span><span class="sxs-lookup"><span data-stu-id="dd562-412">If you select an existing file, then the file is overwritten, there is no append option.</span></span>
4. <span data-ttu-id="dd562-413">Then, choose whether to log all, critical, or no error messages.</span><span class="sxs-lookup"><span data-stu-id="dd562-413">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="dd562-414">Finally, decide how frequently the on-screen transfer message is updated with its progress.</span><span class="sxs-lookup"><span data-stu-id="dd562-414">Finally, decide how frequently the on-screen transfer message is updated with its progress.</span></span>

   ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="dd562-416">Confirm import settings and view command-line</span><span class="sxs-lookup"><span data-stu-id="dd562-416">Confirm import settings and view command-line</span></span>
1. <span data-ttu-id="dd562-417">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span><span class="sxs-lookup"><span data-stu-id="dd562-417">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Screenshot of summary screen](./media/import-data/summary.png)
   
    ![Screenshot of summary screen](./media/import-data/summarycommand.png)
2. <span data-ttu-id="dd562-420">Once you’re satisfied with your source and target options, click **Import**.</span><span class="sxs-lookup"><span data-stu-id="dd562-420">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="dd562-421">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) update as the import is in process.</span><span class="sxs-lookup"><span data-stu-id="dd562-421">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) update as the import is in process.</span></span> <span data-ttu-id="dd562-422">Once complete, you can export the results (for example, to deal with any import failures).</span><span class="sxs-lookup"><span data-stu-id="dd562-422">Once complete, you can export the results (for example, to deal with any import failures).</span></span>
   
    ![Screenshot of Azure Cosmos DB JSON export option](./media/import-data/viewresults.png)
3. <span data-ttu-id="dd562-424">You may also start a new import, either keeping the existing settings (for example, connection string information, source and target choice, etc.) or resetting all values.</span><span class="sxs-lookup"><span data-stu-id="dd562-424">You may also start a new import, either keeping the existing settings (for example, connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Screenshot of Azure Cosmos DB JSON export option](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="dd562-426">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd562-426">Next steps</span></span>

<span data-ttu-id="dd562-427">In this tutorial, you've done the following tasks:</span><span class="sxs-lookup"><span data-stu-id="dd562-427">In this tutorial, you've done the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd562-428">Installed the Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="dd562-428">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="dd562-429">Imported data from different data sources</span><span class="sxs-lookup"><span data-stu-id="dd562-429">Imported data from different data sources</span></span>
> * <span data-ttu-id="dd562-430">Exported from Azure Cosmos DB to JSON</span><span class="sxs-lookup"><span data-stu-id="dd562-430">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="dd562-431">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd562-431">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="dd562-432">How to query data?</span><span class="sxs-lookup"><span data-stu-id="dd562-432">How to query data?</span></span>](../cosmos-db/tutorial-query-sql-api.md)
