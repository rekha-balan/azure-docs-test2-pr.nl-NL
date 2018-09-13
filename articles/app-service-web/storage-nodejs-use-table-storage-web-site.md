---
title: Node.js web app using the Azure Table Service
description: This tutorial teaches you how to use the Azure Table service to store data from a Node.js application which is hosted in Azure App Service Web Apps.
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 1f6ef210537607cacae3c91f7ab8d04e6aeaccb7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564362"
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="0a187-103">Node.js web app using the Azure Table Service</span><span class="sxs-lookup"><span data-stu-id="0a187-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="0a187-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0a187-104">Overview</span></span>
<span data-ttu-id="0a187-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span><span class="sxs-lookup"><span data-stu-id="0a187-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="0a187-106">This tutorial assumes that you have some prior experience using node and [Git].</span><span class="sxs-lookup"><span data-stu-id="0a187-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="0a187-107">You will learn:</span><span class="sxs-lookup"><span data-stu-id="0a187-107">You will learn:</span></span>

* <span data-ttu-id="0a187-108">How to use npm (node package manager) to install the node modules</span><span class="sxs-lookup"><span data-stu-id="0a187-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="0a187-109">How to work with the Azure Table service</span><span class="sxs-lookup"><span data-stu-id="0a187-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="0a187-110">How to use the Azure CLI to create a web app.</span><span class="sxs-lookup"><span data-stu-id="0a187-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="0a187-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span><span class="sxs-lookup"><span data-stu-id="0a187-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="0a187-112">The tasks are stored in the Table service.</span><span class="sxs-lookup"><span data-stu-id="0a187-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="0a187-113">Here is the completed application:</span><span class="sxs-lookup"><span data-stu-id="0a187-113">Here is the completed application:</span></span>

![A web page displaying an empty tasklist][node-table-finished]

> [!NOTE]
> <span data-ttu-id="0a187-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="0a187-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0a187-116">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="0a187-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0a187-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a187-117">Prerequisites</span></span>
<span data-ttu-id="0a187-118">Before following the instructions in this article, ensure that you have the following installed:</span><span class="sxs-lookup"><span data-stu-id="0a187-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="0a187-119">[node] version 0.10.24 or higher</span><span class="sxs-lookup"><span data-stu-id="0a187-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="0a187-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="0a187-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="0a187-121">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="0a187-121">Create a storage account</span></span>
<span data-ttu-id="0a187-122">Create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0a187-122">Create an Azure storage account.</span></span> <span data-ttu-id="0a187-123">The app will use this account to store the to-do items.</span><span class="sxs-lookup"><span data-stu-id="0a187-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="0a187-124">Log into the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0a187-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0a187-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span><span class="sxs-lookup"><span data-stu-id="0a187-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="0a187-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span><span class="sxs-lookup"><span data-stu-id="0a187-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![New Button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="0a187-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span><span class="sxs-lookup"><span data-stu-id="0a187-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="0a187-129">In the storage account's blade, click **Settings** > **Keys**.</span><span class="sxs-lookup"><span data-stu-id="0a187-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="0a187-130">Copy the primary access key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="0a187-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Access key][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="0a187-132">Install modules and generate scaffolding</span><span class="sxs-lookup"><span data-stu-id="0a187-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="0a187-133">In this section you will create a new Node application and use npm to add module packages.</span><span class="sxs-lookup"><span data-stu-id="0a187-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="0a187-134">For this application you will use the [Express] and [Azure] modules.</span><span class="sxs-lookup"><span data-stu-id="0a187-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="0a187-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span><span class="sxs-lookup"><span data-stu-id="0a187-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="0a187-136">Install express and generate scaffolding</span><span class="sxs-lookup"><span data-stu-id="0a187-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="0a187-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span><span class="sxs-lookup"><span data-stu-id="0a187-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="0a187-138">Enter the following command to install the Express module.</span><span class="sxs-lookup"><span data-stu-id="0a187-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="0a187-139">Depending on the operating system, you may need to put 'sudo' before the command:</span><span class="sxs-lookup"><span data-stu-id="0a187-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="0a187-140">The output appears similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="0a187-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="0a187-141">The '-g' parameter installs the module globally.</span><span class="sxs-lookup"><span data-stu-id="0a187-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="0a187-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span><span class="sxs-lookup"><span data-stu-id="0a187-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="0a187-143">To create the scaffolding for the application, enter the **express** command:</span><span class="sxs-lookup"><span data-stu-id="0a187-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="0a187-144">The output of this command appears similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="0a187-144">The output of this command appears similar to the following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="0a187-145">You now have several new directories and files in the **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="0a187-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="0a187-146">Install additional modules</span><span class="sxs-lookup"><span data-stu-id="0a187-146">Install additional modules</span></span>
<span data-ttu-id="0a187-147">One of the files that **express** creates is **package.json**.</span><span class="sxs-lookup"><span data-stu-id="0a187-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="0a187-148">This file contains a list of module dependencies.</span><span class="sxs-lookup"><span data-stu-id="0a187-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="0a187-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span><span class="sxs-lookup"><span data-stu-id="0a187-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="0a187-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span><span class="sxs-lookup"><span data-stu-id="0a187-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="0a187-151">You may need to use 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="0a187-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="0a187-152">The output of this command appears similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="0a187-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="0a187-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span><span class="sxs-lookup"><span data-stu-id="0a187-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="0a187-154">The **--save** flag adds entries for these modules to the **package.json** file.</span><span class="sxs-lookup"><span data-stu-id="0a187-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="0a187-155">The output of this command appears similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="0a187-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="0a187-156">Create the application</span><span class="sxs-lookup"><span data-stu-id="0a187-156">Create the application</span></span>
<span data-ttu-id="0a187-157">Now we're ready to build the application.</span><span class="sxs-lookup"><span data-stu-id="0a187-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="0a187-158">Create a model</span><span class="sxs-lookup"><span data-stu-id="0a187-158">Create a model</span></span>
<span data-ttu-id="0a187-159">A *model* is an object that represents the data in your application.</span><span class="sxs-lookup"><span data-stu-id="0a187-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="0a187-160">For the application, the only model is a task object, which represents an item in the to-do list.</span><span class="sxs-lookup"><span data-stu-id="0a187-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="0a187-161">Tasks will have the following fields:</span><span class="sxs-lookup"><span data-stu-id="0a187-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="0a187-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="0a187-162">PartitionKey</span></span>
* <span data-ttu-id="0a187-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="0a187-163">RowKey</span></span>
* <span data-ttu-id="0a187-164">name (string)</span><span class="sxs-lookup"><span data-stu-id="0a187-164">name (string)</span></span>
* <span data-ttu-id="0a187-165">category (string)</span><span class="sxs-lookup"><span data-stu-id="0a187-165">category (string)</span></span>
* <span data-ttu-id="0a187-166">completed (Boolean)</span><span class="sxs-lookup"><span data-stu-id="0a187-166">completed (Boolean)</span></span>

