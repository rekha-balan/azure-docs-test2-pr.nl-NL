---
title: How to get started with table storage and Visual Studio connected services (ASP.NET Core) | Microsoft Docs
description: How to get started with Azure Table storage in an ASP.NET Core project in Visual Studio after connecting to a storage account using Visual Studio connected services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: b64d4f7e55977c7ce144987f7600e5ddcb25596c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563886"
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="de2bc-103">How to get started with Azure Table storage and Visual Studio connected services</span><span class="sxs-lookup"><span data-stu-id="de2bc-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="de2bc-104">Overview</span><span class="sxs-lookup"><span data-stu-id="de2bc-104">Overview</span></span>
<span data-ttu-id="de2bc-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span><span class="sxs-lookup"><span data-stu-id="de2bc-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="de2bc-106">The Azure Table storage service enables you to store large amounts of structured data.</span><span class="sxs-lookup"><span data-stu-id="de2bc-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="de2bc-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="de2bc-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="de2bc-108">Azure tables are ideal for storing structured, non-relational data.</span><span class="sxs-lookup"><span data-stu-id="de2bc-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="de2bc-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span><span class="sxs-lookup"><span data-stu-id="de2bc-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="de2bc-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="de2bc-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="de2bc-111">To get started, you first need to create a table in your storage account.</span><span class="sxs-lookup"><span data-stu-id="de2bc-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="de2bc-112">We'll show you how to create an Azure table in code.</span><span class="sxs-lookup"><span data-stu-id="de2bc-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="de2bc-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span><span class="sxs-lookup"><span data-stu-id="de2bc-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="de2bc-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span><span class="sxs-lookup"><span data-stu-id="de2bc-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="de2bc-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="de2bc-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="de2bc-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="de2bc-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="de2bc-117">The code below assumes Async programming methods are being used.</span><span class="sxs-lookup"><span data-stu-id="de2bc-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="de2bc-118">Access tables in code</span><span class="sxs-lookup"><span data-stu-id="de2bc-118">Access tables in code</span></span>
<span data-ttu-id="de2bc-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span><span class="sxs-lookup"><span data-stu-id="de2bc-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="de2bc-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span><span class="sxs-lookup"><span data-stu-id="de2bc-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="de2bc-121">Get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="de2bc-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="de2bc-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span><span class="sxs-lookup"><span data-stu-id="de2bc-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="de2bc-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span><span class="sxs-lookup"><span data-stu-id="de2bc-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="de2bc-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span><span class="sxs-lookup"><span data-stu-id="de2bc-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="de2bc-125">Get a **CloudTable** reference object to reference a specific table and entities.</span><span class="sxs-lookup"><span data-stu-id="de2bc-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="de2bc-126">Create a table in code</span><span class="sxs-lookup"><span data-stu-id="de2bc-126">Create a table in code</span></span>
<span data-ttu-id="de2bc-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="de2bc-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="de2bc-128">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="de2bc-128">Add an entity to a table</span></span>
<span data-ttu-id="de2bc-129">To add an entity to a table you create a class that defines the properties of your entity.</span><span class="sxs-lookup"><span data-stu-id="de2bc-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="de2bc-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span><span class="sxs-lookup"><span data-stu-id="de2bc-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

<span data-ttu-id="de2bc-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span><span class="sxs-lookup"><span data-stu-id="de2bc-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="de2bc-132">The **TableOperation** object represents the operation to be done.</span><span class="sxs-lookup"><span data-stu-id="de2bc-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="de2bc-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="de2bc-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="de2bc-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span><span class="sxs-lookup"><span data-stu-id="de2bc-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="de2bc-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="de2bc-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="de2bc-136">Insert a batch of entities</span><span class="sxs-lookup"><span data-stu-id="de2bc-136">Insert a batch of entities</span></span>
<span data-ttu-id="de2bc-137">You can insert multiple entities into a table in a single write operation.</span><span class="sxs-lookup"><span data-stu-id="de2bc-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="de2bc-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="de2bc-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="de2bc-139">Get all of the entities in a partition</span><span class="sxs-lookup"><span data-stu-id="de2bc-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="de2bc-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span><span class="sxs-lookup"><span data-stu-id="de2bc-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="de2bc-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span><span class="sxs-lookup"><span data-stu-id="de2bc-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="de2bc-142">This example prints the fields of each entity in the query results to the console.</span><span class="sxs-lookup"><span data-stu-id="de2bc-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="de2bc-143">Get a single entity</span><span class="sxs-lookup"><span data-stu-id="de2bc-143">Get a single entity</span></span>
<span data-ttu-id="de2bc-144">You can write a query to get a single, specific entity.</span><span class="sxs-lookup"><span data-stu-id="de2bc-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="de2bc-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="de2bc-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="de2bc-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="de2bc-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="de2bc-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span><span class="sxs-lookup"><span data-stu-id="de2bc-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="de2bc-148">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="de2bc-148">Delete an entity</span></span>
<span data-ttu-id="de2bc-149">You can delete an entity after you find it.</span><span class="sxs-lookup"><span data-stu-id="de2bc-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="de2bc-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span><span class="sxs-lookup"><span data-stu-id="de2bc-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="de2bc-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="de2bc-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

