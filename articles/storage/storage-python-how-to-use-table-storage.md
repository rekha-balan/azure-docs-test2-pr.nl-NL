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
# <a name="how-to-use-table-storage-from-python"></a><span data-ttu-id="2ec15-103">How to use Table storage from Python</span><span class="sxs-lookup"><span data-stu-id="2ec15-103">How to use Table storage from Python</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]

[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="2ec15-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2ec15-104">Overview</span></span>
<span data-ttu-id="2ec15-105">This guide shows you how to perform common scenarios by using the Azure Table storage service.</span><span class="sxs-lookup"><span data-stu-id="2ec15-105">This guide shows you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="2ec15-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span><span class="sxs-lookup"><span data-stu-id="2ec15-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="2ec15-107">The covered scenarios include creating and deleting a table, in addition to inserting and querying entities in a table.</span><span class="sxs-lookup"><span data-stu-id="2ec15-107">The covered scenarios include creating and deleting a table, in addition to inserting and querying entities in a table.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-table"></a><span data-ttu-id="2ec15-108">Create a table</span><span class="sxs-lookup"><span data-stu-id="2ec15-108">Create a table</span></span>
<span data-ttu-id="2ec15-109">The **TableService** object lets you work with table services.</span><span class="sxs-lookup"><span data-stu-id="2ec15-109">The **TableService** object lets you work with table services.</span></span> <span data-ttu-id="2ec15-110">The following code creates a **TableService** object.</span><span class="sxs-lookup"><span data-stu-id="2ec15-110">The following code creates a **TableService** object.</span></span> <span data-ttu-id="2ec15-111">Add the code near the top of any Python file in which you wish to programmatically access Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="2ec15-111">Add the code near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="2ec15-112">The following code creates a **TableService** object by using the storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="2ec15-112">The following code creates a **TableService** object by using the storage account name and account key.</span></span>  <span data-ttu-id="2ec15-113">Replace 'myaccount' and 'mykey' with your account name and key.</span><span class="sxs-lookup"><span data-stu-id="2ec15-113">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="2ec15-114">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="2ec15-114">Add an entity to a table</span></span>
<span data-ttu-id="2ec15-115">To add an entity, first create a dictionary or Entity that defines your entity property names and values.</span><span class="sxs-lookup"><span data-stu-id="2ec15-115">To add an entity, first create a dictionary or Entity that defines your entity property names and values.</span></span> <span data-ttu-id="2ec15-116">Note that for every entity, you must specify **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="2ec15-116">Note that for every entity, you must specify **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="2ec15-117">These are the unique identifiers of your entities.</span><span class="sxs-lookup"><span data-stu-id="2ec15-117">These are the unique identifiers of your entities.</span></span> <span data-ttu-id="2ec15-118">You can query using these values much faster than you can query your other properties.</span><span class="sxs-lookup"><span data-stu-id="2ec15-118">You can query using these values much faster than you can query your other properties.</span></span> <span data-ttu-id="2ec15-119">The system uses **PartitionKey** to automatically distribute the table entities over many storage nodes.</span><span class="sxs-lookup"><span data-stu-id="2ec15-119">The system uses **PartitionKey** to automatically distribute the table entities over many storage nodes.</span></span>
<span data-ttu-id="2ec15-120">Entities that have the same **PartitionKey** are stored on the same node.</span><span class="sxs-lookup"><span data-stu-id="2ec15-120">Entities that have the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="2ec15-121">**RowKey** is the unique ID of the entity within the partition that it belongs to.</span><span class="sxs-lookup"><span data-stu-id="2ec15-121">**RowKey** is the unique ID of the entity within the partition that it belongs to.</span></span>

<span data-ttu-id="2ec15-122">To add an entity to your table, pass a dictionary object to the **insert\_entity** method.</span><span class="sxs-lookup"><span data-stu-id="2ec15-122">To add an entity to your table, pass a dictionary object to the **insert\_entity** method.</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '1', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="2ec15-123">You can also pass an instance of the **Entity** class to the **insert\_entity** method.</span><span class="sxs-lookup"><span data-stu-id="2ec15-123">You can also pass an instance of the **Entity** class to the **insert\_entity** method.</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '2'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

## <a name="update-an-entity"></a><span data-ttu-id="2ec15-124">Update an entity</span><span class="sxs-lookup"><span data-stu-id="2ec15-124">Update an entity</span></span>
<span data-ttu-id="2ec15-125">This code shows how to replace the old version of an existing entity with an updated version.</span><span class="sxs-lookup"><span data-stu-id="2ec15-125">This code shows how to replace the old version of an existing entity with an updated version.</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '1', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', 'tasksSeattle', '1', task, content_type='application/atom+xml')
```

<span data-ttu-id="2ec15-126">If the entity that is being updated does not exist, then the update operation will fail.</span><span class="sxs-lookup"><span data-stu-id="2ec15-126">If the entity that is being updated does not exist, then the update operation will fail.</span></span> <span data-ttu-id="2ec15-127">If you want to store an entity regardless of whether it existed before, use **insert\_or\_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="2ec15-127">If you want to store an entity regardless of whether it existed before, use **insert\_or\_replace_entity**.</span></span>
<span data-ttu-id="2ec15-128">In the following example, the first call will replace the existing entity.</span><span class="sxs-lookup"><span data-stu-id="2ec15-128">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="2ec15-129">The second call will insert a new entity, since no entity with the specified **PartitionKey** and **RowKey** exists in the table.</span><span class="sxs-lookup"><span data-stu-id="2ec15-129">The second call will insert a new entity, since no entity with the specified **PartitionKey** and **RowKey** exists in the table.</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '1', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', 'tasksSeattle', '1', task, content_type='application/atom+xml')

task = {'PartitionKey': 'tasksSeattle', 'RowKey': '3', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', 'tasksSeattle', '1', task, content_type='application/atom+xml')
```

## <a name="change-a-group-of-entities"></a><span data-ttu-id="2ec15-130">Change a group of entities</span><span class="sxs-lookup"><span data-stu-id="2ec15-130">Change a group of entities</span></span>
<span data-ttu-id="2ec15-131">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span><span class="sxs-lookup"><span data-stu-id="2ec15-131">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="2ec15-132">To accomplish that, you use the **TableBatch** class.</span><span class="sxs-lookup"><span data-stu-id="2ec15-132">To accomplish that, you use the **TableBatch** class.</span></span> <span data-ttu-id="2ec15-133">When you do want to submit the batch, you call **commit\_batch**.</span><span class="sxs-lookup"><span data-stu-id="2ec15-133">When you do want to submit the batch, you call **commit\_batch**.</span></span> <span data-ttu-id="2ec15-134">Note that all entities must be in the same partition in order to be changed as a batch.</span><span class="sxs-lookup"><span data-stu-id="2ec15-134">Note that all entities must be in the same partition in order to be changed as a batch.</span></span> <span data-ttu-id="2ec15-135">The example below adds two entities together in a batch.</span><span class="sxs-lookup"><span data-stu-id="2ec15-135">The example below adds two entities together in a batch.</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task10 = {'PartitionKey': 'tasksSeattle', 'RowKey': '10', 'description' : 'Go grocery shopping', 'priority' : 400}
task11 = {'PartitionKey': 'tasksSeattle', 'RowKey': '11', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task10)
batch.insert_entity(task11)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="2ec15-136">Batches can also be used with the context manager syntax:</span><span class="sxs-lookup"><span data-stu-id="2ec15-136">Batches can also be used with the context manager syntax:</span></span>

```python
task12 = {'PartitionKey': 'tasksSeattle', 'RowKey': '12', 'description' : 'Go grocery shopping', 'priority' : 400}
task13 = {'PartitionKey': 'tasksSeattle', 'RowKey': '13', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task12)
    batch.insert_entity(task13)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="2ec15-137">Query for an entity</span><span class="sxs-lookup"><span data-stu-id="2ec15-137">Query for an entity</span></span>
<span data-ttu-id="2ec15-138">To query an entity in a table, use the **get\_entity** method by passing **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="2ec15-138">To query an entity in a table, use the **get\_entity** method by passing **PartitionKey** and **RowKey**.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '1')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="2ec15-139">Query a set of entities</span><span class="sxs-lookup"><span data-stu-id="2ec15-139">Query a set of entities</span></span>
<span data-ttu-id="2ec15-140">This example finds all tasks in Seattle based on **PartitionKey**.</span><span class="sxs-lookup"><span data-stu-id="2ec15-140">This example finds all tasks in Seattle based on **PartitionKey**.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="2ec15-141">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="2ec15-141">Query a subset of entity properties</span></span>
<span data-ttu-id="2ec15-142">A query to a table can retrieve just a few properties from an entity.</span><span class="sxs-lookup"><span data-stu-id="2ec15-142">A query to a table can retrieve just a few properties from an entity.</span></span>
<span data-ttu-id="2ec15-143">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="2ec15-143">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="2ec15-144">Use the **select** parameter and pass the names of the properties that you want to bring over to the client.</span><span class="sxs-lookup"><span data-stu-id="2ec15-144">Use the **select** parameter and pass the names of the properties that you want to bring over to the client.</span></span>

<span data-ttu-id="2ec15-145">The query in the following code returns only the descriptions of entities in the table.</span><span class="sxs-lookup"><span data-stu-id="2ec15-145">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="2ec15-146">The following snippet works only against the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2ec15-146">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="2ec15-147">It is not supported by the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="2ec15-147">It is not supported by the storage emulator.</span></span>
>
>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="2ec15-148">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="2ec15-148">Delete an entity</span></span>
<span data-ttu-id="2ec15-149">You can delete an entity by using its partition and row key.</span><span class="sxs-lookup"><span data-stu-id="2ec15-149">You can delete an entity by using its partition and row key.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '1')
```

## <a name="delete-a-table"></a><span data-ttu-id="2ec15-150">Delete a table</span><span class="sxs-lookup"><span data-stu-id="2ec15-150">Delete a table</span></span>
<span data-ttu-id="2ec15-151">The following code deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="2ec15-151">The following code deletes a table from a storage account.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="2ec15-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ec15-152">Next steps</span></span>
<span data-ttu-id="2ec15-153">Now that you've learned the basics of Table storage, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="2ec15-153">Now that you've learned the basics of Table storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="2ec15-154">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="2ec15-154">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="2ec15-155">Azure Storage Services REST API</span><span class="sxs-lookup"><span data-stu-id="2ec15-155">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="2ec15-156">[Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="2ec15-156">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="2ec15-157">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="2ec15-157">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Storage Team blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python
