---
title: Database migration tool for DocumentDB | Microsoft Docs
description: Learn how to use the open source DocumentDB data migration tools to import data to DocumentDB from various sources including MongoDB, SQL Server, Table storage, Amazon DynamoDB, CSV, and JSON files. CSV to JSON conversion.
keywords: csv to json, database migration tools, convert csv to json
services: documentdb
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/14/2017
ms.author: anhoh
ms.openlocfilehash: 8edc24afea429b4109152677ceab2fdb96f6f674
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549896"
---
# <a name="import-data-to-documentdb-with-the-database-migration-tool"></a><span data-ttu-id="195ec-105">Import data to DocumentDB with the Database Migration tool</span><span class="sxs-lookup"><span data-stu-id="195ec-105">Import data to DocumentDB with the Database Migration tool</span></span>
> [!div class="op_single_selector"]
> * [Import to DocumentDB](documentdb-import-data.md)
> * [Import to API for MongoDB](documentdb-mongodb-migrate.md)
>
>

<span data-ttu-id="195ec-108">This article shows you how to use the official open source DocumentDB data migration tool to import data to [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and DocumentDB collections.</span><span class="sxs-lookup"><span data-stu-id="195ec-108">This article shows you how to use the official open source DocumentDB data migration tool to import data to [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and DocumentDB collections.</span></span>

<span data-ttu-id="195ec-109">If you are importing data to an API for MongoDB database, follow the instructions in [Migrate data to DocumentDB with protocol support for MongoDB](documentdb-mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="195ec-109">If you are importing data to an API for MongoDB database, follow the instructions in [Migrate data to DocumentDB with protocol support for MongoDB](documentdb-mongodb-migrate.md).</span></span>

<span data-ttu-id="195ec-110">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="195ec-110">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="195ec-111">How can I import JSON file, CSV file, SQL Server data, or MongoDB data to DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="195ec-111">How can I import JSON file, CSV file, SQL Server data, or MongoDB data to DocumentDB?</span></span>
* <span data-ttu-id="195ec-112">How can I import data from Azure Table storage, Amazon DynamoDB, and HBase to DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="195ec-112">How can I import data from Azure Table storage, Amazon DynamoDB, and HBase to DocumentDB?</span></span>
* <span data-ttu-id="195ec-113">How can I migrate data between DocumentDB collections?</span><span class="sxs-lookup"><span data-stu-id="195ec-113">How can I migrate data between DocumentDB collections?</span></span>

## <a id="Prerequisites"></a><span data-ttu-id="195ec-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="195ec-114">Prerequisites</span></span>
<span data-ttu-id="195ec-115">Before following the instructions in this article, ensure that you have the following installed:</span><span class="sxs-lookup"><span data-stu-id="195ec-115">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="195ec-116">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span><span class="sxs-lookup"><span data-stu-id="195ec-116">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <a id="Overviewl"></a><span data-ttu-id="195ec-117">Overview of the DocumentDB Data Migration Tool</span><span class="sxs-lookup"><span data-stu-id="195ec-117">Overview of the DocumentDB Data Migration Tool</span></span>
<span data-ttu-id="195ec-118">The DocumentDB Data Migration tool is an open source solution that imports data to DocumentDB from a variety of sources, including:</span><span class="sxs-lookup"><span data-stu-id="195ec-118">The DocumentDB Data Migration tool is an open source solution that imports data to DocumentDB from a variety of sources, including:</span></span>

* <span data-ttu-id="195ec-119">JSON files</span><span class="sxs-lookup"><span data-stu-id="195ec-119">JSON files</span></span>
* <span data-ttu-id="195ec-120">MongoDB</span><span class="sxs-lookup"><span data-stu-id="195ec-120">MongoDB</span></span>
* <span data-ttu-id="195ec-121">SQL Server</span><span class="sxs-lookup"><span data-stu-id="195ec-121">SQL Server</span></span>
* <span data-ttu-id="195ec-122">CSV files</span><span class="sxs-lookup"><span data-stu-id="195ec-122">CSV files</span></span>
* <span data-ttu-id="195ec-123">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="195ec-123">Azure Table storage</span></span>
* <span data-ttu-id="195ec-124">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="195ec-124">Amazon DynamoDB</span></span>
* <span data-ttu-id="195ec-125">HBase</span><span class="sxs-lookup"><span data-stu-id="195ec-125">HBase</span></span>
* <span data-ttu-id="195ec-126">DocumentDB collections</span><span class="sxs-lookup"><span data-stu-id="195ec-126">DocumentDB collections</span></span>

<span data-ttu-id="195ec-127">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="195ec-127">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="195ec-128">In fact, there is an option to output the associated command after setting up an import through the UI.</span><span class="sxs-lookup"><span data-stu-id="195ec-128">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="195ec-129">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span><span class="sxs-lookup"><span data-stu-id="195ec-129">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="195ec-130">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span><span class="sxs-lookup"><span data-stu-id="195ec-130">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <a id="Install"></a><span data-ttu-id="195ec-131">Installing the DocumentDB Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="195ec-131">Installing the DocumentDB Data Migration tool</span></span>
<span data-ttu-id="195ec-132">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="195ec-132">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="195ec-133">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span><span class="sxs-lookup"><span data-stu-id="195ec-133">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="195ec-134">Then run either:</span><span class="sxs-lookup"><span data-stu-id="195ec-134">Then run either:</span></span>

* <span data-ttu-id="195ec-135">**Dtui.exe**: Graphical interface version of the tool</span><span class="sxs-lookup"><span data-stu-id="195ec-135">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="195ec-136">**Dt.exe**: Command-line version of the tool</span><span class="sxs-lookup"><span data-stu-id="195ec-136">**Dt.exe**: Command-line version of the tool</span></span>

## <a id="JSON"></a><span data-ttu-id="195ec-137">Import JSON files</span><span class="sxs-lookup"><span data-stu-id="195ec-137">Import JSON files</span></span>
<span data-ttu-id="195ec-138">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="195ec-138">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="195ec-139">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span><span class="sxs-lookup"><span data-stu-id="195ec-139">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Screenshot of JSON file source options - Database migration tools](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/jsonsource.png)

<span data-ttu-id="195ec-141">Here are some command line samples to import JSON files:</span><span class="sxs-lookup"><span data-stu-id="195ec-141">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a><span data-ttu-id="195ec-142">Import from MongoDB</span><span class="sxs-lookup"><span data-stu-id="195ec-142">Import from MongoDB</span></span>

> [!IMPORTANT]
> If you are importing to a DocumentDB account with Support for MongoDB, follow these [instructions](documentdb-mongodb-migrate.md).
> 
> 

<span data-ttu-id="195ec-144">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span><span class="sxs-lookup"><span data-stu-id="195ec-144">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Screenshot of MongoDB source options - documentdb vs mongodb](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/mongodbsource.png)

<span data-ttu-id="195ec-146">The connection string is in the standard MongoDB format:</span><span class="sxs-lookup"><span data-stu-id="195ec-146">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-148">Enter the name of the collection from which data will be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-148">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="195ec-149">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-149">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="195ec-150">Here are some command line samples to import from MongoDB:</span><span class="sxs-lookup"><span data-stu-id="195ec-150">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a><span data-ttu-id="195ec-151">Import MongoDB export files</span><span class="sxs-lookup"><span data-stu-id="195ec-151">Import MongoDB export files</span></span>

> [!IMPORTANT]
> If you are importing to a DocumentDB account with Support for MongoDB, follow these [instructions](documentdb-mongodb-migrate.md).
> 
> 

<span data-ttu-id="195ec-153">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span><span class="sxs-lookup"><span data-stu-id="195ec-153">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Screenshot of MongoDB export source options - documentdb vs mongodb](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/mongodbexportsource.png)

