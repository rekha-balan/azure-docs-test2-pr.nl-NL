---
title: Using bulk executor Java library to perform bulk operations in Azure Cosmos DB | Microsoft Docs
description: Use Azure Cosmos DB’s bulk executor Java library to bulk import and update documents to Azure Cosmos DB containers.
keywords: Java bulk executor
services: cosmos-db
author: tknandu
manager: kfile
ms.service: cosmos-db
ms.devlang: java
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: ramkris
ms.openlocfilehash: 9285b0ea50b7207aa40cea2dcab50f79863ffda9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869761"
---
# <a name="use-bulk-executor-java-library-to-perform-bulk-operations-on-azure-cosmos-db-data"></a><span data-ttu-id="fb03a-104">Use bulk executor Java library to perform bulk operations on Azure Cosmos DB data</span><span class="sxs-lookup"><span data-stu-id="fb03a-104">Use bulk executor Java library to perform bulk operations on Azure Cosmos DB data</span></span>

<span data-ttu-id="fb03a-105">This tutorial provides instructions on using the Azure Cosmos DB’s bulk executor Java library to import, and update Azure Cosmos DB documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-105">This tutorial provides instructions on using the Azure Cosmos DB’s bulk executor Java library to import, and update Azure Cosmos DB documents.</span></span> <span data-ttu-id="fb03a-106">To learn about bulk executor library and how it helps you leverage massive throughput and storage, see [bulk executor Library overview](bulk-executor-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="fb03a-106">To learn about bulk executor library and how it helps you leverage massive throughput and storage, see [bulk executor Library overview](bulk-executor-overview.md) article.</span></span> <span data-ttu-id="fb03a-107">In this tutorial, you build a Java application that generates random documents and they are bulk imported into an Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="fb03a-107">In this tutorial, you build a Java application that generates random documents and they are bulk imported into an Azure Cosmos DB container.</span></span> <span data-ttu-id="fb03a-108">After importing, you will bulk update some properties of a document.</span><span class="sxs-lookup"><span data-stu-id="fb03a-108">After importing, you will bulk update some properties of a document.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fb03a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb03a-109">Prerequisites</span></span>

* <span data-ttu-id="fb03a-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="fb03a-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>  

