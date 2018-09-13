---
title: Build a Java application by using Azure Cosmos DB Async Java SDK | Microsoft Docs
description: This tutorial shows you how to use Azure Cosmos DB SQL API accounts to store and access data by using an Async Java application.
keywords: nosql tutorial, online database, java console application
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: java
ms.topic: tutorial
ms.date: 06/29/2018
ms.author: sngun
ms.openlocfilehash: 75546ad8d52cdc3f3377439775333a6dd5be0427
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867351"
---
# <a name="build-a-java-application-by-using-azure-cosmos-db-async-java-sdk"></a><span data-ttu-id="3526d-104">Build a Java application by using Azure Cosmos DB Async Java SDK</span><span class="sxs-lookup"><span data-stu-id="3526d-104">Build a Java application by using Azure Cosmos DB Async Java SDK</span></span> 

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Node.js- v2](sql-api-nodejs-get-started-preview.md) 
> 

<span data-ttu-id="3526d-111">Azure Cosmos DB is a globally distributed multi-model database.</span><span class="sxs-lookup"><span data-stu-id="3526d-111">Azure Cosmos DB is a globally distributed multi-model database.</span></span> <span data-ttu-id="3526d-112">This tutorial shows you how to use Azure Cosmos DB SQL API accounts to store and access data by using an Async Java application.</span><span class="sxs-lookup"><span data-stu-id="3526d-112">This tutorial shows you how to use Azure Cosmos DB SQL API accounts to store and access data by using an Async Java application.</span></span> 

<span data-ttu-id="3526d-113">We cover:</span><span class="sxs-lookup"><span data-stu-id="3526d-113">We cover:</span></span>

* <span data-ttu-id="3526d-114">Creating and connecting to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="3526d-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="3526d-115">Configuring your Solution</span><span class="sxs-lookup"><span data-stu-id="3526d-115">Configuring your Solution</span></span>
* <span data-ttu-id="3526d-116">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="3526d-116">Creating a collection</span></span>
* <span data-ttu-id="3526d-117">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="3526d-117">Creating JSON documents</span></span>
* <span data-ttu-id="3526d-118">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="3526d-118">Querying the collection</span></span>

<span data-ttu-id="3526d-119">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="3526d-119">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3526d-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3526d-120">Prerequisites</span></span>
<span data-ttu-id="3526d-121">Make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="3526d-121">Make sure you have the following:</span></span>

* <span data-ttu-id="3526d-122">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="3526d-122">An active Azure account.</span></span> <span data-ttu-id="3526d-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3526d-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="3526d-124">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="3526d-124">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="3526d-125">[Java Development Kit (JDK) 8+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="3526d-125">[Java Development Kit (JDK) 8+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="3526d-126">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="3526d-126">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="3526d-127">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="3526d-127">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="3526d-128">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="3526d-128">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="3526d-129">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="3526d-129">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="3526d-130">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="3526d-130">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a><span data-ttu-id="3526d-131">Step 2: Clone the GitHub project</span><span class="sxs-lookup"><span data-stu-id="3526d-131">Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="3526d-132">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="3526d-132">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started).</span></span> <span data-ttu-id="3526d-133">For example, from a local directory run the following to retrieve the sample project locally.</span><span class="sxs-lookup"><span data-stu-id="3526d-133">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started.git

cd azure-cosmos-db-sql-api-async-java-getting-started
cd azure-cosmosdb-get-started

```
<span data-ttu-id="3526d-134">The directory contains a `pom.xml` for the project and a `src/main/java/com/microsoft/azure/cosmosdb/sample` folder containing Java source code including `Main.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span><span class="sxs-lookup"><span data-stu-id="3526d-134">The directory contains a `pom.xml` for the project and a `src/main/java/com/microsoft/azure/cosmosdb/sample` folder containing Java source code including `Main.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="3526d-135">The `pom.xml` includes a dependency on the [Azure Cosmos DB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="3526d-135">The `pom.xml` includes a dependency on the [Azure Cosmos DB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

```xml
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-documentdb</artifactId>
  <version>2.0.0</version>
</dependency>
```

## <a id="Connect"></a><span data-ttu-id="3526d-136">Step 3: Connect to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="3526d-136">Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="3526d-137">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span><span class="sxs-lookup"><span data-stu-id="3526d-137">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="3526d-138">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="3526d-138">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span> <span data-ttu-id="3526d-139">The `AccountSettings.java` file holds the primary key and URI values.</span><span class="sxs-lookup"><span data-stu-id="3526d-139">The `AccountSettings.java` file holds the primary key and URI values.</span></span> 

<span data-ttu-id="3526d-140">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="3526d-140">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="3526d-141">Copy the URI and the PRIMARY KEY from the portal and paste it into the `AccountSettings.java` file.</span><span class="sxs-lookup"><span data-stu-id="3526d-141">Copy the URI and the PRIMARY KEY from the portal and paste it into the `AccountSettings.java` file.</span></span> 

```java
public class AccountSettings 
{
  // Replace MASTER_KEY and HOST with values from your Azure Cosmos DB account.
    
