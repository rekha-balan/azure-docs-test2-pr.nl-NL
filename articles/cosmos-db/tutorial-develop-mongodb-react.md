---
title: MongoDB, React, and Node.js tutorial for Azure | Microsoft Docs
description: Learn how to create a MongoDB app with React and Node.js on Azure Cosmos DB using the exact same APIs you use for MongoDB with this video based tutorial series.
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
ms.openlocfilehash: 28651f0b9a2c775292b5c9406f676b45fc4e5d14
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868534"
---
# <a name="create-a-mongodb-app-with-react-and-azure-cosmos-db"></a><span data-ttu-id="1beb8-103">Create a MongoDB app with React and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-103">Create a MongoDB app with React and Azure Cosmos DB</span></span>  

<span data-ttu-id="1beb8-104">This multi-part video tutorial demonstrates how to create a hero tracking app with a React front-end.</span><span class="sxs-lookup"><span data-stu-id="1beb8-104">This multi-part video tutorial demonstrates how to create a hero tracking app with a React front-end.</span></span> <span data-ttu-id="1beb8-105">The app used Node and Express for the server, connects to Azure Cosmos DB with the [MongoDB API](mongodb-introduction.md), and then connects the React front-end to the server portion of the app.</span><span class="sxs-lookup"><span data-stu-id="1beb8-105">The app used Node and Express for the server, connects to Azure Cosmos DB with the [MongoDB API](mongodb-introduction.md), and then connects the React front-end to the server portion of the app.</span></span> <span data-ttu-id="1beb8-106">The tutorial also demonstrates how to do point-and-click scaling of Azure Cosmos DB in the Azure portal and how to deploy the app to the internet so everyone can track their favorite heroes.</span><span class="sxs-lookup"><span data-stu-id="1beb8-106">The tutorial also demonstrates how to do point-and-click scaling of Azure Cosmos DB in the Azure portal and how to deploy the app to the internet so everyone can track their favorite heroes.</span></span> 

<span data-ttu-id="1beb8-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) supports MongoDB client connections, so you can use Azure Cosmos DB in place of MongoDB, but use the same code that you use for MongoDB apps; but with added benefits such as simple cloud deployment, scaling, and super-fast reads and writes.</span><span class="sxs-lookup"><span data-stu-id="1beb8-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) supports MongoDB client connections, so you can use Azure Cosmos DB in place of MongoDB, but use the same code that you use for MongoDB apps; but with added benefits such as simple cloud deployment, scaling, and super-fast reads and writes.</span></span>  

<span data-ttu-id="1beb8-108">This multi-part tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="1beb8-108">This multi-part tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1beb8-109">Introduction</span><span class="sxs-lookup"><span data-stu-id="1beb8-109">Introduction</span></span>
> * <span data-ttu-id="1beb8-110">Setup the project</span><span class="sxs-lookup"><span data-stu-id="1beb8-110">Setup the project</span></span>
> * <span data-ttu-id="1beb8-111">Build the UI with React</span><span class="sxs-lookup"><span data-stu-id="1beb8-111">Build the UI with React</span></span>
> * <span data-ttu-id="1beb8-112">Create an Azure Cosmos DB account using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1beb8-112">Create an Azure Cosmos DB account using the Azure portal</span></span>
> * <span data-ttu-id="1beb8-113">Use Mongoose to connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-113">Use Mongoose to connect to Azure Cosmos DB</span></span>
> * <span data-ttu-id="1beb8-114">Add React, Create, Update, and Delete operations to the app</span><span class="sxs-lookup"><span data-stu-id="1beb8-114">Add React, Create, Update, and Delete operations to the app</span></span>

