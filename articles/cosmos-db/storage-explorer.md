---
title: Manage Azure Cosmos DB in Azure Storage Explorer
description: Learn how to manage Azure Cosmos DB in Azure Storage Explorer.
Keywords: Azure Cosmos DB, Azure Storage Explorer, MongoDB
services: cosmos-db
author: Jejiang
manager: kfile
editor: ''
tags: Azure Cosmos DB
ms.service: cosmos-db
ms.custom: Azure Cosmos DB active
ms.devlang: na
ms.topic: conceptual
ms.date: 03/20/2018
ms.author: jejiang
ms.openlocfilehash: b45328425cff978377d5e05de487d42e786c063b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856647"
---
# <a name="manage-azure-cosmos-db-in-azure-storage-explorer"></a><span data-ttu-id="27e55-103">Manage Azure Cosmos DB in Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="27e55-103">Manage Azure Cosmos DB in Azure Storage Explorer</span></span>

<span data-ttu-id="27e55-104">Using Azure Cosmos DB in Azure Storage Explorer enables users to manage Azure Cosmos DB entities, manipulate data, update stored procedures and triggers along with other Azure entities like Storage blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="27e55-104">Using Azure Cosmos DB in Azure Storage Explorer enables users to manage Azure Cosmos DB entities, manipulate data, update stored procedures and triggers along with other Azure entities like Storage blobs and queues.</span></span> <span data-ttu-id="27e55-105">Now you can use the same tool to manage your different Azure entities in one place.</span><span class="sxs-lookup"><span data-stu-id="27e55-105">Now you can use the same tool to manage your different Azure entities in one place.</span></span> <span data-ttu-id="27e55-106">At this time, Azure Storage Explorer supports SQL, MongoDB, Graph, and Table accounts.</span><span class="sxs-lookup"><span data-stu-id="27e55-106">At this time, Azure Storage Explorer supports SQL, MongoDB, Graph, and Table accounts.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="27e55-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="27e55-107">Prerequisites</span></span>

<span data-ttu-id="27e55-108">An Azure Cosmos DB account for the SQL API<!--or MongoDB API-->.</span><span class="sxs-lookup"><span data-stu-id="27e55-108">An Azure Cosmos DB account for the SQL API<!--or MongoDB API-->.</span></span> <span data-ttu-id="27e55-109">If you don't have an account, you can create one in the Azure portal, as described in [Azure Cosmos DB: Build a SQL API web app with .NET and the Azure portal](create-sql-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="27e55-109">If you don't have an account, you can create one in the Azure portal, as described in [Azure Cosmos DB: Build a SQL API web app with .NET and the Azure portal](create-sql-api-dotnet.md).</span></span>

## <a name="installation"></a><span data-ttu-id="27e55-110">Installation</span><span class="sxs-lookup"><span data-stu-id="27e55-110">Installation</span></span>

<span data-ttu-id="27e55-111">Install the newest Azure Storage Explorer bits here: [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/), now we support Windows, Linux, and MAC version.</span><span class="sxs-lookup"><span data-stu-id="27e55-111">Install the newest Azure Storage Explorer bits here: [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/), now we support Windows, Linux, and MAC version.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="27e55-112">Connect to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="27e55-112">Connect to an Azure subscription</span></span>

1. <span data-ttu-id="27e55-113">After installing the **Azure Storage Explorer**, click the **plug-in** icon on the left as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="27e55-113">After installing the **Azure Storage Explorer**, click the **plug-in** icon on the left as shown in the following image:</span></span>
       
   ![Plug in icon](./media/storage-explorer/plug-in-icon.png)
 
2. <span data-ttu-id="27e55-115">Select **Add an Azure Account**, and then click **Sign-in**.</span><span class="sxs-lookup"><span data-stu-id="27e55-115">Select **Add an Azure Account**, and then click **Sign-in**.</span></span>

   ![Connect to Azure subscription](./media/storage-explorer/connect-to-azure-subscription.png)

2. <span data-ttu-id="27e55-117">In the **Azure Sign in** dialog box, select **Sign in**, and then enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="27e55-117">In the **Azure Sign in** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Sign in](./media/storage-explorer/sign-in.png)

3. <span data-ttu-id="27e55-119">Select your subscription from the list and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="27e55-119">Select your subscription from the list and then click **Apply**.</span></span>

    ![Apply](./media/storage-explorer/apply-subscription.png)

    <span data-ttu-id="27e55-121">The Explorer pane updates and displays the accounts in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="27e55-121">The Explorer pane updates and displays the accounts in the selected subscription.</span></span>

    ![Account list](./media/storage-explorer/account-list.png)

    <span data-ttu-id="27e55-123">You have successfully connected to your **Cosmos DB account** to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="27e55-123">You have successfully connected to your **Cosmos DB account** to your Azure subscription.</span></span>

## <a name="connect-to-azure-cosmos-db-by-using-a-connection-string"></a><span data-ttu-id="27e55-124">Connect to Azure Cosmos DB by using a connection string</span><span class="sxs-lookup"><span data-stu-id="27e55-124">Connect to Azure Cosmos DB by using a connection string</span></span>

<span data-ttu-id="27e55-125">An alternative way of connecting to an Azure Cosmos DB is to use a connection string.</span><span class="sxs-lookup"><span data-stu-id="27e55-125">An alternative way of connecting to an Azure Cosmos DB is to use a connection string.</span></span> <span data-ttu-id="27e55-126">Use the following steps to connect using a connection string.</span><span class="sxs-lookup"><span data-stu-id="27e55-126">Use the following steps to connect using a connection string.</span></span>

