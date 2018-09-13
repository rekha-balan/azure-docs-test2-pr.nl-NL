---
title: Build a Node.js web app for Azure Cosmos DB | Microsoft Docs
description: This Node.js tutorial explores how to use Microsoft Azure Cosmos DB to store and access data from a Node.js Express web application hosted on Azure Websites.
keywords: Application development, database tutorial, learn Node.js, Node.js tutorial
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/31/2018
ms.author: sngun
ms.openlocfilehash: 8e788207e99a87e9635fbf668ad99c21ca101ecf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856485"
---
# <a name="_Toc395783175"></a><span data-ttu-id="d6132-104">Build a Node.js web application using Azure Cosmos DB and Node.js SDK (Preview)</span><span class="sxs-lookup"><span data-stu-id="d6132-104">Build a Node.js web application using Azure Cosmos DB and Node.js SDK (Preview)</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Java](sql-api-java-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Node.js- v2](sql-api-nodejs-application-preview.md)
> * [Python](sql-api-python-application.md)
> * [Xamarin](mobile-apps-with-xamarin.md)
> 

<span data-ttu-id="d6132-111">This Node.js tutorial shows you how to use Azure Cosmos DB SQL API account to store and access data from a Node.js Express application that is hosted on Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="d6132-111">This Node.js tutorial shows you how to use Azure Cosmos DB SQL API account to store and access data from a Node.js Express application that is hosted on Azure Websites.</span></span> <span data-ttu-id="d6132-112">In this tutorial, you will build a simple web-based application (Todo app), that allows you to create, retrieve, and complete tasks.</span><span class="sxs-lookup"><span data-stu-id="d6132-112">In this tutorial, you will build a simple web-based application (Todo app), that allows you to create, retrieve, and complete tasks.</span></span> <span data-ttu-id="d6132-113">The tasks are stored as JSON documents in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6132-113">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="d6132-114">The following image shows a screen shot of the Todo application:</span><span class="sxs-lookup"><span data-stu-id="d6132-114">The following image shows a screen shot of the Todo application:</span></span>

![Screen shot of the My Todo List application created in this Node.js tutorial](./media/sql-api-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="d6132-116">This tutorial demonstrates how to create an Azure Cosmos DB SQL API account using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d6132-116">This tutorial demonstrates how to create an Azure Cosmos DB SQL API account using the Azure portal.</span></span> <span data-ttu-id="d6132-117">You then build and run a web app that is built on the Node.js SDK to create database, container and add items to the container.</span><span class="sxs-lookup"><span data-stu-id="d6132-117">You then build and run a web app that is built on the Node.js SDK to create database, container and add items to the container.</span></span> <span data-ttu-id="d6132-118">This tutorial uses 2.0 version of the Node.js SDK, which is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="d6132-118">This tutorial uses 2.0 version of the Node.js SDK, which is currently in preview.</span></span>

<span data-ttu-id="d6132-119">You can also get the completed sample from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="d6132-119">You can also get the completed sample from [GitHub][GitHub].</span></span> <span data-ttu-id="d6132-120">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span><span class="sxs-lookup"><span data-stu-id="d6132-120">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <a name="_Toc395783176"></a><span data-ttu-id="d6132-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6132-121">Prerequisites</span></span>

<span data-ttu-id="d6132-122">Before following the instructions in this article, you should ensure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="d6132-122">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="d6132-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="d6132-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="d6132-124">[Node.js][Node.js] version 6.10 or higher.</span><span class="sxs-lookup"><span data-stu-id="d6132-124">[Node.js][Node.js] version 6.10 or higher.</span></span>
* <span data-ttu-id="d6132-125">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="d6132-125">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="d6132-126">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="d6132-126">[Git][Git].</span></span>

## <a name="_Toc395637761"></a><span data-ttu-id="d6132-127">Step 1: Create an Azure Cosmos DB database account</span><span class="sxs-lookup"><span data-stu-id="d6132-127">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="d6132-128">Let's start by creating an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d6132-128">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="d6132-129">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="d6132-129">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a><span data-ttu-id="d6132-130">Step 2: Create a new Node.js application</span><span class="sxs-lookup"><span data-stu-id="d6132-130">Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="d6132-131">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="d6132-131">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="d6132-132">Open your favorite terminal, such as the Node.js command prompt.</span><span class="sxs-lookup"><span data-stu-id="d6132-132">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="d6132-133">Navigate to the directory in which you'd like to store the new application.</span><span class="sxs-lookup"><span data-stu-id="d6132-133">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="d6132-134">Use the express generator to generate a new application called **todo**.</span><span class="sxs-lookup"><span data-stu-id="d6132-134">Use the express generator to generate a new application called **todo**.</span></span>

   ```bash
   express todo
   ```
4. <span data-ttu-id="d6132-135">Open your new **todo** directory and install dependencies.</span><span class="sxs-lookup"><span data-stu-id="d6132-135">Open your new **todo** directory and install dependencies.</span></span>

   ```bash
   cd todo
   npm install
   ```
5. <span data-ttu-id="d6132-136">Run your new application.</span><span class="sxs-lookup"><span data-stu-id="d6132-136">Run your new application.</span></span>

   ```bash
   npm start
   ```

6. <span data-ttu-id="d6132-137">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="d6132-137">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Learn Node.js - Screenshot of the Hello World application in a browser window](./media/sql-api-nodejs-application/cosmos-db-node-js-express.png)

 <span data-ttu-id="d6132-139">Stop the application by using CTRL+C in the terminal window and click **y** to terminate the batch job.</span><span class="sxs-lookup"><span data-stu-id="d6132-139">Stop the application by using CTRL+C in the terminal window and click **y** to terminate the batch job.</span></span>

