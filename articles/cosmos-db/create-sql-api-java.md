---
title: Create an Azure Cosmos DB document database with Java | Microsoft Docs | Microsoft Docs'
description: Presents a Java code sample you can use to connect to and query the Azure Cosmos DB SQL API
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.custom: quick start connect, mvc, devcenter
ms.devlang: java
ms.topic: quickstart
ms.date: 03/26/2018
ms.author: sngun
ms.openlocfilehash: e218dccee322b6e387e78c04dba5afb9677c1b4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866013"
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a><span data-ttu-id="68978-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="68978-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-sql-api-dotnet.md)
> * [Java](create-sql-api-java.md)
> * [Node.js](create-sql-api-nodejs.md)
> * [Node.js- v2](create-sql-api-nodejs-preview.md)
> * [Python](create-sql-api-python.md)
> * [Xamarin](create-sql-api-xamarin-dotnet.md)
>  

<span data-ttu-id="68978-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="68978-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="68978-111">Using Azure Cosmos DB, you can quickly create and query managed document, table, and graph databases.</span><span class="sxs-lookup"><span data-stu-id="68978-111">Using Azure Cosmos DB, you can quickly create and query managed document, table, and graph databases.</span></span>

<span data-ttu-id="68978-112">This quickstart creates a document database using the Azure portal tools for the Azure Cosmos DB [SQL API](sql-api-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68978-112">This quickstart creates a document database using the Azure portal tools for the Azure Cosmos DB [SQL API](sql-api-introduction.md).</span></span> <span data-ttu-id="68978-113">This quickstart also shows you how to quickly create a Java console app using the [SQL Java API](sql-api-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="68978-113">This quickstart also shows you how to quickly create a Java console app using the [SQL Java API](sql-api-sdk-java.md).</span></span> <span data-ttu-id="68978-114">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span><span class="sxs-lookup"><span data-stu-id="68978-114">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="68978-115">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programmatically, whichever is your preference.</span><span class="sxs-lookup"><span data-stu-id="68978-115">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programmatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68978-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="68978-116">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

<span data-ttu-id="68978-117">In addition:</span><span class="sxs-lookup"><span data-stu-id="68978-117">In addition:</span></span> 

* [<span data-ttu-id="68978-118">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="68978-118">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="68978-119">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="68978-119">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="68978-120">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="68978-120">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="68978-121">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span><span class="sxs-lookup"><span data-stu-id="68978-121">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="68978-122">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="68978-122">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="68978-123">Git</span><span class="sxs-lookup"><span data-stu-id="68978-123">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="68978-124">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="68978-124">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="68978-125">Create a database account</span><span class="sxs-lookup"><span data-stu-id="68978-125">Create a database account</span></span>

<span data-ttu-id="68978-126">Before you can create a document database, you need to create a SQL API account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="68978-126">Before you can create a document database, you need to create a SQL API account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="68978-127">Add a collection</span><span class="sxs-lookup"><span data-stu-id="68978-127">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="68978-128">Add sample data</span><span class="sxs-lookup"><span data-stu-id="68978-128">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-add-sample-data](../../includes/cosmos-db-create-sql-api-add-sample-data.md)]

## <a name="query-your-data"></a><span data-ttu-id="68978-129">Query your data</span><span class="sxs-lookup"><span data-stu-id="68978-129">Query your data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-query-data](../../includes/cosmos-db-create-sql-api-query-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="68978-130">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="68978-130">Clone the sample application</span></span>

<span data-ttu-id="68978-131">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="68978-131">Now let's switch to working with code.</span></span> <span data-ttu-id="68978-132">Let's clone a SQL API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="68978-132">Let's clone a SQL API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="68978-133">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="68978-133">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="68978-134">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="68978-134">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="68978-135">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="68978-135">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span> 

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="68978-136">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="68978-136">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="68978-137">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="68978-137">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="68978-138">Review the code</span><span class="sxs-lookup"><span data-stu-id="68978-138">Review the code</span></span>

