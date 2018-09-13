---
title: Build a Node.js web app for Azure Cosmos DB | Microsoft Docs
description: This Node.js tutorial explores how to use Microsoft Azure Cosmos DB to store and access data from a Node.js Express web application hosted on Azure Websites.
keywords: Application development, database tutorial, learn node.js, node.js tutorial
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/23/2018
ms.author: sngun
ms.openlocfilehash: f7f41e9d77e0687c6c8b25a4163348a7310aa40c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868809"
---
# <a name="_Toc395783175"></a><span data-ttu-id="e0850-104">Build a Node.js web application using Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e0850-104">Build a Node.js web application using Azure Cosmos DB</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Java](sql-api-java-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Node.js- v2](sql-api-nodejs-application-preview.md)
> * [Python](sql-api-python-application.md)
> * [Xamarin](mobile-apps-with-xamarin.md)
> 

<span data-ttu-id="e0850-111">This Node.js tutorial shows you how to use Azure Cosmos DB and the SQL API to store and access data from a Node.js Express application hosted on Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="e0850-111">This Node.js tutorial shows you how to use Azure Cosmos DB and the SQL API to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="e0850-112">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span><span class="sxs-lookup"><span data-stu-id="e0850-112">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="e0850-113">The tasks are stored as JSON documents in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0850-113">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="e0850-114">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span><span class="sxs-lookup"><span data-stu-id="e0850-114">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![Screen shot of the My Todo List application created in this Node.js tutorial](./media/sql-api-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="e0850-116">Don't have time to complete the tutorial and just want to get the complete solution?</span><span class="sxs-lookup"><span data-stu-id="e0850-116">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="e0850-117">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e0850-117">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="e0850-118">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span><span class="sxs-lookup"><span data-stu-id="e0850-118">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <a name="_Toc395783176"></a><span data-ttu-id="e0850-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0850-119">Prerequisites</span></span>
> [!TIP]
> This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.
> 
> 

<span data-ttu-id="e0850-121">Before following the instructions in this article, you should ensure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="e0850-121">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="e0850-122">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e0850-122">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="e0850-123">[Node.js][Node.js] version v0.10.29 or higher.</span><span class="sxs-lookup"><span data-stu-id="e0850-123">[Node.js][Node.js] version v0.10.29 or higher.</span></span> <span data-ttu-id="e0850-124">We recommend Node.js 6.10 or higher.</span><span class="sxs-lookup"><span data-stu-id="e0850-124">We recommend Node.js 6.10 or higher.</span></span>
* <span data-ttu-id="e0850-125">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="e0850-125">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="e0850-126">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="e0850-126">[Git][Git].</span></span>

## <a name="_Toc395637761"></a><span data-ttu-id="e0850-127">Step 1: Create an Azure Cosmos DB database account</span><span class="sxs-lookup"><span data-stu-id="e0850-127">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="e0850-128">Let's start by creating an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="e0850-128">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="e0850-129">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="e0850-129">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a><span data-ttu-id="e0850-130">Step 2: Create a new Node.js application</span><span class="sxs-lookup"><span data-stu-id="e0850-130">Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="e0850-131">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="e0850-131">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="e0850-132">Open your favorite terminal, such as the Node.js command prompt.</span><span class="sxs-lookup"><span data-stu-id="e0850-132">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="e0850-133">Navigate to the directory in which you'd like to store the new application.</span><span class="sxs-lookup"><span data-stu-id="e0850-133">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="e0850-134">Use the express generator to generate a new application called **todo**.</span><span class="sxs-lookup"><span data-stu-id="e0850-134">Use the express generator to generate a new application called **todo**.</span></span>

   ```bash
   express todo
   ```
4. <span data-ttu-id="e0850-135">Open your new **todo** directory and install dependencies.</span><span class="sxs-lookup"><span data-stu-id="e0850-135">Open your new **todo** directory and install dependencies.</span></span>

   ```bash
    cd todo
    npm install
   ```
5. <span data-ttu-id="e0850-136">Run your new application.</span><span class="sxs-lookup"><span data-stu-id="e0850-136">Run your new application.</span></span>

   ```bash
   npm start
   ```
