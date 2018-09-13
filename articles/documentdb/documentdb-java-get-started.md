---
title: 'NoSQL tutorial: Azure DocumentDB Java SDK | Microsoft Docs'
description: A NoSQL tutorial that creates an online database and Java console application using the DocumentDB Java SDK. Azure DocumentDB is a NoSQL database for JSON.
keywords: nosql tutorial, online database, java console application
services: documentdb
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 01/05/2017
ms.author: arramac
ms.openlocfilehash: 0ab0f6a7bb3370b347a9729742d8123a66f6b456
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556587"
---
# <a name="nosql-tutorial-build-a-documentdb-java-console-application"></a><span data-ttu-id="efceb-105">NoSQL tutorial: Build a DocumentDB Java console application</span><span class="sxs-lookup"><span data-stu-id="efceb-105">NoSQL tutorial: Build a DocumentDB Java console application</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="efceb-112">Welcome to the NoSQL tutorial for the Azure DocumentDB Java SDK!</span><span class="sxs-lookup"><span data-stu-id="efceb-112">Welcome to the NoSQL tutorial for the Azure DocumentDB Java SDK!</span></span> <span data-ttu-id="efceb-113">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="efceb-113">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span></span>

<span data-ttu-id="efceb-114">We cover:</span><span class="sxs-lookup"><span data-stu-id="efceb-114">We cover:</span></span>

* <span data-ttu-id="efceb-115">Creating and connecting to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="efceb-115">Creating and connecting to a DocumentDB account</span></span>
* <span data-ttu-id="efceb-116">Configuring your Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="efceb-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="efceb-117">Creating an online database</span><span class="sxs-lookup"><span data-stu-id="efceb-117">Creating an online database</span></span>
* <span data-ttu-id="efceb-118">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="efceb-118">Creating a collection</span></span>
* <span data-ttu-id="efceb-119">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="efceb-119">Creating JSON documents</span></span>
* <span data-ttu-id="efceb-120">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="efceb-120">Querying the collection</span></span>
* <span data-ttu-id="efceb-121">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="efceb-121">Creating JSON documents</span></span>
* <span data-ttu-id="efceb-122">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="efceb-122">Querying the collection</span></span>
* <span data-ttu-id="efceb-123">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="efceb-123">Replacing a document</span></span>
* <span data-ttu-id="efceb-124">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="efceb-124">Deleting a document</span></span>
* <span data-ttu-id="efceb-125">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="efceb-125">Deleting the database</span></span>

<span data-ttu-id="efceb-126">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="efceb-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efceb-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="efceb-127">Prerequisites</span></span>
<span data-ttu-id="efceb-128">Make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="efceb-128">Make sure you have the following:</span></span>

* <span data-ttu-id="efceb-129">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="efceb-129">An active Azure account.</span></span> <span data-ttu-id="efceb-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="efceb-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="efceb-131">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="efceb-131">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="efceb-132">Git</span><span class="sxs-lookup"><span data-stu-id="efceb-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="efceb-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="efceb-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="efceb-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="efceb-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-a-documentdb-account"></a><span data-ttu-id="efceb-135">Step 1: Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="efceb-135">Step 1: Create a DocumentDB account</span></span>
<span data-ttu-id="efceb-136">Let's create a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="efceb-136">Let's create a DocumentDB account.</span></span> <span data-ttu-id="efceb-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="efceb-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="efceb-138">If you are using the DocumentDB Emulator, follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="efceb-138">If you are using the DocumentDB Emulator, follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="GitClone"></a><span data-ttu-id="efceb-139">Step 2: Clone the GitHub project</span><span class="sxs-lookup"><span data-stu-id="efceb-139">Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="efceb-140">You can get started by cloning the GitHub repository for [Get Started with DocumentDB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="efceb-140">You can get started by cloning the GitHub repository for [Get Started with DocumentDB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="efceb-141">For example, from a local directory run the following to retrieve the sample project locally.</span><span class="sxs-lookup"><span data-stu-id="efceb-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/documentdb-java-getting-started.git

    cd documentdb-java-getting-started

<span data-ttu-id="efceb-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure DocumentDB like creating documents and querying data within a collection.</span><span class="sxs-lookup"><span data-stu-id="efceb-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure DocumentDB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="efceb-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="efceb-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a><span data-ttu-id="efceb-144">Step 3: Connect to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="efceb-144">Step 3: Connect to a DocumentDB account</span></span>
<span data-ttu-id="efceb-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span><span class="sxs-lookup"><span data-stu-id="efceb-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="efceb-146">The DocumentDB endpoint and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="efceb-146">The DocumentDB endpoint and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span></span>

<span data-ttu-id="efceb-147">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="efceb-147">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span></span> <span data-ttu-id="efceb-148">Copy the URI from the portal and paste it into `<your endpoint URI>` in the Program.java file.</span><span class="sxs-lookup"><span data-stu-id="efceb-148">Copy the URI from the portal and paste it into `<your endpoint URI>` in the Program.java file.</span></span> <span data-ttu-id="efceb-149">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="efceb-149">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span>

    this.client = new DocumentClient(
        "<your endpoint URI>",
        "<your key>"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a Java console application.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="efceb-152">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="efceb-152">Step 4: Create a database</span></span>
<span data-ttu-id="efceb-153">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createDatabase-com.microsoft.azure.documentdb.Database-com.microsoft.azure.documentdb.RequestOptions-) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="efceb-153">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createDatabase-com.microsoft.azure.documentdb.Database-com.microsoft.azure.documentdb.RequestOptions-) method of the **DocumentClient** class.</span></span> <span data-ttu-id="efceb-154">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="efceb-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a><span data-ttu-id="efceb-155">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="efceb-155">Step 5: Create a collection</span></span>
> [!WARNING]
> **createCollection** creates a new collection with reserved throughput, which has pricing implications. For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).
> 
> 

