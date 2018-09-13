---
title: MongoDB, Angular, and Node tutorial for Azure - Part 5 | Microsoft Docs
description: Part 5 of the tutorial series on creating a MongoDB app with Angular and Node on Azure Cosmos DB using the exact same APIs you use for MongoDB
services: cosmos-db
author: johnpapa
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 09/05/2017
ms.author: jopapa
ms.custom: mvc
ms.openlocfilehash: 5bb1aeadeb31728dcc2d9ac5fa0aeade31857169
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865399"
---
# <a name="create-a-mongodb-app-with-angular-and-azure-cosmos-db---part-5-use-mongoose-to-connect-to-azure-cosmos-db"></a><span data-ttu-id="098fa-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 5: Use Mongoose to connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="098fa-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 5: Use Mongoose to connect to Azure Cosmos DB</span></span>

<span data-ttu-id="098fa-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express, Angular, and your Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="098fa-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express, Angular, and your Azure Cosmos DB database.</span></span>

<span data-ttu-id="098fa-105">Part 5 of the tutorial builds on [Part 4](tutorial-develop-mongodb-nodejs-part4.md) and covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="098fa-105">Part 5 of the tutorial builds on [Part 4](tutorial-develop-mongodb-nodejs-part4.md) and covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="098fa-106">Use Mongoose to connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="098fa-106">Use Mongoose to connect to Azure Cosmos DB</span></span>
> * <span data-ttu-id="098fa-107">Get connection string information from Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="098fa-107">Get connection string information from Azure Cosmos DB</span></span>
> * <span data-ttu-id="098fa-108">Create the hero model</span><span class="sxs-lookup"><span data-stu-id="098fa-108">Create the hero model</span></span>
> * <span data-ttu-id="098fa-109">Create the hero service to get hero data</span><span class="sxs-lookup"><span data-stu-id="098fa-109">Create the hero service to get hero data</span></span>
> * <span data-ttu-id="098fa-110">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="098fa-110">Run the app locally</span></span>

## <a name="video-walkthrough"></a><span data-ttu-id="098fa-111">Video walkthrough</span><span class="sxs-lookup"><span data-stu-id="098fa-111">Video walkthrough</span></span>

