---
title: Build a Node.js and MongoDB web app in Azure | Microsoft Docs
description: Learn how to get a Node.js app working in Azure, with connection to a Cosmos DB database with a MongoDB connection string.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 70b7af1701c13e6a5d7644f04e4502f76ef7743a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856872"
---
# <a name="tutorial-build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="279e7-103">Tutorial: Build a Node.js and MongoDB web app in Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-103">Tutorial: Build a Node.js and MongoDB web app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="279e7-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="279e7-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="279e7-105">To deploy to App Service on _Linux_, see [Build a Node.js and MongoDB web app in Azure App Service on Linux](./containers/tutorial-nodejs-mongodb-app.md).</span><span class="sxs-lookup"><span data-stu-id="279e7-105">To deploy to App Service on _Linux_, see [Build a Node.js and MongoDB web app in Azure App Service on Linux](./containers/tutorial-nodejs-mongodb-app.md).</span></span>
>

<span data-ttu-id="279e7-106">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="279e7-106">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="279e7-107">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="279e7-107">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="279e7-108">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="279e7-108">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="279e7-109">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="279e7-109">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![MEAN.js app running in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="279e7-111">What you'll learn:</span><span class="sxs-lookup"><span data-stu-id="279e7-111">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="279e7-112">Create a MongoDB database in Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-112">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="279e7-113">Connect a Node.js app to MongoDB</span><span class="sxs-lookup"><span data-stu-id="279e7-113">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="279e7-114">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-114">Deploy the app to Azure</span></span>
> * <span data-ttu-id="279e7-115">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="279e7-115">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="279e7-116">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-116">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="279e7-117">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="279e7-117">Manage the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="279e7-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="279e7-118">Prerequisites</span></span>

<span data-ttu-id="279e7-119">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="279e7-119">To complete this tutorial:</span></span>

1. [<span data-ttu-id="279e7-120">Install Git</span><span class="sxs-lookup"><span data-stu-id="279e7-120">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="279e7-121">Install Node.js and NPM</span><span class="sxs-lookup"><span data-stu-id="279e7-121">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="279e7-122">[Install Bower](https://bower.io/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="279e7-122">[Install Bower](https://bower.io/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. <span data-ttu-id="279e7-123">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="279e7-123">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="279e7-124">Install and run MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="279e7-124">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

## <a name="test-local-mongodb"></a><span data-ttu-id="279e7-125">Test local MongoDB</span><span class="sxs-lookup"><span data-stu-id="279e7-125">Test local MongoDB</span></span>

<span data-ttu-id="279e7-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span><span class="sxs-lookup"><span data-stu-id="279e7-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="279e7-127">You can use this terminal window to run all the commands in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="279e7-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="279e7-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="279e7-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="279e7-129">If your connection is successful, then your MongoDB database is already running.</span><span class="sxs-lookup"><span data-stu-id="279e7-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="279e7-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="279e7-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="279e7-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span><span class="sxs-lookup"><span data-stu-id="279e7-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="279e7-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="279e7-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="279e7-133">Create local Node.js app</span><span class="sxs-lookup"><span data-stu-id="279e7-133">Create local Node.js app</span></span>

<span data-ttu-id="279e7-134">In this step, you set up the local Node.js project.</span><span class="sxs-lookup"><span data-stu-id="279e7-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="279e7-135">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="279e7-135">Clone the sample application</span></span>

<span data-ttu-id="279e7-136">In the terminal window, `cd` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="279e7-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="279e7-137">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="279e7-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="279e7-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="279e7-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="279e7-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="279e7-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="279e7-140">Run the application</span><span class="sxs-lookup"><span data-stu-id="279e7-140">Run the application</span></span>

<span data-ttu-id="279e7-141">Run the following commands to install the required packages and start the application.</span><span class="sxs-lookup"><span data-stu-id="279e7-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="279e7-142">When the app is fully loaded, you see something similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="279e7-142">When the app is fully loaded, you see something similar to the following message:</span></span>

```console
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="279e7-143">Navigate to `http://localhost:3000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="279e7-143">Navigate to `http://localhost:3000` in a browser.</span></span> <span data-ttu-id="279e7-144">Click **Sign Up** in the top menu and create a test user.</span><span class="sxs-lookup"><span data-stu-id="279e7-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="279e7-145">The MEAN.js sample application stores user data in the database.</span><span class="sxs-lookup"><span data-stu-id="279e7-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="279e7-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="279e7-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js connects successfully to MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="279e7-148">Select **Admin > Manage Articles** to add some articles.</span><span class="sxs-lookup"><span data-stu-id="279e7-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="279e7-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="279e7-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

> [!NOTE]
> <span data-ttu-id="279e7-150">The [Node.js quickstart](app-service-web-get-started-nodejs.md) mentions the need for a web.config in the root app directory.</span><span class="sxs-lookup"><span data-stu-id="279e7-150">The [Node.js quickstart](app-service-web-get-started-nodejs.md) mentions the need for a web.config in the root app directory.</span></span> <span data-ttu-id="279e7-151">However, in this tutorial, this web.config file will be automatically generated by App Service when you deploy your files using [local Git deployment](app-service-deploy-local-git.md) instead of ZIP file deployment.</span><span class="sxs-lookup"><span data-stu-id="279e7-151">However, in this tutorial, this web.config file will be automatically generated by App Service when you deploy your files using [local Git deployment](app-service-deploy-local-git.md) instead of ZIP file deployment.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-production-mongodb"></a><span data-ttu-id="279e7-152">Create production MongoDB</span><span class="sxs-lookup"><span data-stu-id="279e7-152">Create production MongoDB</span></span>

<span data-ttu-id="279e7-153">In this step, you create a MongoDB database in Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-153">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="279e7-154">When your app is deployed to Azure, it uses this cloud database.</span><span class="sxs-lookup"><span data-stu-id="279e7-154">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="279e7-155">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="279e7-155">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="279e7-156">Cosmos DB supports MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="279e7-156">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="279e7-157">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="279e7-157">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="279e7-158">Create a Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="279e7-158">Create a Cosmos DB account</span></span>

> [!NOTE]
> <span data-ttu-id="279e7-159">There is a cost to creating the Azure Cosmos DB databases in this tutorial in your own Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="279e7-159">There is a cost to creating the Azure Cosmos DB databases in this tutorial in your own Azure subscription.</span></span> <span data-ttu-id="279e7-160">To use a free Azure Cosmos DB account for seven days, you can use the [Try Azure Cosmos DB for free](https://azure.microsoft.com/en-us/try/cosmosdb/) experience.</span><span class="sxs-lookup"><span data-stu-id="279e7-160">To use a free Azure Cosmos DB account for seven days, you can use the [Try Azure Cosmos DB for free](https://azure.microsoft.com/en-us/try/cosmosdb/) experience.</span></span> <span data-ttu-id="279e7-161">Just click the **Create** button in the MongoDB tile to create a free MongoDB database on Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-161">Just click the **Create** button in the MongoDB tile to create a free MongoDB database on Azure.</span></span> <span data-ttu-id="279e7-162">Once the database is created, navigate to **Connection String** in the portal and retrieve your Azure Cosmos DB connection string for use later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="279e7-162">Once the database is created, navigate to **Connection String** in the portal and retrieve your Azure Cosmos DB connection string for use later in the tutorial.</span></span>
>

<span data-ttu-id="279e7-163">In the Cloud Shell, create a Cosmos DB account with the [`az cosmosdb create`](/cli/azure/cosmosdb?view=azure-cli-latest#az-cosmosdb-create) command.</span><span class="sxs-lookup"><span data-stu-id="279e7-163">In the Cloud Shell, create a Cosmos DB account with the [`az cosmosdb create`](/cli/azure/cosmosdb?view=azure-cli-latest#az-cosmosdb-create) command.</span></span>

<span data-ttu-id="279e7-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span><span class="sxs-lookup"><span data-stu-id="279e7-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="279e7-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="279e7-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span><span class="sxs-lookup"><span data-stu-id="279e7-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create --name <cosmosdb_name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="279e7-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="279e7-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="279e7-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="279e7-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="279e7-169">Connect app to production MongoDB</span><span class="sxs-lookup"><span data-stu-id="279e7-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="279e7-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span><span class="sxs-lookup"><span data-stu-id="279e7-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="279e7-171">Retrieve the database key</span><span class="sxs-lookup"><span data-stu-id="279e7-171">Retrieve the database key</span></span>

<span data-ttu-id="279e7-172">To connect to the Cosmos DB database, you need the database key.</span><span class="sxs-lookup"><span data-stu-id="279e7-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="279e7-173">In the Cloud Shell, use the [`az cosmosdb list-keys`](/cli/azure/cosmosdb?view=azure-cli-latest#az-cosmosdb-list-keys) command to retrieve the primary key.</span><span class="sxs-lookup"><span data-stu-id="279e7-173">In the Cloud Shell, use the [`az cosmosdb list-keys`](/cli/azure/cosmosdb?view=azure-cli-latest#az-cosmosdb-list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="279e7-174">The Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="279e7-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copy the value of `primaryMasterKey`. <span data-ttu-id="279e7-176">You need this information in the next step.</span><span class="sxs-lookup"><span data-stu-id="279e7-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="279e7-177">Configure the connection string in your Node.js application</span><span class="sxs-lookup"><span data-stu-id="279e7-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="279e7-178">In your local MEAN.js repository, in the _config/env/_ folder, create a file named _local-production.js_.</span><span class="sxs-lookup"><span data-stu-id="279e7-178">In your local MEAN.js repository, in the _config/env/_ folder, create a file named _local-production.js_.</span></span> <span data-ttu-id="279e7-179">By default, _.gitignore_ is configured to keep this file out of the repository.</span><span class="sxs-lookup"><span data-stu-id="279e7-179">By default, _.gitignore_ is configured to keep this file out of the repository.</span></span> 

<span data-ttu-id="279e7-180">Copy the following code into it.</span><span class="sxs-lookup"><span data-stu-id="279e7-180">Copy the following code into it.</span></span> <span data-ttu-id="279e7-181">Be sure to replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name, and replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span><span class="sxs-lookup"><span data-stu-id="279e7-181">Be sure to replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name, and replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

```javascript
module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false'
  }
};
```

<span data-ttu-id="279e7-182">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="279e7-182">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="279e7-183">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="279e7-183">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="279e7-184">Test the application in production mode</span><span class="sxs-lookup"><span data-stu-id="279e7-184">Test the application in production mode</span></span> 

<span data-ttu-id="279e7-185">Run the following command to minify and bundle scripts for the production environment.</span><span class="sxs-lookup"><span data-stu-id="279e7-185">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="279e7-186">This process generates the files needed by the production environment.</span><span class="sxs-lookup"><span data-stu-id="279e7-186">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="279e7-187">Run the following command to use the connection string you configured in _config/env/local-production.js_.</span><span class="sxs-lookup"><span data-stu-id="279e7-187">Run the following command to use the connection string you configured in _config/env/local-production.js_.</span></span>

```bash
# Bash
NODE_ENV=production node server.js

# Windows PowerShell
$env:NODE_ENV = "production" 
node server.js
```

<span data-ttu-id="279e7-188">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span><span class="sxs-lookup"><span data-stu-id="279e7-188">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="279e7-189">`node server.js` starts the Node.js server with `server.js` in your repository root.</span><span class="sxs-lookup"><span data-stu-id="279e7-189">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="279e7-190">This is how your Node.js application is loaded in Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-190">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="279e7-191">When the app is loaded, check to make sure that it's running in the production environment:</span><span class="sxs-lookup"><span data-stu-id="279e7-191">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```console
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="279e7-192">Navigate to `http://localhost:8443` in a browser.</span><span class="sxs-lookup"><span data-stu-id="279e7-192">Navigate to `http://localhost:8443` in a browser.</span></span> <span data-ttu-id="279e7-193">Click **Sign Up** in the top menu and create a test user.</span><span class="sxs-lookup"><span data-stu-id="279e7-193">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="279e7-194">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-194">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="279e7-195">In the terminal, stop Node.js by typing `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="279e7-195">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="279e7-196">Deploy app to Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-196">Deploy app to Azure</span></span>

<span data-ttu-id="279e7-197">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="279e7-197">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="279e7-198">Configure a deployment user</span><span class="sxs-lookup"><span data-stu-id="279e7-198">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a><span data-ttu-id="279e7-199">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="279e7-199">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

<a name="create"></a>
### <a name="create-a-web-app"></a><span data-ttu-id="279e7-200">Create a web app</span><span class="sxs-lookup"><span data-stu-id="279e7-200">Create a web app</span></span>

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app-nodejs-no-h.md)] 

### <a name="configure-an-environment-variable"></a><span data-ttu-id="279e7-201">Configure an environment variable</span><span class="sxs-lookup"><span data-stu-id="279e7-201">Configure an environment variable</span></span>

<span data-ttu-id="279e7-202">By default, the MEAN.js project keeps _config/env/local-production.js_ out of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="279e7-202">By default, the MEAN.js project keeps _config/env/local-production.js_ out of the Git repository.</span></span> <span data-ttu-id="279e7-203">So for your Azure web app, you use app settings to define your MongoDB connection string.</span><span class="sxs-lookup"><span data-stu-id="279e7-203">So for your Azure web app, you use app settings to define your MongoDB connection string.</span></span>

<span data-ttu-id="279e7-204">To set app settings, use the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="279e7-204">To set app settings, use the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span></span> 

<span data-ttu-id="279e7-205">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="279e7-205">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="279e7-206">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span><span class="sxs-lookup"><span data-stu-id="279e7-206">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="279e7-207">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span><span class="sxs-lookup"><span data-stu-id="279e7-207">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="279e7-208">In your local MEAN.js repository, open _config/env/production.js_ (not _config/env/local-production.js_), which has production-environment specific configuration.</span><span class="sxs-lookup"><span data-stu-id="279e7-208">In your local MEAN.js repository, open _config/env/production.js_ (not _config/env/local-production.js_), which has production-environment specific configuration.</span></span> <span data-ttu-id="279e7-209">The default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span><span class="sxs-lookup"><span data-stu-id="279e7-209">The default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="push-to-azure-from-git"></a><span data-ttu-id="279e7-210">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="279e7-210">Push to Azure from Git</span></span>

[!INCLUDE [app-service-plan-no-h](../../includes/app-service-web-git-push-to-azure-no-h.md)]

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="279e7-211">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span><span class="sxs-lookup"><span data-stu-id="279e7-211">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="279e7-212">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span><span class="sxs-lookup"><span data-stu-id="279e7-212">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="279e7-213">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="279e7-213">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="279e7-214">_deploy.sh_ - The custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="279e7-214">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="279e7-215">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span><span class="sxs-lookup"><span data-stu-id="279e7-215">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="279e7-216">You can use this approach to add any step to your Git-based deployment.</span><span class="sxs-lookup"><span data-stu-id="279e7-216">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="279e7-217">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span><span class="sxs-lookup"><span data-stu-id="279e7-217">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="279e7-218">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="279e7-218">Browse to the Azure web app</span></span> 

<span data-ttu-id="279e7-219">Browse to the deployed web app using your web browser.</span><span class="sxs-lookup"><span data-stu-id="279e7-219">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="279e7-220">Click **Sign Up** in the top menu and create a dummy user.</span><span class="sxs-lookup"><span data-stu-id="279e7-220">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="279e7-221">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span><span class="sxs-lookup"><span data-stu-id="279e7-221">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![MEAN.js app running in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="279e7-223">Select **Admin > Manage Articles** to add some articles.</span><span class="sxs-lookup"><span data-stu-id="279e7-223">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="279e7-224">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="279e7-224">**Congratulations!**</span></span> <span data-ttu-id="279e7-225">You're running a data-driven Node.js app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="279e7-225">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="279e7-226">Update data model and redeploy</span><span class="sxs-lookup"><span data-stu-id="279e7-226">Update data model and redeploy</span></span>

<span data-ttu-id="279e7-227">In this step, you change the `article` data model and publish your change to Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-227">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="279e7-228">Update the data model</span><span class="sxs-lookup"><span data-stu-id="279e7-228">Update the data model</span></span>

<span data-ttu-id="279e7-229">Open _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="279e7-229">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="279e7-230">In `ArticleSchema`, add a `String` type called `comment`.</span><span class="sxs-lookup"><span data-stu-id="279e7-230">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="279e7-231">When you're done, your schema code should look like this:</span><span class="sxs-lookup"><span data-stu-id="279e7-231">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-the-articles-code"></a><span data-ttu-id="279e7-232">Update the articles code</span><span class="sxs-lookup"><span data-stu-id="279e7-232">Update the articles code</span></span>

<span data-ttu-id="279e7-233">Update the rest of your `articles` code to use `comment`.</span><span class="sxs-lookup"><span data-stu-id="279e7-233">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="279e7-234">There are five files you need to modify: the server controller and the four client views.</span><span class="sxs-lookup"><span data-stu-id="279e7-234">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="279e7-235">Open _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="279e7-235">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="279e7-236">In the `update` function, add an assignment for `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="279e7-236">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="279e7-237">The following code shows the completed `update` function:</span><span class="sxs-lookup"><span data-stu-id="279e7-237">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="279e7-238">Open _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="279e7-238">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="279e7-239">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span><span class="sxs-lookup"><span data-stu-id="279e7-239">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="279e7-240">Open _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="279e7-240">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="279e7-241">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span><span class="sxs-lookup"><span data-stu-id="279e7-241">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="279e7-242">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="279e7-242">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="279e7-243">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span><span class="sxs-lookup"><span data-stu-id="279e7-243">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="279e7-244">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="279e7-244">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="279e7-245">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span><span class="sxs-lookup"><span data-stu-id="279e7-245">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="279e7-246">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span><span class="sxs-lookup"><span data-stu-id="279e7-246">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="279e7-247">Your new element should look like this:</span><span class="sxs-lookup"><span data-stu-id="279e7-247">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="279e7-248">Test your changes locally</span><span class="sxs-lookup"><span data-stu-id="279e7-248">Test your changes locally</span></span>

<span data-ttu-id="279e7-249">Save all your changes.</span><span class="sxs-lookup"><span data-stu-id="279e7-249">Save all your changes.</span></span>

<span data-ttu-id="279e7-250">In the local terminal window, test your changes in production mode again.</span><span class="sxs-lookup"><span data-stu-id="279e7-250">In the local terminal window, test your changes in production mode again.</span></span>

```bash
# Bash
gulp prod
NODE_ENV=production node server.js

# Windows PowerShell
gulp prod
$env:NODE_ENV = "production" 
node server.js
```

<span data-ttu-id="279e7-251">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span><span class="sxs-lookup"><span data-stu-id="279e7-251">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="279e7-252">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span><span class="sxs-lookup"><span data-stu-id="279e7-252">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="279e7-253">You see the new `Comment` textbox now.</span><span class="sxs-lookup"><span data-stu-id="279e7-253">You see the new `Comment` textbox now.</span></span>

![Added comment field to Articles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="279e7-255">In the terminal, stop Node.js by typing `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="279e7-255">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="279e7-256">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-256">Publish changes to Azure</span></span>

<span data-ttu-id="279e7-257">In the local terminal window, commit your changes in Git, then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="279e7-257">In the local terminal window, commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="279e7-258">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span><span class="sxs-lookup"><span data-stu-id="279e7-258">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Model and database changes published to Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="279e7-260">If you added any articles earlier, you still can see them.</span><span class="sxs-lookup"><span data-stu-id="279e7-260">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="279e7-261">Existing data in your Cosmos DB is not lost.</span><span class="sxs-lookup"><span data-stu-id="279e7-261">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="279e7-262">Also, your updates to the data schema and leaves your existing data intact.</span><span class="sxs-lookup"><span data-stu-id="279e7-262">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="279e7-263">Stream diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="279e7-263">Stream diagnostic logs</span></span> 

<span data-ttu-id="279e7-264">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span><span class="sxs-lookup"><span data-stu-id="279e7-264">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="279e7-265">That way, you can get the same diagnostic messages to help you debug application errors.</span><span class="sxs-lookup"><span data-stu-id="279e7-265">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="279e7-266">To start log streaming, use the [`az webapp log tail`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-tail) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="279e7-266">To start log streaming, use the [`az webapp log tail`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-tail) command in the Cloud Shell.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="279e7-267">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span><span class="sxs-lookup"><span data-stu-id="279e7-267">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="279e7-268">You now see console logs piped to your terminal.</span><span class="sxs-lookup"><span data-stu-id="279e7-268">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="279e7-269">Stop log streaming at any time by typing `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="279e7-269">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="279e7-270">Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="279e7-270">Manage your Azure web app</span></span>

<span data-ttu-id="279e7-271">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="279e7-271">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="279e7-272">From the left menu, click **App Services**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="279e7-272">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="279e7-274">By default, the portal shows your web app's **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="279e7-274">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="279e7-275">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="279e7-275">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="279e7-276">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="279e7-276">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="279e7-277">The tabs on the left side of the page show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="279e7-277">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![App Service page in Azure portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="279e7-279">Next steps</span><span class="sxs-lookup"><span data-stu-id="279e7-279">Next steps</span></span>

<span data-ttu-id="279e7-280">What you learned:</span><span class="sxs-lookup"><span data-stu-id="279e7-280">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="279e7-281">Create a MongoDB database in Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-281">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="279e7-282">Connect a Node.js app to MongoDB</span><span class="sxs-lookup"><span data-stu-id="279e7-282">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="279e7-283">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="279e7-283">Deploy the app to Azure</span></span>
> * <span data-ttu-id="279e7-284">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="279e7-284">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="279e7-285">Stream logs from Azure to your terminal</span><span class="sxs-lookup"><span data-stu-id="279e7-285">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="279e7-286">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="279e7-286">Manage the app in the Azure portal</span></span>

<span data-ttu-id="279e7-287">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span><span class="sxs-lookup"><span data-stu-id="279e7-287">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="279e7-288">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="279e7-288">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