  // <!--[SuppressMessage("Microsoft.Security", "CS002:SecretInNextLine")]-->
  public static String MASTER_KEY = System.getProperty("ACCOUNT_KEY", 
          StringUtils.defaultString(StringUtils.trimToNull(
          System.getenv().get("ACCOUNT_KEY")), "<Fill your Azure Cosmos DB account key>"));

  public static String HOST = System.getProperty("ACCOUNT_HOST",
           StringUtils.defaultString(StringUtils.trimToNull(
           System.getenv().get("ACCOUNT_HOST")),"<Fill your Azure Cosmos DB URI>"));
}
```

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a Java console application.][keys]

## <a name="step-4-initialize-the-client-object"></a><span data-ttu-id="3526d-144">Step 4: Initialize the client object</span><span class="sxs-lookup"><span data-stu-id="3526d-144">Step 4: Initialize the client object</span></span>
<span data-ttu-id="3526d-145">Initialize the client object by using the host URI and primary key values defined in the "AccountSettings.java" file</span><span class="sxs-lookup"><span data-stu-id="3526d-145">Initialize the client object by using the host URI and primary key values defined in the "AccountSettings.java" file</span></span>

```java
client = new AsyncDocumentClient.Builder()
         .withServiceEndpoint(AccountSettings.HOST)
         .withMasterKey(AccountSettings.MASTER_KEY)
         .withConnectionPolicy(ConnectionPolicy.GetDefault())
         .withConsistencyLevel(ConsistencyLevel.Session)
         .build();
```

## <a id="CreateDatabase"></a><span data-ttu-id="3526d-146">Step 5: Create a database</span><span class="sxs-lookup"><span data-stu-id="3526d-146">Step 5: Create a database</span></span>

<span data-ttu-id="3526d-147">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the createDatabaseIfNotExists() method of the DocumentClient class.</span><span class="sxs-lookup"><span data-stu-id="3526d-147">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the createDatabaseIfNotExists() method of the DocumentClient class.</span></span> <span data-ttu-id="3526d-148">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="3526d-148">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```java
private void createDatabaseIfNotExists() throws Exception 
{
    
    writeToConsoleAndPromptToContinue("Check if database " + databaseName + " exists.");

    String databaseLink = String.format("/dbs/%s", databaseName);

    Observable<ResourceResponse<Database>> databaseReadObs = client.readDatabase(databaseLink, null);

    Observable<ResourceResponse<Database>> databaseExistenceObs = databaseReadObs
                .doOnNext(x -> {System.out.println("database " + databaseName + " already exists.");}).onErrorResumeNext(e -> {
   // if the database doesn't already exists
   // readDatabase() will result in 404 error
   if (e instanceof DocumentClientException) 
   {
       DocumentClientException de = (DocumentClientException) e;
       // if database 
       if (de.getStatusCode() == 404) {
       // if the database doesn't exist, create it.
       System.out.println("database " + databaseName + " doesn't existed," + " creating it...");
       Database dbDefinition = new Database();
       dbDefinition.setId(databaseName);
       return client.createDatabase(dbDefinition, null);
     }
     }

    // some unexpected failure in reading database happened.
    // pass the error up.
    System.err.println("Reading database " + databaseName + " failed.");
        return Observable.error(e);     
    });

   // wait for completion
   databaseExistenceObs.toCompletable().await();

   System.out.println("Checking database " + databaseName + " completed!\n");
}
```

## <a id="CreateColl"></a><span data-ttu-id="3526d-149">Step 6: Create a collection</span><span class="sxs-lookup"><span data-stu-id="3526d-149">Step 6: Create a collection</span></span>

> [!WARNING]
> **createCollection** creates a new collection with reserved throughput, which has pricing implications. For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 
<span data-ttu-id="3526d-152">A collection can be created by using the createDocumentCollectionIfNotExists() method of the DocumentClient class.</span><span class="sxs-lookup"><span data-stu-id="3526d-152">A collection can be created by using the createDocumentCollectionIfNotExists() method of the DocumentClient class.</span></span> <span data-ttu-id="3526d-153">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="3526d-153">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

```java
private void createDocumentCollectionIfNotExists() throws Exception 
{
    
    writeToConsoleAndPromptToContinue("Check if collection " + collectionName + " exists.");

    // query for a collection with a given id
    // if it exists nothing else to be done
    // if the collection doesn't exist, create it.

    String databaseLink = String.format("/dbs/%s", databaseName);

    // we know there is only single page of result (empty or with a match)
    client.queryCollections(databaseLink, new SqlQuerySpec("SELECT * FROM r where r.id = @id", 
            new SqlParameterCollection(new SqlParameter("@id", collectionName))), null).single() 
            .flatMap(page -> {
            if (page.getResults().isEmpty()) {
             // if there is no matching collection create the collection.
             DocumentCollection collection = new DocumentCollection();
             collection.setId(collectionName);
             System.out.println("Creating collection " + collectionName);

             return client.createCollection(databaseLink, collection, null);
            } 
            else {
              // collection already exists, nothing else to be done.
              System.out.println("Collection " + collectionName + "already exists");
              return Observable.empty();
            }
      }).toCompletable().await();

 System.out.println("Checking collection " + collectionName + " completed!\n");
    }
