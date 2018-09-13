---
title: MongoDB, Angular, and Node tutorial for Azure - Part 2 | Microsoft Docs
description: Part 2 of the tutorial series on creating a MongoDB app with Angular and Node on Azure Cosmos DB using the exact same APIs you use for MongoDB.
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
ms.openlocfilehash: 99fc6c7dc43f66d92b17f25ad0fba52ce8f34413
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866081"
---
# <a name="create-a-mongodb-app-with-angular-and-azure-cosmos-db---part-2-create-a-nodejs-express-app-with-the-angular-cli"></a><span data-ttu-id="8867e-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 2: Create a Node.js Express app with the Angular CLI</span><span class="sxs-lookup"><span data-stu-id="8867e-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 2: Create a Node.js Express app with the Angular CLI</span></span> 

<span data-ttu-id="8867e-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express, Angular, and your Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="8867e-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express, Angular, and your Azure Cosmos DB database.</span></span>

<span data-ttu-id="8867e-105">Part 2 of the tutorial builds on [the introduction](tutorial-develop-mongodb-nodejs.md) and covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8867e-105">Part 2 of the tutorial builds on [the introduction](tutorial-develop-mongodb-nodejs.md) and covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8867e-106">Install the Angular CLI and TypeScript</span><span class="sxs-lookup"><span data-stu-id="8867e-106">Install the Angular CLI and TypeScript</span></span>
> * <span data-ttu-id="8867e-107">Create a new project using Angular</span><span class="sxs-lookup"><span data-stu-id="8867e-107">Create a new project using Angular</span></span>
> * <span data-ttu-id="8867e-108">Build out the app using the Express framework</span><span class="sxs-lookup"><span data-stu-id="8867e-108">Build out the app using the Express framework</span></span>
> * <span data-ttu-id="8867e-109">Test the app in Postman</span><span class="sxs-lookup"><span data-stu-id="8867e-109">Test the app in Postman</span></span>

## <a name="video-walkthrough"></a><span data-ttu-id="8867e-110">Video walkthrough</span><span class="sxs-lookup"><span data-stu-id="8867e-110">Video walkthrough</span></span>

