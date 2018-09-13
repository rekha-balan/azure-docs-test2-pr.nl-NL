---
title: 'Azure Cosmos DB: Build a Xamarin.Forms app with .NET and the MongoDB API | Microsoft Docs'
description: Presents a Xamarin code sample you can use to connect to and query the Azure Cosmos DB MongoDB API
services: cosmos-db
author: codemillmatt
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: quickstart, xamarin
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 06/20/2018
ms.author: masoucou
ms.openlocfilehash: 255f23906bc93ce78b28f4f0806d7076a97b0ef2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968795"
---
# <a name="quickstart-build-a-mongodb-api-xamarinforms-app-with-net-and-the-azure-portal"></a><span data-ttu-id="6770f-103">QuickStart: Build a MongoDB API Xamarin.Forms app with .NET and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6770f-103">QuickStart: Build a MongoDB API Xamarin.Forms app with .NET and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-mongodb-dotnet.md)
> * [Java](create-mongodb-java.md)
> * [Node.js](create-mongodb-nodejs.md)
> * [Python](create-mongodb-flask.md)
> * [Xamarin](create-mongodb-xamarin.md)
> * [Golang](create-mongodb-golang.md)
>  

<span data-ttu-id="6770f-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="6770f-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6770f-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6770f-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="6770f-112">This quickstart demonstrates how to create an Azure Cosmos DB [MongoDB API](mongodb-introduction.md) account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6770f-112">This quickstart demonstrates how to create an Azure Cosmos DB [MongoDB API](mongodb-introduction.md) account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="6770f-113">You'll then build a todo app Xamarin.Forms app by  using the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="6770f-113">You'll then build a todo app Xamarin.Forms app by  using the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span>

## <a name="prerequisites-to-run-the-sample-app"></a><span data-ttu-id="6770f-114">Prerequisites to run the sample app</span><span class="sxs-lookup"><span data-stu-id="6770f-114">Prerequisites to run the sample app</span></span>