> [!VIDEO https://www.youtube.com/embed/sI5hw6KPPXI]


## <a name="prerequisites"></a><span data-ttu-id="098fa-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="098fa-112">Prerequisites</span></span>

<span data-ttu-id="098fa-113">Before starting this part of the tutorial, ensure you've completed the steps in [Part 4](tutorial-develop-mongodb-nodejs-part4.md) of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="098fa-113">Before starting this part of the tutorial, ensure you've completed the steps in [Part 4](tutorial-develop-mongodb-nodejs-part4.md) of the tutorial.</span></span>

> [!TIP]
> <span data-ttu-id="098fa-114">This tutorial walks you through the steps to build the application step-by-step.</span><span class="sxs-lookup"><span data-stu-id="098fa-114">This tutorial walks you through the steps to build the application step-by-step.</span></span> <span data-ttu-id="098fa-115">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="098fa-115">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span></span>

## <a name="use-mongoose-to-connect-to-azure-cosmos-db"></a><span data-ttu-id="098fa-116">Use Mongoose to connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="098fa-116">Use Mongoose to connect to Azure Cosmos DB</span></span>

1. <span data-ttu-id="098fa-117">Install the mongoose npm module, which is an API normally used to talk to MongoDB.</span><span class="sxs-lookup"><span data-stu-id="098fa-117">Install the mongoose npm module, which is an API normally used to talk to MongoDB.</span></span>

    ```bash
    npm i mongoose --save
    ```

2. <span data-ttu-id="098fa-118">Now create a new file in your **server** folder called **mongo.js**.</span><span class="sxs-lookup"><span data-stu-id="098fa-118">Now create a new file in your **server** folder called **mongo.js**.</span></span> <span data-ttu-id="098fa-119">In this file, you add all of your connection info for the Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="098fa-119">In this file, you add all of your connection info for the Azure Cosmos DB database.</span></span>

3. <span data-ttu-id="098fa-120">Copy the following code into **mongo.js**.</span><span class="sxs-lookup"><span data-stu-id="098fa-120">Copy the following code into **mongo.js**.</span></span> <span data-ttu-id="098fa-121">This code:</span><span class="sxs-lookup"><span data-stu-id="098fa-121">This code:</span></span>
    * <span data-ttu-id="098fa-122">Requires Mongoose.</span><span class="sxs-lookup"><span data-stu-id="098fa-122">Requires Mongoose.</span></span>
    * <span data-ttu-id="098fa-123">Overrides the Mongo promise to use the basic promise that's built into ES6/ES2015 and above.</span><span class="sxs-lookup"><span data-stu-id="098fa-123">Overrides the Mongo promise to use the basic promise that's built into ES6/ES2015 and above.</span></span>
    * <span data-ttu-id="098fa-124">Calls on an env file that lets you set up certain things based on whether you're in staging, prod, or dev.</span><span class="sxs-lookup"><span data-stu-id="098fa-124">Calls on an env file that lets you set up certain things based on whether you're in staging, prod, or dev.</span></span> <span data-ttu-id="098fa-125">We will create that file soon.</span><span class="sxs-lookup"><span data-stu-id="098fa-125">We will create that file soon.</span></span>
    * <span data-ttu-id="098fa-126">Includes our MongoDB connection string, which will be set in the env file.</span><span class="sxs-lookup"><span data-stu-id="098fa-126">Includes our MongoDB connection string, which will be set in the env file.</span></span>
    * <span data-ttu-id="098fa-127">Creates a connect function that calls Mongoose.</span><span class="sxs-lookup"><span data-stu-id="098fa-127">Creates a connect function that calls Mongoose.</span></span>

    ```javascript
    const mongoose = require('mongoose');
    /**
     * Set to Node.js native promises
     * Per http://mongoosejs.com/docs/promises.html
     */
    mongoose.Promise = global.Promise;

    const env = require('./env/environment');

    // eslint-disable-next-line max-len
    const mongoUri = `mongodb://${env.accountName}:${env.key}@${env.accountName}.documents.azure.com:${env.port}/${env.databaseName}?ssl=true`;

    function connect() {
     mongoose.set('debug', true);
     return mongoose.connect(mongoUri, { useMongoClient: true });
    }

    module.exports = {
      connect,
      mongoose
    };
    ```
    
4. <span data-ttu-id="098fa-128">In the Explorer pane, create a folder under **server** called **environment** and in the **environment** folder create a new file called **environment.js**.</span><span class="sxs-lookup"><span data-stu-id="098fa-128">In the Explorer pane, create a folder under **server** called **environment** and in the **environment** folder create a new file called **environment.js**.</span></span>

5. <span data-ttu-id="098fa-129">From the mongo.js file, we know we need to include the `dbName`, the `key`, and the `cosmosPort`, so copy the following code into **environment.js**.</span><span class="sxs-lookup"><span data-stu-id="098fa-129">From the mongo.js file, we know we need to include the `dbName`, the `key`, and the `cosmosPort`, so copy the following code into **environment.js**.</span></span>

    ```javascript
    // TODO: replace if yours are different
    module.exports = {
      accountName: 'your-cosmosdb-account-name-goes-here',
      databaseName: 'admin', 
      key: 'your-key-goes-here',
      port: 10255
    };
    ```

## <a name="get-the-connection-string-information"></a><span data-ttu-id="098fa-130">Get the connection string information</span><span class="sxs-lookup"><span data-stu-id="098fa-130">Get the connection string information</span></span>

1. <span data-ttu-id="098fa-131">In **environment.js**, change the value of `port` to 10255.</span><span class="sxs-lookup"><span data-stu-id="098fa-131">In **environment.js**, change the value of `port` to 10255.</span></span> <span data-ttu-id="098fa-132">(You can find your Cosmos DB port the Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="098fa-132">(You can find your Cosmos DB port the Azure Portal)</span></span>

    ```javascript
    const port = 10255;
    ```

2. <span data-ttu-id="098fa-133">In **environment.js**, change the value of `accountName` to the name of the Azure Cosmos DB account you created in [Step 4](tutorial-develop-mongodb-nodejs-part4.md).</span><span class="sxs-lookup"><span data-stu-id="098fa-133">In **environment.js**, change the value of `accountName` to the name of the Azure Cosmos DB account you created in [Step 4](tutorial-develop-mongodb-nodejs-part4.md).</span></span> 

3. <span data-ttu-id="098fa-134">Retrieve the primary key for the Azure Cosmos DB account by using the following CLI command in the terminal window:</span><span class="sxs-lookup"><span data-stu-id="098fa-134">Retrieve the primary key for the Azure Cosmos DB account by using the following CLI command in the terminal window:</span></span> 

    ```azure-cli-interactive
    az cosmosdb list-keys --name <cosmosdb-name> -g myResourceGroup
    ```    
    
    * <span data-ttu-id="098fa-135">`<cosmosdb-name>` is the name of the Azure Cosmos DB account you created in [Step 4](tutorial-develop-mongodb-nodejs-part4.md).</span><span class="sxs-lookup"><span data-stu-id="098fa-135">`<cosmosdb-name>` is the name of the Azure Cosmos DB account you created in [Step 4](tutorial-develop-mongodb-nodejs-part4.md).</span></span>

4. <span data-ttu-id="098fa-136">Copy the primary key into the environment.js file as the `key` value.</span><span class="sxs-lookup"><span data-stu-id="098fa-136">Copy the primary key into the environment.js file as the `key` value.</span></span>

    <span data-ttu-id="098fa-137">Your app now has all the information it needs to connect to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="098fa-137">Your app now has all the information it needs to connect to Azure Cosmos DB.</span></span> <span data-ttu-id="098fa-138">This information can also be retrieved in the portal.</span><span class="sxs-lookup"><span data-stu-id="098fa-138">This information can also be retrieved in the portal.</span></span> <span data-ttu-id="098fa-139">For more information, see [Get the MongoDB connection string to customize](connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="098fa-139">For more information, see [Get the MongoDB connection string to customize](connect-mongodb-account.md#GetCustomConnection).</span></span> <span data-ttu-id="098fa-140">The Username in the portal equates to the dbName in environments.js.</span><span class="sxs-lookup"><span data-stu-id="098fa-140">The Username in the portal equates to the dbName in environments.js.</span></span> 

## <a name="create-a-hero-model"></a><span data-ttu-id="098fa-141">Create a Hero model</span><span class="sxs-lookup"><span data-stu-id="098fa-141">Create a Hero model</span></span>

1.  <span data-ttu-id="098fa-142">In the Explorer pane, create the file **hero.model.js** under the **server** folder.</span><span class="sxs-lookup"><span data-stu-id="098fa-142">In the Explorer pane, create the file **hero.model.js** under the **server** folder.</span></span>

2. <span data-ttu-id="098fa-143">Copy the following code into **hero.model.js**.</span><span class="sxs-lookup"><span data-stu-id="098fa-143">Copy the following code into **hero.model.js**.</span></span> <span data-ttu-id="098fa-144">This code:</span><span class="sxs-lookup"><span data-stu-id="098fa-144">This code:</span></span>
   * <span data-ttu-id="098fa-145">Requires Mongoose.</span><span class="sxs-lookup"><span data-stu-id="098fa-145">Requires Mongoose.</span></span>
   * <span data-ttu-id="098fa-146">Creates a new schema with an ID, name, and saying.</span><span class="sxs-lookup"><span data-stu-id="098fa-146">Creates a new schema with an ID, name, and saying.</span></span>
   * <span data-ttu-id="098fa-147">Creates a model using the schema.</span><span class="sxs-lookup"><span data-stu-id="098fa-147">Creates a model using the schema.</span></span>
   * <span data-ttu-id="098fa-148">Exports the model.</span><span class="sxs-lookup"><span data-stu-id="098fa-148">Exports the model.</span></span> 
   * <span data-ttu-id="098fa-149">Name the collection Heroes (instead of Heros, which would be the default name of the collection based on Mongoose plural naming rules).</span><span class="sxs-lookup"><span data-stu-id="098fa-149">Name the collection Heroes (instead of Heros, which would be the default name of the collection based on Mongoose plural naming rules).</span></span>

   ```javascript
   const mongoose = require('mongoose');

   const Schema = mongoose.Schema;

   const heroSchema = new Schema(
     {
       id: { type: Number, required: true, unique: true },
       name: String,
       saying: String
     },
     {
       collection: 'Heroes'
     }
   );

   const Hero = mongoose.model('Hero', heroSchema);

   module.exports = Hero;
   ```

## <a name="create-a-hero-service"></a><span data-ttu-id="098fa-150">Create a Hero service</span><span class="sxs-lookup"><span data-stu-id="098fa-150">Create a Hero service</span></span>

1.  <span data-ttu-id="098fa-151">In the Explorer pane, create the file **hero.service.js** under the **server** folder.</span><span class="sxs-lookup"><span data-stu-id="098fa-151">In the Explorer pane, create the file **hero.service.js** under the **server** folder.</span></span>

2. <span data-ttu-id="098fa-152">Copy the following code into **hero.service.js**.</span><span class="sxs-lookup"><span data-stu-id="098fa-152">Copy the following code into **hero.service.js**.</span></span> <span data-ttu-id="098fa-153">This code:</span><span class="sxs-lookup"><span data-stu-id="098fa-153">This code:</span></span>
   * <span data-ttu-id="098fa-154">Gets the model you just created</span><span class="sxs-lookup"><span data-stu-id="098fa-154">Gets the model you just created</span></span>
   * <span data-ttu-id="098fa-155">Connects to the database</span><span class="sxs-lookup"><span data-stu-id="098fa-155">Connects to the database</span></span>
   * <span data-ttu-id="098fa-156">Creates a docquery variable that uses the hero.find method to define a query that returns all heroes.</span><span class="sxs-lookup"><span data-stu-id="098fa-156">Creates a docquery variable that uses the hero.find method to define a query that returns all heroes.</span></span>
   * <span data-ttu-id="098fa-157">Runs a query with the docquery.exec with a promise to get a list of all heroes, where the response status is 200.</span><span class="sxs-lookup"><span data-stu-id="098fa-157">Runs a query with the docquery.exec with a promise to get a list of all heroes, where the response status is 200.</span></span> 
   * <span data-ttu-id="098fa-158">If the status is 500, sends back the error message</span><span class="sxs-lookup"><span data-stu-id="098fa-158">If the status is 500, sends back the error message</span></span>
   * <span data-ttu-id="098fa-159">Because we're using modules, it get the heroes.</span><span class="sxs-lookup"><span data-stu-id="098fa-159">Because we're using modules, it get the heroes.</span></span> 

   ```javascript
   const Hero = require('./hero.model');

   require('./mongo').connect();

   function getHeroes() {
     const docquery = Hero.find({});
     docquery
       .exec()
       .then(heroes => {
         res.status(200).json(heroes);
       })
       .catch(error => {
         res.status(500).send(error);
         return;
       });
   }

   module.exports = {
     getHeroes
   };
   ```

## <a name="add-the-hero-service-to-routesjs"></a><span data-ttu-id="098fa-160">Add the hero service to routes.js</span><span class="sxs-lookup"><span data-stu-id="098fa-160">Add the hero service to routes.js</span></span>

1. <span data-ttu-id="098fa-161">In Visual Studio Code, in **routes.js**, comment out the `res.send` function that sends the sample hero data and add a line to call the `heroService.getHeroes` function instead.</span><span class="sxs-lookup"><span data-stu-id="098fa-161">In Visual Studio Code, in **routes.js**, comment out the `res.send` function that sends the sample hero data and add a line to call the `heroService.getHeroes` function instead.</span></span>

    ```javascript
    router.get('/heroes', (req, res) => {
      heroService.getHeroes(req, res);
    //  res.send(200, [
    //      {"id": 10, "name": "Starlord", "saying": "oh yeah"}
    //  ])
    });
    ```

2. <span data-ttu-id="098fa-162">In **routes.js** require the hero service:</span><span class="sxs-lookup"><span data-stu-id="098fa-162">In **routes.js** require the hero service:</span></span>

    ```javascript
    const heroService = require('./hero.service'); 
    ```

3. <span data-ttu-id="098fa-163">In **hero.service.js**, update the getHeroes function to take the `req` and `res` parameters as follows:</span><span class="sxs-lookup"><span data-stu-id="098fa-163">In **hero.service.js**, update the getHeroes function to take the `req` and `res` parameters as follows:</span></span>

    ```javascript
    function getHeroes(req, res) {
    ```

    <span data-ttu-id="098fa-164">Let's take a minute to review and walk through the call chain here.</span><span class="sxs-lookup"><span data-stu-id="098fa-164">Let's take a minute to review and walk through the call chain here.</span></span> <span data-ttu-id="098fa-165">First we come into the `index.js`, which sets up the node server, and notice that's setting up and defining our routes.</span><span class="sxs-lookup"><span data-stu-id="098fa-165">First we come into the `index.js`, which sets up the node server, and notice that's setting up and defining our routes.</span></span> <span data-ttu-id="098fa-166">Our routes.js file then talks to the hero service and tells it to go get our functions like getHeroes and pass the request and response.</span><span class="sxs-lookup"><span data-stu-id="098fa-166">Our routes.js file then talks to the hero service and tells it to go get our functions like getHeroes and pass the request and response.</span></span> <span data-ttu-id="098fa-167">Here hero.service.js is going to grab the model and connect to Mongo, and then it's going to execute getHeroes when we call it, and return back a response of 200.</span><span class="sxs-lookup"><span data-stu-id="098fa-167">Here hero.service.js is going to grab the model and connect to Mongo, and then it's going to execute getHeroes when we call it, and return back a response of 200.</span></span> <span data-ttu-id="098fa-168">Then it bubbles back out through the chain.</span><span class="sxs-lookup"><span data-stu-id="098fa-168">Then it bubbles back out through the chain.</span></span> 

## <a name="run-the-app"></a><span data-ttu-id="098fa-169">Run the app</span><span class="sxs-lookup"><span data-stu-id="098fa-169">Run the app</span></span>

1. <span data-ttu-id="098fa-170">Now lets run the app again.</span><span class="sxs-lookup"><span data-stu-id="098fa-170">Now lets run the app again.</span></span> <span data-ttu-id="098fa-171">In Visual Studio Code, save all your changes, click the **Debug** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part5/debug-button.png) on the left side, then click the **Start Debugging** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part5/start-debugging-button.png).</span><span class="sxs-lookup"><span data-stu-id="098fa-171">In Visual Studio Code, save all your changes, click the **Debug** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part5/debug-button.png) on the left side, then click the **Start Debugging** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part5/start-debugging-button.png).</span></span>

3. <span data-ttu-id="098fa-172">Now lets flip over to the browser, open the Developer tools and the Network tab, then navigate to http://localhost:3000, and there's our application.</span><span class="sxs-lookup"><span data-stu-id="098fa-172">Now lets flip over to the browser, open the Developer tools and the Network tab, then navigate to http://localhost:3000, and there's our application.</span></span>

    ![New Azure Cosmos DB account in the Azure portal](./media/tutorial-develop-mongodb-nodejs-part5/azure-cosmos-db-heroes-app.png)

   <span data-ttu-id="098fa-174">There are no heroes stored in the app yet, but in the next step of the tutorial we'll add the put, push, and delete functionality so we can add, update, and delete heroes from the UI using Mongoose connections to our Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="098fa-174">There are no heroes stored in the app yet, but in the next step of the tutorial we'll add the put, push, and delete functionality so we can add, update, and delete heroes from the UI using Mongoose connections to our Azure Cosmos DB database.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="098fa-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="098fa-175">Next steps</span></span>

<span data-ttu-id="098fa-176">In this part of the tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="098fa-176">In this part of the tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="098fa-177">Used Mongoose APIs to connect your heroes app to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="098fa-177">Used Mongoose APIs to connect your heroes app to Azure Cosmos DB</span></span> 
> * <span data-ttu-id="098fa-178">Added the get heroes functionality to the app</span><span class="sxs-lookup"><span data-stu-id="098fa-178">Added the get heroes functionality to the app</span></span>

<span data-ttu-id="098fa-179">You can proceed to the next part of the tutorial to add Post, Put, and Delete functions to the app.</span><span class="sxs-lookup"><span data-stu-id="098fa-179">You can proceed to the next part of the tutorial to add Post, Put, and Delete functions to the app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="098fa-180">Add Post, Put, and Delete functions to the app</span><span class="sxs-lookup"><span data-stu-id="098fa-180">Add Post, Put, and Delete functions to the app</span></span>](tutorial-develop-mongodb-nodejs-part6.md)
