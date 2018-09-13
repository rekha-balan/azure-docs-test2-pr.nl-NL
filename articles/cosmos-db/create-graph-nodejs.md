---
title: Build an Azure Cosmos DB Node.js application by using Gremlin API | Microsoft Docs
description: Presents a Node.js code sample you can use to connect to and query Azure Cosmos DB
services: cosmos-db
author: luisbosquez
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.custom: quick start connect, mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lbosq
ms.openlocfilehash: 5f7e2a30ee4ea069e8c08187312f09e33a5a921a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868861"
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-gremlin-api"></a><span data-ttu-id="2a419-103">Azure Cosmos DB: Build a Node.js application by using Gremlin API</span><span class="sxs-lookup"><span data-stu-id="2a419-103">Azure Cosmos DB: Build a Node.js application by using Gremlin API</span></span>

> [!div class="op_single_selector"]
> * [Gremlin console](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

<span data-ttu-id="2a419-110">Azure Cosmos DB is the globally distributed multimodel database service from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2a419-110">Azure Cosmos DB is the globally distributed multimodel database service from Microsoft.</span></span> <span data-ttu-id="2a419-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2a419-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2a419-112">This quick start demonstrates how to create an Azure Cosmos DB [Gremlin API](graph-introduction.md) account, database, and graph using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2a419-112">This quick start demonstrates how to create an Azure Cosmos DB [Gremlin API](graph-introduction.md) account, database, and graph using the Azure portal.</span></span> <span data-ttu-id="2a419-113">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin) driver.</span><span class="sxs-lookup"><span data-stu-id="2a419-113">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin) driver.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a419-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2a419-114">Prerequisites</span></span>

<span data-ttu-id="2a419-115">Before you can run this sample, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="2a419-115">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="2a419-116">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span><span class="sxs-lookup"><span data-stu-id="2a419-116">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="2a419-117">Git</span><span class="sxs-lookup"><span data-stu-id="2a419-117">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="2a419-118">Create a database account</span><span class="sxs-lookup"><span data-stu-id="2a419-118">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="2a419-119">Add a graph</span><span class="sxs-lookup"><span data-stu-id="2a419-119">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="2a419-120">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="2a419-120">Clone the sample application</span></span>

<span data-ttu-id="2a419-121">Now let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="2a419-121">Now let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="2a419-122">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="2a419-122">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="2a419-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="2a419-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="2a419-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="2a419-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="2a419-125">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="2a419-125">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="2a419-126">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="2a419-126">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="2a419-127">Open the solution file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a419-127">Open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="2a419-128">Review the code</span><span class="sxs-lookup"><span data-stu-id="2a419-128">Review the code</span></span>

<span data-ttu-id="2a419-129">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="2a419-129">This step is optional.</span></span> <span data-ttu-id="2a419-130">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="2a419-130">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="2a419-131">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="2a419-131">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="2a419-132">The following snippets are all taken from the app.js file.</span><span class="sxs-lookup"><span data-stu-id="2a419-132">The following snippets are all taken from the app.js file.</span></span>

