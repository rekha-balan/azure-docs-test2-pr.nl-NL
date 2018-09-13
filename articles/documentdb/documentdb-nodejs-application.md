---
title: Learn Node.js - DocumentDB Node.js Tutorial | Microsoft Docs
description: Learn Node.js! Tutorial explores how to use Microsoft Azure DocumentDB to store and access data from a Node.js Express web application hosted on Azure Websites.
keywords: Application development, database tutorial, learn node.js, node.js tutorial, documentdb, azure, Microsoft azure
services: documentdb
documentationcenter: nodejs
author: syamkmsft
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 12/16/2016
ms.author: syamk
ms.openlocfilehash: 40586fbe16de91ebb774be8e653bc0c94ca0fee7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563920"
---
# <a name="_Toc395783175"></a><span data-ttu-id="2a22a-105">Build a Node.js web application using DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2a22a-105">Build a Node.js web application using DocumentDB</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [.NET for MongoDB](documentdb-mongodb-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

<span data-ttu-id="2a22a-111">This Node.js tutorial shows you how to use Azure DocumentDB to store and access data from a Node.js Express application hosted on Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="2a22a-111">This Node.js tutorial shows you how to use Azure DocumentDB to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="2a22a-112">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span><span class="sxs-lookup"><span data-stu-id="2a22a-112">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="2a22a-113">The tasks are stored as JSON documents in Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2a22a-113">The tasks are stored as JSON documents in Azure DocumentDB.</span></span> <span data-ttu-id="2a22a-114">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span><span class="sxs-lookup"><span data-stu-id="2a22a-114">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![Screen shot of the My Todo List application created in this Node.js tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-application/image1.png)

<span data-ttu-id="2a22a-116">Don't have time to complete the tutorial and just want to get the complete solution?</span><span class="sxs-lookup"><span data-stu-id="2a22a-116">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="2a22a-117">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2a22a-117">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="2a22a-118">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span><span class="sxs-lookup"><span data-stu-id="2a22a-118">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <a name="_Toc395783176"></a><span data-ttu-id="2a22a-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2a22a-119">Prerequisites</span></span>
> [!TIP]
> This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.
> 
> 

<span data-ttu-id="2a22a-121">Before following the instructions in this article, you should ensure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="2a22a-121">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="2a22a-122">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="2a22a-122">An active Azure account.</span></span> <span data-ttu-id="2a22a-123">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="2a22a-123">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2a22a-124">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a22a-124">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="2a22a-125">OR</span><span class="sxs-lookup"><span data-stu-id="2a22a-125">OR</span></span>

   <span data-ttu-id="2a22a-126">A local installation of the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2a22a-126">A local installation of the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span></span>
* <span data-ttu-id="2a22a-127">[Node.js][Node.js] version v0.10.29 or higher.</span><span class="sxs-lookup"><span data-stu-id="2a22a-127">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="2a22a-128">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="2a22a-128">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="2a22a-129">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="2a22a-129">[Git][Git].</span></span>

## <a name="_Toc395637761"></a><span data-ttu-id="2a22a-130">Step 1: Create a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="2a22a-130">Step 1: Create a DocumentDB database account</span></span>
<span data-ttu-id="2a22a-131">Let's start by creating a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="2a22a-131">Let's start by creating a DocumentDB account.</span></span> <span data-ttu-id="2a22a-132">If you already have an account or if you are using the DocumentDB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="2a22a-132">If you already have an account or if you are using the DocumentDB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

[!INCLUDE [documentdb-keys](../../includes/documentdb-keys.md)]

## <a name="_Toc395783178"></a><span data-ttu-id="2a22a-133">Step 2: Learn to create a new Node.js application</span><span class="sxs-lookup"><span data-stu-id="2a22a-133">Step 2: Learn to create a new Node.js application</span></span>
<span data-ttu-id="2a22a-134">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="2a22a-134">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="2a22a-135">Open your favorite terminal, such as the Node.js command prompt.</span><span class="sxs-lookup"><span data-stu-id="2a22a-135">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="2a22a-136">Navigate to the directory in which you'd like to store the new application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-136">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="2a22a-137">Use the express generator to generate a new application called **todo**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-137">Use the express generator to generate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="2a22a-138">Open your new **todo** directory and install dependencies.</span><span class="sxs-lookup"><span data-stu-id="2a22a-138">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="2a22a-139">Run your new application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-139">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="2a22a-140">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="2a22a-140">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Learn Node.js - Screenshot of the Hello World application in a browser window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-application/image12.png)

    <span data-ttu-id="2a22a-142">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span><span class="sxs-lookup"><span data-stu-id="2a22a-142">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span></span>

