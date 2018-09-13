---
title: 'NoSQL tutorial: SQL API for Azure Cosmos DB Java SDK | Microsoft Docs'
description: A NoSQL tutorial that creates an online database and Java console application using the SQL API for Azure Cosmos DB. Azure SQL is a NoSQL database for JSON.
keywords: nosql tutorial, online database, java console application
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: sngun
ms.openlocfilehash: c69aefa6271f9766687ce3b63f959dd4e414b98c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867062"
---
# <a name="nosql-tutorial-build-a-sql-api-java-console-application"></a><span data-ttu-id="982e3-105">NoSQL tutorial: Build a SQL API Java console application</span><span class="sxs-lookup"><span data-stu-id="982e3-105">NoSQL tutorial: Build a SQL API Java console application</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Node.js- v2](sql-api-nodejs-get-started-preview.md) 
> 

<span data-ttu-id="982e3-112">Welcome to the NoSQL tutorial for the SQL API for Azure Cosmos DB Java SDK!</span><span class="sxs-lookup"><span data-stu-id="982e3-112">Welcome to the NoSQL tutorial for the SQL API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="982e3-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="982e3-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="982e3-114">We cover:</span><span class="sxs-lookup"><span data-stu-id="982e3-114">We cover:</span></span>

* <span data-ttu-id="982e3-115">Creating and connecting to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="982e3-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="982e3-116">Configuring your Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="982e3-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="982e3-117">Creating an online database</span><span class="sxs-lookup"><span data-stu-id="982e3-117">Creating an online database</span></span>
* <span data-ttu-id="982e3-118">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="982e3-118">Creating a collection</span></span>
* <span data-ttu-id="982e3-119">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="982e3-119">Creating JSON documents</span></span>
* <span data-ttu-id="982e3-120">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="982e3-120">Querying the collection</span></span>
* <span data-ttu-id="982e3-121">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="982e3-121">Creating JSON documents</span></span>
* <span data-ttu-id="982e3-122">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="982e3-122">Querying the collection</span></span>
* <span data-ttu-id="982e3-123">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="982e3-123">Replacing a document</span></span>
* <span data-ttu-id="982e3-124">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="982e3-124">Deleting a document</span></span>
* <span data-ttu-id="982e3-125">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="982e3-125">Deleting the database</span></span>

<span data-ttu-id="982e3-126">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="982e3-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="982e3-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="982e3-127">Prerequisites</span></span>
<span data-ttu-id="982e3-128">Make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="982e3-128">Make sure you have the following:</span></span>

* <span data-ttu-id="982e3-129">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="982e3-129">An active Azure account.</span></span> <span data-ttu-id="982e3-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="982e3-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="982e3-131">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="982e3-131">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="982e3-132">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="982e3-132">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="982e3-133">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="982e3-133">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="982e3-134">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="982e3-134">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="982e3-135">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="982e3-135">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="982e3-136">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="982e3-136">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="982e3-137">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="982e3-137">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a><span data-ttu-id="982e3-138">Step 2: Clone the GitHub project</span><span class="sxs-lookup"><span data-stu-id="982e3-138">Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="982e3-139">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="982e3-139">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="982e3-140">For example, from a local directory run the following to retrieve the sample project locally.</span><span class="sxs-lookup"><span data-stu-id="982e3-140">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="982e3-141">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span><span class="sxs-lookup"><span data-stu-id="982e3-141">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="982e3-142">The `pom.xml` includes a dependency on the [Azure Cosmos DB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="982e3-142">The `pom.xml` includes a dependency on the [Azure Cosmos DB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a><span data-ttu-id="982e3-143">Step 3: Connect to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="982e3-143">Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="982e3-144">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span><span class="sxs-lookup"><span data-stu-id="982e3-144">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="982e3-145">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="982e3-145">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="982e3-146">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="982e3-146">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="982e3-147">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span><span class="sxs-lookup"><span data-stu-id="982e3-147">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="982e3-148">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="982e3-148">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a Java console application.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="982e3-151">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="982e3-151">Step 4: Create a database</span></span>
<span data-ttu-id="982e3-152">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="982e3-152">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="982e3-153">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="982e3-153">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a><span data-ttu-id="982e3-154">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="982e3-154">Step 5: Create a collection</span></span>
> [!WARNING]
> **createCollection** creates a new collection with reserved throughput, which has pricing implications. For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

<span data-ttu-id="982e3-157">A [collection](sql-api-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="982e3-157">A [collection](sql-api-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="982e3-158">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="982e3-158">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a><span data-ttu-id="982e3-159">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="982e3-159">Step 6: Create JSON documents</span></span>
<span data-ttu-id="982e3-160">A [document](sql-api-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="982e3-160">A [document](sql-api-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="982e3-161">Documents are user-defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="982e3-161">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="982e3-162">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="982e3-162">We can now insert one or more documents.</span></span> <span data-ttu-id="982e3-163">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span><span class="sxs-lookup"><span data-stu-id="982e3-163">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a Java console application](./media/sql-api-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="982e3-165">Step 7: Query Azure Cosmos DB resources</span><span class="sxs-lookup"><span data-stu-id="982e3-165">Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="982e3-166">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="982e3-166">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="982e3-167">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span><span class="sxs-lookup"><span data-stu-id="982e3-167">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a><span data-ttu-id="982e3-168">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="982e3-168">Step 8: Replace JSON document</span></span>
<span data-ttu-id="982e3-169">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span><span class="sxs-lookup"><span data-stu-id="982e3-169">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a><span data-ttu-id="982e3-170">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="982e3-170">Step 9: Delete JSON document</span></span>
<span data-ttu-id="982e3-171">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span><span class="sxs-lookup"><span data-stu-id="982e3-171">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a><span data-ttu-id="982e3-172">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="982e3-172">Step 10: Delete the database</span></span>
<span data-ttu-id="982e3-173">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="982e3-173">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a><span data-ttu-id="982e3-174">Step 11: Run your Java console application all together!</span><span class="sxs-lookup"><span data-stu-id="982e3-174">Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="982e3-175">To run the application from the console, navigate to the project folder and compile using Maven:</span><span class="sxs-lookup"><span data-stu-id="982e3-175">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="982e3-176">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="982e3-176">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="982e3-177">Then run the app by running:</span><span class="sxs-lookup"><span data-stu-id="982e3-177">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="982e3-178">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="982e3-178">Congratulations!</span></span> <span data-ttu-id="982e3-179">You've completed this NoSQL tutorial and have a working Java console application!</span><span class="sxs-lookup"><span data-stu-id="982e3-179">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="982e3-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="982e3-180">Next steps</span></span>
* <span data-ttu-id="982e3-181">Want a Java web app tutorial?</span><span class="sxs-lookup"><span data-stu-id="982e3-181">Want a Java web app tutorial?</span></span> <span data-ttu-id="982e3-182">See [Build a web application with Java using Azure Cosmos DB](sql-api-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="982e3-182">See [Build a web application with Java using Azure Cosmos DB](sql-api-java-application.md).</span></span>
* <span data-ttu-id="982e3-183">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="982e3-183">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="982e3-184">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="982e3-184">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>

[keys]: media/sql-api-get-started/nosql-tutorial-keys.png