* <span data-ttu-id="2a419-133">The Gremlin client is created.</span><span class="sxs-lookup"><span data-stu-id="2a419-133">The Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="2a419-134">The configurations are all in `config.js`, which we edit in the [following section](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="2a419-134">The configurations are all in `config.js`, which we edit in the [following section](#update-your-connection-string).</span></span>

* <span data-ttu-id="2a419-135">A series of functions are defined to execute different Gremlin operations.</span><span class="sxs-lookup"><span data-stu-id="2a419-135">A series of functions are defined to execute different Gremlin operations.</span></span> <span data-ttu-id="2a419-136">This is one of them:</span><span class="sxs-lookup"><span data-stu-id="2a419-136">This is one of them:</span></span>

    ```nodejs
    function addVertex1(callback)
    {
        console.log('Running Add Vertex1'); 
        client.execute("g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44).property('userid', 1)", { }, (err, results) => {
          if (err) callback(console.error(err));
          console.log("Result: %s\n", JSON.stringify(results));
          callback(null)
        });
    }
    ```

* <span data-ttu-id="2a419-137">Each function executes a `client.execute` method with a Gremlin query string parameter.</span><span class="sxs-lookup"><span data-stu-id="2a419-137">Each function executes a `client.execute` method with a Gremlin query string parameter.</span></span> <span data-ttu-id="2a419-138">Here is an example of how `g.V().count()` is executed:</span><span class="sxs-lookup"><span data-stu-id="2a419-138">Here is an example of how `g.V().count()` is executed:</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

* <span data-ttu-id="2a419-139">At the end of the file, all methods are then invoked using the `async.waterfall()` method.</span><span class="sxs-lookup"><span data-stu-id="2a419-139">At the end of the file, all methods are then invoked using the `async.waterfall()` method.</span></span> <span data-ttu-id="2a419-140">This will execute them one after the other:</span><span class="sxs-lookup"><span data-stu-id="2a419-140">This will execute them one after the other:</span></span>

    ```nodejs
    try{
        async.waterfall([
            dropGraph,
            addVertex1,
            addVertex2,
            addEdge,
            countVertices
            ], finish);
    } catch(err) {
        console.log(err)
    }
    ```


## <a name="update-your-connection-string"></a><span data-ttu-id="2a419-141">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="2a419-141">Update your connection string</span></span>

1. <span data-ttu-id="2a419-142">Open the config.js file.</span><span class="sxs-lookup"><span data-stu-id="2a419-142">Open the config.js file.</span></span> 

2. <span data-ttu-id="2a419-143">In config.js, fill in the `config.endpoint` key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2a419-143">In config.js, fill in the `config.endpoint` key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![View and copy an access key in the Azure portal, Keys blade](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="2a419-145">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="2a419-145">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal.</span></span> <span data-ttu-id="2a419-146">Use the **URI** value, remove https://, and change documents to gremlin.cosmosdb.</span><span class="sxs-lookup"><span data-stu-id="2a419-146">Use the **URI** value, remove https://, and change documents to gremlin.cosmosdb.</span></span> <span data-ttu-id="2a419-147">If your graph account was created before December 20th, 2017, change documents to graphs.</span><span class="sxs-lookup"><span data-stu-id="2a419-147">If your graph account was created before December 20th, 2017, change documents to graphs.</span></span> 

   <span data-ttu-id="2a419-148">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.gremlin.cosmosdb.azure.com` (not `https://mygraphdb.gremlin.cosmosdb.azure.com` or `mygraphdb.gremlin.cosmosdb.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="2a419-148">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.gremlin.cosmosdb.azure.com` (not `https://mygraphdb.gremlin.cosmosdb.azure.com` or `mygraphdb.gremlin.cosmosdb.azure.com:433`).</span></span>

3. <span data-ttu-id="2a419-149">In config.js, fill in the config.primaryKey value with the **Primary Key** value from the **Keys** page of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2a419-149">In config.js, fill in the config.primaryKey value with the **Primary Key** value from the **Keys** page of the Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Azure portal "Keys" blade](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="2a419-151">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span><span class="sxs-lookup"><span data-stu-id="2a419-151">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span></span> 

<span data-ttu-id="2a419-152">Here's an example of what your completed config.js file should look like:</span><span class="sxs-lookup"><span data-stu-id="2a419-152">Here's an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.gremlin.cosmosdb.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a><span data-ttu-id="2a419-153">Run the console app</span><span class="sxs-lookup"><span data-stu-id="2a419-153">Run the console app</span></span>

1. <span data-ttu-id="2a419-154">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span><span class="sxs-lookup"><span data-stu-id="2a419-154">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span></span>

2. <span data-ttu-id="2a419-155">Run `npm install` to install the required npm modules, including `gremlin`.</span><span class="sxs-lookup"><span data-stu-id="2a419-155">Run `npm install` to install the required npm modules, including `gremlin`.</span></span>

3. <span data-ttu-id="2a419-156">Run `node app.js` in a terminal to start your node application.</span><span class="sxs-lookup"><span data-stu-id="2a419-156">Run `node app.js` in a terminal to start your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="2a419-157">Browse with Data Explorer</span><span class="sxs-lookup"><span data-stu-id="2a419-157">Browse with Data Explorer</span></span>

<span data-ttu-id="2a419-158">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span><span class="sxs-lookup"><span data-stu-id="2a419-158">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="2a419-159">In Data Explorer, the new database appears in the **Graphs** pane.</span><span class="sxs-lookup"><span data-stu-id="2a419-159">In Data Explorer, the new database appears in the **Graphs** pane.</span></span> <span data-ttu-id="2a419-160">Expand the database, followed by the container, and then select **Graph**.</span><span class="sxs-lookup"><span data-stu-id="2a419-160">Expand the database, followed by the container, and then select **Graph**.</span></span>

<span data-ttu-id="2a419-161">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you select **Apply Filter**.</span><span class="sxs-lookup"><span data-stu-id="2a419-161">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you select **Apply Filter**.</span></span>

<span data-ttu-id="2a419-162">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span><span class="sxs-lookup"><span data-stu-id="2a419-162">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span></span> <span data-ttu-id="2a419-163">Note that the value is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="2a419-163">Note that the value is case sensitive.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="2a419-164">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2a419-164">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="2a419-165">Clean up your resources</span><span class="sxs-lookup"><span data-stu-id="2a419-165">Clean up your resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="2a419-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a419-166">Next steps</span></span>

<span data-ttu-id="2a419-167">In this article, you learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="2a419-167">In this article, you learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="2a419-168">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span><span class="sxs-lookup"><span data-stu-id="2a419-168">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [Query by using Gremlin](tutorial-query-graph.md)
