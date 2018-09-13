---
title: 'Azure Cosmos DB: Develop with the Table API in .NET | Microsoft Docs'
description: Learn how to develop with Azure Cosmos DB's Table API using .NET
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 12/18/2017
ms.author: sngun
ms.custom: mvc
ms.openlocfilehash: e6511b9511d2598b58fd3afee34803ceb09ac5ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867576"
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="2c018-103">Azure Cosmos DB: Develop with the Table API in .NET</span><span class="sxs-lookup"><span data-stu-id="2c018-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="2c018-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="2c018-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2c018-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c018-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="2c018-106">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="2c018-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="2c018-107">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="2c018-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="2c018-108">Enable functionality in the app.config file</span><span class="sxs-lookup"><span data-stu-id="2c018-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="2c018-109">Create a table using the [Table API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2c018-109">Create a table using the [Table API](table-introduction.md)</span></span>
> * <span data-ttu-id="2c018-110">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="2c018-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="2c018-111">Insert a batch of entities</span><span class="sxs-lookup"><span data-stu-id="2c018-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="2c018-112">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="2c018-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="2c018-113">Query entities using automatic secondary indexes</span><span class="sxs-lookup"><span data-stu-id="2c018-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="2c018-114">Replace an entity</span><span class="sxs-lookup"><span data-stu-id="2c018-114">Replace an entity</span></span> 
> * <span data-ttu-id="2c018-115">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="2c018-115">Delete an entity</span></span> 
> * <span data-ttu-id="2c018-116">Delete a table</span><span class="sxs-lookup"><span data-stu-id="2c018-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="2c018-117">Tables in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2c018-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="2c018-118">Azure Cosmos DB provides the [Table API](table-introduction.md) for applications that need a key-value store with a schema-less design.</span><span class="sxs-lookup"><span data-stu-id="2c018-118">Azure Cosmos DB provides the [Table API](table-introduction.md) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="2c018-119">Both Azure Cosmos DB Table API and [Azure Table storage](../storage/common/storage-introduction.md) now support the same SDKs and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="2c018-119">Both Azure Cosmos DB Table API and [Azure Table storage](../storage/common/storage-introduction.md) now support the same SDKs and REST APIs.</span></span> <span data-ttu-id="2c018-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span><span class="sxs-lookup"><span data-stu-id="2c018-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span>

<span data-ttu-id="2c018-121">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c018-121">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available with Azure Cosmos DB.</span></span> <span data-ttu-id="2c018-122">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span><span class="sxs-lookup"><span data-stu-id="2c018-122">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="2c018-123">This tutorial describes how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table API application.</span><span class="sxs-lookup"><span data-stu-id="2c018-123">This tutorial describes how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table API application.</span></span> <span data-ttu-id="2c018-124">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span><span class="sxs-lookup"><span data-stu-id="2c018-124">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="2c018-125">If you currently use Azure Table storage, you gain the following benefits with Azure Cosmos DB Table API:</span><span class="sxs-lookup"><span data-stu-id="2c018-125">If you currently use Azure Table storage, you gain the following benefits with Azure Cosmos DB Table API:</span></span>

- <span data-ttu-id="2c018-126">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="2c018-126">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="2c018-127">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span><span class="sxs-lookup"><span data-stu-id="2c018-127">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="2c018-128">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span><span class="sxs-lookup"><span data-stu-id="2c018-128">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="2c018-129">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span><span class="sxs-lookup"><span data-stu-id="2c018-129">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="2c018-130">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span><span class="sxs-lookup"><span data-stu-id="2c018-130">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="2c018-131">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) on general availability</span><span class="sxs-lookup"><span data-stu-id="2c018-131">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) on general availability</span></span>
- <span data-ttu-id="2c018-132">Work with the existing Azure storage .NET SDK, and no code changes to your application</span><span class="sxs-lookup"><span data-stu-id="2c018-132">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="2c018-133">This tutorial covers Azure Cosmos DB Table API using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2c018-133">This tutorial covers Azure Cosmos DB Table API using the .NET SDK.</span></span> <span data-ttu-id="2c018-134">You can download the [Azure Cosmos DB Table API .NET SDK](https://aka.ms/tableapinuget) from NuGet.</span><span class="sxs-lookup"><span data-stu-id="2c018-134">You can download the [Azure Cosmos DB Table API .NET SDK](https://aka.ms/tableapinuget) from NuGet.</span></span>

