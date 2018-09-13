---
title: How to use Azure Table Storage and the Azure Cosmos DB Table API with Ruby | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: ruby
ms.topic: sample
ms.date: 04/05/2018
ms.author: sngun
ms.openlocfilehash: d1583001550f5f272f4070006a4a6ac3be000de6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866052"
---
# <a name="how-to-use-azure-table-storage-and-the-azure-cosmos-db-table-api-with-ruby"></a><span data-ttu-id="957ac-103">How to use Azure Table Storage and the Azure Cosmos DB Table API with Ruby</span><span class="sxs-lookup"><span data-stu-id="957ac-103">How to use Azure Table Storage and the Azure Cosmos DB Table API with Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

## <a name="overview"></a><span data-ttu-id="957ac-104">Overview</span><span class="sxs-lookup"><span data-stu-id="957ac-104">Overview</span></span>
<span data-ttu-id="957ac-105">This guide shows you how to perform common scenarios using Azure Table service and the Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="957ac-105">This guide shows you how to perform common scenarios using Azure Table service and the Azure Cosmos DB Table API.</span></span> <span data-ttu-id="957ac-106">The samples are written in Ruby and use the [Azure Storage Table Client Library for Ruby](https://github.com/azure/azure-storage-ruby/tree/master/table).</span><span class="sxs-lookup"><span data-stu-id="957ac-106">The samples are written in Ruby and use the [Azure Storage Table Client Library for Ruby](https://github.com/azure/azure-storage-ruby/tree/master/table).</span></span> <span data-ttu-id="957ac-107">The scenarios covered include **creating and deleting a table, and inserting and querying entities in a table**.</span><span class="sxs-lookup"><span data-stu-id="957ac-107">The scenarios covered include **creating and deleting a table, and inserting and querying entities in a table**.</span></span>

## <a name="create-an-azure-service-account"></a><span data-ttu-id="957ac-108">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="957ac-108">Create an Azure service account</span></span>
[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="957ac-109">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="957ac-109">Create an Azure storage account</span></span>
[!INCLUDE [cosmos-db-create-storage-account](../../includes/cosmos-db-create-storage-account.md)]

### <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="957ac-110">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="957ac-110">Create an Azure Cosmos DB account</span></span>
[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

## <a name="add-access-to-storage-or-azure-cosmos-db"></a><span data-ttu-id="957ac-111">Add access to Storage or Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="957ac-111">Add access to Storage or Azure Cosmos DB</span></span>
<span data-ttu-id="957ac-112">To use Azure Storage or Azure Cosmos DB, you must download and use the Ruby Azure package that includes a set of convenience libraries that communicate with the Table REST services.</span><span class="sxs-lookup"><span data-stu-id="957ac-112">To use Azure Storage or Azure Cosmos DB, you must download and use the Ruby Azure package that includes a set of convenience libraries that communicate with the Table REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="957ac-113">Use RubyGems to obtain the package</span><span class="sxs-lookup"><span data-stu-id="957ac-113">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="957ac-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="957ac-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="957ac-115">Type **gem install azure-storage-table** in the command window to install the gem and dependencies.</span><span class="sxs-lookup"><span data-stu-id="957ac-115">Type **gem install azure-storage-table** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="957ac-116">Import the package</span><span class="sxs-lookup"><span data-stu-id="957ac-116">Import the package</span></span>
<span data-ttu-id="957ac-117">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span><span class="sxs-lookup"><span data-stu-id="957ac-117">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure/storage/table"
```

## <a name="add-an-azure-storage-connection"></a><span data-ttu-id="957ac-118">Add an Azure Storage connection</span><span class="sxs-lookup"><span data-stu-id="957ac-118">Add an Azure Storage connection</span></span>
<span data-ttu-id="957ac-119">The Azure Storage module reads the environment variables **AZURE_STORAGE_ACCOUNT** and **AZURE_STORAGE_ACCESS_KEY** for information required to connect to your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="957ac-119">The Azure Storage module reads the environment variables **AZURE_STORAGE_ACCOUNT** and **AZURE_STORAGE_ACCESS_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="957ac-120">If these environment variables are not set, you must specify the account information before using **Azure::Storage::Table::TableService** with the following code:</span><span class="sxs-lookup"><span data-stu-id="957ac-120">If these environment variables are not set, you must specify the account information before using **Azure::Storage::Table::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your Azure Storage account>"
Azure.config.storage_access_key = "<your Azure Storage access key>"
```

<span data-ttu-id="957ac-121">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="957ac-121">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="957ac-122">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="957ac-122">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="957ac-123">Navigate to the Storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="957ac-123">Navigate to the Storage account you want to use.</span></span>
3. <span data-ttu-id="957ac-124">In the Settings blade on the right, click **Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="957ac-124">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="957ac-125">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span><span class="sxs-lookup"><span data-stu-id="957ac-125">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="957ac-126">You can use either of these.</span><span class="sxs-lookup"><span data-stu-id="957ac-126">You can use either of these.</span></span>
5. <span data-ttu-id="957ac-127">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="957ac-127">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="add-an-azure-cosmos-db-connection"></a><span data-ttu-id="957ac-128">Add an Azure Cosmos DB connection</span><span class="sxs-lookup"><span data-stu-id="957ac-128">Add an Azure Cosmos DB connection</span></span>
<span data-ttu-id="957ac-129">To connect to Azure Cosmos DB, copy your primary connection string from the Azure portal, and create a **Client** object using your copied connection string.</span><span class="sxs-lookup"><span data-stu-id="957ac-129">To connect to Azure Cosmos DB, copy your primary connection string from the Azure portal, and create a **Client** object using your copied connection string.</span></span> <span data-ttu-id="957ac-130">You can pass the **Client** object when you create a **TableService** object:</span><span class="sxs-lookup"><span data-stu-id="957ac-130">You can pass the **Client** object when you create a **TableService** object:</span></span>

```ruby
common_client = Azure::Storage::Common::Client.create(storage_account_name:'myaccount', storage_access_key:'mykey', storage_table_host:'mycosmosdb_endpoint')
table_client = Azure::Storage::Table::TableService.new(client: common_client)
```

## <a name="create-a-table"></a><span data-ttu-id="957ac-131">Create a table</span><span class="sxs-lookup"><span data-stu-id="957ac-131">Create a table</span></span>
<span data-ttu-id="957ac-132">The **Azure::Storage::Table::TableService** object lets you work with tables and entities.</span><span class="sxs-lookup"><span data-stu-id="957ac-132">The **Azure::Storage::Table::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="957ac-133">To create a table, use the **create_table()** method.</span><span class="sxs-lookup"><span data-stu-id="957ac-133">To create a table, use the **create_table()** method.</span></span> <span data-ttu-id="957ac-134">The following example creates a table or prints the error if there is any.</span><span class="sxs-lookup"><span data-stu-id="957ac-134">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::Storage::Table::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="957ac-135">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="957ac-135">Add an entity to a table</span></span>
<span data-ttu-id="957ac-136">To add an entity, first create a hash object that defines your entity properties.</span><span class="sxs-lookup"><span data-stu-id="957ac-136">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="957ac-137">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="957ac-137">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="957ac-138">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span><span class="sxs-lookup"><span data-stu-id="957ac-138">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="957ac-139">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span><span class="sxs-lookup"><span data-stu-id="957ac-139">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="957ac-140">Entities with the same **PartitionKey** are stored on the same node.</span><span class="sxs-lookup"><span data-stu-id="957ac-140">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="957ac-141">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span><span class="sxs-lookup"><span data-stu-id="957ac-141">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="957ac-142">Update an entity</span><span class="sxs-lookup"><span data-stu-id="957ac-142">Update an entity</span></span>
<span data-ttu-id="957ac-143">There are multiple methods available to update an existing entity:</span><span class="sxs-lookup"><span data-stu-id="957ac-143">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="957ac-144">**update_entity():** Update an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="957ac-144">**update_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="957ac-145">**merge_entity():** Updates an existing entity by merging new property values into the existing entity.</span><span class="sxs-lookup"><span data-stu-id="957ac-145">**merge_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="957ac-146">**insert_or_merge_entity():** Updates an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="957ac-146">**insert_or_merge_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="957ac-147">If no entity exists, a new one will be inserted:</span><span class="sxs-lookup"><span data-stu-id="957ac-147">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="957ac-148">**insert_or_replace_entity():** Updates an existing entity by merging new property values into the existing entity.</span><span class="sxs-lookup"><span data-stu-id="957ac-148">**insert_or_replace_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="957ac-149">If no entity exists, a new one will be inserted.</span><span class="sxs-lookup"><span data-stu-id="957ac-149">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="957ac-150">The following example demonstrates updating an entity using **update_entity()**:</span><span class="sxs-lookup"><span data-stu-id="957ac-150">The following example demonstrates updating an entity using **update_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="957ac-151">With **update_entity()** and **merge_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span><span class="sxs-lookup"><span data-stu-id="957ac-151">With **update_entity()** and **merge_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="957ac-152">Therefore, if you want to store an entity regardless of whether it already exists, you should instead use **insert_or_replace_entity()** or **insert_or_merge_entity()**.</span><span class="sxs-lookup"><span data-stu-id="957ac-152">Therefore, if you want to store an entity regardless of whether it already exists, you should instead use **insert_or_replace_entity()** or **insert_or_merge_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="957ac-153">Work with groups of entities</span><span class="sxs-lookup"><span data-stu-id="957ac-153">Work with groups of entities</span></span>
<span data-ttu-id="957ac-154">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span><span class="sxs-lookup"><span data-stu-id="957ac-154">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="957ac-155">To accomplish that, you first create a **Batch** object and then use the **execute_batch()** method on **TableService**.</span><span class="sxs-lookup"><span data-stu-id="957ac-155">To accomplish that, you first create a **Batch** object and then use the **execute_batch()** method on **TableService**.</span></span> <span data-ttu-id="957ac-156">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span><span class="sxs-lookup"><span data-stu-id="957ac-156">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="957ac-157">Notice that it only works for entities with the same PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="957ac-157">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="957ac-158">Query for an entity</span><span class="sxs-lookup"><span data-stu-id="957ac-158">Query for an entity</span></span>
<span data-ttu-id="957ac-159">To query an entity in a table, use the **get_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="957ac-159">To query an entity in a table, use the **get_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="957ac-160">Query a set of entities</span><span class="sxs-lookup"><span data-stu-id="957ac-160">Query a set of entities</span></span>
<span data-ttu-id="957ac-161">To query a set of entities in a table, create a query hash object and use the **query_entities()** method.</span><span class="sxs-lookup"><span data-stu-id="957ac-161">To query a set of entities in a table, create a query hash object and use the **query_entities()** method.</span></span> <span data-ttu-id="957ac-162">The following example demonstrates getting all the entities with the same **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="957ac-162">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="957ac-163">If the result set is too large for a single query to return, a continuation token is returned that you can use to retrieve subsequent pages.</span><span class="sxs-lookup"><span data-stu-id="957ac-163">If the result set is too large for a single query to return, a continuation token is returned that you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="957ac-164">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="957ac-164">Query a subset of entity properties</span></span>
<span data-ttu-id="957ac-165">A query to a table can retrieve just a few properties from an entity.</span><span class="sxs-lookup"><span data-stu-id="957ac-165">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="957ac-166">This technique, called "projection," reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="957ac-166">This technique, called "projection," reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="957ac-167">Use the select clause and pass the names of the properties you would like to bring over to the client.</span><span class="sxs-lookup"><span data-stu-id="957ac-167">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="957ac-168">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="957ac-168">Delete an entity</span></span>
<span data-ttu-id="957ac-169">To delete an entity, use the **delete_entity()** method.</span><span class="sxs-lookup"><span data-stu-id="957ac-169">To delete an entity, use the **delete_entity()** method.</span></span> <span data-ttu-id="957ac-170">Pass in the name of the table that contains the entity, the PartitionKey, and the RowKey of the entity.</span><span class="sxs-lookup"><span data-stu-id="957ac-170">Pass in the name of the table that contains the entity, the PartitionKey, and the RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="957ac-171">Delete a table</span><span class="sxs-lookup"><span data-stu-id="957ac-171">Delete a table</span></span>
<span data-ttu-id="957ac-172">To delete a table, use the **delete_table()** method and pass in the name of the table you want to delete.</span><span class="sxs-lookup"><span data-stu-id="957ac-172">To delete a table, use the **delete_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="957ac-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="957ac-173">Next steps</span></span>

* <span data-ttu-id="957ac-174">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="957ac-174">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="957ac-175">Ruby Developer Center</span><span class="sxs-lookup"><span data-stu-id="957ac-175">Ruby Developer Center</span></span>](https://azure.microsoft.com/develop/ruby/)
* [<span data-ttu-id="957ac-176">Microsoft Azure Storage Table Client Library for Ruby</span><span class="sxs-lookup"><span data-stu-id="957ac-176">Microsoft Azure Storage Table Client Library for Ruby</span></span>](https://github.com/azure/azure-storage-ruby/tree/master/table) 

