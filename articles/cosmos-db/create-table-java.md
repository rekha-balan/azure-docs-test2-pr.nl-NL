---
title: 'Quickstart: Table API with Java - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Table API to create an application with the Azure portal and Java
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.custom: quick start connect, mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 04/10/2018
ms.author: sngun
ms.openlocfilehash: 349fe9eafc169d232c4434a2c536d2020d4ea76a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857970"
---
# <a name="quickstart-build-a-table-api-app-with-java-and-azure-cosmos-db"></a><span data-ttu-id="22eb4-103">Quickstart: Build a Table API app with Java and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22eb4-103">Quickstart: Build a Table API app with Java and Azure Cosmos DB</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-table-dotnet.md)
> * [Java](create-table-java.md)
> * [Node.js](create-table-nodejs.md)
> * [Python](create-table-python.md)
> 

<span data-ttu-id="22eb4-108">This quickstart shows how to use Java and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="22eb4-108">This quickstart shows how to use Java and the Azure Cosmos DB [Table API](table-introduction.md) to build an app by cloning an example from GitHub.</span></span> <span data-ttu-id="22eb4-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="22eb4-109">This quickstart also shows you how to create an Azure Cosmos DB account and how to use Data Explorer to create tables and entities in the web-based Azure portal.</span></span>

<span data-ttu-id="22eb4-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="22eb4-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="22eb4-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22eb4-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="22eb4-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="22eb4-112">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

<span data-ttu-id="22eb4-113">In addition:</span><span class="sxs-lookup"><span data-stu-id="22eb4-113">In addition:</span></span> 

* [<span data-ttu-id="22eb4-114">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="22eb4-114">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="22eb4-115">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="22eb4-115">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="22eb4-116">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="22eb4-116">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="22eb4-117">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span><span class="sxs-lookup"><span data-stu-id="22eb4-117">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="22eb4-118">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="22eb4-118">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="22eb4-119">Git</span><span class="sxs-lookup"><span data-stu-id="22eb4-119">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="22eb4-120">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="22eb4-120">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="22eb4-121">Create a database account</span><span class="sxs-lookup"><span data-stu-id="22eb4-121">Create a database account</span></span>

> [!IMPORTANT] 
> You need to create a new Table API account to work with the generally available Table API SDKs. Table API accounts created during preview are not supported by the generally available SDKs.
>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="22eb4-124">Add a table</span><span class="sxs-lookup"><span data-stu-id="22eb4-124">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="22eb4-125">Add sample data</span><span class="sxs-lookup"><span data-stu-id="22eb4-125">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-table-add-sample-data](../../includes/cosmos-db-create-table-add-sample-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="22eb4-126">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="22eb4-126">Clone the sample application</span></span>

<span data-ttu-id="22eb4-127">Now let's clone a Table app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="22eb4-127">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="22eb4-128">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="22eb4-128">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="22eb4-129">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="22eb4-129">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="22eb4-130">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="22eb4-130">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="22eb4-131">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="22eb4-131">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="22eb4-132">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="22eb4-132">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/storage-table-java-getting-started.git 
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="22eb4-133">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="22eb4-133">Update your connection string</span></span>

<span data-ttu-id="22eb4-134">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="22eb4-134">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="22eb4-135">This enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="22eb4-135">This enables your app to communicate with your hosted database.</span></span> 

1. <span data-ttu-id="22eb4-136">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="22eb4-136">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

   ![View and copy the required connection string information from the in the Connection String pane](./media/create-table-java/connection-string.png)

2. <span data-ttu-id="22eb4-138">Copy the PRIMARY CONNECTION STRING using the copy button on the right.</span><span class="sxs-lookup"><span data-stu-id="22eb4-138">Copy the PRIMARY CONNECTION STRING using the copy button on the right.</span></span>

3. <span data-ttu-id="22eb4-139">Open config.properties from the C:\git-samples\storage-table-java-getting-started\src\main\resources folder.</span><span class="sxs-lookup"><span data-stu-id="22eb4-139">Open config.properties from the C:\git-samples\storage-table-java-getting-started\src\main\resources folder.</span></span> 

5. <span data-ttu-id="22eb4-140">Comment out line one and uncomment line two.</span><span class="sxs-lookup"><span data-stu-id="22eb4-140">Comment out line one and uncomment line two.</span></span> <span data-ttu-id="22eb4-141">The first two lines should now look like this.</span><span class="sxs-lookup"><span data-stu-id="22eb4-141">The first two lines should now look like this.</span></span>

    ```
    #StorageConnectionString = UseDevelopmentStorage=true
    StorageConnectionString = DefaultEndpointsProtocol=https;AccountName=[ACCOUNTNAME];AccountKey=[ACCOUNTKEY]
    ```

6. <span data-ttu-id="22eb4-142">Paste your PRIMARY CONNECTION STRING from the portal into the StorageConnectionString value in line 2.</span><span class="sxs-lookup"><span data-stu-id="22eb4-142">Paste your PRIMARY CONNECTION STRING from the portal into the StorageConnectionString value in line 2.</span></span> 

    > [!IMPORTANT]
    > If your Endpoint uses documents.azure.com, that means you have a preview account, and you need to create a [new Table API account](#create-a-database-account) to work with the generally available Table API SDK.
    >

7. <span data-ttu-id="22eb4-144">Save the config.properties file.</span><span class="sxs-lookup"><span data-stu-id="22eb4-144">Save the config.properties file.</span></span>

<span data-ttu-id="22eb4-145">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22eb4-145">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-app"></a><span data-ttu-id="22eb4-146">Run the app</span><span class="sxs-lookup"><span data-stu-id="22eb4-146">Run the app</span></span>

1. <span data-ttu-id="22eb4-147">In the git terminal window, `cd` to the storage-table-java-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="22eb4-147">In the git terminal window, `cd` to the storage-table-java-getting-started folder.</span></span>

    ```git
    cd "C:\git-samples\storage-table-java-getting-started"
    ```

2. <span data-ttu-id="22eb4-148">In the git terminal window, run the following commands to run start the Java application.</span><span class="sxs-lookup"><span data-stu-id="22eb4-148">In the git terminal window, run the following commands to run start the Java application.</span></span>

    ```git
    mvn compile exec:java 
    ```

    <span data-ttu-id="22eb4-149">The console window displays the table data being added to the new table database in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22eb4-149">The console window displays the table data being added to the new table database in Azure Cosmos DB.</span></span>

    <span data-ttu-id="22eb4-150">You can now go back to Data Explorer and see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="22eb4-150">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="22eb4-151">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="22eb4-151">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="22eb4-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="22eb4-152">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="22eb4-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="22eb4-153">Next steps</span></span>

<span data-ttu-id="22eb4-154">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="22eb4-154">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="22eb4-155">Now you can query your data using the Table API.</span><span class="sxs-lookup"><span data-stu-id="22eb4-155">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [Import table data to the Table API](table-import.md)
