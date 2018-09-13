---
title: MongoDB, Angular, and Node tutorial for Azure - Part 6 | Microsoft Docs
description: Part 6 of the tutorial series on creating a MongoDB app with Angular and Node on Azure Cosmos DB using the exact same APIs you use for MongoDB
services: cosmos-db
author: johnpapa
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/17/2018
ms.author: jopapa
ms.custom: mvc
ms.openlocfilehash: a1705913e1656901d0a87a3cebb2eb69a6c7ad63
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871686"
---
# <a name="create-a-mongodb-app-with-angular-and-azure-cosmos-db---part-6-add-post-put-and-delete-functions-to-the-app"></a><span data-ttu-id="a6609-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 6: Add Post, Put, and Delete functions to the app</span><span class="sxs-lookup"><span data-stu-id="a6609-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 6: Add Post, Put, and Delete functions to the app</span></span>

<span data-ttu-id="a6609-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express and Angular and then connect it to your Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="a6609-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express and Angular and then connect it to your Azure Cosmos DB database.</span></span>

<span data-ttu-id="a6609-105">Part 6 of the tutorial builds on [Part 5](tutorial-develop-mongodb-nodejs-part5.md) and covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="a6609-105">Part 6 of the tutorial builds on [Part 5](tutorial-develop-mongodb-nodejs-part5.md) and covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a6609-106">Create Post, Put, and Delete functions for the hero service</span><span class="sxs-lookup"><span data-stu-id="a6609-106">Create Post, Put, and Delete functions for the hero service</span></span>
> * <span data-ttu-id="a6609-107">Run the app</span><span class="sxs-lookup"><span data-stu-id="a6609-107">Run the app</span></span>

