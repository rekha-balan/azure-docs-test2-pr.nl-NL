---
title: How to use Table storage from Python | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage, a NoSQL data store.
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 98b02e8faa21e6d0e04d2f2c70bee6b8b018c010
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553925"
---
# <a name="how-to-use-table-storage-from-python"></a>How to use Table storage from Python
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]

[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Overview
This guide shows you how to perform common scenarios by using the Azure Table storage service. The samples are written in Python and use the [Microsoft Azure Storage SDK for Python]. The covered scenarios include creating and deleting a table, in addition to inserting and querying entities in a table.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-table"></a>Create a table
The **TableService** object lets you work with table services. The following code creates a **TableService** object. Add the code near the top of any Python file in which you wish to programmatically access Azure Storage:

```python
from azure.storage.table import TableService, Entity
```

The following code creates a **TableService** object by using the storage account name and account key.  Replace 'myaccount' and 'mykey' with your account name and key.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a>Add an entity to a table
To add an entity, first create a dictionary or Entity that defines your entity property names and values. Note that for every entity, you must specify **PartitionKey** and **RowKey**. These are the unique identifiers of your entities. You can query using these values much faster than you can query your other properties. The system uses **PartitionKey** to automatically distribute the table entities over many storage nodes.
Entities that have the same **PartitionKey** are stored on the same node. **RowKey** is the unique ID of the entity within the partition that it belongs to.

To add an entity to your table, pass a dictionary object to the **insert\_entity** method.

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '1', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

You can also pass an instance of the **Entity** class to the **insert\_entity** method.

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '2'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

## <a name="update-an-entity"></a>Update an entity
This code shows how to replace the old version of an existing entity with an updated version.

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '1', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', 'tasksSeattle', '1', task, content_type='application/atom+xml')
```

If the entity that is being updated does not exist, then the update operation will fail. If you want to store an entity regardless of whether it existed before, use **insert\_or\_replace_entity**.
In the following example, the first call will replace the existing entity. The second call will insert a new entity, since no entity with the specified **PartitionKey** and **RowKey** exists in the table.

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '1', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', 'tasksSeattle', '1', task, content_type='application/atom+xml')

task = {'PartitionKey': 'tasksSeattle', 'RowKey': '3', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', 'tasksSeattle', '1', task, content_type='application/atom+xml')
```

## <a name="change-a-group-of-entities"></a>Change a group of entities
Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server. To accomplish that, you use the **TableBatch** class. When you do want to submit the batch, you call **commit\_batch**. Note that all entities must be in the same partition in order to be changed as a batch. The example below adds two entities together in a batch.

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task10 = {'PartitionKey': 'tasksSeattle', 'RowKey': '10', 'description' : 'Go grocery shopping', 'priority' : 400}
task11 = {'PartitionKey': 'tasksSeattle', 'RowKey': '11', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task10)
batch.insert_entity(task11)
table_service.commit_batch('tasktable', batch)
```

Batches can also be used with the context manager syntax:

```python
task12 = {'PartitionKey': 'tasksSeattle', 'RowKey': '12', 'description' : 'Go grocery shopping', 'priority' : 400}
task13 = {'PartitionKey': 'tasksSeattle', 'RowKey': '13', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task12)
    batch.insert_entity(task13)
```

## <a name="query-for-an-entity"></a>Query for an entity
To query an entity in a table, use the **get\_entity** method by passing **PartitionKey** and **RowKey**.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '1')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Query a set of entities
This example finds all tasks in Seattle based on **PartitionKey**.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Query a subset of entity properties
A query to a table can retrieve just a few properties from an entity.
This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities. Use the **select** parameter and pass the names of the properties that you want to bring over to the client.

The query in the following code returns only the descriptions of entities in the table.

> [!NOTE]
> The following snippet works only against the Azure Storage. It is not supported by the storage emulator.
>
>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Delete an entity
You can delete an entity by using its partition and row key.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '1')
```

## <a name="delete-a-table"></a>Delete a table
The following code deletes a table from a storage account.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Next steps
Now that you've learned the basics of Table storage, follow these links to learn more.

* [Python Developer Center](/develop/python/)
* [Azure Storage Services REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure Storage Team Blog]
* [Microsoft Azure Storage SDK for Python]

[Azure Storage Team blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python
