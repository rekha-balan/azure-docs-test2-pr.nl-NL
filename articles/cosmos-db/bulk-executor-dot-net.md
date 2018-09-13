---
title: Using bulk executor .NET library to perform bulk operations in Azure Cosmos DB | Microsoft Docs
description: Use Azure Cosmos DB’s bulk executor .NET library to bulk import and update documents to Azure Cosmos DB containers.
keywords: .Net bulk executor
services: cosmos-db
author: tknandu
manager: kfile
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: ramkris
ms.openlocfilehash: cc0faa44501ea130309a02bb48d02f9c5b33febd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870621"
---
# <a name="use-bulk-executor-net-library-to-perform-bulk-operations-in-azure-cosmos-db"></a><span data-ttu-id="915c8-104">Use bulk executor .NET library to perform bulk operations in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="915c8-104">Use bulk executor .NET library to perform bulk operations in Azure Cosmos DB</span></span>

<span data-ttu-id="915c8-105">This tutorial provides instructions on using the Azure Cosmos DB’s bulk executor .NET library to import and update documents to Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="915c8-105">This tutorial provides instructions on using the Azure Cosmos DB’s bulk executor .NET library to import and update documents to Azure Cosmos DB container.</span></span> <span data-ttu-id="915c8-106">To learn about bulk executor library and how it helps you leverage massive throughput and storage, see [bulk executor library overview](bulk-executor-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="915c8-106">To learn about bulk executor library and how it helps you leverage massive throughput and storage, see [bulk executor library overview](bulk-executor-overview.md) article.</span></span> <span data-ttu-id="915c8-107">This tutorial will walk you through a sample .NET application that bulk imports randomly generated documents into an Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="915c8-107">This tutorial will walk you through a sample .NET application that bulk imports randomly generated documents into an Azure Cosmos DB container.</span></span> <span data-ttu-id="915c8-108">After importing, it shows you how you can bulk update the imported data by specifying patches as operations to perform on specific document fields.</span><span class="sxs-lookup"><span data-stu-id="915c8-108">After importing, it shows you how you can bulk update the imported data by specifying patches as operations to perform on specific document fields.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="915c8-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="915c8-109">Prerequisites</span></span>

* <span data-ttu-id="915c8-110">If you don’t already have Visual Studio 2017 installed, you can download and use the [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="915c8-110">If you don’t already have Visual Studio 2017 installed, you can download and use the [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="915c8-111">Make sure that you enable Azure development during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="915c8-111">Make sure that you enable Azure development during the Visual Studio setup.</span></span>

* <span data-ttu-id="915c8-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="915c8-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span> 

* <span data-ttu-id="915c8-113">You can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="915c8-113">You can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span> <span data-ttu-id="915c8-114">Or, you can use the [Azure Cosmos DB Emulator](https://docs.microsoft.com/azure/cosmos-db/local-emulator) with  the `https://localhost:8081` URI.</span><span class="sxs-lookup"><span data-stu-id="915c8-114">Or, you can use the [Azure Cosmos DB Emulator](https://docs.microsoft.com/azure/cosmos-db/local-emulator) with  the `https://localhost:8081` URI.</span></span> <span data-ttu-id="915c8-115">The Primary Key is provided in [Authenticating requests](local-emulator.md#authenticating-requests).</span><span class="sxs-lookup"><span data-stu-id="915c8-115">The Primary Key is provided in [Authenticating requests](local-emulator.md#authenticating-requests).</span></span>

* <span data-ttu-id="915c8-116">Create an Azure Cosmos DB SQL API account by using the steps described in [create database account](create-sql-api-dotnet.md#create-a-database-account) section of the .NET quickstart article.</span><span class="sxs-lookup"><span data-stu-id="915c8-116">Create an Azure Cosmos DB SQL API account by using the steps described in [create database account](create-sql-api-dotnet.md#create-a-database-account) section of the .NET quickstart article.</span></span> 

## <a name="clone-the-sample-application"></a><span data-ttu-id="915c8-117">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="915c8-117">Clone the sample application</span></span>

<span data-ttu-id="915c8-118">Now let's switch to working with code by downloading some sample .NET applications from GitHub.</span><span class="sxs-lookup"><span data-stu-id="915c8-118">Now let's switch to working with code by downloading some sample .NET applications from GitHub.</span></span> <span data-ttu-id="915c8-119">These applications perform bulk operations on Azure Cosmos DB data.</span><span class="sxs-lookup"><span data-stu-id="915c8-119">These applications perform bulk operations on Azure Cosmos DB data.</span></span> <span data-ttu-id="915c8-120">To clone the applications, open a command prompt, navigate to the directory where you want to copy the them and run the following command:</span><span class="sxs-lookup"><span data-stu-id="915c8-120">To clone the applications, open a command prompt, navigate to the directory where you want to copy the them and run the following command:</span></span>

```
git clone https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started.git
```

<span data-ttu-id="915c8-121">The cloned repository contains two samples "BulkImportSample" and "BulkUpdateSample."</span><span class="sxs-lookup"><span data-stu-id="915c8-121">The cloned repository contains two samples "BulkImportSample" and "BulkUpdateSample."</span></span> <span data-ttu-id="915c8-122">You can open either of the sample applications, update the connection strings in App.config file with your Azure Cosmos DB account’s connection strings, build the solution, and run it.</span><span class="sxs-lookup"><span data-stu-id="915c8-122">You can open either of the sample applications, update the connection strings in App.config file with your Azure Cosmos DB account’s connection strings, build the solution, and run it.</span></span> 

<span data-ttu-id="915c8-123">The "BulkImportSample" application generates random documents and bulk imports them to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="915c8-123">The "BulkImportSample" application generates random documents and bulk imports them to Azure Cosmos DB.</span></span> <span data-ttu-id="915c8-124">The "BulkUpdateSample" application bulk updates the imported documents by specifying patches as operations to perform on specific document fields.</span><span class="sxs-lookup"><span data-stu-id="915c8-124">The "BulkUpdateSample" application bulk updates the imported documents by specifying patches as operations to perform on specific document fields.</span></span> <span data-ttu-id="915c8-125">In the next sections, you will review the code in each of these sample apps.</span><span class="sxs-lookup"><span data-stu-id="915c8-125">In the next sections, you will review the code in each of these sample apps.</span></span>

## <a name="bulk-import-data-to-azure-cosmos-db"></a><span data-ttu-id="915c8-126">Bulk import data to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="915c8-126">Bulk import data to Azure Cosmos DB</span></span>

1. <span data-ttu-id="915c8-127">Navigate to the "BulkImportSample" folder and open the "BulkImportSample.sln" file.</span><span class="sxs-lookup"><span data-stu-id="915c8-127">Navigate to the "BulkImportSample" folder and open the "BulkImportSample.sln" file.</span></span>  

2. <span data-ttu-id="915c8-128">The Azure Cosmos DB’s connection strings are retrieved from the App.config file as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="915c8-128">The Azure Cosmos DB’s connection strings are retrieved from the App.config file as shown in the following code:</span></span>  

   ```csharp
   private static readonly string EndpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
   private static readonly string AuthorizationKey = ConfigurationManager.AppSettings["AuthorizationKey"];
   private static readonly string DatabaseName = ConfigurationManager.AppSettings["DatabaseName"];
   private static readonly string CollectionName = ConfigurationManager.AppSettings["CollectionName"];
   private static readonly int CollectionThroughput = int.Parse(ConfigurationManager.AppSettings["CollectionThroughput"]);
   ```

   <span data-ttu-id="915c8-129">The bulk importer creates a new database and a collection with the database name, collection name, and throughput values specified in the App.config file.</span><span class="sxs-lookup"><span data-stu-id="915c8-129">The bulk importer creates a new database and a collection with the database name, collection name, and throughput values specified in the App.config file.</span></span> 

3. <span data-ttu-id="915c8-130">Next the DocumentClient object is initialized with Direct TCP connection mode:</span><span class="sxs-lookup"><span data-stu-id="915c8-130">Next the DocumentClient object is initialized with Direct TCP connection mode:</span></span>  

   ```csharp
   ConnectionPolicy connectionPolicy = new ConnectionPolicy
   {
      ConnectionMode = ConnectionMode.Direct,
      ConnectionProtocol = Protocol.Tcp
   };
   DocumentClient client = new DocumentClient(new Uri(endpointUrl),authorizationKey,
   connectionPolicy)
   ```

4. <span data-ttu-id="915c8-131">The BulkExecutor object is initialized with a high retry values for wait time and throttled requests.</span><span class="sxs-lookup"><span data-stu-id="915c8-131">The BulkExecutor object is initialized with a high retry values for wait time and throttled requests.</span></span> <span data-ttu-id="915c8-132">And then they are set to 0 to pass congestion control to BulkExecutor for its lifetime.</span><span class="sxs-lookup"><span data-stu-id="915c8-132">And then they are set to 0 to pass congestion control to BulkExecutor for its lifetime.</span></span>  

   ```csharp
   // Set retry options high during initialization (default values).
   client.ConnectionPolicy.RetryOptions.MaxRetryWaitTimeInSeconds = 30;
   client.ConnectionPolicy.RetryOptions.MaxRetryAttemptsOnThrottledRequests = 9;

   IBulkExecutor bulkExecutor = new BulkExecutor(client, dataCollection);
   await bulkExecutor.InitializeAsync();

   // Set retries to 0 to pass complete control to bulk executor.
   client.ConnectionPolicy.RetryOptions.MaxRetryWaitTimeInSeconds = 0;
   client.ConnectionPolicy.RetryOptions.MaxRetryAttemptsOnThrottledRequests = 0;
   ```

5. <span data-ttu-id="915c8-133">The application invokes the BulkImportAsync API.</span><span class="sxs-lookup"><span data-stu-id="915c8-133">The application invokes the BulkImportAsync API.</span></span> <span data-ttu-id="915c8-134">The .NET library provides two overloads of the bulk import API - one that accepts a list of serialized JSON documents and the other accepts a list of deserialized POCO documents.</span><span class="sxs-lookup"><span data-stu-id="915c8-134">The .NET library provides two overloads of the bulk import API - one that accepts a list of serialized JSON documents and the other accepts a list of deserialized POCO documents.</span></span> <span data-ttu-id="915c8-135">To learn about the definitions of each of these overloaded methods, refer to [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.bulkexecutor.bulkimportasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="915c8-135">To learn about the definitions of each of these overloaded methods, refer to [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.bulkexecutor.bulkimportasync?view=azure-dotnet).</span></span>

   ```csharp
   BulkImportResponse bulkImportResponse = await bulkExecutor.BulkImportAsync(
     documents: documentsToImportInBatch,
     enableUpsert: true,
     disableAutomaticIdGeneration: true,
     maxConcurrencyPerPartitionKeyRange: null,
     maxInMemorySortingBatchSize: null,
     cancellationToken: token);
   ```
   <span data-ttu-id="915c8-136">**BulkImportAsync method accepts the following parameters:**</span><span class="sxs-lookup"><span data-stu-id="915c8-136">**BulkImportAsync method accepts the following parameters:**</span></span>
   
   |<span data-ttu-id="915c8-137">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="915c8-137">**Parameter**</span></span>  |<span data-ttu-id="915c8-138">**Description**</span><span class="sxs-lookup"><span data-stu-id="915c8-138">**Description**</span></span> |
   |---------|---------|
   |<span data-ttu-id="915c8-139">enableUpsert</span><span class="sxs-lookup"><span data-stu-id="915c8-139">enableUpsert</span></span>    |   <span data-ttu-id="915c8-140">A flag to enable upsert of the documents.</span><span class="sxs-lookup"><span data-stu-id="915c8-140">A flag to enable upsert of the documents.</span></span> <span data-ttu-id="915c8-141">If a document with given id already exists, it's updated.</span><span class="sxs-lookup"><span data-stu-id="915c8-141">If a document with given id already exists, it's updated.</span></span> <span data-ttu-id="915c8-142">By default, it is set to false.</span><span class="sxs-lookup"><span data-stu-id="915c8-142">By default, it is set to false.</span></span>      |
   |<span data-ttu-id="915c8-143">disableAutomaticIdGeneration</span><span class="sxs-lookup"><span data-stu-id="915c8-143">disableAutomaticIdGeneration</span></span>    |    <span data-ttu-id="915c8-144">A flag to disable automatic generation of ID.</span><span class="sxs-lookup"><span data-stu-id="915c8-144">A flag to disable automatic generation of ID.</span></span> <span data-ttu-id="915c8-145">By default, it is set to true.</span><span class="sxs-lookup"><span data-stu-id="915c8-145">By default, it is set to true.</span></span>     |
   |<span data-ttu-id="915c8-146">maxConcurrencyPerPartitionKeyRange</span><span class="sxs-lookup"><span data-stu-id="915c8-146">maxConcurrencyPerPartitionKeyRange</span></span>    | <span data-ttu-id="915c8-147">The maximum degree of concurrency per partition key range, setting to null will cause library to use a default value of 20.</span><span class="sxs-lookup"><span data-stu-id="915c8-147">The maximum degree of concurrency per partition key range, setting to null will cause library to use a default value of 20.</span></span> |
   |<span data-ttu-id="915c8-148">maxInMemorySortingBatchSize</span><span class="sxs-lookup"><span data-stu-id="915c8-148">maxInMemorySortingBatchSize</span></span>     |  <span data-ttu-id="915c8-149">The maximum number of documents pulled from the document enumerator that is passed to the API call in each stage.</span><span class="sxs-lookup"><span data-stu-id="915c8-149">The maximum number of documents pulled from the document enumerator that is passed to the API call in each stage.</span></span>  <span data-ttu-id="915c8-150">For in-memory pre-processing sorting phase prior to bulk importing, setting to null will cause library to use default value of min(documents.count, 1000000).</span><span class="sxs-lookup"><span data-stu-id="915c8-150">For in-memory pre-processing sorting phase prior to bulk importing, setting to null will cause library to use default value of min(documents.count, 1000000).</span></span>       |
   |<span data-ttu-id="915c8-151">cancellationToken</span><span class="sxs-lookup"><span data-stu-id="915c8-151">cancellationToken</span></span>    |    <span data-ttu-id="915c8-152">The cancellation token to gracefully exit bulk import.</span><span class="sxs-lookup"><span data-stu-id="915c8-152">The cancellation token to gracefully exit bulk import.</span></span>     |

   <span data-ttu-id="915c8-153">**Bulk import response object definition** The result of the bulk import API call contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="915c8-153">**Bulk import response object definition** The result of the bulk import API call contains the following attributes:</span></span>

   |<span data-ttu-id="915c8-154">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="915c8-154">**Parameter**</span></span>  |<span data-ttu-id="915c8-155">**Description**</span><span class="sxs-lookup"><span data-stu-id="915c8-155">**Description**</span></span>  |
   |---------|---------|
   |<span data-ttu-id="915c8-156">NumberOfDocumentsImported (long)</span><span class="sxs-lookup"><span data-stu-id="915c8-156">NumberOfDocumentsImported (long)</span></span>   |  <span data-ttu-id="915c8-157">The total number of documents that were successfully imported out of the documents supplied to the bulk import API call.</span><span class="sxs-lookup"><span data-stu-id="915c8-157">The total number of documents that were successfully imported out of the documents supplied to the bulk import API call.</span></span>       |
   |<span data-ttu-id="915c8-158">TotalRequestUnitsConsumed (double)</span><span class="sxs-lookup"><span data-stu-id="915c8-158">TotalRequestUnitsConsumed (double)</span></span>   |   <span data-ttu-id="915c8-159">The total request units (RU) consumed by the bulk import API call.</span><span class="sxs-lookup"><span data-stu-id="915c8-159">The total request units (RU) consumed by the bulk import API call.</span></span>      |
   |<span data-ttu-id="915c8-160">TotalTimeTaken (TimeSpan)</span><span class="sxs-lookup"><span data-stu-id="915c8-160">TotalTimeTaken (TimeSpan)</span></span>    |   <span data-ttu-id="915c8-161">The total time taken by the bulk import API call to complete execution.</span><span class="sxs-lookup"><span data-stu-id="915c8-161">The total time taken by the bulk import API call to complete execution.</span></span>      |
   |<span data-ttu-id="915c8-162">BadInputDocuments (List<object>)</span><span class="sxs-lookup"><span data-stu-id="915c8-162">BadInputDocuments (List<object>)</span></span>   |     <span data-ttu-id="915c8-163">The list of bad-format documents that were not successfully imported in the bulk import API call.</span><span class="sxs-lookup"><span data-stu-id="915c8-163">The list of bad-format documents that were not successfully imported in the bulk import API call.</span></span> <span data-ttu-id="915c8-164">User should fix the documents returned and retry import.</span><span class="sxs-lookup"><span data-stu-id="915c8-164">User should fix the documents returned and retry import.</span></span> <span data-ttu-id="915c8-165">Bad-formatted documents include documents whose ID value is not a string (null or any other datatype is considered invalid).</span><span class="sxs-lookup"><span data-stu-id="915c8-165">Bad-formatted documents include documents whose ID value is not a string (null or any other datatype is considered invalid).</span></span>    |

## <a name="bulk-update-data-in-azure-cosmos-db"></a><span data-ttu-id="915c8-166">Bulk update data in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="915c8-166">Bulk update data in Azure Cosmos DB</span></span>

<span data-ttu-id="915c8-167">You can update existing documents by using the BulkUpdateAsync API.</span><span class="sxs-lookup"><span data-stu-id="915c8-167">You can update existing documents by using the BulkUpdateAsync API.</span></span> <span data-ttu-id="915c8-168">In this example, you will set the Name field to a new value and remove the Description field from the existing documents.</span><span class="sxs-lookup"><span data-stu-id="915c8-168">In this example, you will set the Name field to a new value and remove the Description field from the existing documents.</span></span> <span data-ttu-id="915c8-169">For the full set of supported field update operations, refer to [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.bulkupdate?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="915c8-169">For the full set of supported field update operations, refer to [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.bulkupdate?view=azure-dotnet).</span></span> 

1. <span data-ttu-id="915c8-170">Navigate to the "BulkUpdateSample" folder and open the "BulkUpdateSample.sln" file.</span><span class="sxs-lookup"><span data-stu-id="915c8-170">Navigate to the "BulkUpdateSample" folder and open the "BulkUpdateSample.sln" file.</span></span>  

2. <span data-ttu-id="915c8-171">Define the update items along with corresponding field update operations.</span><span class="sxs-lookup"><span data-stu-id="915c8-171">Define the update items along with corresponding field update operations.</span></span> <span data-ttu-id="915c8-172">In this example, you will use SetUpdateOperation to update the Name field and UnsetUpdateOperation to remove the Description field from all the documents.</span><span class="sxs-lookup"><span data-stu-id="915c8-172">In this example, you will use SetUpdateOperation to update the Name field and UnsetUpdateOperation to remove the Description field from all the documents.</span></span> <span data-ttu-id="915c8-173">You can also perform other operations like increment a document field by a specific value, push specific values into an array field, or remove a specific value from an array field.</span><span class="sxs-lookup"><span data-stu-id="915c8-173">You can also perform other operations like increment a document field by a specific value, push specific values into an array field, or remove a specific value from an array field.</span></span> <span data-ttu-id="915c8-174">To learn about different methods provided by the bulk update API, refer to the [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.bulkupdate?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="915c8-174">To learn about different methods provided by the bulk update API, refer to the [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.bulkupdate?view=azure-dotnet).</span></span>

   ```csharp
   SetUpdateOperation<string> nameUpdate = new SetUpdateOperation<string>("Name", "UpdatedDoc");
   UnsetUpdateOperation descriptionUpdate = new UnsetUpdateOperation("description");

   List<UpdateOperation> updateOperations = new List<UpdateOperation>();
   updateOperations.Add(nameUpdate);
   updateOperations.Add(descriptionUpdate);

   List<UpdateItem> updateItems = new List<UpdateItem>();
   for (int i = 0; i < 10; i++)
   {
    updateItems.Add(new UpdateItem(i.ToString(), i.ToString(), updateOperations));
   }
   ```

3. <span data-ttu-id="915c8-175">The application invokes the BulkUpdateAsync API.</span><span class="sxs-lookup"><span data-stu-id="915c8-175">The application invokes the BulkUpdateAsync API.</span></span> <span data-ttu-id="915c8-176">To learn about the definition of the BulkUpdateAsync method, refer to [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.ibulkexecutor.bulkupdateasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="915c8-176">To learn about the definition of the BulkUpdateAsync method, refer to [API documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.bulkexecutor.ibulkexecutor.bulkupdateasync?view=azure-dotnet).</span></span>  

   ```csharp
   BulkUpdateResponse bulkUpdateResponse = await bulkExecutor.BulkUpdateAsync(
     updateItems: updateItems,
     maxConcurrencyPerPartitionKeyRange: null,
     maxInMemorySortingBatchSize: null,
     cancellationToken: token);
   ```  
   <span data-ttu-id="915c8-177">**BulkUpdateAsync method accepts the following parameters:**</span><span class="sxs-lookup"><span data-stu-id="915c8-177">**BulkUpdateAsync method accepts the following parameters:**</span></span>

   |<span data-ttu-id="915c8-178">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="915c8-178">**Parameter**</span></span>  |<span data-ttu-id="915c8-179">**Description**</span><span class="sxs-lookup"><span data-stu-id="915c8-179">**Description**</span></span> |
   |---------|---------|
   |<span data-ttu-id="915c8-180">maxConcurrencyPerPartitionKeyRange</span><span class="sxs-lookup"><span data-stu-id="915c8-180">maxConcurrencyPerPartitionKeyRange</span></span>    |   <span data-ttu-id="915c8-181">The maximum degree of concurrency per partition key range, setting to null will cause library to use default value of 20.</span><span class="sxs-lookup"><span data-stu-id="915c8-181">The maximum degree of concurrency per partition key range, setting to null will cause library to use default value of 20.</span></span>   |
   |<span data-ttu-id="915c8-182">maxInMemorySortingBatchSize</span><span class="sxs-lookup"><span data-stu-id="915c8-182">maxInMemorySortingBatchSize</span></span>    |    <span data-ttu-id="915c8-183">The maximum number of update items pulled from the update items enumerator passed to the API call in each stage for in-memory pre-processing sorting phase prior to bulk updating, setting to null will cause library to use default value of min(updateItems.count, 1000000).</span><span class="sxs-lookup"><span data-stu-id="915c8-183">The maximum number of update items pulled from the update items enumerator passed to the API call in each stage for in-memory pre-processing sorting phase prior to bulk updating, setting to null will cause library to use default value of min(updateItems.count, 1000000).</span></span>     |
   | <span data-ttu-id="915c8-184">cancellationToken</span><span class="sxs-lookup"><span data-stu-id="915c8-184">cancellationToken</span></span>|<span data-ttu-id="915c8-185">The cancellation token to gracefully exit bulk update.</span><span class="sxs-lookup"><span data-stu-id="915c8-185">The cancellation token to gracefully exit bulk update.</span></span> |

   <span data-ttu-id="915c8-186">**Bulk update response object definition** The result of the bulk update API call contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="915c8-186">**Bulk update response object definition** The result of the bulk update API call contains the following attributes:</span></span>

   |<span data-ttu-id="915c8-187">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="915c8-187">**Parameter**</span></span>  |<span data-ttu-id="915c8-188">**Description**</span><span class="sxs-lookup"><span data-stu-id="915c8-188">**Description**</span></span> |
   |---------|---------|
   |<span data-ttu-id="915c8-189">NumberOfDocumentsUpdated (long)</span><span class="sxs-lookup"><span data-stu-id="915c8-189">NumberOfDocumentsUpdated (long)</span></span>    |   <span data-ttu-id="915c8-190">The total number of documents that were successfully updated out of the ones supplied to the bulk update API call.</span><span class="sxs-lookup"><span data-stu-id="915c8-190">The total number of documents that were successfully updated out of the ones supplied to the bulk update API call.</span></span>      |
   |<span data-ttu-id="915c8-191">TotalRequestUnitsConsumed (double)</span><span class="sxs-lookup"><span data-stu-id="915c8-191">TotalRequestUnitsConsumed (double)</span></span>   |    <span data-ttu-id="915c8-192">The total request units (RU) consumed by the bulk update API call.</span><span class="sxs-lookup"><span data-stu-id="915c8-192">The total request units (RU) consumed by the bulk update API call.</span></span>    |
   |<span data-ttu-id="915c8-193">TotalTimeTaken (TimeSpan)</span><span class="sxs-lookup"><span data-stu-id="915c8-193">TotalTimeTaken (TimeSpan)</span></span>   | <span data-ttu-id="915c8-194">The total time taken by the bulk update API call to complete execution.</span><span class="sxs-lookup"><span data-stu-id="915c8-194">The total time taken by the bulk update API call to complete execution.</span></span> |
    
## <a name="performance-tips"></a><span data-ttu-id="915c8-195">Performance tips</span><span class="sxs-lookup"><span data-stu-id="915c8-195">Performance tips</span></span> 

<span data-ttu-id="915c8-196">Consider the following points for better performance when using bulk executor library:</span><span class="sxs-lookup"><span data-stu-id="915c8-196">Consider the following points for better performance when using bulk executor library:</span></span>

* <span data-ttu-id="915c8-197">For best performance, run your application from an Azure virtual machine that is in the same region as your Cosmos DB account write region.</span><span class="sxs-lookup"><span data-stu-id="915c8-197">For best performance, run your application from an Azure virtual machine that is in the same region as your Cosmos DB account write region.</span></span>  

* <span data-ttu-id="915c8-198">It is recommended to instantiate a single BulkExecutor object for the whole application within a single virtual machine corresponding to a specific Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="915c8-198">It is recommended to instantiate a single BulkExecutor object for the whole application within a single virtual machine corresponding to a specific Cosmos DB container.</span></span>  

* <span data-ttu-id="915c8-199">Since a single bulk operation API execution consumes a large chunk of the client machine's CPU and network IO.</span><span class="sxs-lookup"><span data-stu-id="915c8-199">Since a single bulk operation API execution consumes a large chunk of the client machine's CPU and network IO.</span></span> <span data-ttu-id="915c8-200">This happens by spawning multiple tasks internally, avoid spawning multiple concurrent tasks within your application process each executing bulk operation API calls.</span><span class="sxs-lookup"><span data-stu-id="915c8-200">This happens by spawning multiple tasks internally, avoid spawning multiple concurrent tasks within your application process each executing bulk operation API calls.</span></span> <span data-ttu-id="915c8-201">If a single bulk operation API call running on a single virtual machine is unable to consume your entire container's throughput (if your container's throughput > 1 million RU/s), it's preferable to create separate virtual machines to concurrently execute bulk operation API calls.</span><span class="sxs-lookup"><span data-stu-id="915c8-201">If a single bulk operation API call running on a single virtual machine is unable to consume your entire container's throughput (if your container's throughput > 1 million RU/s), it's preferable to create separate virtual machines to concurrently execute bulk operation API calls.</span></span>  

* <span data-ttu-id="915c8-202">Ensure InitializeAsync() is invoked after instantiating a BulkExecutor object to fetch the target Cosmos DB container partition map.</span><span class="sxs-lookup"><span data-stu-id="915c8-202">Ensure InitializeAsync() is invoked after instantiating a BulkExecutor object to fetch the target Cosmos DB container partition map.</span></span>  

* <span data-ttu-id="915c8-203">In your application's App.Config, ensure **gcServer** is enabled for better performance</span><span class="sxs-lookup"><span data-stu-id="915c8-203">In your application's App.Config, ensure **gcServer** is enabled for better performance</span></span>
  ```xml  
  <runtime>
    <gcServer enabled="true" />
  </runtime>
  ```
* <span data-ttu-id="915c8-204">The library emits traces that can be collected either into a log file or on the console.</span><span class="sxs-lookup"><span data-stu-id="915c8-204">The library emits traces that can be collected either into a log file or on the console.</span></span> <span data-ttu-id="915c8-205">To enable both, add the following to your application's App.Config.</span><span class="sxs-lookup"><span data-stu-id="915c8-205">To enable both, add the following to your application's App.Config.</span></span>

  ```xml
  <system.diagnostics>
    <trace autoflush="false" indentsize="4">
      <listeners>
        <add name="logListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="application.log" />
        <add name="consoleListener" type="System.Diagnostics.ConsoleTraceListener" />
      </listeners>
    </trace>
  </system.diagnostics>
```

## <a name="next-steps"></a><span data-ttu-id="915c8-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="915c8-206">Next steps</span></span>
* <span data-ttu-id="915c8-207">To learn about Nuget package details and release notes of bulk executor .Net library, see[bulk executor SDK details](sql-api-sdk-bulk-executor-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="915c8-207">To learn about Nuget package details and release notes of bulk executor .Net library, see[bulk executor SDK details](sql-api-sdk-bulk-executor-dot-net.md).</span></span> 