<span data-ttu-id="195ec-155">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span><span class="sxs-lookup"><span data-stu-id="195ec-155">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="195ec-156">Here is a command line sample to import from MongoDB export JSON files:</span><span class="sxs-lookup"><span data-stu-id="195ec-156">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a><span data-ttu-id="195ec-157">Import from SQL Server</span><span class="sxs-lookup"><span data-stu-id="195ec-157">Import from SQL Server</span></span>
<span data-ttu-id="195ec-158">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span><span class="sxs-lookup"><span data-stu-id="195ec-158">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="195ec-159">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span><span class="sxs-lookup"><span data-stu-id="195ec-159">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Screenshot of SQL source options - database migration tools](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/sqlexportsource.png)

<span data-ttu-id="195ec-161">The format of the connection string is the standard SQL connection string format.</span><span class="sxs-lookup"><span data-stu-id="195ec-161">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-163">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span><span class="sxs-lookup"><span data-stu-id="195ec-163">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="195ec-164">Consider the following SQL query:</span><span class="sxs-lookup"><span data-stu-id="195ec-164">Consider the following SQL query:</span></span>

<span data-ttu-id="195ec-165">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="195ec-165">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="195ec-166">Which returns the following (partial) results:</span><span class="sxs-lookup"><span data-stu-id="195ec-166">Which returns the following (partial) results:</span></span>

![Screenshot of SQL query results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/sqlqueryresults.png)

<span data-ttu-id="195ec-168">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="195ec-168">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="195ec-169">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span><span class="sxs-lookup"><span data-stu-id="195ec-169">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="195ec-170">Here is an example of a resulting document in DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="195ec-170">Here is an example of a resulting document in DocumentDB:</span></span>

