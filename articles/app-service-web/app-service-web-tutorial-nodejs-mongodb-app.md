---
title: Build a Node.js and MongoDB web app in Azure | Microsoft Docs
description: Learn how to get a Node.js app working in Azure, with connection to a DocumentDB database with a MongoDB connection string.
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
ms.topic: article
ms.date: 03/30/2017
ms.author: cephalin
ms.openlocfilehash: 5aa4c850a8a8cab6efd138b221096c376da1f803
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553570"
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="ff56f-103">Build a Node.js and MongoDB web app in Azure</span><span class="sxs-lookup"><span data-stu-id="ff56f-103">Build a Node.js and MongoDB web app in Azure</span></span>
<span data-ttu-id="ff56f-104">This tutorial shows you how to create a Node.js web app in Azure and connect it to a MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="ff56f-104">This tutorial shows you how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="ff56f-105">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff56f-105">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![MEAN.js app running in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

## <a name="before-you-begin"></a><span data-ttu-id="ff56f-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ff56f-107">Before you begin</span></span>

<span data-ttu-id="ff56f-108">Before running this sample, install the following prerequisites locally:</span><span class="sxs-lookup"><span data-stu-id="ff56f-108">Before running this sample, install the following prerequisites locally:</span></span>

1. [<span data-ttu-id="ff56f-109">Download and install git</span><span class="sxs-lookup"><span data-stu-id="ff56f-109">Download and install git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="ff56f-110">Download and install Node.js and NPM</span><span class="sxs-lookup"><span data-stu-id="ff56f-110">Download and install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="ff56f-111">[Download, install, and run MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="ff56f-111">[Download, install, and run MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> 
1. [<span data-ttu-id="ff56f-112">Download and install the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ff56f-112">Download and install the Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="step-1---test-local-mongodb-database"></a><span data-ttu-id="ff56f-113">Step 1 - Test local MongoDB database</span><span class="sxs-lookup"><span data-stu-id="ff56f-113">Step 1 - Test local MongoDB database</span></span>
<span data-ttu-id="ff56f-114">In this step, you make sure that your local MongoDB database is running.</span><span class="sxs-lookup"><span data-stu-id="ff56f-114">In this step, you make sure that your local MongoDB database is running.</span></span>

<span data-ttu-id="ff56f-115">Open the terminal window and `CD` to the `bin` directory of your MongoDB installation.</span><span class="sxs-lookup"><span data-stu-id="ff56f-115">Open the terminal window and `CD` to the `bin` directory of your MongoDB installation.</span></span> 

<span data-ttu-id="ff56f-116">Run `mongo` in the terminal to connect to your local MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="ff56f-116">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="ff56f-117">If your connection is successful, then your MongoDB database is already running.</span><span class="sxs-lookup"><span data-stu-id="ff56f-117">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="ff56f-118">If not, make sure that your local MongoDB database is started by following the steps at [Download, install, and run MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="ff56f-118">If not, make sure that your local MongoDB database is started by following the steps at [Download, install, and run MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span>

<span data-ttu-id="ff56f-119">When you are done testing your MongoDB database, type `Ctrl`+`C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="ff56f-119">When you are done testing your MongoDB database, type `Ctrl`+`C` in the terminal.</span></span> 

<a name="step2"></a>

## <a name="step-2---create-local-nodejs-application"></a><span data-ttu-id="ff56f-120">Step 2 - Create local Node.js application</span><span class="sxs-lookup"><span data-stu-id="ff56f-120">Step 2 - Create local Node.js application</span></span>
<span data-ttu-id="ff56f-121">In this step, you set up the local Node.js project.</span><span class="sxs-lookup"><span data-stu-id="ff56f-121">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="ff56f-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="ff56f-122">Clone the sample application</span></span>

<span data-ttu-id="ff56f-123">Open the terminal window and `CD` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="ff56f-123">Open the terminal window and `CD` to a working directory.</span></span>  

<span data-ttu-id="ff56f-124">Run the following commands to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="ff56f-124">Run the following commands to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="ff56f-125">This sample repository contains a [MEAN.js](http://meanjs.org/) application.</span><span class="sxs-lookup"><span data-stu-id="ff56f-125">This sample repository contains a [MEAN.js](http://meanjs.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="ff56f-126">Run the application</span><span class="sxs-lookup"><span data-stu-id="ff56f-126">Run the application</span></span>

<span data-ttu-id="ff56f-127">Install the required packages and start the application.</span><span class="sxs-lookup"><span data-stu-id="ff56f-127">Install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="ff56f-128">When the app is fully loaded, you should see something similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="ff56f-128">When the app is fully loaded, you should see something similar to the following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="ff56f-129">Navigate to `http://localhost:3000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="ff56f-129">Navigate to `http://localhost:3000` in a browser.</span></span> <span data-ttu-id="ff56f-130">Click **Sign Up** in the top menu and try to create a dummy user.</span><span class="sxs-lookup"><span data-stu-id="ff56f-130">Click **Sign Up** in the top menu and try to create a dummy user.</span></span> 

<span data-ttu-id="ff56f-131">The MEAN.js sample application stores user data in the database.</span><span class="sxs-lookup"><span data-stu-id="ff56f-131">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="ff56f-132">If you are successful and MEAN.js automatically signs into the created user, then your app is writing data to the local MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="ff56f-132">If you are successful and MEAN.js automatically signs into the created user, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js connects successfully to MongoDB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="ff56f-134">Try clicking **Admin** > **Manage Articles** to add some articles.</span><span class="sxs-lookup"><span data-stu-id="ff56f-134">Try clicking **Admin** > **Manage Articles** to add some articles.</span></span>

<span data-ttu-id="ff56f-135">To stop Node.js at anytime, type `Ctrl`+`C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="ff56f-135">To stop Node.js at anytime, type `Ctrl`+`C` in the terminal.</span></span> 

## <a name="step-3---create-a-production-mongodb-database"></a><span data-ttu-id="ff56f-136">Step 3 - Create a production MongoDB database</span><span class="sxs-lookup"><span data-stu-id="ff56f-136">Step 3 - Create a production MongoDB database</span></span>

<span data-ttu-id="ff56f-137">In this step, you create a MongoDB database in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-137">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="ff56f-138">When your app is deployed to Azure, it uses this database for its production workload.</span><span class="sxs-lookup"><span data-stu-id="ff56f-138">When your app is deployed to Azure, it uses this database for its production workload.</span></span>

<span data-ttu-id="ff56f-139">For MongoDB, this tutorial uses [Azure DocumentDB](/azure/documentdb/), which can support MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="ff56f-139">For MongoDB, this tutorial uses [Azure DocumentDB](/azure/documentdb/), which can support MongoDB client connections.</span></span> <span data-ttu-id="ff56f-140">In other words, your Node.js application only knows that it's connecting to a MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="ff56f-140">In other words, your Node.js application only knows that it's connecting to a MongoDB database.</span></span> <span data-ttu-id="ff56f-141">The fact that the connection is backed by a DocumentDB database is transparent to the application.</span><span class="sxs-lookup"><span data-stu-id="ff56f-141">The fact that the connection is backed by a DocumentDB database is transparent to the application.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="ff56f-142">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="ff56f-142">Log in to Azure</span></span>

<span data-ttu-id="ff56f-143">You are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Node.js application in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ff56f-143">You are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Node.js application in Azure App Service.</span></span>  <span data-ttu-id="ff56f-144">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="ff56f-144">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="ff56f-145">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="ff56f-145">Create a resource group</span></span>

<span data-ttu-id="ff56f-146">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ff56f-146">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ff56f-147">An Azure resource group is a logical container into which Azure resources like web apps, databases, and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="ff56f-147">An Azure resource group is a logical container into which Azure resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="ff56f-148">The following example creates a resource group in the West Europe region:</span><span class="sxs-lookup"><span data-stu-id="ff56f-148">The following example creates a resource group in the West Europe region:</span></span>

```azurecli
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="ff56f-149">To see what possible values you can use for `--location`, use the `az appservice list-locations` Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="ff56f-149">To see what possible values you can use for `--location`, use the `az appservice list-locations` Azure CLI command.</span></span>

### <a name="create-a-documentdb-account"></a><span data-ttu-id="ff56f-150">Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="ff56f-150">Create a DocumentDB account</span></span>

<span data-ttu-id="ff56f-151">Create a DocumentDB account with the [az documentdb create](/cli/azure/documentdb#create) command.</span><span class="sxs-lookup"><span data-stu-id="ff56f-151">Create a DocumentDB account with the [az documentdb create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="ff56f-152">In the following command, substitute your own unique DocumentDB name where you see the `<documentdb_name>` placeholder.</span><span class="sxs-lookup"><span data-stu-id="ff56f-152">In the following command, substitute your own unique DocumentDB name where you see the `<documentdb_name>` placeholder.</span></span> <span data-ttu-id="ff56f-153">This unique name will be used as the part of your DocumentDB endpoint (`https://<documentdb_name>.documents.azure.com/`), so the name needs to be unique across all DocumentDB accounts in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-153">This unique name will be used as the part of your DocumentDB endpoint (`https://<documentdb_name>.documents.azure.com/`), so the name needs to be unique across all DocumentDB accounts in Azure.</span></span> 

```azurecli
az documentdb create --name <documentdb_name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="ff56f-154">The `--kind MongoDB` parameter enables MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="ff56f-154">The `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="ff56f-155">When the DocumentDB account is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ff56f-155">When the DocumentDB account is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<documentdb_name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<documentdb_name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<documentdb_name>",
  "readLocations": [
    ...
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    ...
  ]
} 
```

## <a name="step-4---connect-your-nodejs-application-to-the-database"></a><span data-ttu-id="ff56f-156">Step 4 - Connect your Node.js application to the database</span><span class="sxs-lookup"><span data-stu-id="ff56f-156">Step 4 - Connect your Node.js application to the database</span></span>

<span data-ttu-id="ff56f-157">In this step, you connect your MEAN.js sample application to the DocumentDB database you just created, using a MongoDB connection string.</span><span class="sxs-lookup"><span data-stu-id="ff56f-157">In this step, you connect your MEAN.js sample application to the DocumentDB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="ff56f-158">Retrieve the database key</span><span class="sxs-lookup"><span data-stu-id="ff56f-158">Retrieve the database key</span></span>

<span data-ttu-id="ff56f-159">To connect to the DocumentDB database, you need the database key.</span><span class="sxs-lookup"><span data-stu-id="ff56f-159">To connect to the DocumentDB database, you need the database key.</span></span> <span data-ttu-id="ff56f-160">Use the [az documentdb list-keys](/cli/azure/documentdb#list-keys) command to retrieve the primary key.</span><span class="sxs-lookup"><span data-stu-id="ff56f-160">Use the [az documentdb list-keys](/cli/azure/documentdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli
az documentdb list-keys --name <documentdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="ff56f-161">The Azure CLI outputs information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ff56f-161">The Azure CLI outputs information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RUayjYjixJDWG5xTqIiXjC...",
  "primaryReadonlyMasterKey": "...",
  "secondaryMasterKey": "...",
  "secondaryReadonlyMasterKey": "..."
}
```

<span data-ttu-id="ff56f-162">Copy the value of `primaryMasterKey` to a text editor.</span><span class="sxs-lookup"><span data-stu-id="ff56f-162">Copy the value of `primaryMasterKey` to a text editor.</span></span> <span data-ttu-id="ff56f-163">You need this information in the next step.</span><span class="sxs-lookup"><span data-stu-id="ff56f-163">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="ff56f-164">Configure the connection string in your Node.js application</span><span class="sxs-lookup"><span data-stu-id="ff56f-164">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="ff56f-165">In your MEAN.js repository, open `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-165">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="ff56f-166">In the `db` object, replace the value of `uri` as show in the following example.</span><span class="sxs-lookup"><span data-stu-id="ff56f-166">In the `db` object, replace the value of `uri` as show in the following example.</span></span> <span data-ttu-id="ff56f-167">Be sure to also replace the two `<documentdb_name>` placeholders with your DocumentDB database name, and the `<primary_maste_key>` placeholder with the key you copied in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ff56f-167">Be sure to also replace the two `<documentdb_name>` placeholders with your DocumentDB database name, and the `<primary_maste_key>` placeholder with the key you copied in the previous step.</span></span>

```javascript
db: {
  uri: 'mongodb://<documentdb_name>:<primary_maste_key>@<documentdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

> [!NOTE] 
> <span data-ttu-id="ff56f-168">The `ssl=true` option is important because [Azure DocumentDB requires SSL](../documentdb/documentdb-connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="ff56f-168">The `ssl=true` option is important because [Azure DocumentDB requires SSL](../documentdb/documentdb-connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="ff56f-169">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="ff56f-169">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="ff56f-170">Test the application in production mode</span><span class="sxs-lookup"><span data-stu-id="ff56f-170">Test the application in production mode</span></span> 

<span data-ttu-id="ff56f-171">Like some other Node.js applications, MEAN.js uses `gulp prod` to minify and bundle scripts for the production environment.</span><span class="sxs-lookup"><span data-stu-id="ff56f-171">Like some other Node.js applications, MEAN.js uses `gulp prod` to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="ff56f-172">This generates the files needed by the production environment.</span><span class="sxs-lookup"><span data-stu-id="ff56f-172">This generates the files needed by the production environment.</span></span> 

<span data-ttu-id="ff56f-173">Run `gulp prod` now.</span><span class="sxs-lookup"><span data-stu-id="ff56f-173">Run `gulp prod` now.</span></span>

```bash
gulp prod
```

<span data-ttu-id="ff56f-174">Next, run the following command to use the connection string you configured in `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-174">Next, run the following command to use the connection string you configured in `config/env/production.js`.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="ff56f-175">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment, and `node server.js` starts the Node.js server with `server.js` in your repository root.</span><span class="sxs-lookup"><span data-stu-id="ff56f-175">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment, and `node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="ff56f-176">This is how your Node.js application is loaded in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-176">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="ff56f-177">When the app is loaded, check to make sure that it's running in production:</span><span class="sxs-lookup"><span data-stu-id="ff56f-177">When the app is loaded, check to make sure that it's running in production:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<documentdb_name>:<primary_maste_key>@<documentdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="ff56f-178">Navigate to `http://localhost:8443` in a browser.</span><span class="sxs-lookup"><span data-stu-id="ff56f-178">Navigate to `http://localhost:8443` in a browser.</span></span> <span data-ttu-id="ff56f-179">Click **Sign Up** in the top menu and try to create a dummy user just like before.</span><span class="sxs-lookup"><span data-stu-id="ff56f-179">Click **Sign Up** in the top menu and try to create a dummy user just like before.</span></span> <span data-ttu-id="ff56f-180">If you are successful, then your app is writing data to the DocumentDB database in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-180">If you are successful, then your app is writing data to the DocumentDB database in Azure.</span></span> 

## <a name="step-5---deploy-the-nodejs-application-to-azure"></a><span data-ttu-id="ff56f-181">Step 5 - Deploy the Node.js application to Azure</span><span class="sxs-lookup"><span data-stu-id="ff56f-181">Step 5 - Deploy the Node.js application to Azure</span></span>
<span data-ttu-id="ff56f-182">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ff56f-182">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="ff56f-183">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="ff56f-183">Create an App Service plan</span></span>

<span data-ttu-id="ff56f-184">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span><span class="sxs-lookup"><span data-stu-id="ff56f-184">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ff56f-185">An App Service plan represents the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="ff56f-185">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="ff56f-186">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="ff56f-186">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span> 
> 
> <span data-ttu-id="ff56f-187">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="ff56f-187">App Service plans define:</span></span> 
> 
> * <span data-ttu-id="ff56f-188">Region (North Europe, East US, Southeast Asia)</span><span class="sxs-lookup"><span data-stu-id="ff56f-188">Region (North Europe, East US, Southeast Asia)</span></span> 
> * <span data-ttu-id="ff56f-189">Instance Size (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="ff56f-189">Instance Size (Small, Medium, Large)</span></span> 
> * <span data-ttu-id="ff56f-190">Scale Count (one, two, or three instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="ff56f-190">Scale Count (one, two, or three instances, etc.)</span></span> 
> * <span data-ttu-id="ff56f-191">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="ff56f-191">SKU (Free, Shared, Basic, Standard, Premium)</span></span> 
> 

<span data-ttu-id="ff56f-192">The following example creates an App Service plan named `myAppServicePlan` using the **FREE** pricing tier:</span><span class="sxs-lookup"><span data-stu-id="ff56f-192">The following example creates an App Service plan named `myAppServicePlan` using the **FREE** pricing tier:</span></span>

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="ff56f-193">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ff56f-193">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 0, 
    "family": "F", 
    "name": "F1", 
    "tier": "Free" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="ff56f-194">Create a web app</span><span class="sxs-lookup"><span data-stu-id="ff56f-194">Create a web app</span></span>

<span data-ttu-id="ff56f-195">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="ff56f-195">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="ff56f-196">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span><span class="sxs-lookup"><span data-stu-id="ff56f-196">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="ff56f-197">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span><span class="sxs-lookup"><span data-stu-id="ff56f-197">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="ff56f-198">In the following command, substitute `<app_name>` placeholder with your own unique app name.</span><span class="sxs-lookup"><span data-stu-id="ff56f-198">In the following command, substitute `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="ff56f-199">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-199">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="ff56f-200">You can later map any custom DNS entry to the web app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="ff56f-200">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="ff56f-201">When the web app has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ff56f-201">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="ff56f-202">Configure an environment variable</span><span class="sxs-lookup"><span data-stu-id="ff56f-202">Configure an environment variable</span></span>

<span data-ttu-id="ff56f-203">Earlier in the tutorial, you hardcoded the database connection string in `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-203">Earlier in the tutorial, you hardcoded the database connection string in `config/env/production.js`.</span></span> <span data-ttu-id="ff56f-204">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span><span class="sxs-lookup"><span data-stu-id="ff56f-204">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="ff56f-205">For your app running in Azure, you will use an environment variable instead.</span><span class="sxs-lookup"><span data-stu-id="ff56f-205">For your app running in Azure, you will use an environment variable instead.</span></span>

<span data-ttu-id="ff56f-206">In App Service, you set environment variables as _app settings_ by using the [az appservice web config appsettings update](/cli/azure/appservice/web/config/appsettings#update) command.</span><span class="sxs-lookup"><span data-stu-id="ff56f-206">In App Service, you set environment variables as _app settings_ by using the [az appservice web config appsettings update](/cli/azure/appservice/web/config/appsettings#update) command.</span></span> 

<span data-ttu-id="ff56f-207">The following example lets you configure a `MONGODB_URI` app setting in your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ff56f-207">The following example lets you configure a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="ff56f-208">Be sure to replace the placeholders like before.</span><span class="sxs-lookup"><span data-stu-id="ff56f-208">Be sure to replace the placeholders like before.</span></span>

```azurecli
az appservice web config appsettings update --name <app_name> --resource-group myResourceGroup --settings MONGODB_URI="mongodb://<documentdb_name>:<primary_maste_key>@<documentdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="ff56f-209">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span><span class="sxs-lookup"><span data-stu-id="ff56f-209">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="ff56f-210">Now, undo your changes to `config/env/production.js` with the following command:</span><span class="sxs-lookup"><span data-stu-id="ff56f-210">Now, undo your changes to `config/env/production.js` with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="ff56f-211">Open `config/env/production.js` again.</span><span class="sxs-lookup"><span data-stu-id="ff56f-211">Open `config/env/production.js` again.</span></span> <span data-ttu-id="ff56f-212">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you just created.</span><span class="sxs-lookup"><span data-stu-id="ff56f-212">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you just created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="ff56f-213">Configure local git deployment</span><span class="sxs-lookup"><span data-stu-id="ff56f-213">Configure local git deployment</span></span> 

<span data-ttu-id="ff56f-214">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span><span class="sxs-lookup"><span data-stu-id="ff56f-214">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="ff56f-215">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span><span class="sxs-lookup"><span data-stu-id="ff56f-215">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> 

<span data-ttu-id="ff56f-216">Use the [az appservice web deployment user set](/cli/azure/appservice/web/deployment/user#set) command to create your account-level credentials.</span><span class="sxs-lookup"><span data-stu-id="ff56f-216">Use the [az appservice web deployment user set](/cli/azure/appservice/web/deployment/user#set) command to create your account-level credentials.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ff56f-217">A deployment user is required for FTP and Local Git deployment to App Service.</span><span class="sxs-lookup"><span data-stu-id="ff56f-217">A deployment user is required for FTP and Local Git deployment to App Service.</span></span> <span data-ttu-id="ff56f-218">This deployment user is account-level.</span><span class="sxs-lookup"><span data-stu-id="ff56f-218">This deployment user is account-level.</span></span> <span data-ttu-id="ff56f-219">As such, it is different from your Azure subscription account.</span><span class="sxs-lookup"><span data-stu-id="ff56f-219">As such, it is different from your Azure subscription account.</span></span> <span data-ttu-id="ff56f-220">You only need to configure this deployment user once.</span><span class="sxs-lookup"><span data-stu-id="ff56f-220">You only need to configure this deployment user once.</span></span>

```azurecli
az appservice web deployment user set --user-name <specify-a-username> --password <mininum-8-char-captital-lowercase-number>
```

<span data-ttu-id="ff56f-221">Use the [az appservice web source-control config-local-git](/cli/azure/appservice/web/source-control#config-local-git) command to configure local Git access to the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ff56f-221">Use the [az appservice web source-control config-local-git](/cli/azure/appservice/web/source-control#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli
az appservice web source-control config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="ff56f-222">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span><span class="sxs-lookup"><span data-stu-id="ff56f-222">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="ff56f-223">Copy the output from the terminal as it will be used in the next step.</span><span class="sxs-lookup"><span data-stu-id="ff56f-223">Copy the output from the terminal as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="ff56f-224">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="ff56f-224">Push to Azure from Git</span></span>

<span data-ttu-id="ff56f-225">Add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="ff56f-225">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="ff56f-226">Push to the Azure remote to deploy your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="ff56f-226">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="ff56f-227">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span><span class="sxs-lookup"><span data-stu-id="ff56f-227">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="ff56f-228">During deployment, Azure App Service communicates its progress with Git.</span><span class="sxs-lookup"><span data-stu-id="ff56f-228">During deployment, Azure App Service communicates its progress with Git.</span></span>

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

> [!NOTE]
> <span data-ttu-id="ff56f-229">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-229">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="ff56f-230">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span><span class="sxs-lookup"><span data-stu-id="ff56f-230">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 
>
> - <span data-ttu-id="ff56f-231">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="ff56f-231">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="ff56f-232">`deploy.sh` - The custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="ff56f-232">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="ff56f-233">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-233">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 
>
> <span data-ttu-id="ff56f-234">You can use this approach to add any step to your Git-based deployment.</span><span class="sxs-lookup"><span data-stu-id="ff56f-234">You can use this approach to add any step to your Git-based deployment.</span></span>
>
> <span data-ttu-id="ff56f-235">Note that if you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span><span class="sxs-lookup"><span data-stu-id="ff56f-235">Note that if you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>
>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="ff56f-236">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="ff56f-236">Browse to the Azure web app</span></span> 
<span data-ttu-id="ff56f-237">Browse to the deployed web app using your web browser.</span><span class="sxs-lookup"><span data-stu-id="ff56f-237">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="ff56f-238">Click **Sign Up** in the top menu and try to create a dummy user.</span><span class="sxs-lookup"><span data-stu-id="ff56f-238">Click **Sign Up** in the top menu and try to create a dummy user.</span></span> 

<span data-ttu-id="ff56f-239">If you are successful and the app automatically signs into the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (DocumentDB) database.</span><span class="sxs-lookup"><span data-stu-id="ff56f-239">If you are successful and the app automatically signs into the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (DocumentDB) database.</span></span> 

![MEAN.js app running in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="ff56f-241">Try clicking **Admin** > **Manage Articles** to add some articles.</span><span class="sxs-lookup"><span data-stu-id="ff56f-241">Try clicking **Admin** > **Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="ff56f-242">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="ff56f-242">**Congratulations!**</span></span> <span data-ttu-id="ff56f-243">You're running a data-driven Node.js app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ff56f-243">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="step-6---update-data-model-and-redeploy"></a><span data-ttu-id="ff56f-244">Step 6 - Update data model and redeploy</span><span class="sxs-lookup"><span data-stu-id="ff56f-244">Step 6 - Update data model and redeploy</span></span>

<span data-ttu-id="ff56f-245">In this step, you make some changes to the `article` data model and publish your changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-245">In this step, you make some changes to the `article` data model and publish your changes to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="ff56f-246">Update the data model</span><span class="sxs-lookup"><span data-stu-id="ff56f-246">Update the data model</span></span>

<span data-ttu-id="ff56f-247">Open `modules/articles/server/models/articles.server.controller.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-247">Open `modules/articles/server/models/articles.server.controller.js`.</span></span>

<span data-ttu-id="ff56f-248">In `ArticleSchema`, add a `String` type called `comment`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-248">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="ff56f-249">When you're done, your schema code should look like this:</span><span class="sxs-lookup"><span data-stu-id="ff56f-249">When you're done, your schema code should look like this:</span></span>

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

<span data-ttu-id="ff56f-250">You are done with the model changes.</span><span class="sxs-lookup"><span data-stu-id="ff56f-250">You are done with the model changes.</span></span> 

### <a name="update-the-articles-code"></a><span data-ttu-id="ff56f-251">Update the articles code</span><span class="sxs-lookup"><span data-stu-id="ff56f-251">Update the articles code</span></span>

<span data-ttu-id="ff56f-252">Next, update the rest of your `articles` code to use `comment`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-252">Next, update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="ff56f-253">In all, there are five (5) files you need to modify, the server controller and the four client views.</span><span class="sxs-lookup"><span data-stu-id="ff56f-253">In all, there are five (5) files you need to modify, the server controller and the four client views.</span></span> 

<span data-ttu-id="ff56f-254">First, open `modules/articles/server/controllers/articles.server.controller.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-254">First, open `modules/articles/server/controllers/articles.server.controller.js`.</span></span>

<span data-ttu-id="ff56f-255">In the `update` function, add an assignment for `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-255">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="ff56f-256">When you're done, your `update` function should look like this:</span><span class="sxs-lookup"><span data-stu-id="ff56f-256">When you're done, your `update` function should look like this:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="ff56f-257">Next, open `modules/client/views/view-article.client.view.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-257">Next, open `modules/client/views/view-article.client.view.js`.</span></span>

<span data-ttu-id="ff56f-258">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span><span class="sxs-lookup"><span data-stu-id="ff56f-258">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="ff56f-259">Next, open `modules/client/views/list-articles.client.view.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-259">Next, open `modules/client/views/list-articles.client.view.js`.</span></span>

<span data-ttu-id="ff56f-260">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span><span class="sxs-lookup"><span data-stu-id="ff56f-260">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="ff56f-261">Next, open `modules/client/views/admin/list-articles.client.view.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-261">Next, open `modules/client/views/admin/list-articles.client.view.js`.</span></span>

<span data-ttu-id="ff56f-262">Inside the `<div class="list-group">` tag and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span><span class="sxs-lookup"><span data-stu-id="ff56f-262">Inside the `<div class="list-group">` tag and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="ff56f-263">Finally, open `modules/client/views/admin/list-articles.client.view.js`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-263">Finally, open `modules/client/views/admin/list-articles.client.view.js`.</span></span>

<span data-ttu-id="ff56f-264">Find the `<div class="form-group">` tag that contains the submit button, which looks like this:</span><span class="sxs-lookup"><span data-stu-id="ff56f-264">Find the `<div class="form-group">` tag that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="ff56f-265">Just above this tag, add another `<div class="form-group">` tag that lets people edit the `comment` field.</span><span class="sxs-lookup"><span data-stu-id="ff56f-265">Just above this tag, add another `<div class="form-group">` tag that lets people edit the `comment` field.</span></span> <span data-ttu-id="ff56f-266">Your new tag should look like this:</span><span class="sxs-lookup"><span data-stu-id="ff56f-266">Your new tag should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="ff56f-267">Test your changes locally</span><span class="sxs-lookup"><span data-stu-id="ff56f-267">Test your changes locally</span></span>

<span data-ttu-id="ff56f-268">Save all your changes.</span><span class="sxs-lookup"><span data-stu-id="ff56f-268">Save all your changes.</span></span>

<span data-ttu-id="ff56f-269">Test your changes in production mode again.</span><span class="sxs-lookup"><span data-stu-id="ff56f-269">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="ff56f-270">Remember that your `config/env/production.js` has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span><span class="sxs-lookup"><span data-stu-id="ff56f-270">Remember that your `config/env/production.js` has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="ff56f-271">If you take a look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="ff56f-271">If you take a look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="ff56f-272">This makes sure that you don't touch production data when you test your code changes locally.</span><span class="sxs-lookup"><span data-stu-id="ff56f-272">This makes sure that you don't touch production data when you test your code changes locally.</span></span>
>
>

<span data-ttu-id="ff56f-273">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span><span class="sxs-lookup"><span data-stu-id="ff56f-273">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="ff56f-274">Click **Admin** > **Manage Articles**, then add an article by clicking the **+** button.</span><span class="sxs-lookup"><span data-stu-id="ff56f-274">Click **Admin** > **Manage Articles**, then add an article by clicking the **+** button.</span></span>

<span data-ttu-id="ff56f-275">You should see the new `Comment` textbox now.</span><span class="sxs-lookup"><span data-stu-id="ff56f-275">You should see the new `Comment` textbox now.</span></span>

![Added comment field to Articles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="ff56f-277">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="ff56f-277">Publish changes to Azure</span></span>

<span data-ttu-id="ff56f-278">Commit your changes in git, then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56f-278">Commit your changes in git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="ff56f-279">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality again.</span><span class="sxs-lookup"><span data-stu-id="ff56f-279">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality again.</span></span>

![Model and database changes published to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

> [!NOTE]
> <span data-ttu-id="ff56f-281">If you added any articles earlier, you still can see them.</span><span class="sxs-lookup"><span data-stu-id="ff56f-281">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="ff56f-282">Existing data in your DocumentDB is not lost.</span><span class="sxs-lookup"><span data-stu-id="ff56f-282">Existing data in your DocumentDB is not lost.</span></span> <span data-ttu-id="ff56f-283">Also, your updates to the data schema and leaves your existing data intact.</span><span class="sxs-lookup"><span data-stu-id="ff56f-283">Also, your updates to the data schema and leaves your existing data intact.</span></span>
>
>

## <a name="step-7---stream-diagnostic-logs"></a><span data-ttu-id="ff56f-284">Step 7 - Stream diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="ff56f-284">Step 7 - Stream diagnostic logs</span></span> 

<span data-ttu-id="ff56f-285">While your Node.js application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span><span class="sxs-lookup"><span data-stu-id="ff56f-285">While your Node.js application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="ff56f-286">That way, you can get the same diagnostic messages to help you debug application errors.</span><span class="sxs-lookup"><span data-stu-id="ff56f-286">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="ff56f-287">To start log streaming, use the [az appservice web log tail](/cli/azure/appservice/web/log#tail) command.</span><span class="sxs-lookup"><span data-stu-id="ff56f-287">To start log streaming, use the [az appservice web log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli 
az appservice web log tail --name <app_name> --resource-group myResourceGroup 
``` 

<span data-ttu-id="ff56f-288">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span><span class="sxs-lookup"><span data-stu-id="ff56f-288">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="ff56f-289">You should now see console logs piped to your terminal.</span><span class="sxs-lookup"><span data-stu-id="ff56f-289">You should now see console logs piped to your terminal.</span></span>

<span data-ttu-id="ff56f-290">To stop log streaming at anytime, type `Ctrl`+`C`.</span><span class="sxs-lookup"><span data-stu-id="ff56f-290">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span> 

## <a name="step-8---manage-your-azure-web-app"></a><span data-ttu-id="ff56f-291">Step 8 - Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="ff56f-291">Step 8 - Manage your Azure web app</span></span>

<span data-ttu-id="ff56f-292">Go to the Azure portal to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="ff56f-292">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="ff56f-293">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff56f-293">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="ff56f-294">From the left menu, click **App Service**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ff56f-294">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="ff56f-296">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="ff56f-296">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span></span>

<span data-ttu-id="ff56f-297">By default, your web app's blade shows the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="ff56f-297">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="ff56f-298">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="ff56f-298">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="ff56f-299">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="ff56f-299">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="ff56f-300">The tabs on the left side of the blade show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="ff56f-300">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![App Service blade in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

<span data-ttu-id="ff56f-302">These tabs in the blade show the many great features you can add to your web app.</span><span class="sxs-lookup"><span data-stu-id="ff56f-302">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="ff56f-303">The following list gives you just a few of the possibilities:</span><span class="sxs-lookup"><span data-stu-id="ff56f-303">The following list gives you just a few of the possibilities:</span></span>

* <span data-ttu-id="ff56f-304">Map a custom DNS name</span><span class="sxs-lookup"><span data-stu-id="ff56f-304">Map a custom DNS name</span></span>
* <span data-ttu-id="ff56f-305">Bind a custom SSL certificate</span><span class="sxs-lookup"><span data-stu-id="ff56f-305">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="ff56f-306">Configure continuous deployment</span><span class="sxs-lookup"><span data-stu-id="ff56f-306">Configure continuous deployment</span></span>
* <span data-ttu-id="ff56f-307">Scale up and out</span><span class="sxs-lookup"><span data-stu-id="ff56f-307">Scale up and out</span></span>
* <span data-ttu-id="ff56f-308">Add user authentication</span><span class="sxs-lookup"><span data-stu-id="ff56f-308">Add user authentication</span></span>

<!--

## Step 4 - Download server logs
In this step, you turn on monitoring of your web app with web server logs, and then download these logs. 

### Enable logging
Enable all logging options for your web app.

```azurecli
az appservice web log config --name <app_name> --resource-group myResourceGroup --application-logging true --detailed-error-messages true --failed-request-tracing true --web-server-logging filesystem
```

### Generate errors

To generate some error entries, navigate to a nonexistent page in your web app. For example: `http://<app_name>.azurewebsites.net/404`. 

### Download log files
Download the log files for review.

```azurecli
az appservice web log download --name <app_name> --resource-group myResourceGroup
```

## Step 5 - Scale to another region
In this step, you scale your Node.js app to serve your customers in a new region. That way, you can tailor your web app to customers in different regions, and also put your web app closer to them to improve performance. When you're done with this step, you will have a [Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/) profile with two endpoints, which route traffic to two web apps which reside in different geographical regions.

1. Create a Traffic Manager profile with a unique name and add it to your resource group.

    ```azurecli
    az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name <unique-dns-name>
    ```

    > [!NOTE]
    > `--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).

2. Get the resource ID of your existing Node.js web app.

    ```azurecli
    az appservice web show --name <app_name> --resource-group myResourceGroup --query id --output tsv
    ```

3. Add an endpoint to the Traffic Manager profile and put the output of the last command in `<web-app-1-resource-id>`:

    ```azurecli
    az network traffic-manager endpoint create --name <app_name>-westeurope --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id <web-app-1-resource-id>
    ```

4. Your Traffic Manager profile now has an endpoint that points to your web app. Query for its URL to try it out.

    ```azurecli
    az network traffic-manager profile show --name cephalin-express --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
    ```

    Copy the output into your browser. You should get the default Express page again, with data from your database.

5. Let's add some identifying characteristic to your West Europe app. Add an environment variable.

    ```azurecli
    az appservice web config appsettings update --settings region="Europe" --name <app_name> --resource-group myResourceGroup    
    ```

6. Open `routes/index.js` and change the `router.get()` to use the environment variable.

    ```javascript
    router.get('/', function(req, res, next) {
      res.render('index', { title: 'Express ' + process.env.region, data: output });
    });
    ```

7. Save your changes and push them to Azure.

    ```
    git add .
    git commit -m "added region string."
    git push azure master
    ```

8. Refresh your browser on your Traffic Manager profile's URL. You should now see `Express Europe` in the homepage. 

    Since your Traffic Manager profile only has one endpoint which points to your West Europe web app, this is the only page you'll see. Next, you create a new web app in Southeast Asia and add a new endpoint to the profile.

4. Create an App Service plan and web app in the Southeast Asia region, and deploy the same code to it just like you did in [Step 2]<#step2>.

    ```azurecli
    az appservice plan create --name my-expressjs-appservice-plan-asia --resource-group myResourceGroup --location "Southeast Asia" --sku FREE
    az appservice web create --name <app_name>-asia --plan my-expressjs-appservice-plan-asia --resource-group myResourceGroup
    url=$(az appservice web source-control config-local-git --name <app_name>-asia --resource-group myResourceGroup --query url --output tsv)
    git remote add azureasia $url
    git push azureasia master
    ```

5. Add the same application settings to the new web app. Set the region to `"Asia"`.

    ```azurecli
    az appservice web config appsettings update --settings dbconnstring="mongodb://$accountname:$password@$accountname.documents.azure.com:10250/tutorial?ssl=true&sslverifycertificate=false" --name <app_name>-asia --resource-group myResourceGroup    
    az appservice web config appsettings update --settings region="Asia" --name <app_name>-asia --resource-group myResourceGroup    
    ```

    Since DocumentDB is a [geographically distributed](../documentdb/documentdb-distribute-data-globally.md) NoSQL service, you can use the same MongoDB connection string in the Southeast Asia web app. When the MongoDB client driver connects to your DocumentDB account, Azure automatically figures out where is the closest place to route the connection. No code change is necessary. You only need to add the regions you want to support to your DocumentDB account, which you will do next.

6. Add `Southeast Asia` as a region to your DocumentDB account.

    ```azurecli
    az documentdb update --locations "West Europe"=0 "Southeast Asia"=1 --name $accountname --resource-group myResourceGroup
    ```

3. To finish, add a second endpoint to the Traffic Manager profile and put the output of the last command in `<web-app-2-resource-id>`:

    ```azurecli
    resourceid=$(az appservice web show --name <app_name>-asia --resource-group myResourceGroup --query id --output tsv)
    az network traffic-manager endpoint create -n <app_name>-southeastasia --profile-name myTrafficManagerProfile -g myResourceGroup --type azureEndpoints --target-resource-id resourceid
    ```
  
Now, try to access the URL of your Traffic Manager profile. If you access the URL from the Europe region, you should see "Express Europe", but from the Asia region, you should see "Express Asia".

-->
## <a name="more-resources"></a><span data-ttu-id="ff56f-309">More resources</span><span class="sxs-lookup"><span data-stu-id="ff56f-309">More resources</span></span>







