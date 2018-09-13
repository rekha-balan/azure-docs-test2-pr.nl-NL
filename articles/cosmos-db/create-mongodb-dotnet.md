---
title: 'Azure Cosmos DB: Build a web app with .NET and the MongoDB API | Microsoft Docs'
description: Presents a .NET code sample you can use to connect to and query the Azure Cosmos DB MongoDB API
services: cosmos-db
author: slyons
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: quick start connect, mvc
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 05/22/2018
ms.author: sclyon
ms.openlocfilehash: 7ab02cf2cc9a25a5c4c7aa6d782d37d932dc8369
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857881"
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="70b00-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="70b00-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-mongodb-dotnet.md)
> * [Java](create-mongodb-java.md)
> * [Node.js](create-mongodb-nodejs.md)
> * [Python](create-mongodb-flask.md)
> * [Xamarin](create-mongodb-xamarin.md)
> * [Golang](create-mongodb-golang.md)
>  

<span data-ttu-id="70b00-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="70b00-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="70b00-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="70b00-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="70b00-112">This quickstart demonstrates how to create an Azure Cosmos DB [MongoDB API](mongodb-introduction.md) account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="70b00-112">This quickstart demonstrates how to create an Azure Cosmos DB [MongoDB API](mongodb-introduction.md) account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="70b00-113">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="70b00-113">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span>

## <a name="prerequisites-to-run-the-sample-app"></a><span data-ttu-id="70b00-114">Prerequisites to run the sample app</span><span class="sxs-lookup"><span data-stu-id="70b00-114">Prerequisites to run the sample app</span></span>