<span data-ttu-id="68978-139">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="68978-139">This step is optional.</span></span> <span data-ttu-id="68978-140">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="68978-140">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="68978-141">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="68978-141">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="68978-142">The following snippets are all taken from the C:\git-samples\azure-cosmos-db-documentdb-java-getting-started\src\GetStarted\Program.java file.</span><span class="sxs-lookup"><span data-stu-id="68978-142">The following snippets are all taken from the C:\git-samples\azure-cosmos-db-documentdb-java-getting-started\src\GetStarted\Program.java file.</span></span>

* <span data-ttu-id="68978-143">`DocumentClient` initialization.</span><span class="sxs-lookup"><span data-stu-id="68978-143">`DocumentClient` initialization.</span></span> <span data-ttu-id="68978-144">The [DocumentClient](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client) provides client-side logical representation for the Azure Cosmos DB database service.</span><span class="sxs-lookup"><span data-stu-id="68978-144">The [DocumentClient](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client) provides client-side logical representation for the Azure Cosmos DB database service.</span></span> <span data-ttu-id="68978-145">This client is used to configure and execute requests against the service.</span><span class="sxs-lookup"><span data-stu-id="68978-145">This client is used to configure and execute requests against the service.</span></span> <span data-ttu-id="68978-146">The `FILLME` portions of this code will be updated later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="68978-146">The `FILLME` portions of this code will be updated later in the quickstart.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="68978-147">[Database](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._database) creation.</span><span class="sxs-lookup"><span data-stu-id="68978-147">[Database](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._database) creation.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="68978-148">[DocumentCollection](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_collection) creation.</span><span class="sxs-lookup"><span data-stu-id="68978-148">[DocumentCollection](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_collection) creation.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="68978-149">Document creation by using the [createDocument](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method.</span><span class="sxs-lookup"><span data-stu-id="68978-149">Document creation by using the [createDocument](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="68978-150">SQL queries over JSON are performed using the [queryDocuments](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span><span class="sxs-lookup"><span data-stu-id="68978-150">SQL queries over JSON are performed using the [queryDocuments](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="68978-151">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="68978-151">Update your connection string</span></span>

<span data-ttu-id="68978-152">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="68978-152">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="68978-153">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="68978-153">This enables your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="68978-154">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="68978-154">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span></span> 

    <span data-ttu-id="68978-155">Use the copy buttons on the right side of the screen to copy the top value, the URI.</span><span class="sxs-lookup"><span data-stu-id="68978-155">Use the copy buttons on the right side of the screen to copy the top value, the URI.</span></span>

    ![View and copy an access key in the Azure portal, Keys page](./media/create-sql-api-java/keys.png)

2. <span data-ttu-id="68978-157">Open the `Program.java` file from C:\git-samples\azure-cosmos-db-documentdb-java-getting-started\src\GetStarted folder.</span><span class="sxs-lookup"><span data-stu-id="68978-157">Open the `Program.java` file from C:\git-samples\azure-cosmos-db-documentdb-java-getting-started\src\GetStarted folder.</span></span> 

3. <span data-ttu-id="68978-158">Paste the URI value from the portal over `https://FILLME.documents.azure.com` on line 45.</span><span class="sxs-lookup"><span data-stu-id="68978-158">Paste the URI value from the portal over `https://FILLME.documents.azure.com` on line 45.</span></span>

4. <span data-ttu-id="68978-159">Go back to portal and copy the PRIMARY KEY value as shown in the screenshot.</span><span class="sxs-lookup"><span data-stu-id="68978-159">Go back to portal and copy the PRIMARY KEY value as shown in the screenshot.</span></span> <span data-ttu-id="68978-160">Paste the PRIMARY KEY value from the portal over `FILLME` on line 46.</span><span class="sxs-lookup"><span data-stu-id="68978-160">Paste the PRIMARY KEY value from the portal over `FILLME` on line 46.</span></span>

    <span data-ttu-id="68978-161">The getStartedDemo method should now look similar to this:</span><span class="sxs-lookup"><span data-stu-id="68978-161">The getStartedDemo method should now look similar to this:</span></span> 
    
    ```java
    private void getStartedDemo() throws DocumentClientException, IOException {
        this.client = new DocumentClient("https://youraccountname.documents.azure.com:443/",
                "your-primary-key...RJhQrqQ5QQ==", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);
    ```

5. <span data-ttu-id="68978-162">Save the Program.java file.</span><span class="sxs-lookup"><span data-stu-id="68978-162">Save the Program.java file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="68978-163">Run the app</span><span class="sxs-lookup"><span data-stu-id="68978-163">Run the app</span></span>

1. <span data-ttu-id="68978-164">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="68978-164">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

    ```git
    cd "C:\git-samples\azure-cosmos-db-documentdb-java-getting-started"
    ```

2. <span data-ttu-id="68978-165">In the git terminal window, use the following command to install the required Java packages.</span><span class="sxs-lookup"><span data-stu-id="68978-165">In the git terminal window, use the following command to install the required Java packages.</span></span>

    ```
    mvn package
    ```

3. <span data-ttu-id="68978-166">In the git terminal window, use the following command to start the Java application.</span><span class="sxs-lookup"><span data-stu-id="68978-166">In the git terminal window, use the following command to start the Java application.</span></span>

    ```
    mvn exec:java -D exec.mainClass=GetStarted.Program
    ```

    <span data-ttu-id="68978-167">The terminal window displays a notification that the FamilyDB database was created.</span><span class="sxs-lookup"><span data-stu-id="68978-167">The terminal window displays a notification that the FamilyDB database was created.</span></span> 
    
4. <span data-ttu-id="68978-168">Press a key to create the database, and then another key to create the collection.</span><span class="sxs-lookup"><span data-stu-id="68978-168">Press a key to create the database, and then another key to create the collection.</span></span> 

    <span data-ttu-id="68978-169">At the end of the program all the resources are deleted, so switch back to Data Explorer in your browser to see that it now contains a FamilyDB database, and FamilyCollection collection.</span><span class="sxs-lookup"><span data-stu-id="68978-169">At the end of the program all the resources are deleted, so switch back to Data Explorer in your browser to see that it now contains a FamilyDB database, and FamilyCollection collection.</span></span>

5. <span data-ttu-id="68978-170">Switch to the console window and press a key to create the first document, and then another key to create the second document.</span><span class="sxs-lookup"><span data-stu-id="68978-170">Switch to the console window and press a key to create the first document, and then another key to create the second document.</span></span> <span data-ttu-id="68978-171">Then switch back to Data Explorer to view them.</span><span class="sxs-lookup"><span data-stu-id="68978-171">Then switch back to Data Explorer to view them.</span></span> 

6. <span data-ttu-id="68978-172">Press a key to run a query and see the output in the console window.</span><span class="sxs-lookup"><span data-stu-id="68978-172">Press a key to run a query and see the output in the console window.</span></span> 

7. <span data-ttu-id="68978-173">The next key you press deletes the resources.</span><span class="sxs-lookup"><span data-stu-id="68978-173">The next key you press deletes the resources.</span></span> <span data-ttu-id="68978-174">If you want to keep the resources you can press CTRL+C in the console window to end the program.</span><span class="sxs-lookup"><span data-stu-id="68978-174">If you want to keep the resources you can press CTRL+C in the console window to end the program.</span></span> <span data-ttu-id="68978-175">Otherwise, press any key to delete the resources from your account so that you don't incur charges.</span><span class="sxs-lookup"><span data-stu-id="68978-175">Otherwise, press any key to delete the resources from your account so that you don't incur charges.</span></span> 

    ![Console output](./media/create-sql-api-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="68978-177">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="68978-177">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="68978-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="68978-178">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="68978-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="68978-179">Next steps</span></span>

<span data-ttu-id="68978-180">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span><span class="sxs-lookup"><span data-stu-id="68978-180">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="68978-181">You can now import additional data into your Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="68978-181">You can now import additional data into your Azure Cosmos DB collection.</span></span> 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md)