<span data-ttu-id="efceb-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createCollection-java.lang.String-com.microsoft.azure.documentdb.DocumentCollection-com.microsoft.azure.documentdb.RequestOptions-) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="efceb-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createCollection-java.lang.String-com.microsoft.azure.documentdb.DocumentCollection-com.microsoft.azure.documentdb.RequestOptions-) method of the **DocumentClient** class.</span></span> <span data-ttu-id="efceb-159">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="efceb-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // DocumentDB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a><span data-ttu-id="efceb-160">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="efceb-160">Step 6: Create JSON documents</span></span>
<span data-ttu-id="efceb-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createDocument-java.lang.String-java.lang.Object-com.microsoft.azure.documentdb.RequestOptions-boolean-) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="efceb-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createDocument-java.lang.String-java.lang.Object-com.microsoft.azure.documentdb.RequestOptions-boolean-) method of the **DocumentClient** class.</span></span> <span data-ttu-id="efceb-162">Documents are user-defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="efceb-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="efceb-163">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="efceb-163">We can now insert one or more documents.</span></span> <span data-ttu-id="efceb-164">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) to import the data into a database.</span><span class="sxs-lookup"><span data-stu-id="efceb-164">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) to import the data into a database.</span></span>

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

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a Java console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="efceb-166">Step 7: Query DocumentDB resources</span><span class="sxs-lookup"><span data-stu-id="efceb-166">Step 7: Query DocumentDB resources</span></span>
<span data-ttu-id="efceb-167">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="efceb-167">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="efceb-168">The following sample code shows how to query documents in DocumentDB using SQL syntax with the [queryDocuments](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#queryDocuments-java.lang.String-com.microsoft.azure.documentdb.SqlQuerySpec-com.microsoft.azure.documentdb.FeedOptions-) method.</span><span class="sxs-lookup"><span data-stu-id="efceb-168">The following sample code shows how to query documents in DocumentDB using SQL syntax with the [queryDocuments](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#queryDocuments-java.lang.String-com.microsoft.azure.documentdb.SqlQuerySpec-com.microsoft.azure.documentdb.FeedOptions-) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a><span data-ttu-id="efceb-169">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="efceb-169">Step 8: Replace JSON document</span></span>
<span data-ttu-id="efceb-170">DocumentDB supports updating JSON documents using the [replaceDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#replaceDocument-com.microsoft.azure.documentdb.Document-com.microsoft.azure.documentdb.RequestOptions-) method.</span><span class="sxs-lookup"><span data-stu-id="efceb-170">DocumentDB supports updating JSON documents using the [replaceDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#replaceDocument-com.microsoft.azure.documentdb.Document-com.microsoft.azure.documentdb.RequestOptions-) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a><span data-ttu-id="efceb-171">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="efceb-171">Step 9: Delete JSON document</span></span>
<span data-ttu-id="efceb-172">Similarly, DocumentDB supports deleting JSON documents using the [deleteDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#deleteDocument-java.lang.String-com.microsoft.azure.documentdb.RequestOptions-) method.</span><span class="sxs-lookup"><span data-stu-id="efceb-172">Similarly, DocumentDB supports deleting JSON documents using the [deleteDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#deleteDocument-java.lang.String-com.microsoft.azure.documentdb.RequestOptions-) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a><span data-ttu-id="efceb-173">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="efceb-173">Step 10: Delete the database</span></span>
<span data-ttu-id="efceb-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="efceb-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a><span data-ttu-id="efceb-175">Step 11: Run your Java console application all together!</span><span class="sxs-lookup"><span data-stu-id="efceb-175">Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="efceb-176">To run the application from the console, first compile using Maven:</span><span class="sxs-lookup"><span data-stu-id="efceb-176">To run the application from the console, first compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="efceb-177">Running `mvn package` downloads the latest DocumentDB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="efceb-177">Running `mvn package` downloads the latest DocumentDB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="efceb-178">Then run the app by running:</span><span class="sxs-lookup"><span data-stu-id="efceb-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="efceb-179">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="efceb-179">Congratulations!</span></span> <span data-ttu-id="efceb-180">You've completed this NoSQL tutorial and have a working Java console application!</span><span class="sxs-lookup"><span data-stu-id="efceb-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="efceb-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="efceb-181">Next steps</span></span>
* <span data-ttu-id="efceb-182">Want a Java web app tutorial?</span><span class="sxs-lookup"><span data-stu-id="efceb-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="efceb-183">See [Build a web application with Java using DocumentDB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="efceb-183">See [Build a web application with Java using DocumentDB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="efceb-184">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="efceb-184">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="efceb-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="efceb-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="efceb-186">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="efceb-186">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[documentdb-create-account]: documentdb-create-account.md
[keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-keys.png