> [!VIDEO https://www.youtube.com/embed/lIwJIYcGSUg]

## <a name="prerequisites"></a><span data-ttu-id="8867e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8867e-111">Prerequisites</span></span>

<span data-ttu-id="8867e-112">Before starting this part of the tutorial, ensure you've watched the [introduction video](tutorial-develop-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8867e-112">Before starting this part of the tutorial, ensure you've watched the [introduction video](tutorial-develop-mongodb-nodejs.md).</span></span>

<span data-ttu-id="8867e-113">This tutorial also requires:</span><span class="sxs-lookup"><span data-stu-id="8867e-113">This tutorial also requires:</span></span> 
* <span data-ttu-id="8867e-114">[Node.js](https://nodejs.org/) version 8.4.0 or above.</span><span class="sxs-lookup"><span data-stu-id="8867e-114">[Node.js](https://nodejs.org/) version 8.4.0 or above.</span></span>
* [<span data-ttu-id="8867e-115">Postman</span><span class="sxs-lookup"><span data-stu-id="8867e-115">Postman</span></span>](https://www.getpostman.com/)
* <span data-ttu-id="8867e-116">[Visual Studio Code](https://code.visualstudio.com/) or your favorite code editor.</span><span class="sxs-lookup"><span data-stu-id="8867e-116">[Visual Studio Code](https://code.visualstudio.com/) or your favorite code editor.</span></span>

> [!TIP]
> <span data-ttu-id="8867e-117">This tutorial walks you through the steps to build the application step-by-step.</span><span class="sxs-lookup"><span data-stu-id="8867e-117">This tutorial walks you through the steps to build the application step-by-step.</span></span> <span data-ttu-id="8867e-118">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8867e-118">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span></span>

## <a name="install-the-angular-cli-and-typescript"></a><span data-ttu-id="8867e-119">Install the Angular CLI and TypeScript</span><span class="sxs-lookup"><span data-stu-id="8867e-119">Install the Angular CLI and TypeScript</span></span>

1. <span data-ttu-id="8867e-120">Open a Windows Command Prompt or Mac Terminal window and install the Angular CLI.</span><span class="sxs-lookup"><span data-stu-id="8867e-120">Open a Windows Command Prompt or Mac Terminal window and install the Angular CLI.</span></span>

    ```bash
    npm install -g @angular/cli
    ```

2. <span data-ttu-id="8867e-121">Install TypeScript by entering the following command in the prompt.</span><span class="sxs-lookup"><span data-stu-id="8867e-121">Install TypeScript by entering the following command in the prompt.</span></span> 

    ```bash
    npm install -g typescript
    ```

## <a name="use-the-angular-cli-to-create-a-new-project"></a><span data-ttu-id="8867e-122">Use the Angular CLI to create a new project</span><span class="sxs-lookup"><span data-stu-id="8867e-122">Use the Angular CLI to create a new project</span></span>

1. <span data-ttu-id="8867e-123">At the command prompt, change to the folder where you want to create your new project, then run the following command.</span><span class="sxs-lookup"><span data-stu-id="8867e-123">At the command prompt, change to the folder where you want to create your new project, then run the following command.</span></span> <span data-ttu-id="8867e-124">This command creates a new folder and project named angular-cosmosdb and installs the Angular components required for a new app.</span><span class="sxs-lookup"><span data-stu-id="8867e-124">This command creates a new folder and project named angular-cosmosdb and installs the Angular components required for a new app.</span></span> <span data-ttu-id="8867e-125">It uses the minimal setup (--minimal), and specifies that the project uses Sass (a CSS-like syntax with the flag --style scss).</span><span class="sxs-lookup"><span data-stu-id="8867e-125">It uses the minimal setup (--minimal), and specifies that the project uses Sass (a CSS-like syntax with the flag --style scss).</span></span>

    ```bash
    ng new angular-cosmosdb --minimal --style scss
    ```

2. <span data-ttu-id="8867e-126">Once the command completes, change directories into the src/client folder.</span><span class="sxs-lookup"><span data-stu-id="8867e-126">Once the command completes, change directories into the src/client folder.</span></span>

    ```bash
    cd angular-cosmosdb
    ```

3. <span data-ttu-id="8867e-127">Then open the folder in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8867e-127">Then open the folder in Visual Studio Code.</span></span>

    ```bash
    code .
    ```

## <a name="build-the-app-using-the-express-framework"></a><span data-ttu-id="8867e-128">Build the app using the Express framework</span><span class="sxs-lookup"><span data-stu-id="8867e-128">Build the app using the Express framework</span></span>

1. <span data-ttu-id="8867e-129">In Visual Studio Code, in the **Explorer** pane, right-click the **src** folder, click **New Folder**, and name the new folder *server*.</span><span class="sxs-lookup"><span data-stu-id="8867e-129">In Visual Studio Code, in the **Explorer** pane, right-click the **src** folder, click **New Folder**, and name the new folder *server*.</span></span>

2. <span data-ttu-id="8867e-130">In the **Explorer** pane, right-click the **server** folder, click **New File**, and name the new file *index.js*.</span><span class="sxs-lookup"><span data-stu-id="8867e-130">In the **Explorer** pane, right-click the **server** folder, click **New File**, and name the new file *index.js*.</span></span>

3. <span data-ttu-id="8867e-131">Back at the command prompt, use the following command to install the body parser.</span><span class="sxs-lookup"><span data-stu-id="8867e-131">Back at the command prompt, use the following command to install the body parser.</span></span> <span data-ttu-id="8867e-132">This helps our app parse the JSON data that are passed in through the APIs.</span><span class="sxs-lookup"><span data-stu-id="8867e-132">This helps our app parse the JSON data that are passed in through the APIs.</span></span>

    ```bash
    npm i express body-parser --save
    ```

4. <span data-ttu-id="8867e-133">In Visual Studio Code, copy the following code into the index.js file.</span><span class="sxs-lookup"><span data-stu-id="8867e-133">In Visual Studio Code, copy the following code into the index.js file.</span></span> <span data-ttu-id="8867e-134">This code:</span><span class="sxs-lookup"><span data-stu-id="8867e-134">This code:</span></span>
    * <span data-ttu-id="8867e-135">References Express</span><span class="sxs-lookup"><span data-stu-id="8867e-135">References Express</span></span>
    * <span data-ttu-id="8867e-136">Pulls in the body-parser for reading JSON data in the body of requests</span><span class="sxs-lookup"><span data-stu-id="8867e-136">Pulls in the body-parser for reading JSON data in the body of requests</span></span>
    * <span data-ttu-id="8867e-137">Uses a built-in feature called path</span><span class="sxs-lookup"><span data-stu-id="8867e-137">Uses a built-in feature called path</span></span>
    * <span data-ttu-id="8867e-138">Sets root variables to make it easier to find where our code is located</span><span class="sxs-lookup"><span data-stu-id="8867e-138">Sets root variables to make it easier to find where our code is located</span></span>
    * <span data-ttu-id="8867e-139">Sets up a port</span><span class="sxs-lookup"><span data-stu-id="8867e-139">Sets up a port</span></span>
    * <span data-ttu-id="8867e-140">Cranks up Express</span><span class="sxs-lookup"><span data-stu-id="8867e-140">Cranks up Express</span></span>
    * <span data-ttu-id="8867e-141">Tells the app how to use the middleware that were going to be using to serve up the server</span><span class="sxs-lookup"><span data-stu-id="8867e-141">Tells the app how to use the middleware that were going to be using to serve up the server</span></span>
    * <span data-ttu-id="8867e-142">Serves everything that's in the dist folder, which will be the static content</span><span class="sxs-lookup"><span data-stu-id="8867e-142">Serves everything that's in the dist folder, which will be the static content</span></span>
    * <span data-ttu-id="8867e-143">Serves up the application, and serves index.html for any GET requests not found on the server (for deep links)</span><span class="sxs-lookup"><span data-stu-id="8867e-143">Serves up the application, and serves index.html for any GET requests not found on the server (for deep links)</span></span>
    * <span data-ttu-id="8867e-144">Starts the server with app.listen</span><span class="sxs-lookup"><span data-stu-id="8867e-144">Starts the server with app.listen</span></span>
    * <span data-ttu-id="8867e-145">Uses an arow function to log that the port is alive</span><span class="sxs-lookup"><span data-stu-id="8867e-145">Uses an arow function to log that the port is alive</span></span>
    
   ```node
   const express = require('express');
   const bodyParser = require('body-parser');
   const path = require('path');
   const routes = require('./routes');

   const root = './';
   const port = process.env.PORT || '3000';
   const app = express();

   app.use(bodyParser.json());
   app.use(bodyParser.urlencoded({ extended: false }));
   app.use(express.static(path.join(root, 'dist/angular-cosmosdb')));
   app.use('/api', routes);
   app.get('*', (req, res) => {
     res.sendFile('dist/angular-cosmosdb/index.html', {root});
   });

   app.listen(port, () => console.log(`API running on localhost:${port}`));
   ```

5. <span data-ttu-id="8867e-146">In Visual Studio Code, in the **Explorer** pane, right-click the **server** folder, and then click **New file**.</span><span class="sxs-lookup"><span data-stu-id="8867e-146">In Visual Studio Code, in the **Explorer** pane, right-click the **server** folder, and then click **New file**.</span></span> <span data-ttu-id="8867e-147">Name the new file *routes.js*.</span><span class="sxs-lookup"><span data-stu-id="8867e-147">Name the new file *routes.js*.</span></span> 

6. <span data-ttu-id="8867e-148">Copy the following code into **routes.js**.</span><span class="sxs-lookup"><span data-stu-id="8867e-148">Copy the following code into **routes.js**.</span></span> <span data-ttu-id="8867e-149">This code:</span><span class="sxs-lookup"><span data-stu-id="8867e-149">This code:</span></span>
   * <span data-ttu-id="8867e-150">References the Express router</span><span class="sxs-lookup"><span data-stu-id="8867e-150">References the Express router</span></span>
   * <span data-ttu-id="8867e-151">Gets the heroes</span><span class="sxs-lookup"><span data-stu-id="8867e-151">Gets the heroes</span></span>
   * <span data-ttu-id="8867e-152">Sends back the JSON for a defined hero</span><span class="sxs-lookup"><span data-stu-id="8867e-152">Sends back the JSON for a defined hero</span></span>

   ```node
   const express = require('express');
   const router = express.Router();

   router.get('/heroes', (req, res) => {
    res.send(200, [
       {"id": 10, "name": "Starlord", "saying": "oh yeah"}
    ])
   });

   module.exports=router;
   ```

7. <span data-ttu-id="8867e-153">Save all your modified files.</span><span class="sxs-lookup"><span data-stu-id="8867e-153">Save all your modified files.</span></span> 

8. <span data-ttu-id="8867e-154">In Visual Studio Code, click the **Debug** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part2/debug-button.png), click the Gear button ![Gear button in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part2/gear-button.png).</span><span class="sxs-lookup"><span data-stu-id="8867e-154">In Visual Studio Code, click the **Debug** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part2/debug-button.png), click the Gear button ![Gear button in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part2/gear-button.png).</span></span> <span data-ttu-id="8867e-155">The new launch.json file opens in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8867e-155">The new launch.json file opens in Visual Studio Code.</span></span>

8. <span data-ttu-id="8867e-156">On line 11 of the launch.json file, change `"${workspaceFolder}\\server"` to `"program": "${workspaceRoot}/src/server/index.js"` and save the file.</span><span class="sxs-lookup"><span data-stu-id="8867e-156">On line 11 of the launch.json file, change `"${workspaceFolder}\\server"` to `"program": "${workspaceRoot}/src/server/index.js"` and save the file.</span></span>

9. <span data-ttu-id="8867e-157">Click the **Start Debugging** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part2/start-debugging-button.png) to run the app.</span><span class="sxs-lookup"><span data-stu-id="8867e-157">Click the **Start Debugging** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part2/start-debugging-button.png) to run the app.</span></span>

    <span data-ttu-id="8867e-158">The app should run without errors.</span><span class="sxs-lookup"><span data-stu-id="8867e-158">The app should run without errors.</span></span>

