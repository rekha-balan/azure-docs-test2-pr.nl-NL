---
title: Build a .NET web app with Azure Cosmos DB using the SQL API | Microsoft Docs
description: In this quickstart, use the Azure Cosmos DB SQL API and the Azure portal to create a .NET web app
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.custom: quick start connect, mvc, devcenter
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 04/10/2018
ms.author: sngun
clicktale: true
ms.openlocfilehash: 672156d6c301fc26f8e4da5f78523f1fe30bac6f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867738"
---
# <a name="quickstart-build-a-net-web-app-with-azure-cosmos-db-using-the-sql-api-and-the-azure-portal"></a><span data-ttu-id="b9237-103">Quickstart: Build a .NET web app with Azure Cosmos DB using the SQL API and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b9237-103">Quickstart: Build a .NET web app with Azure Cosmos DB using the SQL API and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-sql-api-dotnet.md)
> * [Java](create-sql-api-java.md)
> * [Node.js](create-sql-api-nodejs.md)
> * [Node.js- v2](create-sql-api-nodejs-preview.md)
> * [Python](create-sql-api-python.md)
> * [Xamarin](create-sql-api-xamarin-dotnet.md)
>  
> 

<span data-ttu-id="b9237-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="b9237-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b9237-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b9237-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b9237-112">This quick start demonstrates how to create an Azure Cosmos DB [SQL API](sql-api-introduction.md) account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9237-112">This quick start demonstrates how to create an Azure Cosmos DB [SQL API](sql-api-introduction.md) account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="b9237-113">You'll then build and deploy a todo list web app built on the [SQL .NET API](sql-api-sdk-dotnet.md), as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="b9237-113">You'll then build and deploy a todo list web app built on the [SQL .NET API](sql-api-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Todo app with sample data](./media/create-sql-api-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="b9237-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9237-115">Prerequisites</span></span>

<span data-ttu-id="b9237-116">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b9237-116">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b9237-117">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="b9237-117">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]  

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="b9237-118">Create a database account</span><span class="sxs-lookup"><span data-stu-id="b9237-118">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="b9237-119">Add a collection</span><span class="sxs-lookup"><span data-stu-id="b9237-119">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="b9237-120">Add sample data</span><span class="sxs-lookup"><span data-stu-id="b9237-120">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-add-sample-data](../../includes/cosmos-db-create-sql-api-add-sample-data.md)]

## <a name="query-your-data"></a><span data-ttu-id="b9237-121">Query your data</span><span class="sxs-lookup"><span data-stu-id="b9237-121">Query your data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-query-data](../../includes/cosmos-db-create-sql-api-query-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="b9237-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="b9237-122">Clone the sample application</span></span>

<span data-ttu-id="b9237-123">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="b9237-123">Now let's switch to working with code.</span></span> <span data-ttu-id="b9237-124">Let's clone a [SQL API app from GitHub](https://github.com/Azure-Samples/documentdb-dotnet-todo-app), set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="b9237-124">Let's clone a [SQL API app from GitHub](https://github.com/Azure-Samples/documentdb-dotnet-todo-app), set the connection string, and run it.</span></span> <span data-ttu-id="b9237-125">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="b9237-125">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="b9237-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="b9237-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="b9237-127">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="b9237-127">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="b9237-128">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="b9237-128">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="b9237-129">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="b9237-129">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

4. <span data-ttu-id="b9237-130">Then open the todo solution file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9237-130">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="b9237-131">Review the code</span><span class="sxs-lookup"><span data-stu-id="b9237-131">Review the code</span></span>

<span data-ttu-id="b9237-132">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="b9237-132">This step is optional.</span></span> <span data-ttu-id="b9237-133">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="b9237-133">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="b9237-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="b9237-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="b9237-135">The following snippets are all taken from the DocumentDBRepository.cs file.</span><span class="sxs-lookup"><span data-stu-id="b9237-135">The following snippets are all taken from the DocumentDBRepository.cs file.</span></span>

* <span data-ttu-id="b9237-136">The DocumentClient is initialized on line 76.</span><span class="sxs-lookup"><span data-stu-id="b9237-136">The DocumentClient is initialized on line 76.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
    ```

* <span data-ttu-id="b9237-137">A new database is created on line 91.</span><span class="sxs-lookup"><span data-stu-id="b9237-137">A new database is created on line 91.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="b9237-138">A new collection is created on line 110.</span><span class="sxs-lookup"><span data-stu-id="b9237-138">A new collection is created on line 110.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection
            {
               Id = CollectionId
            },
        new RequestOptions { OfferThroughput = 400 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b9237-139">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="b9237-139">Update your connection string</span></span>

<span data-ttu-id="b9237-140">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="b9237-140">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="b9237-141">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span><span class="sxs-lookup"><span data-stu-id="b9237-141">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b9237-142">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span><span class="sxs-lookup"><span data-stu-id="b9237-142">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![View and copy an access key in the Azure portal, Keys blade](./media/create-sql-api-dotnet/keys.png)

2. <span data-ttu-id="b9237-144">In Visual Studio 2017, open the web.config file.</span><span class="sxs-lookup"><span data-stu-id="b9237-144">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="b9237-145">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span><span class="sxs-lookup"><span data-stu-id="b9237-145">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="b9237-146">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config.</span><span class="sxs-lookup"><span data-stu-id="b9237-146">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
5. <span data-ttu-id="b9237-147">Then update the database value to match the name of the database you have created earlier.</span><span class="sxs-lookup"><span data-stu-id="b9237-147">Then update the database value to match the name of the database you have created earlier.</span></span> <span data-ttu-id="b9237-148">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b9237-148">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="database" value="Tasks" />`    
    
## <a name="run-the-web-app"></a><span data-ttu-id="b9237-149">Run the web app</span><span class="sxs-lookup"><span data-stu-id="b9237-149">Run the web app</span></span>
1. <span data-ttu-id="b9237-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="b9237-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="b9237-151">In the NuGet **Browse** box, type *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="b9237-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="b9237-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span><span class="sxs-lookup"><span data-stu-id="b9237-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="b9237-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span><span class="sxs-lookup"><span data-stu-id="b9237-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="b9237-154">Click CTRL + F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="b9237-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="b9237-155">Your app displays in your browser.</span><span class="sxs-lookup"><span data-stu-id="b9237-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="b9237-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span><span class="sxs-lookup"><span data-stu-id="b9237-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Todo app with sample data](./media/create-sql-api-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="b9237-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="b9237-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="b9237-159">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b9237-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b9237-160">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b9237-160">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="b9237-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9237-161">Next steps</span></span>

<span data-ttu-id="b9237-162">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span><span class="sxs-lookup"><span data-stu-id="b9237-162">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="b9237-163">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="b9237-163">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md)


