---
title: How to use Azure Table Storage and Azure Cosmos DB Table API with C++ | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: cpp
ms.topic: sample
ms.date: 04/05/2018
ms.author: sngun
ms.openlocfilehash: 520c0868e51f1212ee1beca8967d3c08f1d6e869
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865211"
---
# <a name="how-to-use-azure-table-storage-and-azure-cosmos-db-table-api-with-c"></a><span data-ttu-id="e6818-103">How to use Azure Table storage and Azure Cosmos DB Table API with C++</span><span class="sxs-lookup"><span data-stu-id="e6818-103">How to use Azure Table storage and Azure Cosmos DB Table API with C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

## <a name="overview"></a><span data-ttu-id="e6818-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e6818-104">Overview</span></span>
<span data-ttu-id="e6818-105">This guide will show you how to perform common scenarios by using the Azure Table storage service or Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="e6818-105">This guide will show you how to perform common scenarios by using the Azure Table storage service or Azure Cosmos DB Table API.</span></span> <span data-ttu-id="e6818-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e6818-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="e6818-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span><span class="sxs-lookup"><span data-stu-id="e6818-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="e6818-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span><span class="sxs-lookup"><span data-stu-id="e6818-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="e6818-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="e6818-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 

## <a name="create-an-azure-service-account"></a><span data-ttu-id="e6818-110">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="e6818-110">Create an Azure service account</span></span>
[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="e6818-111">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="e6818-111">Create an Azure storage account</span></span>
[!INCLUDE [cosmos-db-create-storage-account](../../includes/cosmos-db-create-storage-account.md)]

### <a name="create-an-azure-cosmos-db-table-api-account"></a><span data-ttu-id="e6818-112">Create an Azure Cosmos DB Table API account</span><span class="sxs-lookup"><span data-stu-id="e6818-112">Create an Azure Cosmos DB Table API account</span></span>
[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="e6818-113">Create a C++ application</span><span class="sxs-lookup"><span data-stu-id="e6818-113">Create a C++ application</span></span>
<span data-ttu-id="e6818-114">In this guide, you will use storage features that can be run within a C++ application.</span><span class="sxs-lookup"><span data-stu-id="e6818-114">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="e6818-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e6818-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="e6818-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span><span class="sxs-lookup"><span data-stu-id="e6818-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="e6818-117">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span><span class="sxs-lookup"><span data-stu-id="e6818-117">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="e6818-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e6818-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="e6818-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span><span class="sxs-lookup"><span data-stu-id="e6818-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="e6818-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="e6818-120">Install-Package wastorage</span></span>

## <a name="configure-access-to-the-table-client-library"></a><span data-ttu-id="e6818-121">Configure access to the Table client library</span><span class="sxs-lookup"><span data-stu-id="e6818-121">Configure access to the Table client library</span></span>
<span data-ttu-id="e6818-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span><span class="sxs-lookup"><span data-stu-id="e6818-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

<span data-ttu-id="e6818-123">An Azure Storage client or Cosmos DB client uses a connection string to store endpoints and credentials to access data management services.</span><span class="sxs-lookup"><span data-stu-id="e6818-123">An Azure Storage client or Cosmos DB client uses a connection string to store endpoints and credentials to access data management services.</span></span> <span data-ttu-id="e6818-124">When running a client application, you must provide the storage connection string or Azure Cosmos DB connection string in the appropriate format.</span><span class="sxs-lookup"><span data-stu-id="e6818-124">When running a client application, you must provide the storage connection string or Azure Cosmos DB connection string in the appropriate format.</span></span>

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e6818-125">Set up an Azure Storage connection string</span><span class="sxs-lookup"><span data-stu-id="e6818-125">Set up an Azure Storage connection string</span></span>
 <span data-ttu-id="e6818-126">Use the name of your Storage account and the access key for the Storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span><span class="sxs-lookup"><span data-stu-id="e6818-126">Use the name of your Storage account and the access key for the Storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e6818-127">For information on Storage accounts and access keys, see [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e6818-127">For information on Storage accounts and access keys, see [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e6818-128">This example shows how you can declare a static field to hold the Azure Storage connection string:</span><span class="sxs-lookup"><span data-stu-id="e6818-128">This example shows how you can declare a static field to hold the Azure Storage connection string:</span></span>  

```cpp
// Define the Storage connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="set-up-an-azure-cosmos-db-connection-string"></a><span data-ttu-id="e6818-129">Set up an Azure Cosmos DB connection string</span><span class="sxs-lookup"><span data-stu-id="e6818-129">Set up an Azure Cosmos DB connection string</span></span>
<span data-ttu-id="e6818-130">Use the name of your Azure Cosmos DB account, your primary key, and endpoint listed in the [Azure Portal](https://portal.azure.com) for the *Account Name*, *Primary Key*, and *Endpoint* values.</span><span class="sxs-lookup"><span data-stu-id="e6818-130">Use the name of your Azure Cosmos DB account, your primary key, and endpoint listed in the [Azure Portal](https://portal.azure.com) for the *Account Name*, *Primary Key*, and *Endpoint* values.</span></span> <span data-ttu-id="e6818-131">This example shows how you can declare a static field to hold the Azure Cosmos DB connection string:</span><span class="sxs-lookup"><span data-stu-id="e6818-131">This example shows how you can declare a static field to hold the Azure Cosmos DB connection string:</span></span>

```cpp
// Define the Azure Cosmos DB connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_cosmos_db_account;AccountKey=your_cosmos_db_account_key;TableEndpoint=your_cosmos_db_endpoint"));
```


<span data-ttu-id="e6818-132">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e6818-132">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="e6818-133">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span><span class="sxs-lookup"><span data-stu-id="e6818-133">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="e6818-134">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span><span class="sxs-lookup"><span data-stu-id="e6818-134">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="e6818-135">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span><span class="sxs-lookup"><span data-stu-id="e6818-135">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="e6818-136">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span><span class="sxs-lookup"><span data-stu-id="e6818-136">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="e6818-137">The following samples assume that you have used one of these two methods to get the storage connection string.</span><span class="sxs-lookup"><span data-stu-id="e6818-137">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="e6818-138">Retrieve your connection string</span><span class="sxs-lookup"><span data-stu-id="e6818-138">Retrieve your connection string</span></span>
<span data-ttu-id="e6818-139">You can use the **cloud_storage_account** class to represent your storage account information.</span><span class="sxs-lookup"><span data-stu-id="e6818-139">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="e6818-140">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span><span class="sxs-lookup"><span data-stu-id="e6818-140">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="e6818-141">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span><span class="sxs-lookup"><span data-stu-id="e6818-141">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="e6818-142">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span><span class="sxs-lookup"><span data-stu-id="e6818-142">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="e6818-143">Create a table</span><span class="sxs-lookup"><span data-stu-id="e6818-143">Create a table</span></span>
<span data-ttu-id="e6818-144">A **cloud_table_client** object lets you get reference objects for tables and entities.</span><span class="sxs-lookup"><span data-stu-id="e6818-144">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="e6818-145">The following code creates a **cloud_table_client** object and uses it to create a new table.</span><span class="sxs-lookup"><span data-stu-id="e6818-145">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e6818-146">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="e6818-146">Add an entity to a table</span></span>
<span data-ttu-id="e6818-147">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="e6818-147">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="e6818-148">The following code uses the customer's first name as the row key and last name as the partition key.</span><span class="sxs-lookup"><span data-stu-id="e6818-148">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="e6818-149">Together, an entity's partition and row key uniquely identify the entity in the table.</span><span class="sxs-lookup"><span data-stu-id="e6818-149">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="e6818-150">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span><span class="sxs-lookup"><span data-stu-id="e6818-150">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="e6818-151">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="e6818-151">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="e6818-152">The following code creates a new instance of **table_entity** with some customer data to be stored.</span><span class="sxs-lookup"><span data-stu-id="e6818-152">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="e6818-153">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span><span class="sxs-lookup"><span data-stu-id="e6818-153">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="e6818-154">Finally, the code calls the execute method on the **cloud_table** object.</span><span class="sxs-lookup"><span data-stu-id="e6818-154">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="e6818-155">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span><span class="sxs-lookup"><span data-stu-id="e6818-155">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="e6818-156">Insert a batch of entities</span><span class="sxs-lookup"><span data-stu-id="e6818-156">Insert a batch of entities</span></span>
<span data-ttu-id="e6818-157">You can insert a batch of entities to the Table service in one write operation.</span><span class="sxs-lookup"><span data-stu-id="e6818-157">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="e6818-158">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span><span class="sxs-lookup"><span data-stu-id="e6818-158">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="e6818-159">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span><span class="sxs-lookup"><span data-stu-id="e6818-159">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="e6818-160">Then, **cloud_table.execute** is called to execute the operation.</span><span class="sxs-lookup"><span data-stu-id="e6818-160">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="e6818-161">Some things to note on batch operations:</span><span class="sxs-lookup"><span data-stu-id="e6818-161">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="e6818-162">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span><span class="sxs-lookup"><span data-stu-id="e6818-162">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="e6818-163">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span><span class="sxs-lookup"><span data-stu-id="e6818-163">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="e6818-164">All entities in a single batch operation must have the same partition key.</span><span class="sxs-lookup"><span data-stu-id="e6818-164">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="e6818-165">A batch operation is limited to a 4-MB data payload.</span><span class="sxs-lookup"><span data-stu-id="e6818-165">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="e6818-166">Retrieve all entities in a partition</span><span class="sxs-lookup"><span data-stu-id="e6818-166">Retrieve all entities in a partition</span></span>
<span data-ttu-id="e6818-167">To query a table for all entities in a partition, use a **table_query** object.</span><span class="sxs-lookup"><span data-stu-id="e6818-167">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="e6818-168">The following code example specifies a filter for entities where 'Smith' is the partition key.</span><span class="sxs-lookup"><span data-stu-id="e6818-168">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="e6818-169">This example prints the fields of each entity in the query results to the console.</span><span class="sxs-lookup"><span data-stu-id="e6818-169">This example prints the fields of each entity in the query results to the console.</span></span>  

> [!NOTE]
> <span data-ttu-id="e6818-170">These methods are not currently supported for C++ in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e6818-170">These methods are not currently supported for C++ in Azure Cosmos DB.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="e6818-171">The query in this example brings all the entities that match the filter criteria.</span><span class="sxs-lookup"><span data-stu-id="e6818-171">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="e6818-172">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span><span class="sxs-lookup"><span data-stu-id="e6818-172">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="e6818-173">Retrieve a range of entities in a partition</span><span class="sxs-lookup"><span data-stu-id="e6818-173">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="e6818-174">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span><span class="sxs-lookup"><span data-stu-id="e6818-174">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="e6818-175">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span><span class="sxs-lookup"><span data-stu-id="e6818-175">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

> [!NOTE]
> <span data-ttu-id="e6818-176">These methods are not currently supported for C++ in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e6818-176">These methods are not currently supported for C++ in Azure Cosmos DB.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="e6818-177">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="e6818-177">Retrieve a single entity</span></span>
<span data-ttu-id="e6818-178">You can write a query to retrieve a single, specific entity.</span><span class="sxs-lookup"><span data-stu-id="e6818-178">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="e6818-179">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span><span class="sxs-lookup"><span data-stu-id="e6818-179">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="e6818-180">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span><span class="sxs-lookup"><span data-stu-id="e6818-180">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="e6818-181">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span><span class="sxs-lookup"><span data-stu-id="e6818-181">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="e6818-182">Replace an entity</span><span class="sxs-lookup"><span data-stu-id="e6818-182">Replace an entity</span></span>
<span data-ttu-id="e6818-183">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span><span class="sxs-lookup"><span data-stu-id="e6818-183">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="e6818-184">The following code changes an existing customer's phone number and email address.</span><span class="sxs-lookup"><span data-stu-id="e6818-184">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="e6818-185">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="e6818-185">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="e6818-186">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span><span class="sxs-lookup"><span data-stu-id="e6818-186">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="e6818-187">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span><span class="sxs-lookup"><span data-stu-id="e6818-187">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="e6818-188">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span><span class="sxs-lookup"><span data-stu-id="e6818-188">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="e6818-189">The next section will show you how to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="e6818-189">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="e6818-190">Insert-or-replace an entity</span><span class="sxs-lookup"><span data-stu-id="e6818-190">Insert-or-replace an entity</span></span>
<span data-ttu-id="e6818-191">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span><span class="sxs-lookup"><span data-stu-id="e6818-191">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="e6818-192">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span><span class="sxs-lookup"><span data-stu-id="e6818-192">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="e6818-193">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span><span class="sxs-lookup"><span data-stu-id="e6818-193">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="e6818-194">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span><span class="sxs-lookup"><span data-stu-id="e6818-194">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="e6818-195">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span><span class="sxs-lookup"><span data-stu-id="e6818-195">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="e6818-196">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="e6818-196">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="e6818-197">Any updates made to the entity between the retrieval and update operation will be overwritten.</span><span class="sxs-lookup"><span data-stu-id="e6818-197">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="e6818-198">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="e6818-198">Query a subset of entity properties</span></span>
<span data-ttu-id="e6818-199">A query to a table can retrieve just a few properties from an entity.</span><span class="sxs-lookup"><span data-stu-id="e6818-199">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="e6818-200">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span><span class="sxs-lookup"><span data-stu-id="e6818-200">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="e6818-201">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span><span class="sxs-lookup"><span data-stu-id="e6818-201">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="e6818-202">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="e6818-202">Delete an entity</span></span>
<span data-ttu-id="e6818-203">You can easily delete an entity after you have retrieved it.</span><span class="sxs-lookup"><span data-stu-id="e6818-203">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="e6818-204">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span><span class="sxs-lookup"><span data-stu-id="e6818-204">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="e6818-205">Then call the **cloud_table.execute** method.</span><span class="sxs-lookup"><span data-stu-id="e6818-205">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="e6818-206">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span><span class="sxs-lookup"><span data-stu-id="e6818-206">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="e6818-207">Delete a table</span><span class="sxs-lookup"><span data-stu-id="e6818-207">Delete a table</span></span>
<span data-ttu-id="e6818-208">Finally, the following code example deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="e6818-208">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="e6818-209">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span><span class="sxs-lookup"><span data-stu-id="e6818-209">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Delete the table if it exists
if (table.delete_table_if_exists())
    {
        std::cout << "Table deleted!";
    }
    else
    {
        std::cout << "Table didn't exist";
    }
```

## <a name="troubleshooting"></a><span data-ttu-id="e6818-210">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="e6818-210">Troubleshooting</span></span>
* <span data-ttu-id="e6818-211">Build errors in Visual Studio 2017 Community Edition</span><span class="sxs-lookup"><span data-stu-id="e6818-211">Build errors in Visual Studio 2017 Community Edition</span></span>

  <span data-ttu-id="e6818-212">If your project gets build errors because of the include files storage_account.h and table.h, remove the **/permissive-** compiler switch.</span><span class="sxs-lookup"><span data-stu-id="e6818-212">If your project gets build errors because of the include files storage_account.h and table.h, remove the **/permissive-** compiler switch.</span></span> 
  - <span data-ttu-id="e6818-213">In **Solution Explorer**, right-click your project and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="e6818-213">In **Solution Explorer**, right-click your project and select **Properties**.</span></span>
  - <span data-ttu-id="e6818-214">In the **Property Pages** dialog box, expand **Configuration Properties**, expand **C/C++**, and select **Language**.</span><span class="sxs-lookup"><span data-stu-id="e6818-214">In the **Property Pages** dialog box, expand **Configuration Properties**, expand **C/C++**, and select **Language**.</span></span>
  - <span data-ttu-id="e6818-215">Set **Conformance mode** to **No**.</span><span class="sxs-lookup"><span data-stu-id="e6818-215">Set **Conformance mode** to **No**.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="e6818-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6818-216">Next steps</span></span>
<span data-ttu-id="e6818-217">Follow these links to learn more about Azure Storage and the Table API in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="e6818-217">Follow these links to learn more about Azure Storage and the Table API in Azure Cosmos DB:</span></span> 

* [<span data-ttu-id="e6818-218">Introduction to the Table API</span><span class="sxs-lookup"><span data-stu-id="e6818-218">Introduction to the Table API</span></span>](table-introduction.md)
* <span data-ttu-id="e6818-219">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="e6818-219">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="e6818-220">List Azure Storage resources in C++</span><span class="sxs-lookup"><span data-stu-id="e6818-220">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="e6818-221">Storage Client Library for C++ reference</span><span class="sxs-lookup"><span data-stu-id="e6818-221">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="e6818-222">Azure Storage documentation</span><span class="sxs-lookup"><span data-stu-id="e6818-222">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