<span data-ttu-id="2c018-135">To learn more about complex Azure Table storage tasks, see:</span><span class="sxs-lookup"><span data-stu-id="2c018-135">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="2c018-136">Introduction to Azure Cosmos DB Table API</span><span class="sxs-lookup"><span data-stu-id="2c018-136">Introduction to Azure Cosmos DB Table API</span></span>](table-introduction.md)
* <span data-ttu-id="2c018-137">The Table service reference documentation for complete details about available APIs [Azure Cosmos DB Table API .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/cosmosdb/client?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="2c018-137">The Table service reference documentation for complete details about available APIs [Azure Cosmos DB Table API .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/cosmosdb/client?view=azure-dotnet)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="2c018-138">About this tutorial</span><span class="sxs-lookup"><span data-stu-id="2c018-138">About this tutorial</span></span>
<span data-ttu-id="2c018-139">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c018-139">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="2c018-140">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span><span class="sxs-lookup"><span data-stu-id="2c018-140">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="2c018-141">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span><span class="sxs-lookup"><span data-stu-id="2c018-141">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="2c018-142">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span><span class="sxs-lookup"><span data-stu-id="2c018-142">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="2c018-143">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2c018-143">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="2c018-144">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="2c018-144">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="2c018-145">Create a database account</span><span class="sxs-lookup"><span data-stu-id="2c018-145">Create a database account</span></span>

<span data-ttu-id="2c018-146">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2c018-146">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  
 
> [!IMPORTANT]  
> <span data-ttu-id="2c018-147">You need to create a new Table API account to work with the generally available Table API SDKs.</span><span class="sxs-lookup"><span data-stu-id="2c018-147">You need to create a new Table API account to work with the generally available Table API SDKs.</span></span> <span data-ttu-id="2c018-148">Table API accounts created during preview are not supported by the generally available SDKs.</span><span class="sxs-lookup"><span data-stu-id="2c018-148">Table API accounts created during preview are not supported by the generally available SDKs.</span></span> 
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="2c018-149">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="2c018-149">Clone the sample application</span></span>

<span data-ttu-id="2c018-150">Now let's clone a Table app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="2c018-150">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="2c018-151">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="2c018-151">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="2c018-152">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="2c018-152">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span></span> 

    ```bash
    cd "C:\git-samples"
    ```

2. <span data-ttu-id="2c018-153">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="2c018-153">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="2c018-154">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="2c018-154">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/storage-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="2c018-155">Then open the solution file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2c018-155">Then open the solution file in Visual Studio.</span></span> 

## <a name="update-your-connection-string"></a><span data-ttu-id="2c018-156">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="2c018-156">Update your connection string</span></span>

<span data-ttu-id="2c018-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="2c018-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="2c018-158">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="2c018-158">This enables your app to communicate with your hosted database.</span></span> 

1. <span data-ttu-id="2c018-159">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="2c018-159">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    <span data-ttu-id="2c018-160">Use the copy buttons on the right side of the screen to copy the PRIMARY CONNECTION STRING.</span><span class="sxs-lookup"><span data-stu-id="2c018-160">Use the copy buttons on the right side of the screen to copy the PRIMARY CONNECTION STRING.</span></span>

    ![View and copy the CONNECTION STRING in the Connection String pane](./media/create-table-dotnet/connection-string.png)

2. <span data-ttu-id="2c018-162">In Visual Studio, open the app.config file.</span><span class="sxs-lookup"><span data-stu-id="2c018-162">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="2c018-163">Uncomment the StorageConnectionString on line 8 and comment out the StorageConnectionString on line 7 as this tutorial does not use the Storage Emulator.</span><span class="sxs-lookup"><span data-stu-id="2c018-163">Uncomment the StorageConnectionString on line 8 and comment out the StorageConnectionString on line 7 as this tutorial does not use the Storage Emulator.</span></span> <span data-ttu-id="2c018-164">Line 7 and 8 should now look like this:</span><span class="sxs-lookup"><span data-stu-id="2c018-164">Line 7 and 8 should now look like this:</span></span>

    ```
    <!--key="StorageConnectionString" value="UseDevelopmentStorage=true;" />-->
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=[AccountName];AccountKey=[AccountKey]" />
    ```

4. <span data-ttu-id="2c018-165">Paste the PRIMARY CONNECTION STRING from the portal into the StorageConnectionString value on line 8.</span><span class="sxs-lookup"><span data-stu-id="2c018-165">Paste the PRIMARY CONNECTION STRING from the portal into the StorageConnectionString value on line 8.</span></span> <span data-ttu-id="2c018-166">Paste the string inside the quotes.</span><span class="sxs-lookup"><span data-stu-id="2c018-166">Paste the string inside the quotes.</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="2c018-167">If your Endpoint uses documents.azure.com, that means you have a preview account, and you need to create a [new Table API account](#create-a-database-account) to work with the generally available Table API SDK.</span><span class="sxs-lookup"><span data-stu-id="2c018-167">If your Endpoint uses documents.azure.com, that means you have a preview account, and you need to create a [new Table API account](#create-a-database-account) to work with the generally available Table API SDK.</span></span> 
    >

    <span data-ttu-id="2c018-168">Line 8 should now look similar to:</span><span class="sxs-lookup"><span data-stu-id="2c018-168">Line 8 should now look similar to:</span></span>

    ```
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=txZACN9f...==;TableEndpoint=https://<account name>.table.cosmosdb.azure.com;" />
    ```

5. <span data-ttu-id="2c018-169">Save the app.config file.</span><span class="sxs-lookup"><span data-stu-id="2c018-169">Save the app.config file.</span></span>

<span data-ttu-id="2c018-170">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c018-170">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="2c018-171">Azure Cosmos DB capabilities</span><span class="sxs-lookup"><span data-stu-id="2c018-171">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="2c018-172">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span><span class="sxs-lookup"><span data-stu-id="2c018-172">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> 

<span data-ttu-id="2c018-173">Certain functionality is accessed via new overloads to CreateCloudTableClient that enable one to specify connection policy and consistency level.</span><span class="sxs-lookup"><span data-stu-id="2c018-173">Certain functionality is accessed via new overloads to CreateCloudTableClient that enable one to specify connection policy and consistency level.</span></span>

| <span data-ttu-id="2c018-174">Table Connection Settings</span><span class="sxs-lookup"><span data-stu-id="2c018-174">Table Connection Settings</span></span> | <span data-ttu-id="2c018-175">Description</span><span class="sxs-lookup"><span data-stu-id="2c018-175">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c018-176">Connection Mode</span><span class="sxs-lookup"><span data-stu-id="2c018-176">Connection Mode</span></span>  | <span data-ttu-id="2c018-177">Azure Cosmos DB supports two connectivity modes.</span><span class="sxs-lookup"><span data-stu-id="2c018-177">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="2c018-178">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span><span class="sxs-lookup"><span data-stu-id="2c018-178">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="2c018-179">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span><span class="sxs-lookup"><span data-stu-id="2c018-179">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="2c018-180">We recommend `Direct`, the default.</span><span class="sxs-lookup"><span data-stu-id="2c018-180">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="2c018-181">Connection Protocol</span><span class="sxs-lookup"><span data-stu-id="2c018-181">Connection Protocol</span></span> | <span data-ttu-id="2c018-182">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="2c018-182">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="2c018-183">`Tcp` is the default, and recommended because it is more lightweight.</span><span class="sxs-lookup"><span data-stu-id="2c018-183">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="2c018-184">Preferred Locations</span><span class="sxs-lookup"><span data-stu-id="2c018-184">Preferred Locations</span></span> | <span data-ttu-id="2c018-185">Comma-separated list of preferred (multi-homing) locations for reads.</span><span class="sxs-lookup"><span data-stu-id="2c018-185">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="2c018-186">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span><span class="sxs-lookup"><span data-stu-id="2c018-186">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="2c018-187">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span><span class="sxs-lookup"><span data-stu-id="2c018-187">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="2c018-188">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span><span class="sxs-lookup"><span data-stu-id="2c018-188">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="2c018-189">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="2c018-189">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span> |
| <span data-ttu-id="2c018-190">Consistency Level</span><span class="sxs-lookup"><span data-stu-id="2c018-190">Consistency Level</span></span> | <span data-ttu-id="2c018-191">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="2c018-191">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="2c018-192">Default is `Session`.</span><span class="sxs-lookup"><span data-stu-id="2c018-192">Default is `Session`.</span></span> <span data-ttu-id="2c018-193">The choice of consistency level makes a significant performance difference in multi-region setups.</span><span class="sxs-lookup"><span data-stu-id="2c018-193">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="2c018-194">See [Consistency levels](consistency-levels.md) for details.</span><span class="sxs-lookup"><span data-stu-id="2c018-194">See [Consistency levels](consistency-levels.md) for details.</span></span> |

<span data-ttu-id="2c018-195">Other functionality can be enabled via the following `appSettings` configuration values.</span><span class="sxs-lookup"><span data-stu-id="2c018-195">Other functionality can be enabled via the following `appSettings` configuration values.</span></span>

| <span data-ttu-id="2c018-196">Key</span><span class="sxs-lookup"><span data-stu-id="2c018-196">Key</span></span> | <span data-ttu-id="2c018-197">Description</span><span class="sxs-lookup"><span data-stu-id="2c018-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c018-198">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="2c018-198">TableQueryMaxItemCount</span></span> | <span data-ttu-id="2c018-199">Configure the maximum number of items returned per table query in a single round trip.</span><span class="sxs-lookup"><span data-stu-id="2c018-199">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="2c018-200">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span><span class="sxs-lookup"><span data-stu-id="2c018-200">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="2c018-201">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="2c018-201">TableQueryEnableScan</span></span> | <span data-ttu-id="2c018-202">If the query cannot use the index for any filter, then run it anyway via a scan.</span><span class="sxs-lookup"><span data-stu-id="2c018-202">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="2c018-203">Default is `false`.</span><span class="sxs-lookup"><span data-stu-id="2c018-203">Default is `false`.</span></span>|
| <span data-ttu-id="2c018-204">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="2c018-204">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="2c018-205">The degree of parallelism for execution of a cross-partition query.</span><span class="sxs-lookup"><span data-stu-id="2c018-205">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="2c018-206">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span><span class="sxs-lookup"><span data-stu-id="2c018-206">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="2c018-207">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span><span class="sxs-lookup"><span data-stu-id="2c018-207">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="2c018-208">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2c018-208">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="2c018-209">Add the contents of the `<appSettings>` element shown below.</span><span class="sxs-lookup"><span data-stu-id="2c018-209">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="2c018-210">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span><span class="sxs-lookup"><span data-stu-id="2c018-210">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    ...
    <appSettings>
      <!-- Client options -->
      <add key="CosmosDBStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://account-name.table.cosmosdb.azure.com" />
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="2c018-211">Let's make a quick review of what's happening in the app.</span><span class="sxs-lookup"><span data-stu-id="2c018-211">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="2c018-212">Open the `Program.cs` file and you will find that these lines of code create the Table resources.</span><span class="sxs-lookup"><span data-stu-id="2c018-212">Open the `Program.cs` file and you will find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="2c018-213">Create the table client</span><span class="sxs-lookup"><span data-stu-id="2c018-213">Create the table client</span></span>
<span data-ttu-id="2c018-214">You initialize a `CloudTableClient` to connect to the table account.</span><span class="sxs-lookup"><span data-stu-id="2c018-214">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="2c018-215">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span><span class="sxs-lookup"><span data-stu-id="2c018-215">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="2c018-216">Create a table</span><span class="sxs-lookup"><span data-stu-id="2c018-216">Create a table</span></span>
<span data-ttu-id="2c018-217">Then, you create a table using `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="2c018-217">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="2c018-218">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span><span class="sxs-lookup"><span data-stu-id="2c018-218">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="2c018-219">Azure Cosmos DB supports both fixed size and unlimited tables.</span><span class="sxs-lookup"><span data-stu-id="2c018-219">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="2c018-220">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span><span class="sxs-lookup"><span data-stu-id="2c018-220">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");
400
table.CreateIfNotExists(throughput: 800);
```

<span data-ttu-id="2c018-221">There is an important difference in how tables are created.</span><span class="sxs-lookup"><span data-stu-id="2c018-221">There is an important difference in how tables are created.</span></span> <span data-ttu-id="2c018-222">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span><span class="sxs-lookup"><span data-stu-id="2c018-222">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="2c018-223">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="2c018-223">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput.</span></span>

<span data-ttu-id="2c018-224">You can configure the default throughput by including it as a parameter of CreateIfNotExists.</span><span class="sxs-lookup"><span data-stu-id="2c018-224">You can configure the default throughput by including it as a parameter of CreateIfNotExists.</span></span>

<span data-ttu-id="2c018-225">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span><span class="sxs-lookup"><span data-stu-id="2c018-225">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="2c018-226">Learn more about [Request units in Azure Cosmos DB](request-units.md) and specifically for [key value stores](key-value-store-cost.md).</span><span class="sxs-lookup"><span data-stu-id="2c018-226">Learn more about [Request units in Azure Cosmos DB](request-units.md) and specifically for [key value stores](key-value-store-cost.md).</span></span>

<span data-ttu-id="2c018-227">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span><span class="sxs-lookup"><span data-stu-id="2c018-227">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="2c018-228">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c018-228">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="2c018-229">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="2c018-229">Add an entity to a table</span></span>
<span data-ttu-id="2c018-230">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span><span class="sxs-lookup"><span data-stu-id="2c018-230">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="2c018-231">Here's a sample definition for a customer entity.</span><span class="sxs-lookup"><span data-stu-id="2c018-231">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="2c018-232">The following snippet shows how to insert an entity with the Azure storage SDK.</span><span class="sxs-lookup"><span data-stu-id="2c018-232">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="2c018-233">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span><span class="sxs-lookup"><span data-stu-id="2c018-233">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="2c018-234">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2c018-234">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="2c018-235">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span><span class="sxs-lookup"><span data-stu-id="2c018-235">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>


```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="2c018-236">Insert a batch of entities</span><span class="sxs-lookup"><span data-stu-id="2c018-236">Insert a batch of entities</span></span>
<span data-ttu-id="2c018-237">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same batch operation.</span><span class="sxs-lookup"><span data-stu-id="2c018-237">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same batch operation.</span></span>

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="2c018-238">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="2c018-238">Retrieve a single entity</span></span>
<span data-ttu-id="2c018-239">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="2c018-239">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="2c018-240">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="2c018-240">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="2c018-241">You can retrieve a single entity using the following snippet:</span><span class="sxs-lookup"><span data-stu-id="2c018-241">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="2c018-242">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="2c018-242">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="2c018-243">Query entities using automatic secondary indexes</span><span class="sxs-lookup"><span data-stu-id="2c018-243">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="2c018-244">Tables can be queried using the `TableQuery` class.</span><span class="sxs-lookup"><span data-stu-id="2c018-244">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="2c018-245">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span><span class="sxs-lookup"><span data-stu-id="2c018-245">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="2c018-246">Indexing in Azure Cosmos DB is agnostic to schema.</span><span class="sxs-lookup"><span data-stu-id="2c018-246">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="2c018-247">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span><span class="sxs-lookup"><span data-stu-id="2c018-247">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="2c018-248">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span><span class="sxs-lookup"><span data-stu-id="2c018-248">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="2c018-249">Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span><span class="sxs-lookup"><span data-stu-id="2c018-249">Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="2c018-250">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span><span class="sxs-lookup"><span data-stu-id="2c018-250">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="2c018-251">The additional functionality will be provided in the Table API in a future service update.</span><span class="sxs-lookup"><span data-stu-id="2c018-251">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="2c018-252">See [Azure Cosmos DB query](sql-api-sql-query.md) for an overview of these capabilities.</span><span class="sxs-lookup"><span data-stu-id="2c018-252">See [Azure Cosmos DB query](sql-api-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="2c018-253">Replace an entity</span><span class="sxs-lookup"><span data-stu-id="2c018-253">Replace an entity</span></span>
<span data-ttu-id="2c018-254">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span><span class="sxs-lookup"><span data-stu-id="2c018-254">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="2c018-255">The following code changes an existing customer's phone number.</span><span class="sxs-lookup"><span data-stu-id="2c018-255">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="2c018-256">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span><span class="sxs-lookup"><span data-stu-id="2c018-256">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="2c018-257">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="2c018-257">Delete an entity</span></span>
<span data-ttu-id="2c018-258">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span><span class="sxs-lookup"><span data-stu-id="2c018-258">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="2c018-259">The following code retrieves and deletes a customer entity.</span><span class="sxs-lookup"><span data-stu-id="2c018-259">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="2c018-260">Delete a table</span><span class="sxs-lookup"><span data-stu-id="2c018-260">Delete a table</span></span>
<span data-ttu-id="2c018-261">Finally, the following code example deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="2c018-261">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="2c018-262">You can delete and recreate a table immediately with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c018-262">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="2c018-263">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2c018-263">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="2c018-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c018-264">Next steps</span></span>

<span data-ttu-id="2c018-265">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span><span class="sxs-lookup"><span data-stu-id="2c018-265">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="2c018-266">Created an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="2c018-266">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="2c018-267">Enabled functionality in the app.config file</span><span class="sxs-lookup"><span data-stu-id="2c018-267">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="2c018-268">Created a table</span><span class="sxs-lookup"><span data-stu-id="2c018-268">Created a table</span></span> 
> * <span data-ttu-id="2c018-269">Added an entity to a table</span><span class="sxs-lookup"><span data-stu-id="2c018-269">Added an entity to a table</span></span> 
> * <span data-ttu-id="2c018-270">Inserted a batch of entities</span><span class="sxs-lookup"><span data-stu-id="2c018-270">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="2c018-271">Retrieved a single entity</span><span class="sxs-lookup"><span data-stu-id="2c018-271">Retrieved a single entity</span></span> 
> * <span data-ttu-id="2c018-272">Queried entities using automatic secondary indexes</span><span class="sxs-lookup"><span data-stu-id="2c018-272">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="2c018-273">Replaced an entity</span><span class="sxs-lookup"><span data-stu-id="2c018-273">Replaced an entity</span></span> 
> * <span data-ttu-id="2c018-274">Deleted an entity</span><span class="sxs-lookup"><span data-stu-id="2c018-274">Deleted an entity</span></span> 
> * <span data-ttu-id="2c018-275">Deleted a table</span><span class="sxs-lookup"><span data-stu-id="2c018-275">Deleted a table</span></span>  

<span data-ttu-id="2c018-276">You can now proceed to the next tutorial and learn more about querying table data.</span><span class="sxs-lookup"><span data-stu-id="2c018-276">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2c018-277">Query with the Table API</span><span class="sxs-lookup"><span data-stu-id="2c018-277">Query with the Table API</span></span>](tutorial-query-table.md)