## <a name="_Toc395783179"></a><span data-ttu-id="d6132-140">Step 3: Install the required modules</span><span class="sxs-lookup"><span data-stu-id="d6132-140">Step 3: Install the required modules</span></span>

<span data-ttu-id="d6132-141">The **package.json** file is one of the files created in the root of the project.</span><span class="sxs-lookup"><span data-stu-id="d6132-141">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="d6132-142">This file contains a list of additional modules that are required for your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="d6132-142">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="d6132-143">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span><span class="sxs-lookup"><span data-stu-id="d6132-143">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="d6132-144">You need to install two more packages for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6132-144">You need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="d6132-145">Open the terminal, install the **async** module via npm.</span><span class="sxs-lookup"><span data-stu-id="d6132-145">Open the terminal, install the **async** module via npm.</span></span>

   ```bash
   npm install async --save
   ```

2. <span data-ttu-id="d6132-146">Install the **@azure/cosmos** module via npm.</span><span class="sxs-lookup"><span data-stu-id="d6132-146">Install the **@azure/cosmos** module via npm.</span></span> 

   ```bash
   npm install @azure/cosmos
   ```

## <a name="_Toc395783180"></a><span data-ttu-id="d6132-147">Step 4: Using the Azure Cosmos DB service in a Node application</span><span class="sxs-lookup"><span data-stu-id="d6132-147">Step 4: Using the Azure Cosmos DB service in a Node application</span></span>
<span data-ttu-id="d6132-148">Now that you have completed the initial setup and configuration, next you will write code that is required by the todo application to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6132-148">Now that you have completed the initial setup and configuration, next you will write code that is required by the todo application to communicate with Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="d6132-149">Create the model</span><span class="sxs-lookup"><span data-stu-id="d6132-149">Create the model</span></span>
1. <span data-ttu-id="d6132-150">At the root of your project directory, create a new directory named **models**</span><span class="sxs-lookup"><span data-stu-id="d6132-150">At the root of your project directory, create a new directory named **models**</span></span>  

2. <span data-ttu-id="d6132-151">In the **models** directory, create a new file named **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="d6132-151">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="d6132-152">This file contains code required to create the database, container and defines methods to read, update, create, and find tasks in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6132-152">This file contains code required to create the database, container and defines methods to read, update, create, and find tasks in Azure Cosmos DB.</span></span> 

3. <span data-ttu-id="d6132-153">Copy the following code in to **taskDao.js** file</span><span class="sxs-lookup"><span data-stu-id="d6132-153">Copy the following code in to **taskDao.js** file</span></span>

   ```nodejs
   // @ts-check
   const CosmosClient = require("@azure/cosmos").CosmosClient;
   const debug = require("debug")("todo:taskDao");
   class TaskDao {
     /**
      * Manages reading, adding, and updating Tasks in Cosmos DB
      * @param {CosmosClient} cosmosClient
      * @param {string} databaseId
      * @param {string} containerId
      */
     constructor(cosmosClient, databaseId, containerId) {
       this.client = cosmosClient;
       this.databaseId = databaseId;
       this.collectionId = containerId;

       this.database = null;
       this.container = null;
     }

     async init() {
       debug("Setting up the database...");
       const dbResponse = await this.client.databases.createIfNotExists({
         id: this.databaseId
       });
       this.database = dbResponse.database;
       debug("Setting up the database...done!");
       debug("Setting up the container...");
       const coResponse = await this.database.containers.createIfNotExists({
         id: this.collectionId
       });
       this.container = coResponse.container;
       debug("Setting up the container...done!");
     }

     async find(querySpec) {
       debug("Querying for items from the database");
       if (!this.container) {
         throw new Error("Collection is not initialized.");
       }
       const { result: results } = await this.container.items
        .query(querySpec)
        .toArray();
      return results;
    }

    async addItem(item) {
      debug("Adding an item to the database");
      item.date = Date.now();
      item.completed = false;
      const { body: doc } = await this.container.items.create(item);
      return doc;
    }

    async updateItem(itemId) {
      debug("Update an item in the database");
      const doc = await this.getItem(itemId);
      doc.completed = true;

      const { body: replaced } = await this.container.item(itemId).replace(doc);
      return replaced;
    }

    async getItem(itemId) {
      debug("Getting an item from the database");
      const { body } = await this.container.item(itemId).read();
      return body;
    }
  }

   module.exports = TaskDao;
   ```
