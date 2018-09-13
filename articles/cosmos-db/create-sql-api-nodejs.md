---
title: 'Azure Cosmos DB: Build an app with Node.js and the SQL API | Microsoft Docs'
description: Presents a Node.js code sample you can use to connect to and query the Azure Cosmos DB SQL API
services: cosmos-db
author: deborahc
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.custom: quick start connect, mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 04/10/2018
ms.author: dech
ms.openlocfilehash: f5130a1ec1817448285d9995fa2d769178629114
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857140"
---
# <a name="azure-cosmos-db-build-a-sql-api-app-with-nodejs-and-the-azure-portal"></a><span data-ttu-id="f1888-103">Azure Cosmos DB: Build a SQL API app with Node.js and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f1888-103">Azure Cosmos DB: Build a SQL API app with Node.js and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-sql-api-dotnet.md)
> * [Java](create-sql-api-java.md)
> * [Node.js](create-sql-api-nodejs.md)
> * [Node.js- v2](create-sql-api-nodejs-preview.md)
> * [Python](create-sql-api-python.md)
> * [Xamarin](create-sql-api-xamarin-dotnet.md)
>  

<span data-ttu-id="f1888-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="f1888-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="f1888-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1888-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f1888-112">This quick start demonstrates how to create an Azure Cosmos DB [SQL API](sql-api-introduction.md) account, document database, and collection using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f1888-112">This quick start demonstrates how to create an Azure Cosmos DB [SQL API](sql-api-introduction.md) account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="f1888-113">You then build and run a console app built on the [SQL Node.js API](sql-api-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="f1888-113">You then build and run a console app built on the [SQL Node.js API](sql-api-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1888-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f1888-114">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="f1888-115">In addition:</span><span class="sxs-lookup"><span data-stu-id="f1888-115">In addition:</span></span>
    * <span data-ttu-id="f1888-116">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span><span class="sxs-lookup"><span data-stu-id="f1888-116">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="f1888-117">Git</span><span class="sxs-lookup"><span data-stu-id="f1888-117">Git</span></span>](http://git-scm.com/)

## <a name="create-a-database-account"></a><span data-ttu-id="f1888-118">Create a database account</span><span class="sxs-lookup"><span data-stu-id="f1888-118">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="f1888-119">Add a collection</span><span class="sxs-lookup"><span data-stu-id="f1888-119">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="add-sample-data"></a><span data-ttu-id="f1888-120">Add sample data</span><span class="sxs-lookup"><span data-stu-id="f1888-120">Add sample data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-add-sample-data](../../includes/cosmos-db-create-sql-api-add-sample-data.md)]

## <a name="query-your-data"></a><span data-ttu-id="f1888-121">Query your data</span><span class="sxs-lookup"><span data-stu-id="f1888-121">Query your data</span></span>

[!INCLUDE [cosmos-db-create-sql-api-query-data](../../includes/cosmos-db-create-sql-api-query-data.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="f1888-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="f1888-122">Clone the sample application</span></span>

<span data-ttu-id="f1888-123">Now let's clone a SQL API app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="f1888-123">Now let's clone a SQL API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="f1888-124">You see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="f1888-124">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="f1888-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="f1888-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="f1888-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="f1888-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="f1888-127">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="f1888-127">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="f1888-128">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="f1888-128">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="f1888-129">Review the code</span><span class="sxs-lookup"><span data-stu-id="f1888-129">Review the code</span></span>

<span data-ttu-id="f1888-130">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="f1888-130">This step is optional.</span></span> <span data-ttu-id="f1888-131">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="f1888-131">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="f1888-132">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="f1888-132">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="f1888-133">The following snippets are all taken from the app.js file.</span><span class="sxs-lookup"><span data-stu-id="f1888-133">The following snippets are all taken from the app.js file.</span></span>

* <span data-ttu-id="f1888-134">The `documentClient` is initialized.</span><span class="sxs-lookup"><span data-stu-id="f1888-134">The `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="f1888-135">A new database is created.</span><span class="sxs-lookup"><span data-stu-id="f1888-135">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="f1888-136">A new collection is created.</span><span class="sxs-lookup"><span data-stu-id="f1888-136">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="f1888-137">Some documents are created.</span><span class="sxs-lookup"><span data-stu-id="f1888-137">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="f1888-138">A SQL query over JSON is performed.</span><span class="sxs-lookup"><span data-stu-id="f1888-138">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="f1888-139">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="f1888-139">Update your connection string</span></span>

<span data-ttu-id="f1888-140">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="f1888-140">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="f1888-141">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span><span class="sxs-lookup"><span data-stu-id="f1888-141">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="f1888-142">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span><span class="sxs-lookup"><span data-stu-id="f1888-142">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span></span>

    ![View and copy an access key in the Azure portal, Keys blade](./media/create-sql-api-dotnet/keys.png)

2. <span data-ttu-id="f1888-144">In Open the `config.js` file.</span><span class="sxs-lookup"><span data-stu-id="f1888-144">In Open the `config.js` file.</span></span> 

3. <span data-ttu-id="f1888-145">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="f1888-145">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="f1888-146">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="f1888-146">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="f1888-147">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1888-147">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="f1888-148">Run the app</span><span class="sxs-lookup"><span data-stu-id="f1888-148">Run the app</span></span>
1. <span data-ttu-id="f1888-149">Run `npm install` in a terminal to install required npm modules</span><span class="sxs-lookup"><span data-stu-id="f1888-149">Run `npm install` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="f1888-150">Run `node app.js` in a terminal to start your node application.</span><span class="sxs-lookup"><span data-stu-id="f1888-150">Run `node app.js` in a terminal to start your node application.</span></span>

<span data-ttu-id="f1888-151">You can now go back to Data Explorer and see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="f1888-151">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="f1888-152">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f1888-152">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="f1888-153">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f1888-153">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="f1888-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1888-154">Next steps</span></span>

<span data-ttu-id="f1888-155">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="f1888-155">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="f1888-156">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="f1888-156">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md)


