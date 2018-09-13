---
title: 'Quickstart: Gremlin API with Python - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Gremlin API to create a console application with the Azure portal and Python
services: cosmos-db
author: luisbosquez
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.custom: quick start connect, mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 01/22/2018
ms.author: lbosq
ms.openlocfilehash: d01ee78c4e3fdf0eab694deaeed03e0f61989851
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869370"
---
# <a name="azure-cosmos-db-create-a-graph-database-using-python-and-the-azure-portal"></a><span data-ttu-id="36015-103">Azure Cosmos DB: Create a graph database using Python and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="36015-103">Azure Cosmos DB: Create a graph database using Python and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Gremlin console](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

<span data-ttu-id="36015-110">This quickstart shows how to use Python and the Azure Cosmos DB [Gremlin API](graph-introduction.md) to build a console app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="36015-110">This quickstart shows how to use Python and the Azure Cosmos DB [Gremlin API](graph-introduction.md) to build a console app by cloning an example from GitHub.</span></span> <span data-ttu-id="36015-111">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="36015-111">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span></span>   

<span data-ttu-id="36015-112">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="36015-112">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="36015-113">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="36015-113">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>  

> [!NOTE]
> This quickstart requires a graph database account created after December 20th, 2017. Existing accounts will support Python once they’re migrated to general availability.

## <a name="prerequisites"></a><span data-ttu-id="36015-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="36015-116">Prerequisites</span></span>