## <a name="_Toc395783179"></a><span data-ttu-id="2a22a-143">Step 3: Install additional modules</span><span class="sxs-lookup"><span data-stu-id="2a22a-143">Step 3: Install additional modules</span></span>
<span data-ttu-id="2a22a-144">The **package.json** file is one of the files created in the root of the project.</span><span class="sxs-lookup"><span data-stu-id="2a22a-144">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="2a22a-145">This file contains a list of additional modules that are required for your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-145">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="2a22a-146">Later, when you deploy this application to an Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-146">Later, when you deploy this application to an Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="2a22a-147">We still need to install two more packages for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a22a-147">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="2a22a-148">Back in the terminal, install the **async** module via npm.</span><span class="sxs-lookup"><span data-stu-id="2a22a-148">Back in the terminal, install the **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="2a22a-149">Install the **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="2a22a-149">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="2a22a-150">This is the module where all the DocumentDB magic happens.</span><span class="sxs-lookup"><span data-stu-id="2a22a-150">This is the module where all the DocumentDB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="2a22a-151">A quick check of the **package.json** file of the application should show the additional modules.</span><span class="sxs-lookup"><span data-stu-id="2a22a-151">A quick check of the **package.json** file of the application should show the additional modules.</span></span> <span data-ttu-id="2a22a-152">This file will tell Azure which packages to download and install when running your application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-152">This file will tell Azure which packages to download and install when running your application.</span></span> <span data-ttu-id="2a22a-153">It should resemble the example below.</span><span class="sxs-lookup"><span data-stu-id="2a22a-153">It should resemble the example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="2a22a-154">This tells Node (and Azure later) that your application depends on these additional modules.</span><span class="sxs-lookup"><span data-stu-id="2a22a-154">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <a name="_Toc395783180"></a><span data-ttu-id="2a22a-155">Step 4: Using the DocumentDB service in a node application</span><span class="sxs-lookup"><span data-stu-id="2a22a-155">Step 4: Using the DocumentDB service in a node application</span></span>
<span data-ttu-id="2a22a-156">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2a22a-156">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure DocumentDB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="2a22a-157">Create the model</span><span class="sxs-lookup"><span data-stu-id="2a22a-157">Create the model</span></span>
1. <span data-ttu-id="2a22a-158">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-158">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="2a22a-159">In the **models** directory, create a new file named **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-159">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="2a22a-160">This file will contain the model for the tasks created by our application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-160">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="2a22a-161">In the same **models** directory, create another new file named **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-161">In the same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="2a22a-162">This file will contain some useful, reusable, code that we will use throughout our application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-162">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="2a22a-163">Copy the following code in to **docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="2a22a-163">Copy the following code in to **docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
   > [!TIP]
   > createCollection takes an optional requestOptions parameter that can be used to specify the Offer Type for the Collection. If no requestOptions.offerType value is supplied then the Collection will be created using the default Offer Type.
   > 
   > For more information on DocumentDB Offer Types please refer to [Performance levels in DocumentDB](documentdb-performance-levels.md) 
   > 
   > 
