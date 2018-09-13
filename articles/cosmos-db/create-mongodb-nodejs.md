---
title: Connect a MongoDB app to Azure Cosmos DB by using Node.js | Microsoft Docs
description: Learn how to connect an existing Node.js MongoDB app to Azure Cosmos DB
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: quick start connect, mvc, devcenter
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/19/2017
ms.author: sngun
ms.openlocfilehash: 9fcc03721d410d4d7b8cfed0f8fa5b0ae8cf80ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869145"
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="39e30-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span><span class="sxs-lookup"><span data-stu-id="39e30-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

> [!div class="op_single_selector"]
> * [.NET](create-mongodb-dotnet.md)
> * [Java](create-mongodb-java.md)
> * [Node.js](create-mongodb-nodejs.md)
> * [Python](create-mongodb-flask.md)
> * [Xamarin](create-mongodb-xamarin.md)
> * [Golang](create-mongodb-golang.md)
>  

<span data-ttu-id="39e30-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="39e30-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="39e30-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39e30-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="39e30-112">This quickstart demonstrates how to use an existing MongoDB app written in Node.js and connect it to your Azure Cosmos DB database, which supports MongoDB client connections by using the [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39e30-112">This quickstart demonstrates how to use an existing MongoDB app written in Node.js and connect it to your Azure Cosmos DB database, which supports MongoDB client connections by using the [MongoDB API](mongodb-introduction.md).</span></span> <span data-ttu-id="39e30-113">In other words, your Node.js application only knows that it's connecting to a database using MongoDB APIs.</span><span class="sxs-lookup"><span data-stu-id="39e30-113">In other words, your Node.js application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="39e30-114">It is transparent to the application that the data is stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39e30-114">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="39e30-115">When you are done, you will have a MEAN application (MongoDB, Express, Angular, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="39e30-115">When you are done, you will have a MEAN application (MongoDB, Express, Angular, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![MEAN.js app running in Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="39e30-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="39e30-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="39e30-118">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="39e30-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="39e30-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="39e30-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="39e30-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39e30-120">Prerequisites</span></span> 
<span data-ttu-id="39e30-121">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="39e30-121">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 
[!INCLUDE [cosmos-db-emulator-mongodb](../../includes/cosmos-db-emulator-mongodb.md)]

<span data-ttu-id="39e30-122">In addition to Azure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally to run `npm` and `git` commands.</span><span class="sxs-lookup"><span data-stu-id="39e30-122">In addition to Azure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally to run `npm` and `git` commands.</span></span>

<span data-ttu-id="39e30-123">You should have working knowledge of Node.js.</span><span class="sxs-lookup"><span data-stu-id="39e30-123">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="39e30-124">This quickstart is not intended to help you with developing Node.js applications in general.</span><span class="sxs-lookup"><span data-stu-id="39e30-124">This quickstart is not intended to help you with developing Node.js applications in general.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="39e30-125">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="39e30-125">Clone the sample application</span></span>

<span data-ttu-id="39e30-126">Run the following commands to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="39e30-126">Run the following commands to clone the sample repository.</span></span> <span data-ttu-id="39e30-127">This sample repository contains the default [MEAN.js](http://meanjs.org/) application.</span><span class="sxs-lookup"><span data-stu-id="39e30-127">This sample repository contains the default [MEAN.js](http://meanjs.org/) application.</span></span>

1. <span data-ttu-id="39e30-128">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="39e30-128">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="39e30-129">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="39e30-129">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="39e30-130">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="39e30-130">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="39e30-131">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="39e30-131">This command creates a copy of the sample app on your computer.</span></span> 

    ```bash
    git clone https://github.com/prashanthmadi/mean
    ```

## <a name="run-the-application"></a><span data-ttu-id="39e30-132">Run the application</span><span class="sxs-lookup"><span data-stu-id="39e30-132">Run the application</span></span>

<span data-ttu-id="39e30-133">Install the required packages and start the application.</span><span class="sxs-lookup"><span data-stu-id="39e30-133">Install the required packages and start the application.</span></span>

```bash
cd mean
npm install
npm start
```
<span data-ttu-id="39e30-134">The application will try to connect to a MongoDB source and fail, go ahead and exit the application when the output returns "[MongoError: connect ECONNREFUSED 127.0.0.1:27017]".</span><span class="sxs-lookup"><span data-stu-id="39e30-134">The application will try to connect to a MongoDB source and fail, go ahead and exit the application when the output returns "[MongoError: connect ECONNREFUSED 127.0.0.1:27017]".</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="39e30-135">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="39e30-135">Log in to Azure</span></span>

<span data-ttu-id="39e30-136">If you are using an installed Azure CLI, log in to your Azure subscription with the [az login](/cli/azure/reference-index#az-login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="39e30-136">If you are using an installed Azure CLI, log in to your Azure subscription with the [az login](/cli/azure/reference-index#az-login) command and follow the on-screen directions.</span></span> <span data-ttu-id="39e30-137">You can skip this step if you're using the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="39e30-137">You can skip this step if you're using the Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-the-azure-cosmos-db-module"></a><span data-ttu-id="39e30-138">Add the Azure Cosmos DB module</span><span class="sxs-lookup"><span data-stu-id="39e30-138">Add the Azure Cosmos DB module</span></span>

<span data-ttu-id="39e30-139">If you are using an installed Azure CLI, check to see if the `cosmosdb` component is already installed by running the `az` command.</span><span class="sxs-lookup"><span data-stu-id="39e30-139">If you are using an installed Azure CLI, check to see if the `cosmosdb` component is already installed by running the `az` command.</span></span> <span data-ttu-id="39e30-140">If `cosmosdb` is in the list of base commands, proceed to the next command.</span><span class="sxs-lookup"><span data-stu-id="39e30-140">If `cosmosdb` is in the list of base commands, proceed to the next command.</span></span> <span data-ttu-id="39e30-141">You can skip this step if you're using the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="39e30-141">You can skip this step if you're using the Azure Cloud Shell.</span></span>

<span data-ttu-id="39e30-142">If `cosmosdb` is not in the list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="39e30-142">If `cosmosdb` is not in the list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="39e30-143">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="39e30-143">Create a resource group</span></span>

<span data-ttu-id="39e30-144">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="39e30-144">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#az-group-create).</span></span> <span data-ttu-id="39e30-145">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="39e30-145">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="39e30-146">The following example creates a resource group in the West Europe region.</span><span class="sxs-lookup"><span data-stu-id="39e30-146">The following example creates a resource group in the West Europe region.</span></span> <span data-ttu-id="39e30-147">Choose a unique name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="39e30-147">Choose a unique name for the resource group.</span></span>

<span data-ttu-id="39e30-148">If you are using Azure Cloud Shell, click **Try It**, follow the onscreen prompts to login, then copy the command into the command prompt.</span><span class="sxs-lookup"><span data-stu-id="39e30-148">If you are using Azure Cloud Shell, click **Try It**, follow the onscreen prompts to login, then copy the command into the command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="39e30-149">Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="39e30-149">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="39e30-150">Create an Azure Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#az-cosmosdb-create) command.</span><span class="sxs-lookup"><span data-stu-id="39e30-150">Create an Azure Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#az-cosmosdb-create) command.</span></span>

<span data-ttu-id="39e30-151">In the following command, please substitute your own unique Azure Cosmos DB account name where you see the `<cosmosdb-name>` placeholder.</span><span class="sxs-lookup"><span data-stu-id="39e30-151">In the following command, please substitute your own unique Azure Cosmos DB account name where you see the `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="39e30-152">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so the name needs to be unique across all Azure Cosmos DB accounts in Azure.</span><span class="sxs-lookup"><span data-stu-id="39e30-152">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so the name needs to be unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="39e30-153">The `--kind MongoDB` parameter enables MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="39e30-153">The `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="39e30-154">When the Azure Cosmos DB account is created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="39e30-154">When the Azure Cosmos DB account is created, the Azure CLI shows information similar to the following example.</span></span> 

> [!NOTE]
> This example uses JSON as the Azure CLI output format, which is the default. To use another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-to-the-database"></a><span data-ttu-id="39e30-157">Connect your Node.js application to the database</span><span class="sxs-lookup"><span data-stu-id="39e30-157">Connect your Node.js application to the database</span></span>

<span data-ttu-id="39e30-158">In this step, you connect your MEAN.js sample application to an Azure Cosmos DB database you just created, using a MongoDB connection string.</span><span class="sxs-lookup"><span data-stu-id="39e30-158">In this step, you connect your MEAN.js sample application to an Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="39e30-159">Configure the connection string in your Node.js application</span><span class="sxs-lookup"><span data-stu-id="39e30-159">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="39e30-160">In your MEAN.js repository, open `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="39e30-160">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="39e30-161">Replace the content of this file with the following code.</span><span class="sxs-lookup"><span data-stu-id="39e30-161">Replace the content of this file with the following code.</span></span> <span data-ttu-id="39e30-162">Be sure to also replace the two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span><span class="sxs-lookup"><span data-stu-id="39e30-162">Be sure to also replace the two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-the-key"></a><span data-ttu-id="39e30-163">Retrieve the key</span><span class="sxs-lookup"><span data-stu-id="39e30-163">Retrieve the key</span></span>

<span data-ttu-id="39e30-164">In order to connect to an Azure Cosmos DB database, you need the database key.</span><span class="sxs-lookup"><span data-stu-id="39e30-164">In order to connect to an Azure Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="39e30-165">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span><span class="sxs-lookup"><span data-stu-id="39e30-165">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="39e30-166">The Azure CLI outputs information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="39e30-166">The Azure CLI outputs information similar to the following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="39e30-167">Copy the value of `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="39e30-167">Copy the value of `primaryMasterKey`.</span></span> <span data-ttu-id="39e30-168">Paste this over the  `<primary_master_key>` in `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="39e30-168">Paste this over the  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="39e30-169">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="39e30-169">Save your changes.</span></span>

### <a name="run-the-application-again"></a><span data-ttu-id="39e30-170">Run the application again.</span><span class="sxs-lookup"><span data-stu-id="39e30-170">Run the application again.</span></span>

<span data-ttu-id="39e30-171">Run `npm start` again.</span><span class="sxs-lookup"><span data-stu-id="39e30-171">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="39e30-172">A console message should now tell you that the development environment is up and running.</span><span class="sxs-lookup"><span data-stu-id="39e30-172">A console message should now tell you that the development environment is up and running.</span></span> 

<span data-ttu-id="39e30-173">Navigate to `http://localhost:3000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="39e30-173">Navigate to `http://localhost:3000` in a browser.</span></span> <span data-ttu-id="39e30-174">Click **Sign Up** in the top menu and try to create two dummy users.</span><span class="sxs-lookup"><span data-stu-id="39e30-174">Click **Sign Up** in the top menu and try to create two dummy users.</span></span> 

<span data-ttu-id="39e30-175">The MEAN.js sample application stores user data in the database.</span><span class="sxs-lookup"><span data-stu-id="39e30-175">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="39e30-176">If you are successful and MEAN.js automatically signs into the created user, then your Azure Cosmos DB connection is working.</span><span class="sxs-lookup"><span data-stu-id="39e30-176">If you are successful and MEAN.js automatically signs into the created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js connects successfully to MongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="39e30-178">View data in Data Explorer</span><span class="sxs-lookup"><span data-stu-id="39e30-178">View data in Data Explorer</span></span>

<span data-ttu-id="39e30-179">Data stored by an Azure Cosmos DB is available to view, query, and run business-logic on in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39e30-179">Data stored by an Azure Cosmos DB is available to view, query, and run business-logic on in the Azure portal.</span></span>

<span data-ttu-id="39e30-180">To view, query, and work with the user data created in the previous step, login to the [Azure portal](https://portal.azure.com) in your web browser.</span><span class="sxs-lookup"><span data-stu-id="39e30-180">To view, query, and work with the user data created in the previous step, login to the [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="39e30-181">In the top Search box, type Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39e30-181">In the top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="39e30-182">When your Cosmos DB account blade opens, select your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="39e30-182">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="39e30-183">In the left navigation, click Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="39e30-183">In the left navigation, click Data Explorer.</span></span> <span data-ttu-id="39e30-184">Expand your collection in the Collections pane, and then you can view the documents in the collection, query the data, and even create and run stored procedures, triggers, and UDFs.</span><span class="sxs-lookup"><span data-stu-id="39e30-184">Expand your collection in the Collections pane, and then you can view the documents in the collection, query the data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Data Explorer in the Azure portal](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-the-nodejs-application-to-azure"></a><span data-ttu-id="39e30-186">Deploy the Node.js application to Azure</span><span class="sxs-lookup"><span data-stu-id="39e30-186">Deploy the Node.js application to Azure</span></span>

<span data-ttu-id="39e30-187">In this step, you deploy your MongoDB-connected Node.js application to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39e30-187">In this step, you deploy your MongoDB-connected Node.js application to Azure Cosmos DB.</span></span>

<span data-ttu-id="39e30-188">You may have noticed that the configuration file that you changed earlier is for the development environment (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="39e30-188">You may have noticed that the configuration file that you changed earlier is for the development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="39e30-189">When you deploy your application to App Service, it will run in the production environment by default.</span><span class="sxs-lookup"><span data-stu-id="39e30-189">When you deploy your application to App Service, it will run in the production environment by default.</span></span> <span data-ttu-id="39e30-190">So now, you need to make the same change to the respective configuration file.</span><span class="sxs-lookup"><span data-stu-id="39e30-190">So now, you need to make the same change to the respective configuration file.</span></span>

<span data-ttu-id="39e30-191">In your MEAN.js repository, open `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="39e30-191">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="39e30-192">In the `db` object, replace the value of `uri` as show in the following example.</span><span class="sxs-lookup"><span data-stu-id="39e30-192">In the `db` object, replace the value of `uri` as show in the following example.</span></span> <span data-ttu-id="39e30-193">Be sure to replace the placeholders as before.</span><span class="sxs-lookup"><span data-stu-id="39e30-193">Be sure to replace the placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> The `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements). 
>
>

<span data-ttu-id="39e30-195">In the terminal, commit all your changes into Git.</span><span class="sxs-lookup"><span data-stu-id="39e30-195">In the terminal, commit all your changes into Git.</span></span> <span data-ttu-id="39e30-196">You can copy both commands to run them together.</span><span class="sxs-lookup"><span data-stu-id="39e30-196">You can copy both commands to run them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="39e30-197">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="39e30-197">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="39e30-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="39e30-198">Next steps</span></span>

<span data-ttu-id="39e30-199">In this quickstart, you've learned how to create an Azure Cosmos DB account and create a MongoDB collection using the Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="39e30-199">In this quickstart, you've learned how to create an Azure Cosmos DB account and create a MongoDB collection using the Data Explorer.</span></span> <span data-ttu-id="39e30-200">You can now migrate your MongoDB data to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39e30-200">You can now migrate your MongoDB data to Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [Import MongoDB data into Azure Cosmos DB](mongodb-migrate.md)
