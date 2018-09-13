---
title: How to work with the Node.js backend server SDK for Mobile Apps | Microsoft Docs
description: Learn how to work with the Node.js backend server SDK for Azure App Service Mobile Apps.
services: app-service\mobile
documentationcenter: ''
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 15527e58090fbde202509b0b1c208d09a2241b7d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553124"
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="e4188-103">How to use the Azure Mobile Apps Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="e4188-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="e4188-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="e4188-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <a name="Introduction"></a><span data-ttu-id="e4188-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="e4188-105">Introduction</span></span>
<span data-ttu-id="e4188-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span><span class="sxs-lookup"><span data-stu-id="e4188-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="e4188-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span><span class="sxs-lookup"><span data-stu-id="e4188-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="e4188-108">The SDK provides the following operations:</span><span class="sxs-lookup"><span data-stu-id="e4188-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="e4188-109">Table operations (Read, Insert, Update, Delete) for data access</span><span class="sxs-lookup"><span data-stu-id="e4188-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="e4188-110">Custom API operations</span><span class="sxs-lookup"><span data-stu-id="e4188-110">Custom API operations</span></span>

<span data-ttu-id="e4188-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span><span class="sxs-lookup"><span data-stu-id="e4188-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="e4188-112">You can find samples for each use case in the [samples directory on GitHub].</span><span class="sxs-lookup"><span data-stu-id="e4188-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="e4188-113">Supported Platforms</span><span class="sxs-lookup"><span data-stu-id="e4188-113">Supported Platforms</span></span>
<span data-ttu-id="e4188-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span><span class="sxs-lookup"><span data-stu-id="e4188-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="e4188-115">As of writing, the latest LTS version is Node v4.5.0.</span><span class="sxs-lookup"><span data-stu-id="e4188-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="e4188-116">Other versions of Node may work, but are not supported.</span><span class="sxs-lookup"><span data-stu-id="e4188-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="e4188-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span><span class="sxs-lookup"><span data-stu-id="e4188-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="e4188-118">The sqlite3 driver supports SQLite databases on a single instance only.</span><span class="sxs-lookup"><span data-stu-id="e4188-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <a name="howto-cmdline-basicapp"></a><span data-ttu-id="e4188-119">How to: Create a Basic Node.js backend using the Command Line</span><span class="sxs-lookup"><span data-stu-id="e4188-119">How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="e4188-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span><span class="sxs-lookup"><span data-stu-id="e4188-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="e4188-121">ExpressJS is the most popular web service framework available for Node.js.</span><span class="sxs-lookup"><span data-stu-id="e4188-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="e4188-122">You can create a basic [Express] application as follows:</span><span class="sxs-lookup"><span data-stu-id="e4188-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="e4188-123">In a command or PowerShell window, create a directory for your project.</span><span class="sxs-lookup"><span data-stu-id="e4188-123">In a command or PowerShell window, create a directory for your project.</span></span>
   
        mkdir basicapp
2. <span data-ttu-id="e4188-124">Run npm init to initialize the package structure.</span><span class="sxs-lookup"><span data-stu-id="e4188-124">Run npm init to initialize the package structure.</span></span>
   
        cd basicapp
        npm init
   
    <span data-ttu-id="e4188-125">The npm init command asks a set of questions to initialize the project.</span><span class="sxs-lookup"><span data-stu-id="e4188-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="e4188-126">See the example output:</span><span class="sxs-lookup"><span data-stu-id="e4188-126">See the example output:</span></span>
   
    ![The npm init output][0]
3. <span data-ttu-id="e4188-128">Install the express and azure-mobile-apps libraries from the npm repository.</span><span class="sxs-lookup"><span data-stu-id="e4188-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>
   
        npm install --save express azure-mobile-apps
4. <span data-ttu-id="e4188-129">Create an app.js file to implement the basic mobile server.</span><span class="sxs-lookup"><span data-stu-id="e4188-129">Create an app.js file to implement the basic mobile server.</span></span>
   
        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');
   
        var app = express(),
            mobile = azureMobileApps();
   
        // Define a TodoItem table
        mobile.tables.add('TodoItem');
   
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);
   
        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="e4188-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span><span class="sxs-lookup"><span data-stu-id="e4188-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="e4188-131">It is suitable for following the client library quick starts:</span><span class="sxs-lookup"><span data-stu-id="e4188-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="e4188-132">[Android Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="e4188-133">[Apache Cordova Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="e4188-134">[iOS Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="e4188-135">[Windows Store Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="e4188-136">[Xamarin.iOS Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="e4188-137">[Xamarin.Android Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="e4188-138">[Xamarin.Forms Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="e4188-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="e4188-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span><span class="sxs-lookup"><span data-stu-id="e4188-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <a name="howto-vs2015-basicapp"></a><span data-ttu-id="e4188-140">How to: Create a Node backend with Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e4188-140">How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="e4188-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span><span class="sxs-lookup"><span data-stu-id="e4188-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="e4188-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e4188-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="e4188-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span><span class="sxs-lookup"><span data-stu-id="e4188-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="e4188-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span><span class="sxs-lookup"><span data-stu-id="e4188-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="e4188-145">Expand **Templates** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="e4188-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="e4188-146">Select the **Basic Azure Node.js Express 4 Application**.</span><span class="sxs-lookup"><span data-stu-id="e4188-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="e4188-147">Fill in the project name.</span><span class="sxs-lookup"><span data-stu-id="e4188-147">Fill in the project name.</span></span>  <span data-ttu-id="e4188-148">Click *OK*.</span><span class="sxs-lookup"><span data-stu-id="e4188-148">Click *OK*.</span></span>
   
    ![Visual Studio 2015 New Project][1]
5. <span data-ttu-id="e4188-150">Right-click the **npm** node and select **Install New npm packages...**.</span><span class="sxs-lookup"><span data-stu-id="e4188-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="e4188-151">You may need to refresh the npm catalog on creating your first Node.js application.</span><span class="sxs-lookup"><span data-stu-id="e4188-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="e4188-152">Click **Refresh** if necessary.</span><span class="sxs-lookup"><span data-stu-id="e4188-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="e4188-153">Enter *azure-mobile-apps* in the search box.</span><span class="sxs-lookup"><span data-stu-id="e4188-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="e4188-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span><span class="sxs-lookup"><span data-stu-id="e4188-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>
   
    ![Install New npm packages][2]
8. <span data-ttu-id="e4188-156">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="e4188-156">Click **Close**.</span></span>
9. <span data-ttu-id="e4188-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="e4188-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="e4188-158">At line 6 at the bottom of the library require statements, add the following code:</span><span class="sxs-lookup"><span data-stu-id="e4188-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>
   
        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');
   
    <span data-ttu-id="e4188-159">At approximately line 27 after the other app.use statements, add the following code:</span><span class="sxs-lookup"><span data-stu-id="e4188-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>
   
        app.use('/users', users);
   
        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);
   
    <span data-ttu-id="e4188-160">Save the file.</span><span class="sxs-lookup"><span data-stu-id="e4188-160">Save the file.</span></span>
10. <span data-ttu-id="e4188-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span><span class="sxs-lookup"><span data-stu-id="e4188-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <a name="create-node-backend-portal"></a><span data-ttu-id="e4188-162">How to: Create a Node.js backend using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4188-162">How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="e4188-163">You can create a Mobile App backend right in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="e4188-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="e4188-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="e4188-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span><span class="sxs-lookup"><span data-stu-id="e4188-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="e4188-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span><span class="sxs-lookup"><span data-stu-id="e4188-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span> <span data-ttu-id="e4188-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span><span class="sxs-lookup"><span data-stu-id="e4188-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <a name="download-quickstart"></a><span data-ttu-id="e4188-168">How to: Download the Node.js backend quickstart code project using Git</span><span class="sxs-lookup"><span data-stu-id="e4188-168">How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="e4188-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span><span class="sxs-lookup"><span data-stu-id="e4188-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="e4188-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span><span class="sxs-lookup"><span data-stu-id="e4188-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="e4188-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span><span class="sxs-lookup"><span data-stu-id="e4188-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="e4188-172">For more information, see the [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="e4188-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="e4188-173">the following procedure uses a Git repository to download the quickstart project code.</span><span class="sxs-lookup"><span data-stu-id="e4188-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="e4188-174">Install Git, if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="e4188-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="e4188-175">The steps required to install Git vary between operating systems.</span><span class="sxs-lookup"><span data-stu-id="e4188-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="e4188-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span><span class="sxs-lookup"><span data-stu-id="e4188-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="e4188-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span><span class="sxs-lookup"><span data-stu-id="e4188-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="e4188-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span><span class="sxs-lookup"><span data-stu-id="e4188-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="e4188-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="e4188-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>
   
        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="e4188-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span><span class="sxs-lookup"><span data-stu-id="e4188-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="e4188-181">Locate the `todoitem.json` file in the `/tables` directory.</span><span class="sxs-lookup"><span data-stu-id="e4188-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="e4188-182">This file defines permissions on the table.</span><span class="sxs-lookup"><span data-stu-id="e4188-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="e4188-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span><span class="sxs-lookup"><span data-stu-id="e4188-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="e4188-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span><span class="sxs-lookup"><span data-stu-id="e4188-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>
   
        $ git commit -m "updated the table script"
        $ git push origin master
   
    <span data-ttu-id="e4188-185">When you add new files to the project, you first need to execute the `git add .` command.</span><span class="sxs-lookup"><span data-stu-id="e4188-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="e4188-186">The site is republished every time a new set of commits is pushed to the site.</span><span class="sxs-lookup"><span data-stu-id="e4188-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <a name="howto-publish-to-azure"></a><span data-ttu-id="e4188-187">How to: Publish your Node.js backend to Azure</span><span class="sxs-lookup"><span data-stu-id="e4188-187">How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="e4188-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span><span class="sxs-lookup"><span data-stu-id="e4188-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="e4188-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span><span class="sxs-lookup"><span data-stu-id="e4188-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="e4188-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="e4188-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="e4188-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span><span class="sxs-lookup"><span data-stu-id="e4188-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="e4188-192">How to [specify the Node Version]</span><span class="sxs-lookup"><span data-stu-id="e4188-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="e4188-193">How to [use Node modules]</span><span class="sxs-lookup"><span data-stu-id="e4188-193">How to [use Node modules]</span></span>

### <a name="howto-enable-homepage"></a><span data-ttu-id="e4188-194">How to: Enable a Home Page for your application</span><span class="sxs-lookup"><span data-stu-id="e4188-194">How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="e4188-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span><span class="sxs-lookup"><span data-stu-id="e4188-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="e4188-196">Sometimes, however, you may wish to only implement a mobile interface.</span><span class="sxs-lookup"><span data-stu-id="e4188-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="e4188-197">It is useful to provide a landing page to ensure the app service is up and running.</span><span class="sxs-lookup"><span data-stu-id="e4188-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="e4188-198">You can either provide your own home page or enable a temporary home page.</span><span class="sxs-lookup"><span data-stu-id="e4188-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="e4188-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="e4188-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="e4188-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span><span class="sxs-lookup"><span data-stu-id="e4188-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <a name="TableOperations"></a><span data-ttu-id="e4188-201">Table operations</span><span class="sxs-lookup"><span data-stu-id="e4188-201">Table operations</span></span>
<span data-ttu-id="e4188-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span><span class="sxs-lookup"><span data-stu-id="e4188-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="e4188-203">Five operations are provided.</span><span class="sxs-lookup"><span data-stu-id="e4188-203">Five operations are provided.</span></span>

