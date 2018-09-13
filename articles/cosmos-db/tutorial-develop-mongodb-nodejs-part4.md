---
title: MongoDB, Angular, and Node tutorial for Azure - Part 4 | Microsoft Docs
description: Part 4 of the tutorial series on creating a MongoDB app with Angular and Node on Azure Cosmos DB using the exact same APIs you use for MongoDB
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
ms.openlocfilehash: 583400dba7077ebab3ce80d6a03b26f13a659b35
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855598"
---
# <a name="create-a-mongodb-app-with-angular-and-azure-cosmos-db---part-4-create-an-azure-cosmos-db-account-using-the-azure-cli"></a><span data-ttu-id="a8c24-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 4: Create an Azure Cosmos DB account using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8c24-103">Create a MongoDB app with Angular and Azure Cosmos DB - Part 4: Create an Azure Cosmos DB account using the Azure CLI</span></span>

<span data-ttu-id="a8c24-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express, Angular, and your Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="a8c24-104">This multi-part tutorial demonstrates how to create a new [MongoDB API](mongodb-introduction.md) app written in Node.js with Express, Angular, and your Azure Cosmos DB database.</span></span>

<span data-ttu-id="a8c24-105">Part 4 of the tutorial builds on [Part 3](tutorial-develop-mongodb-nodejs-part3.md) and covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="a8c24-105">Part 4 of the tutorial builds on [Part 3](tutorial-develop-mongodb-nodejs-part3.md) and covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8c24-106">Create an Azure resource group using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8c24-106">Create an Azure resource group using the Azure CLI</span></span>
> * <span data-ttu-id="a8c24-107">Create an Azure Cosmos DB account using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8c24-107">Create an Azure Cosmos DB account using the Azure CLI</span></span>

## <a name="video-walkthrough"></a><span data-ttu-id="a8c24-108">Video walkthrough</span><span class="sxs-lookup"><span data-stu-id="a8c24-108">Video walkthrough</span></span>

> [!VIDEO https://www.youtube.com/embed/hfUM-AbOh94]

## <a name="prerequisites"></a><span data-ttu-id="a8c24-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8c24-109">Prerequisites</span></span>

<span data-ttu-id="a8c24-110">Before starting this part of the tutorial, ensure you've completed the steps in [Part 3](tutorial-develop-mongodb-nodejs-part3.md) of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a8c24-110">Before starting this part of the tutorial, ensure you've completed the steps in [Part 3](tutorial-develop-mongodb-nodejs-part3.md) of the tutorial.</span></span> 

<span data-ttu-id="a8c24-111">In this tutorial section, you can either use the Azure Cloud Shell (in your internet browser) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) installed locally.</span><span class="sxs-lookup"><span data-stu-id="a8c24-111">In this tutorial section, you can either use the Azure Cloud Shell (in your internet browser) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) installed locally.</span></span> <span data-ttu-id="a8c24-112">If you use the Azure CLI locally, ensure you running Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="a8c24-112">If you use the Azure CLI locally, ensure you running Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a8c24-113">Run `az --version` at the command prompt to check your version.</span><span class="sxs-lookup"><span data-stu-id="a8c24-113">Run `az --version` at the command prompt to check your version.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

> [!TIP]
> <span data-ttu-id="a8c24-114">This tutorial walks you through the steps to build the application step-by-step.</span><span class="sxs-lookup"><span data-stu-id="a8c24-114">This tutorial walks you through the steps to build the application step-by-step.</span></span> <span data-ttu-id="a8c24-115">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8c24-115">If you want to download the finished project, you can get the completed application from the [angular-cosmosdb repo](https://github.com/Azure-Samples/angular-cosmosdb) on GitHub.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="a8c24-116">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="a8c24-116">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="a8c24-117">Create an Azure Cosmos DB account with the [`az cosmosdb create`](/cli/azure/cosmosdb#az-cosmosdb-create) command.</span><span class="sxs-lookup"><span data-stu-id="a8c24-117">Create an Azure Cosmos DB account with the [`az cosmosdb create`](/cli/azure/cosmosdb#az-cosmosdb-create) command.</span></span>

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

* <span data-ttu-id="a8c24-118">For `<cosmosdb-name>` use your own unique Azure Cosmos DB account name, the name needs to be unique across all Azure Cosmos DB account names in Azure.</span><span class="sxs-lookup"><span data-stu-id="a8c24-118">For `<cosmosdb-name>` use your own unique Azure Cosmos DB account name, the name needs to be unique across all Azure Cosmos DB account names in Azure.</span></span>
* <span data-ttu-id="a8c24-119">The `--kind MongoDB` setting enables the Azure Cosmos DB to have MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="a8c24-119">The `--kind MongoDB` setting enables the Azure Cosmos DB to have MongoDB client connections.</span></span>