<span data-ttu-id="1beb8-115">Want to do build this same app with Angular?</span><span class="sxs-lookup"><span data-stu-id="1beb8-115">Want to do build this same app with Angular?</span></span> <span data-ttu-id="1beb8-116">See the [Angular tutorial video series](tutorial-develop-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1beb8-116">See the [Angular tutorial video series](tutorial-develop-mongodb-nodejs.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1beb8-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1beb8-117">Prerequisites</span></span>
* [<span data-ttu-id="1beb8-118">Node.js</span><span class="sxs-lookup"><span data-stu-id="1beb8-118">Node.js</span></span>](https://www.nodejs.org)

### <a name="finished-project"></a><span data-ttu-id="1beb8-119">Finished Project</span><span class="sxs-lookup"><span data-stu-id="1beb8-119">Finished Project</span></span>
<span data-ttu-id="1beb8-120">Get the completed application [from GitHub](https://github.com/Azure-Samples/react-cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="1beb8-120">Get the completed application [from GitHub](https://github.com/Azure-Samples/react-cosmosdb).</span></span>

## <a name="introduction"></a><span data-ttu-id="1beb8-121">Introduction</span><span class="sxs-lookup"><span data-stu-id="1beb8-121">Introduction</span></span> 

<span data-ttu-id="1beb8-122">In this video, Burke Holland gives an introduction to Azure Cosmos DB and walks you through the app that is created in this video series.</span><span class="sxs-lookup"><span data-stu-id="1beb8-122">In this video, Burke Holland gives an introduction to Azure Cosmos DB and walks you through the app that is created in this video series.</span></span> 

> [!VIDEO https://www.youtube.com/embed/58IflnJbYJc]

## <a name="project-setup"></a><span data-ttu-id="1beb8-123">Project setup</span><span class="sxs-lookup"><span data-stu-id="1beb8-123">Project setup</span></span>

<span data-ttu-id="1beb8-124">This video shows how set up the Express and React in the same project.</span><span class="sxs-lookup"><span data-stu-id="1beb8-124">This video shows how set up the Express and React in the same project.</span></span> <span data-ttu-id="1beb8-125">Burke then provides a walkthrough of the code in the project.</span><span class="sxs-lookup"><span data-stu-id="1beb8-125">Burke then provides a walkthrough of the code in the project.</span></span>

> [!VIDEO https://www.youtube.com/embed/ytFUPStJJds]

## <a name="build-the-ui"></a><span data-ttu-id="1beb8-126">Build the UI</span><span class="sxs-lookup"><span data-stu-id="1beb8-126">Build the UI</span></span>

<span data-ttu-id="1beb8-127">This video shows how to create the application's user interface (UI) with React.</span><span class="sxs-lookup"><span data-stu-id="1beb8-127">This video shows how to create the application's user interface (UI) with React.</span></span> 

> [!NOTE]
> <span data-ttu-id="1beb8-128">The CSS referenced in this video can be found in the [react-cosmosdb GitHub repo](https://github.com/Azure-Samples/react-cosmosdb/blob/master/src/index.css).</span><span class="sxs-lookup"><span data-stu-id="1beb8-128">The CSS referenced in this video can be found in the [react-cosmosdb GitHub repo](https://github.com/Azure-Samples/react-cosmosdb/blob/master/src/index.css).</span></span>

> [!VIDEO https://www.youtube.com/embed/SzHzX0fTUUQ]

## <a name="connect-to-azure-cosmos-db"></a><span data-ttu-id="1beb8-129">Connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-129">Connect to Azure Cosmos DB</span></span>

<span data-ttu-id="1beb8-130">This video shows how to create an Azure Cosmos DB account in the Azure portal, install the MongoDB and Mongoose packages, and then connect the app to the newly created account using the Azure Cosmos DB connection string.</span><span class="sxs-lookup"><span data-stu-id="1beb8-130">This video shows how to create an Azure Cosmos DB account in the Azure portal, install the MongoDB and Mongoose packages, and then connect the app to the newly created account using the Azure Cosmos DB connection string.</span></span> 

> [!VIDEO https://www.youtube.com/embed/0U2jV1thfvs]

## <a name="read-and-create-heroes-in-the-app"></a><span data-ttu-id="1beb8-131">Read and create heroes in the app</span><span class="sxs-lookup"><span data-stu-id="1beb8-131">Read and create heroes in the app</span></span>

<span data-ttu-id="1beb8-132">This video shows how to read heroes and create heroes in the Cosmos DB database, as well as how to test those methods using Postman and the React UI.</span><span class="sxs-lookup"><span data-stu-id="1beb8-132">This video shows how to read heroes and create heroes in the Cosmos DB database, as well as how to test those methods using Postman and the React UI.</span></span> 

> [!VIDEO https://www.youtube.com/embed/AQK9n_8fsQI] 

## <a name="delete-and-update-heroes-in-the-app"></a><span data-ttu-id="1beb8-133">Delete and update heroes in the app</span><span class="sxs-lookup"><span data-stu-id="1beb8-133">Delete and update heroes in the app</span></span>

<span data-ttu-id="1beb8-134">This video shows how to delete and update heroes from the app and display the updates in the UI.</span><span class="sxs-lookup"><span data-stu-id="1beb8-134">This video shows how to delete and update heroes from the app and display the updates in the UI.</span></span> 

> [!VIDEO https://www.youtube.com/embed/YmaGT7ztTQM] 

## <a name="complete-the-app"></a><span data-ttu-id="1beb8-135">Complete the app</span><span class="sxs-lookup"><span data-stu-id="1beb8-135">Complete the app</span></span>

<span data-ttu-id="1beb8-136">This video shows how to complete the app and finish hooking the UI up to the backend API.</span><span class="sxs-lookup"><span data-stu-id="1beb8-136">This video shows how to complete the app and finish hooking the UI up to the backend API.</span></span> 

> [!VIDEO https://www.youtube.com/embed/TcSm2ISfTu8]

## <a name="clean-up-resources"></a><span data-ttu-id="1beb8-137">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1beb8-137">Clean up resources</span></span>

<span data-ttu-id="1beb8-138">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1beb8-138">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span> 

1. <span data-ttu-id="1beb8-139">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span><span class="sxs-lookup"><span data-stu-id="1beb8-139">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1beb8-140">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-140">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1beb8-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="1beb8-141">Next steps</span></span>

<span data-ttu-id="1beb8-142">In this tutorial, you've learned how to:</span><span class="sxs-lookup"><span data-stu-id="1beb8-142">In this tutorial, you've learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1beb8-143">Create an app with React, Node, Express, and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-143">Create an app with React, Node, Express, and Azure Cosmos DB</span></span> 
> * <span data-ttu-id="1beb8-144">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="1beb8-144">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="1beb8-145">Connect the app to the Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="1beb8-145">Connect the app to the Azure Cosmos DB account</span></span>
> * <span data-ttu-id="1beb8-146">Test the app using Postman</span><span class="sxs-lookup"><span data-stu-id="1beb8-146">Test the app using Postman</span></span>
> * <span data-ttu-id="1beb8-147">Run the application and add heroes to the database</span><span class="sxs-lookup"><span data-stu-id="1beb8-147">Run the application and add heroes to the database</span></span>

<span data-ttu-id="1beb8-148">Check back for an additional video in this tutorial series that will cover deploying the application and globally replicating your data.</span><span class="sxs-lookup"><span data-stu-id="1beb8-148">Check back for an additional video in this tutorial series that will cover deploying the application and globally replicating your data.</span></span>

<span data-ttu-id="1beb8-149">You can proceed to the next tutorial and learn how to import MongoDB data into Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-149">You can proceed to the next tutorial and learn how to import MongoDB data into Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="1beb8-150">Import MongoDB data into Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-150">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
 