<span data-ttu-id="6770f-115">To run the sample, you'll need [Visual Studio](https://www.visualstudio.com/downloads/) or [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) and a valid Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="6770f-115">To run the sample, you'll need [Visual Studio](https://www.visualstudio.com/downloads/) or [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) and a valid Azure CosmosDB account.</span></span>

<span data-ttu-id="6770f-116">If you don't already have Visual Studio, download [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) with the **Mobile development with .NET** workload installed with setup.</span><span class="sxs-lookup"><span data-stu-id="6770f-116">If you don't already have Visual Studio, download [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) with the **Mobile development with .NET** workload installed with setup.</span></span>

<span data-ttu-id="6770f-117">If you prefer to work on a Mac, download [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) and run the setup.</span><span class="sxs-lookup"><span data-stu-id="6770f-117">If you prefer to work on a Mac, download [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) and run the setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>

## <a name="create-a-database-account"></a><span data-ttu-id="6770f-118">Create a database account</span><span class="sxs-lookup"><span data-stu-id="6770f-118">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

<span data-ttu-id="6770f-119">The sample described in this article is compatible with MongoDB.Driver version 2.6.1.</span><span class="sxs-lookup"><span data-stu-id="6770f-119">The sample described in this article is compatible with MongoDB.Driver version 2.6.1.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="6770f-120">Clone the sample app</span><span class="sxs-lookup"><span data-stu-id="6770f-120">Clone the sample app</span></span>

<span data-ttu-id="6770f-121">First, download the sample MongoDB API app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="6770f-121">First, download the sample MongoDB API app from GitHub.</span></span> <span data-ttu-id="6770f-122">It implements a todo app with MongoDB's document storage model.</span><span class="sxs-lookup"><span data-stu-id="6770f-122">It implements a todo app with MongoDB's document storage model.</span></span>

1. <span data-ttu-id="6770f-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="6770f-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="6770f-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="6770f-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="6770f-125">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="6770f-125">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="6770f-126">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="6770f-126">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-xamarin-getting-started.git
    ```

<span data-ttu-id="6770f-127">If you don't wish to use git, you can also [download the project as a ZIP file](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-xamarin-getting-started/archive/master.zip)</span><span class="sxs-lookup"><span data-stu-id="6770f-127">If you don't wish to use git, you can also [download the project as a ZIP file](https://github.com/Azure-Samples/azure-cosmos-db-mongodb-xamarin-getting-started/archive/master.zip)</span></span>

## <a name="review-the-code"></a><span data-ttu-id="6770f-128">Review the code</span><span class="sxs-lookup"><span data-stu-id="6770f-128">Review the code</span></span>

<span data-ttu-id="6770f-129">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="6770f-129">This step is optional.</span></span> <span data-ttu-id="6770f-130">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="6770f-130">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="6770f-131">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="6770f-131">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span>

<span data-ttu-id="6770f-132">The following snippets are all taken from the `MongoService` class, found at the follwing path: src/TaskList.Core/Services/MongoService.cs.</span><span class="sxs-lookup"><span data-stu-id="6770f-132">The following snippets are all taken from the `MongoService` class, found at the follwing path: src/TaskList.Core/Services/MongoService.cs.</span></span>

* <span data-ttu-id="6770f-133">Initialize the Mongo Client.</span><span class="sxs-lookup"><span data-stu-id="6770f-133">Initialize the Mongo Client.</span></span>
    ```cs
    MongoClientSettings settings = MongoClientSettings.FromUrl(
        new MongoUrl(APIKeys.ConnectionString)
    );

    settings.SslSettings =
        new SslSettings() { EnabledSslProtocols = SslProtocols.Tls12 };

    MongoClient mongoClient = new MongoClient(settings);
    ```

* <span data-ttu-id="6770f-134">Retrieve a reference to the database and collection.</span><span class="sxs-lookup"><span data-stu-id="6770f-134">Retrieve a reference to the database and collection.</span></span> <span data-ttu-id="6770f-135">The MongoDB .NET SDK will automatically create both the database and collection if they do not already exist.</span><span class="sxs-lookup"><span data-stu-id="6770f-135">The MongoDB .NET SDK will automatically create both the database and collection if they do not already exist.</span></span>
    ```cs
    string dbName = "MyTasks";
    string collectionName = "TaskList";

    var db = mongoClient.GetDatabase(dbName);

    var collectionSettings = new MongoCollectionSettings {
        ReadPreference = ReadPreference.Nearest
    };

    tasksCollection = db.GetCollection<MyTask>(collectionName, collectionSettings);
    ```
* <span data-ttu-id="6770f-136">Retrieve all documents as a List.</span><span class="sxs-lookup"><span data-stu-id="6770f-136">Retrieve all documents as a List.</span></span>
    ```cs
    var allTasks = await TasksCollection
                    .Find(new BsonDocument())
                    .ToListAsync();
    ```

* <span data-ttu-id="6770f-137">Query for particular documents.</span><span class="sxs-lookup"><span data-stu-id="6770f-137">Query for particular documents.</span></span>
    ```cs
    public async Task<List<MyTask>> GetIncompleteTasksDueBefore(DateTime date)
    {
        var tasks = await TasksCollection
                        .AsQueryable()
                        .Where(t => t.Complete == false)
                        .Where(t => t.DueDate < date)
                        .ToListAsync();

        return tasks;
    }
    ```

* <span data-ttu-id="6770f-138">Create a task and insert it into the MongoDB collection.</span><span class="sxs-lookup"><span data-stu-id="6770f-138">Create a task and insert it into the MongoDB collection.</span></span>
    ```cs
    public async Task CreateTask(MyTask task)
    {
        await TasksCollection.InsertOneAsync(task);
    }
    ```

* <span data-ttu-id="6770f-139">Update a task in a MongoDB collection.</span><span class="sxs-lookup"><span data-stu-id="6770f-139">Update a task in a MongoDB collection.</span></span>
    ```cs
    public async Task UpdateTask(MyTask task)
    {
        await TasksCollection.ReplaceOneAsync(t => t.Id.Equals(task.Id), task);
    }
    ```

* <span data-ttu-id="6770f-140">Delete a task from a MongoDB collection.</span><span class="sxs-lookup"><span data-stu-id="6770f-140">Delete a task from a MongoDB collection.</span></span>
    ```cs
    public async Task DeleteTask(MyTask task)
    {
        await TasksCollection.DeleteOneAsync(t => t.Id.Equals(task.Id));
    }
    ```

<a id="update-your-connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="6770f-141">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="6770f-141">Update your connection string</span></span>

<span data-ttu-id="6770f-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="6770f-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="6770f-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span><span class="sxs-lookup"><span data-stu-id="6770f-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="6770f-144">You'll use the copy buttons on the right side of the screen to copy the Primary Connection String in the next steps.</span><span class="sxs-lookup"><span data-stu-id="6770f-144">You'll use the copy buttons on the right side of the screen to copy the Primary Connection String in the next steps.</span></span>

2. <span data-ttu-id="6770f-145">Open the **APIKeys.cs** file in the **Helpers** directory of the **TaskList.Core** project.</span><span class="sxs-lookup"><span data-stu-id="6770f-145">Open the **APIKeys.cs** file in the **Helpers** directory of the **TaskList.Core** project.</span></span>

3. <span data-ttu-id="6770f-146">Copy your **primary connection string** value from the portal (using the copy button) and make it the value of the **ConnectionString** field in your **APIKeys.cs** file.</span><span class="sxs-lookup"><span data-stu-id="6770f-146">Copy your **primary connection string** value from the portal (using the copy button) and make it the value of the **ConnectionString** field in your **APIKeys.cs** file.</span></span>

<span data-ttu-id="6770f-147">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6770f-147">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="6770f-148">Run the app</span><span class="sxs-lookup"><span data-stu-id="6770f-148">Run the app</span></span>

### <a name="visual-studio-2017"></a><span data-ttu-id="6770f-149">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6770f-149">Visual Studio 2017</span></span>

1. <span data-ttu-id="6770f-150">In Visual Studio, right-click on each project in **Solution Explorer** and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="6770f-150">In Visual Studio, right-click on each project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6770f-151">Click **Restore all NuGet packages**.</span><span class="sxs-lookup"><span data-stu-id="6770f-151">Click **Restore all NuGet packages**.</span></span>
3. <span data-ttu-id="6770f-152">Right click on the **TaskList.Android** and select **Set as startup project**.</span><span class="sxs-lookup"><span data-stu-id="6770f-152">Right click on the **TaskList.Android** and select **Set as startup project**.</span></span>
4. <span data-ttu-id="6770f-153">Press F5 to start debugging the application.</span><span class="sxs-lookup"><span data-stu-id="6770f-153">Press F5 to start debugging the application.</span></span>
5. <span data-ttu-id="6770f-154">If you want to run on iOS, first your machine is connected to a Mac (here are [instructions](https://docs.microsoft.com/en-us/xamarin/ios/get-started/installation/windows/introduction-to-xamarin-ios-for-visual-studio) on how to do so).</span><span class="sxs-lookup"><span data-stu-id="6770f-154">If you want to run on iOS, first your machine is connected to a Mac (here are [instructions](https://docs.microsoft.com/en-us/xamarin/ios/get-started/installation/windows/introduction-to-xamarin-ios-for-visual-studio) on how to do so).</span></span>
6. <span data-ttu-id="6770f-155">Right click on **TaskList.iOS** project and select **Set as startup project**.</span><span class="sxs-lookup"><span data-stu-id="6770f-155">Right click on **TaskList.iOS** project and select **Set as startup project**.</span></span>
7. <span data-ttu-id="6770f-156">Click F5 to start debugging the application.</span><span class="sxs-lookup"><span data-stu-id="6770f-156">Click F5 to start debugging the application.</span></span>

### <a name="visual-studio-for-mac"></a><span data-ttu-id="6770f-157">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="6770f-157">Visual Studio for Mac</span></span>

1. <span data-ttu-id="6770f-158">In the platform dropdown list, select either TaskList.iOS or TaskList.Android, depending which platform you want to run on.</span><span class="sxs-lookup"><span data-stu-id="6770f-158">In the platform dropdown list, select either TaskList.iOS or TaskList.Android, depending which platform you want to run on.</span></span>
2. <span data-ttu-id="6770f-159">Press cmd+Enter to start debugging the application.</span><span class="sxs-lookup"><span data-stu-id="6770f-159">Press cmd+Enter to start debugging the application.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="6770f-160">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6770f-160">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="6770f-161">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6770f-161">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="6770f-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="6770f-162">Next steps</span></span>

<span data-ttu-id="6770f-163">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Xamarin.Forms app using the API for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6770f-163">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Xamarin.Forms app using the API for MongoDB.</span></span> <span data-ttu-id="6770f-164">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6770f-164">You can now import additional data to your Cosmos DB account.</span></span>

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB for the MongoDB API](mongodb-migrate.md)