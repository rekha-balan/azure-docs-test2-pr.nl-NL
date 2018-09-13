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
# <a name="nosql-tutorial-build-a-documentdb-java-console-application"></a>NoSQL tutorial: Build a DocumentDB Java console application
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Welcome to the NoSQL tutorial for the Azure DocumentDB Java SDK! After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.

We cover:

* Creating and connecting to a DocumentDB account
* Configuring your Visual Studio Solution
* Creating an online database
* Creating a collection
* Creating JSON documents
* Querying the collection
* Creating JSON documents
* Querying the collection
* Replacing a document
* Deleting a document
* Deleting the database

Now let's get started!

## <a name="prerequisites"></a>Prerequisites
Make sure you have the following:

* An active Azure account. If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/). Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.
* [Git](https://git-scm.com/downloads)
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-a-documentdb-account"></a>Step 1: Create a DocumentDB account
Let's create a DocumentDB account. If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone). If you are using the DocumentDB Emulator, follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="GitClone"></a>Step 2: Clone the GitHub project
You can get started by cloning the GitHub repository for [Get Started with DocumentDB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started). For example, from a local directory run the following to retrieve the sample project locally.

    git clone git@github.com:Azure-Samples/documentdb-java-getting-started.git

    cd documentdb-java-getting-started

The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure DocumentDB like creating documents and querying data within a collection. The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Step 3: Connect to a DocumentDB account
Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key. The DocumentDB endpoint and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.

In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**. Copy the URI from the portal and paste it into `<your endpoint URI>` in the Program.java file. Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.

    this.client = new DocumentClient(
        "<your endpoint URI>",
        "<your key>"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a Java console application. Shows a DocumentDB account, with the ACTIVE hub highlighted, the KEYS button highlighted on the DocumentDB account blade, and the URI, PRIMARY KEY and SECONDARY KEY values highlighted on the Keys blade][keys]

## <a name="step-4-create-a-database"></a>Step 4: Create a database
Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createDatabase-com.microsoft.azure.documentdb.Database-com.microsoft.azure.documentdb.RequestOptions-) method of the **DocumentClient** class. A database is the logical container of JSON document storage partitioned across collections.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Step 5: Create a collection
> [!WARNING]
> **createCollection** creates a new collection with reserved throughput, which has pricing implications. For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).
> 
> 

A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createCollection-java.lang.String-com.microsoft.azure.documentdb.DocumentCollection-com.microsoft.azure.documentdb.RequestOptions-) method of the **DocumentClient** class. A collection is a container of JSON documents and associated JavaScript application logic.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // DocumentDB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Step 6: Create JSON documents
A [document](documentdb-resources.md#documents) can be created by using the [createDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#createDocument-java.lang.String-java.lang.Object-com.microsoft.azure.documentdb.RequestOptions-boolean-) method of the **DocumentClient** class. Documents are user-defined (arbitrary) JSON content. We can now insert one or more documents. If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) to import the data into a database.

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

## <a id="Query"></a>Step 7: Query DocumentDB resources
DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.  The following sample code shows how to query documents in DocumentDB using SQL syntax with the [queryDocuments](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#queryDocuments-java.lang.String-com.microsoft.azure.documentdb.SqlQuerySpec-com.microsoft.azure.documentdb.FeedOptions-) method.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Step 8: Replace JSON document
DocumentDB supports updating JSON documents using the [replaceDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#replaceDocument-com.microsoft.azure.documentdb.Document-com.microsoft.azure.documentdb.RequestOptions-) method.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Step 9: Delete JSON document
Similarly, DocumentDB supports deleting JSON documents using the [deleteDocument](http://azure.github.io/azure-documentdb-java/com/microsoft/azure/documentdb/DocumentClient.html#deleteDocument-java.lang.String-com.microsoft.azure.documentdb.RequestOptions-) method.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Step 10: Delete the database
Deleting the created database removes the database and all children resources (collections, documents, etc.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Step 11: Run your Java console application all together!
To run the application from the console, first compile using Maven:
    
    mvn package

Running `mvn package` downloads the latest DocumentDB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`. Then run the app by running:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Congratulations! You've completed this NoSQL tutorial and have a working Java console application!

## <a name="next-steps"></a>Next steps
* Want a Java web app tutorial? See [Build a web application with Java using DocumentDB](documentdb-java-application.md).
* Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).
* Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).
* Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).

[documentdb-create-account]: documentdb-create-account.md
[keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-keys.png