<span data-ttu-id="36015-117">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="36015-117">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="36015-118">In addition:</span><span class="sxs-lookup"><span data-stu-id="36015-118">In addition:</span></span>
* <span data-ttu-id="36015-119">[Python](https://www.python.org/downloads/) version v3.5 or newer</span><span class="sxs-lookup"><span data-stu-id="36015-119">[Python](https://www.python.org/downloads/) version v3.5 or newer</span></span>
* [<span data-ttu-id="36015-120">pip package manager</span><span class="sxs-lookup"><span data-stu-id="36015-120">pip package manager</span></span>](https://pip.pypa.io/en/stable/installing/)
* [<span data-ttu-id="36015-121">Git</span><span class="sxs-lookup"><span data-stu-id="36015-121">Git</span></span>](http://git-scm.com/)
* [<span data-ttu-id="36015-122">Python Driver for Gremlin</span><span class="sxs-lookup"><span data-stu-id="36015-122">Python Driver for Gremlin</span></span>](https://github.com/apache/tinkerpop/tree/master/gremlin-python)

## <a name="create-a-database-account"></a><span data-ttu-id="36015-123">Create a database account</span><span class="sxs-lookup"><span data-stu-id="36015-123">Create a database account</span></span>

<span data-ttu-id="36015-124">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="36015-124">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="36015-125">Add a graph</span><span class="sxs-lookup"><span data-stu-id="36015-125">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="36015-126">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="36015-126">Clone the sample application</span></span>

<span data-ttu-id="36015-127">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="36015-127">Now let's switch to working with code.</span></span> <span data-ttu-id="36015-128">Let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="36015-128">Let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="36015-129">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="36015-129">You'll see how easy it is to work with data programmatically.</span></span>  

1. <span data-ttu-id="36015-130">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="36015-130">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="36015-131">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="36015-131">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span></span>  

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="36015-132">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="36015-132">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="36015-133">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="36015-133">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="36015-134">Review the code</span><span class="sxs-lookup"><span data-stu-id="36015-134">Review the code</span></span>

<span data-ttu-id="36015-135">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="36015-135">This step is optional.</span></span> <span data-ttu-id="36015-136">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="36015-136">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="36015-137">The snippets are all taken from the connect.py file in the C:\git-samples\azure-cosmos-db-graph-python-getting-started\ folder.</span><span class="sxs-lookup"><span data-stu-id="36015-137">The snippets are all taken from the connect.py file in the C:\git-samples\azure-cosmos-db-graph-python-getting-started\ folder.</span></span> <span data-ttu-id="36015-138">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-information).</span><span class="sxs-lookup"><span data-stu-id="36015-138">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-information).</span></span> 

* <span data-ttu-id="36015-139">The Gremlin `client` is initialized in line 104 in `connect.py`:</span><span class="sxs-lookup"><span data-stu-id="36015-139">The Gremlin `client` is initialized in line 104 in `connect.py`:</span></span>

    ```python
    ...
    client = client.Client('wss://<YOUR_ENDPOINT>.gremlin.cosmosdb.azure.com:443/','g', 
        username="/dbs/<YOUR_DATABASE>/colls/<YOUR_COLLECTION_OR_GRAPH>", 
        password="<YOUR_PASSWORD>")
    ...
    ```

* <span data-ttu-id="36015-140">A series of Gremlin steps are declared at the beginning of the `connect.py` file.</span><span class="sxs-lookup"><span data-stu-id="36015-140">A series of Gremlin steps are declared at the beginning of the `connect.py` file.</span></span> <span data-ttu-id="36015-141">They are then executed using the `client.submitAsync()` method:</span><span class="sxs-lookup"><span data-stu-id="36015-141">They are then executed using the `client.submitAsync()` method:</span></span>

    ```python
    client.submitAsync(_gremlin_cleanup_graph)
    ```

## <a name="update-your-connection-information"></a><span data-ttu-id="36015-142">Update your connection information</span><span class="sxs-lookup"><span data-stu-id="36015-142">Update your connection information</span></span>

<span data-ttu-id="36015-143">Now go back to the Azure portal to get your connection information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="36015-143">Now go back to the Azure portal to get your connection information and copy it into the app.</span></span> <span data-ttu-id="36015-144">These settings enable your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="36015-144">These settings enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="36015-145">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="36015-145">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span></span> 

    <span data-ttu-id="36015-146">Copy the first portion of the URI value.</span><span class="sxs-lookup"><span data-stu-id="36015-146">Copy the first portion of the URI value.</span></span>

    ![View and copy an access key in the Azure portal, Keys page](./media/create-graph-python/keys.png)

2. <span data-ttu-id="36015-148">Open the connect.py file and in line 104 paste the URI value over `<YOUR_ENDPOINT>` in here:</span><span class="sxs-lookup"><span data-stu-id="36015-148">Open the connect.py file and in line 104 paste the URI value over `<YOUR_ENDPOINT>` in here:</span></span>

    ```python
    client = client.Client('wss://<YOUR_ENDPOINT>.gremlin.cosmosdb.azure.com:443/','g', 
        username="/dbs/<YOUR_DATABASE>/colls/<YOUR_COLLECTION_OR_GRAPH>", 
        password="<YOUR_PASSWORD>")
    ```

    <span data-ttu-id="36015-149">The URI portion of the client object should now look similar to this code:</span><span class="sxs-lookup"><span data-stu-id="36015-149">The URI portion of the client object should now look similar to this code:</span></span>

    ```python
    client = client.Client('wss://test.gremlin.cosmosdb.azure.com:443/','g', 
        username="/dbs/<YOUR_DATABASE>/colls/<YOUR_COLLECTION_OR_GRAPH>", 
        password="<YOUR_PASSWORD>")
    ```

3. <span data-ttu-id="36015-150">Change the second parameter of the `client` object to replace the `<YOUR_DATABASE>` and `<YOUR_COLLECTION_OR_GRAPH>` strings.</span><span class="sxs-lookup"><span data-stu-id="36015-150">Change the second parameter of the `client` object to replace the `<YOUR_DATABASE>` and `<YOUR_COLLECTION_OR_GRAPH>` strings.</span></span> <span data-ttu-id="36015-151">If you used the suggested values, the parameter should look like this code:</span><span class="sxs-lookup"><span data-stu-id="36015-151">If you used the suggested values, the parameter should look like this code:</span></span>

    `username="/dbs/sample-database/colls/sample-graph"`

    <span data-ttu-id="36015-152">The entire `client` object should now look like this code:</span><span class="sxs-lookup"><span data-stu-id="36015-152">The entire `client` object should now look like this code:</span></span>

    ```python
    client = client.Client('wss://test.gremlin.cosmosdb.azure.com:443/','g', 
        username="/dbs/sample-database/colls/sample-graph", 
        password="<YOUR_PASSWORD>")
    ```

4. <span data-ttu-id="36015-153">In the Azure portal, use the copy button to copy the PRIMARY KEY and paste it over `<YOUR_PASSWORD>` in the `password=<YOUR_PASSWORD>` parameter.</span><span class="sxs-lookup"><span data-stu-id="36015-153">In the Azure portal, use the copy button to copy the PRIMARY KEY and paste it over `<YOUR_PASSWORD>` in the `password=<YOUR_PASSWORD>` parameter.</span></span>

    <span data-ttu-id="36015-154">The entire `client` object definition should now look like this code:</span><span class="sxs-lookup"><span data-stu-id="36015-154">The entire `client` object definition should now look like this code:</span></span>
    ```python
    client = client.Client('wss://test.gremlin.cosmosdb.azure.com:443/','g', 
        username="/dbs/sample-database/colls/sample-graph", 
        password="asdb13Fadsf14FASc22Ggkr662ifxz2Mg==")
    ```

6. <span data-ttu-id="36015-155">Save the `connect.py` file.</span><span class="sxs-lookup"><span data-stu-id="36015-155">Save the `connect.py` file.</span></span>

## <a name="run-the-console-app"></a><span data-ttu-id="36015-156">Run the console app</span><span class="sxs-lookup"><span data-stu-id="36015-156">Run the console app</span></span>

1. <span data-ttu-id="36015-157">In the git terminal window, `cd` to the azure-cosmos-db-graph-python-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="36015-157">In the git terminal window, `cd` to the azure-cosmos-db-graph-python-getting-started folder.</span></span>

    ```git
    cd "C:\git-samples\azure-cosmos-db-graph-python-getting-started"
    ```

2. <span data-ttu-id="36015-158">In the git terminal window, use the following command to install the required Python packages.</span><span class="sxs-lookup"><span data-stu-id="36015-158">In the git terminal window, use the following command to install the required Python packages.</span></span>

   ```
   pip install -r requirements.txt
   ```

3. <span data-ttu-id="36015-159">In the git terminal window, use the following command to start the Python application.</span><span class="sxs-lookup"><span data-stu-id="36015-159">In the git terminal window, use the following command to start the Python application.</span></span>
    
    ```
    python connect.py
    ```

    <span data-ttu-id="36015-160">The terminal window displays the vertices and edges being added to the graph.</span><span class="sxs-lookup"><span data-stu-id="36015-160">The terminal window displays the vertices and edges being added to the graph.</span></span> 
    
    <span data-ttu-id="36015-161">If you experience timeout errors, check that you updated the connection information correctly in [Update your connection information](#update-your-connection-information), and also try running the last command again.</span><span class="sxs-lookup"><span data-stu-id="36015-161">If you experience timeout errors, check that you updated the connection information correctly in [Update your connection information](#update-your-connection-information), and also try running the last command again.</span></span> 
    
    <span data-ttu-id="36015-162">Once the program stops, press Enter, then switch back to the Azure portal in your internet browser.</span><span class="sxs-lookup"><span data-stu-id="36015-162">Once the program stops, press Enter, then switch back to the Azure portal in your internet browser.</span></span>

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="36015-163">Review and add sample data</span><span class="sxs-lookup"><span data-stu-id="36015-163">Review and add sample data</span></span>

<span data-ttu-id="36015-164">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span><span class="sxs-lookup"><span data-stu-id="36015-164">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span></span>

1. <span data-ttu-id="36015-165">Click **Data Explorer**, expand **sample-graph**, click **Graph**, and then click **Apply Filter**.</span><span class="sxs-lookup"><span data-stu-id="36015-165">Click **Data Explorer**, expand **sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Create new documents in Data Explorer in the Azure portal](./media/create-graph-python/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="36015-167">In the **Results** list, notice the new users added to the graph.</span><span class="sxs-lookup"><span data-stu-id="36015-167">In the **Results** list, notice the new users added to the graph.</span></span> <span data-ttu-id="36015-168">Select **ben** and notice that he's connected to robin.</span><span class="sxs-lookup"><span data-stu-id="36015-168">Select **ben** and notice that he's connected to robin.</span></span> <span data-ttu-id="36015-169">You can move the vertices around by dragging and dropping, zoom in and out by scrolling the wheel of your mouse, and expand the size of the graph with the double-arrow.</span><span class="sxs-lookup"><span data-stu-id="36015-169">You can move the vertices around by dragging and dropping, zoom in and out by scrolling the wheel of your mouse, and expand the size of the graph with the double-arrow.</span></span> 

   ![New vertices in the graph in Data Explorer in the Azure portal](./media/create-graph-python/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="36015-171">Let's add a few new users.</span><span class="sxs-lookup"><span data-stu-id="36015-171">Let's add a few new users.</span></span> <span data-ttu-id="36015-172">Click the **New Vertex** button to add data to your graph.</span><span class="sxs-lookup"><span data-stu-id="36015-172">Click the **New Vertex** button to add data to your graph.</span></span>

   ![Create new documents in Data Explorer in the Azure portal](./media/create-graph-python/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="36015-174">Enter a label of *person*.</span><span class="sxs-lookup"><span data-stu-id="36015-174">Enter a label of *person*.</span></span>

5. <span data-ttu-id="36015-175">Click **Add property** to add each of the following properties.</span><span class="sxs-lookup"><span data-stu-id="36015-175">Click **Add property** to add each of the following properties.</span></span> <span data-ttu-id="36015-176">Notice that you can create unique properties for each person in your graph.</span><span class="sxs-lookup"><span data-stu-id="36015-176">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="36015-177">Only the id key is required.</span><span class="sxs-lookup"><span data-stu-id="36015-177">Only the id key is required.</span></span>

    <span data-ttu-id="36015-178">key</span><span class="sxs-lookup"><span data-stu-id="36015-178">key</span></span>|<span data-ttu-id="36015-179">value</span><span class="sxs-lookup"><span data-stu-id="36015-179">value</span></span>|<span data-ttu-id="36015-180">Notes</span><span class="sxs-lookup"><span data-stu-id="36015-180">Notes</span></span>
    ----|----|----
    <span data-ttu-id="36015-181">id</span><span class="sxs-lookup"><span data-stu-id="36015-181">id</span></span>|<span data-ttu-id="36015-182">ashley</span><span class="sxs-lookup"><span data-stu-id="36015-182">ashley</span></span>|<span data-ttu-id="36015-183">The unique identifier for the vertex.</span><span class="sxs-lookup"><span data-stu-id="36015-183">The unique identifier for the vertex.</span></span> <span data-ttu-id="36015-184">If you don't specify an id, one is generated for you.</span><span class="sxs-lookup"><span data-stu-id="36015-184">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="36015-185">gender</span><span class="sxs-lookup"><span data-stu-id="36015-185">gender</span></span>|<span data-ttu-id="36015-186">female</span><span class="sxs-lookup"><span data-stu-id="36015-186">female</span></span>| 
    <span data-ttu-id="36015-187">tech</span><span class="sxs-lookup"><span data-stu-id="36015-187">tech</span></span> | <span data-ttu-id="36015-188">java</span><span class="sxs-lookup"><span data-stu-id="36015-188">java</span></span> | 

    > [!NOTE]
    > In this quickstart create a non-partitioned collection. However, if you create a partitioned collection by specifying a partition key during the collection creation, then you need to include the partition key as a key in each new vertex. 

6. <span data-ttu-id="36015-191">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="36015-191">Click **OK**.</span></span> <span data-ttu-id="36015-192">You may need to expand your screen to see **OK** on the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="36015-192">You may need to expand your screen to see **OK** on the bottom of the screen.</span></span>

7. <span data-ttu-id="36015-193">Click **New Vertex** again and add an additional new user.</span><span class="sxs-lookup"><span data-stu-id="36015-193">Click **New Vertex** again and add an additional new user.</span></span> 

8. <span data-ttu-id="36015-194">Enter a label of *person*.</span><span class="sxs-lookup"><span data-stu-id="36015-194">Enter a label of *person*.</span></span>

9. <span data-ttu-id="36015-195">Click **Add property** to add each of the following properties:</span><span class="sxs-lookup"><span data-stu-id="36015-195">Click **Add property** to add each of the following properties:</span></span>

    <span data-ttu-id="36015-196">key</span><span class="sxs-lookup"><span data-stu-id="36015-196">key</span></span>|<span data-ttu-id="36015-197">value</span><span class="sxs-lookup"><span data-stu-id="36015-197">value</span></span>|<span data-ttu-id="36015-198">Notes</span><span class="sxs-lookup"><span data-stu-id="36015-198">Notes</span></span>
    ----|----|----
    <span data-ttu-id="36015-199">id</span><span class="sxs-lookup"><span data-stu-id="36015-199">id</span></span>|<span data-ttu-id="36015-200">rakesh</span><span class="sxs-lookup"><span data-stu-id="36015-200">rakesh</span></span>|<span data-ttu-id="36015-201">The unique identifier for the vertex.</span><span class="sxs-lookup"><span data-stu-id="36015-201">The unique identifier for the vertex.</span></span> <span data-ttu-id="36015-202">If you don't specify an id, one is generated for you.</span><span class="sxs-lookup"><span data-stu-id="36015-202">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="36015-203">gender</span><span class="sxs-lookup"><span data-stu-id="36015-203">gender</span></span>|<span data-ttu-id="36015-204">male</span><span class="sxs-lookup"><span data-stu-id="36015-204">male</span></span>| 
    <span data-ttu-id="36015-205">school</span><span class="sxs-lookup"><span data-stu-id="36015-205">school</span></span>|<span data-ttu-id="36015-206">MIT</span><span class="sxs-lookup"><span data-stu-id="36015-206">MIT</span></span>| 

10. <span data-ttu-id="36015-207">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="36015-207">Click **OK**.</span></span> 

11. <span data-ttu-id="36015-208">Click the **Apply Filter** button with the default `g.V()` filter to display all the values in the graph.</span><span class="sxs-lookup"><span data-stu-id="36015-208">Click the **Apply Filter** button with the default `g.V()` filter to display all the values in the graph.</span></span> <span data-ttu-id="36015-209">All of the users now show in the **Results** list.</span><span class="sxs-lookup"><span data-stu-id="36015-209">All of the users now show in the **Results** list.</span></span> 

    <span data-ttu-id="36015-210">As you add more data, you can use filters to limit your results.</span><span class="sxs-lookup"><span data-stu-id="36015-210">As you add more data, you can use filters to limit your results.</span></span> <span data-ttu-id="36015-211">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph.</span><span class="sxs-lookup"><span data-stu-id="36015-211">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph.</span></span> <span data-ttu-id="36015-212">You can change it to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span><span class="sxs-lookup"><span data-stu-id="36015-212">You can change it to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span></span> <span data-ttu-id="36015-213">If you changed the filter, change the filter back to `g.V()` and click **Apply Filter** to display all the results again.</span><span class="sxs-lookup"><span data-stu-id="36015-213">If you changed the filter, change the filter back to `g.V()` and click **Apply Filter** to display all the results again.</span></span>

12. <span data-ttu-id="36015-214">Now we can connect rakesh and ashley.</span><span class="sxs-lookup"><span data-stu-id="36015-214">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="36015-215">Ensure **ashley** is selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span><span class="sxs-lookup"><span data-stu-id="36015-215">Ensure **ashley** is selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span></span> <span data-ttu-id="36015-216">You may need to widen your window to see the **Properties** area.</span><span class="sxs-lookup"><span data-stu-id="36015-216">You may need to widen your window to see the **Properties** area.</span></span>

   ![Change the target of a vertex in a graph](./media/create-graph-python/azure-cosmosdb-data-explorer-edit-target.png)

13. <span data-ttu-id="36015-218">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check.</span><span class="sxs-lookup"><span data-stu-id="36015-218">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check.</span></span>

   ![Add a connection between ashley and rakesh in Data Explorer](./media/create-graph-python/azure-cosmosdb-data-explorer-set-target.png)

14. <span data-ttu-id="36015-220">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span><span class="sxs-lookup"><span data-stu-id="36015-220">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span></span> 

   ![Two vertices connected in Data Explorer](./media/create-graph-python/azure-cosmosdb-graph-explorer.png)

   <span data-ttu-id="36015-222">That completes the resource creation part of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="36015-222">That completes the resource creation part of this tutorial.</span></span> <span data-ttu-id="36015-223">You can continue to add vertexes to your graph, modify the existing vertexes, or change the queries.</span><span class="sxs-lookup"><span data-stu-id="36015-223">You can continue to add vertexes to your graph, modify the existing vertexes, or change the queries.</span></span> <span data-ttu-id="36015-224">Now let's review the metrics Azure Cosmos DB provides, and then clean up the resources.</span><span class="sxs-lookup"><span data-stu-id="36015-224">Now let's review the metrics Azure Cosmos DB provides, and then clean up the resources.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="36015-225">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="36015-225">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="36015-226">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="36015-226">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="36015-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="36015-227">Next steps</span></span>

<span data-ttu-id="36015-228">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="36015-228">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="36015-229">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span><span class="sxs-lookup"><span data-stu-id="36015-229">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md)

