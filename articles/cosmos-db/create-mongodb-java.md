---
title: 'Azure Cosmos DB: Build a console app with Java and the MongoDB API | Microsoft Docs'
description: Presents a Java code sample you can use to connect to and query the Azure Cosmos DB MongoDB API
services: cosmos-db
author: slyons
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: quick start connect, mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 05/10/2017
ms.author: sclyon
ms.openlocfilehash: ac5c0427ee178cee3abd71f4fbdfd5f8697f11a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867368"
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="a86ac-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a86ac-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-mongodb-dotnet.md)
> * [Java](create-mongodb-java.md)
> * [Node.js](create-mongodb-nodejs.md)
> * [Python](create-mongodb-flask.md)
> * [Xamarin](create-mongodb-xamarin.md)
> * [Golang](create-mongodb-golang.md)
>  

<span data-ttu-id="a86ac-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="a86ac-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a86ac-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a86ac-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a86ac-112">This quick start demonstrates how to create an Azure Cosmos DB [MongoDB API](mongodb-introduction.md) account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a86ac-112">This quick start demonstrates how to create an Azure Cosmos DB [MongoDB API](mongodb-introduction.md) account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="a86ac-113">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="a86ac-113">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a86ac-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a86ac-114">Prerequisites</span></span>

<span data-ttu-id="a86ac-115">Before you can run this sample, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="a86ac-115">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="a86ac-116">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span><span class="sxs-lookup"><span data-stu-id="a86ac-116">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
* <span data-ttu-id="a86ac-117">Maven (Run `apt-get install maven` if you don't have Maven)</span><span class="sxs-lookup"><span data-stu-id="a86ac-117">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cosmos-db-emulator-mongodb](../../includes/cosmos-db-emulator-mongodb.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="a86ac-118">Create a database account</span><span class="sxs-lookup"><span data-stu-id="a86ac-118">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="a86ac-119">Add a collection</span><span class="sxs-lookup"><span data-stu-id="a86ac-119">Add a collection</span></span>

<span data-ttu-id="a86ac-120">Name your new database, **db**, and your new collection, **coll**.</span><span class="sxs-lookup"><span data-stu-id="a86ac-120">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="a86ac-121">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="a86ac-121">Clone the sample application</span></span>

<span data-ttu-id="a86ac-122">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="a86ac-122">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="a86ac-123">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="a86ac-123">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="a86ac-124">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="a86ac-124">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="a86ac-125">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="a86ac-125">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="a86ac-126">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="a86ac-126">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="a86ac-127">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="a86ac-127">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="a86ac-128">Then open the code in your favorite editor.</span><span class="sxs-lookup"><span data-stu-id="a86ac-128">Then open the code in your favorite editor.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="a86ac-129">Review the code</span><span class="sxs-lookup"><span data-stu-id="a86ac-129">Review the code</span></span>

<span data-ttu-id="a86ac-130">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="a86ac-130">This step is optional.</span></span> <span data-ttu-id="a86ac-131">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="a86ac-131">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="a86ac-132">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="a86ac-132">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="a86ac-133">The following snippets are all taken from the Program.java file.</span><span class="sxs-lookup"><span data-stu-id="a86ac-133">The following snippets are all taken from the Program.java file.</span></span>

* <span data-ttu-id="a86ac-134">The DocumentClient is initialized.</span><span class="sxs-lookup"><span data-stu-id="a86ac-134">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="a86ac-135">A new database and collection are created.</span><span class="sxs-lookup"><span data-stu-id="a86ac-135">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="a86ac-136">Some documents are inserted using `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="a86ac-136">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="a86ac-137">Some queries are performed using `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="a86ac-137">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="a86ac-138">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="a86ac-138">Update your connection string</span></span>

<span data-ttu-id="a86ac-139">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="a86ac-139">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="a86ac-140">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span><span class="sxs-lookup"><span data-stu-id="a86ac-140">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="a86ac-141">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span><span class="sxs-lookup"><span data-stu-id="a86ac-141">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="a86ac-142">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a86ac-142">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="a86ac-143">Run the console app</span><span class="sxs-lookup"><span data-stu-id="a86ac-143">Run the console app</span></span>

1. <span data-ttu-id="a86ac-144">Run `mvn package` in a terminal to install required npm modules</span><span class="sxs-lookup"><span data-stu-id="a86ac-144">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="a86ac-145">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span><span class="sxs-lookup"><span data-stu-id="a86ac-145">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="a86ac-146">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="a86ac-146">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="a86ac-147">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a86ac-147">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="a86ac-148">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a86ac-148">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="a86ac-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="a86ac-149">Next steps</span></span>

<span data-ttu-id="a86ac-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span><span class="sxs-lookup"><span data-stu-id="a86ac-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="a86ac-151">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="a86ac-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import MongoDB data into Azure Cosmos DB](mongodb-migrate.md)


