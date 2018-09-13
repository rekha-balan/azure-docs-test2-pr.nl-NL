---
title: Create an Azure Cosmos DB graph database with Java | Microsoft Docs
description: Presents a Java code sample you can use to connect to and query graph data in Azure Cosmos DB using Gremlin.
services: cosmos-db
author: luisbosquez
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.custom: quick start connect, mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 03/26/2018
ms.author: lbosq
ms.openlocfilehash: 0c174b6979e1601d992b0e19d216d1b7211e51d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966669"
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-the-azure-portal"></a><span data-ttu-id="209e5-103">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="209e5-103">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Gremlin console](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

<span data-ttu-id="209e5-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="209e5-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="209e5-111">Using Azure Cosmos DB, you can quickly create and query managed document, table, and graph databases.</span><span class="sxs-lookup"><span data-stu-id="209e5-111">Using Azure Cosmos DB, you can quickly create and query managed document, table, and graph databases.</span></span> 

<span data-ttu-id="209e5-112">This quickstart creates a simple graph database using the Azure portal tools for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="209e5-112">This quickstart creates a simple graph database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="209e5-113">This quickstart also shows you how to quickly create a Java console app using a [Gremlin API](graph-introduction.md) database using the OSS [Apache TinkerPop](http://tinkerpop.apache.org/) driver.</span><span class="sxs-lookup"><span data-stu-id="209e5-113">This quickstart also shows you how to quickly create a Java console app using a [Gremlin API](graph-introduction.md) database using the OSS [Apache TinkerPop](http://tinkerpop.apache.org/) driver.</span></span> <span data-ttu-id="209e5-114">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span><span class="sxs-lookup"><span data-stu-id="209e5-114">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="209e5-115">This quickstart familiarizes you with creating and modifying graphs in either the UI or programmatically, whichever is your preference.</span><span class="sxs-lookup"><span data-stu-id="209e5-115">This quickstart familiarizes you with creating and modifying graphs in either the UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="209e5-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="209e5-116">Prerequisites</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="209e5-117">In addition:</span><span class="sxs-lookup"><span data-stu-id="209e5-117">In addition:</span></span>

* [<span data-ttu-id="209e5-118">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="209e5-118">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="209e5-119">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span><span class="sxs-lookup"><span data-stu-id="209e5-119">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="209e5-120">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="209e5-120">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="209e5-121">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span><span class="sxs-lookup"><span data-stu-id="209e5-121">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="209e5-122">On Ubuntu, you can run `apt-get install maven` to install Maven.</span><span class="sxs-lookup"><span data-stu-id="209e5-122">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="209e5-123">Git</span><span class="sxs-lookup"><span data-stu-id="209e5-123">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="209e5-124">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span><span class="sxs-lookup"><span data-stu-id="209e5-124">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="209e5-125">Create a database account</span><span class="sxs-lookup"><span data-stu-id="209e5-125">Create a database account</span></span>

<span data-ttu-id="209e5-126">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="209e5-126">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="209e5-127">Add a graph</span><span class="sxs-lookup"><span data-stu-id="209e5-127">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="209e5-128">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="209e5-128">Clone the sample application</span></span>

<span data-ttu-id="209e5-129">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="209e5-129">Now let's switch to working with code.</span></span> <span data-ttu-id="209e5-130">Let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="209e5-130">Let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="209e5-131">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="209e5-131">You'll see how easy it is to work with data programmatically.</span></span>  

1. <span data-ttu-id="209e5-132">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="209e5-132">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="209e5-133">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="209e5-133">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span></span>  

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="209e5-134">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="209e5-134">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="209e5-135">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="209e5-135">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="209e5-136">Review the code</span><span class="sxs-lookup"><span data-stu-id="209e5-136">Review the code</span></span>

<span data-ttu-id="209e5-137">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="209e5-137">This step is optional.</span></span> <span data-ttu-id="209e5-138">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="209e5-138">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="209e5-139">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-information).</span><span class="sxs-lookup"><span data-stu-id="209e5-139">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-information).</span></span>

<span data-ttu-id="209e5-140">The following snippets are all taken from the C:\git-samples\azure-cosmos-db-graph-java-getting-started\src\GetStarted\Program.java file.</span><span class="sxs-lookup"><span data-stu-id="209e5-140">The following snippets are all taken from the C:\git-samples\azure-cosmos-db-graph-java-getting-started\src\GetStarted\Program.java file.</span></span>