<span data-ttu-id="a8c24-120">It may take a minute or two for the command to complete.</span><span class="sxs-lookup"><span data-stu-id="a8c24-120">It may take a minute or two for the command to complete.</span></span> <span data-ttu-id="a8c24-121">When it's done, the terminal window displays information about the new database.</span><span class="sxs-lookup"><span data-stu-id="a8c24-121">When it's done, the terminal window displays information about the new database.</span></span> 

<span data-ttu-id="a8c24-122">Once the Azure Cosmos DB account has been created:</span><span class="sxs-lookup"><span data-stu-id="a8c24-122">Once the Azure Cosmos DB account has been created:</span></span>
1. <span data-ttu-id="a8c24-123">Open a new browser window and go to [https://portal.azure.com](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a8c24-123">Open a new browser window and go to [https://portal.azure.com](https://portal.azure.com)</span></span>
1. <span data-ttu-id="a8c24-124">Click the Azure Cosmos DB logo</span><span class="sxs-lookup"><span data-stu-id="a8c24-124">Click the Azure Cosmos DB logo</span></span> ![Azure Cosmos DB icon in the Azure portal](./media/tutorial-develop-mongodb-nodejs-part4/azure-cosmos-db-icon.png) <span data-ttu-id="a8c24-126">on the left bar, and it shows you all the Azure Cosmos DBs you have.</span><span class="sxs-lookup"><span data-stu-id="a8c24-126">on the left bar, and it shows you all the Azure Cosmos DBs you have.</span></span>
1. <span data-ttu-id="a8c24-127">Click on the Azure Cosmos DB account you just created, select the **Overview** tab and scroll down to view the map where the database is located.</span><span class="sxs-lookup"><span data-stu-id="a8c24-127">Click on the Azure Cosmos DB account you just created, select the **Overview** tab and scroll down to view the map where the database is located.</span></span> 

    ![New Azure Cosmos DB account in the Azure portal](./media/tutorial-develop-mongodb-nodejs-part4/azure-cosmos-db-angular-portal.png)

4. <span data-ttu-id="a8c24-129">Scroll down on the left navigation and click the **Replicate data globally** tab, this displays a map where you can see the different areas you can replicate into.</span><span class="sxs-lookup"><span data-stu-id="a8c24-129">Scroll down on the left navigation and click the **Replicate data globally** tab, this displays a map where you can see the different areas you can replicate into.</span></span> <span data-ttu-id="a8c24-130">For example, you can click Australia Southeast or Australia East and replicate your data to Australia.</span><span class="sxs-lookup"><span data-stu-id="a8c24-130">For example, you can click Australia Southeast or Australia East and replicate your data to Australia.</span></span> <span data-ttu-id="a8c24-131">You can learn more about global replication in [How to distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="a8c24-131">You can learn more about global replication in [How to distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span> <span data-ttu-id="a8c24-132">For now, let's just keep the once instance and when we want to replicate, we know how.</span><span class="sxs-lookup"><span data-stu-id="a8c24-132">For now, let's just keep the once instance and when we want to replicate, we know how.</span></span>

    ![New Azure Cosmos DB account in the Azure portal](./media/tutorial-develop-mongodb-nodejs-part4/azure-cosmos-db-replicate-portal.png)

## <a name="next-steps"></a><span data-ttu-id="a8c24-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8c24-134">Next steps</span></span>

<span data-ttu-id="a8c24-135">In this part of the tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="a8c24-135">In this part of the tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8c24-136">Created an Azure resource group using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8c24-136">Created an Azure resource group using the Azure CLI</span></span>
> * <span data-ttu-id="a8c24-137">Created an Azure Cosmos DB account using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8c24-137">Created an Azure Cosmos DB account using the Azure CLI</span></span>

<span data-ttu-id="a8c24-138">You can proceed to the next part of the tutorial to connect Azure Cosmos DB to your app using Mongoose.</span><span class="sxs-lookup"><span data-stu-id="a8c24-138">You can proceed to the next part of the tutorial to connect Azure Cosmos DB to your app using Mongoose.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8c24-139">Use Mongoose to connect to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a8c24-139">Use Mongoose to connect to Azure Cosmos DB</span></span>](tutorial-develop-mongodb-nodejs-part5.md)