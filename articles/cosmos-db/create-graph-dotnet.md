---
title: Build an Azure Cosmos DB .NET Framework or Core application using the Gremlin API | Microsoft Docs
description: Presents a .NET Framework/Core code sample you can use to connect to and query Azure Cosmos DB
services: cosmos-db
author: luisbosquez
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.custom: quick start connect, mvc
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lbosq
ms.openlocfilehash: dff675fc64d9ee7e01a7e050a42a2724d00ec3ef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857089"
---
# <a name="azure-cosmos-db-build-a-net-framework-or-core-application-using-the-gremlin-api"></a><span data-ttu-id="aab7f-103">Azure Cosmos DB: Build a .NET Framework or Core application using the Gremlin API</span><span class="sxs-lookup"><span data-stu-id="aab7f-103">Azure Cosmos DB: Build a .NET Framework or Core application using the Gremlin API</span></span>

> [!div class="op_single_selector"]
> * [Gremlin console](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

<span data-ttu-id="aab7f-110">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="aab7f-110">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="aab7f-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aab7f-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="aab7f-112">This quick start demonstrates how to create an Azure Cosmos DB [Gremlin API](graph-introduction.md) account, database, and graph (container) using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aab7f-112">This quick start demonstrates how to create an Azure Cosmos DB [Gremlin API](graph-introduction.md) account, database, and graph (container) using the Azure portal.</span></span> <span data-ttu-id="aab7f-113">You then build and run a console app built using the open-source driver [Gremlin.Net](http://tinkerpop.apache.org/docs/3.2.7/reference/#gremlin-DotNet).</span><span class="sxs-lookup"><span data-stu-id="aab7f-113">You then build and run a console app built using the open-source driver [Gremlin.Net](http://tinkerpop.apache.org/docs/3.2.7/reference/#gremlin-DotNet).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="aab7f-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aab7f-114">Prerequisites</span></span>

<span data-ttu-id="aab7f-115">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="aab7f-115">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="aab7f-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="aab7f-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

<span data-ttu-id="aab7f-117">If you already have Visual Studio 2017 installed, make sure to be installed up to [Visual Studio 2017 Update 3](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes).</span><span class="sxs-lookup"><span data-stu-id="aab7f-117">If you already have Visual Studio 2017 installed, make sure to be installed up to [Visual Studio 2017 Update 3](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="aab7f-118">Create a database account</span><span class="sxs-lookup"><span data-stu-id="aab7f-118">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="aab7f-119">Add a graph</span><span class="sxs-lookup"><span data-stu-id="aab7f-119">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="aab7f-120">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="aab7f-120">Clone the sample application</span></span>

<span data-ttu-id="aab7f-121">Now let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="aab7f-121">Now let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="aab7f-122">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="aab7f-122">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="aab7f-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="aab7f-123">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="aab7f-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="aab7f-124">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="aab7f-125">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="aab7f-125">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="aab7f-126">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="aab7f-126">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-gremlindotnet-getting-started.git
    ```

4. <span data-ttu-id="aab7f-127">Then open Visual Studio and open the solution file.</span><span class="sxs-lookup"><span data-stu-id="aab7f-127">Then open Visual Studio and open the solution file.</span></span>

5. <span data-ttu-id="aab7f-128">Restore the NuGet packages in the project.</span><span class="sxs-lookup"><span data-stu-id="aab7f-128">Restore the NuGet packages in the project.</span></span> <span data-ttu-id="aab7f-129">This should include the Gremlin.Net driver, as well as the Newtonsoft.Json package.</span><span class="sxs-lookup"><span data-stu-id="aab7f-129">This should include the Gremlin.Net driver, as well as the Newtonsoft.Json package.</span></span>


6. <span data-ttu-id="aab7f-130">You can also install the Gremlin.Net driver manually using the Nuget package manager, or the [nuget command-line utility](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools):</span><span class="sxs-lookup"><span data-stu-id="aab7f-130">You can also install the Gremlin.Net driver manually using the Nuget package manager, or the [nuget command-line utility](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools):</span></span> 

    ```bash
    nuget install Gremlin.Net
    ```

## <a name="review-the-code"></a><span data-ttu-id="aab7f-131">Review the code</span><span class="sxs-lookup"><span data-stu-id="aab7f-131">Review the code</span></span>

<span data-ttu-id="aab7f-132">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="aab7f-132">This step is optional.</span></span> <span data-ttu-id="aab7f-133">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="aab7f-133">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="aab7f-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="aab7f-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span> 

<span data-ttu-id="aab7f-135">The following snippets are all taken from the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="aab7f-135">The following snippets are all taken from the Program.cs file.</span></span>

* <span data-ttu-id="aab7f-136">Set your connection parameters based on the account created above (Line 19):</span><span class="sxs-lookup"><span data-stu-id="aab7f-136">Set your connection parameters based on the account created above (Line 19):</span></span> 

    ```csharp
    private static string hostname = "your-endpoint.gremlin.cosmosdb.azure.com";
    private static int port = 443;
    private static string authKey = "your-authentication-key";
    private static string database = "your-database";
    private static string collection = "your-graph-container";
    ```

* <span data-ttu-id="aab7f-137">The Gremlin commands to be executed are listed in a Dictionary (Line 26):</span><span class="sxs-lookup"><span data-stu-id="aab7f-137">The Gremlin commands to be executed are listed in a Dictionary (Line 26):</span></span>

    ```csharp
    private static Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
    {
        { "Cleanup",        "g.V().drop()" },
        { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
        { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
        { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
        { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
        { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
        { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
        { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
        { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
        { "CountVertices",  "g.V().count()" },
        { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
        { "Project",        "g.V().hasLabel('person').values('firstName')" },
        { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
        { "Traverse",       "g.V('thomas').out('knows').hasLabel('person')" },
        { "Traverse 2x",    "g.V('thomas').out('knows').hasLabel('person').out('knows').hasLabel('person')" },
        { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
        { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
        { "CountEdges",     "g.E().count()" },
        { "DropVertex",     "g.V('thomas').drop()" },
    };
    ```


* <span data-ttu-id="aab7f-138">Create a `GremlinServer` connection object using the parameters provided above (Line 52):</span><span class="sxs-lookup"><span data-stu-id="aab7f-138">Create a `GremlinServer` connection object using the parameters provided above (Line 52):</span></span>

    ```csharp
    var gremlinServer = new GremlinServer(hostname, port, enableSsl: true, 
                                                    username: "/dbs/" + database + "/colls/" + collection, 
                                                    password: authKey);
    ```

* <span data-ttu-id="aab7f-139">Create a new `GremlinClient` object (Line 56):</span><span class="sxs-lookup"><span data-stu-id="aab7f-139">Create a new `GremlinClient` object (Line 56):</span></span>

    ```csharp
    var gremlinClient = new GremlinClient(gremlinServer);
    ```

* <span data-ttu-id="aab7f-140">Execute each Gremlin query using the `GremlinClient` object with an async task (Line 63).</span><span class="sxs-lookup"><span data-stu-id="aab7f-140">Execute each Gremlin query using the `GremlinClient` object with an async task (Line 63).</span></span> <span data-ttu-id="aab7f-141">This will read the Gremlin queries from the dictionary defined above (Line 26):</span><span class="sxs-lookup"><span data-stu-id="aab7f-141">This will read the Gremlin queries from the dictionary defined above (Line 26):</span></span>

    ```csharp
    var task = gremlinClient.SubmitAsync<dynamic>(query.Value);
    task.Wait();
    ```

* <span data-ttu-id="aab7f-142">Retrieve the result and read the values, which are formatted as a dictionary, using the `JsonSerializer` class from Newtonsoft.Json:</span><span class="sxs-lookup"><span data-stu-id="aab7f-142">Retrieve the result and read the values, which are formatted as a dictionary, using the `JsonSerializer` class from Newtonsoft.Json:</span></span>

    ```csharp
    foreach (var result in task.Result)
    {
        // The vertex results are formed as dictionaries with a nested dictionary for their properties
        string output = JsonConvert.SerializeObject(result);
        Console.WriteLine(String.Format("\tResult:\n\t{0}", output));
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="aab7f-143">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="aab7f-143">Update your connection string</span></span>

<span data-ttu-id="aab7f-144">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="aab7f-144">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="aab7f-145">From the [Azure portal](http://portal.azure.com/), navigate to your graph database account.</span><span class="sxs-lookup"><span data-stu-id="aab7f-145">From the [Azure portal](http://portal.azure.com/), navigate to your graph database account.</span></span> <span data-ttu-id="aab7f-146">In the **Overview** tab, you can see two endpoints-</span><span class="sxs-lookup"><span data-stu-id="aab7f-146">In the **Overview** tab, you can see two endpoints-</span></span> 
 
   <span data-ttu-id="aab7f-147">**.Net SDK URI** - This value is used when you connect to the graph account by using Microsoft.Azure.Graphs library.</span><span class="sxs-lookup"><span data-stu-id="aab7f-147">**.Net SDK URI** - This value is used when you connect to the graph account by using Microsoft.Azure.Graphs library.</span></span> 

   <span data-ttu-id="aab7f-148">**Gremlin Endpoint** - This value is used when you connect to the graph account by using Gremlin.Net library.</span><span class="sxs-lookup"><span data-stu-id="aab7f-148">**Gremlin Endpoint** - This value is used when you connect to the graph account by using Gremlin.Net library.</span></span>

    ![Copy the endpoint](./media/create-graph-dotnet/endpoint.png)

   <span data-ttu-id="aab7f-150">To run this sample, copy the **Gremlin Endpoint** value, delete the port number at the end, that is the URI becomes `https://<your cosmos db account name>.gremlin.cosmosdb.azure.com`</span><span class="sxs-lookup"><span data-stu-id="aab7f-150">To run this sample, copy the **Gremlin Endpoint** value, delete the port number at the end, that is the URI becomes `https://<your cosmos db account name>.gremlin.cosmosdb.azure.com`</span></span>

2. <span data-ttu-id="aab7f-151">In Program.cs paste the value over `your-endpoint` in the `hostname` variable in line 19.</span><span class="sxs-lookup"><span data-stu-id="aab7f-151">In Program.cs paste the value over `your-endpoint` in the `hostname` variable in line 19.</span></span> 

    `"private static string hostname = "<your cosmos db account name>.gremlin.cosmosdb.azure.com";`

    <span data-ttu-id="aab7f-152">The endpoint value should now look like this:</span><span class="sxs-lookup"><span data-stu-id="aab7f-152">The endpoint value should now look like this:</span></span>

    `"private static string hostname = "testgraphacct.gremlin.cosmosdb.azure.com";`

3. <span data-ttu-id="aab7f-153">Next, navigate to the **Keys** tab and copy **PRIMARY KEY** value from the portal, and paste it in the `authkey` variable, replacing the `"your-authentication-key"` placeholder in line 21.</span><span class="sxs-lookup"><span data-stu-id="aab7f-153">Next, navigate to the **Keys** tab and copy **PRIMARY KEY** value from the portal, and paste it in the `authkey` variable, replacing the `"your-authentication-key"` placeholder in line 21.</span></span> 

    `private static string authKey = "your-authentication-key";`

4. <span data-ttu-id="aab7f-154">Using the information of the database created above, paste the database name inside of the `database` variable in line 22.</span><span class="sxs-lookup"><span data-stu-id="aab7f-154">Using the information of the database created above, paste the database name inside of the `database` variable in line 22.</span></span> 

    `private static string database = "your-database";`

5. <span data-ttu-id="aab7f-155">Similarly, using the information of the container created above, paste the collection (which is also the graph name) inside of the `collection` variable in line 23.</span><span class="sxs-lookup"><span data-stu-id="aab7f-155">Similarly, using the information of the container created above, paste the collection (which is also the graph name) inside of the `collection` variable in line 23.</span></span> 

    `private static string collection = "your-collection-or-graph";`

6. <span data-ttu-id="aab7f-156">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="aab7f-156">Save the Program.cs file.</span></span> 

<span data-ttu-id="aab7f-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aab7f-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-console-app"></a><span data-ttu-id="aab7f-158">Run the console app</span><span class="sxs-lookup"><span data-stu-id="aab7f-158">Run the console app</span></span>

<span data-ttu-id="aab7f-159">Click CTRL + F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="aab7f-159">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="aab7f-160">The application will print both the Gremlin query commands and results in the console.</span><span class="sxs-lookup"><span data-stu-id="aab7f-160">The application will print both the Gremlin query commands and results in the console.</span></span>

   <span data-ttu-id="aab7f-161">The console window displays the vertexes and edges being added to the graph.</span><span class="sxs-lookup"><span data-stu-id="aab7f-161">The console window displays the vertexes and edges being added to the graph.</span></span> <span data-ttu-id="aab7f-162">When the script completes, press ENTER to close the console window.</span><span class="sxs-lookup"><span data-stu-id="aab7f-162">When the script completes, press ENTER to close the console window.</span></span>

## <a name="browse-using-the-data-explorer"></a><span data-ttu-id="aab7f-163">Browse using the Data Explorer</span><span class="sxs-lookup"><span data-stu-id="aab7f-163">Browse using the Data Explorer</span></span>

<span data-ttu-id="aab7f-164">You can now go back to Data Explorer in the Azure portal and browse and query your new graph data.</span><span class="sxs-lookup"><span data-stu-id="aab7f-164">You can now go back to Data Explorer in the Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="aab7f-165">In Data Explorer, the new database appears in the Graphs pane.</span><span class="sxs-lookup"><span data-stu-id="aab7f-165">In Data Explorer, the new database appears in the Graphs pane.</span></span> <span data-ttu-id="aab7f-166">Expand the database and container nodes, and then click **Graph**.</span><span class="sxs-lookup"><span data-stu-id="aab7f-166">Expand the database and container nodes, and then click **Graph**.</span></span>

2. <span data-ttu-id="aab7f-167">Click the **Apply Filter** button to use the default query to view all the vertices in the graph.</span><span class="sxs-lookup"><span data-stu-id="aab7f-167">Click the **Apply Filter** button to use the default query to view all the vertices in the graph.</span></span> <span data-ttu-id="aab7f-168">The data generated by the sample app is displayed in the Graphs pane.</span><span class="sxs-lookup"><span data-stu-id="aab7f-168">The data generated by the sample app is displayed in the Graphs pane.</span></span>

    <span data-ttu-id="aab7f-169">You can zoom in and out of the graph, you can expand the graph display space, add additional vertices, and move vertices on the display surface.</span><span class="sxs-lookup"><span data-stu-id="aab7f-169">You can zoom in and out of the graph, you can expand the graph display space, add additional vertices, and move vertices on the display surface.</span></span>

    ![View the graph in Data Explorer in the Azure portal](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="aab7f-171">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="aab7f-171">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="aab7f-172">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="aab7f-172">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="aab7f-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="aab7f-173">Next steps</span></span>

<span data-ttu-id="aab7f-174">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="aab7f-174">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="aab7f-175">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aab7f-175">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md)