4. <span data-ttu-id="d6132-154">Save and close the **taskDao.js** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-154">Save and close the **taskDao.js** file.</span></span>  

### <a name="create-the-controller"></a><span data-ttu-id="d6132-155">Create the controller</span><span class="sxs-lookup"><span data-stu-id="d6132-155">Create the controller</span></span>

1. <span data-ttu-id="d6132-156">In the **routes** directory of your project, create a new file named **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="d6132-156">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span>  

2. <span data-ttu-id="d6132-157">Add the following code to **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="d6132-157">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="d6132-158">This loads the CosmosClient and async modules, which are used by **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="d6132-158">This loads the CosmosClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="d6132-159">This also defines the **TaskList** class, which is passed as an instance of the **TaskDao** object we defined earlier:</span><span class="sxs-lookup"><span data-stu-id="d6132-159">This also defines the **TaskList** class, which is passed as an instance of the **TaskDao** object we defined earlier:</span></span>
   
   ```nodejs
   const TaskDao = require("../models/TaskDao");

   class TaskList {
     /**
      * Handles the various APIs for displaying and managing tasks
      * @param {TaskDao} taskDao
     */
    constructor(taskDao) {
    this.taskDao = taskDao;
    }
    async showTasks(req, res) {
      const querySpec = {
        query: "SELECT * FROM root r WHERE r.completed=@completed",
        parameters: [
          {
            name: "@completed",
            value: false
          }
        ]
      };

      const items = await this.taskDao.find(querySpec);
      res.render("index", {
        title: "My ToDo List ",
        tasks: items
      });
    }

    async addTask(req, res) {
      const item = req.body;

      await this.taskDao.addItem(item);
      res.redirect("/");
    }

    async completeTask(req, res) {
      const completedTasks = Object.keys(req.body);
      const tasks = [];

      completedTasks.forEach(task => {
        tasks.push(this.taskDao.updateItem(task));
      });

      await Promise.all(tasks);

      res.redirect("/");
    }
  }

  module.exports = TaskList;
   ```

3. <span data-ttu-id="d6132-160">Save and close the **tasklist.js** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-160">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="d6132-161">Add config.js</span><span class="sxs-lookup"><span data-stu-id="d6132-161">Add config.js</span></span>

1. <span data-ttu-id="d6132-162">At the root of your project directory, create a new file named **config.js**.</span><span class="sxs-lookup"><span data-stu-id="d6132-162">At the root of your project directory, create a new file named **config.js**.</span></span> 

2. <span data-ttu-id="d6132-163">Add the following code to **config.js** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-163">Add the following code to **config.js** file.</span></span> <span data-ttu-id="d6132-164">This code defines configuration settings and values needed for our application.</span><span class="sxs-lookup"><span data-stu-id="d6132-164">This code defines configuration settings and values needed for our application.</span></span>
   
   ```nodejs
   const config = {};

   config.host = process.env.HOST || "[the endpoint URI of your Azure Cosmos DB account]";
   config.authKey =
     process.env.AUTH_KEY || "[the PRIMARY KEY value of your Azure Cosmos DB account";
   config.databaseId = "ToDoList";
   config.containerId = "Items";

   if (config.host.includes("https://localhost:")) {
     console.log("Local environment detected");
     console.log("WARNING: Disabled checking of self-signed certs. Do not have this code in production.");
     process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";
     console.log(`Go to http://localhost:${process.env.PORT || '3000'} to try the sample.`);
   }

   module.exports = config;
   ```

3. <span data-ttu-id="d6132-165">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys page of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6132-165">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys page of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span> 

4. <span data-ttu-id="d6132-166">Save and close the **config.js** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-166">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="d6132-167">Modify app.js</span><span class="sxs-lookup"><span data-stu-id="d6132-167">Modify app.js</span></span>
1. <span data-ttu-id="d6132-168">In the project directory, open the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-168">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="d6132-169">This file was created earlier when the Express web application was created.</span><span class="sxs-lookup"><span data-stu-id="d6132-169">This file was created earlier when the Express web application was created.</span></span>  

2. <span data-ttu-id="d6132-170">Add the following code to the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-170">Add the following code to the **app.js** file.</span></span> <span data-ttu-id="d6132-171">This code defines the config file to be used, and proceeds to read values out of this file into some variables which we will use soon.</span><span class="sxs-lookup"><span data-stu-id="d6132-171">This code defines the config file to be used, and proceeds to read values out of this file into some variables which we will use soon.</span></span> 
   
   ```nodejs
   const CosmosClient = require("@azure/cosmos").CosmosClient;
   const config = require("./config");
   const TaskList = require("./routes/tasklist");
   const TaskDao = require("./models/taskDao");

   const express = require("express");
   const path = require("path");
   const logger = require("morgan");
   const cookieParser = require("cookie-parser");
   const bodyParser = require("body-parser");

   const app = express();

   // view engine setup
   app.set("views", path.join(__dirname, "views"));
   app.set("view engine", "jade");

   // uncomment after placing your favicon in /public
   //app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')));
   app.use(logger("dev"));
   app.use(bodyParser.json());
   app.use(bodyParser.urlencoded({ extended: false }));
   app.use(cookieParser());
   app.use(express.static(path.join(__dirname, "public")));

   //Todo App:
   const cosmosClient = new CosmosClient({
     endpoint: config.host,
     auth: {
       masterKey: config.authKey
     }
   });
   const taskDao = new TaskDao(cosmosClient, config.databaseId, config.containerId);
   const taskList = new TaskList(taskDao);
   taskDao
     .init(err => {
       console.error(err);
     })
     .catch(err => {
       console.error(err);
       console.error("Shutting down because there was an error settinig up the database.");
       process.exit(1);
     });

   app.get("/", (req, res, next) => taskList.showTasks(req, res).catch(next));
   app.post("/addtask", (req, res, next) => taskList.addTask(req, res).catch(next));
   app.post("/completetask", (req, res, next) => taskList.completeTask(req, res).catch(next));
   app.set("view engine", "jade");

   // catch 404 and forward to error handler
   app.use(function(req, res, next) {
     const err = new Error("Not Found");
     err.status = 404;
     next(err);
   });

   // error handler
   app.use(function(err, req, res, next) {
     // set locals, only providing error in development
     res.locals.message = err.message;
     res.locals.error = req.app.get("env") === "development" ? err : {};

     // render the error page
     res.status(err.status || 500);
     res.render("error");
   });

   module.exports = app;
   ```

3. <span data-ttu-id="d6132-172">Finally, save and close the **app.js** file, we're just about done.</span><span class="sxs-lookup"><span data-stu-id="d6132-172">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <a name="_Toc395783181"></a><span data-ttu-id="d6132-173">Step 5: Build a user interface</span><span class="sxs-lookup"><span data-stu-id="d6132-173">Step 5: Build a user interface</span></span>
<span data-ttu-id="d6132-174">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span><span class="sxs-lookup"><span data-stu-id="d6132-174">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="d6132-175">The Express application we created uses **Jade** as the view engine.</span><span class="sxs-lookup"><span data-stu-id="d6132-175">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="d6132-176">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="d6132-176">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="d6132-177">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span><span class="sxs-lookup"><span data-stu-id="d6132-177">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="d6132-178">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span><span class="sxs-lookup"><span data-stu-id="d6132-178">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>  

2. <span data-ttu-id="d6132-179">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span><span class="sxs-lookup"><span data-stu-id="d6132-179">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

   ```html
   doctype html
   html
     head
       title= title
       link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
       link(rel='stylesheet', href='/stylesheets/style.css')
     body
       nav.navbar.navbar-inverse.navbar-fixed-top
         div.navbar-header
           a.navbar-brand(href='#') My Tasks
       block content
       script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
       script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
   ```

    <span data-ttu-id="d6132-180">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span><span class="sxs-lookup"><span data-stu-id="d6132-180">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="d6132-181">Save and close this **layout.jade** file.</span><span class="sxs-lookup"><span data-stu-id="d6132-181">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="d6132-182">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span><span class="sxs-lookup"><span data-stu-id="d6132-182">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>

   ```html
   extends layout
   block content
        h1 #{title}
        br
        
        form(action="/completetask", method="post")
         table.table.table-striped.table-bordered
            tr
              td Name
              td Category
              td Date
              td Complete
            if (typeof tasks === "undefined")
              tr
                td
            else
              each task in tasks
                tr
                  td #{task.name}
                  td #{task.category}
                  - var date  = new Date(task.date);
                  - var day   = date.getDate();
                  - var month = date.getMonth() + 1;
                  - var year  = date.getFullYear();
                  td #{month + "/" + day + "/" + year}
                  td
                   if(task.completed) 
                    input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
                   else
                    input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
          button.btn.btn-primary(type="submit") Update tasks
        hr
        form.well(action="/addtask", method="post")
          label Item Name:
          input(name="name", type="textbox")
          label Item Category:
          input(name="category", type="textbox")
          br
          button.btn(type="submit") Add item
   ```

<span data-ttu-id="d6132-183">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span><span class="sxs-lookup"><span data-stu-id="d6132-183">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="d6132-184">In this layout we created two HTML forms.</span><span class="sxs-lookup"><span data-stu-id="d6132-184">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="d6132-185">The first form contains a table for our data and a button that allows us to update items by posting to **/completeTask** method of our controller.</span><span class="sxs-lookup"><span data-stu-id="d6132-185">The first form contains a table for our data and a button that allows us to update items by posting to **/completeTask** method of our controller.</span></span>
    
<span data-ttu-id="d6132-186">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span><span class="sxs-lookup"><span data-stu-id="d6132-186">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="d6132-187">This should be all that we need for our application to work.</span><span class="sxs-lookup"><span data-stu-id="d6132-187">This should be all that we need for our application to work.</span></span>

## <a name="_Toc395783181"></a><span data-ttu-id="d6132-188">Step 6: Run your application locally</span><span class="sxs-lookup"><span data-stu-id="d6132-188">Step 6: Run your application locally</span></span>
1. <span data-ttu-id="d6132-189">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span><span class="sxs-lookup"><span data-stu-id="d6132-189">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="d6132-190">The page should now look like the image below:</span><span class="sxs-lookup"><span data-stu-id="d6132-190">The page should now look like the image below:</span></span>
   
    ![Screenshot of the MyTodo List application in a browser window](./media/sql-api-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces. If there are spaces before the first two lines, remove them, save both files, then refresh your browser window. 

2. <span data-ttu-id="d6132-194">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span><span class="sxs-lookup"><span data-stu-id="d6132-194">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="d6132-195">This creates a document in Azure Cosmos DB with those properties.</span><span class="sxs-lookup"><span data-stu-id="d6132-195">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="d6132-196">The page should update to display the newly created item in the ToDo list.</span><span class="sxs-lookup"><span data-stu-id="d6132-196">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![Screenshot of the application with a new item in the ToDo list](./media/sql-api-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="d6132-198">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span><span class="sxs-lookup"><span data-stu-id="d6132-198">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="d6132-199">This updates the document you already created and removes it from the view.</span><span class="sxs-lookup"><span data-stu-id="d6132-199">This updates the document you already created and removes it from the view.</span></span>

5. <span data-ttu-id="d6132-200">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span><span class="sxs-lookup"><span data-stu-id="d6132-200">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <a name="_Toc395783182"></a><span data-ttu-id="d6132-201">Step 7: Deploy your application development project to Azure Websites</span><span class="sxs-lookup"><span data-stu-id="d6132-201">Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="d6132-202">If you haven't already, enable a git repository for your Azure Website.</span><span class="sxs-lookup"><span data-stu-id="d6132-202">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="d6132-203">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service/app-service-deploy-local-git.md) topic.</span><span class="sxs-lookup"><span data-stu-id="d6132-203">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="d6132-204">Add your Azure Website as a git remote.</span><span class="sxs-lookup"><span data-stu-id="d6132-204">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="d6132-205">Deploy by pushing to the remote.</span><span class="sxs-lookup"><span data-stu-id="d6132-205">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="d6132-206">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span><span class="sxs-lookup"><span data-stu-id="d6132-206">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="d6132-207">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="d6132-207">Congratulations!</span></span> <span data-ttu-id="d6132-208">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="d6132-208">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="d6132-209">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="d6132-209">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <a name="_Toc395637775"></a><span data-ttu-id="d6132-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6132-210">Next steps</span></span>

* <span data-ttu-id="d6132-211">Want to perform scale and performance testing with Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d6132-211">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="d6132-212">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="d6132-212">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="d6132-213">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="d6132-213">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="d6132-214">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="d6132-214">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="d6132-215">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d6132-215">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/azure-cosmos-db-sql-api-nodejs-todo-app

