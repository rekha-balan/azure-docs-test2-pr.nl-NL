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
# <a name="how-to-use-azure-table-storage-from-ruby"></a>How to use Azure Table Storage from Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Overview
This guide shows you how to perform common scenarios using the Azure Table service. The samples are written using the Ruby API. The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Create a Ruby application
For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-to-access-storage"></a>Configure your application to access Storage
To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.

### <a name="use-rubygems-to-obtain-the-package"></a>Use RubyGems to obtain the package
1. Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).
2. Type **gem install azure** in the command window to install the gem and dependencies.

### <a name="import-the-package"></a>Import the package
Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Set up an Azure Storage connection
The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account. If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

To obtain these values from a classic or Resource Manager storage account in the Azure portal:

1. Log in to the [Azure portal](https://portal.azure.com).
2. Navigate to the storage account you want to use.
3. In the Settings blade on the right, click **Access Keys**.
4. In the Access keys blade that appears, you'll see the access key 1 and access key 2. You can use either of these.
5. Click the copy icon to copy the key to the clipboard.

To obtain these values from a classic storage account in the classic Azure portal:

1. Log in to the [Azure classic portal](https://manage.windowsazure.com).
2. Navigate to the storage account you want to use.
3. Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.
4. In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key. For access key, you can use either the primary one or the secondary one.
5. Click the copy icon to copy the key to the clipboard.

## <a name="create-a-table"></a>Create a table
The **Azure::TableService** object lets you work with tables and entities. To create a table, use the **create\_table()** method. The following example creates a table or prints the error if there is any.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a>Add an entity to a table
To add an entity, first create a hash object that defines your entity properties. Note that for every entity you must specify a **PartitionKey** and **RowKey**. These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties. Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes. Entities with the same **PartitionKey** are stored on the same node. The **RowKey** is the unique ID of the entity within the partition it belongs to.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Update an entity
There are multiple methods available to update an existing entity:

* **update\_entity():** Update an existing entity by replacing it.
* **merge\_entity():** Updates an existing entity by merging new property values into the existing entity.
* **insert\_or\_merge\_entity():** Updates an existing entity by replacing it. If no entity exists, a new one will be inserted:
* **insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity. If no entity exists, a new one will be inserted.

The following example demonstrates updating an entity using **update\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail. Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.

## <a name="work-with-groups-of-entities"></a>Work with groups of entities
Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server. To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**. The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch. Notice that it only works for entities with the same PartitionKey.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Query for an entity
To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Query a set of entities
To query a set of entities in a table, create a query hash object and use the **query\_entities()** method. The following example demonstrates getting all the entities with the same **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Query a subset of entity properties
A query to a table can retrieve just a few properties from an entity. This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities. Use the select clause and pass the names of the properties you would like to bring over to the client.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Delete an entity
To delete an entity, use the **delete\_entity()** method. You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Delete a table
To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Next steps
To learn about more complex storage tasks, follow these links:

* [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub

