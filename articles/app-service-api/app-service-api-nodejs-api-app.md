---
title: Node.js API app in Azure App Service | Microsoft Docs
description: Learn how to create a Node.js RESTful API and deploy it to an API app in Azure App Service.
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: ''
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: get-started-article
ms.date: 05/26/2016
ms.author: rachelap
ms.openlocfilehash: ae09e2b0327f2305f832218ecf737eff0669eac0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552364"
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="c9c21-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span><span class="sxs-lookup"><span data-stu-id="c9c21-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="c9c21-104">This tutorial shows how to create a simple [Node.js](http://nodejs.org) API and deploy it to an [API app](app-service-api-apps-why-best-platform.md) in [Azure App Service](../app-service/app-service-value-prop-what-is.md) by using [Git](http://git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="c9c21-104">This tutorial shows how to create a simple [Node.js](http://nodejs.org) API and deploy it to an [API app](app-service-api-apps-why-best-platform.md) in [Azure App Service](../app-service/app-service-value-prop-what-is.md) by using [Git](http://git-scm.com).</span></span> <span data-ttu-id="c9c21-105">You can use any operating system that can run Node.js, and you'll do all your work using command line tools such as cmd.exe or bash.</span><span class="sxs-lookup"><span data-stu-id="c9c21-105">You can use any operating system that can run Node.js, and you'll do all your work using command line tools such as cmd.exe or bash.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9c21-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c9c21-106">Prerequisites</span></span>
1. <span data-ttu-id="c9c21-107">Microsoft Azure account ([open a free account here](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="c9c21-107">Microsoft Azure account ([open a free account here](https://azure.microsoft.com/pricing/free-trial/))</span></span>
2. <span data-ttu-id="c9c21-108">[Node.js](http://nodejs.org) installed (this sample assumes that you have Node.js version 4.2.2)</span><span class="sxs-lookup"><span data-stu-id="c9c21-108">[Node.js](http://nodejs.org) installed (this sample assumes that you have Node.js version 4.2.2)</span></span>
3. <span data-ttu-id="c9c21-109">[Git](https://git-scm.com/) installed</span><span class="sxs-lookup"><span data-stu-id="c9c21-109">[Git](https://git-scm.com/) installed</span></span>
4. <span data-ttu-id="c9c21-110">[GitHub](https://github.com/) account</span><span class="sxs-lookup"><span data-stu-id="c9c21-110">[GitHub](https://github.com/) account</span></span>

<span data-ttu-id="c9c21-111">While App Service supports many ways to deploy your code to an API app, this tutorial shows the Git method and assumes that you have basic knowledge of how to work with Git.</span><span class="sxs-lookup"><span data-stu-id="c9c21-111">While App Service supports many ways to deploy your code to an API app, this tutorial shows the Git method and assumes that you have basic knowledge of how to work with Git.</span></span> <span data-ttu-id="c9c21-112">For information about other deployment methods, see [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c9c21-112">For information about other deployment methods, see [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="c9c21-113">Get the sample code</span><span class="sxs-lookup"><span data-stu-id="c9c21-113">Get the sample code</span></span>
1. <span data-ttu-id="c9c21-114">Open a command line interface that can run Node.js and Git commands.</span><span class="sxs-lookup"><span data-stu-id="c9c21-114">Open a command line interface that can run Node.js and Git commands.</span></span>
2. <span data-ttu-id="c9c21-115">Navigate to a folder that you can use for a local Git repository, and clone the [GitHub repository containing the sample code](https://github.com/Azure-Samples/app-service-api-node-contact-list).</span><span class="sxs-lookup"><span data-stu-id="c9c21-115">Navigate to a folder that you can use for a local Git repository, and clone the [GitHub repository containing the sample code](https://github.com/Azure-Samples/app-service-api-node-contact-list).</span></span>
   
        git clone https://github.com/Azure-Samples/app-service-api-node-contact-list.git
   
    <span data-ttu-id="c9c21-116">The sample API provides two endpoints: a Get request to `/contacts` returns a list of names and email addresses in JSON format, while `/contacts/{id}` returns only the selected contact.</span><span class="sxs-lookup"><span data-stu-id="c9c21-116">The sample API provides two endpoints: a Get request to `/contacts` returns a list of names and email addresses in JSON format, while `/contacts/{id}` returns only the selected contact.</span></span>

## <a name="scaffold-auto-generate-nodejs-code-based-on-swagger-metadata"></a><span data-ttu-id="c9c21-117">Scaffold (auto-generate) Node.js code based on Swagger metadata</span><span class="sxs-lookup"><span data-stu-id="c9c21-117">Scaffold (auto-generate) Node.js code based on Swagger metadata</span></span>
<span data-ttu-id="c9c21-118">[Swagger](http://swagger.io/) is a file format for metadata that describes a RESTful API.</span><span class="sxs-lookup"><span data-stu-id="c9c21-118">[Swagger](http://swagger.io/) is a file format for metadata that describes a RESTful API.</span></span> <span data-ttu-id="c9c21-119">Azure App Service has [built-in support for Swagger metadata](app-service-api-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="c9c21-119">Azure App Service has [built-in support for Swagger metadata](app-service-api-metadata.md).</span></span> <span data-ttu-id="c9c21-120">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span><span class="sxs-lookup"><span data-stu-id="c9c21-120">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

> [!NOTE]
> <span data-ttu-id="c9c21-121">You can skip this section if you don't want to learn how to scaffold Node.js code from a Swagger metadata file.</span><span class="sxs-lookup"><span data-stu-id="c9c21-121">You can skip this section if you don't want to learn how to scaffold Node.js code from a Swagger metadata file.</span></span> <span data-ttu-id="c9c21-122">If you want to just deploy sample code to a new API app, go directly to the [Create an API app in Azure](#createapiapp) section.</span><span class="sxs-lookup"><span data-stu-id="c9c21-122">If you want to just deploy sample code to a new API app, go directly to the [Create an API app in Azure](#createapiapp) section.</span></span>
> 
> 

### <a name="install-and-execute-swaggerize"></a><span data-ttu-id="c9c21-123">Install and execute Swaggerize</span><span class="sxs-lookup"><span data-stu-id="c9c21-123">Install and execute Swaggerize</span></span>
1. <span data-ttu-id="c9c21-124">Execute the following commands to install the **yo** and **generator-swaggerize** NPM modules globally.</span><span class="sxs-lookup"><span data-stu-id="c9c21-124">Execute the following commands to install the **yo** and **generator-swaggerize** NPM modules globally.</span></span>
   
        npm install -g yo
        npm install -g generator-swaggerize
   
    <span data-ttu-id="c9c21-125">Swaggerize is a tool that generates server code for an API described by a Swagger metadata file.</span><span class="sxs-lookup"><span data-stu-id="c9c21-125">Swaggerize is a tool that generates server code for an API described by a Swagger metadata file.</span></span> <span data-ttu-id="c9c21-126">The Swagger file that you'll use is named *api.json* and is located in the *start* folder of the repository you cloned.</span><span class="sxs-lookup"><span data-stu-id="c9c21-126">The Swagger file that you'll use is named *api.json* and is located in the *start* folder of the repository you cloned.</span></span>
2. <span data-ttu-id="c9c21-127">Navigate to the *start* folder, and then execute the `yo swaggerize` command.</span><span class="sxs-lookup"><span data-stu-id="c9c21-127">Navigate to the *start* folder, and then execute the `yo swaggerize` command.</span></span> <span data-ttu-id="c9c21-128">Swaggerize will ask a series of questions.</span><span class="sxs-lookup"><span data-stu-id="c9c21-128">Swaggerize will ask a series of questions.</span></span>  <span data-ttu-id="c9c21-129">For **what to call this project**, enter "ContactList", for **path to swagger document**, enter "api.json", and for **Express, Hapi, or Restify**, enter "express".</span><span class="sxs-lookup"><span data-stu-id="c9c21-129">For **what to call this project**, enter "ContactList", for **path to swagger document**, enter "api.json", and for **Express, Hapi, or Restify**, enter "express".</span></span>
   
        yo swaggerize
   
    ![Swaggerize Command Line](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/swaggerize-command-line.png)
   
    <span data-ttu-id="c9c21-131">**Note**: if you encounter an error in this step, the next step explains how to fix it.</span><span class="sxs-lookup"><span data-stu-id="c9c21-131">**Note**: if you encounter an error in this step, the next step explains how to fix it.</span></span>
   
    <span data-ttu-id="c9c21-132">Swaggerize creates an application folder, scaffolds handlers and configuration files, and generates a **package.json** file.</span><span class="sxs-lookup"><span data-stu-id="c9c21-132">Swaggerize creates an application folder, scaffolds handlers and configuration files, and generates a **package.json** file.</span></span> <span data-ttu-id="c9c21-133">The express view engine is used to generate the Swagger help page.</span><span class="sxs-lookup"><span data-stu-id="c9c21-133">The express view engine is used to generate the Swagger help page.</span></span>  
3. <span data-ttu-id="c9c21-134">If the `swaggerize` command fails with an "unexpected token" or "invalid escape sequence" error, correct the cause of the error by editing the generated *package.json* file.</span><span class="sxs-lookup"><span data-stu-id="c9c21-134">If the `swaggerize` command fails with an "unexpected token" or "invalid escape sequence" error, correct the cause of the error by editing the generated *package.json* file.</span></span> <span data-ttu-id="c9c21-135">In the `regenerate` line under `scripts`, change the back slash that precedes *api.json* to a forward slash, so that the line looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="c9c21-135">In the `regenerate` line under `scripts`, change the back slash that precedes *api.json* to a forward slash, so that the line looks like the following example:</span></span>
   
         "regenerate": "yo swaggerize --only=handlers,models,tests --framework express --apiPath config/api.json"
4. <span data-ttu-id="c9c21-136">Navigate to the folder that contains the scaffolded code (in this case, the */start/ContactList* subfolder).</span><span class="sxs-lookup"><span data-stu-id="c9c21-136">Navigate to the folder that contains the scaffolded code (in this case, the */start/ContactList* subfolder).</span></span>
5. <span data-ttu-id="c9c21-137">Run `npm install`.</span><span class="sxs-lookup"><span data-stu-id="c9c21-137">Run `npm install`.</span></span>
   
        npm install
6. <span data-ttu-id="c9c21-138">Install the **jsonpath** NPM module.</span><span class="sxs-lookup"><span data-stu-id="c9c21-138">Install the **jsonpath** NPM module.</span></span> 
   
        npm install --save jsonpath
   
    ![Jsonpath Install](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/jsonpath-install.png)
7. <span data-ttu-id="c9c21-140">Install the **swaggerize-ui** NPM module.</span><span class="sxs-lookup"><span data-stu-id="c9c21-140">Install the **swaggerize-ui** NPM module.</span></span> 
   
        npm install --save swaggerize-ui
   
    ![Swaggerize Ui Install](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/swaggerize-ui-install.png)

### <a name="customize-the-scaffolded-code"></a><span data-ttu-id="c9c21-142">Customize the scaffolded code</span><span class="sxs-lookup"><span data-stu-id="c9c21-142">Customize the scaffolded code</span></span>
1. <span data-ttu-id="c9c21-143">Copy the **lib** folder from the **start** folder into the **ContactList** folder created by the scaffolder.</span><span class="sxs-lookup"><span data-stu-id="c9c21-143">Copy the **lib** folder from the **start** folder into the **ContactList** folder created by the scaffolder.</span></span> 
2. <span data-ttu-id="c9c21-144">Replace the code in the **handlers/contacts.js** file with the following code.</span><span class="sxs-lookup"><span data-stu-id="c9c21-144">Replace the code in the **handlers/contacts.js** file with the following code.</span></span> 
   
    <span data-ttu-id="c9c21-145">This code uses the JSON data stored in the **lib/contacts.json** file that is served by **lib/contactRepository.js**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-145">This code uses the JSON data stored in the **lib/contacts.json** file that is served by **lib/contactRepository.js**.</span></span> <span data-ttu-id="c9c21-146">The new contacts.js code responds to HTTP requests to get all of the contacts and return them as a JSON payload.</span><span class="sxs-lookup"><span data-stu-id="c9c21-146">The new contacts.js code responds to HTTP requests to get all of the contacts and return them as a JSON payload.</span></span> 
   
        'use strict';
   
        var repository = require('../lib/contactRepository');
   
        module.exports = {
            get: function contacts_get(req, res) {
                res.json(repository.all())
            }
        };
3. <span data-ttu-id="c9c21-147">Replace the code in the **handlers/contacts/{id}.js** file with the following code.</span><span class="sxs-lookup"><span data-stu-id="c9c21-147">Replace the code in the **handlers/contacts/{id}.js** file with the following code.</span></span> 
   
        'use strict';
   
        var repository = require('../../lib/contactRepository');
   
        module.exports = {
            get: function contacts_get(req, res) {
                res.json(repository.get(req.params['id']));
            }    
        };
4. <span data-ttu-id="c9c21-148">Replace the code in **server.js** with the following code.</span><span class="sxs-lookup"><span data-stu-id="c9c21-148">Replace the code in **server.js** with the following code.</span></span> 
   
    <span data-ttu-id="c9c21-149">The changes made to the server.js file are called out by using comments so you can see the changes being made.</span><span class="sxs-lookup"><span data-stu-id="c9c21-149">The changes made to the server.js file are called out by using comments so you can see the changes being made.</span></span> 
   
        'use strict';
   
        var port = process.env.PORT || 8000; // first change
   
        var http = require('http');
        var express = require('express');
        var bodyParser = require('body-parser');
        var swaggerize = require('swaggerize-express');
        var swaggerUi = require('swaggerize-ui'); // second change
        var path = require('path');
   
        var app = express();
   
        var server = http.createServer(app);
   
        app.use(bodyParser.json());
   
        app.use(swaggerize({
            api: path.resolve('./config/swagger.json'), // third change
            handlers: path.resolve('./handlers'),
            docspath: '/swagger' // fourth change
        }));
   
        // change four
        app.use('/docs', swaggerUi({
          docs: '/swagger'  
        }));
   
        server.listen(port, function () { // fifth and final change
        });

### <a name="test-with-the-api-running-locally"></a><span data-ttu-id="c9c21-150">Test with the API running locally</span><span class="sxs-lookup"><span data-stu-id="c9c21-150">Test with the API running locally</span></span>
1. <span data-ttu-id="c9c21-151">Activate the server using the Node.js command-line executable.</span><span class="sxs-lookup"><span data-stu-id="c9c21-151">Activate the server using the Node.js command-line executable.</span></span> 
   
        node server.js
2. <span data-ttu-id="c9c21-152">When you browse to **http://localhost:8000/contacts**, you see the JSON output of the contact list (or you're prompted to download it, depending on your browser).</span><span class="sxs-lookup"><span data-stu-id="c9c21-152">When you browse to **http://localhost:8000/contacts**, you see the JSON output of the contact list (or you're prompted to download it, depending on your browser).</span></span> 
   
    ![All Contacts Api Call](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/all-contacts-api-call.png)
3. <span data-ttu-id="c9c21-154">When you browse to **http://localhost:8000/contacts/2**, you'll see the contact represented by that id value.</span><span class="sxs-lookup"><span data-stu-id="c9c21-154">When you browse to **http://localhost:8000/contacts/2**, you'll see the contact represented by that id value.</span></span>
   
    ![Specific Contact Api Call](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/specific-contact-api-call.png)
4. <span data-ttu-id="c9c21-156">The Swagger JSON data is served via the **/swagger** endpoint:</span><span class="sxs-lookup"><span data-stu-id="c9c21-156">The Swagger JSON data is served via the **/swagger** endpoint:</span></span>
   
    ![Contacts Swagger Json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/contacts-swagger-json.png)
5. <span data-ttu-id="c9c21-158">The Swagger UI is served via the **/docs** endpoint.</span><span class="sxs-lookup"><span data-stu-id="c9c21-158">The Swagger UI is served via the **/docs** endpoint.</span></span> <span data-ttu-id="c9c21-159">In the Swagger UI, you can use the rich HTML client features to test out your API.</span><span class="sxs-lookup"><span data-stu-id="c9c21-159">In the Swagger UI, you can use the rich HTML client features to test out your API.</span></span>
   
    ![Swagger Ui](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> <span data-ttu-id="c9c21-161">Create a new API App</span><span class="sxs-lookup"><span data-stu-id="c9c21-161">Create a new API App</span></span>
<span data-ttu-id="c9c21-162">In this section you use the Azure portal to create a new API App in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c21-162">In this section you use the Azure portal to create a new API App in Azure.</span></span> <span data-ttu-id="c9c21-163">This API app represents the compute resources that Azure will provide to run your code.</span><span class="sxs-lookup"><span data-stu-id="c9c21-163">This API app represents the compute resources that Azure will provide to run your code.</span></span> <span data-ttu-id="c9c21-164">In later sections you'll deploy your code to the new API app.</span><span class="sxs-lookup"><span data-stu-id="c9c21-164">In later sections you'll deploy your code to the new API app.</span></span>

1. <span data-ttu-id="c9c21-165">Browse to the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c9c21-165">Browse to the [Azure Portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="c9c21-166">Click **New > Web + Mobile > API App**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-166">Click **New > Web + Mobile > API App**.</span></span> 
   
    ![New API app in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/new-api-app-portal.png)
3. <span data-ttu-id="c9c21-168">Enter an **App name** that is unique in the *azurewebsites.net* domain, such as NodejsAPIApp plus a number to make it unique.</span><span class="sxs-lookup"><span data-stu-id="c9c21-168">Enter an **App name** that is unique in the *azurewebsites.net* domain, such as NodejsAPIApp plus a number to make it unique.</span></span> 
   
    <span data-ttu-id="c9c21-169">For example, if the name is `NodejsAPIApp`, the URL will be `nodejsapiapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c9c21-169">For example, if the name is `NodejsAPIApp`, the URL will be `nodejsapiapp.azurewebsites.net`.</span></span>
   
    <span data-ttu-id="c9c21-170">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span><span class="sxs-lookup"><span data-stu-id="c9c21-170">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
4. <span data-ttu-id="c9c21-171">In the **Resource Group** drop-down, click **New**, and then in **New resource group name** enter "NodejsAPIAppGroup" or another name if you prefer.</span><span class="sxs-lookup"><span data-stu-id="c9c21-171">In the **Resource Group** drop-down, click **New**, and then in **New resource group name** enter "NodejsAPIAppGroup" or another name if you prefer.</span></span> 
   
    <span data-ttu-id="c9c21-172">A [resource group](../azure-resource-manager/resource-group-overview.md) is a collection of Azure resources such as API apps, databases, and VMs.</span><span class="sxs-lookup"><span data-stu-id="c9c21-172">A [resource group](../azure-resource-manager/resource-group-overview.md) is a collection of Azure resources such as API apps, databases, and VMs.</span></span> <span data-ttu-id="c9c21-173">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c9c21-173">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
5. <span data-ttu-id="c9c21-174">Click **App Service plan/Location**, and then click **Create New**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-174">Click **App Service plan/Location**, and then click **Create New**.</span></span>
   
    ![Create App Service plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/newappserviceplan.png)
   
    <span data-ttu-id="c9c21-176">In the following steps, you create an App Service plan for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="c9c21-176">In the following steps, you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="c9c21-177">An App Service plan specifies the compute resources that your API app runs on.</span><span class="sxs-lookup"><span data-stu-id="c9c21-177">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="c9c21-178">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="c9c21-178">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="c9c21-179">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9c21-179">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
6. <span data-ttu-id="c9c21-180">In the **App Service Plan** blade, enter "NodejsAPIAppPlan" or another name if you prefer.</span><span class="sxs-lookup"><span data-stu-id="c9c21-180">In the **App Service Plan** blade, enter "NodejsAPIAppPlan" or another name if you prefer.</span></span>
7. <span data-ttu-id="c9c21-181">In the **Location** drop-down list, choose the location that is closest to you.</span><span class="sxs-lookup"><span data-stu-id="c9c21-181">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="c9c21-182">This setting specifies which Azure datacenter your app will run in.</span><span class="sxs-lookup"><span data-stu-id="c9c21-182">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="c9c21-183">For this tutorial, you can select any region and it won't make a noticeable difference.</span><span class="sxs-lookup"><span data-stu-id="c9c21-183">For this tutorial, you can select any region and it won't make a noticeable difference.</span></span> <span data-ttu-id="c9c21-184">But for a production app, you want your server to be as close as possible to the clients that are accessing it to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="c9c21-184">But for a production app, you want your server to be as close as possible to the clients that are accessing it to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
8. <span data-ttu-id="c9c21-185">Click **Pricing tier > View All > F1 Free**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-185">Click **Pricing tier > View All > F1 Free**.</span></span>
   
    <span data-ttu-id="c9c21-186">For this tutorial, the free pricing tier will provide sufficient performance.</span><span class="sxs-lookup"><span data-stu-id="c9c21-186">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
   
    ![Select Free pricing tier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/selectfreetier.png)
9. <span data-ttu-id="c9c21-188">In the **App Service Plan** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-188">In the **App Service Plan** blade, click **OK**.</span></span>
10. <span data-ttu-id="c9c21-189">In the **API App** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-189">In the **API App** blade, click **Create**.</span></span>

## <a name="set-up-your-new-api-app-for-git-deployment"></a><span data-ttu-id="c9c21-190">Set up your new API app for Git deployment</span><span class="sxs-lookup"><span data-stu-id="c9c21-190">Set up your new API app for Git deployment</span></span>
<span data-ttu-id="c9c21-191">You'll deploy your code to the API app by pushing commits to a Git repository in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c9c21-191">You'll deploy your code to the API app by pushing commits to a Git repository in Azure App Service.</span></span> <span data-ttu-id="c9c21-192">In this section of the tutorial, you create the credentials and Git repository in Azure that you'll use for deployment.</span><span class="sxs-lookup"><span data-stu-id="c9c21-192">In this section of the tutorial, you create the credentials and Git repository in Azure that you'll use for deployment.</span></span>  

1. <span data-ttu-id="c9c21-193">After your API app has been created, click **App Services > {your API app}** from the portal home page.</span><span class="sxs-lookup"><span data-stu-id="c9c21-193">After your API app has been created, click **App Services > {your API app}** from the portal home page.</span></span> 
   
    <span data-ttu-id="c9c21-194">The portal displays the **API App** and **Settings** blades.</span><span class="sxs-lookup"><span data-stu-id="c9c21-194">The portal displays the **API App** and **Settings** blades.</span></span>
   
    ![Portal API app and Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/portalapiappblade.png)
2. <span data-ttu-id="c9c21-196">In the **Settings** blade, scroll down to the **Publishing** section, and then click **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-196">In the **Settings** blade, scroll down to the **Publishing** section, and then click **Deployment credentials**.</span></span>
3. <span data-ttu-id="c9c21-197">In the **Set deployment credentials** blade, enter a user name and password, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-197">In the **Set deployment credentials** blade, enter a user name and password, and then click **Save**.</span></span>
   
    <span data-ttu-id="c9c21-198">You'll use these credentials for publishing your Node.js code to your API app.</span><span class="sxs-lookup"><span data-stu-id="c9c21-198">You'll use these credentials for publishing your Node.js code to your API app.</span></span> 
   
    ![Deployment Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/deployment-credentials.png)
4. <span data-ttu-id="c9c21-200">In the **Settings** blade, click **Deployment source > Choose Source > Local Git Repository**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9c21-200">In the **Settings** blade, click **Deployment source > Choose Source > Local Git Repository**, then click **OK**.</span></span>
   
    ![Create Git Repo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/create-git-repo.png)
5. <span data-ttu-id="c9c21-202">Once your Git repository has been created the blade changes to show you your active deployments.</span><span class="sxs-lookup"><span data-stu-id="c9c21-202">Once your Git repository has been created the blade changes to show you your active deployments.</span></span> <span data-ttu-id="c9c21-203">Since the repository is new, you have no active deployments in the list.</span><span class="sxs-lookup"><span data-stu-id="c9c21-203">Since the repository is new, you have no active deployments in the list.</span></span> 
   
    ![No Active Deployments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/no-active-deployments.png)
6. <span data-ttu-id="c9c21-205">Copy the Git repository URL.</span><span class="sxs-lookup"><span data-stu-id="c9c21-205">Copy the Git repository URL.</span></span> <span data-ttu-id="c9c21-206">To do this, navigate to the blade for your new API App and look at the **Essentials** section of the blade.</span><span class="sxs-lookup"><span data-stu-id="c9c21-206">To do this, navigate to the blade for your new API App and look at the **Essentials** section of the blade.</span></span> <span data-ttu-id="c9c21-207">Notice the **Git clone URL** in the **Essentials** section.</span><span class="sxs-lookup"><span data-stu-id="c9c21-207">Notice the **Git clone URL** in the **Essentials** section.</span></span> <span data-ttu-id="c9c21-208">When you hover over this URL, you see an icon on the right that will copy the URL to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="c9c21-208">When you hover over this URL, you see an icon on the right that will copy the URL to your clipboard.</span></span> <span data-ttu-id="c9c21-209">Click this icon to copy the URL.</span><span class="sxs-lookup"><span data-stu-id="c9c21-209">Click this icon to copy the URL.</span></span>
   
    ![Get The Git Url From The Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/get-the-git-url-from-the-portal.png)
   
    <span data-ttu-id="c9c21-211">**Note**: You will need the Git clone URL in the next section so make sure to save it somewhere for the moment.</span><span class="sxs-lookup"><span data-stu-id="c9c21-211">**Note**: You will need the Git clone URL in the next section so make sure to save it somewhere for the moment.</span></span>

<span data-ttu-id="c9c21-212">Now that you have an API App with a Git repository backing it up, you can push code into the repository to deploy the code to the API app.</span><span class="sxs-lookup"><span data-stu-id="c9c21-212">Now that you have an API App with a Git repository backing it up, you can push code into the repository to deploy the code to the API app.</span></span> 

## <a name="deploy-your-api-code-to-azure"></a><span data-ttu-id="c9c21-213">Deploy your API code to Azure</span><span class="sxs-lookup"><span data-stu-id="c9c21-213">Deploy your API code to Azure</span></span>
<span data-ttu-id="c9c21-214">In this section you create a local Git repository that contains your server code for the API, and then you push your code from that repository to the repository in Azure that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="c9c21-214">In this section you create a local Git repository that contains your server code for the API, and then you push your code from that repository to the repository in Azure that you created earlier.</span></span>

1. <span data-ttu-id="c9c21-215">Copy the `ContactList` folder to a location that you can use for a new local Git repository.</span><span class="sxs-lookup"><span data-stu-id="c9c21-215">Copy the `ContactList` folder to a location that you can use for a new local Git repository.</span></span> <span data-ttu-id="c9c21-216">If you did the first part of the tutorial, copy `ContactList` from the `start` folder; otherwise, copy `ContactList` from the `end` folder.</span><span class="sxs-lookup"><span data-stu-id="c9c21-216">If you did the first part of the tutorial, copy `ContactList` from the `start` folder; otherwise, copy `ContactList` from the `end` folder.</span></span>
2. <span data-ttu-id="c9c21-217">In your command line tool, navigate to the new folder, then execute the following command to create a new local Git repository.</span><span class="sxs-lookup"><span data-stu-id="c9c21-217">In your command line tool, navigate to the new folder, then execute the following command to create a new local Git repository.</span></span> 
   
        git init
   
     ![New Local Git Repo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/new-local-git-repo.png)
3. <span data-ttu-id="c9c21-219">If you did the first part of this tutorial and copied the `ContactList` folder, the copy likely included the `node_modules` folder.</span><span class="sxs-lookup"><span data-stu-id="c9c21-219">If you did the first part of this tutorial and copied the `ContactList` folder, the copy likely included the `node_modules` folder.</span></span> <span data-ttu-id="c9c21-220">You do not want to include the `node_modules` folder in source control as it is created for you during the deployment process via the `package.json` file and `npm install`.</span><span class="sxs-lookup"><span data-stu-id="c9c21-220">You do not want to include the `node_modules` folder in source control as it is created for you during the deployment process via the `package.json` file and `npm install`.</span></span> <span data-ttu-id="c9c21-221">Thus, add a `.gitignore` file by running the following command in the root of your project directory.</span><span class="sxs-lookup"><span data-stu-id="c9c21-221">Thus, add a `.gitignore` file by running the following command in the root of your project directory.</span></span>

         touch .gitignore
      
   <span data-ttu-id="c9c21-222">Open the .gitignore file and add `node_modules` to the first line of the file.</span><span class="sxs-lookup"><span data-stu-id="c9c21-222">Open the .gitignore file and add `node_modules` to the first line of the file.</span></span> <span data-ttu-id="c9c21-223">You can confirm the `node_modules` folder is being ignored by source control if you run `git status` and do not see the directory in the list.</span><span class="sxs-lookup"><span data-stu-id="c9c21-223">You can confirm the `node_modules` folder is being ignored by source control if you run `git status` and do not see the directory in the list.</span></span> <span data-ttu-id="c9c21-224">There is a (GitHub project)[https://github.com/github/gitignore/blob/master/Node.gitignore] for recommended files to ignore in a NodeJS project if you want to add more rules.</span><span class="sxs-lookup"><span data-stu-id="c9c21-224">There is a (GitHub project)[https://github.com/github/gitignore/blob/master/Node.gitignore] for recommended files to ignore in a NodeJS project if you want to add more rules.</span></span>
 
4. <span data-ttu-id="c9c21-225">Execute the following command to add a Git remote for your API app's repository.</span><span class="sxs-lookup"><span data-stu-id="c9c21-225">Execute the following command to add a Git remote for your API app's repository.</span></span> 
   
        git remote add azure YOUR_GIT_CLONE_URL_HERE
   
    <span data-ttu-id="c9c21-226">**Note**: Replace the string "YOUR_GIT_CLONE_URL_HERE" with your own Git clone URL that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="c9c21-226">**Note**: Replace the string "YOUR_GIT_CLONE_URL_HERE" with your own Git clone URL that you copied earlier.</span></span> 
5. <span data-ttu-id="c9c21-227">Execute the following commands to create a commit that contains all of your code.</span><span class="sxs-lookup"><span data-stu-id="c9c21-227">Execute the following commands to create a commit that contains all of your code.</span></span> 
   
        git add .
        git commit -m "initial revision"
   
    ![Git Commit Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/git-commit-output.png)
6. <span data-ttu-id="c9c21-229">Execute the command to push your code to Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c21-229">Execute the command to push your code to Azure.</span></span> <span data-ttu-id="c9c21-230">When you're prompted for a password, enter the one that you created earlier in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c9c21-230">When you're prompted for a password, enter the one that you created earlier in the Azure portal.</span></span>
   
        git push azure master
   
    <span data-ttu-id="c9c21-231">This triggers a deployment to your API app.</span><span class="sxs-lookup"><span data-stu-id="c9c21-231">This triggers a deployment to your API app.</span></span>  
7. <span data-ttu-id="c9c21-232">In your browser, navigate back to the **Deployments** blade for your API app, and you see that the deployment is occurring.</span><span class="sxs-lookup"><span data-stu-id="c9c21-232">In your browser, navigate back to the **Deployments** blade for your API app, and you see that the deployment is occurring.</span></span> 
   
    ![Deployment Happening](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/deployment-happening.png)
   
    <span data-ttu-id="c9c21-234">Simultaneously, the command line interface reflects the status of your deployment while it is happening.</span><span class="sxs-lookup"><span data-stu-id="c9c21-234">Simultaneously, the command line interface reflects the status of your deployment while it is happening.</span></span> 
   
    ![Node Js Deployment Happening](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/node-js-deployment-happening.png)
   
    <span data-ttu-id="c9c21-236">Once the deployment has completed, the **Deployments** blade reflects the successful deployment of your code changes to your API App.</span><span class="sxs-lookup"><span data-stu-id="c9c21-236">Once the deployment has completed, the **Deployments** blade reflects the successful deployment of your code changes to your API App.</span></span> 

## <a name="test-with-the-api-running-in-azure"></a><span data-ttu-id="c9c21-237">Test with the API running in Azure</span><span class="sxs-lookup"><span data-stu-id="c9c21-237">Test with the API running in Azure</span></span>
1. <span data-ttu-id="c9c21-238">Copy the **URL** in the **Essentials** section of your API App blade.</span><span class="sxs-lookup"><span data-stu-id="c9c21-238">Copy the **URL** in the **Essentials** section of your API App blade.</span></span> 
   
    ![Deployment Completed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/deployment-completed.png)
2. <span data-ttu-id="c9c21-240">Using a REST API client such as Postman or Fiddler (or your web browser), provide the URL of your contacts API call, which is the `/contacts` endpoint of your API app.</span><span class="sxs-lookup"><span data-stu-id="c9c21-240">Using a REST API client such as Postman or Fiddler (or your web browser), provide the URL of your contacts API call, which is the `/contacts` endpoint of your API app.</span></span> <span data-ttu-id="c9c21-241">The URL will be `https://{your API app name}.azurewebsites.net/contacts`</span><span class="sxs-lookup"><span data-stu-id="c9c21-241">The URL will be `https://{your API app name}.azurewebsites.net/contacts`</span></span>
   
    <span data-ttu-id="c9c21-242">When you issue a GET request to this endpoint, you get the JSON output of your API app.</span><span class="sxs-lookup"><span data-stu-id="c9c21-242">When you issue a GET request to this endpoint, you get the JSON output of your API app.</span></span>
   
    ![Postman Hitting Api](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-nodejs-api-app/postman-hitting-api.png)
3. <span data-ttu-id="c9c21-244">In a browser, go to the `/docs` endpoint to try out the Swagger UI as it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c21-244">In a browser, go to the `/docs` endpoint to try out the Swagger UI as it runs in Azure.</span></span>

<span data-ttu-id="c9c21-245">Now that you have continuous delivery wired up, you can make code changes and deploy them to Azure simply by pushing commits to your Azure Git repository.</span><span class="sxs-lookup"><span data-stu-id="c9c21-245">Now that you have continuous delivery wired up, you can make code changes and deploy them to Azure simply by pushing commits to your Azure Git repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c21-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9c21-246">Next steps</span></span>
<span data-ttu-id="c9c21-247">At this point you've successfully created an API App and deployed Node.js API code to it.</span><span class="sxs-lookup"><span data-stu-id="c9c21-247">At this point you've successfully created an API App and deployed Node.js API code to it.</span></span> <span data-ttu-id="c9c21-248">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="c9c21-248">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS](app-service-api-cors-consume-javascript.md).</span></span>






