<span data-ttu-id="70b00-115">To run the sample, you'll need [Visual Studio](https://www.visualstudio.com/downloads/) and a valid Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="70b00-115">To run the sample, you'll need [Visual Studio](https://www.visualstudio.com/downloads/) and a valid Azure CosmosDB account.</span></span>

<span data-ttu-id="70b00-116">If you don't already have Visual Studio, download [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload installed with setup.</span><span class="sxs-lookup"><span data-stu-id="70b00-116">If you don't already have Visual Studio, download [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload installed with setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="70b00-117">Create a database account</span><span class="sxs-lookup"><span data-stu-id="70b00-117">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

<span data-ttu-id="70b00-118">The sample described in this article is compatible with MongoDB.Driver version 2.6.1.</span><span class="sxs-lookup"><span data-stu-id="70b00-118">The sample described in this article is compatible with MongoDB.Driver version 2.6.1.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="70b00-119">Clone the sample app</span><span class="sxs-lookup"><span data-stu-id="70b00-119">Clone the sample app</span></span>

<span data-ttu-id="70b00-120">First, download the sample MongoDB API app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="70b00-120">First, download the sample MongoDB API app from GitHub.</span></span> <span data-ttu-id="70b00-121">It implements a task list with MongoDB's document storage model.</span><span class="sxs-lookup"><span data-stu-id="70b00-121">It implements a task list with MongoDB's document storage model.</span></span>

1. <span data-ttu-id="70b00-122">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="70b00-122">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="70b00-123">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="70b00-123">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="70b00-124">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="70b00-124">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="70b00-125">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="70b00-125">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

<span data-ttu-id="70b00-126">If you don't wish to use git, you can also [download the project as a ZIP file](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="70b00-126">If you don't wish to use git, you can also [download the project as a ZIP file](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started/archive/master.zip).</span></span>

## <a name="review-the-code"></a><span data-ttu-id="70b00-127">Review the code</span><span class="sxs-lookup"><span data-stu-id="70b00-127">Review the code</span></span>

<span data-ttu-id="70b00-128">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="70b00-128">This step is optional.</span></span> <span data-ttu-id="70b00-129">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="70b00-129">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="70b00-130">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="70b00-130">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="70b00-131">The following snippets are all taken from the Dal.cs file in the DAL directory.</span><span class="sxs-lookup"><span data-stu-id="70b00-131">The following snippets are all taken from the Dal.cs file in the DAL directory.</span></span>

* <span data-ttu-id="70b00-132">Initialize the Mongo Client.</span><span class="sxs-lookup"><span data-stu-id="70b00-132">Initialize the Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credential = new MongoCredential("SCRAM-SHA-1", identity, evidence);

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="70b00-133">Retrieve the database and the collection.</span><span class="sxs-lookup"><span data-stu-id="70b00-133">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="70b00-134">Retrieve all documents.</span><span class="sxs-lookup"><span data-stu-id="70b00-134">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

* <span data-ttu-id="70b00-135">Creates a task and insert it into the MongoDB collection</span><span class="sxs-lookup"><span data-stu-id="70b00-135">Creates a task and insert it into the MongoDB collection</span></span>

   ```csharp
    public void CreateTask(MyTask task)
    {
        var collection = GetTasksCollectionForEdit();
        try
        {
            collection.InsertOne(task);
        }
        catch (MongoCommandException ex)
        {
            string msg = ex.Message;
        }
    }
   ```
   <span data-ttu-id="70b00-136">Similarly, you can update and delete documents by using the [collection.UpdateOne()](https://docs.mongodb.com/stitch/mongodb/actions/collection.updateOne/index.html) and [collection.DeleteOne()](https://docs.mongodb.com/stitch/mongodb/actions/collection.deleteOne/index.html) methods.</span><span class="sxs-lookup"><span data-stu-id="70b00-136">Similarly, you can update and delete documents by using the [collection.UpdateOne()](https://docs.mongodb.com/stitch/mongodb/actions/collection.updateOne/index.html) and [collection.DeleteOne()](https://docs.mongodb.com/stitch/mongodb/actions/collection.deleteOne/index.html) methods.</span></span> 

## <a name="update-your-connection-string"></a><span data-ttu-id="70b00-137">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="70b00-137">Update your connection string</span></span>

<span data-ttu-id="70b00-138">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="70b00-138">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="70b00-139">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span><span class="sxs-lookup"><span data-stu-id="70b00-139">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="70b00-140">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span><span class="sxs-lookup"><span data-stu-id="70b00-140">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="70b00-141">Open the **Dal.cs** file in the **DAL** directory.</span><span class="sxs-lookup"><span data-stu-id="70b00-141">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="70b00-142">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span><span class="sxs-lookup"><span data-stu-id="70b00-142">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="70b00-143">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span><span class="sxs-lookup"><span data-stu-id="70b00-143">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="70b00-144">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span><span class="sxs-lookup"><span data-stu-id="70b00-144">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="70b00-145">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="70b00-145">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="70b00-146">Run the web app</span><span class="sxs-lookup"><span data-stu-id="70b00-146">Run the web app</span></span>

1. <span data-ttu-id="70b00-147">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="70b00-147">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="70b00-148">In the NuGet **Browse** box, type *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="70b00-148">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="70b00-149">From the results, install the **MongoDB.Driver** library.</span><span class="sxs-lookup"><span data-stu-id="70b00-149">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="70b00-150">This installs the MongoDB.Driver package as well as all dependencies.</span><span class="sxs-lookup"><span data-stu-id="70b00-150">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="70b00-151">Click CTRL + F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="70b00-151">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="70b00-152">Your app displays in your browser.</span><span class="sxs-lookup"><span data-stu-id="70b00-152">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="70b00-153">Click **Create** in the browser and create a few new tasks in your task list app.</span><span class="sxs-lookup"><span data-stu-id="70b00-153">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="70b00-154">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="70b00-154">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="70b00-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="70b00-155">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="70b00-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="70b00-156">Next steps</span></span>

<span data-ttu-id="70b00-157">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="70b00-157">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="70b00-158">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="70b00-158">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB for the MongoDB API](mongodb-migrate.md)