<span data-ttu-id="195ec-171">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="195ec-171">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="195ec-172">Here are some command line samples to import from SQL Server:</span><span class="sxs-lookup"><span data-stu-id="195ec-172">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a><span data-ttu-id="195ec-173">Import CSV files - Convert CSV to JSON</span><span class="sxs-lookup"><span data-stu-id="195ec-173">Import CSV files - Convert CSV to JSON</span></span>
<span data-ttu-id="195ec-174">The CSV file source importer option enables you to import one or more CSV files.</span><span class="sxs-lookup"><span data-stu-id="195ec-174">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="195ec-175">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span><span class="sxs-lookup"><span data-stu-id="195ec-175">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Screenshot of CSV source options - CSV to JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/csvsource.png)

<span data-ttu-id="195ec-177">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span><span class="sxs-lookup"><span data-stu-id="195ec-177">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="195ec-178">Consider the following CSV header row and data rows:</span><span class="sxs-lookup"><span data-stu-id="195ec-178">Consider the following CSV header row and data rows:</span></span>

![Screenshot of CSV sample records - CSV to JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/csvsample.png)

<span data-ttu-id="195ec-180">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="195ec-180">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="195ec-181">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span><span class="sxs-lookup"><span data-stu-id="195ec-181">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="195ec-182">Here is an example of a resulting document in DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="195ec-182">Here is an example of a resulting document in DocumentDB:</span></span>

<span data-ttu-id="195ec-183">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="195ec-183">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="195ec-184">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span><span class="sxs-lookup"><span data-stu-id="195ec-184">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="195ec-185">Types are identified in the following order: number, datetime, boolean.</span><span class="sxs-lookup"><span data-stu-id="195ec-185">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="195ec-186">There are two other things to note about CSV import:</span><span class="sxs-lookup"><span data-stu-id="195ec-186">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="195ec-187">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span><span class="sxs-lookup"><span data-stu-id="195ec-187">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="195ec-188">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span><span class="sxs-lookup"><span data-stu-id="195ec-188">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="195ec-189">By default, an unquoted null is treated as a null value.</span><span class="sxs-lookup"><span data-stu-id="195ec-189">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="195ec-190">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span><span class="sxs-lookup"><span data-stu-id="195ec-190">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="195ec-191">Here is a command line sample for CSV import:</span><span class="sxs-lookup"><span data-stu-id="195ec-191">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a><span data-ttu-id="195ec-192">Import from Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="195ec-192">Import from Azure Table storage</span></span>
<span data-ttu-id="195ec-193">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-193">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span>  

![Screenshot of Azure Table storage source options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/azuretablesource.png)

<span data-ttu-id="195ec-195">The format of the Azure Table storage connection string is:</span><span class="sxs-lookup"><span data-stu-id="195ec-195">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-197">Enter the name of the Azure table from which data will be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-197">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="195ec-198">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="195ec-198">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="195ec-199">The Azure Table storage source importer option has the following additional options:</span><span class="sxs-lookup"><span data-stu-id="195ec-199">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="195ec-200">Include Internal Fields</span><span class="sxs-lookup"><span data-stu-id="195ec-200">Include Internal Fields</span></span>
   1. <span data-ttu-id="195ec-201">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span><span class="sxs-lookup"><span data-stu-id="195ec-201">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="195ec-202">None - Exclude all internal fields</span><span class="sxs-lookup"><span data-stu-id="195ec-202">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="195ec-203">RowKey - Only include the RowKey field</span><span class="sxs-lookup"><span data-stu-id="195ec-203">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="195ec-204">Select Columns</span><span class="sxs-lookup"><span data-stu-id="195ec-204">Select Columns</span></span>
   1. <span data-ttu-id="195ec-205">Azure Table storage filters do not support projections.</span><span class="sxs-lookup"><span data-stu-id="195ec-205">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="195ec-206">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span><span class="sxs-lookup"><span data-stu-id="195ec-206">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="195ec-207">All other entity properties will be ignored.</span><span class="sxs-lookup"><span data-stu-id="195ec-207">All other entity properties will be ignored.</span></span>

<span data-ttu-id="195ec-208">Here is a command line sample to import from Azure Table storage:</span><span class="sxs-lookup"><span data-stu-id="195ec-208">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a><span data-ttu-id="195ec-209">Import from Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="195ec-209">Import from Amazon DynamoDB</span></span>
<span data-ttu-id="195ec-210">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-210">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="195ec-211">Several templates are provided so that setting up an import is as easy as possible.</span><span class="sxs-lookup"><span data-stu-id="195ec-211">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Screenshot of Amazon DynamoDB source options - database migration tools](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/dynamodbsource1.png)

![Screenshot of Amazon DynamoDB source options - database migration tools](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/dynamodbsource2.png)