```

## <a id="CreateDoc"></a><span data-ttu-id="3526d-154">Step 7: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="3526d-154">Step 7: Create JSON documents</span></span>

<span data-ttu-id="3526d-155">A [document](sql-api-resources.md#documents) can be created by using the createDocument method of the DocumentClient class.</span><span class="sxs-lookup"><span data-stu-id="3526d-155">A [document](sql-api-resources.md#documents) can be created by using the createDocument method of the DocumentClient class.</span></span> <span data-ttu-id="3526d-156">Documents are user-defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="3526d-156">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="3526d-157">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="3526d-157">We can now insert one or more documents.</span></span> <span data-ttu-id="3526d-158">The "src/main/java/com/microsoft/azure/cosmosdb/sample/Families.java" file defines the family JSON documents</span><span class="sxs-lookup"><span data-stu-id="3526d-158">The "src/main/java/com/microsoft/azure/cosmosdb/sample/Families.java" file defines the family JSON documents</span></span> 

```java
public static Family getJohnsonFamilyDocument() {
     Family andersenFamily = new Family();
     andersenFamily.setId("Johnson" + System.currentTimeMillis());
     andersenFamily.setLastName("Johnson");

      Parent parent1 = new Parent();
      parent1.setFirstName("John");

      Parent parent2 = new Parent();
      parent2.setFirstName("Lili");

      return andersenFamily;
    }
```

## <a id="Query"></a><span data-ttu-id="3526d-159">Step 8: Query Azure Cosmos DB resources</span><span class="sxs-lookup"><span data-stu-id="3526d-159">Step 8: Query Azure Cosmos DB resources</span></span>

<span data-ttu-id="3526d-160">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="3526d-160">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="3526d-161">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.cosmosdb.rx._async_document_client.querydocuments) method.</span><span class="sxs-lookup"><span data-stu-id="3526d-161">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.cosmosdb.rx._async_document_client.querydocuments) method.</span></span>

```java
private void executeSimpleQueryAsyncAndRegisterListenerForResult(CountDownLatch completionLatch) 
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setMaxItemCount(100);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    Observable<FeedResponse<Document>> queryObservable = client.queryDocuments(collectionLink,
           "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    queryObservable.subscribe(queryResultPage -> {
            System.out.println("Got a page of query result with " +
            queryResultPage.getResults().size() + " document(s)"
            + " and request charge of " + queryResultPage.getRequestCharge());
    },
   // terminal error signal
        e -> {
          e.printStackTrace();
          completionLatch.countDown();
        },

   // terminal completion signal
         () -> {
            completionLatch.countDown();
         });
}
```

## <a id="Run"></a><span data-ttu-id="3526d-162">Step 9: Run your Java console application all together!</span><span class="sxs-lookup"><span data-stu-id="3526d-162">Step 9: Run your Java console application all together!</span></span>
<span data-ttu-id="3526d-163">To run the application from the console, navigate to the project folder and compile using Maven:</span><span class="sxs-lookup"><span data-stu-id="3526d-163">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>

```bash
mvn package
```

<span data-ttu-id="3526d-164">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="3526d-164">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="3526d-165">Then run the app by running:</span><span class="sxs-lookup"><span data-stu-id="3526d-165">Then run the app by running:</span></span>

```bash
mvn exec:java -DACCOUNT_HOST=<YOUR_COSMOS_DB_HOSTNAME> -DACCOUNT_KEY= <YOUR_COSMOS_DB_MASTER_KEY>
```
<span data-ttu-id="3526d-166">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="3526d-166">Congratulations!</span></span> <span data-ttu-id="3526d-167">You've completed this NoSQL tutorial and have a working Java console application!</span><span class="sxs-lookup"><span data-stu-id="3526d-167">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="3526d-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="3526d-168">Next steps</span></span>
* <span data-ttu-id="3526d-169">Want a Java web app tutorial?</span><span class="sxs-lookup"><span data-stu-id="3526d-169">Want a Java web app tutorial?</span></span> <span data-ttu-id="3526d-170">See [Build a web application with Java using Azure Cosmos DB](sql-api-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="3526d-170">See [Build a web application with Java using Azure Cosmos DB](sql-api-java-application.md).</span></span>
* <span data-ttu-id="3526d-171">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3526d-171">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="3526d-172">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="3526d-172">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>

[keys]: media/sql-api-get-started/nosql-tutorial-keys.png
