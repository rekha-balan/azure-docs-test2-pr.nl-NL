---
title: How to use Azure Table Storage from Ruby | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage, a NoSQL data store.
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: ''
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e1df2fcf4478ef7f58c5686e85abd6ae94b5a2d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564201"
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="4c51d-103">How to use Azure Table Storage from Ruby</span><span class="sxs-lookup"><span data-stu-id="4c51d-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="4c51d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4c51d-104">Overview</span></span>
<span data-ttu-id="4c51d-105">This guide shows you how to perform common scenarios using the Azure Table service.</span><span class="sxs-lookup"><span data-stu-id="4c51d-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="4c51d-106">The samples are written using the Ruby API.</span><span class="sxs-lookup"><span data-stu-id="4c51d-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="4c51d-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span><span class="sxs-lookup"><span data-stu-id="4c51d-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="4c51d-108">Create a Ruby application</span><span class="sxs-lookup"><span data-stu-id="4c51d-108">Create a Ruby application</span></span>
<span data-ttu-id="4c51d-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c51d-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="4c51d-110">Configure your application to access Storage</span><span class="sxs-lookup"><span data-stu-id="4c51d-110">Configure your application to access Storage</span></span>
<span data-ttu-id="4c51d-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span><span class="sxs-lookup"><span data-stu-id="4c51d-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="4c51d-112">Use RubyGems to obtain the package</span><span class="sxs-lookup"><span data-stu-id="4c51d-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="4c51d-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="4c51d-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="4c51d-114">Type **gem install azure** in the command window to install the gem and dependencies.</span><span class="sxs-lookup"><span data-stu-id="4c51d-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="4c51d-115">Import the package</span><span class="sxs-lookup"><span data-stu-id="4c51d-115">Import the package</span></span>
<span data-ttu-id="4c51d-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span><span class="sxs-lookup"><span data-stu-id="4c51d-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="4c51d-117">Set up an Azure Storage connection</span><span class="sxs-lookup"><span data-stu-id="4c51d-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="4c51d-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="4c51d-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="4c51d-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span><span class="sxs-lookup"><span data-stu-id="4c51d-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="4c51d-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="4c51d-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="4c51d-121">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c51d-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c51d-122">Navigate to the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="4c51d-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="4c51d-123">In the Settings blade on the right, click **Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="4c51d-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="4c51d-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span><span class="sxs-lookup"><span data-stu-id="4c51d-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="4c51d-125">You can use either of these.</span><span class="sxs-lookup"><span data-stu-id="4c51d-125">You can use either of these.</span></span>
5. <span data-ttu-id="4c51d-126">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="4c51d-126">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="4c51d-127">To obtain these values from a classic storage account in the classic Azure portal:</span><span class="sxs-lookup"><span data-stu-id="4c51d-127">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="4c51d-128">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4c51d-128">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4c51d-129">Navigate to the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="4c51d-129">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="4c51d-130">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span><span class="sxs-lookup"><span data-stu-id="4c51d-130">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="4c51d-131">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span><span class="sxs-lookup"><span data-stu-id="4c51d-131">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="4c51d-132">For access key, you can use either the primary one or the secondary one.</span><span class="sxs-lookup"><span data-stu-id="4c51d-132">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="4c51d-133">Click the copy icon to copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="4c51d-133">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="4c51d-134">Create a table</span><span class="sxs-lookup"><span data-stu-id="4c51d-134">Create a table</span></span>
<span data-ttu-id="4c51d-135">The **Azure::TableService** object lets you work with tables and entities.</span><span class="sxs-lookup"><span data-stu-id="4c51d-135">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="4c51d-136">To create a table, use the **create\_table()** method.</span><span class="sxs-lookup"><span data-stu-id="4c51d-136">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="4c51d-137">The following example creates a table or prints the error if there is any.</span><span class="sxs-lookup"><span data-stu-id="4c51d-137">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="4c51d-138">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="4c51d-138">Add an entity to a table</span></span>
<span data-ttu-id="4c51d-139">To add an entity, first create a hash object that defines your entity properties.</span><span class="sxs-lookup"><span data-stu-id="4c51d-139">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="4c51d-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="4c51d-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="4c51d-141">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span><span class="sxs-lookup"><span data-stu-id="4c51d-141">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="4c51d-142">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span><span class="sxs-lookup"><span data-stu-id="4c51d-142">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="4c51d-143">Entities with the same **PartitionKey** are stored on the same node.</span><span class="sxs-lookup"><span data-stu-id="4c51d-143">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="4c51d-144">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span><span class="sxs-lookup"><span data-stu-id="4c51d-144">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="4c51d-145">Update an entity</span><span class="sxs-lookup"><span data-stu-id="4c51d-145">Update an entity</span></span>
<span data-ttu-id="4c51d-146">There are multiple methods available to update an existing entity:</span><span class="sxs-lookup"><span data-stu-id="4c51d-146">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="4c51d-147">**update\_entity():** Update an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="4c51d-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="4c51d-148">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span><span class="sxs-lookup"><span data-stu-id="4c51d-148">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="4c51d-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span><span class="sxs-lookup"><span data-stu-id="4c51d-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="4c51d-150">If no entity exists, a new one will be inserted:</span><span class="sxs-lookup"><span data-stu-id="4c51d-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="4c51d-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span><span class="sxs-lookup"><span data-stu-id="4c51d-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="4c51d-152">If no entity exists, a new one will be inserted.</span><span class="sxs-lookup"><span data-stu-id="4c51d-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="4c51d-153">The following example demonstrates updating an entity using **update\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="4c51d-153">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="4c51d-154">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span><span class="sxs-lookup"><span data-stu-id="4c51d-154">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="4c51d-155">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="4c51d-155">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="4c51d-156">Work with groups of entities</span><span class="sxs-lookup"><span data-stu-id="4c51d-156">Work with groups of entities</span></span>
<span data-ttu-id="4c51d-157">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span><span class="sxs-lookup"><span data-stu-id="4c51d-157">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="4c51d-158">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span><span class="sxs-lookup"><span data-stu-id="4c51d-158">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="4c51d-159">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span><span class="sxs-lookup"><span data-stu-id="4c51d-159">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="4c51d-160">Notice that it only works for entities with the same PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="4c51d-160">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="4c51d-161">Query for an entity</span><span class="sxs-lookup"><span data-stu-id="4c51d-161">Query for an entity</span></span>
<span data-ttu-id="4c51d-162">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="4c51d-162">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="4c51d-163">Query a set of entities</span><span class="sxs-lookup"><span data-stu-id="4c51d-163">Query a set of entities</span></span>
<span data-ttu-id="4c51d-164">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span><span class="sxs-lookup"><span data-stu-id="4c51d-164">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="4c51d-165">The following example demonstrates getting all the entities with the same **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="4c51d-165">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="4c51d-166">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span><span class="sxs-lookup"><span data-stu-id="4c51d-166">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="4c51d-167">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="4c51d-167">Query a subset of entity properties</span></span>
<span data-ttu-id="4c51d-168">A query to a table can retrieve just a few properties from an entity.</span><span class="sxs-lookup"><span data-stu-id="4c51d-168">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="4c51d-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="4c51d-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="4c51d-170">Use the select clause and pass the names of the properties you would like to bring over to the client.</span><span class="sxs-lookup"><span data-stu-id="4c51d-170">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="4c51d-171">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="4c51d-171">Delete an entity</span></span>
<span data-ttu-id="4c51d-172">To delete an entity, use the **delete\_entity()** method.</span><span class="sxs-lookup"><span data-stu-id="4c51d-172">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="4c51d-173">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span><span class="sxs-lookup"><span data-stu-id="4c51d-173">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="4c51d-174">Delete a table</span><span class="sxs-lookup"><span data-stu-id="4c51d-174">Delete a table</span></span>
<span data-ttu-id="4c51d-175">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span><span class="sxs-lookup"><span data-stu-id="4c51d-175">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="4c51d-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c51d-176">Next steps</span></span>
<span data-ttu-id="4c51d-177">To learn about more complex storage tasks, follow these links:</span><span class="sxs-lookup"><span data-stu-id="4c51d-177">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="4c51d-178">Azure Storage Team Blog</span><span class="sxs-lookup"><span data-stu-id="4c51d-178">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="4c51d-179">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span><span class="sxs-lookup"><span data-stu-id="4c51d-179">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

