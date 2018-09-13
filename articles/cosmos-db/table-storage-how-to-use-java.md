---
title: How to use Azure Table storage or the Azure Cosmos DB Table API from Java | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: Java
ms.topic: sample
ms.date: 04/05/2018
ms.author: sngun
ms.openlocfilehash: f4ebcf51ab6682009190e467ca9dbf67caf1c182
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871173"
---
# <a name="how-to-use-azure-table-storage-or-azure-cosmos-db-table-api-from-java"></a><span data-ttu-id="c06bb-103">How to use Azure Table storage or Azure Cosmos DB Table API from Java</span><span class="sxs-lookup"><span data-stu-id="c06bb-103">How to use Azure Table storage or Azure Cosmos DB Table API from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

## <a name="overview"></a><span data-ttu-id="c06bb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c06bb-104">Overview</span></span>
<span data-ttu-id="c06bb-105">This article demonstrates how to perform common scenarios using the Azure Table storage service and Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c06bb-105">This article demonstrates how to perform common scenarios using the Azure Table storage service and Azure Cosmos DB.</span></span> <span data-ttu-id="c06bb-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="c06bb-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="c06bb-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span><span class="sxs-lookup"><span data-stu-id="c06bb-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="c06bb-108">For more information on tables, see the [Next steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="c06bb-108">For more information on tables, see the [Next steps](#next-steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="c06bb-109">An SDK is available for developers who are using Azure Storage on Android devices.</span><span class="sxs-lookup"><span data-stu-id="c06bb-109">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="c06bb-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="c06bb-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>