## <a name="use-postman-to-test-the-app"></a><span data-ttu-id="8867e-159">Use Postman to test the app</span><span class="sxs-lookup"><span data-stu-id="8867e-159">Use Postman to test the app</span></span>

1. <span data-ttu-id="8867e-160">Now open Postman and put `http://localhost:3000/api/heroes` in the GET box.</span><span class="sxs-lookup"><span data-stu-id="8867e-160">Now open Postman and put `http://localhost:3000/api/heroes` in the GET box.</span></span> 

2. <span data-ttu-id="8867e-161">Click the **Send** button and get the json response from the app.</span><span class="sxs-lookup"><span data-stu-id="8867e-161">Click the **Send** button and get the json response from the app.</span></span> 

    <span data-ttu-id="8867e-162">This response shows the app is up and running locally.</span><span class="sxs-lookup"><span data-stu-id="8867e-162">This response shows the app is up and running locally.</span></span> 

    ![Postman showing the request and the response](./media/tutorial-develop-mongodb-nodejs-part2/azure-cosmos-db-postman.png)


## <a name="next-steps"></a><span data-ttu-id="8867e-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="8867e-164">Next steps</span></span>

<span data-ttu-id="8867e-165">In this part of the tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="8867e-165">In this part of the tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8867e-166">Created a Node.js project using the Angular CLI</span><span class="sxs-lookup"><span data-stu-id="8867e-166">Created a Node.js project using the Angular CLI</span></span>
> * <span data-ttu-id="8867e-167">Tested the app using Postman</span><span class="sxs-lookup"><span data-stu-id="8867e-167">Tested the app using Postman</span></span>

<span data-ttu-id="8867e-168">You can proceed to the next part of the tutorial to build the UI.</span><span class="sxs-lookup"><span data-stu-id="8867e-168">You can proceed to the next part of the tutorial to build the UI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8867e-169">Build the UI with Angular</span><span class="sxs-lookup"><span data-stu-id="8867e-169">Build the UI with Angular</span></span>](tutorial-develop-mongodb-nodejs-part3.md)