6. <span data-ttu-id="e0850-137">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="e0850-137">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Learn Node.js - Screenshot of the Hello World application in a browser window](./media/sql-api-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="e0850-139">Then, to stop the application, press CTRL+C in the terminal window and then, on Windows machines only, click **y** to terminate the batch job.</span><span class="sxs-lookup"><span data-stu-id="e0850-139">Then, to stop the application, press CTRL+C in the terminal window and then, on Windows machines only, click **y** to terminate the batch job.</span></span>

## <a name="_Toc395783179"></a><span data-ttu-id="e0850-140">Step 3: Install additional modules</span><span class="sxs-lookup"><span data-stu-id="e0850-140">Step 3: Install additional modules</span></span>
<span data-ttu-id="e0850-141">The **package.json** file is one of the files created in the root of the project.</span><span class="sxs-lookup"><span data-stu-id="e0850-141">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="e0850-142">This file contains a list of additional modules that are required for your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="e0850-142">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="e0850-143">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span><span class="sxs-lookup"><span data-stu-id="e0850-143">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="e0850-144">We still need to install two more packages for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0850-144">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="e0850-145">Back in the terminal, install the **async** module via npm.</span><span class="sxs-lookup"><span data-stu-id="e0850-145">Back in the terminal, install the **async** module via npm.</span></span>

   ```bash
   npm install async --save
   ```
2. <span data-ttu-id="e0850-146">Install the **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="e0850-146">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="e0850-147">This is the module where all the Azure Cosmos DB magic happens.</span><span class="sxs-lookup"><span data-stu-id="e0850-147">This is the module where all the Azure Cosmos DB magic happens.</span></span>

   ```bash
   npm install documentdb --save
   ```

## <a name="_Toc395783180"></a><span data-ttu-id="e0850-148">Step 4: Using the Azure Cosmos DB service in a node application</span><span class="sxs-lookup"><span data-stu-id="e0850-148">Step 4: Using the Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="e0850-149">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0850-149">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="e0850-150">Create the model</span><span class="sxs-lookup"><span data-stu-id="e0850-150">Create the model</span></span>
1. <span data-ttu-id="e0850-151">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span><span class="sxs-lookup"><span data-stu-id="e0850-151">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="e0850-152">In the **models** directory, create a new file named **task-model.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-152">In the **models** directory, create a new file named **task-model.js**.</span></span> <span data-ttu-id="e0850-153">This file will contain the model for the tasks created by our application.</span><span class="sxs-lookup"><span data-stu-id="e0850-153">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="e0850-154">In the same **models** directory, create another new file named **cosmosdb-manager.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-154">In the same **models** directory, create another new file named **cosmosdb-manager.js**.</span></span> <span data-ttu-id="e0850-155">This file will contain some useful, reusable, code that we will use throughout our application.</span><span class="sxs-lookup"><span data-stu-id="e0850-155">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="e0850-156">Copy the following code in to **cosmosdb-manager.js**</span><span class="sxs-lookup"><span data-stu-id="e0850-156">Copy the following code in to **cosmosdb-manager.js**</span></span>
    ```nodejs
    let DocumentDBClient = require('documentdb').DocumentClient;

    module.exports = {
    getOrCreateDatabase: (client, databaseId, callback) => {
        let querySpec = {
        query: 'SELECT * FROM root r WHERE r.id = @id',
        parameters: [{ name: '@id', value: databaseId }]
        };

        client.queryDatabases(querySpec).toArray((err, results) => {
        if (err) {
            callback(err);
        } else {
            if (results.length === 0) {
            let databaseSpec = { id: databaseId };
            client.createDatabase(databaseSpec, (err, created) => {
                callback(null, created);
            });
            } else {
            callback(null, results[0]);
            }
        }
        });
    },

    getOrCreateCollection: (client, databaseLink, collectionId, callback) => {
        let querySpec = {
        query: 'SELECT * FROM root r WHERE r.id=@id',
        parameters: [{ name: '@id', value: collectionId }]
        };

        client.queryCollections(databaseLink, querySpec).toArray((err, results) => {
        if (err) {
            callback(err);
        } else {
            if (results.length === 0) {
            let collectionSpec = { id: collectionId };
            client.createCollection(databaseLink, collectionSpec, (err, created) => {
                callback(null, created);
            });
            } else {
            callback(null, results[0]);
            }
        }
        });
    }
    };
    ```
5. <span data-ttu-id="e0850-157">Save and close the **cosmosdb-manager.js** file.</span><span class="sxs-lookup"><span data-stu-id="e0850-157">Save and close the **cosmosdb-manager.js** file.</span></span>
6. <span data-ttu-id="e0850-158">At the beginning of the **task-model.js** file, add the following code to reference the **DocumentDBClient** and the **cosmosdb-manager.js** we created above:</span><span class="sxs-lookup"><span data-stu-id="e0850-158">At the beginning of the **task-model.js** file, add the following code to reference the **DocumentDBClient** and the **cosmosdb-manager.js** we created above:</span></span> 

    ```nodejs
    let DocumentDBClient = require('documentdb').DocumentClient;
    let docdbUtils = require('./cosmosdb-manager.js');
    ```
7. <span data-ttu-id="e0850-159">Next, you will add code to define and export the Task object.</span><span class="sxs-lookup"><span data-stu-id="e0850-159">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="e0850-160">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span><span class="sxs-lookup"><span data-stu-id="e0850-160">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>  

    ```nodejs
    function TaskModel(documentDBClient, databaseId, collectionId) {
      this.client = documentDBClient;
      this.databaseId = databaseId;
      this.collectionId = collectionId;
   
      this.database = null;
      this.collection = null;
    }
   
    module.exports = TaskModel;
    ```
8. <span data-ttu-id="e0850-161">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0850-161">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>

    ```nodejs
    let DocumentDBClient = require('documentdb').DocumentClient;
    let docdbUtils = require('./cosmosdb-manager');

    function TaskModel(documentDBClient, databaseId, collectionId) {
    this.client = documentDBClient;
    this.databaseId = databaseId;
    this.collectionId = collectionId;

    this.database = null;
    this.collection = null;
    }

    TaskModel.prototype = {
    init: function(callback) {
        let self = this;

        docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function(err, db) {
        if (err) {
            callback(err);
        } else {
            self.database = db;
            docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function(err, coll) {
            if (err) {
                callback(err);
            } else {
                self.collection = coll;
            }
            });
        }
        });
    },

    find: function(querySpec, callback) {
        let self = this;

        self.client.queryDocuments(self.collection._self, querySpec).toArray(function(err, results) {
        if (err) {
            callback(err);
        } else {
            callback(null, results);
        }
        });
    },

    addItem: function(item, callback) {
        let self = this;

        item.date = Date.now();
        item.completed = false;

        self.client.createDocument(self.collection._self, item, function(err, doc) {
        if (err) {
            callback(err);
        } else {
            callback(null, doc);
        }
        });
    },

    updateItem: function(itemId, callback) {
        let self = this;

        self.getItem(itemId, function(err, doc) {
        if (err) {
            callback(err);
        } else {
            doc.completed = true;

            self.client.replaceDocument(doc._self, doc, function(err, replaced) {
            if (err) {
                callback(err);
            } else {
                callback(null, replaced);
            }
            });
        }
        });
    },

    getItem: function(itemId, callback) {
        let self = this;
        let querySpec = {
        query: 'SELECT * FROM root r WHERE r.id = @id',
        parameters: [{ name: '@id', value: itemId }]
        };

        self.client.queryDocuments(self.collection._self, querySpec).toArray(function(err, results) {
        if (err) {
            callback(err);
        } else {
            callback(null, results[0]);
        }
        });
    }
    };

    module.exports = TaskModel;
    ```
9. <span data-ttu-id="e0850-162">Save and close the **task-model.js** file.</span><span class="sxs-lookup"><span data-stu-id="e0850-162">Save and close the **task-model.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="e0850-163">Create the controller</span><span class="sxs-lookup"><span data-stu-id="e0850-163">Create the controller</span></span>
1. <span data-ttu-id="e0850-164">In the **routes** directory of your project, create a new file named **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-164">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="e0850-165">Add the following code to **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-165">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="e0850-166">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-166">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="e0850-167">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span><span class="sxs-lookup"><span data-stu-id="e0850-167">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
    ```nodejs
    let DocumentDBClient = require('documentdb').DocumentClient;
    let async = require('async');

    function TaskList(taskModel) {
    this.taskModel = taskModel;
    }

    module.exports = TaskList;
    ```
3. <span data-ttu-id="e0850-168">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="e0850-168">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
   ```nodejs
    TaskList.prototype = {
    showTasks: function(req, res) {
        let self = this;

        let querySpec = {
        query: 'SELECT * FROM root r WHERE r.completed=@completed',
        parameters: [
            {
            name: '@completed',
            value: false
            }
        ]
        };

        self.taskModel.find(querySpec, function(err, items) {
        if (err) {
            throw err;
        }

        res.render('index', {
            title: 'My ToDo List ',
            tasks: items
        });
        });
    },

    addTask: function(req, res) {
        let self = this;
        let item = req.body;

        self.taskModel.addItem(item, function(err) {
        if (err) {
            throw err;
        }

        res.redirect('/');
        });
    },

    completeTask: function(req, res) {
        let self = this;
        let completedTasks = Object.keys(req.body);

        async.forEach(
        completedTasks,
        function taskIterator(completedTask, callback) {
            self.taskModel.updateItem(completedTask, function(err) {
            if (err) {
                callback(err);
            } else {
                callback(null);
            }
            });
        },
        function goHome(err) {
            if (err) {
            throw err;
            } else {
            res.redirect('/');
            }
        }
        );
    }
    };
    ```        
4. <span data-ttu-id="e0850-169">Save and close the **tasklist.js** file.</span><span class="sxs-lookup"><span data-stu-id="e0850-169">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="e0850-170">Add config.js</span><span class="sxs-lookup"><span data-stu-id="e0850-170">Add config.js</span></span>
1. <span data-ttu-id="e0850-171">In your project directory create a new file named **config.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-171">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="e0850-172">Add the following to **config.js**.</span><span class="sxs-lookup"><span data-stu-id="e0850-172">Add the following to **config.js**.</span></span> <span data-ttu-id="e0850-173">This defines configuration settings and values needed for our application.</span><span class="sxs-lookup"><span data-stu-id="e0850-173">This defines configuration settings and values needed for our application.</span></span>
   
    ```nodejs
    let config = {}
   
    config.host = process.env.HOST || "[the URI value from the Azure Cosmos DB Keys page on http://portal.azure.com]";
    config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the Azure Cosmos DB Keys page on http://portal.azure.com]";
    config.databaseId = "ToDoList";
    config.collectionId = "Items";
   
    module.exports = config;
    ```
3. <span data-ttu-id="e0850-174">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys page of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0850-174">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys page of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="e0850-175">Save and close the **config.js** file.</span><span class="sxs-lookup"><span data-stu-id="e0850-175">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="e0850-176">Modify app.js</span><span class="sxs-lookup"><span data-stu-id="e0850-176">Modify app.js</span></span>
1. <span data-ttu-id="e0850-177">In the project directory, open the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="e0850-177">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="e0850-178">This file was created earlier when the Express web application was created.</span><span class="sxs-lookup"><span data-stu-id="e0850-178">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="e0850-179">Add the following code to the top of **app.js**:</span><span class="sxs-lookup"><span data-stu-id="e0850-179">Add the following code to the top of **app.js**:</span></span>
   
    ```nodejs
    var DocumentDBClient = require('documentdb').DocumentClient;
    var config = require('./config');
    var TaskList = require('./routes/tasklist');
    var TaskModel = require('./models/task-model');
    ```
3. <span data-ttu-id="e0850-180">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span><span class="sxs-lookup"><span data-stu-id="e0850-180">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="e0850-181">Replace the following two lines in **app.js** file:</span><span class="sxs-lookup"><span data-stu-id="e0850-181">Replace the following two lines in **app.js** file:</span></span>
   
    ```nodejs
    app.use('/', index);
    app.use('/users', users); 
    ```
   
    <span data-ttu-id="e0850-182">with the following snippet:</span><span class="sxs-lookup"><span data-stu-id="e0850-182">with the following snippet:</span></span>
   
    ```nodejs
    let docDbClient = new DocumentDBClient(config.host, {
        masterKey: config.authKey
    });
    let taskModel = new TaskModel(docDbClient, config.databaseId, config.collectionId);
    let taskList = new TaskList(taskModel);
    taskModel.init();
   
    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    app.set('view engine', 'jade');
    ```
5. <span data-ttu-id="e0850-183">These lines define a new instance of our **TaskModel** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span><span class="sxs-lookup"><span data-stu-id="e0850-183">These lines define a new instance of our **TaskModel** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="e0850-184">Finally, save and close the **app.js** file, we're just about done.</span><span class="sxs-lookup"><span data-stu-id="e0850-184">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <a name="_Toc395783181"></a><span data-ttu-id="e0850-185">Step 5: Build a user interface</span><span class="sxs-lookup"><span data-stu-id="e0850-185">Step 5: Build a user interface</span></span>
<span data-ttu-id="e0850-186">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span><span class="sxs-lookup"><span data-stu-id="e0850-186">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="e0850-187">The Express application we created uses **Jade** as the view engine.</span><span class="sxs-lookup"><span data-stu-id="e0850-187">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="e0850-188">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="e0850-188">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="e0850-189">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span><span class="sxs-lookup"><span data-stu-id="e0850-189">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="e0850-190">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span><span class="sxs-lookup"><span data-stu-id="e0850-190">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="e0850-191">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span><span class="sxs-lookup"><span data-stu-id="e0850-191">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

    ```
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

    <span data-ttu-id="e0850-192">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span><span class="sxs-lookup"><span data-stu-id="e0850-192">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="e0850-193">Save and close this **layout.jade** file.</span><span class="sxs-lookup"><span data-stu-id="e0850-193">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="e0850-194">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span><span class="sxs-lookup"><span data-stu-id="e0850-194">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
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
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="e0850-195">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span><span class="sxs-lookup"><span data-stu-id="e0850-195">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="e0850-196">In this layout we created two HTML forms.</span><span class="sxs-lookup"><span data-stu-id="e0850-196">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="e0850-197">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span><span class="sxs-lookup"><span data-stu-id="e0850-197">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    
<span data-ttu-id="e0850-198">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span><span class="sxs-lookup"><span data-stu-id="e0850-198">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="e0850-199">This should be all that we need for our application to work.</span><span class="sxs-lookup"><span data-stu-id="e0850-199">This should be all that we need for our application to work.</span></span>

## <a name="_Toc395783181"></a><span data-ttu-id="e0850-200">Step 6: Run your application locally</span><span class="sxs-lookup"><span data-stu-id="e0850-200">Step 6: Run your application locally</span></span>
1. <span data-ttu-id="e0850-201">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span><span class="sxs-lookup"><span data-stu-id="e0850-201">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="e0850-202">The page should now look like the image below:</span><span class="sxs-lookup"><span data-stu-id="e0850-202">The page should now look like the image below:</span></span>
   
    ![Screenshot of the MyTodo List application in a browser window](./media/sql-api-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces. If there are spaces before the first two lines, remove them, save both files, then refresh your browser window. 

2. <span data-ttu-id="e0850-206">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span><span class="sxs-lookup"><span data-stu-id="e0850-206">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="e0850-207">This creates a document in Azure Cosmos DB with those properties.</span><span class="sxs-lookup"><span data-stu-id="e0850-207">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="e0850-208">The page should update to display the newly created item in the ToDo list.</span><span class="sxs-lookup"><span data-stu-id="e0850-208">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![Screenshot of the application with a new item in the ToDo list](./media/sql-api-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="e0850-210">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span><span class="sxs-lookup"><span data-stu-id="e0850-210">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="e0850-211">This updates the document you already created and removes it from the view.</span><span class="sxs-lookup"><span data-stu-id="e0850-211">This updates the document you already created and removes it from the view.</span></span>

5. <span data-ttu-id="e0850-212">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span><span class="sxs-lookup"><span data-stu-id="e0850-212">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <a name="_Toc395783182"></a><span data-ttu-id="e0850-213">Step 7: Deploy your application development project to Azure Websites</span><span class="sxs-lookup"><span data-stu-id="e0850-213">Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="e0850-214">If you haven't already, enable a git repository for your Azure Website.</span><span class="sxs-lookup"><span data-stu-id="e0850-214">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="e0850-215">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service/app-service-deploy-local-git.md) topic.</span><span class="sxs-lookup"><span data-stu-id="e0850-215">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="e0850-216">Add your Azure Website as a git remote.</span><span class="sxs-lookup"><span data-stu-id="e0850-216">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="e0850-217">Deploy by pushing to the remote.</span><span class="sxs-lookup"><span data-stu-id="e0850-217">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="e0850-218">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span><span class="sxs-lookup"><span data-stu-id="e0850-218">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="e0850-219">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="e0850-219">Congratulations!</span></span> <span data-ttu-id="e0850-220">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="e0850-220">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="e0850-221">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e0850-221">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <a name="_Toc395637775"></a><span data-ttu-id="e0850-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0850-222">Next steps</span></span>

* <span data-ttu-id="e0850-223">Want to perform scale and performance testing with Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e0850-223">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="e0850-224">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="e0850-224">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="e0850-225">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="e0850-225">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="e0850-226">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="e0850-226">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="e0850-227">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e0850-227">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