> [!VIDEO https://www.youtube.com/embed/Y5mdAlFGZjc]

## <a name="prerequisites"></a><span data-ttu-id="a6609-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a6609-108">Prerequisites</span></span>

<span data-ttu-id="a6609-109">Before starting this part of the tutorial, ensure you've completed the steps in [Part 5](tutorial-develop-mongodb-nodejs-part5.md) of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a6609-109">Before starting this part of the tutorial, ensure you've completed the steps in [Part 5](tutorial-develop-mongodb-nodejs-part5.md) of the tutorial.</span></span>

> [!TIP]
> <span data-ttu-id="a6609-110">This tutorial walks you through the steps to build the application step-by-step.</span><span class="sxs-lookup"><span data-stu-id="a6609-110">This tutorial walks you through the steps to build the application step-by-step.</span></span> <span data-ttu-id="a6609-111">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="a6609-111">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span></span>

## <a name="add-a-post-function-to-the-hero-service"></a><span data-ttu-id="a6609-112">Add a Post function to the hero service</span><span class="sxs-lookup"><span data-stu-id="a6609-112">Add a Post function to the hero service</span></span>

1. <span data-ttu-id="a6609-113">In Visual Studio Code, open **routes.js** and **hero.service.js** side by side by pressing the **Split Editor** button ![Split Editor button in Visual Studio](./media/tutorial-develop-mongodb-nodejs-part6/split-editor-button.png).</span><span class="sxs-lookup"><span data-stu-id="a6609-113">In Visual Studio Code, open **routes.js** and **hero.service.js** side by side by pressing the **Split Editor** button ![Split Editor button in Visual Studio](./media/tutorial-develop-mongodb-nodejs-part6/split-editor-button.png).</span></span>

    <span data-ttu-id="a6609-114">See that routes.js line 7 is calling the `getHeroes` function on line 5 in **hero.service.js**.</span><span class="sxs-lookup"><span data-stu-id="a6609-114">See that routes.js line 7 is calling the `getHeroes` function on line 5 in **hero.service.js**.</span></span>  <span data-ttu-id="a6609-115">We need to create this same pairing for the post, put, and delete functions.</span><span class="sxs-lookup"><span data-stu-id="a6609-115">We need to create this same pairing for the post, put, and delete functions.</span></span> 

    ![routes.js and hero.service.js in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/routes-heroservicejs.png)
    
    <span data-ttu-id="a6609-117">Let's start by coding up the hero service.</span><span class="sxs-lookup"><span data-stu-id="a6609-117">Let's start by coding up the hero service.</span></span> 

2. <span data-ttu-id="a6609-118">Copy the following code into **hero.service.js** after the `getHeroes` function and before `module.exports`.</span><span class="sxs-lookup"><span data-stu-id="a6609-118">Copy the following code into **hero.service.js** after the `getHeroes` function and before `module.exports`.</span></span> <span data-ttu-id="a6609-119">This code:</span><span class="sxs-lookup"><span data-stu-id="a6609-119">This code:</span></span>  
   * <span data-ttu-id="a6609-120">Uses the hero model to post a new hero.</span><span class="sxs-lookup"><span data-stu-id="a6609-120">Uses the hero model to post a new hero.</span></span>
   * <span data-ttu-id="a6609-121">Checks the responses to see if there's an error and returns a status value of 500.</span><span class="sxs-lookup"><span data-stu-id="a6609-121">Checks the responses to see if there's an error and returns a status value of 500.</span></span>

   ```javascript
   function postHero(req, res) {
     const originalHero = { uid: req.body.uid, name: req.body.name, saying: req.body.saying };
     const hero = new Hero(originalHero);
     hero.save(error => {
       if (checkServerError(res, error)) return;
       res.status(201).json(hero);
       console.log('Hero created successfully!');
     });
   }

   function checkServerError(res, error) {
     if (error) {
       res.status(500).send(error);
       return error;
     }
   }
   ```

3. <span data-ttu-id="a6609-122">In **hero.service.js**, update the `module.exports` to include the new `postHero` function.</span><span class="sxs-lookup"><span data-stu-id="a6609-122">In **hero.service.js**, update the `module.exports` to include the new `postHero` function.</span></span> 

    ```javascript
    module.exports = {
      getHeroes,
      postHero
    };
    ```

4. <span data-ttu-id="a6609-123">In **routes.js**, add a router for the `post` function after the `get` router.</span><span class="sxs-lookup"><span data-stu-id="a6609-123">In **routes.js**, add a router for the `post` function after the `get` router.</span></span> <span data-ttu-id="a6609-124">This router posts one hero at a time.</span><span class="sxs-lookup"><span data-stu-id="a6609-124">This router posts one hero at a time.</span></span> <span data-ttu-id="a6609-125">Structuring the router file this way cleanly shows you all of the available API endpoints and leaves the real work to the **hero.service.js** file.</span><span class="sxs-lookup"><span data-stu-id="a6609-125">Structuring the router file this way cleanly shows you all of the available API endpoints and leaves the real work to the **hero.service.js** file.</span></span>

    ```javascript
    router.post('/hero', (req, res) => {
      heroService.postHero(req, res);
    });
    ```

5. <span data-ttu-id="a6609-126">Check that everything worked by running the app.</span><span class="sxs-lookup"><span data-stu-id="a6609-126">Check that everything worked by running the app.</span></span> <span data-ttu-id="a6609-127">In Visual Studio Code, save all your changes, click the **Debug** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/debug-button.png) on the left side, then click the **Start Debugging** button ![Start debugging icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/start-debugging-button.png).</span><span class="sxs-lookup"><span data-stu-id="a6609-127">In Visual Studio Code, save all your changes, click the **Debug** button ![Debug icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/debug-button.png) on the left side, then click the **Start Debugging** button ![Start debugging icon in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/start-debugging-button.png).</span></span>