* <span data-ttu-id="209e5-141">The Gremlin `Client` is initialized from the configuration in the C:\git-samples\azure-cosmos-db-graph-java-getting-started\src\remote.yaml file.</span><span class="sxs-lookup"><span data-stu-id="209e5-141">The Gremlin `Client` is initialized from the configuration in the C:\git-samples\azure-cosmos-db-graph-java-getting-started\src\remote.yaml file.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="209e5-142">Series of Gremlin steps are executed using the `client.submit` method.</span><span class="sxs-lookup"><span data-stu-id="209e5-142">Series of Gremlin steps are executed using the `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-information"></a><span data-ttu-id="209e5-143">Update your connection information</span><span class="sxs-lookup"><span data-stu-id="209e5-143">Update your connection information</span></span>

<span data-ttu-id="209e5-144">Now go back to the Azure portal to get your connection information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="209e5-144">Now go back to the Azure portal to get your connection information and copy it into the app.</span></span> <span data-ttu-id="209e5-145">These settings enable your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="209e5-145">These settings enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="209e5-146">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="209e5-146">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span></span> 

    <span data-ttu-id="209e5-147">Copy the first portion of the URI value.</span><span class="sxs-lookup"><span data-stu-id="209e5-147">Copy the first portion of the URI value.</span></span>

    ![View and copy an access key in the Azure portal, Keys page](./media/create-graph-java/keys.png)
2. <span data-ttu-id="209e5-149">Open the src/remote.yaml file and paste the unique ID value over `$name$` in `hosts: [$name$.graphs.azure.com]`.</span><span class="sxs-lookup"><span data-stu-id="209e5-149">Open the src/remote.yaml file and paste the unique ID value over `$name$` in `hosts: [$name$.graphs.azure.com]`.</span></span>

    <span data-ttu-id="209e5-150">Line 1 of remote.yaml should now look similar to</span><span class="sxs-lookup"><span data-stu-id="209e5-150">Line 1 of remote.yaml should now look similar to</span></span> 

    `hosts: [test-graph.graphs.azure.com]`

3. <span data-ttu-id="209e5-151">Change `graphs` to `gremlin.cosmosdb` in the `endpoint` value.</span><span class="sxs-lookup"><span data-stu-id="209e5-151">Change `graphs` to `gremlin.cosmosdb` in the `endpoint` value.</span></span> <span data-ttu-id="209e5-152">(If you created your graph database account before December 20, 2017, make no changes to the endpoint value and continue to the next step.)</span><span class="sxs-lookup"><span data-stu-id="209e5-152">(If you created your graph database account before December 20, 2017, make no changes to the endpoint value and continue to the next step.)</span></span>

    <span data-ttu-id="209e5-153">The endpoint value should now look like this:</span><span class="sxs-lookup"><span data-stu-id="209e5-153">The endpoint value should now look like this:</span></span>

    `"endpoint": "https://testgraphacct.gremlin.cosmosdb.azure.com:443/"`

4. <span data-ttu-id="209e5-154">In the Azure portal, use the copy button to copy the PRIMARY KEY and paste it over `$masterKey$` in `password: $masterKey$`.</span><span class="sxs-lookup"><span data-stu-id="209e5-154">In the Azure portal, use the copy button to copy the PRIMARY KEY and paste it over `$masterKey$` in `password: $masterKey$`.</span></span>

    <span data-ttu-id="209e5-155">Line 4 of remote.yaml should now look similar to</span><span class="sxs-lookup"><span data-stu-id="209e5-155">Line 4 of remote.yaml should now look similar to</span></span> 

    `password: 2Ggkr662ifxz2Mg==`

5. <span data-ttu-id="209e5-156">Change line 3 of remote.yaml from</span><span class="sxs-lookup"><span data-stu-id="209e5-156">Change line 3 of remote.yaml from</span></span>

    `username: /dbs/$database$/colls/$collection$`

    <span data-ttu-id="209e5-157">to</span><span class="sxs-lookup"><span data-stu-id="209e5-157">to</span></span> 

    `username: /dbs/sample-database/colls/sample-graph`

    <span data-ttu-id="209e5-158">If you used a unique name for your sample database or graph, update the values as appropriate.</span><span class="sxs-lookup"><span data-stu-id="209e5-158">If you used a unique name for your sample database or graph, update the values as appropriate.</span></span>

6. <span data-ttu-id="209e5-159">Save the remote.yaml file.</span><span class="sxs-lookup"><span data-stu-id="209e5-159">Save the remote.yaml file.</span></span>

## <a name="run-the-console-app"></a><span data-ttu-id="209e5-160">Run the console app</span><span class="sxs-lookup"><span data-stu-id="209e5-160">Run the console app</span></span>

1. <span data-ttu-id="209e5-161">In the git terminal window, `cd` to the azure-cosmos-db-graph-java-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="209e5-161">In the git terminal window, `cd` to the azure-cosmos-db-graph-java-getting-started folder.</span></span>

    ```git
    cd "C:\git-samples\azure-cosmos-db-graph-java-getting-started"
    ```

2. <span data-ttu-id="209e5-162">In the git terminal window, use the following command to install the required Java packages.</span><span class="sxs-lookup"><span data-stu-id="209e5-162">In the git terminal window, use the following command to install the required Java packages.</span></span>

   ```
   mvn package
   ```

3. <span data-ttu-id="209e5-163">In the git terminal window, use the following command to start the Java application.</span><span class="sxs-lookup"><span data-stu-id="209e5-163">In the git terminal window, use the following command to start the Java application.</span></span>
    
    ```
    mvn exec:java -D exec.mainClass=GetStarted.Program
    ```

    <span data-ttu-id="209e5-164">The terminal window displays the vertices being added to the graph.</span><span class="sxs-lookup"><span data-stu-id="209e5-164">The terminal window displays the vertices being added to the graph.</span></span> 
    
    <span data-ttu-id="209e5-165">If you experience timeout errors, check that you updated the connection information correctly in [Update your connection information](#update-your-connection-information), and also try running the last command again.</span><span class="sxs-lookup"><span data-stu-id="209e5-165">If you experience timeout errors, check that you updated the connection information correctly in [Update your connection information](#update-your-connection-information), and also try running the last command again.</span></span> 
    
    <span data-ttu-id="209e5-166">Once the program stops, press Enter, then switch back to the Azure portal in your internet browser.</span><span class="sxs-lookup"><span data-stu-id="209e5-166">Once the program stops, press Enter, then switch back to the Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="209e5-167">Review and add sample data</span><span class="sxs-lookup"><span data-stu-id="209e5-167">Review and add sample data</span></span>

<span data-ttu-id="209e5-168">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span><span class="sxs-lookup"><span data-stu-id="209e5-168">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span></span>

1. <span data-ttu-id="209e5-169">Click **Data Explorer**, expand **sample-graph**, click **Graph**, and then click **Apply Filter**.</span><span class="sxs-lookup"><span data-stu-id="209e5-169">Click **Data Explorer**, expand **sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Create new documents in Data Explorer in the Azure portal](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="209e5-171">In the **Results** list, notice the new users added to the graph.</span><span class="sxs-lookup"><span data-stu-id="209e5-171">In the **Results** list, notice the new users added to the graph.</span></span> <span data-ttu-id="209e5-172">Select **ben** and notice that the user is connected to robin.</span><span class="sxs-lookup"><span data-stu-id="209e5-172">Select **ben** and notice that the user is connected to robin.</span></span> <span data-ttu-id="209e5-173">You can move the vertices around by dragging and dropping, zoom in and out by scrolling the wheel of your mouse, and expand the size of the graph with the double-arrow.</span><span class="sxs-lookup"><span data-stu-id="209e5-173">You can move the vertices around by dragging and dropping, zoom in and out by scrolling the wheel of your mouse, and expand the size of the graph with the double-arrow.</span></span> 

   ![New vertices in the graph in Data Explorer in the Azure portal](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="209e5-175">Let's add a few new users.</span><span class="sxs-lookup"><span data-stu-id="209e5-175">Let's add a few new users.</span></span> <span data-ttu-id="209e5-176">Click the **New Vertex** button to add data to your graph.</span><span class="sxs-lookup"><span data-stu-id="209e5-176">Click the **New Vertex** button to add data to your graph.</span></span>

   ![Create new documents in Data Explorer in the Azure portal](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="209e5-178">In the label box, enter *person*.</span><span class="sxs-lookup"><span data-stu-id="209e5-178">In the label box, enter *person*.</span></span>

5. <span data-ttu-id="209e5-179">Click **Add property** to add each of the following properties.</span><span class="sxs-lookup"><span data-stu-id="209e5-179">Click **Add property** to add each of the following properties.</span></span> <span data-ttu-id="209e5-180">Notice that you can create unique properties for each person in your graph.</span><span class="sxs-lookup"><span data-stu-id="209e5-180">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="209e5-181">Only the id key is required.</span><span class="sxs-lookup"><span data-stu-id="209e5-181">Only the id key is required.</span></span>

    <span data-ttu-id="209e5-182">key</span><span class="sxs-lookup"><span data-stu-id="209e5-182">key</span></span>|<span data-ttu-id="209e5-183">value</span><span class="sxs-lookup"><span data-stu-id="209e5-183">value</span></span>|<span data-ttu-id="209e5-184">Notes</span><span class="sxs-lookup"><span data-stu-id="209e5-184">Notes</span></span>
    ----|----|----
    <span data-ttu-id="209e5-185">id</span><span class="sxs-lookup"><span data-stu-id="209e5-185">id</span></span>|<span data-ttu-id="209e5-186">ashley</span><span class="sxs-lookup"><span data-stu-id="209e5-186">ashley</span></span>|<span data-ttu-id="209e5-187">The unique identifier for the vertex.</span><span class="sxs-lookup"><span data-stu-id="209e5-187">The unique identifier for the vertex.</span></span> <span data-ttu-id="209e5-188">If you don't specify an id, one is generated for you.</span><span class="sxs-lookup"><span data-stu-id="209e5-188">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="209e5-189">gender</span><span class="sxs-lookup"><span data-stu-id="209e5-189">gender</span></span>|<span data-ttu-id="209e5-190">female</span><span class="sxs-lookup"><span data-stu-id="209e5-190">female</span></span>| 
    <span data-ttu-id="209e5-191">tech</span><span class="sxs-lookup"><span data-stu-id="209e5-191">tech</span></span> | <span data-ttu-id="209e5-192">java</span><span class="sxs-lookup"><span data-stu-id="209e5-192">java</span></span> | 

    > [!NOTE]
    > In this quickstart you create a non-partitioned collection. However, if you create a partitioned collection by specifying a partition key during the collection creation, then you need to include the partition key as a key in each new vertex. 

6. <span data-ttu-id="209e5-195">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="209e5-195">Click **OK**.</span></span> <span data-ttu-id="209e5-196">You may need to expand your screen to see **OK** on the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="209e5-196">You may need to expand your screen to see **OK** on the bottom of the screen.</span></span>

7. <span data-ttu-id="209e5-197">Click **New Vertex** again and add an additional new user.</span><span class="sxs-lookup"><span data-stu-id="209e5-197">Click **New Vertex** again and add an additional new user.</span></span> 

8. <span data-ttu-id="209e5-198">Enter a label of *person*.</span><span class="sxs-lookup"><span data-stu-id="209e5-198">Enter a label of *person*.</span></span>

9. <span data-ttu-id="209e5-199">Click **Add property** to add each of the following properties:</span><span class="sxs-lookup"><span data-stu-id="209e5-199">Click **Add property** to add each of the following properties:</span></span>

    <span data-ttu-id="209e5-200">key</span><span class="sxs-lookup"><span data-stu-id="209e5-200">key</span></span>|<span data-ttu-id="209e5-201">value</span><span class="sxs-lookup"><span data-stu-id="209e5-201">value</span></span>|<span data-ttu-id="209e5-202">Notes</span><span class="sxs-lookup"><span data-stu-id="209e5-202">Notes</span></span>
    ----|----|----
    <span data-ttu-id="209e5-203">id</span><span class="sxs-lookup"><span data-stu-id="209e5-203">id</span></span>|<span data-ttu-id="209e5-204">rakesh</span><span class="sxs-lookup"><span data-stu-id="209e5-204">rakesh</span></span>|<span data-ttu-id="209e5-205">The unique identifier for the vertex.</span><span class="sxs-lookup"><span data-stu-id="209e5-205">The unique identifier for the vertex.</span></span> <span data-ttu-id="209e5-206">If you don't specify an id, one is generated for you.</span><span class="sxs-lookup"><span data-stu-id="209e5-206">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="209e5-207">gender</span><span class="sxs-lookup"><span data-stu-id="209e5-207">gender</span></span>|<span data-ttu-id="209e5-208">male</span><span class="sxs-lookup"><span data-stu-id="209e5-208">male</span></span>| 
    <span data-ttu-id="209e5-209">school</span><span class="sxs-lookup"><span data-stu-id="209e5-209">school</span></span>|<span data-ttu-id="209e5-210">MIT</span><span class="sxs-lookup"><span data-stu-id="209e5-210">MIT</span></span>| 

10. <span data-ttu-id="209e5-211">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="209e5-211">Click **OK**.</span></span> 

11. <span data-ttu-id="209e5-212">Click the **Apply Filter** button with the default `g.V()` filter to display all the values in the graph.</span><span class="sxs-lookup"><span data-stu-id="209e5-212">Click the **Apply Filter** button with the default `g.V()` filter to display all the values in the graph.</span></span> <span data-ttu-id="209e5-213">All of the users now show in the **Results** list.</span><span class="sxs-lookup"><span data-stu-id="209e5-213">All of the users now show in the **Results** list.</span></span> 

    <span data-ttu-id="209e5-214">As you add more data, you can use filters to limit your results.</span><span class="sxs-lookup"><span data-stu-id="209e5-214">As you add more data, you can use filters to limit your results.</span></span> <span data-ttu-id="209e5-215">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph.</span><span class="sxs-lookup"><span data-stu-id="209e5-215">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph.</span></span> <span data-ttu-id="209e5-216">You can change it to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span><span class="sxs-lookup"><span data-stu-id="209e5-216">You can change it to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span></span> <span data-ttu-id="209e5-217">If you changed the filter, change the filter back to `g.V()` and click **Apply Filter** to display all the results again.</span><span class="sxs-lookup"><span data-stu-id="209e5-217">If you changed the filter, change the filter back to `g.V()` and click **Apply Filter** to display all the results again.</span></span>

12. <span data-ttu-id="209e5-218">Now you can connect rakesh, and ashley.</span><span class="sxs-lookup"><span data-stu-id="209e5-218">Now you can connect rakesh, and ashley.</span></span> <span data-ttu-id="209e5-219">Ensure **ashley** is selected in the **Results** list, then click ![Change the target of a vertex in a graph](./media/create-graph-java/edit-pencil-button.png)  next to **Targets** on lower right side.</span><span class="sxs-lookup"><span data-stu-id="209e5-219">Ensure **ashley** is selected in the **Results** list, then click ![Change the target of a vertex in a graph](./media/create-graph-java/edit-pencil-button.png)  next to **Targets** on lower right side.</span></span> <span data-ttu-id="209e5-220">You may need to widen your window to see the button.</span><span class="sxs-lookup"><span data-stu-id="209e5-220">You may need to widen your window to see the button.</span></span>

   ![Change the target of a vertex in a graph](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

13. <span data-ttu-id="209e5-222">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the checkbox.</span><span class="sxs-lookup"><span data-stu-id="209e5-222">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the checkbox.</span></span>

   ![Add a connection between ashley and rakesh in Data Explorer](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

14. <span data-ttu-id="209e5-224">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span><span class="sxs-lookup"><span data-stu-id="209e5-224">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span></span> 

   ![Two vertices connected in Data Explorer](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

   <span data-ttu-id="209e5-226">That completes the resource creation part of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="209e5-226">That completes the resource creation part of this tutorial.</span></span> <span data-ttu-id="209e5-227">You can continue to add vertexes to your graph, modify the existing vertexes, or change the queries.</span><span class="sxs-lookup"><span data-stu-id="209e5-227">You can continue to add vertexes to your graph, modify the existing vertexes, or change the queries.</span></span> <span data-ttu-id="209e5-228">Now let's review the metrics Azure Cosmos DB provides, and then clean up the resources.</span><span class="sxs-lookup"><span data-stu-id="209e5-228">Now let's review the metrics Azure Cosmos DB provides, and then clean up the resources.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="209e5-229">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="209e5-229">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="209e5-230">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="209e5-230">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="209e5-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="209e5-231">Next steps</span></span>

<span data-ttu-id="209e5-232">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="209e5-232">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="209e5-233">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span><span class="sxs-lookup"><span data-stu-id="209e5-233">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md)