<span data-ttu-id="195ec-214">The format of the Amazon DynamoDB connection string is:</span><span class="sxs-lookup"><span data-stu-id="195ec-214">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-216">Here is a command line sample to import from Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="195ec-216">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a><span data-ttu-id="195ec-217">Import files from Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="195ec-217">Import files from Azure Blob storage</span></span>
<span data-ttu-id="195ec-218">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="195ec-218">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="195ec-219">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span><span class="sxs-lookup"><span data-stu-id="195ec-219">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Screenshot of Blob file source options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/blobsource.png)

<span data-ttu-id="195ec-221">Here is command line sample to import JSON files from Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="195ec-221">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a><span data-ttu-id="195ec-222">Import from DocumentDB</span><span class="sxs-lookup"><span data-stu-id="195ec-222">Import from DocumentDB</span></span>
<span data-ttu-id="195ec-223">The DocumentDB source importer option allows you to import data from one or more DocumentDB collections and optionally filter documents using a query.</span><span class="sxs-lookup"><span data-stu-id="195ec-223">The DocumentDB source importer option allows you to import data from one or more DocumentDB collections and optionally filter documents using a query.</span></span>  

![Screenshot of DocumentDB source options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/documentdbsource.png)

<span data-ttu-id="195ec-225">The format of the DocumentDB connection string is:</span><span class="sxs-lookup"><span data-stu-id="195ec-225">The format of the DocumentDB connection string is:</span></span>

    AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;

<span data-ttu-id="195ec-226">The DocumentDB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage a DocumentDB account](documentdb-manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span><span class="sxs-lookup"><span data-stu-id="195ec-226">The DocumentDB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage a DocumentDB account](documentdb-manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<DocumentDB Database>;

> [!NOTE]
> Use the Verify command to ensure that the DocumentDB instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-228">To import from a single DocumentDB collection, enter the name of the collection from which data will be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-228">To import from a single DocumentDB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="195ec-229">To import from multiple DocumentDB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="195ec-229">To import from multiple DocumentDB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="195ec-230">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-230">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.
> 
> 

<span data-ttu-id="195ec-232">The DocumentDB source importer option has the following advanced options:</span><span class="sxs-lookup"><span data-stu-id="195ec-232">The DocumentDB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="195ec-233">Include Internal Fields: Specifies whether or not to include DocumentDB document system properties in the export (e.g. _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="195ec-233">Include Internal Fields: Specifies whether or not to include DocumentDB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="195ec-234">Number of Retries on Failure: Specifies the number of times to retry the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="195ec-234">Number of Retries on Failure: Specifies the number of times to retry the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="195ec-235">Retry Interval: Specifies how long to wait between retrying the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="195ec-235">Retry Interval: Specifies how long to wait between retrying the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="195ec-236">Connection Mode: Specifies the connection mode to use with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="195ec-236">Connection Mode: Specifies the connection mode to use with DocumentDB.</span></span> <span data-ttu-id="195ec-237">The available choices are DirectTcp, DirectHttps, and Gateway.</span><span class="sxs-lookup"><span data-stu-id="195ec-237">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="195ec-238">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span><span class="sxs-lookup"><span data-stu-id="195ec-238">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot of DocumentDB source advanced options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/documentdbsourceoptions.png)

> [!TIP]
> The import tool defaults to connection mode DirectTcp. If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.
> 
> 

<span data-ttu-id="195ec-242">Here are some command line samples to import from DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="195ec-242">Here are some command line samples to import from DocumentDB:</span></span>

    #Migrate data from one DocumentDB collection to another DocumentDB collections
    dt.exe /s:DocumentDB /s.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /s.Collection:TEColl /t:DocumentDBBulk /t.ConnectionString:" AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple DocumentDB collections to a single DocumentDB collection
    dt.exe /s:DocumentDB /s.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export a DocumentDB collection to a JSON file
    dt.exe /s:DocumentDB /s.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> The DocumentDB Data Import Tool also supports import of data from the [DocumentDB Emulator](documentdb-nosql-local-emulator.md). When importing data from a local emulator, set the endpoint to https://localhost:<port>. 
> 
> 

## <a id="HBaseSource"></a><span data-ttu-id="195ec-245">Import from HBase</span><span class="sxs-lookup"><span data-stu-id="195ec-245">Import from HBase</span></span>
<span data-ttu-id="195ec-246">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span><span class="sxs-lookup"><span data-stu-id="195ec-246">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="195ec-247">Several templates are provided so that setting up an import is as easy as possible.</span><span class="sxs-lookup"><span data-stu-id="195ec-247">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Screenshot of HBase source options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/hbasesource1.png)

![Screenshot of HBase source options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/hbasesource2.png)