6. <span data-ttu-id="a6609-128">Now go back to your internet browser and open the Developer tools Network tab by pressing F12 on most machines.</span><span class="sxs-lookup"><span data-stu-id="a6609-128">Now go back to your internet browser and open the Developer tools Network tab by pressing F12 on most machines.</span></span> <span data-ttu-id="a6609-129">Navigate to [http://localhost:3000](http://localhost:3000) to watch the calls made over the network.</span><span class="sxs-lookup"><span data-stu-id="a6609-129">Navigate to [http://localhost:3000](http://localhost:3000) to watch the calls made over the network.</span></span>

    ![Networking tab in Chrome that shows network activity](./media/tutorial-develop-mongodb-nodejs-part6/add-new-hero.png)

7. <span data-ttu-id="a6609-131">Add a new hero by clicking the **Add New Hero** button.</span><span class="sxs-lookup"><span data-stu-id="a6609-131">Add a new hero by clicking the **Add New Hero** button.</span></span> <span data-ttu-id="a6609-132">Enter an ID of "999", name of "Fred", and saying of "Hello", then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6609-132">Enter an ID of "999", name of "Fred", and saying of "Hello", then click **Save**.</span></span> <span data-ttu-id="a6609-133">You should see in the Networking tab you've sent a POST request for a new hero.</span><span class="sxs-lookup"><span data-stu-id="a6609-133">You should see in the Networking tab you've sent a POST request for a new hero.</span></span> 

    ![Networking tab in Chrome that shows network activity for Get and Post functions](./media/tutorial-develop-mongodb-nodejs-part6/post-new-hero.png)

    <span data-ttu-id="a6609-135">Now let's go back and add the Put and Delete functions to the app.</span><span class="sxs-lookup"><span data-stu-id="a6609-135">Now let's go back and add the Put and Delete functions to the app.</span></span>

## <a name="add-the-put-and-delete-functions"></a><span data-ttu-id="a6609-136">Add the Put and Delete functions</span><span class="sxs-lookup"><span data-stu-id="a6609-136">Add the Put and Delete functions</span></span>

1. <span data-ttu-id="a6609-137">In **routes.js**, add the `put` and `delete` routers after the post router.</span><span class="sxs-lookup"><span data-stu-id="a6609-137">In **routes.js**, add the `put` and `delete` routers after the post router.</span></span>

    ```javascript
    router.put('/hero/:uid', (req, res) => {
      heroService.putHero(req, res);
    });

    router.delete('/hero/:uid', (req, res) => {
      heroService.deleteHero(req, res);
    });
    ```

2. <span data-ttu-id="a6609-138">Copy the following code into **hero.service.js** after the `checkServerError` function.</span><span class="sxs-lookup"><span data-stu-id="a6609-138">Copy the following code into **hero.service.js** after the `checkServerError` function.</span></span> <span data-ttu-id="a6609-139">This code:</span><span class="sxs-lookup"><span data-stu-id="a6609-139">This code:</span></span>
   * <span data-ttu-id="a6609-140">Creates the `put` and `delete` functions</span><span class="sxs-lookup"><span data-stu-id="a6609-140">Creates the `put` and `delete` functions</span></span>
   * <span data-ttu-id="a6609-141">Performs a check on whether the hero was found</span><span class="sxs-lookup"><span data-stu-id="a6609-141">Performs a check on whether the hero was found</span></span>
   * <span data-ttu-id="a6609-142">Performs error handling</span><span class="sxs-lookup"><span data-stu-id="a6609-142">Performs error handling</span></span> 

   ```javascript
   function putHero(req, res) {
     const originalHero = {
       uid: parseInt(req.params.uid, 10),
       name: req.body.name,
       saying: req.body.saying
     };
     Hero.findOne({ uid: originalHero.uid }, (error, hero) => {
       if (checkServerError(res, error)) return;
       if (!checkFound(res, hero)) return;

      hero.name = originalHero.name;
       hero.saying = originalHero.saying;
       hero.save(error => {
         if (checkServerError(res, error)) return;
         res.status(200).json(hero);
         console.log('Hero updated successfully!');
       });
     });
   }

   function deleteHero(req, res) {
     const uid = parseInt(req.params.uid, 10);
     Hero.findOneAndRemove({ uid: uid })
       .then(hero => {
         if (!checkFound(res, hero)) return;
         res.status(200).json(hero);
         console.log('Hero deleted successfully!');
       })
       .catch(error => {
         if (checkServerError(res, error)) return;
       });
   }

   function checkFound(res, hero) {
     if (!hero) {
       res.status(404).send('Hero not found.');
       return;
     }
     return hero;
   }
   ```

3. <span data-ttu-id="a6609-143">In **hero.service.js**, export the new modules:</span><span class="sxs-lookup"><span data-stu-id="a6609-143">In **hero.service.js**, export the new modules:</span></span>

   ```javascript
    module.exports = {
      getHeroes,
      postHero,
      putHero,
      deleteHero
    };
    ```

4. <span data-ttu-id="a6609-144">Now that we've updated the code, click the **Restart** button ![Restart button in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/restart-debugger-button.png) in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a6609-144">Now that we've updated the code, click the **Restart** button ![Restart button in Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part6/restart-debugger-button.png) in Visual Studio Code.</span></span>

5. <span data-ttu-id="a6609-145">Refresh the page in your internet browser and click the **Add New Hero** button.</span><span class="sxs-lookup"><span data-stu-id="a6609-145">Refresh the page in your internet browser and click the **Add New Hero** button.</span></span> <span data-ttu-id="a6609-146">Add a new hero with an ID of "9", name of "Starlord", and saying "Hi".</span><span class="sxs-lookup"><span data-stu-id="a6609-146">Add a new hero with an ID of "9", name of "Starlord", and saying "Hi".</span></span> <span data-ttu-id="a6609-147">Click the **Save** button to save the new hero.</span><span class="sxs-lookup"><span data-stu-id="a6609-147">Click the **Save** button to save the new hero.</span></span>

6. <span data-ttu-id="a6609-148">Now select the **Starlord** hero, and change the saying from "Hi" to "Bye", then click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a6609-148">Now select the **Starlord** hero, and change the saying from "Hi" to "Bye", then click the **Save** button.</span></span> 

    <span data-ttu-id="a6609-149">You can now select the ID in the Network tab to show the payload.</span><span class="sxs-lookup"><span data-stu-id="a6609-149">You can now select the ID in the Network tab to show the payload.</span></span> <span data-ttu-id="a6609-150">You can see in the payload that the saying is now set to "Bye".</span><span class="sxs-lookup"><span data-stu-id="a6609-150">You can see in the payload that the saying is now set to "Bye".</span></span>

    ![Heroes app and Networking tab showing the payload](./media/tutorial-develop-mongodb-nodejs-part6/put-hero-function.png) 

    <span data-ttu-id="a6609-152">You can also delete one of the heroes in the UI, and see the times it takes to complete the delete operation.</span><span class="sxs-lookup"><span data-stu-id="a6609-152">You can also delete one of the heroes in the UI, and see the times it takes to complete the delete operation.</span></span> <span data-ttu-id="a6609-153">Try this out by clicking the "Delete" button for the hero named "Fred".</span><span class="sxs-lookup"><span data-stu-id="a6609-153">Try this out by clicking the "Delete" button for the hero named "Fred".</span></span>

    ![Heroes app and the Networking tab showing the time to complete the functions](./media/tutorial-develop-mongodb-nodejs-part6/times.png) 

    <span data-ttu-id="a6609-155">If you refresh the page, the Network tab shows the time it takes to get the heroes.</span><span class="sxs-lookup"><span data-stu-id="a6609-155">If you refresh the page, the Network tab shows the time it takes to get the heroes.</span></span> <span data-ttu-id="a6609-156">While these times are fast, a lot depends on where your data is located in the world and your ability to geo-replicate it in an area close to your users.</span><span class="sxs-lookup"><span data-stu-id="a6609-156">While these times are fast, a lot depends on where your data is located in the world and your ability to geo-replicate it in an area close to your users.</span></span> <span data-ttu-id="a6609-157">You can find out more about geo-replication in the next, soon to be released, tutorial.</span><span class="sxs-lookup"><span data-stu-id="a6609-157">You can find out more about geo-replication in the next, soon to be released, tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6609-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6609-158">Next steps</span></span>

<span data-ttu-id="a6609-159">In this part of the tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="a6609-159">In this part of the tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a6609-160">Added Post, Put, and Delete functions to the app</span><span class="sxs-lookup"><span data-stu-id="a6609-160">Added Post, Put, and Delete functions to the app</span></span> 

<span data-ttu-id="a6609-161">Check back soon for additional videos in this tutorial series.</span><span class="sxs-lookup"><span data-stu-id="a6609-161">Check back soon for additional videos in this tutorial series.</span></span>