<span data-ttu-id="0a187-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span><span class="sxs-lookup"><span data-stu-id="0a187-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="0a187-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a187-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="0a187-169">In the **tasklist** directory, create a new directory named **models**.</span><span class="sxs-lookup"><span data-stu-id="0a187-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="0a187-170">In the **models** directory, create a new file named **task.js**.</span><span class="sxs-lookup"><span data-stu-id="0a187-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="0a187-171">This file will contain the model for the tasks created by your application.</span><span class="sxs-lookup"><span data-stu-id="0a187-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="0a187-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span><span class="sxs-lookup"><span data-stu-id="0a187-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="0a187-173">Add the following code to define and export the Task object.</span><span class="sxs-lookup"><span data-stu-id="0a187-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="0a187-174">This object is responsible for connecting to the table.</span><span class="sxs-lookup"><span data-stu-id="0a187-174">This object is responsible for connecting to the table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="0a187-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span><span class="sxs-lookup"><span data-stu-id="0a187-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator to set types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="0a187-176">Save and close the **task.js** file.</span><span class="sxs-lookup"><span data-stu-id="0a187-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="0a187-177">Create a controller</span><span class="sxs-lookup"><span data-stu-id="0a187-177">Create a controller</span></span>
<span data-ttu-id="0a187-178">A *controller* handles HTTP requests and renders the HTML response.</span><span class="sxs-lookup"><span data-stu-id="0a187-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="0a187-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span><span class="sxs-lookup"><span data-stu-id="0a187-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="0a187-180">Add the following code to **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0a187-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="0a187-181">This loads the azure and async modules, which are used by **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0a187-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="0a187-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span><span class="sxs-lookup"><span data-stu-id="0a187-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="0a187-183">Define a **TaskList** object.</span><span class="sxs-lookup"><span data-stu-id="0a187-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="0a187-184">Add the following methods to **TaskList**:</span><span class="sxs-lookup"><span data-stu-id="0a187-184">Add the following methods to **TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="0a187-185">Modify app.js</span><span class="sxs-lookup"><span data-stu-id="0a187-185">Modify app.js</span></span>
1. <span data-ttu-id="0a187-186">From the **tasklist** directory, open the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="0a187-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="0a187-187">This file was created earlier by running the **express** command.</span><span class="sxs-lookup"><span data-stu-id="0a187-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="0a187-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span><span class="sxs-lookup"><span data-stu-id="0a187-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="0a187-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span><span class="sxs-lookup"><span data-stu-id="0a187-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="0a187-190">In the app.js file, scroll down to where you see the following line:</span><span class="sxs-lookup"><span data-stu-id="0a187-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="0a187-191">Replace the above lines with the code shown below.</span><span class="sxs-lookup"><span data-stu-id="0a187-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="0a187-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span><span class="sxs-lookup"><span data-stu-id="0a187-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="0a187-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span><span class="sxs-lookup"><span data-stu-id="0a187-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="0a187-194">Save the **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="0a187-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="0a187-195">Modify the index view</span><span class="sxs-lookup"><span data-stu-id="0a187-195">Modify the index view</span></span>
1. <span data-ttu-id="0a187-196">Open the **tasklist/views/index.jade** file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="0a187-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="0a187-197">Replace the entire contents of the file with the following code.</span><span class="sxs-lookup"><span data-stu-id="0a187-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="0a187-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span><span class="sxs-lookup"><span data-stu-id="0a187-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
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
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="0a187-199">Save and close **index.jade** file.</span><span class="sxs-lookup"><span data-stu-id="0a187-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="0a187-200">Modify the global layout</span><span class="sxs-lookup"><span data-stu-id="0a187-200">Modify the global layout</span></span>
<span data-ttu-id="0a187-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span><span class="sxs-lookup"><span data-stu-id="0a187-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="0a187-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span><span class="sxs-lookup"><span data-stu-id="0a187-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="0a187-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="0a187-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="0a187-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span><span class="sxs-lookup"><span data-stu-id="0a187-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="0a187-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span><span class="sxs-lookup"><span data-stu-id="0a187-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="0a187-206">Create a config file</span><span class="sxs-lookup"><span data-stu-id="0a187-206">Create a config file</span></span>
<span data-ttu-id="0a187-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span><span class="sxs-lookup"><span data-stu-id="0a187-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="0a187-208">Create a file named \**config.json* \*with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="0a187-208">Create a file named \**config.json* \*with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="0a187-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span><span class="sxs-lookup"><span data-stu-id="0a187-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="0a187-210">For example:</span><span class="sxs-lookup"><span data-stu-id="0a187-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="0a187-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span><span class="sxs-lookup"><span data-stu-id="0a187-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="0a187-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span><span class="sxs-lookup"><span data-stu-id="0a187-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="0a187-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span><span class="sxs-lookup"><span data-stu-id="0a187-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="0a187-214">Run the application locally</span><span class="sxs-lookup"><span data-stu-id="0a187-214">Run the application locally</span></span>
<span data-ttu-id="0a187-215">To test the application on your local machine, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a187-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="0a187-216">From the command-line, change directories to the **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="0a187-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="0a187-217">Use the following command to launch the application locally:</span><span class="sxs-lookup"><span data-stu-id="0a187-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="0a187-218">Open a web browser and navigate to http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="0a187-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="0a187-219">A web page similar to the following example appears.</span><span class="sxs-lookup"><span data-stu-id="0a187-219">A web page similar to the following example appears.</span></span>
   
    ![A webpage displaying an empty tasklist][node-table-finished]