* <span data-ttu-id="fb03a-111">You can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="fb03a-111">You can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span> <span data-ttu-id="fb03a-112">Or, you can use the [Azure Cosmos DB Emulator](https://docs.microsoft.com/azure/cosmos-db/local-emulator) with  the `https://localhost:8081` URI.</span><span class="sxs-lookup"><span data-stu-id="fb03a-112">Or, you can use the [Azure Cosmos DB Emulator](https://docs.microsoft.com/azure/cosmos-db/local-emulator) with  the `https://localhost:8081` URI.</span></span> <span data-ttu-id="fb03a-113">The Primary Key is provided in [Authenticating requests](local-emulator.md#authenticating-requests).</span><span class="sxs-lookup"><span data-stu-id="fb03a-113">The Primary Key is provided in [Authenticating requests](local-emulator.md#authenticating-requests).</span></span>  

* [<span data-ttu-id="fb03a-114">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="fb03a-114">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  
  - <span data-ttu-id="fb03a-115">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="fb03a-115">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>  

  - <span data-ttu-id="fb03a-116">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="fb03a-116">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>

* <span data-ttu-id="fb03a-117">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span><span class="sxs-lookup"><span data-stu-id="fb03a-117">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>  
  
  - <span data-ttu-id="fb03a-118">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="fb03a-118">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>

* <span data-ttu-id="fb03a-119">Create an Azure Cosmos DB SQL API account by using the steps described in [create database account](create-sql-api-java.md#create-a-database-account) section of the Java quickstart article.</span><span class="sxs-lookup"><span data-stu-id="fb03a-119">Create an Azure Cosmos DB SQL API account by using the steps described in [create database account](create-sql-api-java.md#create-a-database-account) section of the Java quickstart article.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="fb03a-120">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="fb03a-120">Clone the sample application</span></span>

<span data-ttu-id="fb03a-121">Now let's switch to working with code by downloading a sample Java application from GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb03a-121">Now let's switch to working with code by downloading a sample Java application from GitHub.</span></span> <span data-ttu-id="fb03a-122">This application performs bulk operations on Azure Cosmos DB data.</span><span class="sxs-lookup"><span data-stu-id="fb03a-122">This application performs bulk operations on Azure Cosmos DB data.</span></span> <span data-ttu-id="fb03a-123">To clone the application, open a command prompt, navigate to the directory where you want to copy the application and run the following command:</span><span class="sxs-lookup"><span data-stu-id="fb03a-123">To clone the application, open a command prompt, navigate to the directory where you want to copy the application and run the following command:</span></span>

```
 git clone https://github.com/Azure/azure-cosmosdb-bulkexecutor-java-getting-started.git 
```

<span data-ttu-id="fb03a-124">The cloned repository contains two samples "bulkimport" and "bulkupdate" relative to the "\azure-cosmosdb-bulkexecutor-java-getting-started\samples\bulkexecutor-sample\src\main\java\com\microsoft\azure\cosmosdb\bulkexecutor" folder.</span><span class="sxs-lookup"><span data-stu-id="fb03a-124">The cloned repository contains two samples "bulkimport" and "bulkupdate" relative to the "\azure-cosmosdb-bulkexecutor-java-getting-started\samples\bulkexecutor-sample\src\main\java\com\microsoft\azure\cosmosdb\bulkexecutor" folder.</span></span> <span data-ttu-id="fb03a-125">The "bulkimport" application generates random documents and imports them to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fb03a-125">The "bulkimport" application generates random documents and imports them to Azure Cosmos DB.</span></span> <span data-ttu-id="fb03a-126">The "bulkupdate" application updates some documents in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fb03a-126">The "bulkupdate" application updates some documents in Azure Cosmos DB.</span></span> <span data-ttu-id="fb03a-127">In the next sections, we will review the code in each of these sample apps.</span><span class="sxs-lookup"><span data-stu-id="fb03a-127">In the next sections, we will review the code in each of these sample apps.</span></span> 

## <a name="bulk-import-data-to-azure-cosmos-db"></a><span data-ttu-id="fb03a-128">Bulk import data to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb03a-128">Bulk import data to Azure Cosmos DB</span></span>

1. <span data-ttu-id="fb03a-129">The Azure Cosmos DB’s connection strings are read as arguments and assigned to variables defined in CmdLineConfiguration.java file.</span><span class="sxs-lookup"><span data-stu-id="fb03a-129">The Azure Cosmos DB’s connection strings are read as arguments and assigned to variables defined in CmdLineConfiguration.java file.</span></span>  

2. <span data-ttu-id="fb03a-130">Next the DocumentClient object is initialized by using the following statements:</span><span class="sxs-lookup"><span data-stu-id="fb03a-130">Next the DocumentClient object is initialized by using the following statements:</span></span>  

   ```java
   ConnectionPolicy connectionPolicy = new ConnectionPolicy();
   connectionPolicy.setMaxPoolSize(1000);
   DocumentClient client = new DocumentClient(
      HOST,
      MASTER_KEY, 
      connectionPolicy,
      ConsistencyLevel.Session)
   ```

3. <span data-ttu-id="fb03a-131">The DocumentBulkExecutor object is initialized with a high retry values for wait time and throttled requests.</span><span class="sxs-lookup"><span data-stu-id="fb03a-131">The DocumentBulkExecutor object is initialized with a high retry values for wait time and throttled requests.</span></span> <span data-ttu-id="fb03a-132">And then they are set to 0 to pass congestion control to DocumentBulkExecutor for its lifetime.</span><span class="sxs-lookup"><span data-stu-id="fb03a-132">And then they are set to 0 to pass congestion control to DocumentBulkExecutor for its lifetime.</span></span>  

   ```java
   // Set client's retry options high for initialization
   client.getConnectionPolicy().getRetryOptions().setMaxRetryWaitTimeInSeconds(30);
   client.getConnectionPolicy().getRetryOptions().setMaxRetryAttemptsOnThrottledRequests(9);

   // Builder pattern
   Builder bulkExecutorBuilder = DocumentBulkExecutor.builder().from(
     client,
     DATABASE_NAME,
     COLLECTION_NAME,
     collection.getPartitionKey(),
     offerThroughput) // throughput you want to allocate for bulk import out of the container's total throughput

   // Instantiate DocumentBulkExecutor
   DocumentBulkExecutor bulkExecutor = bulkExecutorBuilder.build()

   // Set retries to 0 to pass complete control to bulk executor
   client.getConnectionPolicy().getRetryOptions().setMaxRetryWaitTimeInSeconds(0);
   client.getConnectionPolicy().getRetryOptions().setMaxRetryAttemptsOnThrottledRequests(0);
```

4. <span data-ttu-id="fb03a-133">Call the importAll API that generates random documents to bulk import into an Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="fb03a-133">Call the importAll API that generates random documents to bulk import into an Azure Cosmos DB container.</span></span> <span data-ttu-id="fb03a-134">You can configure the command line configurations within the CmdLineConfiguration.java file.</span><span class="sxs-lookup"><span data-stu-id="fb03a-134">You can configure the command line configurations within the CmdLineConfiguration.java file.</span></span>

   ```java
   BulkImportResponse bulkImportResponse = bulkExecutor.importAll(documents, false, true, null);
```
   <span data-ttu-id="fb03a-135">The bulk import API accepts a collection of JSON-serialized documents and it has the following syntax, for more details, see the [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor):</span><span class="sxs-lookup"><span data-stu-id="fb03a-135">The bulk import API accepts a collection of JSON-serialized documents and it has the following syntax, for more details, see the [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor):</span></span>

   ```java
   public BulkImportResponse importAll(
        Collection<String> documents,
        boolean isUpsert,
        boolean disableAutomaticIdGeneration,
        Integer maxConcurrencyPerPartitionRange) throws DocumentClientException;   
   ```

   <span data-ttu-id="fb03a-136">The importAll method accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="fb03a-136">The importAll method accepts the following parameters:</span></span>
 
   |<span data-ttu-id="fb03a-137">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="fb03a-137">**Parameter**</span></span>  |<span data-ttu-id="fb03a-138">**Description**</span><span class="sxs-lookup"><span data-stu-id="fb03a-138">**Description**</span></span>  |
   |---------|---------|
   |<span data-ttu-id="fb03a-139">isUpsert</span><span class="sxs-lookup"><span data-stu-id="fb03a-139">isUpsert</span></span>    |   <span data-ttu-id="fb03a-140">A flag to enable upsert of the documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-140">A flag to enable upsert of the documents.</span></span> <span data-ttu-id="fb03a-141">If a document with given ID already exists, it's updated.</span><span class="sxs-lookup"><span data-stu-id="fb03a-141">If a document with given ID already exists, it's updated.</span></span>  |
   |<span data-ttu-id="fb03a-142">disableAutomaticIdGeneration</span><span class="sxs-lookup"><span data-stu-id="fb03a-142">disableAutomaticIdGeneration</span></span>     |   <span data-ttu-id="fb03a-143">A flag to disable automatic generation of ID.</span><span class="sxs-lookup"><span data-stu-id="fb03a-143">A flag to disable automatic generation of ID.</span></span> <span data-ttu-id="fb03a-144">By default, it is set to true.</span><span class="sxs-lookup"><span data-stu-id="fb03a-144">By default, it is set to true.</span></span>   |
   |<span data-ttu-id="fb03a-145">maxConcurrencyPerPartitionRange</span><span class="sxs-lookup"><span data-stu-id="fb03a-145">maxConcurrencyPerPartitionRange</span></span>    |  <span data-ttu-id="fb03a-146">The maximum degree of concurrency per partition key range.</span><span class="sxs-lookup"><span data-stu-id="fb03a-146">The maximum degree of concurrency per partition key range.</span></span> <span data-ttu-id="fb03a-147">The default value is 20.</span><span class="sxs-lookup"><span data-stu-id="fb03a-147">The default value is 20.</span></span>  |

   <span data-ttu-id="fb03a-148">**Bulk import response object definition** The result of the bulk import API call contains the following get methods:</span><span class="sxs-lookup"><span data-stu-id="fb03a-148">**Bulk import response object definition** The result of the bulk import API call contains the following get methods:</span></span>

   |<span data-ttu-id="fb03a-149">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="fb03a-149">**Parameter**</span></span>  |<span data-ttu-id="fb03a-150">**Description**</span><span class="sxs-lookup"><span data-stu-id="fb03a-150">**Description**</span></span>  |
   |---------|---------|
   |<span data-ttu-id="fb03a-151">int getNumberOfDocumentsImported()</span><span class="sxs-lookup"><span data-stu-id="fb03a-151">int getNumberOfDocumentsImported()</span></span>  |   <span data-ttu-id="fb03a-152">The total number of documents that were successfully imported out of the documents supplied to the bulk import API call.</span><span class="sxs-lookup"><span data-stu-id="fb03a-152">The total number of documents that were successfully imported out of the documents supplied to the bulk import API call.</span></span>      |
   |<span data-ttu-id="fb03a-153">double getTotalRequestUnitsConsumed()</span><span class="sxs-lookup"><span data-stu-id="fb03a-153">double getTotalRequestUnitsConsumed()</span></span>   |  <span data-ttu-id="fb03a-154">The total request units (RU) consumed by the bulk import API call.</span><span class="sxs-lookup"><span data-stu-id="fb03a-154">The total request units (RU) consumed by the bulk import API call.</span></span>       |
   |<span data-ttu-id="fb03a-155">Duration getTotalTimeTaken()</span><span class="sxs-lookup"><span data-stu-id="fb03a-155">Duration getTotalTimeTaken()</span></span>   |    <span data-ttu-id="fb03a-156">The total time taken by the bulk import API call to complete execution.</span><span class="sxs-lookup"><span data-stu-id="fb03a-156">The total time taken by the bulk import API call to complete execution.</span></span>     |
   |<span data-ttu-id="fb03a-157">List<Exception> getErrors()</span><span class="sxs-lookup"><span data-stu-id="fb03a-157">List<Exception> getErrors()</span></span> |  <span data-ttu-id="fb03a-158">Gets the list of errors if some documents out of the batch supplied to the bulk import API call failed to get inserted.</span><span class="sxs-lookup"><span data-stu-id="fb03a-158">Gets the list of errors if some documents out of the batch supplied to the bulk import API call failed to get inserted.</span></span>       |
   |<span data-ttu-id="fb03a-159">List<Object> getBadInputDocuments()</span><span class="sxs-lookup"><span data-stu-id="fb03a-159">List<Object> getBadInputDocuments()</span></span>  |    <span data-ttu-id="fb03a-160">The list of bad-format documents that were not successfully imported in the bulk import API call.</span><span class="sxs-lookup"><span data-stu-id="fb03a-160">The list of bad-format documents that were not successfully imported in the bulk import API call.</span></span> <span data-ttu-id="fb03a-161">User should fix the documents returned and retry import.</span><span class="sxs-lookup"><span data-stu-id="fb03a-161">User should fix the documents returned and retry import.</span></span> <span data-ttu-id="fb03a-162">Bad-formatted documents include documents whose ID value is not a string (null or any other datatype is considered invalid).</span><span class="sxs-lookup"><span data-stu-id="fb03a-162">Bad-formatted documents include documents whose ID value is not a string (null or any other datatype is considered invalid).</span></span>     |

5. <span data-ttu-id="fb03a-163">After you have the bulk import application ready, build the command-line tool from source by using the 'mvn clean package' command.</span><span class="sxs-lookup"><span data-stu-id="fb03a-163">After you have the bulk import application ready, build the command-line tool from source by using the 'mvn clean package' command.</span></span> <span data-ttu-id="fb03a-164">This command generates a jar file in the target folder:</span><span class="sxs-lookup"><span data-stu-id="fb03a-164">This command generates a jar file in the target folder:</span></span>  

   ```java
   mvn clean package
   ```

6. <span data-ttu-id="fb03a-165">After the target dependencies are generated, you can invoke the bulk importer application by using the following command:</span><span class="sxs-lookup"><span data-stu-id="fb03a-165">After the target dependencies are generated, you can invoke the bulk importer application by using the following command:</span></span>  

   ```java
   java -Xmx12G -jar bulkexecutor-sample-1.0-SNAPSHOT-jar-with-dependencies.jar -serviceEndpoint *<Fill in your Azure Cosmos DB’s endpoint URI>*  -masterKey *<Fill in your Azure Cosmos DB’s master key>* -databaseId bulkImportDb -collectionId bulkImportColl -operation import -shouldCreateCollection -collectionThroughput 1000000 -partitionKey /profileid -maxConnectionPoolSize 6000 -numberOfDocumentsForEachCheckpoint 1000000 -numberOfCheckpoints 10
   ```

   <span data-ttu-id="fb03a-166">The bulk importer creates a new database and a collection with the database name, collection name, and throughput values specified in the App.config file.</span><span class="sxs-lookup"><span data-stu-id="fb03a-166">The bulk importer creates a new database and a collection with the database name, collection name, and throughput values specified in the App.config file.</span></span> 

## <a name="bulk-update-data-in-azure-cosmos-db"></a><span data-ttu-id="fb03a-167">Bulk update data in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb03a-167">Bulk update data in Azure Cosmos DB</span></span>

<span data-ttu-id="fb03a-168">You can update existing documents by using the BulkUpdateAsync API.</span><span class="sxs-lookup"><span data-stu-id="fb03a-168">You can update existing documents by using the BulkUpdateAsync API.</span></span> <span data-ttu-id="fb03a-169">In this example, you will set the Name field to a new value and remove the Description field from the existing documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-169">In this example, you will set the Name field to a new value and remove the Description field from the existing documents.</span></span> <span data-ttu-id="fb03a-170">For the full set of supported field update operations, see [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor).</span><span class="sxs-lookup"><span data-stu-id="fb03a-170">For the full set of supported field update operations, see [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor).</span></span> 

1. <span data-ttu-id="fb03a-171">Defines the update items along with corresponding field update operations.</span><span class="sxs-lookup"><span data-stu-id="fb03a-171">Defines the update items along with corresponding field update operations.</span></span> <span data-ttu-id="fb03a-172">In this example, you will use SetUpdateOperation to update the Name field and UnsetUpdateOperation to remove the Description field from all the documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-172">In this example, you will use SetUpdateOperation to update the Name field and UnsetUpdateOperation to remove the Description field from all the documents.</span></span> <span data-ttu-id="fb03a-173">You can also perform other operations like increment a document field by a specific value, push specific values into an array field, or remove a specific value from an array field.</span><span class="sxs-lookup"><span data-stu-id="fb03a-173">You can also perform other operations like increment a document field by a specific value, push specific values into an array field, or remove a specific value from an array field.</span></span> <span data-ttu-id="fb03a-174">To learn about different methods provided by the bulk update API, see the [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor).</span><span class="sxs-lookup"><span data-stu-id="fb03a-174">To learn about different methods provided by the bulk update API, see the [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor).</span></span>  

   ```java
   SetUpdateOperation<String> nameUpdate = new SetUpdateOperation<>("Name","UpdatedDocValue");
   UnsetUpdateOperation descriptionUpdate = new UnsetUpdateOperation("description");

   ArrayList<UpdateOperationBase> updateOperations = new ArrayList<>();
   updateOperations.add(nameUpdate);
   updateOperations.add(descriptionUpdate);

   List<UpdateItem> updateItems = new ArrayList<>(cfg.getNumberOfDocumentsForEachCheckpoint());
   IntStream.range(0, cfg.getNumberOfDocumentsForEachCheckpoint()).mapToObj(j -> {                      
    return new UpdateItem(Long.toString(prefix + j), Long.toString(prefix + j), updateOperations);
    }).collect(Collectors.toCollection(() -> updateItems));
   ```

2. <span data-ttu-id="fb03a-175">Call the updateAll API that generates random documents to be then bulk imported into an Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="fb03a-175">Call the updateAll API that generates random documents to be then bulk imported into an Azure Cosmos DB container.</span></span> <span data-ttu-id="fb03a-176">You can configure the command-line configurations to be passed in CmdLineConfiguration.java file.</span><span class="sxs-lookup"><span data-stu-id="fb03a-176">You can configure the command-line configurations to be passed in CmdLineConfiguration.java file.</span></span>

   ```java
   BulkUpdateResponse bulkUpdateResponse = bulkExecutor.updateAll(updateItems, null)
   ```

   <span data-ttu-id="fb03a-177">The bulk update API accepts a collection of items to be updated.</span><span class="sxs-lookup"><span data-stu-id="fb03a-177">The bulk update API accepts a collection of items to be updated.</span></span> <span data-ttu-id="fb03a-178">Each update item specifies the list of field update operations to be performed on a document identified by an ID and a partition key value.</span><span class="sxs-lookup"><span data-stu-id="fb03a-178">Each update item specifies the list of field update operations to be performed on a document identified by an ID and a partition key value.</span></span> <span data-ttu-id="fb03a-179">for more details, see the [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor):</span><span class="sxs-lookup"><span data-stu-id="fb03a-179">for more details, see the [API documentation](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb.bulkexecutor):</span></span>

   ```java
   public BulkUpdateResponse updateAll(
        Collection<UpdateItem> updateItems,
        Integer maxConcurrencyPerPartitionRange) throws DocumentClientException;
   ```

   <span data-ttu-id="fb03a-180">The updateAll method accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="fb03a-180">The updateAll method accepts the following parameters:</span></span>

   |<span data-ttu-id="fb03a-181">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="fb03a-181">**Parameter**</span></span> |<span data-ttu-id="fb03a-182">**Description**</span><span class="sxs-lookup"><span data-stu-id="fb03a-182">**Description**</span></span> |
   |---------|---------|
   |<span data-ttu-id="fb03a-183">maxConcurrencyPerPartitionRange</span><span class="sxs-lookup"><span data-stu-id="fb03a-183">maxConcurrencyPerPartitionRange</span></span>   |  <span data-ttu-id="fb03a-184">The maximum degree of concurrency per partition key range.</span><span class="sxs-lookup"><span data-stu-id="fb03a-184">The maximum degree of concurrency per partition key range.</span></span> <span data-ttu-id="fb03a-185">The default value is 20.</span><span class="sxs-lookup"><span data-stu-id="fb03a-185">The default value is 20.</span></span>  |
 
   <span data-ttu-id="fb03a-186">**Bulk import response object definition** The result of the bulk import API call contains the following get methods:</span><span class="sxs-lookup"><span data-stu-id="fb03a-186">**Bulk import response object definition** The result of the bulk import API call contains the following get methods:</span></span>

   |<span data-ttu-id="fb03a-187">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="fb03a-187">**Parameter**</span></span> |<span data-ttu-id="fb03a-188">**Description**</span><span class="sxs-lookup"><span data-stu-id="fb03a-188">**Description**</span></span>  |
   |---------|---------|
   |<span data-ttu-id="fb03a-189">int getNumberOfDocumentsUpdated()</span><span class="sxs-lookup"><span data-stu-id="fb03a-189">int getNumberOfDocumentsUpdated()</span></span>  |   <span data-ttu-id="fb03a-190">The total number of documents that were successfully updated out of the documents supplied to the bulk update API call.</span><span class="sxs-lookup"><span data-stu-id="fb03a-190">The total number of documents that were successfully updated out of the documents supplied to the bulk update API call.</span></span>      |
   |<span data-ttu-id="fb03a-191">double getTotalRequestUnitsConsumed()</span><span class="sxs-lookup"><span data-stu-id="fb03a-191">double getTotalRequestUnitsConsumed()</span></span> |  <span data-ttu-id="fb03a-192">The total request units (RU) consumed by the bulk update API call.</span><span class="sxs-lookup"><span data-stu-id="fb03a-192">The total request units (RU) consumed by the bulk update API call.</span></span>       |
   |<span data-ttu-id="fb03a-193">Duration getTotalTimeTaken()</span><span class="sxs-lookup"><span data-stu-id="fb03a-193">Duration getTotalTimeTaken()</span></span>  |   <span data-ttu-id="fb03a-194">The total time taken by the bulk update API call to complete execution.</span><span class="sxs-lookup"><span data-stu-id="fb03a-194">The total time taken by the bulk update API call to complete execution.</span></span>      |
   |<span data-ttu-id="fb03a-195">List<Exception> getErrors()</span><span class="sxs-lookup"><span data-stu-id="fb03a-195">List<Exception> getErrors()</span></span>   |     <span data-ttu-id="fb03a-196">Gets the list of errors if some documents out of the batch supplied to the bulk update API call failed to get inserted.</span><span class="sxs-lookup"><span data-stu-id="fb03a-196">Gets the list of errors if some documents out of the batch supplied to the bulk update API call failed to get inserted.</span></span>      |

3. <span data-ttu-id="fb03a-197">After you have the bulk update application ready, build the command-line tool from source by using the 'mvn clean package' command.</span><span class="sxs-lookup"><span data-stu-id="fb03a-197">After you have the bulk update application ready, build the command-line tool from source by using the 'mvn clean package' command.</span></span> <span data-ttu-id="fb03a-198">This command generates a jar file in the target folder:</span><span class="sxs-lookup"><span data-stu-id="fb03a-198">This command generates a jar file in the target folder:</span></span>  

   ```
   mvn clean package
   ```

4. <span data-ttu-id="fb03a-199">After the target dependencies are generated, you can invoke the bulk update application by using the following command:</span><span class="sxs-lookup"><span data-stu-id="fb03a-199">After the target dependencies are generated, you can invoke the bulk update application by using the following command:</span></span>

   ```
   java -Xmx12G -jar bulkexecutor-sample-1.0-SNAPSHOT-jar-with-dependencies.jar -serviceEndpoint **<Fill in your Azure Cosmos DB’s endpoint URI>* -masterKey **<Fill in your Azure Cosmos DB’s master key>* -databaseId bulkUpdateDb -collectionId bulkUpdateColl -operation update -collectionThroughput 1000000 -partitionKey /profileid -maxConnectionPoolSize 6000 -numberOfDocumentsForEachCheckpoint 1000000 -numberOfCheckpoints 10
   ```

## <a name="performance-tips"></a><span data-ttu-id="fb03a-200">Performance tips</span><span class="sxs-lookup"><span data-stu-id="fb03a-200">Performance tips</span></span> 

<span data-ttu-id="fb03a-201">Consider the following points for better performance when using bulk executor library:</span><span class="sxs-lookup"><span data-stu-id="fb03a-201">Consider the following points for better performance when using bulk executor library:</span></span>

* <span data-ttu-id="fb03a-202">For best performance, run your application from an Azure VM in the same region as your Cosmos DB account write region.</span><span class="sxs-lookup"><span data-stu-id="fb03a-202">For best performance, run your application from an Azure VM in the same region as your Cosmos DB account write region.</span></span>  
* <span data-ttu-id="fb03a-203">For achieving higher throughput:</span><span class="sxs-lookup"><span data-stu-id="fb03a-203">For achieving higher throughput:</span></span>  

   * <span data-ttu-id="fb03a-204">Set the JVM’s heap size to a large enough number to avoid any memory issue in handling large number of documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-204">Set the JVM’s heap size to a large enough number to avoid any memory issue in handling large number of documents.</span></span> <span data-ttu-id="fb03a-205">Suggested heap size: max(3GB, 3 \* sizeof(all documents passed to bulk import API in one batch)).</span><span class="sxs-lookup"><span data-stu-id="fb03a-205">Suggested heap size: max(3GB, 3 \* sizeof(all documents passed to bulk import API in one batch)).</span></span>  
   * <span data-ttu-id="fb03a-206">There is a preprocessing time, due to which you will get higher throughput when performing bulk operations with a large number of documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-206">There is a preprocessing time, due to which you will get higher throughput when performing bulk operations with a large number of documents.</span></span> <span data-ttu-id="fb03a-207">So, if you want to import 10,000,000 documents, running bulk import 10 times on 10 bulk of documents each of size 1,000,000 is preferable than running bulk import 100 times on 100 bulk of documents each of size 100,000 documents.</span><span class="sxs-lookup"><span data-stu-id="fb03a-207">So, if you want to import 10,000,000 documents, running bulk import 10 times on 10 bulk of documents each of size 1,000,000 is preferable than running bulk import 100 times on 100 bulk of documents each of size 100,000 documents.</span></span>  

* <span data-ttu-id="fb03a-208">It is recommended to instantiate a single DocumentBulkExecutor object for the entire application within a single virtual machine that corresponds to a specific Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="fb03a-208">It is recommended to instantiate a single DocumentBulkExecutor object for the entire application within a single virtual machine that corresponds to a specific Azure Cosmos DB container.</span></span>  

* <span data-ttu-id="fb03a-209">Since a single bulk operation API execution consumes a large chunk of the client machine's CPU and network IO.</span><span class="sxs-lookup"><span data-stu-id="fb03a-209">Since a single bulk operation API execution consumes a large chunk of the client machine's CPU and network IO.</span></span> <span data-ttu-id="fb03a-210">This happens by spawning multiple tasks internally, avoid spawning multiple concurrent tasks within your application process each executing bulk operation API calls.</span><span class="sxs-lookup"><span data-stu-id="fb03a-210">This happens by spawning multiple tasks internally, avoid spawning multiple concurrent tasks within your application process each executing bulk operation API calls.</span></span> <span data-ttu-id="fb03a-211">If a single bulk operation API call running on a single virtual machine is unable to consume your entire container's throughput (if your container's throughput > 1 million RU/s), it's preferable to create separate virtual machines to concurrently execute bulk operation API calls.</span><span class="sxs-lookup"><span data-stu-id="fb03a-211">If a single bulk operation API call running on a single virtual machine is unable to consume your entire container's throughput (if your container's throughput > 1 million RU/s), it's preferable to create separate virtual machines to concurrently execute bulk operation API calls.</span></span>

    
## <a name="next-steps"></a><span data-ttu-id="fb03a-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb03a-212">Next steps</span></span>
* <span data-ttu-id="fb03a-213">To learn about maven package details and release notes of bulk executor Java library, see[bulk executor SDK details](sql-api-sdk-bulk-executor-java.md).</span><span class="sxs-lookup"><span data-stu-id="fb03a-213">To learn about maven package details and release notes of bulk executor Java library, see[bulk executor SDK details](sql-api-sdk-bulk-executor-java.md).</span></span>


