---
title: 'Quickstart: Gremlin API with PHP - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Gremlin API to create a console application with the Azure portal and PHP
services: cosmos-db
author: luisbosquez
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.custom: quick start connect, mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 01/05/2018
ms.author: lbosq
ms.openlocfilehash: 06f54429957a84de81e3dfaae00c6126b5340b74
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968618"
---
# <a name="azure-cosmos-db-create-a-graph-database-using-php-and-the-azure-portal"></a><span data-ttu-id="333da-103">Azure Cosmos DB: Create a graph database using PHP and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="333da-103">Azure Cosmos DB: Create a graph database using PHP and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Gremlin console](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

<span data-ttu-id="333da-110">This quickstart shows how to use PHP and the Azure Cosmos DB [Gremlin API](graph-introduction.md) to build a console app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="333da-110">This quickstart shows how to use PHP and the Azure Cosmos DB [Gremlin API](graph-introduction.md) to build a console app by cloning an example from GitHub.</span></span> <span data-ttu-id="333da-111">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="333da-111">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span></span>   

<span data-ttu-id="333da-112">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="333da-112">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="333da-113">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="333da-113">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="333da-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="333da-114">Prerequisites</span></span>

<span data-ttu-id="333da-115">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="333da-115">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="333da-116">In addition:</span><span class="sxs-lookup"><span data-stu-id="333da-116">In addition:</span></span>
* <span data-ttu-id="333da-117">[PHP](http://php.net/) 5.6 or newer</span><span class="sxs-lookup"><span data-stu-id="333da-117">[PHP](http://php.net/) 5.6 or newer</span></span>
* [<span data-ttu-id="333da-118">Composer</span><span class="sxs-lookup"><span data-stu-id="333da-118">Composer</span></span>](https://getcomposer.org/download/)

## <a name="create-a-database-account"></a><span data-ttu-id="333da-119">Create a database account</span><span class="sxs-lookup"><span data-stu-id="333da-119">Create a database account</span></span>

<span data-ttu-id="333da-120">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="333da-120">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="333da-121">Add a graph</span><span class="sxs-lookup"><span data-stu-id="333da-121">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="333da-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="333da-122">Clone the sample application</span></span>

<span data-ttu-id="333da-123">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="333da-123">Now let's switch to working with code.</span></span> <span data-ttu-id="333da-124">Let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="333da-124">Let's clone a Gremlin API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="333da-125">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="333da-125">You'll see how easy it is to work with data programmatically.</span></span>  

1. <span data-ttu-id="333da-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="333da-126">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="333da-127">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="333da-127">Open a git terminal window, such as git bash, and use the `cd` command to change to a folder to install the sample app.</span></span>  

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="333da-128">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="333da-128">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="333da-129">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="333da-129">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-php-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="333da-130">Review the code</span><span class="sxs-lookup"><span data-stu-id="333da-130">Review the code</span></span>

<span data-ttu-id="333da-131">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="333da-131">This step is optional.</span></span> <span data-ttu-id="333da-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="333da-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="333da-133">The snippets are all taken from the connect.php file in the C:\git-samples\azure-cosmos-db-graph-php-getting-started\ folder.</span><span class="sxs-lookup"><span data-stu-id="333da-133">The snippets are all taken from the connect.php file in the C:\git-samples\azure-cosmos-db-graph-php-getting-started\ folder.</span></span> <span data-ttu-id="333da-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-information).</span><span class="sxs-lookup"><span data-stu-id="333da-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-information).</span></span> 

* <span data-ttu-id="333da-135">The Gremlin `connection` is initialized in the beginning of the `connect.php` file using the `$db` object.</span><span class="sxs-lookup"><span data-stu-id="333da-135">The Gremlin `connection` is initialized in the beginning of the `connect.php` file using the `$db` object.</span></span>

    ```php
    $db = new Connection([
        'host' => '<your_server_address>.graphs.azure.com',
        'username' => '/dbs/<db>/colls/<coll>',
        'password' => 'your_primary_key'
        ,'port' => '443'

        // Required parameter
        ,'ssl' => TRUE
    ]);
    ```

* <span data-ttu-id="333da-136">A series of Gremlin steps are executed using the `$db->send($query);` method.</span><span class="sxs-lookup"><span data-stu-id="333da-136">A series of Gremlin steps are executed using the `$db->send($query);` method.</span></span>

    ```php
    $query = "g.V().drop()";
    ...
    $result = $db->send($query);
    $errors = array_filter($result);
    }
    ```

## <a name="update-your-connection-information"></a><span data-ttu-id="333da-137">Update your connection information</span><span class="sxs-lookup"><span data-stu-id="333da-137">Update your connection information</span></span>

<span data-ttu-id="333da-138">Now go back to the Azure portal to get your connection information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="333da-138">Now go back to the Azure portal to get your connection information and copy it into the app.</span></span> <span data-ttu-id="333da-139">These settings enable your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="333da-139">These settings enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="333da-140">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="333da-140">In the [Azure portal](http://portal.azure.com/), click **Keys**.</span></span> 

    <span data-ttu-id="333da-141">Copy the first portion of the URI value.</span><span class="sxs-lookup"><span data-stu-id="333da-141">Copy the first portion of the URI value.</span></span>

    ![View and copy an access key in the Azure portal, Keys page](./media/create-graph-php/keys.png)
2. <span data-ttu-id="333da-143">Open the `connect.php` file and in line 8 paste the URI value over `your_server_address`.</span><span class="sxs-lookup"><span data-stu-id="333da-143">Open the `connect.php` file and in line 8 paste the URI value over `your_server_address`.</span></span>

    <span data-ttu-id="333da-144">The connection object initialization should now look similar to the following code:</span><span class="sxs-lookup"><span data-stu-id="333da-144">The connection object initialization should now look similar to the following code:</span></span>

    ```php
    $db = new Connection([
        'host' => 'testgraphacct.graphs.azure.com',
        'username' => '/dbs/<db>/colls/<coll>',
        'password' => 'your_primary_key'
        ,'port' => '443'

        // Required parameter
        ,'ssl' => TRUE
    ]);
    ```

3. <span data-ttu-id="333da-145">If your graph database account was created on or after December 20, 2017, change `graphs.azure.com` in the host name to `gremlin.cosmosdb.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="333da-145">If your graph database account was created on or after December 20, 2017, change `graphs.azure.com` in the host name to `gremlin.cosmosdb.azure.com`.</span></span>

4. <span data-ttu-id="333da-146">Change `username` parameter in the Connection object with your database and graph name.</span><span class="sxs-lookup"><span data-stu-id="333da-146">Change `username` parameter in the Connection object with your database and graph name.</span></span> <span data-ttu-id="333da-147">If you used the recommended values of `sample-database` and `sample-graph`, it should look like the following code:</span><span class="sxs-lookup"><span data-stu-id="333da-147">If you used the recommended values of `sample-database` and `sample-graph`, it should look like the following code:</span></span>

    `'username' => '/dbs/sample-database/colls/sample-graph'`

    <span data-ttu-id="333da-148">The entire Connection object should look like the following code snippet at this time:</span><span class="sxs-lookup"><span data-stu-id="333da-148">The entire Connection object should look like the following code snippet at this time:</span></span>

    ```php
    $db = new Connection([
        'host' => 'testgraphacct.graphs.azure.com',
        'username' => '/dbs/sample-database/colls/sample-graph',
        'password' => 'your_primary_key',
        'port' => '443'

        // Required parameter
        ,'ssl' => TRUE
    ]);
    ```

5. <span data-ttu-id="333da-149">In the Azure portal, use the copy button to copy the PRIMARY KEY and paste it over `your_primary_key` in the password parameter.</span><span class="sxs-lookup"><span data-stu-id="333da-149">In the Azure portal, use the copy button to copy the PRIMARY KEY and paste it over `your_primary_key` in the password parameter.</span></span>

    <span data-ttu-id="333da-150">The Connection object initialization should now look like the following code:</span><span class="sxs-lookup"><span data-stu-id="333da-150">The Connection object initialization should now look like the following code:</span></span>

    ```php
    $db = new Connection([
        'host' => 'testgraphacct.graphs.azure.com',
        'username' => '/dbs/sample-database/colls/sample-graph',
        'password' => '2Ggkr662ifxz2Mg==',
        'port' => '443'

        // Required parameter
        ,'ssl' => TRUE
    ]);
    ```

6. <span data-ttu-id="333da-151">Save the `connect.php` file.</span><span class="sxs-lookup"><span data-stu-id="333da-151">Save the `connect.php` file.</span></span>

## <a name="run-the-console-app"></a><span data-ttu-id="333da-152">Run the console app</span><span class="sxs-lookup"><span data-stu-id="333da-152">Run the console app</span></span>

1. <span data-ttu-id="333da-153">In the git terminal window, `cd` to the azure-cosmos-db-graph-php-getting-started folder.</span><span class="sxs-lookup"><span data-stu-id="333da-153">In the git terminal window, `cd` to the azure-cosmos-db-graph-php-getting-started folder.</span></span>

    ```git
    cd "C:\git-samples\azure-cosmos-db-graph-php-getting-started"
    ```

2. <span data-ttu-id="333da-154">In the git terminal window, use the following command to install the required PHP dependencies.</span><span class="sxs-lookup"><span data-stu-id="333da-154">In the git terminal window, use the following command to install the required PHP dependencies.</span></span>

   ```
   composer install
   ```

3. <span data-ttu-id="333da-155">In the git terminal window, use the following command to start the PHP application.</span><span class="sxs-lookup"><span data-stu-id="333da-155">In the git terminal window, use the following command to start the PHP application.</span></span>
    
    ```
    php connect.php
    ```

    <span data-ttu-id="333da-156">The terminal window displays the vertices being added to the graph.</span><span class="sxs-lookup"><span data-stu-id="333da-156">The terminal window displays the vertices being added to the graph.</span></span> 
    
    <span data-ttu-id="333da-157">If you experience timeout errors, check that you updated the connection information correctly in [Update your connection information](#update-your-connection-information), and also try running the last command again.</span><span class="sxs-lookup"><span data-stu-id="333da-157">If you experience timeout errors, check that you updated the connection information correctly in [Update your connection information](#update-your-connection-information), and also try running the last command again.</span></span> 
    
    <span data-ttu-id="333da-158">Once the program stops, press Enter, then switch back to the Azure portal in your internet browser.</span><span class="sxs-lookup"><span data-stu-id="333da-158">Once the program stops, press Enter, then switch back to the Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="333da-159">Review and add sample data</span><span class="sxs-lookup"><span data-stu-id="333da-159">Review and add sample data</span></span>

<span data-ttu-id="333da-160">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span><span class="sxs-lookup"><span data-stu-id="333da-160">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span></span>

1. <span data-ttu-id="333da-161">Click **Data Explorer**, expand **sample-graph**, click **Graph**, and then click **Apply Filter**.</span><span class="sxs-lookup"><span data-stu-id="333da-161">Click **Data Explorer**, expand **sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Create new documents in Data Explorer in the Azure portal](./media/create-graph-php/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="333da-163">In the **Results** list, notice the new users added to the graph.</span><span class="sxs-lookup"><span data-stu-id="333da-163">In the **Results** list, notice the new users added to the graph.</span></span> <span data-ttu-id="333da-164">Select **ben** and notice that he's connected to robin.</span><span class="sxs-lookup"><span data-stu-id="333da-164">Select **ben** and notice that he's connected to robin.</span></span> <span data-ttu-id="333da-165">You can move the vertices around by dragging and dropping, zoom in and out by scrolling the wheel of your mouse, and expand the size of the graph with the double-arrow.</span><span class="sxs-lookup"><span data-stu-id="333da-165">You can move the vertices around by dragging and dropping, zoom in and out by scrolling the wheel of your mouse, and expand the size of the graph with the double-arrow.</span></span> 

   ![New vertices in the graph in Data Explorer in the Azure portal](./media/create-graph-php/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="333da-167">Let's add a few new users.</span><span class="sxs-lookup"><span data-stu-id="333da-167">Let's add a few new users.</span></span> <span data-ttu-id="333da-168">Click the **New Vertex** button to add data to your graph.</span><span class="sxs-lookup"><span data-stu-id="333da-168">Click the **New Vertex** button to add data to your graph.</span></span>

   ![Create new documents in Data Explorer in the Azure portal](./media/create-graph-php/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="333da-170">Enter a label of *person*.</span><span class="sxs-lookup"><span data-stu-id="333da-170">Enter a label of *person*.</span></span>

5. <span data-ttu-id="333da-171">Click **Add property** to add each of the following properties.</span><span class="sxs-lookup"><span data-stu-id="333da-171">Click **Add property** to add each of the following properties.</span></span> <span data-ttu-id="333da-172">Notice that you can create unique properties for each person in your graph.</span><span class="sxs-lookup"><span data-stu-id="333da-172">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="333da-173">Only the id key is required.</span><span class="sxs-lookup"><span data-stu-id="333da-173">Only the id key is required.</span></span>

    <span data-ttu-id="333da-174">key</span><span class="sxs-lookup"><span data-stu-id="333da-174">key</span></span>|<span data-ttu-id="333da-175">value</span><span class="sxs-lookup"><span data-stu-id="333da-175">value</span></span>|<span data-ttu-id="333da-176">Notes</span><span class="sxs-lookup"><span data-stu-id="333da-176">Notes</span></span>
    ----|----|----
    <span data-ttu-id="333da-177">id</span><span class="sxs-lookup"><span data-stu-id="333da-177">id</span></span>|<span data-ttu-id="333da-178">ashley</span><span class="sxs-lookup"><span data-stu-id="333da-178">ashley</span></span>|<span data-ttu-id="333da-179">The unique identifier for the vertex.</span><span class="sxs-lookup"><span data-stu-id="333da-179">The unique identifier for the vertex.</span></span> <span data-ttu-id="333da-180">If you don't specify an id, one is generated for you.</span><span class="sxs-lookup"><span data-stu-id="333da-180">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="333da-181">gender</span><span class="sxs-lookup"><span data-stu-id="333da-181">gender</span></span>|<span data-ttu-id="333da-182">female</span><span class="sxs-lookup"><span data-stu-id="333da-182">female</span></span>| 
    <span data-ttu-id="333da-183">tech</span><span class="sxs-lookup"><span data-stu-id="333da-183">tech</span></span> | <span data-ttu-id="333da-184">java</span><span class="sxs-lookup"><span data-stu-id="333da-184">java</span></span> | 

    > [!NOTE]
    > In this quickstart you create a non-partitioned collection. However, if you create a partitioned collection by specifying a partition key during the collection creation, then you need to include the partition key as a key in each new vertex. 

6. <span data-ttu-id="333da-187">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="333da-187">Click **OK**.</span></span> <span data-ttu-id="333da-188">You may need to expand your screen to see **OK** on the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="333da-188">You may need to expand your screen to see **OK** on the bottom of the screen.</span></span>

7. <span data-ttu-id="333da-189">Click **New Vertex** again and add an additional new user.</span><span class="sxs-lookup"><span data-stu-id="333da-189">Click **New Vertex** again and add an additional new user.</span></span> 

8. <span data-ttu-id="333da-190">Enter a label of *person*.</span><span class="sxs-lookup"><span data-stu-id="333da-190">Enter a label of *person*.</span></span>

9. <span data-ttu-id="333da-191">Click **Add property** to add each of the following properties:</span><span class="sxs-lookup"><span data-stu-id="333da-191">Click **Add property** to add each of the following properties:</span></span>

    <span data-ttu-id="333da-192">key</span><span class="sxs-lookup"><span data-stu-id="333da-192">key</span></span>|<span data-ttu-id="333da-193">value</span><span class="sxs-lookup"><span data-stu-id="333da-193">value</span></span>|<span data-ttu-id="333da-194">Notes</span><span class="sxs-lookup"><span data-stu-id="333da-194">Notes</span></span>
    ----|----|----
    <span data-ttu-id="333da-195">id</span><span class="sxs-lookup"><span data-stu-id="333da-195">id</span></span>|<span data-ttu-id="333da-196">rakesh</span><span class="sxs-lookup"><span data-stu-id="333da-196">rakesh</span></span>|<span data-ttu-id="333da-197">The unique identifier for the vertex.</span><span class="sxs-lookup"><span data-stu-id="333da-197">The unique identifier for the vertex.</span></span> <span data-ttu-id="333da-198">If you don't specify an id, one is generated for you.</span><span class="sxs-lookup"><span data-stu-id="333da-198">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="333da-199">gender</span><span class="sxs-lookup"><span data-stu-id="333da-199">gender</span></span>|<span data-ttu-id="333da-200">male</span><span class="sxs-lookup"><span data-stu-id="333da-200">male</span></span>| 
    <span data-ttu-id="333da-201">school</span><span class="sxs-lookup"><span data-stu-id="333da-201">school</span></span>|<span data-ttu-id="333da-202">MIT</span><span class="sxs-lookup"><span data-stu-id="333da-202">MIT</span></span>| 

10. <span data-ttu-id="333da-203">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="333da-203">Click **OK**.</span></span> 

11. <span data-ttu-id="333da-204">Click the **Apply Filter** button with the default `g.V()` filter to display all the values in the graph.</span><span class="sxs-lookup"><span data-stu-id="333da-204">Click the **Apply Filter** button with the default `g.V()` filter to display all the values in the graph.</span></span> <span data-ttu-id="333da-205">All of the users now show in the **Results** list.</span><span class="sxs-lookup"><span data-stu-id="333da-205">All of the users now show in the **Results** list.</span></span> 

    <span data-ttu-id="333da-206">As you add more data, you can use filters to limit your results.</span><span class="sxs-lookup"><span data-stu-id="333da-206">As you add more data, you can use filters to limit your results.</span></span> <span data-ttu-id="333da-207">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph.</span><span class="sxs-lookup"><span data-stu-id="333da-207">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph.</span></span> <span data-ttu-id="333da-208">You can change it to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span><span class="sxs-lookup"><span data-stu-id="333da-208">You can change it to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span></span> <span data-ttu-id="333da-209">If you changed the filter, change the filter back to `g.V()` and click **Apply Filter** to display all the results again.</span><span class="sxs-lookup"><span data-stu-id="333da-209">If you changed the filter, change the filter back to `g.V()` and click **Apply Filter** to display all the results again.</span></span>

12. <span data-ttu-id="333da-210">Now you can connect rakesh and ashley.</span><span class="sxs-lookup"><span data-stu-id="333da-210">Now you can connect rakesh and ashley.</span></span> <span data-ttu-id="333da-211">Ensure **ashley** is selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span><span class="sxs-lookup"><span data-stu-id="333da-211">Ensure **ashley** is selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span></span> <span data-ttu-id="333da-212">You may need to widen your window to see the **Properties** area.</span><span class="sxs-lookup"><span data-stu-id="333da-212">You may need to widen your window to see the **Properties** area.</span></span>

   ![Change the target of a vertex in a graph](./media/create-graph-php/azure-cosmosdb-data-explorer-edit-target.png)

13. <span data-ttu-id="333da-214">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check.</span><span class="sxs-lookup"><span data-stu-id="333da-214">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check.</span></span>

   ![Add a connection between ashley and rakesh in Data Explorer](./media/create-graph-php/azure-cosmosdb-data-explorer-set-target.png)

14. <span data-ttu-id="333da-216">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span><span class="sxs-lookup"><span data-stu-id="333da-216">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span></span> 

   ![Two vertices connected in Data Explorer](./media/create-graph-php/azure-cosmosdb-graph-explorer.png)

   <span data-ttu-id="333da-218">That completes the resource creation part of this quickstart.</span><span class="sxs-lookup"><span data-stu-id="333da-218">That completes the resource creation part of this quickstart.</span></span> <span data-ttu-id="333da-219">You can continue to add vertexes to your graph, modify the existing vertexes, or change the queries.</span><span class="sxs-lookup"><span data-stu-id="333da-219">You can continue to add vertexes to your graph, modify the existing vertexes, or change the queries.</span></span> <span data-ttu-id="333da-220">Now let's review the metrics Azure Cosmos DB provides, and then clean up the resources.</span><span class="sxs-lookup"><span data-stu-id="333da-220">Now let's review the metrics Azure Cosmos DB provides, and then clean up the resources.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="333da-221">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="333da-221">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="333da-222">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="333da-222">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="333da-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="333da-223">Next steps</span></span>

<span data-ttu-id="333da-224">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span><span class="sxs-lookup"><span data-stu-id="333da-224">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="333da-225">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span><span class="sxs-lookup"><span data-stu-id="333da-225">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md)