4. <span data-ttu-id="0a187-221">To create a new to-do item, enter a name and category and click **Add Item**.</span><span class="sxs-lookup"><span data-stu-id="0a187-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="0a187-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span><span class="sxs-lookup"><span data-stu-id="0a187-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![An image of the new item in the list of tasks][node-table-list-items]

<span data-ttu-id="0a187-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span><span class="sxs-lookup"><span data-stu-id="0a187-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="0a187-225">Deploy your application to Azure</span><span class="sxs-lookup"><span data-stu-id="0a187-225">Deploy your application to Azure</span></span>
<span data-ttu-id="0a187-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span><span class="sxs-lookup"><span data-stu-id="0a187-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="0a187-227">To perform these steps you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0a187-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0a187-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0a187-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0a187-229">See [Build and deploy a Node.js web app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="0a187-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="0a187-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span><span class="sxs-lookup"><span data-stu-id="0a187-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="0a187-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span><span class="sxs-lookup"><span data-stu-id="0a187-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="0a187-232">Import publishing settings</span><span class="sxs-lookup"><span data-stu-id="0a187-232">Import publishing settings</span></span>
<span data-ttu-id="0a187-233">In this step, you will download a file containing information about your subscription.</span><span class="sxs-lookup"><span data-stu-id="0a187-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="0a187-234">Enter the following command:</span><span class="sxs-lookup"><span data-stu-id="0a187-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="0a187-235">This command launches a browser and navigates to the download page.</span><span class="sxs-lookup"><span data-stu-id="0a187-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="0a187-236">If prompted, log in with the account associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0a187-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="0a187-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span><span class="sxs-lookup"><span data-stu-id="0a187-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="0a187-238">Save the file and note the file path.</span><span class="sxs-lookup"><span data-stu-id="0a187-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="0a187-239">Enter the following command to import the settings:</span><span class="sxs-lookup"><span data-stu-id="0a187-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="0a187-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span><span class="sxs-lookup"><span data-stu-id="0a187-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="0a187-241">After the settings are imported, delete the publish settings file.</span><span class="sxs-lookup"><span data-stu-id="0a187-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="0a187-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0a187-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="0a187-243">Create an App Service web app</span><span class="sxs-lookup"><span data-stu-id="0a187-243">Create an App Service web app</span></span>
1. <span data-ttu-id="0a187-244">From the command-line, change directories to the **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="0a187-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="0a187-245">Use the following command to create a new web app.</span><span class="sxs-lookup"><span data-stu-id="0a187-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="0a187-246">You will be prompted for the web app name and location.</span><span class="sxs-lookup"><span data-stu-id="0a187-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="0a187-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0a187-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="0a187-248">The `--git` parameter creates a Git repository on Azure for this web app.</span><span class="sxs-lookup"><span data-stu-id="0a187-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="0a187-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span><span class="sxs-lookup"><span data-stu-id="0a187-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="0a187-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span><span class="sxs-lookup"><span data-stu-id="0a187-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="0a187-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span><span class="sxs-lookup"><span data-stu-id="0a187-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="0a187-252">Once this command has completed, you will see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="0a187-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="0a187-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span><span class="sxs-lookup"><span data-stu-id="0a187-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="0a187-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span><span class="sxs-lookup"><span data-stu-id="0a187-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="0a187-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="0a187-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="0a187-256">Set environment variables</span><span class="sxs-lookup"><span data-stu-id="0a187-256">Set environment variables</span></span>
<span data-ttu-id="0a187-257">In this step, you will add environment variables to your web app configuration on Azure.</span><span class="sxs-lookup"><span data-stu-id="0a187-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="0a187-258">From the command line, enter the following:</span><span class="sxs-lookup"><span data-stu-id="0a187-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="0a187-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span><span class="sxs-lookup"><span data-stu-id="0a187-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="0a187-260">(Use the same values as the config.json file that you created earlier.)</span><span class="sxs-lookup"><span data-stu-id="0a187-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="0a187-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="0a187-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="0a187-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span><span class="sxs-lookup"><span data-stu-id="0a187-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="0a187-263">In your web app's blade, click **All Settings** > **Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a187-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="0a187-264">Scroll down to the **App settings** section and add the key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="0a187-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="0a187-266">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="0a187-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="0a187-267">Publish the application</span><span class="sxs-lookup"><span data-stu-id="0a187-267">Publish the application</span></span>
<span data-ttu-id="0a187-268">To publish the app, commit the code files to Git and then push to azure/master.</span><span class="sxs-lookup"><span data-stu-id="0a187-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="0a187-269">Set your deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="0a187-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="0a187-270">Add and commit your application files.</span><span class="sxs-lookup"><span data-stu-id="0a187-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="0a187-271">Push the commit to the App Service web app:</span><span class="sxs-lookup"><span data-stu-id="0a187-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="0a187-272">Use **master** as the target branch.</span><span class="sxs-lookup"><span data-stu-id="0a187-272">Use **master** as the target branch.</span></span> <span data-ttu-id="0a187-273">At the end of the deployment, you see a statement similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="0a187-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="0a187-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span><span class="sxs-lookup"><span data-stu-id="0a187-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a187-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a187-275">Next steps</span></span>
<span data-ttu-id="0a187-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="0a187-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0a187-277">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0a187-277">Additional resources</span></span>
<span data-ttu-id="0a187-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="0a187-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="0a187-279">What's changed</span><span class="sxs-lookup"><span data-stu-id="0a187-279">What's changed</span></span>
* <span data-ttu-id="0a187-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0a187-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[node]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remote]: http://git-scm.com/docs/git-remote

[Azure CLI]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[node-uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png