1. <span data-ttu-id="27e55-127">Find **Local and Attached** in the left tree, right-click **Cosmos DB Accounts**, choose **Connect to Cosmos DB...**</span><span class="sxs-lookup"><span data-stu-id="27e55-127">Find **Local and Attached** in the left tree, right-click **Cosmos DB Accounts**, choose **Connect to Cosmos DB...**</span></span>

    ![Connect to Cosmos DB by connection string](./media/storage-explorer/connect-to-db-by-connection-string.png)

2. <span data-ttu-id="27e55-129">Only support SQL and Table API currently.</span><span class="sxs-lookup"><span data-stu-id="27e55-129">Only support SQL and Table API currently.</span></span> <span data-ttu-id="27e55-130">Choose API, paste **Connection String**, input **Account label**, click **Next** to check the summary, and then click **Connect** to connect Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="27e55-130">Choose API, paste **Connection String**, input **Account label**, click **Next** to check the summary, and then click **Connect** to connect Azure Cosmos DB account.</span></span> <span data-ttu-id="27e55-131">For information on retrieving the connection string, see [Get the connection string](https://docs.microsoft.com/azure/cosmos-db/manage-account#get-the--connection-string).</span><span class="sxs-lookup"><span data-stu-id="27e55-131">For information on retrieving the connection string, see [Get the connection string](https://docs.microsoft.com/azure/cosmos-db/manage-account#get-the--connection-string).</span></span>

    ![Connection-string](./media/storage-explorer/connection-string.png)

## <a name="connect-to-azure-cosmos-db-by-using-local-emulator"></a><span data-ttu-id="27e55-133">Connect to Azure Cosmos DB by using local emulator</span><span class="sxs-lookup"><span data-stu-id="27e55-133">Connect to Azure Cosmos DB by using local emulator</span></span>

<span data-ttu-id="27e55-134">Use the following steps to connect to an Azure Cosmos DB by Emulator, only support SQL account currently.</span><span class="sxs-lookup"><span data-stu-id="27e55-134">Use the following steps to connect to an Azure Cosmos DB by Emulator, only support SQL account currently.</span></span>

1. <span data-ttu-id="27e55-135">Install Emulator and launch.</span><span class="sxs-lookup"><span data-stu-id="27e55-135">Install Emulator and launch.</span></span> <span data-ttu-id="27e55-136">For how to install Emulator, see [Cosmos DB Emulator](https://docs.microsoft.com/azure/cosmos-db/local-emulator)</span><span class="sxs-lookup"><span data-stu-id="27e55-136">For how to install Emulator, see [Cosmos DB Emulator](https://docs.microsoft.com/azure/cosmos-db/local-emulator)</span></span>

2. <span data-ttu-id="27e55-137">Find **Local and Attached** in the left tree, right-click **Cosmos DB Accounts**, choose **Connect to Cosmos DB Emulator...**</span><span class="sxs-lookup"><span data-stu-id="27e55-137">Find **Local and Attached** in the left tree, right-click **Cosmos DB Accounts**, choose **Connect to Cosmos DB Emulator...**</span></span>

    ![Connect to Cosmos DB by Emulator](./media/storage-explorer/emulator-entry.png)

3. <span data-ttu-id="27e55-139">Only support SQL API currently.</span><span class="sxs-lookup"><span data-stu-id="27e55-139">Only support SQL API currently.</span></span> <span data-ttu-id="27e55-140">Paste **Connection String**, input **Account label**, click **Next** to check the summary, and then click **Connect** to connect Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="27e55-140">Paste **Connection String**, input **Account label**, click **Next** to check the summary, and then click **Connect** to connect Azure Cosmos DB account.</span></span> <span data-ttu-id="27e55-141">For information on retrieving the connection string, see [Get the connection string](https://docs.microsoft.com/azure/cosmos-db/manage-account#get-the--connection-string).</span><span class="sxs-lookup"><span data-stu-id="27e55-141">For information on retrieving the connection string, see [Get the connection string](https://docs.microsoft.com/azure/cosmos-db/manage-account#get-the--connection-string).</span></span>

    ![Connect to Cosmos DB by Emulator dialog](./media/storage-explorer/emulator-dialog.png)


## <a name="azure-cosmos-db-resource-management"></a><span data-ttu-id="27e55-143">Azure Cosmos DB resource management</span><span class="sxs-lookup"><span data-stu-id="27e55-143">Azure Cosmos DB resource management</span></span>

<span data-ttu-id="27e55-144">You can manage an Azure Cosmos DB account by doing following operations:</span><span class="sxs-lookup"><span data-stu-id="27e55-144">You can manage an Azure Cosmos DB account by doing following operations:</span></span>
* <span data-ttu-id="27e55-145">Open the account in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="27e55-145">Open the account in the Azure portal</span></span>
* <span data-ttu-id="27e55-146">Add the resource to the Quick Access list</span><span class="sxs-lookup"><span data-stu-id="27e55-146">Add the resource to the Quick Access list</span></span>
* <span data-ttu-id="27e55-147">Search and refresh resources</span><span class="sxs-lookup"><span data-stu-id="27e55-147">Search and refresh resources</span></span>
* <span data-ttu-id="27e55-148">Create and delete databases</span><span class="sxs-lookup"><span data-stu-id="27e55-148">Create and delete databases</span></span>
* <span data-ttu-id="27e55-149">Create and delete collections</span><span class="sxs-lookup"><span data-stu-id="27e55-149">Create and delete collections</span></span>
* <span data-ttu-id="27e55-150">Create, edit, delete, and filter documents</span><span class="sxs-lookup"><span data-stu-id="27e55-150">Create, edit, delete, and filter documents</span></span>
* <span data-ttu-id="27e55-151">Manage stored procedures, triggers, and user-defined functions</span><span class="sxs-lookup"><span data-stu-id="27e55-151">Manage stored procedures, triggers, and user-defined functions</span></span>

### <a name="quick-access-tasks"></a><span data-ttu-id="27e55-152">Quick access tasks</span><span class="sxs-lookup"><span data-stu-id="27e55-152">Quick access tasks</span></span>

<span data-ttu-id="27e55-153">By right-clicking on a subscription in the Explorer pane, you can perform many quick action tasks:</span><span class="sxs-lookup"><span data-stu-id="27e55-153">By right-clicking on a subscription in the Explorer pane, you can perform many quick action tasks:</span></span>

* <span data-ttu-id="27e55-154">Right-click an Azure Cosmos DB account or a database, you can choose **Open in Portal** and manage the resource in the browser on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="27e55-154">Right-click an Azure Cosmos DB account or a database, you can choose **Open in Portal** and manage the resource in the browser on the Azure portal.</span></span>

     ![Open in portal](./media/storage-explorer/open-in-portal.png)

* <span data-ttu-id="27e55-156">You can also add Azure Cosmos DB account, database, collection to **Quick Access**.</span><span class="sxs-lookup"><span data-stu-id="27e55-156">You can also add Azure Cosmos DB account, database, collection to **Quick Access**.</span></span>
* <span data-ttu-id="27e55-157">**Search from Here** enables keyword search under the selected path.</span><span class="sxs-lookup"><span data-stu-id="27e55-157">**Search from Here** enables keyword search under the selected path.</span></span>

    ![search from here](./media/storage-explorer/search-from-here.png) 

### <a name="database-and-collection-management"></a><span data-ttu-id="27e55-159">Database and collection management</span><span class="sxs-lookup"><span data-stu-id="27e55-159">Database and collection management</span></span>
#### <a name="create-a-database"></a><span data-ttu-id="27e55-160">Create a database</span><span class="sxs-lookup"><span data-stu-id="27e55-160">Create a database</span></span> 
-   <span data-ttu-id="27e55-161">Right-click the Azure Cosmos DB account, choose **Create Database**, input the database name, and press **Enter** to complete.</span><span class="sxs-lookup"><span data-stu-id="27e55-161">Right-click the Azure Cosmos DB account, choose **Create Database**, input the database name, and press **Enter** to complete.</span></span>
       
    ![Create database](./media/storage-explorer/create-database.png) 

#### <a name="delete-a-database"></a><span data-ttu-id="27e55-163">Delete a database</span><span class="sxs-lookup"><span data-stu-id="27e55-163">Delete a database</span></span>
- <span data-ttu-id="27e55-164">Right-click the database, click **Delete Database**, and click **Yes** in the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="27e55-164">Right-click the database, click **Delete Database**, and click **Yes** in the pop-up window.</span></span> <span data-ttu-id="27e55-165">The database node is deleted, and the Azure Cosmos DB account refreshes automatically.</span><span class="sxs-lookup"><span data-stu-id="27e55-165">The database node is deleted, and the Azure Cosmos DB account refreshes automatically.</span></span>

    ![Delete database1](./media/storage-explorer/delete-database1.png)  

    ![Delete database2](./media/storage-explorer/delete-database2.png) 

#### <a name="create-a-collection"></a><span data-ttu-id="27e55-168">Create a collection</span><span class="sxs-lookup"><span data-stu-id="27e55-168">Create a collection</span></span>
1. <span data-ttu-id="27e55-169">Right-click your database, choose **Create Collection**, and then provide the following information like **Collection ID**, **Storage capacity**, etc. Click **OK** to finish.</span><span class="sxs-lookup"><span data-stu-id="27e55-169">Right-click your database, choose **Create Collection**, and then provide the following information like **Collection ID**, **Storage capacity**, etc. Click **OK** to finish.</span></span> 

    ![Create collection1](./media/storage-explorer/create-collection.png)

    ![Create collection2](./media/storage-explorer/create-collection2.png) 

2. <span data-ttu-id="27e55-172">Select **Unlimited** to be able to specify partition key, then click **OK** to finish.</span><span class="sxs-lookup"><span data-stu-id="27e55-172">Select **Unlimited** to be able to specify partition key, then click **OK** to finish.</span></span>

    <span data-ttu-id="27e55-173">If a partition key is used when creating a collection, once creation is completed, the partition key value can't be changed on the collection.</span><span class="sxs-lookup"><span data-stu-id="27e55-173">If a partition key is used when creating a collection, once creation is completed, the partition key value can't be changed on the collection.</span></span> <span data-ttu-id="27e55-174">For information on partition key settings, see [Design for partitioning](partition-data.md#designing-for-partitioning).</span><span class="sxs-lookup"><span data-stu-id="27e55-174">For information on partition key settings, see [Design for partitioning](partition-data.md#designing-for-partitioning).</span></span>

    ![Partition key](./media/storage-explorer/partitionkey.png)

#### <a name="delete-a-collection"></a><span data-ttu-id="27e55-176">Delete a collection</span><span class="sxs-lookup"><span data-stu-id="27e55-176">Delete a collection</span></span>
- <span data-ttu-id="27e55-177">Right-click the collection, click **Delete Collection**, and then click **Yes** in the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="27e55-177">Right-click the collection, click **Delete Collection**, and then click **Yes** in the pop-up window.</span></span> 

    <span data-ttu-id="27e55-178">The collection node is deleted, and the database refreshes automatically.</span><span class="sxs-lookup"><span data-stu-id="27e55-178">The collection node is deleted, and the database refreshes automatically.</span></span>

    ![Delete collection](./media/storage-explorer/delete-collection.png) 

### <a name="document-management"></a><span data-ttu-id="27e55-180">Document management</span><span class="sxs-lookup"><span data-stu-id="27e55-180">Document management</span></span>

#### <a name="create-and-modify-documents"></a><span data-ttu-id="27e55-181">Create and modify documents</span><span class="sxs-lookup"><span data-stu-id="27e55-181">Create and modify documents</span></span>
- <span data-ttu-id="27e55-182">To create a new document, open **Documents** in the left window, click **New Document**, edit the contents in the right pane, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="27e55-182">To create a new document, open **Documents** in the left window, click **New Document**, edit the contents in the right pane, then click **Save**.</span></span> <span data-ttu-id="27e55-183">You can also update an existing document, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="27e55-183">You can also update an existing document, and then click **Save**.</span></span> <span data-ttu-id="27e55-184">Changes can be discarded by clicking **Discard**.</span><span class="sxs-lookup"><span data-stu-id="27e55-184">Changes can be discarded by clicking **Discard**.</span></span>

    ![Document](./media/storage-explorer/document.png)

#### <a name="delete-a-document"></a><span data-ttu-id="27e55-186">Delete a document</span><span class="sxs-lookup"><span data-stu-id="27e55-186">Delete a document</span></span>
- <span data-ttu-id="27e55-187">Click the **Delete** button to delete the selected document.</span><span class="sxs-lookup"><span data-stu-id="27e55-187">Click the **Delete** button to delete the selected document.</span></span>

#### <a name="query-for-documents"></a><span data-ttu-id="27e55-188">Query for documents</span><span class="sxs-lookup"><span data-stu-id="27e55-188">Query for documents</span></span>
- <span data-ttu-id="27e55-189">Edit the document filter by entering a [SQL query](sql-api-sql-query.md) and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="27e55-189">Edit the document filter by entering a [SQL query](sql-api-sql-query.md) and then click **Apply**.</span></span>

    ![Document Filter](./media/storage-explorer/document-filter.png)



### <a name="graph-management"></a><span data-ttu-id="27e55-191">Graph management</span><span class="sxs-lookup"><span data-stu-id="27e55-191">Graph management</span></span>

#### <a name="create-and-modify-vertex"></a><span data-ttu-id="27e55-192">Create and modify vertex</span><span class="sxs-lookup"><span data-stu-id="27e55-192">Create and modify vertex</span></span>
1. <span data-ttu-id="27e55-193">To create a new vertex, open **Graph** from the left window, click **New Vertex**, edit the contents, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="27e55-193">To create a new vertex, open **Graph** from the left window, click **New Vertex**, edit the contents, then click **OK**.</span></span>    
2. <span data-ttu-id="27e55-194">To modify an existing vertex, click the pen icon in the right pane.</span><span class="sxs-lookup"><span data-stu-id="27e55-194">To modify an existing vertex, click the pen icon in the right pane.</span></span>   

    ![Graph](./media/storage-explorer/vertex.png)

#### <a name="delete-a-graph"></a><span data-ttu-id="27e55-196">Delete a graph</span><span class="sxs-lookup"><span data-stu-id="27e55-196">Delete a graph</span></span>
- <span data-ttu-id="27e55-197">To delete a vertex, click the recycle bin icon beside the vertex name.</span><span class="sxs-lookup"><span data-stu-id="27e55-197">To delete a vertex, click the recycle bin icon beside the vertex name.</span></span>

#### <a name="filter-for-graph"></a><span data-ttu-id="27e55-198">Filter for graph</span><span class="sxs-lookup"><span data-stu-id="27e55-198">Filter for graph</span></span>
- <span data-ttu-id="27e55-199">Edit the graph filter by entering a [gremlin query](gremlin-support.md) and then click **Apply Filter**.</span><span class="sxs-lookup"><span data-stu-id="27e55-199">Edit the graph filter by entering a [gremlin query](gremlin-support.md) and then click **Apply Filter**.</span></span>

    ![Graph Filter](./media/storage-explorer/graph-filter.png)

### <a name="table-management"></a><span data-ttu-id="27e55-201">Table management</span><span class="sxs-lookup"><span data-stu-id="27e55-201">Table management</span></span>

#### <a name="create-and-modify-table"></a><span data-ttu-id="27e55-202">Create and modify table</span><span class="sxs-lookup"><span data-stu-id="27e55-202">Create and modify table</span></span>
1. <span data-ttu-id="27e55-203">To create a new table, open **Entities** from the left window, click **Add**, edit the content in **Add Entity** dialog, add property by clicking button **Add Property**, then click **Insert**.</span><span class="sxs-lookup"><span data-stu-id="27e55-203">To create a new table, open **Entities** from the left window, click **Add**, edit the content in **Add Entity** dialog, add property by clicking button **Add Property**, then click **Insert**.</span></span>
2. <span data-ttu-id="27e55-204">To modify a table, click **Edit**, modify the content, then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="27e55-204">To modify a table, click **Edit**, modify the content, then click **Update**.</span></span>

    ![Table](./media/storage-explorer/table.png)

#### <a name="import-and-export-table"></a><span data-ttu-id="27e55-206">Import and export table</span><span class="sxs-lookup"><span data-stu-id="27e55-206">Import and export table</span></span>
1. <span data-ttu-id="27e55-207">To import, click **Import** button and choose an existing table.</span><span class="sxs-lookup"><span data-stu-id="27e55-207">To import, click **Import** button and choose an existing table.</span></span>
2. <span data-ttu-id="27e55-208">To export, click **Export** button and choose a destination.</span><span class="sxs-lookup"><span data-stu-id="27e55-208">To export, click **Export** button and choose a destination.</span></span>

    ![Table Import and Export](./media/storage-explorer/table-import-export.png)

#### <a name="delete-entities"></a><span data-ttu-id="27e55-210">Delete entities</span><span class="sxs-lookup"><span data-stu-id="27e55-210">Delete entities</span></span>
- <span data-ttu-id="27e55-211">Select the entities and click button **Delete**.</span><span class="sxs-lookup"><span data-stu-id="27e55-211">Select the entities and click button **Delete**.</span></span>

    ![Table delete](./media/storage-explorer/table-delete.png)

#### <a name="query-table"></a><span data-ttu-id="27e55-213">Query table</span><span class="sxs-lookup"><span data-stu-id="27e55-213">Query table</span></span>
- <span data-ttu-id="27e55-214">Click **Query** button, input query condition, then click **Execute Query** button.</span><span class="sxs-lookup"><span data-stu-id="27e55-214">Click **Query** button, input query condition, then click **Execute Query** button.</span></span> <span data-ttu-id="27e55-215">Close Query pane by clicking **Close Query** button.</span><span class="sxs-lookup"><span data-stu-id="27e55-215">Close Query pane by clicking **Close Query** button.</span></span>

    ![Table Query](./media/storage-explorer/table-query.png)

### <a name="manage-stored-procedures-triggers-and-udfs"></a><span data-ttu-id="27e55-217">Manage stored procedures, triggers, and UDFs</span><span class="sxs-lookup"><span data-stu-id="27e55-217">Manage stored procedures, triggers, and UDFs</span></span>
* <span data-ttu-id="27e55-218">To create a stored procedure, in the left tree, right-click **Stored Procedure**, choose **Create Stored Procedure**, enter a name in the left, type the stored procedure scripts in the right window, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="27e55-218">To create a stored procedure, in the left tree, right-click **Stored Procedure**, choose **Create Stored Procedure**, enter a name in the left, type the stored procedure scripts in the right window, and then click **Create**.</span></span> 
* <span data-ttu-id="27e55-219">You can also edit existing stored procedures by double-clicking, making the update, and then clicking **Update** to save, or click **Discard** to cancel the change.</span><span class="sxs-lookup"><span data-stu-id="27e55-219">You can also edit existing stored procedures by double-clicking, making the update, and then clicking **Update** to save, or click **Discard** to cancel the change.</span></span>

    ![Stored procedure](./media/storage-explorer/stored-procedure.png)
* <span data-ttu-id="27e55-221">The operations for **Triggers** and **UDF** are similar with **Stored Procedures**.</span><span class="sxs-lookup"><span data-stu-id="27e55-221">The operations for **Triggers** and **UDF** are similar with **Stored Procedures**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="27e55-222">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="27e55-222">Troubleshooting</span></span>

<span data-ttu-id="27e55-223">[Azure Cosmos DB in Azure Storage Explorer](https://docs.microsoft.com/azure/cosmos-db/storage-explorer) is a standalone app that allows you to connect to Azure Cosmos DB accounts hosted on Azure and Sovereign Clouds from Windows, macOS, or Linux.</span><span class="sxs-lookup"><span data-stu-id="27e55-223">[Azure Cosmos DB in Azure Storage Explorer](https://docs.microsoft.com/azure/cosmos-db/storage-explorer) is a standalone app that allows you to connect to Azure Cosmos DB accounts hosted on Azure and Sovereign Clouds from Windows, macOS, or Linux.</span></span> <span data-ttu-id="27e55-224">It enables you to manage Azure Cosmos DB entities, manipulate data, update stored procedures and triggers along with other Azure entities like Storage blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="27e55-224">It enables you to manage Azure Cosmos DB entities, manipulate data, update stored procedures and triggers along with other Azure entities like Storage blobs and queues.</span></span>

<span data-ttu-id="27e55-225">These are solutions for common issues seen for Azure Cosmos DB in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="27e55-225">These are solutions for common issues seen for Azure Cosmos DB in Storage Explorer.</span></span>

### <a name="sign-in-issues"></a><span data-ttu-id="27e55-226">Sign in issues</span><span class="sxs-lookup"><span data-stu-id="27e55-226">Sign in issues</span></span>

<span data-ttu-id="27e55-227">Before proceeding further, try restarting your application and see if the problems can be fixed.</span><span class="sxs-lookup"><span data-stu-id="27e55-227">Before proceeding further, try restarting your application and see if the problems can be fixed.</span></span>

#### <a name="self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="27e55-228">Self-signed certificate in certificate chain</span><span class="sxs-lookup"><span data-stu-id="27e55-228">Self-signed certificate in certificate chain</span></span>

<span data-ttu-id="27e55-229">There are a few reasons you may be seeing this error, the two most common ones are:</span><span class="sxs-lookup"><span data-stu-id="27e55-229">There are a few reasons you may be seeing this error, the two most common ones are:</span></span>

+ <span data-ttu-id="27e55-230">You're behind a *transparent proxy*, which means someone (such as your IT department) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="27e55-230">You're behind a *transparent proxy*, which means someone (such as your IT department) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

+ <span data-ttu-id="27e55-231">You're running software, such as anti-virus software, which is injecting a self-signed SSL certificates into the HTTPS messages you receive.</span><span class="sxs-lookup"><span data-stu-id="27e55-231">You're running software, such as anti-virus software, which is injecting a self-signed SSL certificates into the HTTPS messages you receive.</span></span>

<span data-ttu-id="27e55-232">When Storage Explorer encounters one of these "self-signed certificates", it can no longer know if the HTTPS message it's receiving has been tampered with.</span><span class="sxs-lookup"><span data-stu-id="27e55-232">When Storage Explorer encounters one of these "self-signed certificates", it can no longer know if the HTTPS message it's receiving has been tampered with.</span></span> <span data-ttu-id="27e55-233">If you have a copy of the self-signed certificate though, then you can tell Storage Explorer to trust it.</span><span class="sxs-lookup"><span data-stu-id="27e55-233">If you have a copy of the self-signed certificate though, then you can tell Storage Explorer to trust it.</span></span> <span data-ttu-id="27e55-234">If you're unsure of who is injecting the certificate, then you can try to find it yourself by doing the following steps:</span><span class="sxs-lookup"><span data-stu-id="27e55-234">If you're unsure of who is injecting the certificate, then you can try to find it yourself by doing the following steps:</span></span>

1. <span data-ttu-id="27e55-235">Install Open SSL</span><span class="sxs-lookup"><span data-stu-id="27e55-235">Install Open SSL</span></span>
     - <span data-ttu-id="27e55-236">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions is ok)</span><span class="sxs-lookup"><span data-stu-id="27e55-236">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions is ok)</span></span>
     - <span data-ttu-id="27e55-237">Mac and Linux: Should be included with your operating system</span><span class="sxs-lookup"><span data-stu-id="27e55-237">Mac and Linux: Should be included with your operating system</span></span>
2. <span data-ttu-id="27e55-238">Run Open SSL</span><span class="sxs-lookup"><span data-stu-id="27e55-238">Run Open SSL</span></span>
    - <span data-ttu-id="27e55-239">Windows: Go to the install directory, then **/bin/**, then double-click on **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="27e55-239">Windows: Go to the install directory, then **/bin/**, then double-click on **openssl.exe**.</span></span>
    - <span data-ttu-id="27e55-240">Mac and Linux: execute **openssl** from a terminal</span><span class="sxs-lookup"><span data-stu-id="27e55-240">Mac and Linux: execute **openssl** from a terminal</span></span>
3. <span data-ttu-id="27e55-241">Execute `s_client -showcerts -connect microsoft.com:443`</span><span class="sxs-lookup"><span data-stu-id="27e55-241">Execute `s_client -showcerts -connect microsoft.com:443`</span></span>
4. <span data-ttu-id="27e55-242">Look for self-signed certificates.</span><span class="sxs-lookup"><span data-stu-id="27e55-242">Look for self-signed certificates.</span></span> <span data-ttu-id="27e55-243">If you're unsure, which are self-signed, then look for anywhere the subject ("s:") and issuer ("i:") are the same.</span><span class="sxs-lookup"><span data-stu-id="27e55-243">If you're unsure, which are self-signed, then look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>
5.  <span data-ttu-id="27e55-244">Once you have found any self-signed certificates, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file for each one.</span><span class="sxs-lookup"><span data-stu-id="27e55-244">Once you have found any self-signed certificates, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file for each one.</span></span>
6.  <span data-ttu-id="27e55-245">Open Storage Explorer and then go to **Edit** > **SSL Certificates** > **Import Certificates**.</span><span class="sxs-lookup"><span data-stu-id="27e55-245">Open Storage Explorer and then go to **Edit** > **SSL Certificates** > **Import Certificates**.</span></span> <span data-ttu-id="27e55-246">Using the file picker, find, select, and open the .cer files you created.</span><span class="sxs-lookup"><span data-stu-id="27e55-246">Using the file picker, find, select, and open the .cer files you created.</span></span>

<span data-ttu-id="27e55-247">If you're unable to find any self-signed certificates using the above steps, could send feedback for more help.</span><span class="sxs-lookup"><span data-stu-id="27e55-247">If you're unable to find any self-signed certificates using the above steps, could send feedback for more help.</span></span>

#### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="27e55-248">Unable to retrieve subscriptions</span><span class="sxs-lookup"><span data-stu-id="27e55-248">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="27e55-249">If you're unable to retrieve your subscriptions after you successfully signed in:</span><span class="sxs-lookup"><span data-stu-id="27e55-249">If you're unable to retrieve your subscriptions after you successfully signed in:</span></span>

- <span data-ttu-id="27e55-250">Verify your account has access to the subscriptions by signing into the [Azure Portal](http://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="27e55-250">Verify your account has access to the subscriptions by signing into the [Azure Portal](http://portal.azure.com/)</span></span>
- <span data-ttu-id="27e55-251">Make sure you have signed in using the correct environment ([Azure](http://portal.azure.com/), [Azure China](https://portal.azure.cn/), [Azure Germany](https://portal.microsoftazure.de/), [Azure US Government](http://portal.azure.us/), or Custom Environment/Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="27e55-251">Make sure you have signed in using the correct environment ([Azure](http://portal.azure.com/), [Azure China](https://portal.azure.cn/), [Azure Germany](https://portal.microsoftazure.de/), [Azure US Government](http://portal.azure.us/), or Custom Environment/Azure Stack)</span></span>
- <span data-ttu-id="27e55-252">If you're behind a proxy, make sure that you have configured the Storage Explorer proxy properly</span><span class="sxs-lookup"><span data-stu-id="27e55-252">If you're behind a proxy, make sure that you have configured the Storage Explorer proxy properly</span></span>
- <span data-ttu-id="27e55-253">Try removing and readding the account</span><span class="sxs-lookup"><span data-stu-id="27e55-253">Try removing and readding the account</span></span>
- <span data-ttu-id="27e55-254">Try deleting the following files from your home directory (such as: C:\Users\ContosoUser), and then readding the account:</span><span class="sxs-lookup"><span data-stu-id="27e55-254">Try deleting the following files from your home directory (such as: C:\Users\ContosoUser), and then readding the account:</span></span>
  - <span data-ttu-id="27e55-255">.adalcache</span><span class="sxs-lookup"><span data-stu-id="27e55-255">.adalcache</span></span>
  - <span data-ttu-id="27e55-256">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="27e55-256">.devaccounts</span></span>
  - <span data-ttu-id="27e55-257">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="27e55-257">.extaccounts</span></span>
- <span data-ttu-id="27e55-258">Watch the developer tools console (f12) while signing in for any error messages</span><span class="sxs-lookup"><span data-stu-id="27e55-258">Watch the developer tools console (f12) while signing in for any error messages</span></span>

![console](./media/storage-explorer/console.png)

#### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="27e55-260">Unable to see the authentication page</span><span class="sxs-lookup"><span data-stu-id="27e55-260">Unable to see the authentication page</span></span> 

<span data-ttu-id="27e55-261">If you're unable to see the authentication page:</span><span class="sxs-lookup"><span data-stu-id="27e55-261">If you're unable to see the authentication page:</span></span>

- <span data-ttu-id="27e55-262">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog</span><span class="sxs-lookup"><span data-stu-id="27e55-262">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog</span></span>
- <span data-ttu-id="27e55-263">If you're behind a proxy, make sure that you have configured the Storage Explorer proxy properly</span><span class="sxs-lookup"><span data-stu-id="27e55-263">If you're behind a proxy, make sure that you have configured the Storage Explorer proxy properly</span></span>
- <span data-ttu-id="27e55-264">Bring up the developer console by pressing F12 key.</span><span class="sxs-lookup"><span data-stu-id="27e55-264">Bring up the developer console by pressing F12 key.</span></span> <span data-ttu-id="27e55-265">Watch the responses from developer console and see if you can find any clue for why authentication is not working</span><span class="sxs-lookup"><span data-stu-id="27e55-265">Watch the responses from developer console and see if you can find any clue for why authentication is not working</span></span>

#### <a name="cannot-remove-account"></a><span data-ttu-id="27e55-266">Cannot remove account</span><span class="sxs-lookup"><span data-stu-id="27e55-266">Cannot remove account</span></span>

<span data-ttu-id="27e55-267">If you're unable to remove an account, or if the reauthenticate link does not do anything</span><span class="sxs-lookup"><span data-stu-id="27e55-267">If you're unable to remove an account, or if the reauthenticate link does not do anything</span></span>

- <span data-ttu-id="27e55-268">Try deleting the following files from your home directory, and then readding the account:</span><span class="sxs-lookup"><span data-stu-id="27e55-268">Try deleting the following files from your home directory, and then readding the account:</span></span>
  - <span data-ttu-id="27e55-269">.adalcache</span><span class="sxs-lookup"><span data-stu-id="27e55-269">.adalcache</span></span>
  - <span data-ttu-id="27e55-270">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="27e55-270">.devaccounts</span></span>
  - <span data-ttu-id="27e55-271">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="27e55-271">.extaccounts</span></span>
- <span data-ttu-id="27e55-272">If you want to remove SAS attached Storage resources, delete:</span><span class="sxs-lookup"><span data-stu-id="27e55-272">If you want to remove SAS attached Storage resources, delete:</span></span>
  - <span data-ttu-id="27e55-273">%AppData%/StorageExplorer folder for Windows</span><span class="sxs-lookup"><span data-stu-id="27e55-273">%AppData%/StorageExplorer folder for Windows</span></span>
  - <span data-ttu-id="27e55-274">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span><span class="sxs-lookup"><span data-stu-id="27e55-274">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>
  - <span data-ttu-id="27e55-275">~/.config/StorageExplorer for Linux</span><span class="sxs-lookup"><span data-stu-id="27e55-275">~/.config/StorageExplorer for Linux</span></span>
  - <span data-ttu-id="27e55-276">**You will have to reenter all your credentials** if you delete these files</span><span class="sxs-lookup"><span data-stu-id="27e55-276">**You will have to reenter all your credentials** if you delete these files</span></span>


### <a name="httphttps-proxy-issue"></a><span data-ttu-id="27e55-277">Http/Https proxy issue</span><span class="sxs-lookup"><span data-stu-id="27e55-277">Http/Https proxy issue</span></span>

<span data-ttu-id="27e55-278">You cannot list Azure Cosmos DB nodes in left tree when configuring http/https proxy in ASE.</span><span class="sxs-lookup"><span data-stu-id="27e55-278">You cannot list Azure Cosmos DB nodes in left tree when configuring http/https proxy in ASE.</span></span> <span data-ttu-id="27e55-279">It's a known issue, and will be fixed in next release.</span><span class="sxs-lookup"><span data-stu-id="27e55-279">It's a known issue, and will be fixed in next release.</span></span> <span data-ttu-id="27e55-280">You could use Azure Cosmos DB data explorer in Azure portal as a work-around at this moment.</span><span class="sxs-lookup"><span data-stu-id="27e55-280">You could use Azure Cosmos DB data explorer in Azure portal as a work-around at this moment.</span></span> 

### <a name="development-node-under-local-and-attached-node-issue"></a><span data-ttu-id="27e55-281">"Development" node under "Local and Attached" node issue</span><span class="sxs-lookup"><span data-stu-id="27e55-281">"Development" node under "Local and Attached" node issue</span></span>

<span data-ttu-id="27e55-282">There is no response after clicking the "Development" node under "Local and Attached" node in left tree.</span><span class="sxs-lookup"><span data-stu-id="27e55-282">There is no response after clicking the "Development" node under "Local and Attached" node in left tree.</span></span>  <span data-ttu-id="27e55-283">The behavior is expected.</span><span class="sxs-lookup"><span data-stu-id="27e55-283">The behavior is expected.</span></span> <span data-ttu-id="27e55-284">Azure Cosmos DB local emulator will be supported in next release.</span><span class="sxs-lookup"><span data-stu-id="27e55-284">Azure Cosmos DB local emulator will be supported in next release.</span></span>

![Development node](./media/storage-explorer/development.png)

### <a name="attaching-azure-cosmos-db-account-in-local-and-attached-node-error"></a><span data-ttu-id="27e55-286">Attaching Azure Cosmos DB account in "Local and Attached" node error</span><span class="sxs-lookup"><span data-stu-id="27e55-286">Attaching Azure Cosmos DB account in "Local and Attached" node error</span></span>

<span data-ttu-id="27e55-287">If you see below error after attaching Azure Cosmos DB account in "Local and Attached" node, then check if you're using the right connection string.</span><span class="sxs-lookup"><span data-stu-id="27e55-287">If you see below error after attaching Azure Cosmos DB account in "Local and Attached" node, then check if you're using the right connection string.</span></span>

![Attaching Azure Cosmos DB in Local and Attached error](./media/storage-explorer/attached-error.png)

### <a name="expand-azure-cosmos-db-node-error"></a><span data-ttu-id="27e55-289">Expand Azure Cosmos DB node error</span><span class="sxs-lookup"><span data-stu-id="27e55-289">Expand Azure Cosmos DB node error</span></span>

<span data-ttu-id="27e55-290">You may see below error while trying to expand the tree nodes in left.</span><span class="sxs-lookup"><span data-stu-id="27e55-290">You may see below error while trying to expand the tree nodes in left.</span></span> 

![Expand Error](./media/storage-explorer/expand-error.png)

<span data-ttu-id="27e55-292">Try the following suggestions:</span><span class="sxs-lookup"><span data-stu-id="27e55-292">Try the following suggestions:</span></span>

- <span data-ttu-id="27e55-293">Check if the Azure Cosmos DB account is in provision progress and try again when the account is being created successfully.</span><span class="sxs-lookup"><span data-stu-id="27e55-293">Check if the Azure Cosmos DB account is in provision progress and try again when the account is being created successfully.</span></span>
- <span data-ttu-id="27e55-294">If the account is under "Quick Access" node or "Local and Attached" nodes, then check if the account has been deleted.</span><span class="sxs-lookup"><span data-stu-id="27e55-294">If the account is under "Quick Access" node or "Local and Attached" nodes, then check if the account has been deleted.</span></span> <span data-ttu-id="27e55-295">If so, you need to remove the node manually.</span><span class="sxs-lookup"><span data-stu-id="27e55-295">If so, you need to remove the node manually.</span></span>

## <a name="contact-us"></a><span data-ttu-id="27e55-296">Contact us</span><span class="sxs-lookup"><span data-stu-id="27e55-296">Contact us</span></span>

<span data-ttu-id="27e55-297">If none of the solutions work for you, send email to Azure Cosmos DB Dev Tooling Team ([cosmosdbtooling@microsoft.com](mailto:cosmosdbtooling@microsoft.com)) with details about the issue, for fixing the issues.</span><span class="sxs-lookup"><span data-stu-id="27e55-297">If none of the solutions work for you, send email to Azure Cosmos DB Dev Tooling Team ([cosmosdbtooling@microsoft.com](mailto:cosmosdbtooling@microsoft.com)) with details about the issue, for fixing the issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27e55-298">Next steps</span><span class="sxs-lookup"><span data-stu-id="27e55-298">Next steps</span></span>

* <span data-ttu-id="27e55-299">Watch the following video to see how to use Azure Cosmos DB in Azure Storage Explorer: [Use Azure Cosmos DB in Azure Storage Explorer](https://www.youtube.com/watch?v=iNIbg1DLgWo&feature=youtu.be).</span><span class="sxs-lookup"><span data-stu-id="27e55-299">Watch the following video to see how to use Azure Cosmos DB in Azure Storage Explorer: [Use Azure Cosmos DB in Azure Storage Explorer](https://www.youtube.com/watch?v=iNIbg1DLgWo&feature=youtu.be).</span></span>
* <span data-ttu-id="27e55-300">Learn more about Storage Explorer and connect more services in [Get started with Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span><span class="sxs-lookup"><span data-stu-id="27e55-300">Learn more about Storage Explorer and connect more services in [Get started with Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span></span>