| <span data-ttu-id="e4188-204">Operation</span><span class="sxs-lookup"><span data-stu-id="e4188-204">Operation</span></span> | <span data-ttu-id="e4188-205">Description</span><span class="sxs-lookup"><span data-stu-id="e4188-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4188-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="e4188-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="e4188-207">Get all records in the table</span><span class="sxs-lookup"><span data-stu-id="e4188-207">Get all records in the table</span></span> |
| <span data-ttu-id="e4188-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="e4188-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="e4188-209">Get a specific record in the table</span><span class="sxs-lookup"><span data-stu-id="e4188-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="e4188-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="e4188-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="e4188-211">Create a record in the table</span><span class="sxs-lookup"><span data-stu-id="e4188-211">Create a record in the table</span></span> |
| <span data-ttu-id="e4188-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="e4188-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="e4188-213">Update a record in the table</span><span class="sxs-lookup"><span data-stu-id="e4188-213">Update a record in the table</span></span> |
| <span data-ttu-id="e4188-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="e4188-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="e4188-215">Delete a record in the table</span><span class="sxs-lookup"><span data-stu-id="e4188-215">Delete a record in the table</span></span> |

<span data-ttu-id="e4188-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span><span class="sxs-lookup"><span data-stu-id="e4188-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <a name="howto-dynamicschema"></a><span data-ttu-id="e4188-217">How to: Define tables using a dynamic schema</span><span class="sxs-lookup"><span data-stu-id="e4188-217">How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="e4188-218">Before a table can be used, it must be defined.</span><span class="sxs-lookup"><span data-stu-id="e4188-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="e4188-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span><span class="sxs-lookup"><span data-stu-id="e4188-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="e4188-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span><span class="sxs-lookup"><span data-stu-id="e4188-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="e4188-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span><span class="sxs-lookup"><span data-stu-id="e4188-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="e4188-222">Extending the basic-app, the app.js file would be adjusted:</span><span class="sxs-lookup"><span data-stu-id="e4188-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="e4188-223">Define the table in ./tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="e4188-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="e4188-224">Tables use dynamic schema by default.</span><span class="sxs-lookup"><span data-stu-id="e4188-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="e4188-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e4188-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="e4188-226">You can find a complete example in the [todo sample on GitHub].</span><span class="sxs-lookup"><span data-stu-id="e4188-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <a name="howto-staticschema"></a><span data-ttu-id="e4188-227">How to: Define tables using a static schema</span><span class="sxs-lookup"><span data-stu-id="e4188-227">How to: Define tables using a static schema</span></span>
<span data-ttu-id="e4188-228">You can explicitly define the columns to expose via the WebAPI.</span><span class="sxs-lookup"><span data-stu-id="e4188-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="e4188-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span><span class="sxs-lookup"><span data-stu-id="e4188-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="e4188-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span><span class="sxs-lookup"><span data-stu-id="e4188-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="e4188-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span><span class="sxs-lookup"><span data-stu-id="e4188-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="e4188-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span><span class="sxs-lookup"><span data-stu-id="e4188-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="e4188-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span><span class="sxs-lookup"><span data-stu-id="e4188-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <a name="howto-sqlexpress-setup"></a><span data-ttu-id="e4188-234">How to: Use SQL Express as a development data store on your local machine</span><span class="sxs-lookup"><span data-stu-id="e4188-234">How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="e4188-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span><span class="sxs-lookup"><span data-stu-id="e4188-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="e4188-236">Use the **memory** driver to provide a non-persistent example store</span><span class="sxs-lookup"><span data-stu-id="e4188-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="e4188-237">Use the **mssql** driver to provide a SQL Express data store for development</span><span class="sxs-lookup"><span data-stu-id="e4188-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="e4188-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span><span class="sxs-lookup"><span data-stu-id="e4188-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="e4188-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e4188-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="e4188-240">This package requires that you enable TCP connections on your SQL Express instance.</span><span class="sxs-lookup"><span data-stu-id="e4188-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="e4188-241">The memory driver does not provide a complete set of facilities for testing.</span><span class="sxs-lookup"><span data-stu-id="e4188-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="e4188-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span><span class="sxs-lookup"><span data-stu-id="e4188-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
> 
> 

