---
title: MongoDB, Angular, and Node tutorial for Azure | Microsoft Docs
description: Learn how to create a MongoDB app with Angular and Node on Azure Cosmos DB using the exact same APIs you use for MongoDB with this video based tutorial series.
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
ms.openlocfilehash: 1a9d608e7f959b3fc164f87d408ccd268e8d2568
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968325"
---
# <a name="create-a-mongodb-app-with-angular-and-azure-cosmos-db"></a><span data-ttu-id="d2dc3-103">Create a MongoDB app with Angular and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d2dc3-103">Create a MongoDB app with Angular and Azure Cosmos DB</span></span> 

<span data-ttu-id="d2dc3-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app with Express, Angular, and Node.js (the MEAN stack), and connect it to your Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app with Express, Angular, and Node.js (the MEAN stack), and connect it to your Azure Cosmos DB database.</span></span> <span data-ttu-id="d2dc3-105">Azure Cosmos DB supports MongoDB client connections, so you can use Azure Cosmos DB in place of MongoDB, but use the same code that you use for MongoDB apps but with added benefits.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-105">Azure Cosmos DB supports MongoDB client connections, so you can use Azure Cosmos DB in place of MongoDB, but use the same code that you use for MongoDB apps but with added benefits.</span></span> <span data-ttu-id="d2dc3-106">These benefits from Azure Cosmos DB are easy cloud deployment, scaling, security, global replicated data, multi-model support, and super-fast reads and writes.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-106">These benefits from Azure Cosmos DB are easy cloud deployment, scaling, security, global replicated data, multi-model support, and super-fast reads and writes.</span></span> 

<span data-ttu-id="d2dc3-107">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-107">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d2dc3-108">It enables you to quickly create and query document, key/value, and graph databases that benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-108">It enables you to quickly create and query document, key/value, and graph databases that benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d2dc3-109">This multi-part tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d2dc3-109">This multi-part tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * [<span data-ttu-id="d2dc3-110">Create a Node.js Express app with the Angular CLI</span><span class="sxs-lookup"><span data-stu-id="d2dc3-110">Create a Node.js Express app with the Angular CLI</span></span>](tutorial-develop-mongodb-nodejs-part2.md)
> * [<span data-ttu-id="d2dc3-111">Build the UI with Angular</span><span class="sxs-lookup"><span data-stu-id="d2dc3-111">Build the UI with Angular</span></span>](tutorial-develop-mongodb-nodejs-part3.md)
> * [<span data-ttu-id="d2dc3-112">Create an Azure Cosmos DB account using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d2dc3-112">Create an Azure Cosmos DB account using the Azure CLI</span></span>](tutorial-develop-mongodb-nodejs-part4.md) 
> * [<span data-ttu-id="d2dc3-113">Use Mongoose to connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d2dc3-113">Use Mongoose to connect to Azure Cosmos DB</span></span>](tutorial-develop-mongodb-nodejs-part5.md)
> * [<span data-ttu-id="d2dc3-114">Add Post, Put, and Delete functions to the app</span><span class="sxs-lookup"><span data-stu-id="d2dc3-114">Add Post, Put, and Delete functions to the app</span></span>](tutorial-develop-mongodb-nodejs-part6.md)

<span data-ttu-id="d2dc3-115">Want to do build this same app with React?</span><span class="sxs-lookup"><span data-stu-id="d2dc3-115">Want to do build this same app with React?</span></span> <span data-ttu-id="d2dc3-116">See the [React tutorial video series](tutorial-develop-mongodb-react.md).</span><span class="sxs-lookup"><span data-stu-id="d2dc3-116">See the [React tutorial video series](tutorial-develop-mongodb-react.md).</span></span>

## <a name="video-walkthrough"></a><span data-ttu-id="d2dc3-117">Video walkthrough</span><span class="sxs-lookup"><span data-stu-id="d2dc3-117">Video walkthrough</span></span>

> [!VIDEO https://www.youtube.com/embed/vlZRP0mDabM]

## <a name="finished-project"></a><span data-ttu-id="d2dc3-118">Finished project</span><span class="sxs-lookup"><span data-stu-id="d2dc3-118">Finished project</span></span> 

<span data-ttu-id="d2dc3-119">This tutorial walks you through the steps to build the application step-by-step.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-119">This tutorial walks you through the steps to build the application step-by-step.</span></span> <span data-ttu-id="d2dc3-120">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-120">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2dc3-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2dc3-121">Next steps</span></span>

<span data-ttu-id="d2dc3-122">In this part of the tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="d2dc3-122">In this part of the tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2dc3-123">Seen an overview of the steps to create a MEAN.js app with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-123">Seen an overview of the steps to create a MEAN.js app with Azure Cosmos DB.</span></span> 

<span data-ttu-id="d2dc3-124">You can proceed to the next part of the tutorial to create the Node.js Express app.</span><span class="sxs-lookup"><span data-stu-id="d2dc3-124">You can proceed to the next part of the tutorial to create the Node.js Express app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2dc3-125">Create a Node.js Express app with the Angular CLI</span><span class="sxs-lookup"><span data-stu-id="d2dc3-125">Create a Node.js Express app with the Angular CLI</span></span>](tutorial-develop-mongodb-nodejs-part2.md)