<span data-ttu-id="195ec-250">The format of the HBase Stargate connection string is:</span><span class="sxs-lookup"><span data-stu-id="195ec-250">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-252">Here is a command line sample to import from HBase:</span><span class="sxs-lookup"><span data-stu-id="195ec-252">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a><span data-ttu-id="195ec-253">Import to DocumentDB (Bulk Import)</span><span class="sxs-lookup"><span data-stu-id="195ec-253">Import to DocumentDB (Bulk Import)</span></span>
<span data-ttu-id="195ec-254">The DocumentDB Bulk importer allows you to import from any of the available source options, using a DocumentDB stored procedure for efficiency.</span><span class="sxs-lookup"><span data-stu-id="195ec-254">The DocumentDB Bulk importer allows you to import from any of the available source options, using a DocumentDB stored procedure for efficiency.</span></span> <span data-ttu-id="195ec-255">The tool supports import to one single-partitioned DocumentDB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned DocumentDB collections.</span><span class="sxs-lookup"><span data-stu-id="195ec-255">The tool supports import to one single-partitioned DocumentDB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned DocumentDB collections.</span></span> <span data-ttu-id="195ec-256">For more information about partitioning data, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="195ec-256">For more information about partitioning data, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).</span></span> <span data-ttu-id="195ec-257">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span><span class="sxs-lookup"><span data-stu-id="195ec-257">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Screenshot of DocumentDB bulk options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/documentdbbulk.png)

<span data-ttu-id="195ec-259">The format of the DocumentDB connection string is:</span><span class="sxs-lookup"><span data-stu-id="195ec-259">The format of the DocumentDB connection string is:</span></span>

    AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;

<span data-ttu-id="195ec-260">The DocumentDB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage a DocumentDB account](documentdb-manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span><span class="sxs-lookup"><span data-stu-id="195ec-260">The DocumentDB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage a DocumentDB account](documentdb-manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<DocumentDB Database>;

> [!NOTE]
> Use the Verify command to ensure that the DocumentDB instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-262">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span><span class="sxs-lookup"><span data-stu-id="195ec-262">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="195ec-263">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="195ec-263">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="195ec-264">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span><span class="sxs-lookup"><span data-stu-id="195ec-264">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="195ec-265">Only integer range name patterns are supported.</span><span class="sxs-lookup"><span data-stu-id="195ec-265">Only integer range name patterns are supported.</span></span> <span data-ttu-id="195ec-266">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="195ec-266">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="195ec-267">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span><span class="sxs-lookup"><span data-stu-id="195ec-267">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="195ec-268">More than one substitution can be provided.</span><span class="sxs-lookup"><span data-stu-id="195ec-268">More than one substitution can be provided.</span></span> <span data-ttu-id="195ec-269">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="195ec-269">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="195ec-270">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span><span class="sxs-lookup"><span data-stu-id="195ec-270">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="195ec-271">For best import performance, choose a higher throughput.</span><span class="sxs-lookup"><span data-stu-id="195ec-271">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="195ec-272">For more information about performance levels, see [Performance levels in DocumentDB](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="195ec-272">For more information about performance levels, see [Performance levels in DocumentDB](documentdb-performance-levels.md).</span></span>

> [!NOTE]
> The performance throughput setting only applies to collection creation. If the specified collection already exists, its throughput will not be modified.
> 
> 

<span data-ttu-id="195ec-275">When importing to multiple collections, the import tool supports hash based sharding.</span><span class="sxs-lookup"><span data-stu-id="195ec-275">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="195ec-276">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span><span class="sxs-lookup"><span data-stu-id="195ec-276">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="195ec-277">You may optionally specify which field in the import source should be used as the DocumentDB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span><span class="sxs-lookup"><span data-stu-id="195ec-277">You may optionally specify which field in the import source should be used as the DocumentDB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="195ec-278">There are a number of advanced options available during import.</span><span class="sxs-lookup"><span data-stu-id="195ec-278">There are a number of advanced options available during import.</span></span> <span data-ttu-id="195ec-279">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span><span class="sxs-lookup"><span data-stu-id="195ec-279">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Screenshot of DocumentDB bulk insert sproc option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/bulkinsertsp.png)

<span data-ttu-id="195ec-281">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span><span class="sxs-lookup"><span data-stu-id="195ec-281">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot of DocumentDB date time import options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/datetimeoptions.png)

* <span data-ttu-id="195ec-283">String: Persist as a string value</span><span class="sxs-lookup"><span data-stu-id="195ec-283">String: Persist as a string value</span></span>
* <span data-ttu-id="195ec-284">Epoch: Persist as an Epoch number value</span><span class="sxs-lookup"><span data-stu-id="195ec-284">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="195ec-285">Both: Persist both string and Epoch number values.</span><span class="sxs-lookup"><span data-stu-id="195ec-285">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="195ec-286">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="195ec-286">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="195ec-287">The DocumentDB Bulk importer has the following additional advanced options:</span><span class="sxs-lookup"><span data-stu-id="195ec-287">The DocumentDB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="195ec-288">Batch Size: The tool defaults to a batch size of 50.</span><span class="sxs-lookup"><span data-stu-id="195ec-288">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="195ec-289">If the documents to be imported are large, consider lowering the batch size.</span><span class="sxs-lookup"><span data-stu-id="195ec-289">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="195ec-290">Conversely, if the documents to be imported are small, consider raising the batch size.</span><span class="sxs-lookup"><span data-stu-id="195ec-290">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="195ec-291">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span><span class="sxs-lookup"><span data-stu-id="195ec-291">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="195ec-292">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span><span class="sxs-lookup"><span data-stu-id="195ec-292">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="195ec-293">Documents missing a unique id field will not be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-293">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="195ec-294">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span><span class="sxs-lookup"><span data-stu-id="195ec-294">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="195ec-295">Selecting this option will allow overwriting existing documents with matching ids.</span><span class="sxs-lookup"><span data-stu-id="195ec-295">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="195ec-296">This feature is useful for scheduled data migrations that update existing documents.</span><span class="sxs-lookup"><span data-stu-id="195ec-296">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="195ec-297">Number of Retries on Failure: Specifies the number of times to retry the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="195ec-297">Number of Retries on Failure: Specifies the number of times to retry the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="195ec-298">Retry Interval: Specifies how long to wait between retrying the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="195ec-298">Retry Interval: Specifies how long to wait between retrying the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="195ec-299">Connection Mode: Specifies the connection mode to use with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="195ec-299">Connection Mode: Specifies the connection mode to use with DocumentDB.</span></span> <span data-ttu-id="195ec-300">The available choices are DirectTcp, DirectHttps, and Gateway.</span><span class="sxs-lookup"><span data-stu-id="195ec-300">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="195ec-301">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span><span class="sxs-lookup"><span data-stu-id="195ec-301">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot of DocumentDB bulk import advanced options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/docdbbulkoptions.png)

> [!TIP]
> The import tool defaults to connection mode DirectTcp. If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a><span data-ttu-id="195ec-305">Import to DocumentDB (Sequential Record Import)</span><span class="sxs-lookup"><span data-stu-id="195ec-305">Import to DocumentDB (Sequential Record Import)</span></span>
<span data-ttu-id="195ec-306">The DocumentDB sequential record importer allows you to import from any of the available source options on a record by record basis.</span><span class="sxs-lookup"><span data-stu-id="195ec-306">The DocumentDB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="195ec-307">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span><span class="sxs-lookup"><span data-stu-id="195ec-307">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="195ec-308">The tool supports import to a single (both single-partition and multi-partition) DocumentDB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition DocumentDB collections.</span><span class="sxs-lookup"><span data-stu-id="195ec-308">The tool supports import to a single (both single-partition and multi-partition) DocumentDB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition DocumentDB collections.</span></span> <span data-ttu-id="195ec-309">For more information about partitioning data, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="195ec-309">For more information about partitioning data, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).</span></span>

![Screenshot of DocumentDB sequential record import options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/documentdbsequential.png)

<span data-ttu-id="195ec-311">The format of the DocumentDB connection string is:</span><span class="sxs-lookup"><span data-stu-id="195ec-311">The format of the DocumentDB connection string is:</span></span>

    AccountEndpoint=<DocumentDB Endpoint>;AccountKey=<DocumentDB Key>;Database=<DocumentDB Database>;

<span data-ttu-id="195ec-312">The DocumentDB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage a DocumentDB account](documentdb-manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span><span class="sxs-lookup"><span data-stu-id="195ec-312">The DocumentDB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage a DocumentDB account](documentdb-manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<DocumentDB Database>;

> [!NOTE]
> Use the Verify command to ensure that the DocumentDB instance specified in the connection string field can be accessed.
> 
> 

<span data-ttu-id="195ec-314">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span><span class="sxs-lookup"><span data-stu-id="195ec-314">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="195ec-315">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="195ec-315">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="195ec-316">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span><span class="sxs-lookup"><span data-stu-id="195ec-316">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="195ec-317">Only integer range name patterns are supported.</span><span class="sxs-lookup"><span data-stu-id="195ec-317">Only integer range name patterns are supported.</span></span> <span data-ttu-id="195ec-318">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="195ec-318">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="195ec-319">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span><span class="sxs-lookup"><span data-stu-id="195ec-319">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="195ec-320">More than one substitution can be provided.</span><span class="sxs-lookup"><span data-stu-id="195ec-320">More than one substitution can be provided.</span></span> <span data-ttu-id="195ec-321">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="195ec-321">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="195ec-322">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span><span class="sxs-lookup"><span data-stu-id="195ec-322">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="195ec-323">For best import performance, choose a higher throughput.</span><span class="sxs-lookup"><span data-stu-id="195ec-323">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="195ec-324">For more information about performance levels, see [Performance levels in DocumentDB](documentdb-performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="195ec-324">For more information about performance levels, see [Performance levels in DocumentDB](documentdb-performance-levels.md).</span></span> <span data-ttu-id="195ec-325">Any import to collections with throughput >10,000 RUs will require a partition key.</span><span class="sxs-lookup"><span data-stu-id="195ec-325">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="195ec-326">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span><span class="sxs-lookup"><span data-stu-id="195ec-326">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> The throughput setting only applies to collection creation. If the specified collection already exists, its throughput will not be modified.
> 
> 

<span data-ttu-id="195ec-329">When importing to multiple collections, the import tool supports hash based sharding.</span><span class="sxs-lookup"><span data-stu-id="195ec-329">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="195ec-330">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span><span class="sxs-lookup"><span data-stu-id="195ec-330">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="195ec-331">You may optionally specify which field in the import source should be used as the DocumentDB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span><span class="sxs-lookup"><span data-stu-id="195ec-331">You may optionally specify which field in the import source should be used as the DocumentDB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="195ec-332">There are a number of advanced options available during import.</span><span class="sxs-lookup"><span data-stu-id="195ec-332">There are a number of advanced options available during import.</span></span> <span data-ttu-id="195ec-333">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span><span class="sxs-lookup"><span data-stu-id="195ec-333">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot of DocumentDB date time import options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/datetimeoptions.png)

* <span data-ttu-id="195ec-335">String: Persist as a string value</span><span class="sxs-lookup"><span data-stu-id="195ec-335">String: Persist as a string value</span></span>
* <span data-ttu-id="195ec-336">Epoch: Persist as an Epoch number value</span><span class="sxs-lookup"><span data-stu-id="195ec-336">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="195ec-337">Both: Persist both string and Epoch number values.</span><span class="sxs-lookup"><span data-stu-id="195ec-337">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="195ec-338">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="195ec-338">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="195ec-339">The DocumentDB - Sequential record importer has the following additional advanced options:</span><span class="sxs-lookup"><span data-stu-id="195ec-339">The DocumentDB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="195ec-340">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span><span class="sxs-lookup"><span data-stu-id="195ec-340">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="195ec-341">If the documents to be imported are small, consider raising the number of parallel requests.</span><span class="sxs-lookup"><span data-stu-id="195ec-341">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="195ec-342">Note that if this number is raised too much, the import may experience throttling.</span><span class="sxs-lookup"><span data-stu-id="195ec-342">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="195ec-343">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span><span class="sxs-lookup"><span data-stu-id="195ec-343">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="195ec-344">Documents missing a unique id field will not be imported.</span><span class="sxs-lookup"><span data-stu-id="195ec-344">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="195ec-345">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span><span class="sxs-lookup"><span data-stu-id="195ec-345">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="195ec-346">Selecting this option will allow overwriting existing documents with matching ids.</span><span class="sxs-lookup"><span data-stu-id="195ec-346">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="195ec-347">This feature is useful for scheduled data migrations that update existing documents.</span><span class="sxs-lookup"><span data-stu-id="195ec-347">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="195ec-348">Number of Retries on Failure: Specifies the number of times to retry the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="195ec-348">Number of Retries on Failure: Specifies the number of times to retry the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="195ec-349">Retry Interval: Specifies how long to wait between retrying the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span><span class="sxs-lookup"><span data-stu-id="195ec-349">Retry Interval: Specifies how long to wait between retrying the connection to DocumentDB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="195ec-350">Connection Mode: Specifies the connection mode to use with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="195ec-350">Connection Mode: Specifies the connection mode to use with DocumentDB.</span></span> <span data-ttu-id="195ec-351">The available choices are DirectTcp, DirectHttps, and Gateway.</span><span class="sxs-lookup"><span data-stu-id="195ec-351">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="195ec-352">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span><span class="sxs-lookup"><span data-stu-id="195ec-352">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot of DocumentDB sequential record import advanced options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/documentdbsequentialoptions.png)

> [!TIP]
> The import tool defaults to connection mode DirectTcp. If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.
> 
> 

## <a id="IndexingPolicy"></a><span data-ttu-id="195ec-356">Specify an indexing policy when creating DocumentDB collections</span><span class="sxs-lookup"><span data-stu-id="195ec-356">Specify an indexing policy when creating DocumentDB collections</span></span>
<span data-ttu-id="195ec-357">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span><span class="sxs-lookup"><span data-stu-id="195ec-357">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="195ec-358">In the advanced options section of the DocumentDB Bulk import and DocumentDB Sequential record options, navigate to the Indexing Policy section.</span><span class="sxs-lookup"><span data-stu-id="195ec-358">In the advanced options section of the DocumentDB Bulk import and DocumentDB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Screenshot of DocumentDB Indexing Policy advanced options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/indexingpolicy1.png)

<span data-ttu-id="195ec-360">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span><span class="sxs-lookup"><span data-stu-id="195ec-360">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="195ec-361">The policy templates the tool provides are:</span><span class="sxs-lookup"><span data-stu-id="195ec-361">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="195ec-362">Default.</span><span class="sxs-lookup"><span data-stu-id="195ec-362">Default.</span></span> <span data-ttu-id="195ec-363">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span><span class="sxs-lookup"><span data-stu-id="195ec-363">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="195ec-364">This policy has a lower index storage overhead than Range.</span><span class="sxs-lookup"><span data-stu-id="195ec-364">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="195ec-365">Range.</span><span class="sxs-lookup"><span data-stu-id="195ec-365">Range.</span></span> <span data-ttu-id="195ec-366">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span><span class="sxs-lookup"><span data-stu-id="195ec-366">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="195ec-367">This policy has a higher index storage overhead than Default or Hash.</span><span class="sxs-lookup"><span data-stu-id="195ec-367">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Screenshot of DocumentDB Indexing Policy advanced options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/indexingpolicy2.png)

> [!NOTE]
> If you do not specify an indexing policy, then the default policy will be applied. For more information about indexing policies, see [DocumentDB indexing policies](documentdb-indexing-policies.md).
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="195ec-371">Export to JSON file</span><span class="sxs-lookup"><span data-stu-id="195ec-371">Export to JSON file</span></span>
<span data-ttu-id="195ec-372">The DocumentDB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span><span class="sxs-lookup"><span data-stu-id="195ec-372">The DocumentDB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="195ec-373">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span><span class="sxs-lookup"><span data-stu-id="195ec-373">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="195ec-374">The resulting JSON file may be stored locally or in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="195ec-374">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Screenshot of DocumentDB JSON local file export option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/jsontarget.png)

![Screenshot of DocumentDB JSON Azure Blob storage export option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/jsontarget2.png)

<span data-ttu-id="195ec-377">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span><span class="sxs-lookup"><span data-stu-id="195ec-377">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in DocumentDB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

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
    "Content": "Don's document in DocumentDB is a valid JSON document as defined by the JSON spec.",
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

## <a name="advanced-configuration"></a><span data-ttu-id="195ec-378">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="195ec-378">Advanced configuration</span></span>
<span data-ttu-id="195ec-379">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span><span class="sxs-lookup"><span data-stu-id="195ec-379">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="195ec-380">The following rules apply to this page:</span><span class="sxs-lookup"><span data-stu-id="195ec-380">The following rules apply to this page:</span></span>

1. <span data-ttu-id="195ec-381">If a file name is not provided, then all errors will be returned on the Results page.</span><span class="sxs-lookup"><span data-stu-id="195ec-381">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="195ec-382">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span><span class="sxs-lookup"><span data-stu-id="195ec-382">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="195ec-383">If you select an existing file, then the file will be overwritten, there is no append option.</span><span class="sxs-lookup"><span data-stu-id="195ec-383">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="195ec-384">Then, choose whether to log all, critical, or no error messages.</span><span class="sxs-lookup"><span data-stu-id="195ec-384">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="195ec-385">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span><span class="sxs-lookup"><span data-stu-id="195ec-385">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="195ec-386">Confirm import settings and view command line</span><span class="sxs-lookup"><span data-stu-id="195ec-386">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="195ec-387">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span><span class="sxs-lookup"><span data-stu-id="195ec-387">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Screenshot of summary screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/summary.png)
   
    ![Screenshot of summary screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/summarycommand.png)
2. <span data-ttu-id="195ec-390">Once you’re satisfied with your source and target options, click **Import**.</span><span class="sxs-lookup"><span data-stu-id="195ec-390">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="195ec-391">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span><span class="sxs-lookup"><span data-stu-id="195ec-391">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="195ec-392">Once complete, you can export the results (e.g. to deal with any import failures).</span><span class="sxs-lookup"><span data-stu-id="195ec-392">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Screenshot of DocumentDB JSON export option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/viewresults.png)
3. <span data-ttu-id="195ec-394">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span><span class="sxs-lookup"><span data-stu-id="195ec-394">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Screenshot of DocumentDB JSON export option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="195ec-396">Next steps</span><span class="sxs-lookup"><span data-stu-id="195ec-396">Next steps</span></span>
* <span data-ttu-id="195ec-397">To learn more about DocumentDB, see the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="195ec-397">To learn more about DocumentDB, see the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/documentdb/).</span></span>
































