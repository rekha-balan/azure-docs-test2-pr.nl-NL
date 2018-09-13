---
title: Get started with Azure Table storage and the Azure Cosmos DB Table API using Python | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: python
ms.topic: sample
ms.date: 04/05/2018
ms.author: sngun
ms.openlocfilehash: 4e9d1742401e30d451282ea8dc22a56c0347dbf9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857372"
---
# <a name="get-started-with-azure-table-storage-and-the-azure-cosmos-db-table-api-using-python"></a><span data-ttu-id="0ba75-103">Get started with Azure Table storage and the Azure Cosmos DB Table API using Python</span><span class="sxs-lookup"><span data-stu-id="0ba75-103">Get started with Azure Table storage and the Azure Cosmos DB Table API using Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

<span data-ttu-id="0ba75-104">Azure Table storage and Azure Cosmos DB are services that store structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span><span class="sxs-lookup"><span data-stu-id="0ba75-104">Azure Table storage and Azure Cosmos DB are services that store structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="0ba75-105">Because Table storage and Azure Cosmos DB are schemaless, it's easy to adapt your data as the needs of your application evolve.</span><span class="sxs-lookup"><span data-stu-id="0ba75-105">Because Table storage and Azure Cosmos DB are schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="0ba75-106">Access to Table storage and Table API data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span><span class="sxs-lookup"><span data-stu-id="0ba75-106">Access to Table storage and Table API data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="0ba75-107">You can use Table storage or Azure Cosmos DB to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span><span class="sxs-lookup"><span data-stu-id="0ba75-107">You can use Table storage or Azure Cosmos DB to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="0ba75-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span><span class="sxs-lookup"><span data-stu-id="0ba75-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-sample"></a><span data-ttu-id="0ba75-109">About this sample</span><span class="sxs-lookup"><span data-stu-id="0ba75-109">About this sample</span></span>
<span data-ttu-id="0ba75-110">This sample shows you how to use the [Azure Cosmos DB Table SDK for Python](https://pypi.python.org/pypi/azure-cosmosdb-table/) in common Azure Table storage scenarios.</span><span class="sxs-lookup"><span data-stu-id="0ba75-110">This sample shows you how to use the [Azure Cosmos DB Table SDK for Python](https://pypi.python.org/pypi/azure-cosmosdb-table/) in common Azure Table storage scenarios.</span></span> <span data-ttu-id="0ba75-111">The name of the SDK indicates it is for use with Azure Cosmos DB, but it works with both Azure Cosmos DB and Azure Tables storage, each service just has a unique endpoint.</span><span class="sxs-lookup"><span data-stu-id="0ba75-111">The name of the SDK indicates it is for use with Azure Cosmos DB, but it works with both Azure Cosmos DB and Azure Tables storage, each service just has a unique endpoint.</span></span> <span data-ttu-id="0ba75-112">These scenarios are explored using Python examples that illustrate how to:</span><span class="sxs-lookup"><span data-stu-id="0ba75-112">These scenarios are explored using Python examples that illustrate how to:</span></span>
* <span data-ttu-id="0ba75-113">Create and delete tables</span><span class="sxs-lookup"><span data-stu-id="0ba75-113">Create and delete tables</span></span>
* <span data-ttu-id="0ba75-114">Insert and query entities</span><span class="sxs-lookup"><span data-stu-id="0ba75-114">Insert and query entities</span></span>
* <span data-ttu-id="0ba75-115">Modify entities</span><span class="sxs-lookup"><span data-stu-id="0ba75-115">Modify entities</span></span>

<span data-ttu-id="0ba75-116">While working through the scenarios in this sample, you may want to refer to the [Azure Cosmos DB SDK for Python API reference](https://azure.github.io/azure-cosmosdb-python/).</span><span class="sxs-lookup"><span data-stu-id="0ba75-116">While working through the scenarios in this sample, you may want to refer to the [Azure Cosmos DB SDK for Python API reference](https://azure.github.io/azure-cosmosdb-python/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ba75-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0ba75-117">Prerequisites</span></span>

<span data-ttu-id="0ba75-118">You need the following to complete this sample successfully:</span><span class="sxs-lookup"><span data-stu-id="0ba75-118">You need the following to complete this sample successfully:</span></span>

- <span data-ttu-id="0ba75-119">[Python](https://www.python.org/downloads/) 2.7, 3.3, 3.4, 3.5, or 3.6</span><span class="sxs-lookup"><span data-stu-id="0ba75-119">[Python](https://www.python.org/downloads/) 2.7, 3.3, 3.4, 3.5, or 3.6</span></span>
- <span data-ttu-id="0ba75-120">[Azure Cosmos DB Table SDK for Python](https://pypi.python.org/pypi/azure-cosmosdb-table/).</span><span class="sxs-lookup"><span data-stu-id="0ba75-120">[Azure Cosmos DB Table SDK for Python](https://pypi.python.org/pypi/azure-cosmosdb-table/).</span></span> <span data-ttu-id="0ba75-121">This SDK connects with both Azure Table storage and the Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="0ba75-121">This SDK connects with both Azure Table storage and the Azure Cosmos DB Table API.</span></span>
- <span data-ttu-id="0ba75-122">[Azure Storage account](../storage/common/storage-quickstart-create-account.md) or [Azure Cosmos DB account](https://azure.microsoft.com/try/cosmosdb/)</span><span class="sxs-lookup"><span data-stu-id="0ba75-122">[Azure Storage account](../storage/common/storage-quickstart-create-account.md) or [Azure Cosmos DB account](https://azure.microsoft.com/try/cosmosdb/)</span></span>

## <a name="create-an-azure-service-account"></a><span data-ttu-id="0ba75-123">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="0ba75-123">Create an Azure service account</span></span>
[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="0ba75-124">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="0ba75-124">Create an Azure storage account</span></span>
[!INCLUDE [cosmos-db-create-storage-account](../../includes/cosmos-db-create-storage-account.md)]

### <a name="create-an-azure-cosmos-db-table-api-account"></a><span data-ttu-id="0ba75-125">Create an Azure Cosmos DB Table API account</span><span class="sxs-lookup"><span data-stu-id="0ba75-125">Create an Azure Cosmos DB Table API account</span></span>
[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

## <a name="install-the-azure-cosmos-db-table-sdk-for-python"></a><span data-ttu-id="0ba75-126">Install the Azure Cosmos DB Table SDK for Python</span><span class="sxs-lookup"><span data-stu-id="0ba75-126">Install the Azure Cosmos DB Table SDK for Python</span></span>

<span data-ttu-id="0ba75-127">After you've created a Storage account, your next step is to install the [Microsoft Azure Cosmos DB Table SDK for Python](https://pypi.python.org/pypi/azure-cosmosdb-table/).</span><span class="sxs-lookup"><span data-stu-id="0ba75-127">After you've created a Storage account, your next step is to install the [Microsoft Azure Cosmos DB Table SDK for Python](https://pypi.python.org/pypi/azure-cosmosdb-table/).</span></span> <span data-ttu-id="0ba75-128">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-cosmosdb-python/blob/master/azure-cosmosdb-table/README.rst) file in the Cosmos DB Table SDK for Python repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="0ba75-128">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-cosmosdb-python/blob/master/azure-cosmosdb-table/README.rst) file in the Cosmos DB Table SDK for Python repository on GitHub.</span></span>

## <a name="import-the-tableservice-and-entity-classes"></a><span data-ttu-id="0ba75-129">Import the TableService and Entity classes</span><span class="sxs-lookup"><span data-stu-id="0ba75-129">Import the TableService and Entity classes</span></span>

<span data-ttu-id="0ba75-130">To work with entities in the Azure Table service in Python, you use the [TableService](https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html) and [Entity][py_Entity] classes.</span><span class="sxs-lookup"><span data-stu-id="0ba75-130">To work with entities in the Azure Table service in Python, you use the [TableService](https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html) and [Entity][py_Entity] classes.</span></span> <span data-ttu-id="0ba75-131">Add this code near the top your Python file to import both:</span><span class="sxs-lookup"><span data-stu-id="0ba75-131">Add this code near the top your Python file to import both:</span></span>

```python
from azure.cosmosdb.table.tableservice import TableService
from azure.cosmosdb.table.models import Entity
```

## <a name="connect-to-azure-table-service"></a><span data-ttu-id="0ba75-132">Connect to Azure Table service</span><span class="sxs-lookup"><span data-stu-id="0ba75-132">Connect to Azure Table service</span></span>

<span data-ttu-id="0ba75-133">To connect to Azure Storage Table service, create a [TableService](https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html) object, and pass in your Storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="0ba75-133">To connect to Azure Storage Table service, create a [TableService](https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html) object, and pass in your Storage account name and account key.</span></span> <span data-ttu-id="0ba75-134">Replace `myaccount` and `mykey` with your account name and key.</span><span class="sxs-lookup"><span data-stu-id="0ba75-134">Replace `myaccount` and `mykey` with your account name and key.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')
```

## <a name="connect-to-azure-cosmos-db"></a><span data-ttu-id="0ba75-135">Connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0ba75-135">Connect to Azure Cosmos DB</span></span>

<span data-ttu-id="0ba75-136">To connect to Azure Cosmos DB, copy your primary connection string from the Azure portal, and create a [TableService](https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html) object using your copied connection string:</span><span class="sxs-lookup"><span data-stu-id="0ba75-136">To connect to Azure Cosmos DB, copy your primary connection string from the Azure portal, and create a [TableService](https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html) object using your copied connection string:</span></span>

```python
table_service = TableService(connection_string='DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;TableEndpoint=myendpoint;)
```

## <a name="create-a-table"></a><span data-ttu-id="0ba75-137">Create a table</span><span class="sxs-lookup"><span data-stu-id="0ba75-137">Create a table</span></span>

<span data-ttu-id="0ba75-138">Call [create_table][py_create_table] to create the table.</span><span class="sxs-lookup"><span data-stu-id="0ba75-138">Call [create_table][py_create_table] to create the table.</span></span>

```python
table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="0ba75-139">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="0ba75-139">Add an entity to a table</span></span>

<span data-ttu-id="0ba75-140">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService.insert_entity method][py_TableService].</span><span class="sxs-lookup"><span data-stu-id="0ba75-140">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService.insert_entity method][py_TableService].</span></span> <span data-ttu-id="0ba75-141">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span><span class="sxs-lookup"><span data-stu-id="0ba75-141">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="0ba75-142">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span><span class="sxs-lookup"><span data-stu-id="0ba75-142">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="0ba75-143">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span><span class="sxs-lookup"><span data-stu-id="0ba75-143">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="0ba75-144">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span><span class="sxs-lookup"><span data-stu-id="0ba75-144">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="0ba75-145">PartitionKey and RowKey</span><span class="sxs-lookup"><span data-stu-id="0ba75-145">PartitionKey and RowKey</span></span>

<span data-ttu-id="0ba75-146">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span><span class="sxs-lookup"><span data-stu-id="0ba75-146">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="0ba75-147">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span><span class="sxs-lookup"><span data-stu-id="0ba75-147">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="0ba75-148">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span><span class="sxs-lookup"><span data-stu-id="0ba75-148">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="0ba75-149">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span><span class="sxs-lookup"><span data-stu-id="0ba75-149">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="0ba75-150">Entities that have the same  **PartitionKey** are stored on the same node.</span><span class="sxs-lookup"><span data-stu-id="0ba75-150">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="0ba75-151">**RowKey** is the unique ID of the entity within the partition it belongs to.</span><span class="sxs-lookup"><span data-stu-id="0ba75-151">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="0ba75-152">Update an entity</span><span class="sxs-lookup"><span data-stu-id="0ba75-152">Update an entity</span></span>

<span data-ttu-id="0ba75-153">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span><span class="sxs-lookup"><span data-stu-id="0ba75-153">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="0ba75-154">This example shows how to replace an existing entity with an updated version:</span><span class="sxs-lookup"><span data-stu-id="0ba75-154">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="0ba75-155">If the entity that is being updated doesn't already exist, then the update operation will fail.</span><span class="sxs-lookup"><span data-stu-id="0ba75-155">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="0ba75-156">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="0ba75-156">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="0ba75-157">In the following example, the first call will replace the existing entity.</span><span class="sxs-lookup"><span data-stu-id="0ba75-157">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="0ba75-158">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span><span class="sxs-lookup"><span data-stu-id="0ba75-158">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="0ba75-159">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span><span class="sxs-lookup"><span data-stu-id="0ba75-159">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="0ba75-160">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span><span class="sxs-lookup"><span data-stu-id="0ba75-160">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="0ba75-161">Modify multiple entities</span><span class="sxs-lookup"><span data-stu-id="0ba75-161">Modify multiple entities</span></span>

<span data-ttu-id="0ba75-162">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span><span class="sxs-lookup"><span data-stu-id="0ba75-162">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="0ba75-163">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span><span class="sxs-lookup"><span data-stu-id="0ba75-163">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="0ba75-164">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span><span class="sxs-lookup"><span data-stu-id="0ba75-164">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="0ba75-165">All entities to be modified in batch must be in the same partition.</span><span class="sxs-lookup"><span data-stu-id="0ba75-165">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="0ba75-166">This example adds two entities together in a batch:</span><span class="sxs-lookup"><span data-stu-id="0ba75-166">This example adds two entities together in a batch:</span></span>

```python
from azure.cosmosdb.table.tablebatch import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="0ba75-167">Batches can also be used with the context manager syntax:</span><span class="sxs-lookup"><span data-stu-id="0ba75-167">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="0ba75-168">Query for an entity</span><span class="sxs-lookup"><span data-stu-id="0ba75-168">Query for an entity</span></span>

<span data-ttu-id="0ba75-169">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span><span class="sxs-lookup"><span data-stu-id="0ba75-169">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="0ba75-170">Query a set of entities</span><span class="sxs-lookup"><span data-stu-id="0ba75-170">Query a set of entities</span></span>

<span data-ttu-id="0ba75-171">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span><span class="sxs-lookup"><span data-stu-id="0ba75-171">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="0ba75-172">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="0ba75-172">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="0ba75-173">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="0ba75-173">Query a subset of entity properties</span></span>

<span data-ttu-id="0ba75-174">You can also restrict which properties are returned for each entity in a query.</span><span class="sxs-lookup"><span data-stu-id="0ba75-174">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="0ba75-175">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span><span class="sxs-lookup"><span data-stu-id="0ba75-175">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="0ba75-176">Use the **select** parameter and pass the names of the properties you want returned to the client.</span><span class="sxs-lookup"><span data-stu-id="0ba75-176">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="0ba75-177">The query in the following code returns only the descriptions of entities in the table.</span><span class="sxs-lookup"><span data-stu-id="0ba75-177">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="0ba75-178">The following snippet works only against the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ba75-178">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="0ba75-179">It is not supported by the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="0ba75-179">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="0ba75-180">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="0ba75-180">Delete an entity</span></span>

<span data-ttu-id="0ba75-181">Delete an entity by passing its **PartitionKey** and **RowKey** to the [delete_entity][py_delete_entity] method.</span><span class="sxs-lookup"><span data-stu-id="0ba75-181">Delete an entity by passing its **PartitionKey** and **RowKey** to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="0ba75-182">Delete a table</span><span class="sxs-lookup"><span data-stu-id="0ba75-182">Delete a table</span></span>

<span data-ttu-id="0ba75-183">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ba75-183">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="0ba75-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ba75-184">Next steps</span></span>

* [<span data-ttu-id="0ba75-185">FAQ - Develop with the Table API</span><span class="sxs-lookup"><span data-stu-id="0ba75-185">FAQ - Develop with the Table API</span></span>](https://docs.microsoft.com/azure/cosmos-db/faq#develop-with-the-table-api)
* [<span data-ttu-id="0ba75-186">Azure Cosmos DB SDK for Python API reference</span><span class="sxs-lookup"><span data-stu-id="0ba75-186">Azure Cosmos DB SDK for Python API reference</span></span>](https://azure.github.io/azure-cosmosdb-python/)
* [<span data-ttu-id="0ba75-187">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="0ba75-187">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="0ba75-188">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="0ba75-188">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="0ba75-189">Working with Python in Visual Studio (Windows)</span><span class="sxs-lookup"><span data-stu-id="0ba75-189">Working with Python in Visual Studio (Windows)</span></span>](https://docs.microsoft.com/visualstudio/python/overview-of-python-tools-for-visual-studio)

[py_commit_batch]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_create_table]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_delete_entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_delete_table]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_Entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.models.html
[py_get_entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_insert_entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_insert_or_replace_entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_TableService]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_TableBatch]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tablebatch.html
[py_merge_entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
[py_update_entity]: https://azure.github.io/azure-cosmosdb-python/ref/azure.cosmosdb.table.tableservice.html
