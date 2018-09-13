---
title: 'Azure Cosmos DB: Build a todo app with Xamarin | Microsoft Docs'
description: Presents a Xamarin code sample you can use to connect to and query Azure Cosmos DB
services: cosmos-db
author: codemillmatt
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.custom: quick start connect, mvc
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 05/30/2018
ms.author: masoucou
ms.openlocfilehash: 36236f8f8a7122369f5888ef21d8f69b719b45aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965629"
---
# <a name="azure-cosmos-db-build-a-todo-app-with-xamarin"></a><span data-ttu-id="1b584-103">Azure Cosmos DB: Build a todo app with Xamarin</span><span class="sxs-lookup"><span data-stu-id="1b584-103">Azure Cosmos DB: Build a todo app with Xamarin</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-sql-api-dotnet.md)
> * [Java](create-sql-api-java.md)
> * [Node.js](create-sql-api-nodejs.md)
> * [Node.js- v2](create-sql-api-nodejs-preview.md)
> * [Python](create-sql-api-python.md)
> * [Xamarin](create-sql-api-xamarin-dotnet.md)
>  

<span data-ttu-id="1b584-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="1b584-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1b584-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b584-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

> [!NOTE]
> Sample code for an entire canonical sample Xamarin app showcasing multiple Azure offerings, including CosmosDB, can be found on GitHub [here](https://github.com/xamarinhq/app-geocontacts). This app demonstrates viewing geographically dispersed contacts, and allowing those contacts to update their location.

<span data-ttu-id="1b584-114">This quickstart demonstrates how to create an Azure Cosmos DB SQL API account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b584-114">This quickstart demonstrates how to create an Azure Cosmos DB SQL API account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="1b584-115">You'll then build and deploy a todo list web app built on the [SQL .NET API](sql-api-sdk-dotnet.md) and [Xamarin](https://docs.microsoft.com/xamarin/#pivot=platforms&panel=Cross-Platform) utilizing [Xamarin.Forms](https://docs.microsoft.com/xamarin/#pivot=platforms&panel=XamarinForms) and the [MVVM architectural pattern](https://docs.microsoft.com/xamarin/xamarin-forms/xaml/xaml-basics/data-bindings-to-mvvm).</span><span class="sxs-lookup"><span data-stu-id="1b584-115">You'll then build and deploy a todo list web app built on the [SQL .NET API](sql-api-sdk-dotnet.md) and [Xamarin](https://docs.microsoft.com/xamarin/#pivot=platforms&panel=Cross-Platform) utilizing [Xamarin.Forms](https://docs.microsoft.com/xamarin/#pivot=platforms&panel=XamarinForms) and the [MVVM architectural pattern](https://docs.microsoft.com/xamarin/xamarin-forms/xaml/xaml-basics/data-bindings-to-mvvm).</span></span>

![Xamarin todo app running on iOS](./media/create-sql-api-xamarin-dotnet/ios-todo-screen.png)

## <a name="prerequisites"></a><span data-ttu-id="1b584-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b584-117">Prerequisites</span></span>

<span data-ttu-id="1b584-118">If you are developing on Windows and don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1b584-118">If you are developing on Windows and don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="1b584-119">Make sure that you enable **Azure development** and **Mobile Development with .NET** workloads during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="1b584-119">Make sure that you enable **Azure development** and **Mobile Development with .NET** workloads during the Visual Studio setup.</span></span>

<span data-ttu-id="1b584-120">If you are using a Mac, you can download the **free** [Visual Studio for Mac](https://www.visualstudio.com/vs/mac/).</span><span class="sxs-lookup"><span data-stu-id="1b584-120">If you are using a Mac, you can download the **free** [Visual Studio for Mac](https://www.visualstudio.com/vs/mac/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="1b584-121">Create a database account</span><span class="sxs-lookup"><span data-stu-id="1b584-121">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="1b584-122">Add a collection</span><span class="sxs-lookup"><span data-stu-id="1b584-122">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="add-sample-data"></a><span data-ttu-id="1b584-123">Add sample data</span><span class="sxs-lookup"><span data-stu-id="1b584-123">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-add-sample-data](../../includes/cosmos-db-create-sql-api-add-sample-data.md)]

## <a name="query-your-data"></a><span data-ttu-id="1b584-124">Query your data</span><span class="sxs-lookup"><span data-stu-id="1b584-124">Query your data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-query-data](../../includes/cosmos-db-create-sql-api-query-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="1b584-125">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="1b584-125">Clone the sample application</span></span>

<span data-ttu-id="1b584-126">Now let's clone the Xamarin SQL API app from github, review the code, obtain the API keys, and run it.</span><span class="sxs-lookup"><span data-stu-id="1b584-126">Now let's clone the Xamarin SQL API app from github, review the code, obtain the API keys, and run it.</span></span> <span data-ttu-id="1b584-127">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="1b584-127">You'll see how easy it is to work with data programmatically.</span></span>

1. <span data-ttu-id="1b584-128">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="1b584-128">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="1b584-129">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="1b584-129">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="1b584-130">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="1b584-130">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="1b584-131">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="1b584-131">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-sql-xamarin-getting-started.git
    ```

4. <span data-ttu-id="1b584-132">Then open the ToDoItems.sln file from the samples/xamarin/ToDoItems folder in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b584-132">Then open the ToDoItems.sln file from the samples/xamarin/ToDoItems folder in Visual Studio.</span></span>

## <a name="obtain-your-api-keys"></a><span data-ttu-id="1b584-133">Obtain your API keys</span><span class="sxs-lookup"><span data-stu-id="1b584-133">Obtain your API keys</span></span>

<span data-ttu-id="1b584-134">Go back to the Azure portal to get your API key information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="1b584-134">Go back to the Azure portal to get your API key information and copy it into the app.</span></span>

1. <span data-ttu-id="1b584-135">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB SQL API account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span><span class="sxs-lookup"><span data-stu-id="1b584-135">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB SQL API account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="1b584-136">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the APIKeys.cs file in the next step.</span><span class="sxs-lookup"><span data-stu-id="1b584-136">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the APIKeys.cs file in the next step.</span></span>

    ![View and copy an access key in the Azure portal, Keys blade](./media/create-sql-api-xamarin-dotnet/keys.png)

2. <span data-ttu-id="1b584-138">In either Visual Studio 2017 or Visual Studio for Mac, open the APIKeys.cs file in the azure-documentdb-dotnet/samples/xamarin/ToDoItems/ToDoItems.Core/Helpers folder.</span><span class="sxs-lookup"><span data-stu-id="1b584-138">In either Visual Studio 2017 or Visual Studio for Mac, open the APIKeys.cs file in the azure-documentdb-dotnet/samples/xamarin/ToDoItems/ToDoItems.Core/Helpers folder.</span></span>

3. <span data-ttu-id="1b584-139">Copy your URI value from the portal (using the copy button) and make it the value of the `CosmosEndpointUrl` variable in APIKeys.cs.</span><span class="sxs-lookup"><span data-stu-id="1b584-139">Copy your URI value from the portal (using the copy button) and make it the value of the `CosmosEndpointUrl` variable in APIKeys.cs.</span></span>

    `public static readonly string CosmosEndpointUrl = "{Azure Cosmos DB account URL}";`

4. <span data-ttu-id="1b584-140">Then copy your PRIMARY KEY value from the portal and make it the value of the `Cosmos Auth Key` in APIKeys.cs.</span><span class="sxs-lookup"><span data-stu-id="1b584-140">Then copy your PRIMARY KEY value from the portal and make it the value of the `Cosmos Auth Key` in APIKeys.cs.</span></span>

    `public static readonly string CosmosAuthKey = "{Azure Cosmos DB secret}";`

[!INCLUDE [cosmos-db-auth-key-info](../../includes/cosmos-db-auth-key-info.md)]

## <a name="review-the-code"></a><span data-ttu-id="1b584-141">Review the code</span><span class="sxs-lookup"><span data-stu-id="1b584-141">Review the code</span></span>

<span data-ttu-id="1b584-142">This solution demonstrates how to create a ToDo app using the Azure Cosmos DB SQL API and Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="1b584-142">This solution demonstrates how to create a ToDo app using the Azure Cosmos DB SQL API and Xamarin.Forms.</span></span> <span data-ttu-id="1b584-143">The app has two tabs, the first tab contains a list view showing todo items that are not yet complete.</span><span class="sxs-lookup"><span data-stu-id="1b584-143">The app has two tabs, the first tab contains a list view showing todo items that are not yet complete.</span></span> <span data-ttu-id="1b584-144">The second tab displays todo items that have been completed.</span><span class="sxs-lookup"><span data-stu-id="1b584-144">The second tab displays todo items that have been completed.</span></span> <span data-ttu-id="1b584-145">In addition to viewing not completed todo items in the first tab, you can also add new todo items, edit existing ones, and mark items as completed.</span><span class="sxs-lookup"><span data-stu-id="1b584-145">In addition to viewing not completed todo items in the first tab, you can also add new todo items, edit existing ones, and mark items as completed.</span></span>

![Copy in json data and click Save in Data Explorer in the Azure portal](./media/create-sql-api-xamarin-dotnet/android-todo-screen.png)

<span data-ttu-id="1b584-147">The code in the ToDoItems solution contains:</span><span class="sxs-lookup"><span data-stu-id="1b584-147">The code in the ToDoItems solution contains:</span></span>

* <span data-ttu-id="1b584-148">ToDoItems.Core: This is a .NET Standard project holding a Xamarin.Forms project and shared application logic code that maintains todo items within Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b584-148">ToDoItems.Core: This is a .NET Standard project holding a Xamarin.Forms project and shared application logic code that maintains todo items within Azure Cosmos DB.</span></span>
* <span data-ttu-id="1b584-149">ToDoItems.Android: This project contains the Android app.</span><span class="sxs-lookup"><span data-stu-id="1b584-149">ToDoItems.Android: This project contains the Android app.</span></span>
* <span data-ttu-id="1b584-150">ToDoItems.iOS: This project contains the iOS app.</span><span class="sxs-lookup"><span data-stu-id="1b584-150">ToDoItems.iOS: This project contains the iOS app.</span></span>

<span data-ttu-id="1b584-151">Now let's take a quick review of how the app communicates with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b584-151">Now let's take a quick review of how the app communicates with Azure Cosmos DB.</span></span>

* <span data-ttu-id="1b584-152">The [Microsoft.Azure.DocumentDb.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/) NuGet package is required to be added to all projects.</span><span class="sxs-lookup"><span data-stu-id="1b584-152">The [Microsoft.Azure.DocumentDb.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/) NuGet package is required to be added to all projects.</span></span>
* <span data-ttu-id="1b584-153">The `ToDoItem` class in the azure-documentdb-dotnet/samples/xamarin/ToDoItems/ToDoItems.Core/Models folder models the documents in the **Items** collection created above.</span><span class="sxs-lookup"><span data-stu-id="1b584-153">The `ToDoItem` class in the azure-documentdb-dotnet/samples/xamarin/ToDoItems/ToDoItems.Core/Models folder models the documents in the **Items** collection created above.</span></span> <span data-ttu-id="1b584-154">Note that property naming is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="1b584-154">Note that property naming is case-sensitive.</span></span>
* <span data-ttu-id="1b584-155">The `CosmosDBService` class in the azure-documentdb-dotnet/samples/xamarin/ToDoItems/ToDoItems.Core/Services folder encapsulates the communication to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b584-155">The `CosmosDBService` class in the azure-documentdb-dotnet/samples/xamarin/ToDoItems/ToDoItems.Core/Services folder encapsulates the communication to Azure Cosmos DB.</span></span>
* <span data-ttu-id="1b584-156">Within the `CosmosDBService` class there is a `DocumentClient` type variable.</span><span class="sxs-lookup"><span data-stu-id="1b584-156">Within the `CosmosDBService` class there is a `DocumentClient` type variable.</span></span> <span data-ttu-id="1b584-157">The `DocumentClient` is used to configure and execute requests against the Azure Cosmos DB account, and is instantiated on line 31:</span><span class="sxs-lookup"><span data-stu-id="1b584-157">The `DocumentClient` is used to configure and execute requests against the Azure Cosmos DB account, and is instantiated on line 31:</span></span>

    ```csharp
    docClient = new DocumentClient(new Uri(APIKeys.CosmosEndpointUrl), APIKeys.CosmosAuthKey);
    ```

* <span data-ttu-id="1b584-158">When querying a collection for documents, the `DocumentClient.CreateDocumentQuery<T>` method is used, as seen here in the `CosmosDBService.GetToDoItems` function:</span><span class="sxs-lookup"><span data-stu-id="1b584-158">When querying a collection for documents, the `DocumentClient.CreateDocumentQuery<T>` method is used, as seen here in the `CosmosDBService.GetToDoItems` function:</span></span>

    ```csharp
    public async static Task<List<ToDoItem>> GetToDoItems()
    {
        var todos = new List<ToDoItem>();

        var todoQuery = docClient.CreateDocumentQuery<ToDoItem>(
                                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                                .Where(todo => todo.Completed == false)
                                .AsDocumentQuery();

        while (todoQuery.HasMoreResults)
        {
            var queryResults = await todoQuery.ExecuteNextAsync<ToDoItem>();

            todos.AddRange(queryResults);
        }

        return todos;
    }
    ```

    <span data-ttu-id="1b584-159">The `CreateDocumentQuery<T>` takes a URI that points to the collection created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="1b584-159">The `CreateDocumentQuery<T>` takes a URI that points to the collection created in the previous section.</span></span> <span data-ttu-id="1b584-160">And you are also able to specify LINQ operators such as a `Where` clause.</span><span class="sxs-lookup"><span data-stu-id="1b584-160">And you are also able to specify LINQ operators such as a `Where` clause.</span></span> <span data-ttu-id="1b584-161">In this case only todo items that are not completed are returned.</span><span class="sxs-lookup"><span data-stu-id="1b584-161">In this case only todo items that are not completed are returned.</span></span>

    <span data-ttu-id="1b584-162">The `CreateDocumentQuery<T>` function is executed synchronously, and returns an `IQueryable<T>`.</span><span class="sxs-lookup"><span data-stu-id="1b584-162">The `CreateDocumentQuery<T>` function is executed synchronously, and returns an `IQueryable<T>`.</span></span> <span data-ttu-id="1b584-163">However, the `AsDocumentQuery` method converts the `IQueryable<T>` to an `IDocumentQuery<T>` object which can be executed asynchronously.</span><span class="sxs-lookup"><span data-stu-id="1b584-163">However, the `AsDocumentQuery` method converts the `IQueryable<T>` to an `IDocumentQuery<T>` object which can be executed asynchronously.</span></span> <span data-ttu-id="1b584-164">Thus not blocking the UI thread for mobile applications.</span><span class="sxs-lookup"><span data-stu-id="1b584-164">Thus not blocking the UI thread for mobile applications.</span></span>

    <span data-ttu-id="1b584-165">The `IDocumentQuery<T>.ExecuteNextAsync<T>` function retrieves the page of results from Azure Cosmos DB, which `HasMoreResults` checking to see if additional results remain to be returned.</span><span class="sxs-lookup"><span data-stu-id="1b584-165">The `IDocumentQuery<T>.ExecuteNextAsync<T>` function retrieves the page of results from Azure Cosmos DB, which `HasMoreResults` checking to see if additional results remain to be returned.</span></span>

> [!TIP]
> Several functions that operate on Azure Cosmos DB collections and documents take an URI as a parameter which specifies the address of the collection or document. This URI is constructed using the `URIFactory` class. URIs for databases, collections, and documents can all be created with this class.

* <span data-ttu-id="1b584-169">The `ComsmosDBService.InsertToDoItem` function on line 107 demonstrates how to insert a new document:</span><span class="sxs-lookup"><span data-stu-id="1b584-169">The `ComsmosDBService.InsertToDoItem` function on line 107 demonstrates how to insert a new document:</span></span>

    ```csharp
    public async static Task InsertToDoItem(ToDoItem item)
    {
        ...
        await docClient.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), item);
        ...
    }
    ```

    <span data-ttu-id="1b584-170">The document collection URI is specified as well as the item to be inserted.</span><span class="sxs-lookup"><span data-stu-id="1b584-170">The document collection URI is specified as well as the item to be inserted.</span></span>

* <span data-ttu-id="1b584-171">The `CosmosDBService.UpdateToDoItem` function on line 124 demonstrates how to replace an existing document with a new one:</span><span class="sxs-lookup"><span data-stu-id="1b584-171">The `CosmosDBService.UpdateToDoItem` function on line 124 demonstrates how to replace an existing document with a new one:</span></span>

    ```csharp
    public async static Task UpdateToDoItem(ToDoItem item)
    {
        ...
        var docUri = UriFactory.CreateDocumentUri(databaseName, collectionName, item.Id);

        await docClient.ReplaceDocumentAsync(docUri, item);
    }
    ```

    <span data-ttu-id="1b584-172">Here a new URI is needed to uniquely identify the document to replace and is obtained by using `UriFactory.CreateDocumentUri` and passing it the database and collection names and the id of the document.</span><span class="sxs-lookup"><span data-stu-id="1b584-172">Here a new URI is needed to uniquely identify the document to replace and is obtained by using `UriFactory.CreateDocumentUri` and passing it the database and collection names and the id of the document.</span></span>

    <span data-ttu-id="1b584-173">The `DocumentClient.ReplaceDocumentAsync` replaces the document identified by the URI with the one specified as a parameter.</span><span class="sxs-lookup"><span data-stu-id="1b584-173">The `DocumentClient.ReplaceDocumentAsync` replaces the document identified by the URI with the one specified as a parameter.</span></span>

* <span data-ttu-id="1b584-174">Deleting an item is demonstrated with the `CosmosDBService.DeleteToDoItem` function on line 115:</span><span class="sxs-lookup"><span data-stu-id="1b584-174">Deleting an item is demonstrated with the `CosmosDBService.DeleteToDoItem` function on line 115:</span></span>

    ```csharp
    public async static Task DeleteToDoItem(ToDoItem item)
    {
        ...
        var docUri = UriFactory.CreateDocumentUri(databaseName, collectionName, item.Id);

        await docClient.DeleteDocumentAsync(docUri);
    }
    ```

    <span data-ttu-id="1b584-175">Again note the unique doument URI being created and passed to the `DocumentClient.DeleteDocumentAsync` function.</span><span class="sxs-lookup"><span data-stu-id="1b584-175">Again note the unique doument URI being created and passed to the `DocumentClient.DeleteDocumentAsync` function.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="1b584-176">Run the app</span><span class="sxs-lookup"><span data-stu-id="1b584-176">Run the app</span></span>

<span data-ttu-id="1b584-177">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b584-177">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span>

<span data-ttu-id="1b584-178">The following steps will demonstrate how to run the app using the Visual Studio for Mac debugger.</span><span class="sxs-lookup"><span data-stu-id="1b584-178">The following steps will demonstrate how to run the app using the Visual Studio for Mac debugger.</span></span>

> [!NOTE]
> Usage of the Android version app is exactly the same, any differences will be called out in the steps below. If you wish to debug with Visual Studio on Windows, documentation todo so can be found for [iOS here](https://docs.microsoft.com/xamarin/ios/deploy-test/debugging-in-xamarin-ios?tabs=vswin) and [Android here](https://docs.microsoft.com/xamarin/android/deploy-test/debugging/).

1. <span data-ttu-id="1b584-181">First select the platform you wish to target by clicking on the dropdown highlighted and selecting either ToDoItems.iOS for iOS or ToDoItems.Android for Android.</span><span class="sxs-lookup"><span data-stu-id="1b584-181">First select the platform you wish to target by clicking on the dropdown highlighted and selecting either ToDoItems.iOS for iOS or ToDoItems.Android for Android.</span></span>

    ![Selecting a platform to debug in Visual Studio for Mac](./media/create-sql-api-xamarin-dotnet/ide-select-platform.png)

2. <span data-ttu-id="1b584-183">To start debugging the app, either press cmd+Enter or click the play button.</span><span class="sxs-lookup"><span data-stu-id="1b584-183">To start debugging the app, either press cmd+Enter or click the play button.</span></span>

    ![Starting to debug in Visual Studio for Mac](./media/create-sql-api-xamarin-dotnet/ide-start-debug.png)

3. <span data-ttu-id="1b584-185">When the iOS simulator or Android emulator finishes launching, the app will display 2 tabs at the bottom of the screen for iOS and the top of the screen for Android.</span><span class="sxs-lookup"><span data-stu-id="1b584-185">When the iOS simulator or Android emulator finishes launching, the app will display 2 tabs at the bottom of the screen for iOS and the top of the screen for Android.</span></span> <span data-ttu-id="1b584-186">The first shows todo items which are not completed, the second shows todo items which are completed.</span><span class="sxs-lookup"><span data-stu-id="1b584-186">The first shows todo items which are not completed, the second shows todo items which are completed.</span></span>

    ![Launch screen of ToDo app](./media/create-sql-api-xamarin-dotnet/ios-droid-started.png)

4. <span data-ttu-id="1b584-188">To complete a todo item on iOS, slide it to the left > tap on the **Complete** button.</span><span class="sxs-lookup"><span data-stu-id="1b584-188">To complete a todo item on iOS, slide it to the left > tap on the **Complete** button.</span></span> <span data-ttu-id="1b584-189">To complete a todo item on Android, long press the item > then tap on the complete button.</span><span class="sxs-lookup"><span data-stu-id="1b584-189">To complete a todo item on Android, long press the item > then tap on the complete button.</span></span>

    ![Complete a todo item](./media/create-sql-api-xamarin-dotnet/simulator-complete.png)

5. <span data-ttu-id="1b584-191">To edit a todo item > tap on the item > a new screen appears letting you enter new values.</span><span class="sxs-lookup"><span data-stu-id="1b584-191">To edit a todo item > tap on the item > a new screen appears letting you enter new values.</span></span> <span data-ttu-id="1b584-192">Tapping the save button will persist the changes to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b584-192">Tapping the save button will persist the changes to Azure Cosmos DB.</span></span>

    ![Edit todo item](./media/create-sql-api-xamarin-dotnet/simulator-edit.png)

6. <span data-ttu-id="1b584-194">To add a todo item > tap on the **Add** button on the upper right of the home screen > a new, blank, edit page will appear.</span><span class="sxs-lookup"><span data-stu-id="1b584-194">To add a todo item > tap on the **Add** button on the upper right of the home screen > a new, blank, edit page will appear.</span></span>

    ![Add todo item](./media/create-sql-api-xamarin-dotnet/simulator-add.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1b584-196">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1b584-196">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1b584-197">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1b584-197">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="1b584-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b584-198">Next steps</span></span>

<span data-ttu-id="1b584-199">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span><span class="sxs-lookup"><span data-stu-id="1b584-199">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="1b584-200">You can now import additional data to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="1b584-200">You can now import additional data to your Azure Cosmos DB account.</span></span>

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md)