1. <span data-ttu-id="e4188-243">Download and install [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="e4188-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="e4188-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span><span class="sxs-lookup"><span data-stu-id="e4188-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="e4188-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span><span class="sxs-lookup"><span data-stu-id="e4188-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="e4188-246">Run the SQL Server 2014 Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="e4188-246">Run the SQL Server 2014 Configuration Manager.</span></span>
   
   1. <span data-ttu-id="e4188-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span><span class="sxs-lookup"><span data-stu-id="e4188-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="e4188-248">Click **Protocols for SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="e4188-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="e4188-249">Right-click **TCP/IP** and select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="e4188-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="e4188-250">Click **OK** in the pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="e4188-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="e4188-251">Right-click **TCP/IP** and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="e4188-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="e4188-252">Click the **IP Addresses** tab.</span><span class="sxs-lookup"><span data-stu-id="e4188-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="e4188-253">Find the **IPAll** node.</span><span class="sxs-lookup"><span data-stu-id="e4188-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="e4188-254">In the **TCP Port** field, enter **1433**.</span><span class="sxs-lookup"><span data-stu-id="e4188-254">In the **TCP Port** field, enter **1433**.</span></span>
      
          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="e4188-255">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4188-255">Click **OK**.</span></span>  <span data-ttu-id="e4188-256">Click **OK** in the pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="e4188-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="e4188-257">Click **SQL Server Services** in the left-hand tree menu.</span><span class="sxs-lookup"><span data-stu-id="e4188-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="e4188-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span><span class="sxs-lookup"><span data-stu-id="e4188-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="e4188-259">Close the SQL Server 2014 Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="e4188-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="e4188-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span><span class="sxs-lookup"><span data-stu-id="e4188-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>
   
   1. <span data-ttu-id="e4188-261">Right-click your instance in the Object Explorer and select **Properties**</span><span class="sxs-lookup"><span data-stu-id="e4188-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="e4188-262">Select the **Security** page.</span><span class="sxs-lookup"><span data-stu-id="e4188-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="e4188-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span><span class="sxs-lookup"><span data-stu-id="e4188-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="e4188-264">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="e4188-264">Click **OK**</span></span>
      
          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="e4188-265">Expand **Security** > **Logins** in the Object Explorer</span><span class="sxs-lookup"><span data-stu-id="e4188-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="e4188-266">Right-click **Logins** and select **New Login...**</span><span class="sxs-lookup"><span data-stu-id="e4188-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="e4188-267">Enter a Login name.</span><span class="sxs-lookup"><span data-stu-id="e4188-267">Enter a Login name.</span></span>  <span data-ttu-id="e4188-268">Select **SQL Server authentication**.</span><span class="sxs-lookup"><span data-stu-id="e4188-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="e4188-269">Enter a Password, then enter the same password in **Confirm password**.</span><span class="sxs-lookup"><span data-stu-id="e4188-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="e4188-270">The password must meet Windows complexity requirements.</span><span class="sxs-lookup"><span data-stu-id="e4188-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="e4188-271">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="e4188-271">Click **OK**</span></span>
      
          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="e4188-272">Right-click your new login and select **Properties**</span><span class="sxs-lookup"><span data-stu-id="e4188-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="e4188-273">Select the **Server Roles** page</span><span class="sxs-lookup"><span data-stu-id="e4188-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="e4188-274">Check the box next to the **dbcreator** server role</span><span class="sxs-lookup"><span data-stu-id="e4188-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="e4188-275">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="e4188-275">Click **OK**</span></span>
   13. <span data-ttu-id="e4188-276">Close the SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="e4188-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="e4188-277">Ensure you record the username and password you selected.</span><span class="sxs-lookup"><span data-stu-id="e4188-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="e4188-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span><span class="sxs-lookup"><span data-stu-id="e4188-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="e4188-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span><span class="sxs-lookup"><span data-stu-id="e4188-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="e4188-280">You can set this variable within your environment.</span><span class="sxs-lookup"><span data-stu-id="e4188-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="e4188-281">For example, you can use PowerShell to set this environment variable:</span><span class="sxs-lookup"><span data-stu-id="e4188-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="e4188-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span><span class="sxs-lookup"><span data-stu-id="e4188-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <a name="howto-config-localdev"></a><span data-ttu-id="e4188-283">How to: Configure your project for local development</span><span class="sxs-lookup"><span data-stu-id="e4188-283">How to: Configure your project for local development</span></span>
<span data-ttu-id="e4188-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span><span class="sxs-lookup"><span data-stu-id="e4188-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="e4188-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span><span class="sxs-lookup"><span data-stu-id="e4188-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="e4188-286">The *azureMobile.js* file should export a configuration object.</span><span class="sxs-lookup"><span data-stu-id="e4188-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="e4188-287">The most common settings are:</span><span class="sxs-lookup"><span data-stu-id="e4188-287">The most common settings are:</span></span>

* <span data-ttu-id="e4188-288">Database Settings</span><span class="sxs-lookup"><span data-stu-id="e4188-288">Database Settings</span></span>
* <span data-ttu-id="e4188-289">Diagnostic Logging Settings</span><span class="sxs-lookup"><span data-stu-id="e4188-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="e4188-290">Alternate CORS Settings</span><span class="sxs-lookup"><span data-stu-id="e4188-290">Alternate CORS Settings</span></span>

<span data-ttu-id="e4188-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span><span class="sxs-lookup"><span data-stu-id="e4188-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="e4188-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e4188-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="e4188-293">Always configure production settings in App Settings within the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <a name="howto-appsettings"></a><span data-ttu-id="e4188-294">How: Configure App Settings for your Mobile App</span><span class="sxs-lookup"><span data-stu-id="e4188-294">How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="e4188-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="e4188-296">Use the following list to configure your app in App Settings:</span><span class="sxs-lookup"><span data-stu-id="e4188-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="e4188-297">App Setting</span><span class="sxs-lookup"><span data-stu-id="e4188-297">App Setting</span></span> | <span data-ttu-id="e4188-298">*azureMobile.js* Setting</span><span class="sxs-lookup"><span data-stu-id="e4188-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="e4188-299">Description</span><span class="sxs-lookup"><span data-stu-id="e4188-299">Description</span></span> | <span data-ttu-id="e4188-300">Valid Values</span><span class="sxs-lookup"><span data-stu-id="e4188-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e4188-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="e4188-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="e4188-302">name</span><span class="sxs-lookup"><span data-stu-id="e4188-302">name</span></span> |<span data-ttu-id="e4188-303">The name of the app</span><span class="sxs-lookup"><span data-stu-id="e4188-303">The name of the app</span></span> |<span data-ttu-id="e4188-304">string</span><span class="sxs-lookup"><span data-stu-id="e4188-304">string</span></span> |
| <span data-ttu-id="e4188-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="e4188-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="e4188-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="e4188-306">logging.level</span></span> |<span data-ttu-id="e4188-307">Minimum log level of messages to log</span><span class="sxs-lookup"><span data-stu-id="e4188-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="e4188-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="e4188-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="e4188-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="e4188-309">**MS_DebugMode**</span></span> |<span data-ttu-id="e4188-310">debug</span><span class="sxs-lookup"><span data-stu-id="e4188-310">debug</span></span> |<span data-ttu-id="e4188-311">Enable or Disable debug mode</span><span class="sxs-lookup"><span data-stu-id="e4188-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="e4188-312">true, false</span><span class="sxs-lookup"><span data-stu-id="e4188-312">true, false</span></span> |
| <span data-ttu-id="e4188-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="e4188-313">**MS_TableSchema**</span></span> |<span data-ttu-id="e4188-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="e4188-314">data.schema</span></span> |<span data-ttu-id="e4188-315">Default schema name for SQL tables</span><span class="sxs-lookup"><span data-stu-id="e4188-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="e4188-316">string (default: dbo)</span><span class="sxs-lookup"><span data-stu-id="e4188-316">string (default: dbo)</span></span> |
| <span data-ttu-id="e4188-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="e4188-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="e4188-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="e4188-318">data.dynamicSchema</span></span> |<span data-ttu-id="e4188-319">Enable or Disable debug mode</span><span class="sxs-lookup"><span data-stu-id="e4188-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="e4188-320">true, false</span><span class="sxs-lookup"><span data-stu-id="e4188-320">true, false</span></span> |
| <span data-ttu-id="e4188-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="e4188-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="e4188-322">version (set to undefined)</span><span class="sxs-lookup"><span data-stu-id="e4188-322">version (set to undefined)</span></span> |<span data-ttu-id="e4188-323">Disables the X-ZUMO-Server-Version header</span><span class="sxs-lookup"><span data-stu-id="e4188-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="e4188-324">true, false</span><span class="sxs-lookup"><span data-stu-id="e4188-324">true, false</span></span> |
| <span data-ttu-id="e4188-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="e4188-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="e4188-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="e4188-326">skipversioncheck</span></span> |<span data-ttu-id="e4188-327">Disables the client API version check</span><span class="sxs-lookup"><span data-stu-id="e4188-327">Disables the client API version check</span></span> |<span data-ttu-id="e4188-328">true, false</span><span class="sxs-lookup"><span data-stu-id="e4188-328">true, false</span></span> |

<span data-ttu-id="e4188-329">To set an App Setting:</span><span class="sxs-lookup"><span data-stu-id="e4188-329">To set an App Setting:</span></span>

1. <span data-ttu-id="e4188-330">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="e4188-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span><span class="sxs-lookup"><span data-stu-id="e4188-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="e4188-332">The Settings blade opens by default.</span><span class="sxs-lookup"><span data-stu-id="e4188-332">The Settings blade opens by default.</span></span> <span data-ttu-id="e4188-333">If it doesn't, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="e4188-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="e4188-334">Click **Application settings** in the GENERAL menu.</span><span class="sxs-lookup"><span data-stu-id="e4188-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="e4188-335">Scroll to the App Settings section.</span><span class="sxs-lookup"><span data-stu-id="e4188-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="e4188-336">If your app setting already exists, click the value of the app setting to edit the value.</span><span class="sxs-lookup"><span data-stu-id="e4188-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="e4188-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span><span class="sxs-lookup"><span data-stu-id="e4188-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="e4188-338">Once you are complete, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e4188-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="e4188-339">Changing most app settings requires a service restart.</span><span class="sxs-lookup"><span data-stu-id="e4188-339">Changing most app settings requires a service restart.</span></span>

### <a name="howto-use-sqlazure"></a><span data-ttu-id="e4188-340">How to: Use SQL Database as your production data store</span><span class="sxs-lookup"><span data-stu-id="e4188-340">How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="e4188-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span><span class="sxs-lookup"><span data-stu-id="e4188-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="e4188-342">If you have not done so already, follow these steps to create a Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="e4188-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="e4188-343">Log in to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="e4188-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="e4188-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="e4188-345">In the **Resource Group** box, enter the same name as your app.</span><span class="sxs-lookup"><span data-stu-id="e4188-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="e4188-346">The Default App Service plan is selected.</span><span class="sxs-lookup"><span data-stu-id="e4188-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="e4188-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span><span class="sxs-lookup"><span data-stu-id="e4188-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="e4188-348">Provide a name of the new App Service plan and select an appropriate location.</span><span class="sxs-lookup"><span data-stu-id="e4188-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="e4188-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span><span class="sxs-lookup"><span data-stu-id="e4188-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="e4188-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span><span class="sxs-lookup"><span data-stu-id="e4188-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="e4188-351">Once you have selected the pricing tier, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="e4188-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="e4188-352">Back in the **App Service plan** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4188-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="e4188-353">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4188-353">Click **Create**.</span></span> <span data-ttu-id="e4188-354">Provisioning a Mobile App backend can take a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="e4188-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="e4188-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="e4188-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="e4188-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span><span class="sxs-lookup"><span data-stu-id="e4188-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="e4188-357">In this section, we create a SQL database.</span><span class="sxs-lookup"><span data-stu-id="e4188-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="e4188-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span><span class="sxs-lookup"><span data-stu-id="e4188-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="e4188-359">The use of a database in a different location is not recommended because of higher latencies.</span><span class="sxs-lookup"><span data-stu-id="e4188-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
> 
> 

1. <span data-ttu-id="e4188-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span><span class="sxs-lookup"><span data-stu-id="e4188-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="e4188-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span><span class="sxs-lookup"><span data-stu-id="e4188-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="e4188-362">Enter the name of the new database in the **Name** field.</span><span class="sxs-lookup"><span data-stu-id="e4188-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="e4188-363">Click **Server**.</span><span class="sxs-lookup"><span data-stu-id="e4188-363">Click **Server**.</span></span>  <span data-ttu-id="e4188-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="e4188-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="e4188-365">Ensure **Allow azure services to access server** is checked.</span><span class="sxs-lookup"><span data-stu-id="e4188-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="e4188-366">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4188-366">Click **OK**.</span></span>
   
    ![Create an Azure SQL Database][6]
4. <span data-ttu-id="e4188-368">On the **New database** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4188-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="e4188-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span><span class="sxs-lookup"><span data-stu-id="e4188-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="e4188-370">If you use an existing database, provide the login credentials for that database.</span><span class="sxs-lookup"><span data-stu-id="e4188-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="e4188-371">Once entered, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4188-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="e4188-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span><span class="sxs-lookup"><span data-stu-id="e4188-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="e4188-373">Creation of the database can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="e4188-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="e4188-374">Use the **Notifications** area to monitor the progress of the deployment.</span><span class="sxs-lookup"><span data-stu-id="e4188-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="e4188-375">Do not progress until the database has been deployed successfully.</span><span class="sxs-lookup"><span data-stu-id="e4188-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="e4188-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span><span class="sxs-lookup"><span data-stu-id="e4188-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="e4188-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span><span class="sxs-lookup"><span data-stu-id="e4188-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <a name="howto-tables-auth"></a><span data-ttu-id="e4188-378">How to: Require authentication for access to tables</span><span class="sxs-lookup"><span data-stu-id="e4188-378">How to: Require authentication for access to tables</span></span>
<span data-ttu-id="e4188-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span><span class="sxs-lookup"><span data-stu-id="e4188-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="e4188-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span><span class="sxs-lookup"><span data-stu-id="e4188-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="e4188-381">[How to configure Azure Active Directory Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="e4188-382">[How to configure Facebook Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="e4188-383">[How to configure Google Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="e4188-384">[How to configure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="e4188-385">[How to configure Twitter Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="e4188-386">Each table has an access property that can be used to control access to the table.</span><span class="sxs-lookup"><span data-stu-id="e4188-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="e4188-387">The following sample shows a statically defined table with authentication required.</span><span class="sxs-lookup"><span data-stu-id="e4188-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="e4188-388">The access property can take one of three values</span><span class="sxs-lookup"><span data-stu-id="e4188-388">The access property can take one of three values</span></span>

* <span data-ttu-id="e4188-389">*anonymous* indicates that the client application is allowed to read data without authentication</span><span class="sxs-lookup"><span data-stu-id="e4188-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="e4188-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span><span class="sxs-lookup"><span data-stu-id="e4188-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="e4188-391">*disabled* indicates that this table is currently disabled</span><span class="sxs-lookup"><span data-stu-id="e4188-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="e4188-392">If the access property is undefined, unauthenticated access is allowed.</span><span class="sxs-lookup"><span data-stu-id="e4188-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <a name="howto-tables-getidentity"></a><span data-ttu-id="e4188-393">How to: Use authentication claims with your tables</span><span class="sxs-lookup"><span data-stu-id="e4188-393">How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="e4188-394">You can set up various claims that are requested when authentication is set up.</span><span class="sxs-lookup"><span data-stu-id="e4188-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="e4188-395">These claims are not normally available through the `context.user` object.</span><span class="sxs-lookup"><span data-stu-id="e4188-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="e4188-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span><span class="sxs-lookup"><span data-stu-id="e4188-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="e4188-397">The `getIdentity()` method returns a Promise that resolves to an object.</span><span class="sxs-lookup"><span data-stu-id="e4188-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="e4188-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span><span class="sxs-lookup"><span data-stu-id="e4188-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="e4188-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span><span class="sxs-lookup"><span data-stu-id="e4188-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="e4188-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span><span class="sxs-lookup"><span data-stu-id="e4188-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <a name="howto-tables-disabled"></a><span data-ttu-id="e4188-401">How to: Disable access to specific table operations</span><span class="sxs-lookup"><span data-stu-id="e4188-401">How to: Disable access to specific table operations</span></span>
<span data-ttu-id="e4188-402">In addition to appearing on the table, the access property can be used to control individual operations.</span><span class="sxs-lookup"><span data-stu-id="e4188-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="e4188-403">There are four operations:</span><span class="sxs-lookup"><span data-stu-id="e4188-403">There are four operations:</span></span>

* <span data-ttu-id="e4188-404">*read* is the RESTful GET operation on the table</span><span class="sxs-lookup"><span data-stu-id="e4188-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="e4188-405">*insert* is the RESTful POST operation on the table</span><span class="sxs-lookup"><span data-stu-id="e4188-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="e4188-406">*update* is the RESTful PATCH operation on the table</span><span class="sxs-lookup"><span data-stu-id="e4188-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="e4188-407">*delete* is the RESTful DELETE operation on the table</span><span class="sxs-lookup"><span data-stu-id="e4188-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="e4188-408">For example, you may wish to provide a read-only unauthenticated table:</span><span class="sxs-lookup"><span data-stu-id="e4188-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a><span data-ttu-id="e4188-409">How to: Adjust the query that is used with table operations</span><span class="sxs-lookup"><span data-stu-id="e4188-409">How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="e4188-410">A common requirement for table operations is to provide a restricted view of the data.</span><span class="sxs-lookup"><span data-stu-id="e4188-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="e4188-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span><span class="sxs-lookup"><span data-stu-id="e4188-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="e4188-412">The following table definition provides this functionality:</span><span class="sxs-lookup"><span data-stu-id="e4188-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="e4188-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span><span class="sxs-lookup"><span data-stu-id="e4188-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="e4188-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span><span class="sxs-lookup"><span data-stu-id="e4188-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="e4188-415">For simple equality cases (like the preceding one), a map can be used.</span><span class="sxs-lookup"><span data-stu-id="e4188-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="e4188-416">You can also add specific SQL clauses:</span><span class="sxs-lookup"><span data-stu-id="e4188-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a><span data-ttu-id="e4188-417">How to: Configure soft delete on a table</span><span class="sxs-lookup"><span data-stu-id="e4188-417">How to: Configure soft delete on a table</span></span>
<span data-ttu-id="e4188-418">Soft Delete does not actually delete records.</span><span class="sxs-lookup"><span data-stu-id="e4188-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="e4188-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span><span class="sxs-lookup"><span data-stu-id="e4188-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="e4188-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="e4188-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="e4188-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span><span class="sxs-lookup"><span data-stu-id="e4188-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="e4188-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span><span class="sxs-lookup"><span data-stu-id="e4188-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <a name="howto-tables-seeding"></a><span data-ttu-id="e4188-423">How to: Seed your database with data</span><span class="sxs-lookup"><span data-stu-id="e4188-423">How to: Seed your database with data</span></span>
<span data-ttu-id="e4188-424">When creating a new application, you may wish to seed a table with data.</span><span class="sxs-lookup"><span data-stu-id="e4188-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="e4188-425">This can be done within the table definition JavaScript file as follows:</span><span class="sxs-lookup"><span data-stu-id="e4188-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="e4188-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="e4188-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="e4188-427">If the table already exists within the database, no data is injected into the table.</span><span class="sxs-lookup"><span data-stu-id="e4188-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="e4188-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span><span class="sxs-lookup"><span data-stu-id="e4188-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="e4188-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span><span class="sxs-lookup"><span data-stu-id="e4188-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <a name="Swagger"></a><span data-ttu-id="e4188-430">How to: Enable Swagger support</span><span class="sxs-lookup"><span data-stu-id="e4188-430">How to: Enable Swagger support</span></span>
<span data-ttu-id="e4188-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span><span class="sxs-lookup"><span data-stu-id="e4188-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="e4188-432">To enable Swagger support, first install the swagger-ui as a dependency:</span><span class="sxs-lookup"><span data-stu-id="e4188-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="e4188-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span><span class="sxs-lookup"><span data-stu-id="e4188-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="e4188-434">You probably only want to enable Swagger support in development editions.</span><span class="sxs-lookup"><span data-stu-id="e4188-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="e4188-435">You can do this by utilizing the `NODE_ENV` app setting:</span><span class="sxs-lookup"><span data-stu-id="e4188-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="e4188-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="e4188-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="e4188-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span><span class="sxs-lookup"><span data-stu-id="e4188-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="e4188-438">if you choose to require authentication across your entire application, Swagger produces an error.</span><span class="sxs-lookup"><span data-stu-id="e4188-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="e4188-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span><span class="sxs-lookup"><span data-stu-id="e4188-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="e4188-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span><span class="sxs-lookup"><span data-stu-id="e4188-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="e4188-441"><a name="push">Push notifications</span><span class="sxs-lookup"><span data-stu-id="e4188-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="e4188-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span><span class="sxs-lookup"><span data-stu-id="e4188-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="e4188-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span><span class="sxs-lookup"><span data-stu-id="e4188-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="e4188-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e4188-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="e4188-445"></a><a name="send-push"></a>How to: Send push notifications</span><span class="sxs-lookup"><span data-stu-id="e4188-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="e4188-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span><span class="sxs-lookup"><span data-stu-id="e4188-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="e4188-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span><span class="sxs-lookup"><span data-stu-id="e4188-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="e4188-448">The following code shows how to send a template notification:</span><span class="sxs-lookup"><span data-stu-id="e4188-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <a name="push-user"></a><span data-ttu-id="e4188-449">How to: Send push notifications to an authenticated user using tags</span><span class="sxs-lookup"><span data-stu-id="e4188-449">How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="e4188-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span><span class="sxs-lookup"><span data-stu-id="e4188-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="e4188-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span><span class="sxs-lookup"><span data-stu-id="e4188-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="e4188-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span><span class="sxs-lookup"><span data-stu-id="e4188-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="e4188-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span><span class="sxs-lookup"><span data-stu-id="e4188-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <a name="CustomAPI"></a> <span data-ttu-id="e4188-454">Custom APIs</span><span class="sxs-lookup"><span data-stu-id="e4188-454">Custom APIs</span></span>
### <a name="howto-customapi-basic"></a><span data-ttu-id="e4188-455">How to: Define a custom API</span><span class="sxs-lookup"><span data-stu-id="e4188-455">How to: Define a custom API</span></span>
<span data-ttu-id="e4188-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span><span class="sxs-lookup"><span data-stu-id="e4188-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="e4188-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span><span class="sxs-lookup"><span data-stu-id="e4188-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="e4188-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span><span class="sxs-lookup"><span data-stu-id="e4188-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="e4188-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span><span class="sxs-lookup"><span data-stu-id="e4188-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="e4188-460">[How to configure Azure Active Directory Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="e4188-461">[How to configure Facebook Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="e4188-462">[How to configure Google Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="e4188-463">[How to configure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="e4188-464">[How to configure Twitter Authentication]</span><span class="sxs-lookup"><span data-stu-id="e4188-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="e4188-465">Custom APIs are defined in much the same way as the Tables API.</span><span class="sxs-lookup"><span data-stu-id="e4188-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="e4188-466">Create an **api** directory</span><span class="sxs-lookup"><span data-stu-id="e4188-466">Create an **api** directory</span></span>
2. <span data-ttu-id="e4188-467">Create an API definition JavaScript file in the **api** directory.</span><span class="sxs-lookup"><span data-stu-id="e4188-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="e4188-468">Use the import method to import the **api** directory.</span><span class="sxs-lookup"><span data-stu-id="e4188-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="e4188-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span><span class="sxs-lookup"><span data-stu-id="e4188-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="e4188-470">Let's take an example API that returns the server date using the *Date.now()* method.</span><span class="sxs-lookup"><span data-stu-id="e4188-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="e4188-471">Here is the api/date.js file:</span><span class="sxs-lookup"><span data-stu-id="e4188-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="e4188-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span><span class="sxs-lookup"><span data-stu-id="e4188-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="e4188-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span><span class="sxs-lookup"><span data-stu-id="e4188-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <a name="howto-customapi-auth"></a><span data-ttu-id="e4188-474">How to: Require authentication for access to a custom API</span><span class="sxs-lookup"><span data-stu-id="e4188-474">How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="e4188-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span><span class="sxs-lookup"><span data-stu-id="e4188-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="e4188-476">To add authentication to the API developed in the previous section, add an **access** property:</span><span class="sxs-lookup"><span data-stu-id="e4188-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="e4188-477">You can also specify authentication on specific operations:</span><span class="sxs-lookup"><span data-stu-id="e4188-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="e4188-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span><span class="sxs-lookup"><span data-stu-id="e4188-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <a name="howto-customapi-auth"></a><span data-ttu-id="e4188-479">How to: Handle large file uploads</span><span class="sxs-lookup"><span data-stu-id="e4188-479">How to: Handle large file uploads</span></span>
<span data-ttu-id="e4188-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span><span class="sxs-lookup"><span data-stu-id="e4188-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="e4188-481">You can pre-configure body-parser to accept larger file uploads:</span><span class="sxs-lookup"><span data-stu-id="e4188-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="e4188-482">The file is base-64 encoded before transmission.</span><span class="sxs-lookup"><span data-stu-id="e4188-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="e4188-483">This increases the size of the actual upload (and hence the size you must account for).</span><span class="sxs-lookup"><span data-stu-id="e4188-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <a name="howto-customapi-sql"></a><span data-ttu-id="e4188-484">How to: Execute custom SQL statements</span><span class="sxs-lookup"><span data-stu-id="e4188-484">How to: Execute custom SQL statements</span></span>
<span data-ttu-id="e4188-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span><span class="sxs-lookup"><span data-stu-id="e4188-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a><span data-ttu-id="e4188-486">Debugging, Easy Tables, and Easy APIs</span><span class="sxs-lookup"><span data-stu-id="e4188-486">Debugging, Easy Tables, and Easy APIs</span></span>
### <a name="howto-diagnostic-logs"></a><span data-ttu-id="e4188-487">How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span><span class="sxs-lookup"><span data-stu-id="e4188-487">How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="e4188-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span><span class="sxs-lookup"><span data-stu-id="e4188-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="e4188-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span><span class="sxs-lookup"><span data-stu-id="e4188-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="e4188-490">[Monitoring an Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="e4188-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="e4188-491">[Enable Diagnostic Logging in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="e4188-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="e4188-492">[Troubleshoot an Azure App Service in Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e4188-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="e4188-493">Node.js applications have access to a wide range of diagnostic log tools.</span><span class="sxs-lookup"><span data-stu-id="e4188-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="e4188-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="e4188-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="e4188-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="e4188-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e4188-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <a name="in-portal-editing"></a><span data-ttu-id="e4188-497"><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4188-497"><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="e4188-498">Easy Tables in the portal let you create and work with tables right in the portal.</span><span class="sxs-lookup"><span data-stu-id="e4188-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="e4188-499">You can even edit table operations using the App Service Editor.</span><span class="sxs-lookup"><span data-stu-id="e4188-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="e4188-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span><span class="sxs-lookup"><span data-stu-id="e4188-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="e4188-501">You can also see data in the table.</span><span class="sxs-lookup"><span data-stu-id="e4188-501">You can also see data in the table.</span></span>

![Work with Easy Tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="e4188-503">The following commands are available on the command bar for a table:</span><span class="sxs-lookup"><span data-stu-id="e4188-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="e4188-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span><span class="sxs-lookup"><span data-stu-id="e4188-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span> 
  <span data-ttu-id="e4188-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span><span class="sxs-lookup"><span data-stu-id="e4188-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span> 
* <span data-ttu-id="e4188-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span><span class="sxs-lookup"><span data-stu-id="e4188-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="e4188-507">**Manage schema** - add or delete columns or change the table index.</span><span class="sxs-lookup"><span data-stu-id="e4188-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="e4188-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span><span class="sxs-lookup"><span data-stu-id="e4188-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="e4188-509">**Delete rows** - delete individual rows of data.</span><span class="sxs-lookup"><span data-stu-id="e4188-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="e4188-510">**View streaming logs** - connects you to the streaming log service for your site.</span><span class="sxs-lookup"><span data-stu-id="e4188-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <a name="work-easy-apis"></a><span data-ttu-id="e4188-511">How to: Work with Easy APIs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4188-511">How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="e4188-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span><span class="sxs-lookup"><span data-stu-id="e4188-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="e4188-513">You can edit API scripts using the App Service Editor.</span><span class="sxs-lookup"><span data-stu-id="e4188-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="e4188-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span><span class="sxs-lookup"><span data-stu-id="e4188-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Work with Easy APIs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="e4188-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span><span class="sxs-lookup"><span data-stu-id="e4188-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <a name="online-editor"></a><span data-ttu-id="e4188-517">How to: Edit code in the App Service Editor</span><span class="sxs-lookup"><span data-stu-id="e4188-517">How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="e4188-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span><span class="sxs-lookup"><span data-stu-id="e4188-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="e4188-519">To edit script files in the online editor:</span><span class="sxs-lookup"><span data-stu-id="e4188-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="e4188-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span><span class="sxs-lookup"><span data-stu-id="e4188-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="e4188-521">The script file is opened in the App Service Editor.</span><span class="sxs-lookup"><span data-stu-id="e4188-521">The script file is opened in the App Service Editor.</span></span>
   
    ![App Service Editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="e4188-523">Make your changes to the code file in the online editor.</span><span class="sxs-lookup"><span data-stu-id="e4188-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="e4188-524">Changes are saved automatically as you type.</span><span class="sxs-lookup"><span data-stu-id="e4188-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android Client QuickStart]: app-service-mobile-android-get-started.md
[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md
[iOS Client QuickStart]: app-service-mobile-ios-get-started.md
[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md
[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[offline data sync]: app-service-mobile-offline-data-sync.md
[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md
[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md
[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md
[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md
[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md
[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md
[use Node modules]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston










