---
title: 'Azure DocumentDB portal tool: Document Explorer | Microsoft Docs'
description: Learn about the DocumentDB Document Explorer, an Azure Portal tool to view JSON, edit, create, and upload JSON documents with DocumentDB, a NoSQL document database.
keywords: view json
services: documentdb
author: kirillg
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: 029d81b3-6382-4799-a1bd-0dcbccd9968d
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: kirillg
ms.openlocfilehash: 81578cdf26f5c0a456c29ebe6fd0f328c9861469
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563575"
---
# <a name="view-edit-create-and-upload-json-documents"></a><span data-ttu-id="57e28-104">View, edit, create, and upload JSON documents</span><span class="sxs-lookup"><span data-stu-id="57e28-104">View, edit, create, and upload JSON documents</span></span> 

<span data-ttu-id="57e28-105">This article provides an overview of the two ways you can create, edit and query documents in the portal: [Document Explorer](#launch-document-explorer) and [Data Explorer (preview)](#data-explorer).</span><span class="sxs-lookup"><span data-stu-id="57e28-105">This article provides an overview of the two ways you can create, edit and query documents in the portal: [Document Explorer](#launch-document-explorer) and [Data Explorer (preview)](#data-explorer).</span></span>

> [!NOTE]
> <span data-ttu-id="57e28-106">Document Explorer is not enabled on DocumentDB accounts with protocol support for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="57e28-106">Document Explorer is not enabled on DocumentDB accounts with protocol support for MongoDB.</span></span> <span data-ttu-id="57e28-107">This page will be updated when this feature is enabled.</span><span class="sxs-lookup"><span data-stu-id="57e28-107">This page will be updated when this feature is enabled.</span></span>

<a id="launch-document-explorer"></a>

## <a name="launch-document-explorer-in-the-azure-portal"></a><span data-ttu-id="57e28-108">Launch Document Explorer in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="57e28-108">Launch Document Explorer in the Azure portal</span></span>
1. <span data-ttu-id="57e28-109">In the [Azure portal](https://portal.azure.com), on the left navigation, click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="57e28-109">In the [Azure portal](https://portal.azure.com), on the left navigation, click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span></span> 

    <span data-ttu-id="57e28-110">If **NoSQL (DocumentDB)** is not visible, click **More Services** at the bottom, and then click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="57e28-110">If **NoSQL (DocumentDB)** is not visible, click **More Services** at the bottom, and then click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span></span>
2. <span data-ttu-id="57e28-111">Select the account name.</span><span class="sxs-lookup"><span data-stu-id="57e28-111">Select the account name.</span></span> 
3. <span data-ttu-id="57e28-112">In the resource menu, click **Document Explorer**.</span><span class="sxs-lookup"><span data-stu-id="57e28-112">In the resource menu, click **Document Explorer**.</span></span> 
   
    ![Screenshot of the Document Explorer command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentexplorercommand.png)
   
    <span data-ttu-id="57e28-114">In the **Document Explorer** blade, the **Databases** and **Collections** drop-down lists are pre-populated depending on the context in which you launched Document Explorer.</span><span class="sxs-lookup"><span data-stu-id="57e28-114">In the **Document Explorer** blade, the **Databases** and **Collections** drop-down lists are pre-populated depending on the context in which you launched Document Explorer.</span></span> 

## <a name="create-a-json-document"></a><span data-ttu-id="57e28-115">Create a JSON document</span><span class="sxs-lookup"><span data-stu-id="57e28-115">Create a JSON document</span></span>
1. <span data-ttu-id="57e28-116">[Launch Document Explorer](#launch-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="57e28-116">[Launch Document Explorer](#launch-document-explorer).</span></span>
2. <span data-ttu-id="57e28-117">In the **Document Explorer** blade, click **Create Document**.</span><span class="sxs-lookup"><span data-stu-id="57e28-117">In the **Document Explorer** blade, click **Create Document**.</span></span> 
   
    <span data-ttu-id="57e28-118">A minimal JSON snippet is provided in the **Document** blade.</span><span class="sxs-lookup"><span data-stu-id="57e28-118">A minimal JSON snippet is provided in the **Document** blade.</span></span>
   
    ![Screenshot of Document Explorer create document experience, where you can view JSON and edit JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/createdocument.png)
3. <span data-ttu-id="57e28-120">In the **Document** blade, type or paste in the content of the JSON document you wish to create, and then click **Save** to commit your document to the database and collection specified in the **Document Explorer** blade.</span><span class="sxs-lookup"><span data-stu-id="57e28-120">In the **Document** blade, type or paste in the content of the JSON document you wish to create, and then click **Save** to commit your document to the database and collection specified in the **Document Explorer** blade.</span></span>
   
    ![Screenshot of Document Explorer save command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/savedocument1.png)
   
   > [!NOTE]
   > <span data-ttu-id="57e28-122">If you do not provide an "id" property, then Document Explorer automatically adds an id property and generates a GUID as the id value.</span><span class="sxs-lookup"><span data-stu-id="57e28-122">If you do not provide an "id" property, then Document Explorer automatically adds an id property and generates a GUID as the id value.</span></span>
   > 
   > 
   
    <span data-ttu-id="57e28-123">If you already have data from JSON files, MongoDB, SQL Server, CSV files, Azure Table storage, Amazon DynamoDB, HBase, or from other DocumentDB collections, you can use DocumentDB's [data migration tool](documentdb-import-data.md) to quickly import your data.</span><span class="sxs-lookup"><span data-stu-id="57e28-123">If you already have data from JSON files, MongoDB, SQL Server, CSV files, Azure Table storage, Amazon DynamoDB, HBase, or from other DocumentDB collections, you can use DocumentDB's [data migration tool](documentdb-import-data.md) to quickly import your data.</span></span>

## <a name="edit-a-json-document"></a><span data-ttu-id="57e28-124">Edit a JSON document</span><span class="sxs-lookup"><span data-stu-id="57e28-124">Edit a JSON document</span></span>
1. <span data-ttu-id="57e28-125">[Launch Document Explorer](#launch-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="57e28-125">[Launch Document Explorer](#launch-document-explorer).</span></span>
2. <span data-ttu-id="57e28-126">To edit an existing document, select it in the **Document Explorer** blade, edit the document in the **Document** blade, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="57e28-126">To edit an existing document, select it in the **Document Explorer** blade, edit the document in the **Document** blade, and then click **Save**.</span></span>
   
    ![Screenshot of Document Explorer edit document functionality used to view JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/editdocument.png)
   
    <span data-ttu-id="57e28-128">If you're editing a document and decide that you want to discard the current set of edits, simply click **Discard** in the **Document** blade, confirm the discard action, and the previous state of the document is reloaded.</span><span class="sxs-lookup"><span data-stu-id="57e28-128">If you're editing a document and decide that you want to discard the current set of edits, simply click **Discard** in the **Document** blade, confirm the discard action, and the previous state of the document is reloaded.</span></span>
   
    ![Screenshot of Document Explorer discard command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/discardedit.png)

## <a name="delete-a-document-from-documentdb"></a><span data-ttu-id="57e28-130">Delete a document from DocumentDB</span><span class="sxs-lookup"><span data-stu-id="57e28-130">Delete a document from DocumentDB</span></span>
1. <span data-ttu-id="57e28-131">[Launch Document Explorer](#launch-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="57e28-131">[Launch Document Explorer](#launch-document-explorer).</span></span>
2. <span data-ttu-id="57e28-132">Select the document in **Document Explorer**, click **Delete**, and then confirm the delete.</span><span class="sxs-lookup"><span data-stu-id="57e28-132">Select the document in **Document Explorer**, click **Delete**, and then confirm the delete.</span></span> <span data-ttu-id="57e28-133">After confirming, the document is immediately removed from the Document Explorer list.</span><span class="sxs-lookup"><span data-stu-id="57e28-133">After confirming, the document is immediately removed from the Document Explorer list.</span></span>
   
    ![Screenshot of Document Explorer delete command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/deletedocument.png)

## <a name="work-with-json-documents"></a><span data-ttu-id="57e28-135">Work with JSON documents</span><span class="sxs-lookup"><span data-stu-id="57e28-135">Work with JSON documents</span></span>
<span data-ttu-id="57e28-136">Document Explorer validates that any new or edited document contains valid JSON.</span><span class="sxs-lookup"><span data-stu-id="57e28-136">Document Explorer validates that any new or edited document contains valid JSON.</span></span>  <span data-ttu-id="57e28-137">You can even view JSON errors by hovering over the incorrect section to get details about the validation error.</span><span class="sxs-lookup"><span data-stu-id="57e28-137">You can even view JSON errors by hovering over the incorrect section to get details about the validation error.</span></span>

![Screenshot of Document Explorer with invalid JSON highlighting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/invalidjson1.png)

<span data-ttu-id="57e28-139">Additionally, Document Explorer prevents you from saving a document with invalid JSON content.</span><span class="sxs-lookup"><span data-stu-id="57e28-139">Additionally, Document Explorer prevents you from saving a document with invalid JSON content.</span></span>

![Screenshot of Document Explorer with invalid JSON save error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/invalidjson2.png)

<span data-ttu-id="57e28-141">Finally, Document Explorer allows you to easily view the system properties of the currently loaded document by clicking the **Properties** command.</span><span class="sxs-lookup"><span data-stu-id="57e28-141">Finally, Document Explorer allows you to easily view the system properties of the currently loaded document by clicking the **Properties** command.</span></span>

![Screenshot of Document Explorer document properties view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentproperties.png)

> [!NOTE]
> <span data-ttu-id="57e28-143">The timestamp (_ts) property is internally represented as epoch time, but Document Explorer displays the value in a human readable GMT format.</span><span class="sxs-lookup"><span data-stu-id="57e28-143">The timestamp (_ts) property is internally represented as epoch time, but Document Explorer displays the value in a human readable GMT format.</span></span>
> 
> 

## <a name="filter-documents"></a><span data-ttu-id="57e28-144">Filter documents</span><span class="sxs-lookup"><span data-stu-id="57e28-144">Filter documents</span></span>
<span data-ttu-id="57e28-145">Document Explorer supports a number of navigation options and advanced settings.</span><span class="sxs-lookup"><span data-stu-id="57e28-145">Document Explorer supports a number of navigation options and advanced settings.</span></span>

<span data-ttu-id="57e28-146">By default, Document Explorer loads up to the first 100 documents in the selected collection, by their created date from earliest to latest.</span><span class="sxs-lookup"><span data-stu-id="57e28-146">By default, Document Explorer loads up to the first 100 documents in the selected collection, by their created date from earliest to latest.</span></span>  <span data-ttu-id="57e28-147">You can load additional documents (in batches of 100) by selecting the **Load more** option at the bottom of the Document Explorer blade.</span><span class="sxs-lookup"><span data-stu-id="57e28-147">You can load additional documents (in batches of 100) by selecting the **Load more** option at the bottom of the Document Explorer blade.</span></span> <span data-ttu-id="57e28-148">You can choose which documents to load through the **Filter** command.</span><span class="sxs-lookup"><span data-stu-id="57e28-148">You can choose which documents to load through the **Filter** command.</span></span>

1. <span data-ttu-id="57e28-149">[Launch Document Explorer](#launch-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="57e28-149">[Launch Document Explorer](#launch-document-explorer).</span></span>
2. <span data-ttu-id="57e28-150">At the top of the **Document Explorer** blade, click **Filter**.</span><span class="sxs-lookup"><span data-stu-id="57e28-150">At the top of the **Document Explorer** blade, click **Filter**.</span></span>  
   
    ![Screenshot of Document Explorer Filter Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentexplorerfiltersettings.png)
3. <span data-ttu-id="57e28-152">The filter settings appear below the command bar.</span><span class="sxs-lookup"><span data-stu-id="57e28-152">The filter settings appear below the command bar.</span></span> <span data-ttu-id="57e28-153">In the filter settings, provide a WHERE clause and/or an ORDER BY clause, and then click **Filter**.</span><span class="sxs-lookup"><span data-stu-id="57e28-153">In the filter settings, provide a WHERE clause and/or an ORDER BY clause, and then click **Filter**.</span></span>
   
   ![Screenshot of Document Explorer Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentexplorerfiltersettings2.png)
   
   <span data-ttu-id="57e28-155">Document Explorer automatically refreshes the results with documents matching the filter query.</span><span class="sxs-lookup"><span data-stu-id="57e28-155">Document Explorer automatically refreshes the results with documents matching the filter query.</span></span> <span data-ttu-id="57e28-156">Read more about the DocumentDB SQL grammar in the [SQL query and SQL syntax](documentdb-sql-query.md) article or print a copy of the [SQL query cheat sheet](documentdb-sql-query-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-156">Read more about the DocumentDB SQL grammar in the [SQL query and SQL syntax](documentdb-sql-query.md) article or print a copy of the [SQL query cheat sheet](documentdb-sql-query-cheat-sheet.md).</span></span>
   
   <span data-ttu-id="57e28-157">The **Database** and **Collection** drop-down list boxes can be used to easily change the collection from which documents are currently being viewed without having to close and re-launch Document Explorer.</span><span class="sxs-lookup"><span data-stu-id="57e28-157">The **Database** and **Collection** drop-down list boxes can be used to easily change the collection from which documents are currently being viewed without having to close and re-launch Document Explorer.</span></span>  
   
   <span data-ttu-id="57e28-158">Document Explorer also supports filtering the currently loaded set of documents by their id property.</span><span class="sxs-lookup"><span data-stu-id="57e28-158">Document Explorer also supports filtering the currently loaded set of documents by their id property.</span></span>  <span data-ttu-id="57e28-159">Simply type in the Documents Filter by id box.</span><span class="sxs-lookup"><span data-stu-id="57e28-159">Simply type in the Documents Filter by id box.</span></span>
   
   ![Screenshot of Document Explorer with filter highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentexplorerfilter.png)
   
   <span data-ttu-id="57e28-161">The results in the Document Explorer list are filtered based on your supplied criteria.</span><span class="sxs-lookup"><span data-stu-id="57e28-161">The results in the Document Explorer list are filtered based on your supplied criteria.</span></span>
   
   ![Screenshot of Document Explorer with filtered results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentexplorerfilterresults.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="57e28-163">The Document Explorer filter functionality only filters from the ***currently*** loaded set of documents and does not perform a query against the currently selected collection.</span><span class="sxs-lookup"><span data-stu-id="57e28-163">The Document Explorer filter functionality only filters from the ***currently*** loaded set of documents and does not perform a query against the currently selected collection.</span></span>
   > 
   > 
4. <span data-ttu-id="57e28-164">To refresh the list of documents loaded by Document Explorer, click **Refresh** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="57e28-164">To refresh the list of documents loaded by Document Explorer, click **Refresh** at the top of the blade.</span></span>
   
    ![Screenshot of Document Explorer refresh command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/documentexplorerrefresh.png)

## <a name="bulk-add-documents"></a><span data-ttu-id="57e28-166">Bulk add documents</span><span class="sxs-lookup"><span data-stu-id="57e28-166">Bulk add documents</span></span>
<span data-ttu-id="57e28-167">Document Explorer supports bulk ingestion of one or more existing JSON documents, up to 100 JSON files per upload operation.</span><span class="sxs-lookup"><span data-stu-id="57e28-167">Document Explorer supports bulk ingestion of one or more existing JSON documents, up to 100 JSON files per upload operation.</span></span>  

1. <span data-ttu-id="57e28-168">[Launch Document Explorer](#launch-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="57e28-168">[Launch Document Explorer](#launch-document-explorer).</span></span>
2. <span data-ttu-id="57e28-169">To start the upload process, click **Upload Document**.</span><span class="sxs-lookup"><span data-stu-id="57e28-169">To start the upload process, click **Upload Document**.</span></span>
   
    ![Screenshot of Document Explorer bulk ingestion functionality](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/uploaddocument1.png)
   
    <span data-ttu-id="57e28-171">The **Upload Document** blade opens.</span><span class="sxs-lookup"><span data-stu-id="57e28-171">The **Upload Document** blade opens.</span></span> 
3. <span data-ttu-id="57e28-172">Click the browse button to open a file explorer window, select one or more JSON documents to upload, and then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="57e28-172">Click the browse button to open a file explorer window, select one or more JSON documents to upload, and then click **Open**.</span></span>
   
    ![Screenshot of Document Explorer bulk ingestion process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/uploaddocument2.png)
   
   > [!NOTE]
   > <span data-ttu-id="57e28-174">Document Explorer currently supports up to 100 JSON documents per individual upload operation.</span><span class="sxs-lookup"><span data-stu-id="57e28-174">Document Explorer currently supports up to 100 JSON documents per individual upload operation.</span></span>
   > 
   > 
4. <span data-ttu-id="57e28-175">Once you're satisfied with your selection, click the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="57e28-175">Once you're satisfied with your selection, click the **Upload** button.</span></span>  <span data-ttu-id="57e28-176">The documents are automatically added to the Document Explorer grid and the upload results are displayed as the operation progresses.</span><span class="sxs-lookup"><span data-stu-id="57e28-176">The documents are automatically added to the Document Explorer grid and the upload results are displayed as the operation progresses.</span></span> <span data-ttu-id="57e28-177">Import failures are reported for individual files.</span><span class="sxs-lookup"><span data-stu-id="57e28-177">Import failures are reported for individual files.</span></span>
   
    ![Screenshot of Document Explorer bulk ingestion results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/uploaddocument3.png)
5. <span data-ttu-id="57e28-179">Once the operation is complete, you can select up to another 100 documents to upload.</span><span class="sxs-lookup"><span data-stu-id="57e28-179">Once the operation is complete, you can select up to another 100 documents to upload.</span></span>

<a id="data-explorer"></a>
## <a name="create-a-collection-by-using-data-explorer-preview"></a><span data-ttu-id="57e28-180">Create a collection by using Data Explorer (preview)</span><span class="sxs-lookup"><span data-stu-id="57e28-180">Create a collection by using Data Explorer (preview)</span></span>

<span data-ttu-id="57e28-181">The other method for creating, editing and querying documents in the portal is to use the Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="57e28-181">The other method for creating, editing and querying documents in the portal is to use the Data Explorer.</span></span> <span data-ttu-id="57e28-182">To open Data Explorer, click **Data Explorer (preview)** on the navigation bar in the portal, then expand your database name, expand your collection name, click **Documents**, and then click **New Document**, as shown in the following screencap.</span><span class="sxs-lookup"><span data-stu-id="57e28-182">To open Data Explorer, click **Data Explorer (preview)** on the navigation bar in the portal, then expand your database name, expand your collection name, click **Documents**, and then click **New Document**, as shown in the following screencap.</span></span>

![Screen shot showing the New Collection button in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-JSON-document-explorer/azure-documentdb-data-explorer.png)

## <a name="work-with-json-documents-outside-the-portal"></a><span data-ttu-id="57e28-184">Work with JSON documents outside the portal</span><span class="sxs-lookup"><span data-stu-id="57e28-184">Work with JSON documents outside the portal</span></span>
<span data-ttu-id="57e28-185">The Document Explorer in the Azure portal is just one way to work with documents in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="57e28-185">The Document Explorer in the Azure portal is just one way to work with documents in DocumentDB.</span></span> <span data-ttu-id="57e28-186">You can also work with documents using the [REST API](https://msdn.microsoft.com/library/azure/mt489082.aspx) or the [client SDKs](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-186">You can also work with documents using the [REST API](https://msdn.microsoft.com/library/azure/mt489082.aspx) or the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="57e28-187">For example code, see the [.NET SDK document examples](documentdb-dotnet-samples.md#document-examples) and the [Node.js SDK document examples](documentdb-nodejs-samples.md#document-examples).</span><span class="sxs-lookup"><span data-stu-id="57e28-187">For example code, see the [.NET SDK document examples](documentdb-dotnet-samples.md#document-examples) and the [Node.js SDK document examples](documentdb-nodejs-samples.md#document-examples).</span></span>

<span data-ttu-id="57e28-188">If you need to import or migrate files from another source (JSON files, MongoDB, SQL Server, CSV files, Azure Table storage, Amazon DynamoDB, or HBase), you can use the DocumentDB [data migration tool](documentdb-import-data.md) to quickly import your data to DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="57e28-188">If you need to import or migrate files from another source (JSON files, MongoDB, SQL Server, CSV files, Azure Table storage, Amazon DynamoDB, or HBase), you can use the DocumentDB [data migration tool](documentdb-import-data.md) to quickly import your data to DocumentDB.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="57e28-189">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="57e28-189">Troubleshoot</span></span>
<span data-ttu-id="57e28-190">**Symptom**: Document Explorer returns **No documents found**.</span><span class="sxs-lookup"><span data-stu-id="57e28-190">**Symptom**: Document Explorer returns **No documents found**.</span></span>

<span data-ttu-id="57e28-191">**Solution**: Ensure that you have selected the correct subscription, database and collection in which the documents were inserted.</span><span class="sxs-lookup"><span data-stu-id="57e28-191">**Solution**: Ensure that you have selected the correct subscription, database and collection in which the documents were inserted.</span></span> <span data-ttu-id="57e28-192">Also, check to ensure that you are operating within your throughput quotas.</span><span class="sxs-lookup"><span data-stu-id="57e28-192">Also, check to ensure that you are operating within your throughput quotas.</span></span> <span data-ttu-id="57e28-193">If you are operating at your maximum throughput level and getting throttled, lower application usage to operate under the maximum throughput quota for the collection.</span><span class="sxs-lookup"><span data-stu-id="57e28-193">If you are operating at your maximum throughput level and getting throttled, lower application usage to operate under the maximum throughput quota for the collection.</span></span>

<span data-ttu-id="57e28-194">**Explanation**: The portal is an application like any other, making calls to your DocumentDB database and collection.</span><span class="sxs-lookup"><span data-stu-id="57e28-194">**Explanation**: The portal is an application like any other, making calls to your DocumentDB database and collection.</span></span> <span data-ttu-id="57e28-195">If your requests are currently being throttled due to calls being made from a separate application, the portal may also be throttled, causing resources not to appear in the portal.</span><span class="sxs-lookup"><span data-stu-id="57e28-195">If your requests are currently being throttled due to calls being made from a separate application, the portal may also be throttled, causing resources not to appear in the portal.</span></span> <span data-ttu-id="57e28-196">To resolve the issue, address the cause of the high throughput usage, and then refresh the portal blade.</span><span class="sxs-lookup"><span data-stu-id="57e28-196">To resolve the issue, address the cause of the high throughput usage, and then refresh the portal blade.</span></span> <span data-ttu-id="57e28-197">Information on how to measure and lower throughput usage can be found in the [Throughput](documentdb-performance-tips.md#throughput) section of the [Performance tips](documentdb-performance-tips.md) article.</span><span class="sxs-lookup"><span data-stu-id="57e28-197">Information on how to measure and lower throughput usage can be found in the [Throughput](documentdb-performance-tips.md#throughput) section of the [Performance tips](documentdb-performance-tips.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57e28-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="57e28-198">Next steps</span></span>
<span data-ttu-id="57e28-199">To learn more about the DocumentDB SQL grammar supported in Document Explorer, see the [SQL query and SQL syntax](documentdb-sql-query.md) article or print out the [SQL query cheat sheet](documentdb-sql-query-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="57e28-199">To learn more about the DocumentDB SQL grammar supported in Document Explorer, see the [SQL query and SQL syntax](documentdb-sql-query.md) article or print out the [SQL query cheat sheet](documentdb-sql-query-cheat-sheet.md).</span></span>





