## <a name="create-an-azure-service-account"></a><span data-ttu-id="c06bb-111">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="c06bb-111">Create an Azure service account</span></span>
[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="c06bb-112">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="c06bb-112">Create an Azure storage account</span></span>
[!INCLUDE [cosmos-db-create-storage-account](../../includes/cosmos-db-create-storage-account.md)]

### <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="c06bb-113">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="c06bb-113">Create an Azure Cosmos DB account</span></span>
[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="c06bb-114">Create a Java application</span><span class="sxs-lookup"><span data-stu-id="c06bb-114">Create a Java application</span></span>
<span data-ttu-id="c06bb-115">In this guide, you will use storage features that you can run in a Java application locally, or in code running in a web role or worker role in Azure.</span><span class="sxs-lookup"><span data-stu-id="c06bb-115">In this guide, you will use storage features that you can run in a Java application locally, or in code running in a web role or worker role in Azure.</span></span>

<span data-ttu-id="c06bb-116">To use the samples in this article, install the Java Development Kit (JDK), then create an Azure storage account or Azure Cosmos DB account in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c06bb-116">To use the samples in this article, install the Java Development Kit (JDK), then create an Azure storage account or Azure Cosmos DB account in your Azure subscription.</span></span> <span data-ttu-id="c06bb-117">Once you have done so, verify that your development system meets the minimum requirements and dependencies that are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="c06bb-117">Once you have done so, verify that your development system meets the minimum requirements and dependencies that are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="c06bb-118">If your system meets those requirements, you can follow the instructions to download and install the Azure Storage Libraries for Java on your system from that repository.</span><span class="sxs-lookup"><span data-stu-id="c06bb-118">If your system meets those requirements, you can follow the instructions to download and install the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="c06bb-119">After you complete those tasks, you can create a Java application that uses the examples in this article.</span><span class="sxs-lookup"><span data-stu-id="c06bb-119">After you complete those tasks, you can create a Java application that uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="c06bb-120">Configure your application to access table storage</span><span class="sxs-lookup"><span data-stu-id="c06bb-120">Configure your application to access table storage</span></span>
<span data-ttu-id="c06bb-121">Add the following import statements to the top of the Java file where you want to use Azure storage APIs or the Azure Cosmos DB Table API to access tables:</span><span class="sxs-lookup"><span data-stu-id="c06bb-121">Add the following import statements to the top of the Java file where you want to use Azure storage APIs or the Azure Cosmos DB Table API to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="add-an-azure-storage-connection-string"></a><span data-ttu-id="c06bb-122">Add an Azure storage connection string</span><span class="sxs-lookup"><span data-stu-id="c06bb-122">Add an Azure storage connection string</span></span>
<span data-ttu-id="c06bb-123">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span><span class="sxs-lookup"><span data-stu-id="c06bb-123">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c06bb-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span><span class="sxs-lookup"><span data-stu-id="c06bb-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> 

<span data-ttu-id="c06bb-125">This example shows how you can declare a static field to hold the connection string:</span><span class="sxs-lookup"><span data-stu-id="c06bb-125">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

## <a name="add-an-azure-cosmos-db-table-api-connection-string"></a><span data-ttu-id="c06bb-126">Add an Azure Cosmos DB Table API connection string</span><span class="sxs-lookup"><span data-stu-id="c06bb-126">Add an Azure Cosmos DB Table API connection string</span></span>
<span data-ttu-id="c06bb-127">An Azure Cosmos DB account uses a connection string to store the table endpoint and your credentials.</span><span class="sxs-lookup"><span data-stu-id="c06bb-127">An Azure Cosmos DB account uses a connection string to store the table endpoint and your credentials.</span></span> <span data-ttu-id="c06bb-128">When running in a client application, you must provide the Azure Cosmos DB connection string in the following format, using the name of your Azure Cosmos DB account and the primary access key for the account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span><span class="sxs-lookup"><span data-stu-id="c06bb-128">When running in a client application, you must provide the Azure Cosmos DB connection string in the following format, using the name of your Azure Cosmos DB account and the primary access key for the account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> 

<span data-ttu-id="c06bb-129">This example shows how you can declare a static field to hold the Azure Cosmos DB connection string:</span><span class="sxs-lookup"><span data-stu-id="c06bb-129">This example shows how you can declare a static field to hold the Azure Cosmos DB connection string:</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=https;" + 
    "AccountName=your_cosmosdb_account;" + 
    "AccountKey=your_account_key;" + 
    "TableEndpoint=https://your_endpoint;" ;
```

<span data-ttu-id="c06bb-130">In an application running within a role in Azure, you can store this string in the service configuration file, *ServiceConfiguration.cscfg*, and you can access it with a call to the **RoleEnvironment.getConfigurationSettings** method.</span><span class="sxs-lookup"><span data-stu-id="c06bb-130">In an application running within a role in Azure, you can store this string in the service configuration file, *ServiceConfiguration.cscfg*, and you can access it with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="c06bb-131">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span><span class="sxs-lookup"><span data-stu-id="c06bb-131">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="c06bb-132">You can also store your connection string in your project's config.properties file:</span><span class="sxs-lookup"><span data-stu-id="c06bb-132">You can also store your connection string in your project's config.properties file:</span></span>

```java
StorageConnectionString = DefaultEndpointsProtocol=https;AccountName=your_account;AccountKey=your_account_key;TableEndpoint=https://your_table_endpoint/
```

<span data-ttu-id="c06bb-133">The following samples assume that you have used one of these methods to get the storage connection string.</span><span class="sxs-lookup"><span data-stu-id="c06bb-133">The following samples assume that you have used one of these methods to get the storage connection string.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c06bb-134">Create a table</span><span class="sxs-lookup"><span data-stu-id="c06bb-134">Create a table</span></span>
<span data-ttu-id="c06bb-135">A **CloudTableClient** object lets you get reference objects for tables and entities.</span><span class="sxs-lookup"><span data-stu-id="c06bb-135">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="c06bb-136">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span><span class="sxs-lookup"><span data-stu-id="c06bb-136">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> 

> [!NOTE]
> <span data-ttu-id="c06bb-137">There are other ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference]).</span><span class="sxs-lookup"><span data-stu-id="c06bb-137">There are other ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference]).</span></span>
>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-tables"></a><span data-ttu-id="c06bb-138">List the tables</span><span class="sxs-lookup"><span data-stu-id="c06bb-138">List the tables</span></span>
<span data-ttu-id="c06bb-139">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span><span class="sxs-lookup"><span data-stu-id="c06bb-139">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="c06bb-140">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="c06bb-140">Add an entity to a table</span></span>
<span data-ttu-id="c06bb-141">Entities map to Java objects using a custom class implementing **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c06bb-141">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="c06bb-142">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span><span class="sxs-lookup"><span data-stu-id="c06bb-142">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="c06bb-143">To add an entity to a table, first create a class that defines the properties of your entity.</span><span class="sxs-lookup"><span data-stu-id="c06bb-143">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="c06bb-144">The following code defines an entity class that uses the customer's first name as the row key, and last name as the partition key.</span><span class="sxs-lookup"><span data-stu-id="c06bb-144">The following code defines an entity class that uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="c06bb-145">Together, an entity's partition and row key uniquely identify the entity in the table.</span><span class="sxs-lookup"><span data-stu-id="c06bb-145">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="c06bb-146">Entities with the same partition key can be queried faster than those with different partition keys.</span><span class="sxs-lookup"><span data-stu-id="c06bb-146">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="c06bb-147">Table operations involving entities require a **TableOperation** object.</span><span class="sxs-lookup"><span data-stu-id="c06bb-147">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="c06bb-148">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span><span class="sxs-lookup"><span data-stu-id="c06bb-148">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="c06bb-149">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span><span class="sxs-lookup"><span data-stu-id="c06bb-149">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="c06bb-150">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span><span class="sxs-lookup"><span data-stu-id="c06bb-150">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="c06bb-151">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span><span class="sxs-lookup"><span data-stu-id="c06bb-151">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="c06bb-152">Insert a batch of entities</span><span class="sxs-lookup"><span data-stu-id="c06bb-152">Insert a batch of entities</span></span>
<span data-ttu-id="c06bb-153">You can insert a batch of entities to the table service in one write operation.</span><span class="sxs-lookup"><span data-stu-id="c06bb-153">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="c06bb-154">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span><span class="sxs-lookup"><span data-stu-id="c06bb-154">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="c06bb-155">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span><span class="sxs-lookup"><span data-stu-id="c06bb-155">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="c06bb-156">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span><span class="sxs-lookup"><span data-stu-id="c06bb-156">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="c06bb-157">Some things to note on batch operations:</span><span class="sxs-lookup"><span data-stu-id="c06bb-157">Some things to note on batch operations:</span></span>

* <span data-ttu-id="c06bb-158">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span><span class="sxs-lookup"><span data-stu-id="c06bb-158">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="c06bb-159">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span><span class="sxs-lookup"><span data-stu-id="c06bb-159">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="c06bb-160">All entities in a single batch operation must have the same partition key.</span><span class="sxs-lookup"><span data-stu-id="c06bb-160">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="c06bb-161">A batch operation is limited to a 4MB data payload.</span><span class="sxs-lookup"><span data-stu-id="c06bb-161">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="c06bb-162">Retrieve all entities in a partition</span><span class="sxs-lookup"><span data-stu-id="c06bb-162">Retrieve all entities in a partition</span></span>
<span data-ttu-id="c06bb-163">To query a table for entities in a partition, you can use a **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="c06bb-163">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="c06bb-164">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span><span class="sxs-lookup"><span data-stu-id="c06bb-164">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="c06bb-165">The following code specifies a filter for entities where 'Smith' is the partition key.</span><span class="sxs-lookup"><span data-stu-id="c06bb-165">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="c06bb-166">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span><span class="sxs-lookup"><span data-stu-id="c06bb-166">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="c06bb-167">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span><span class="sxs-lookup"><span data-stu-id="c06bb-167">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="c06bb-168">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span><span class="sxs-lookup"><span data-stu-id="c06bb-168">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="c06bb-169">You can then use the **Iterator** returned in a for each loop to consume the results.</span><span class="sxs-lookup"><span data-stu-id="c06bb-169">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="c06bb-170">This code prints the fields of each entity in the query results to the console.</span><span class="sxs-lookup"><span data-stu-id="c06bb-170">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="c06bb-171">Retrieve a range of entities in a partition</span><span class="sxs-lookup"><span data-stu-id="c06bb-171">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="c06bb-172">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span><span class="sxs-lookup"><span data-stu-id="c06bb-172">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="c06bb-173">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span><span class="sxs-lookup"><span data-stu-id="c06bb-173">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="c06bb-174">Then it prints the query results.</span><span class="sxs-lookup"><span data-stu-id="c06bb-174">Then it prints the query results.</span></span> <span data-ttu-id="c06bb-175">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span><span class="sxs-lookup"><span data-stu-id="c06bb-175">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="c06bb-176">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="c06bb-176">Retrieve a single entity</span></span>
<span data-ttu-id="c06bb-177">You can write a query to retrieve a single, specific entity.</span><span class="sxs-lookup"><span data-stu-id="c06bb-177">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="c06bb-178">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span><span class="sxs-lookup"><span data-stu-id="c06bb-178">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="c06bb-179">When executed, the retrieve operation returns just one entity, rather than a collection.</span><span class="sxs-lookup"><span data-stu-id="c06bb-179">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="c06bb-180">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="c06bb-180">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="c06bb-181">If this type is not compatible with the type specified for the query, an exception is thrown.</span><span class="sxs-lookup"><span data-stu-id="c06bb-181">If this type is not compatible with the type specified for the query, an exception is thrown.</span></span> <span data-ttu-id="c06bb-182">A null value is returned if no entity has an exact partition and row key match.</span><span class="sxs-lookup"><span data-stu-id="c06bb-182">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="c06bb-183">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span><span class="sxs-lookup"><span data-stu-id="c06bb-183">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="modify-an-entity"></a><span data-ttu-id="c06bb-184">Modify an entity</span><span class="sxs-lookup"><span data-stu-id="c06bb-184">Modify an entity</span></span>
<span data-ttu-id="c06bb-185">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span><span class="sxs-lookup"><span data-stu-id="c06bb-185">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="c06bb-186">The following code changes an existing customer's phone number.</span><span class="sxs-lookup"><span data-stu-id="c06bb-186">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="c06bb-187">Instead of calling **TableOperation.insert** as we did to insert, this code calls **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="c06bb-187">Instead of calling **TableOperation.insert** as we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="c06bb-188">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span><span class="sxs-lookup"><span data-stu-id="c06bb-188">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="c06bb-189">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span><span class="sxs-lookup"><span data-stu-id="c06bb-189">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="c06bb-190">This optimistic concurrency retry pattern is common in a distributed storage system.</span><span class="sxs-lookup"><span data-stu-id="c06bb-190">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c06bb-191">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="c06bb-191">Query a subset of entity properties</span></span>
<span data-ttu-id="c06bb-192">A query to a table can retrieve just a few properties from an entity.</span><span class="sxs-lookup"><span data-stu-id="c06bb-192">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="c06bb-193">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="c06bb-193">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c06bb-194">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span><span class="sxs-lookup"><span data-stu-id="c06bb-194">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="c06bb-195">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span><span class="sxs-lookup"><span data-stu-id="c06bb-195">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="c06bb-196">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="c06bb-196">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="c06bb-197">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span><span class="sxs-lookup"><span data-stu-id="c06bb-197">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="c06bb-198">Insert or Replace an entity</span><span class="sxs-lookup"><span data-stu-id="c06bb-198">Insert or Replace an entity</span></span>
<span data-ttu-id="c06bb-199">Often you want to add an entity to a table without knowing if it already exists in the table.</span><span class="sxs-lookup"><span data-stu-id="c06bb-199">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="c06bb-200">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span><span class="sxs-lookup"><span data-stu-id="c06bb-200">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="c06bb-201">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="c06bb-201">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="c06bb-202">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span><span class="sxs-lookup"><span data-stu-id="c06bb-202">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="c06bb-203">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span><span class="sxs-lookup"><span data-stu-id="c06bb-203">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="c06bb-204">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span><span class="sxs-lookup"><span data-stu-id="c06bb-204">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="c06bb-205">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span><span class="sxs-lookup"><span data-stu-id="c06bb-205">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="c06bb-206">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="c06bb-206">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="c06bb-207">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="c06bb-207">Delete an entity</span></span>
<span data-ttu-id="c06bb-208">You can easily delete an entity after you have retrieved it.</span><span class="sxs-lookup"><span data-stu-id="c06bb-208">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="c06bb-209">After the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span><span class="sxs-lookup"><span data-stu-id="c06bb-209">After the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="c06bb-210">Then call **execute** on the **CloudTable** object.</span><span class="sxs-lookup"><span data-stu-id="c06bb-210">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="c06bb-211">The following code retrieves and deletes a customer entity.</span><span class="sxs-lookup"><span data-stu-id="c06bb-211">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-table"></a><span data-ttu-id="c06bb-212">Delete a table</span><span class="sxs-lookup"><span data-stu-id="c06bb-212">Delete a table</span></span>
<span data-ttu-id="c06bb-213">Finally, the following code deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="c06bb-213">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="c06bb-214">For about 40 seconds after you delete a table, you cannot recreate it.</span><span class="sxs-lookup"><span data-stu-id="c06bb-214">For about 40 seconds after you delete a table, you cannot recreate it.</span></span> 

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="c06bb-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="c06bb-215">Next steps</span></span>

* [<span data-ttu-id="c06bb-216">Getting Started with Azure Table Service in Java</span><span class="sxs-lookup"><span data-stu-id="c06bb-216">Getting Started with Azure Table Service in Java</span></span>](https://github.com/Azure-Samples/storage-table-java-getting-started)
* <span data-ttu-id="c06bb-217">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="c06bb-217">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c06bb-218">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="c06bb-218">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="c06bb-219">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span><span class="sxs-lookup"><span data-stu-id="c06bb-219">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="c06bb-220">[Azure Storage REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="c06bb-220">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="c06bb-221">[Azure Storage Team Blog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="c06bb-221">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="c06bb-222">For more information, visit [Azure for Java developers](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="c06bb-222">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK Reference]: http://azure.github.io/azure-storage-java/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
