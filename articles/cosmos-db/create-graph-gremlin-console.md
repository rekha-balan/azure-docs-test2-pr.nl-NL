---
title: 'Azure Cosmos DB tutorial: Create, query, and traverse in Apache TinkerPops Gremlin Console | Microsoft Docs'
description: An Azure Cosmos DB quickstart to creates vertices, edges, and queries using the Azure Cosmos DB Gremlin API.
services: cosmos-db
author: luisbosquez
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.devlang: na
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lbosq
ms.openlocfilehash: 905873a695635ba80de258cbf458c8dd3e18d443
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856087"
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-the-gremlin-console"></a><span data-ttu-id="56460-103">Azure Cosmos DB: Create, query, and traverse a graph in the Gremlin console</span><span class="sxs-lookup"><span data-stu-id="56460-103">Azure Cosmos DB: Create, query, and traverse a graph in the Gremlin console</span></span>

> [!div class="op_single_selector"]
> * [Gremlin console](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

<span data-ttu-id="56460-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="56460-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="56460-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56460-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="56460-112">This quick start demonstrates how to create an Azure Cosmos DB [Gremlin API](graph-introduction.md) account, database, and graph (container) using the Azure portal and then use the [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) to work with Gremlin API data.</span><span class="sxs-lookup"><span data-stu-id="56460-112">This quick start demonstrates how to create an Azure Cosmos DB [Gremlin API](graph-introduction.md) account, database, and graph (container) using the Azure portal and then use the [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) to work with Gremlin API data.</span></span> <span data-ttu-id="56460-113">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse the graph, and drop a vertex.</span><span class="sxs-lookup"><span data-stu-id="56460-113">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse the graph, and drop a vertex.</span></span>

![Azure Cosmos DB from the Apache Gremlin console](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="56460-115">The Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span><span class="sxs-lookup"><span data-stu-id="56460-115">The Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="56460-116">You can download it from the [Apache TinkerPop site](http://tinkerpop.apache.org/downloads.html).</span><span class="sxs-lookup"><span data-stu-id="56460-116">You can download it from the [Apache TinkerPop site](http://tinkerpop.apache.org/downloads.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56460-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="56460-117">Prerequisites</span></span>

<span data-ttu-id="56460-118">You need to have an Azure subscription to create an Azure Cosmos DB account for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="56460-118">You need to have an Azure subscription to create an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="56460-119">You also need to install the [Gremlin Console](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="56460-119">You also need to install the [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="56460-120">Use version 3.2.5 or above.</span><span class="sxs-lookup"><span data-stu-id="56460-120">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="56460-121">Create a database account</span><span class="sxs-lookup"><span data-stu-id="56460-121">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="56460-122">Add a graph</span><span class="sxs-lookup"><span data-stu-id="56460-122">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a id="ConnectAppService"></a><span data-ttu-id="56460-123">Connect to your app service</span><span class="sxs-lookup"><span data-stu-id="56460-123">Connect to your app service</span></span>
1. <span data-ttu-id="56460-124">Before starting the Gremlin Console, create or modify the remote-secure.yaml configuration file in the `apache-tinkerpop-gremlin-console-3.2.5/conf` directory.</span><span class="sxs-lookup"><span data-stu-id="56460-124">Before starting the Gremlin Console, create or modify the remote-secure.yaml configuration file in the `apache-tinkerpop-gremlin-console-3.2.5/conf` directory.</span></span>
2. <span data-ttu-id="56460-125">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations as defined in the following table:</span><span class="sxs-lookup"><span data-stu-id="56460-125">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations as defined in the following table:</span></span>

    <span data-ttu-id="56460-126">Setting</span><span class="sxs-lookup"><span data-stu-id="56460-126">Setting</span></span>|<span data-ttu-id="56460-127">Suggested value</span><span class="sxs-lookup"><span data-stu-id="56460-127">Suggested value</span></span>|<span data-ttu-id="56460-128">Description</span><span class="sxs-lookup"><span data-stu-id="56460-128">Description</span></span>
    ---|---|---
    <span data-ttu-id="56460-129">hosts</span><span class="sxs-lookup"><span data-stu-id="56460-129">hosts</span></span>|<span data-ttu-id="56460-130">[*account-name*.gremlin.cosmosdb.azure.com] or [*account-name*.graphs.azure.com] for accounts created before December 20th, 2017</span><span class="sxs-lookup"><span data-stu-id="56460-130">[*account-name*.gremlin.cosmosdb.azure.com] or [*account-name*.graphs.azure.com] for accounts created before December 20th, 2017</span></span>|<span data-ttu-id="56460-131">See the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="56460-131">See the following screenshot.</span></span> <span data-ttu-id="56460-132">This is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span><span class="sxs-lookup"><span data-stu-id="56460-132">This is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span>
    <span data-ttu-id="56460-133">port</span><span class="sxs-lookup"><span data-stu-id="56460-133">port</span></span>|<span data-ttu-id="56460-134">443</span><span class="sxs-lookup"><span data-stu-id="56460-134">443</span></span>|<span data-ttu-id="56460-135">Set to 443.</span><span class="sxs-lookup"><span data-stu-id="56460-135">Set to 443.</span></span>
    <span data-ttu-id="56460-136">username</span><span class="sxs-lookup"><span data-stu-id="56460-136">username</span></span>|<span data-ttu-id="56460-137">*Your username*</span><span class="sxs-lookup"><span data-stu-id="56460-137">*Your username*</span></span>|<span data-ttu-id="56460-138">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span><span class="sxs-lookup"><span data-stu-id="56460-138">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="56460-139">password</span><span class="sxs-lookup"><span data-stu-id="56460-139">password</span></span>|<span data-ttu-id="56460-140">*Your primary key*</span><span class="sxs-lookup"><span data-stu-id="56460-140">*Your primary key*</span></span>| <span data-ttu-id="56460-141">See second screenshot below.</span><span class="sxs-lookup"><span data-stu-id="56460-141">See second screenshot below.</span></span> <span data-ttu-id="56460-142">This is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span><span class="sxs-lookup"><span data-stu-id="56460-142">This is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="56460-143">Use the copy button on the left side of the box to copy the value.</span><span class="sxs-lookup"><span data-stu-id="56460-143">Use the copy button on the left side of the box to copy the value.</span></span>
    <span data-ttu-id="56460-144">connectionPool</span><span class="sxs-lookup"><span data-stu-id="56460-144">connectionPool</span></span>|<span data-ttu-id="56460-145">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="56460-145">{enableSsl: true}</span></span>|<span data-ttu-id="56460-146">Your connection pool setting for SSL.</span><span class="sxs-lookup"><span data-stu-id="56460-146">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="56460-147">serializer</span><span class="sxs-lookup"><span data-stu-id="56460-147">serializer</span></span>|<span data-ttu-id="56460-148">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="56460-148">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="56460-149">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="56460-149">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="56460-150">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="56460-150">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="56460-151">Set to this value and delete any `\n` line breaks when pasting in the value.</span><span class="sxs-lookup"><span data-stu-id="56460-151">Set to this value and delete any `\n` line breaks when pasting in the value.</span></span>

    <span data-ttu-id="56460-152">For the hosts value, copy the **Gremlin URI** value from the **Overview** page: ![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="56460-152">For the hosts value, copy the **Gremlin URI** value from the **Overview** page: ![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="56460-153">For the password value, copy the **Primary key** from the **Keys** page: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="56460-153">For the password value, copy the **Primary key** from the **Keys** page: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>

<span data-ttu-id="56460-154">Your remote-secure.yaml file should look like this:</span><span class="sxs-lookup"><span data-stu-id="56460-154">Your remote-secure.yaml file should look like this:</span></span>

```
hosts: [your_database_server.gremlin.cosmosdb.azure.com]
port: 443
username: /dbs/your_database_account/colls/your_collection
password: your_primary_key
connectionPool: {
  enableSsl: true
}
serializer: { className: org.apache.tinkerpop.gremlin.driver.ser.GraphSONMessageSerializerV1d0, config: { serializeResultToString: true }}
```

3. <span data-ttu-id="56460-155">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` to start the [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="56460-155">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` to start the [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="56460-156">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` to connect to your app service.</span><span class="sxs-lookup"><span data-stu-id="56460-156">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` to connect to your app service.</span></span>

    > [!TIP]
    > If you receive the error `No appenders could be found for logger` ensure that you updated the serializer value in the remote-secure.yaml file as described in step 2. 

5. <span data-ttu-id="56460-158">Next run `:remote console` to redirect all console commands to the remote server.</span><span class="sxs-lookup"><span data-stu-id="56460-158">Next run `:remote console` to redirect all console commands to the remote server.</span></span>

<span data-ttu-id="56460-159">Great!</span><span class="sxs-lookup"><span data-stu-id="56460-159">Great!</span></span> <span data-ttu-id="56460-160">Now that we finished the setup, let's start running some console commands.</span><span class="sxs-lookup"><span data-stu-id="56460-160">Now that we finished the setup, let's start running some console commands.</span></span>

<span data-ttu-id="56460-161">Let's try a simple count() command.</span><span class="sxs-lookup"><span data-stu-id="56460-161">Let's try a simple count() command.</span></span> <span data-ttu-id="56460-162">Type the following into the console at the prompt:</span><span class="sxs-lookup"><span data-stu-id="56460-162">Type the following into the console at the prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> Notice the `:>` that precedes the `g.V().count()` text? 
>
> This is part of the command you need to type. It is important when using the Gremlin console, with Azure Cosmos DB.  
>
> Omitting this `:>` prefix instructs the console to execute the command locally, often against an in-memory graph.
> Using this `:>` tells the console to execute a remote command, in this case against Cosmos DB (either the localhost emulator, or an > Azure instance).


## <a name="create-vertices-and-edges"></a><span data-ttu-id="56460-168">Create vertices and edges</span><span class="sxs-lookup"><span data-stu-id="56460-168">Create vertices and edges</span></span>

<span data-ttu-id="56460-169">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span><span class="sxs-lookup"><span data-stu-id="56460-169">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="56460-170">Input (Thomas):</span><span class="sxs-lookup"><span data-stu-id="56460-170">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="56460-171">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-171">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="56460-172">Input (Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="56460-172">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="56460-173">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-173">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="56460-174">Input (Robin):</span><span class="sxs-lookup"><span data-stu-id="56460-174">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="56460-175">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-175">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="56460-176">Input (Ben):</span><span class="sxs-lookup"><span data-stu-id="56460-176">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="56460-177">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-177">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="56460-178">Input (Jack):</span><span class="sxs-lookup"><span data-stu-id="56460-178">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="56460-179">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-179">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="56460-180">Next, let's add edges for relationships between our people.</span><span class="sxs-lookup"><span data-stu-id="56460-180">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="56460-181">Input (Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="56460-181">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="56460-182">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-182">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="56460-183">Input (Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="56460-183">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="56460-184">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-184">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="56460-185">Input (Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="56460-185">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="56460-186">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-186">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="56460-187">Update a vertex</span><span class="sxs-lookup"><span data-stu-id="56460-187">Update a vertex</span></span>

<span data-ttu-id="56460-188">Let's update the *Thomas* vertex with a new age of *45*.</span><span class="sxs-lookup"><span data-stu-id="56460-188">Let's update the *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="56460-189">Input:</span><span class="sxs-lookup"><span data-stu-id="56460-189">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="56460-190">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-190">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="56460-191">Query your graph</span><span class="sxs-lookup"><span data-stu-id="56460-191">Query your graph</span></span>

<span data-ttu-id="56460-192">Now, let's run a variety of queries against your graph.</span><span class="sxs-lookup"><span data-stu-id="56460-192">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="56460-193">First, let's try a query with a filter to return only people who are older than 40 years old.</span><span class="sxs-lookup"><span data-stu-id="56460-193">First, let's try a query with a filter to return only people who are older than 40 years old.</span></span>

<span data-ttu-id="56460-194">Input (filter query):</span><span class="sxs-lookup"><span data-stu-id="56460-194">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="56460-195">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-195">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="56460-196">Next, let's project the first name for the people who are older than 40 years old.</span><span class="sxs-lookup"><span data-stu-id="56460-196">Next, let's project the first name for the people who are older than 40 years old.</span></span>

<span data-ttu-id="56460-197">Input (filter + projection query):</span><span class="sxs-lookup"><span data-stu-id="56460-197">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="56460-198">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-198">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="56460-199">Traverse your graph</span><span class="sxs-lookup"><span data-stu-id="56460-199">Traverse your graph</span></span>

<span data-ttu-id="56460-200">Let's traverse the graph to return all of Thomas's friends.</span><span class="sxs-lookup"><span data-stu-id="56460-200">Let's traverse the graph to return all of Thomas's friends.</span></span>

<span data-ttu-id="56460-201">Input (friends of Thomas):</span><span class="sxs-lookup"><span data-stu-id="56460-201">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="56460-202">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-202">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="56460-203">Next, let's get the next layer of vertices.</span><span class="sxs-lookup"><span data-stu-id="56460-203">Next, let's get the next layer of vertices.</span></span> <span data-ttu-id="56460-204">Traverse the graph to return all the friends of Thomas's friends.</span><span class="sxs-lookup"><span data-stu-id="56460-204">Traverse the graph to return all the friends of Thomas's friends.</span></span>

<span data-ttu-id="56460-205">Input (friends of friends of Thomas):</span><span class="sxs-lookup"><span data-stu-id="56460-205">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="56460-206">Output:</span><span class="sxs-lookup"><span data-stu-id="56460-206">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="56460-207">Drop a vertex</span><span class="sxs-lookup"><span data-stu-id="56460-207">Drop a vertex</span></span>

<span data-ttu-id="56460-208">Let's now delete a vertex from the graph database.</span><span class="sxs-lookup"><span data-stu-id="56460-208">Let's now delete a vertex from the graph database.</span></span>

<span data-ttu-id="56460-209">Input (drop Jack vertex):</span><span class="sxs-lookup"><span data-stu-id="56460-209">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="56460-210">Clear your graph</span><span class="sxs-lookup"><span data-stu-id="56460-210">Clear your graph</span></span>

<span data-ttu-id="56460-211">Finally, let's clear the database of all vertices and edges.</span><span class="sxs-lookup"><span data-stu-id="56460-211">Finally, let's clear the database of all vertices and edges.</span></span>

<span data-ttu-id="56460-212">Input:</span><span class="sxs-lookup"><span data-stu-id="56460-212">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="56460-213">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="56460-213">Congratulations!</span></span> <span data-ttu-id="56460-214">You've completed this Azure Cosmos DB: Gremlin API tutorial!</span><span class="sxs-lookup"><span data-stu-id="56460-214">You've completed this Azure Cosmos DB: Gremlin API tutorial!</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="56460-215">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="56460-215">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="56460-216">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="56460-216">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="56460-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="56460-217">Next steps</span></span>

<span data-ttu-id="56460-218">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, create vertices and edges, and traverse your graph using the Gremlin console.</span><span class="sxs-lookup"><span data-stu-id="56460-218">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, create vertices and edges, and traverse your graph using the Gremlin console.</span></span> <span data-ttu-id="56460-219">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span><span class="sxs-lookup"><span data-stu-id="56460-219">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md)
