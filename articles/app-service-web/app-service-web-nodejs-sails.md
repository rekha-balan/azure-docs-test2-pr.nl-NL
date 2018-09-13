---
title: Deploy a Sails.js web app to Azure App Service | Microsoft Docs
description: Learn how to deploy a Node.js application Azure App Service. This tutorial shows you how to deploy a Sails.js web app.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 78578955ebc3ea58ad68314e6ea44715189556f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670399"
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="a46d9-104">Deploy a Sails.js web app to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a46d9-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="a46d9-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a46d9-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="a46d9-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span><span class="sxs-lookup"><span data-stu-id="a46d9-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="a46d9-107">Here, you will learn useful skills like:</span><span class="sxs-lookup"><span data-stu-id="a46d9-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="a46d9-108">Configure a Sails.js app run in App Service.</span><span class="sxs-lookup"><span data-stu-id="a46d9-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="a46d9-109">Deploy an app to App Service from the command line.</span><span class="sxs-lookup"><span data-stu-id="a46d9-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="a46d9-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span><span class="sxs-lookup"><span data-stu-id="a46d9-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="a46d9-111">Store environment variables outside of source control.</span><span class="sxs-lookup"><span data-stu-id="a46d9-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="a46d9-112">Access Azure environment variables from your app.</span><span class="sxs-lookup"><span data-stu-id="a46d9-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="a46d9-113">Connect to a database (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="a46d9-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="a46d9-114">You should have working knowledge of Sails.js.</span><span class="sxs-lookup"><span data-stu-id="a46d9-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="a46d9-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span><span class="sxs-lookup"><span data-stu-id="a46d9-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a46d9-116">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="a46d9-116">CLI versions to complete the task</span></span>

<span data-ttu-id="a46d9-117">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="a46d9-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a46d9-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span><span class="sxs-lookup"><span data-stu-id="a46d9-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="a46d9-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="a46d9-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a46d9-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a46d9-120">Prerequisites</span></span>
* [<span data-ttu-id="a46d9-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="a46d9-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="a46d9-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="a46d9-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="a46d9-123">Git</span><span class="sxs-lookup"><span data-stu-id="a46d9-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="a46d9-124">Azure CLI 2.0 Preview</span><span class="sxs-lookup"><span data-stu-id="a46d9-124">Azure CLI 2.0 Preview</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="a46d9-125">A Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="a46d9-125">A Microsoft Azure account.</span></span> <span data-ttu-id="a46d9-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a46d9-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="a46d9-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span><span class="sxs-lookup"><span data-stu-id="a46d9-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="a46d9-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span><span class="sxs-lookup"><span data-stu-id="a46d9-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="a46d9-129">Step 1: Create and configure a Sails.js app locally</span><span class="sxs-lookup"><span data-stu-id="a46d9-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="a46d9-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span><span class="sxs-lookup"><span data-stu-id="a46d9-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="a46d9-131">Open the command-line terminal of your choice and `CD` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="a46d9-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="a46d9-132">Create a Sails.js app and run it:</span><span class="sxs-lookup"><span data-stu-id="a46d9-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="a46d9-133">Make sure you can navigate to the default home page at http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="a46d9-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="a46d9-134">Next, enable logging for Azure.</span><span class="sxs-lookup"><span data-stu-id="a46d9-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="a46d9-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span><span class="sxs-lookup"><span data-stu-id="a46d9-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="a46d9-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span><span class="sxs-lookup"><span data-stu-id="a46d9-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="a46d9-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="a46d9-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="a46d9-138">Next, configure the Sails.js app to use Azure environment variables.</span><span class="sxs-lookup"><span data-stu-id="a46d9-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="a46d9-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="a46d9-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="a46d9-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="a46d9-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="a46d9-141">Next, hardcode the Node.js version you want to use.</span><span class="sxs-lookup"><span data-stu-id="a46d9-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="a46d9-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span><span class="sxs-lookup"><span data-stu-id="a46d9-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="a46d9-143">Finally, initialize a Git repository and commit your files.</span><span class="sxs-lookup"><span data-stu-id="a46d9-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="a46d9-144">In the application root (where package.json is), run the following Git commands:</span><span class="sxs-lookup"><span data-stu-id="a46d9-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="a46d9-145">Your code is ready to be deployed.</span><span class="sxs-lookup"><span data-stu-id="a46d9-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="a46d9-146">Step 2: Create an Azure app and deploy Sails.js</span><span class="sxs-lookup"><span data-stu-id="a46d9-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="a46d9-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span><span class="sxs-lookup"><span data-stu-id="a46d9-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="a46d9-148">log in to Azure like so:</span><span class="sxs-lookup"><span data-stu-id="a46d9-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="a46d9-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a46d9-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="a46d9-150">Set the deployment user for App Service.</span><span class="sxs-lookup"><span data-stu-id="a46d9-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="a46d9-151">You will deploy code using these credentials later.</span><span class="sxs-lookup"><span data-stu-id="a46d9-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="a46d9-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span><span class="sxs-lookup"><span data-stu-id="a46d9-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="a46d9-153">For this PHP tutorial, you don't really need to know what it is.</span><span class="sxs-lookup"><span data-stu-id="a46d9-153">For this PHP tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="a46d9-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span><span class="sxs-lookup"><span data-stu-id="a46d9-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="a46d9-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span><span class="sxs-lookup"><span data-stu-id="a46d9-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="a46d9-156">For this PHP tutorial, just know that you won't be charged for web apps in this plan.</span><span class="sxs-lookup"><span data-stu-id="a46d9-156">For this PHP tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="a46d9-157">Create a new web app with a unique name in `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="a46d9-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="a46d9-158">Step 3: Configure and deploy your Sails.js app</span><span class="sxs-lookup"><span data-stu-id="a46d9-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="a46d9-159">Configure local Git deployment for your new web app with the following command:</span><span class="sxs-lookup"><span data-stu-id="a46d9-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="a46d9-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span><span class="sxs-lookup"><span data-stu-id="a46d9-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="a46d9-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span><span class="sxs-lookup"><span data-stu-id="a46d9-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="a46d9-162">Deploy your sample code to the `azure` Git remote.</span><span class="sxs-lookup"><span data-stu-id="a46d9-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="a46d9-163">When prompted, use the deployment credentials you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="a46d9-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="a46d9-164">Finally, just launch your live Azure app in the browser:</span><span class="sxs-lookup"><span data-stu-id="a46d9-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="a46d9-165">You should now see the same Sails.js home page.</span><span class="sxs-lookup"><span data-stu-id="a46d9-165">You should now see the same Sails.js home page.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="a46d9-166">Troubleshoot your deployment</span><span class="sxs-lookup"><span data-stu-id="a46d9-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="a46d9-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span><span class="sxs-lookup"><span data-stu-id="a46d9-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="a46d9-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="a46d9-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="a46d9-169">If the app has started successfully, the stdout log should show you the familiar message:</span><span class="sxs-lookup"><span data-stu-id="a46d9-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="a46d9-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span><span class="sxs-lookup"><span data-stu-id="a46d9-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="a46d9-171">Connect to a database in Azure</span><span class="sxs-lookup"><span data-stu-id="a46d9-171">Connect to a database in Azure</span></span>
<span data-ttu-id="a46d9-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span><span class="sxs-lookup"><span data-stu-id="a46d9-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="a46d9-173">The steps in this section show you how to connect to MongoDB by using an [Azure DocumentDB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span><span class="sxs-lookup"><span data-stu-id="a46d9-173">The steps in this section show you how to connect to MongoDB by using an [Azure DocumentDB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="a46d9-174">[Create a DocumentDB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="a46d9-174">[Create a DocumentDB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="a46d9-175">[Create a DocumentDB collection and database](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="a46d9-175">[Create a DocumentDB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="a46d9-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span><span class="sxs-lookup"><span data-stu-id="a46d9-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="a46d9-177">[Find the connection information for your DocumentDB database](../documentdb/documentdb-connect-mongodb-account.md#a-idgetcustomconnectiona-get-the-mongodb-connection-string-to-customize).</span><span class="sxs-lookup"><span data-stu-id="a46d9-177">[Find the connection information for your DocumentDB database](../documentdb/documentdb-connect-mongodb-account.md#a-idgetcustomconnectiona-get-the-mongodb-connection-string-to-customize).</span></span>
2. <span data-ttu-id="a46d9-178">From your command-line terminal, install the MongoDB adapter:</span><span class="sxs-lookup"><span data-stu-id="a46d9-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="a46d9-179">Open config/connections.js and add the following connection object to the list:</span><span class="sxs-lookup"><span data-stu-id="a46d9-179">Open config/connections.js and add the following connection object to the list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="a46d9-180">The `ssl: true` option is important because [Azure DocumentDB requires it](../documentdb/documentdb-connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="a46d9-180">The `ssl: true` option is important because [Azure DocumentDB requires it](../documentdb/documentdb-connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="a46d9-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span><span class="sxs-lookup"><span data-stu-id="a46d9-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="a46d9-182">To do this, run the following commands from your terminal.</span><span class="sxs-lookup"><span data-stu-id="a46d9-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="a46d9-183">Use the connection information for your DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="a46d9-183">Use the connection information for your DocumentDB database.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="a46d9-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span><span class="sxs-lookup"><span data-stu-id="a46d9-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="a46d9-185">Next, you will configure your development environment to use the same connection information.</span><span class="sxs-lookup"><span data-stu-id="a46d9-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="a46d9-186">Open config/local.js and add the following connections object:</span><span class="sxs-lookup"><span data-stu-id="a46d9-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="a46d9-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span><span class="sxs-lookup"><span data-stu-id="a46d9-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="a46d9-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span><span class="sxs-lookup"><span data-stu-id="a46d9-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="a46d9-189">Now, you are able to connect to your DocumentDB (MongoDB) database both from your Azure web app and from your local development environment.</span><span class="sxs-lookup"><span data-stu-id="a46d9-189">Now, you are able to connect to your DocumentDB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="a46d9-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span><span class="sxs-lookup"><span data-stu-id="a46d9-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="a46d9-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span><span class="sxs-lookup"><span data-stu-id="a46d9-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="a46d9-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span><span class="sxs-lookup"><span data-stu-id="a46d9-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="a46d9-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="a46d9-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="a46d9-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span><span class="sxs-lookup"><span data-stu-id="a46d9-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="a46d9-195">For example:</span><span class="sxs-lookup"><span data-stu-id="a46d9-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="a46d9-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span><span class="sxs-lookup"><span data-stu-id="a46d9-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="a46d9-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span><span class="sxs-lookup"><span data-stu-id="a46d9-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="a46d9-198">Access the blueprint API you just created in the browser.</span><span class="sxs-lookup"><span data-stu-id="a46d9-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="a46d9-199">For example:</span><span class="sxs-lookup"><span data-stu-id="a46d9-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="a46d9-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span><span class="sxs-lookup"><span data-stu-id="a46d9-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="a46d9-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span><span class="sxs-lookup"><span data-stu-id="a46d9-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="a46d9-202">Access the blueprint API of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a46d9-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="a46d9-203">For example:</span><span class="sxs-lookup"><span data-stu-id="a46d9-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="a46d9-204">If the API returns another new entry, then your Azure web app is talking to your DocumentDB (MongoDB) database.</span><span class="sxs-lookup"><span data-stu-id="a46d9-204">If the API returns another new entry, then your Azure web app is talking to your DocumentDB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="a46d9-205">More resources</span><span class="sxs-lookup"><span data-stu-id="a46d9-205">More resources</span></span>
* [<span data-ttu-id="a46d9-206">Get started with Node.js web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a46d9-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="a46d9-207">Using Node.js Modules with Azure applications</span><span class="sxs-lookup"><span data-stu-id="a46d9-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)