5. <span data-ttu-id="2a22a-167">Save and close the **docdbUtils.js** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-167">Save and close the **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="2a22a-168">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span><span class="sxs-lookup"><span data-stu-id="2a22a-168">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="2a22a-169">Next, you will add code to define and export the Task object.</span><span class="sxs-lookup"><span data-stu-id="2a22a-169">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="2a22a-170">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span><span class="sxs-lookup"><span data-stu-id="2a22a-170">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="2a22a-171">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2a22a-171">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in DocumentDB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="2a22a-172">Save and close the **taskDao.js** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-172">Save and close the **taskDao.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="2a22a-173">Create the controller</span><span class="sxs-lookup"><span data-stu-id="2a22a-173">Create the controller</span></span>
1. <span data-ttu-id="2a22a-174">In the **routes** directory of your project, create a new file named **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-174">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="2a22a-175">Add the following code to **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-175">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="2a22a-176">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-176">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="2a22a-177">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span><span class="sxs-lookup"><span data-stu-id="2a22a-177">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="2a22a-178">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="2a22a-178">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="2a22a-179">Save and close the **tasklist.js** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-179">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="2a22a-180">Add config.js</span><span class="sxs-lookup"><span data-stu-id="2a22a-180">Add config.js</span></span>
1. <span data-ttu-id="2a22a-181">In your project directory create a new file named **config.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-181">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="2a22a-182">Add the following to **config.js**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-182">Add the following to **config.js**.</span></span> <span data-ttu-id="2a22a-183">This defines configuration settings and values needed for our application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-183">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[the URI value from the DocumentDB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the DocumentDB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="2a22a-184">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your DocumentDB account on the [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2a22a-184">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your DocumentDB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="2a22a-185">Save and close the **config.js** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-185">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="2a22a-186">Modify app.js</span><span class="sxs-lookup"><span data-stu-id="2a22a-186">Modify app.js</span></span>
1. <span data-ttu-id="2a22a-187">In the project directory, open the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-187">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="2a22a-188">This file was created earlier when the Express web application was created.</span><span class="sxs-lookup"><span data-stu-id="2a22a-188">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="2a22a-189">Add the following code to the top of **app.js**</span><span class="sxs-lookup"><span data-stu-id="2a22a-189">Add the following code to the top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="2a22a-190">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span><span class="sxs-lookup"><span data-stu-id="2a22a-190">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="2a22a-191">Replace the following two lines in **app.js** file:</span><span class="sxs-lookup"><span data-stu-id="2a22a-191">Replace the following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="2a22a-192">with the following snippet:</span><span class="sxs-lookup"><span data-stu-id="2a22a-192">with the following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="2a22a-193">These lines define a new instance of our **TaskDao** object, with a new connection to DocumentDB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span><span class="sxs-lookup"><span data-stu-id="2a22a-193">These lines define a new instance of our **TaskDao** object, with a new connection to DocumentDB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="2a22a-194">Finally, save and close the **app.js** file, we're just about done.</span><span class="sxs-lookup"><span data-stu-id="2a22a-194">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <a name="_Toc395783181"></a><span data-ttu-id="2a22a-195">Step 5: Build a user interface</span><span class="sxs-lookup"><span data-stu-id="2a22a-195">Step 5: Build a user interface</span></span>
<span data-ttu-id="2a22a-196">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span><span class="sxs-lookup"><span data-stu-id="2a22a-196">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="2a22a-197">The Express application we created uses **Jade** as the view engine.</span><span class="sxs-lookup"><span data-stu-id="2a22a-197">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="2a22a-198">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="2a22a-198">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="2a22a-199">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span><span class="sxs-lookup"><span data-stu-id="2a22a-199">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="2a22a-200">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span><span class="sxs-lookup"><span data-stu-id="2a22a-200">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="2a22a-201">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span><span class="sxs-lookup"><span data-stu-id="2a22a-201">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>
   
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

    <span data-ttu-id="2a22a-202">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span><span class="sxs-lookup"><span data-stu-id="2a22a-202">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>
    <span data-ttu-id="2a22a-203">Save and close this **layout.jade** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-203">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="2a22a-204">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span><span class="sxs-lookup"><span data-stu-id="2a22a-204">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
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
             button.btn(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             label Item Name:
             input(name="name", type="textbox")
             label Item Category:
             input(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   
    <span data-ttu-id="2a22a-205">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span><span class="sxs-lookup"><span data-stu-id="2a22a-205">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
    <span data-ttu-id="2a22a-206">In this layout we created two HTML forms.</span><span class="sxs-lookup"><span data-stu-id="2a22a-206">In this layout we created two HTML forms.</span></span> 
    <span data-ttu-id="2a22a-207">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span><span class="sxs-lookup"><span data-stu-id="2a22a-207">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    <span data-ttu-id="2a22a-208">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span><span class="sxs-lookup"><span data-stu-id="2a22a-208">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>
   
    <span data-ttu-id="2a22a-209">This should be all that we need for our application to work.</span><span class="sxs-lookup"><span data-stu-id="2a22a-209">This should be all that we need for our application to work.</span></span>
4. <span data-ttu-id="2a22a-210">Open the **style.css** file in **public\stylesheets** directory and replace the code with the following:</span><span class="sxs-lookup"><span data-stu-id="2a22a-210">Open the **style.css** file in **public\stylesheets** directory and replace the code with the following:</span></span>
   
        body {
          padding: 50px;
          font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
        }
        a {
          color: #00B7FF;
        }
        .well label {
          display: block;
        }
        .well input {
          margin-bottom: 5px;
        }
        .btn {
          margin-top: 5px;
          border: outset 1px #C8C8C8;
        }
   
    <span data-ttu-id="2a22a-211">Save and close this **style.css** file.</span><span class="sxs-lookup"><span data-stu-id="2a22a-211">Save and close this **style.css** file.</span></span>

## <a name="_Toc395783181"></a><span data-ttu-id="2a22a-212">Step 6: Run your application locally</span><span class="sxs-lookup"><span data-stu-id="2a22a-212">Step 6: Run your application locally</span></span>
1. <span data-ttu-id="2a22a-213">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span><span class="sxs-lookup"><span data-stu-id="2a22a-213">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="2a22a-214">The page should now look like the image below:</span><span class="sxs-lookup"><span data-stu-id="2a22a-214">The page should now look like the image below:</span></span>
   
    ![Screenshot of the MyTodo List application in a browser window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-application/image18.png)

    > [!TIP]
    > If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces. If there are spaces before the first two lines, remove them, save both files, then refresh your browser window. 

2. <span data-ttu-id="2a22a-218">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-218">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="2a22a-219">This creates a document in DocumentDB with those properties.</span><span class="sxs-lookup"><span data-stu-id="2a22a-219">This creates a document in DocumentDB with those properties.</span></span> 
3. <span data-ttu-id="2a22a-220">The page should update to display the newly created item in the ToDo list.</span><span class="sxs-lookup"><span data-stu-id="2a22a-220">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![Screenshot of the application with a new item in the ToDo list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nodejs-application/image19.png)
4. <span data-ttu-id="2a22a-222">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span><span class="sxs-lookup"><span data-stu-id="2a22a-222">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="2a22a-223">This updates the document you already created.</span><span class="sxs-lookup"><span data-stu-id="2a22a-223">This updates the document you already created.</span></span>

5. <span data-ttu-id="2a22a-224">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span><span class="sxs-lookup"><span data-stu-id="2a22a-224">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <a name="_Toc395783182"></a><span data-ttu-id="2a22a-225">Step 7: Deploy your application development project to Azure Websites</span><span class="sxs-lookup"><span data-stu-id="2a22a-225">Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="2a22a-226">If you haven't already, enable a git repository for your Azure Website.</span><span class="sxs-lookup"><span data-stu-id="2a22a-226">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="2a22a-227">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span><span class="sxs-lookup"><span data-stu-id="2a22a-227">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="2a22a-228">Add your Azure Website as a git remote.</span><span class="sxs-lookup"><span data-stu-id="2a22a-228">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="2a22a-229">Deploy by pushing to the remote.</span><span class="sxs-lookup"><span data-stu-id="2a22a-229">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="2a22a-230">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handy work running in Azure!</span><span class="sxs-lookup"><span data-stu-id="2a22a-230">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handy work running in Azure!</span></span>

    <span data-ttu-id="2a22a-231">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="2a22a-231">Congratulations!</span></span> <span data-ttu-id="2a22a-232">You have just built your first Node.js Express Web Application using Azure DocumentDB and published it to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="2a22a-232">You have just built your first Node.js Express Web Application using Azure DocumentDB and published it to Azure Websites.</span></span>

    <span data-ttu-id="2a22a-233">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2a22a-233">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <a name="_Toc395637775"></a><span data-ttu-id="2a22a-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a22a-234">Next steps</span></span>

* <span data-ttu-id="2a22a-235">Want to perform scale and performance testing with DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="2a22a-235">Want to perform scale and performance testing with DocumentDB?</span></span> <span data-ttu-id="2a22a-236">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="2a22a-236">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span></span>
* <span data-ttu-id="2a22a-237">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="2a22a-237">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="2a22a-238">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2a22a-238">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2a22a-239">Explore the [DocumentDB documentation](https://docs.microsoft.com/en-us/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2a22a-239">Explore the [DocumentDB documentation](https://docs.microsoft.com/en-us/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app





