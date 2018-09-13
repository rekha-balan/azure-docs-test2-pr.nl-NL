---
title: Create a Node.js chat application with Socket.IO in Azure App Service
description: A tutorial that demonstrates using socket.io in a node.js web app hosted on Azure.
services: app-service\web
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 4f5c04525437aefeccbe58e06b084433d0413dc1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556564"
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="34e0c-103">Create a Node.js chat application with Socket.IO in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="34e0c-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="34e0c-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span><span class="sxs-lookup"><span data-stu-id="34e0c-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="34e0c-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span><span class="sxs-lookup"><span data-stu-id="34e0c-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="34e0c-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span><span class="sxs-lookup"><span data-stu-id="34e0c-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="34e0c-107">For more information on Socket.IO, see <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="34e0c-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="34e0c-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span><span class="sxs-lookup"><span data-stu-id="34e0c-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="34e0c-109">Download the chat example</span><span class="sxs-lookup"><span data-stu-id="34e0c-109">Download the chat example</span></span>
<span data-ttu-id="34e0c-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span><span class="sxs-lookup"><span data-stu-id="34e0c-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="34e0c-111">Perform the following steps to download the example and add it to the project you previously created.</span><span class="sxs-lookup"><span data-stu-id="34e0c-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="34e0c-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span><span class="sxs-lookup"><span data-stu-id="34e0c-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="34e0c-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span><span class="sxs-lookup"><span data-stu-id="34e0c-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="34e0c-114">For example, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="34e0c-115">Modify app.js and install modules</span><span class="sxs-lookup"><span data-stu-id="34e0c-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="34e0c-116">Rename the **index.js** file to **app.js**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="34e0c-117">This allows Azure to detect that this is a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="34e0c-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="34e0c-118">Open the **app.js** file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="34e0c-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="34e0c-119">Change the line containing `var io = require('../..')(server);` as shown below:</span><span class="sxs-lookup"><span data-stu-id="34e0c-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="34e0c-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span><span class="sxs-lookup"><span data-stu-id="34e0c-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="34e0c-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span><span class="sxs-lookup"><span data-stu-id="34e0c-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="34e0c-122">This will install the modules into a subfolder named **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="34e0c-123">Create an Azure Web App</span><span class="sxs-lookup"><span data-stu-id="34e0c-123">Create an Azure Web App</span></span>
<span data-ttu-id="34e0c-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span><span class="sxs-lookup"><span data-stu-id="34e0c-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="34e0c-125">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="34e0c-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="34e0c-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="34e0c-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="34e0c-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span><span class="sxs-lookup"><span data-stu-id="34e0c-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="34e0c-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="34e0c-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="34e0c-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="34e0c-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="34e0c-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span><span class="sxs-lookup"><span data-stu-id="34e0c-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="34e0c-131">From the Azure CLI, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="34e0c-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="34e0c-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="34e0c-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="34e0c-133">This command also creates a Git remote named 'azure'.</span><span class="sxs-lookup"><span data-stu-id="34e0c-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="34e0c-134">You must replace 'mysitename' with a unique name for your web app.</span><span class="sxs-lookup"><span data-stu-id="34e0c-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="34e0c-135">Commit the existing files to the local repository by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="34e0c-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="34e0c-136">Push the files to the Azure Web Apps repository with the following command:</span><span class="sxs-lookup"><span data-stu-id="34e0c-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="34e0c-137">When prompted, enter your credentials from step 2.</span><span class="sxs-lookup"><span data-stu-id="34e0c-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="34e0c-138">You will receive status messages as modules are imported on the server.</span><span class="sxs-lookup"><span data-stu-id="34e0c-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="34e0c-139">Once this process has completed, the application will be hosted on your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="34e0c-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34e0c-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span><span class="sxs-lookup"><span data-stu-id="34e0c-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="34e0c-141">These can safely be ignored.</span><span class="sxs-lookup"><span data-stu-id="34e0c-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="34e0c-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span><span class="sxs-lookup"><span data-stu-id="34e0c-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="34e0c-143">To enable web sockets, use the following command:</span><span class="sxs-lookup"><span data-stu-id="34e0c-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="34e0c-144">If prompted, enter the name of the web app.</span><span class="sxs-lookup"><span data-stu-id="34e0c-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34e0c-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span><span class="sxs-lookup"><span data-stu-id="34e0c-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="34e0c-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34e0c-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="34e0c-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="34e0c-148">Under **Web Sockets**, click **On**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="34e0c-149">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="34e0c-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span><span class="sxs-lookup"><span data-stu-id="34e0c-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="34e0c-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="34e0c-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="34e0c-152">Scale out</span><span class="sxs-lookup"><span data-stu-id="34e0c-152">Scale out</span></span>
<span data-ttu-id="34e0c-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span><span class="sxs-lookup"><span data-stu-id="34e0c-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="34e0c-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span><span class="sxs-lookup"><span data-stu-id="34e0c-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="34e0c-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span><span class="sxs-lookup"><span data-stu-id="34e0c-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="34e0c-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span><span class="sxs-lookup"><span data-stu-id="34e0c-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="34e0c-157">For more information, see [Instance Affinity in Azure Web Sites].</span><span class="sxs-lookup"><span data-stu-id="34e0c-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="34e0c-158">Create a Redis cache</span><span class="sxs-lookup"><span data-stu-id="34e0c-158">Create a Redis cache</span></span>
<span data-ttu-id="34e0c-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span><span class="sxs-lookup"><span data-stu-id="34e0c-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="34e0c-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span><span class="sxs-lookup"><span data-stu-id="34e0c-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="34e0c-161">Add the redis and socket.io-redis modules</span><span class="sxs-lookup"><span data-stu-id="34e0c-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="34e0c-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span><span class="sxs-lookup"><span data-stu-id="34e0c-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="34e0c-163">The versions specified in this command are the versions used when testing this article.</span><span class="sxs-lookup"><span data-stu-id="34e0c-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="34e0c-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="34e0c-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="34e0c-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span><span class="sxs-lookup"><span data-stu-id="34e0c-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="34e0c-166">This will create a publish and subscribe client to the Redis cache created previously.</span><span class="sxs-lookup"><span data-stu-id="34e0c-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="34e0c-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span><span class="sxs-lookup"><span data-stu-id="34e0c-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34e0c-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span><span class="sxs-lookup"><span data-stu-id="34e0c-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="34e0c-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span><span class="sxs-lookup"><span data-stu-id="34e0c-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="34e0c-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span><span class="sxs-lookup"><span data-stu-id="34e0c-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="34e0c-171">The above code uses the default, unsecure port of 6379.</span><span class="sxs-lookup"><span data-stu-id="34e0c-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="34e0c-172">Save the modified **app.js**</span><span class="sxs-lookup"><span data-stu-id="34e0c-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="34e0c-173">Commit changes and redeploy</span><span class="sxs-lookup"><span data-stu-id="34e0c-173">Commit changes and redeploy</span></span>
<span data-ttu-id="34e0c-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span><span class="sxs-lookup"><span data-stu-id="34e0c-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="34e0c-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span><span class="sxs-lookup"><span data-stu-id="34e0c-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="34e0c-176">Where **#** is the number of instances to create.</span><span class="sxs-lookup"><span data-stu-id="34e0c-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="34e0c-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span><span class="sxs-lookup"><span data-stu-id="34e0c-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="34e0c-178">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="34e0c-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="34e0c-179">Connection limits</span><span class="sxs-lookup"><span data-stu-id="34e0c-179">Connection limits</span></span>
<span data-ttu-id="34e0c-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span><span class="sxs-lookup"><span data-stu-id="34e0c-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="34e0c-181">This includes the number of allowed WebSocket connections.</span><span class="sxs-lookup"><span data-stu-id="34e0c-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="34e0c-182">For more information, see the [Web Apps Pricing page].</span><span class="sxs-lookup"><span data-stu-id="34e0c-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="34e0c-183">Messages aren't being sent using WebSockets</span><span class="sxs-lookup"><span data-stu-id="34e0c-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="34e0c-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span><span class="sxs-lookup"><span data-stu-id="34e0c-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="34e0c-185">**Try limiting the transport to just WebSockets**</span><span class="sxs-lookup"><span data-stu-id="34e0c-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="34e0c-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span><span class="sxs-lookup"><span data-stu-id="34e0c-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="34e0c-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span><span class="sxs-lookup"><span data-stu-id="34e0c-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="34e0c-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="34e0c-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="34e0c-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="34e0c-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="34e0c-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span><span class="sxs-lookup"><span data-stu-id="34e0c-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="34e0c-191">**Use SSL**</span><span class="sxs-lookup"><span data-stu-id="34e0c-191">**Use SSL**</span></span>
  
    <span data-ttu-id="34e0c-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span><span class="sxs-lookup"><span data-stu-id="34e0c-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="34e0c-193">Some intermediate network devices, such as web proxies, may remove these headers.</span><span class="sxs-lookup"><span data-stu-id="34e0c-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="34e0c-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span><span class="sxs-lookup"><span data-stu-id="34e0c-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="34e0c-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="34e0c-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="34e0c-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span><span class="sxs-lookup"><span data-stu-id="34e0c-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="34e0c-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span><span class="sxs-lookup"><span data-stu-id="34e0c-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="34e0c-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="34e0c-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="34e0c-199">**Verify web.config settings**</span><span class="sxs-lookup"><span data-stu-id="34e0c-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="34e0c-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span><span class="sxs-lookup"><span data-stu-id="34e0c-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="34e0c-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span><span class="sxs-lookup"><span data-stu-id="34e0c-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="34e0c-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="34e0c-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="34e0c-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span><span class="sxs-lookup"><span data-stu-id="34e0c-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="34e0c-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span><span class="sxs-lookup"><span data-stu-id="34e0c-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="34e0c-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span><span class="sxs-lookup"><span data-stu-id="34e0c-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="34e0c-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span><span class="sxs-lookup"><span data-stu-id="34e0c-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="34e0c-207">The URLs are displayed in the **quick glance** section.</span><span class="sxs-lookup"><span data-stu-id="34e0c-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="34e0c-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span><span class="sxs-lookup"><span data-stu-id="34e0c-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="34e0c-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="34e0c-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="34e0c-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span><span class="sxs-lookup"><span data-stu-id="34e0c-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="34e0c-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span><span class="sxs-lookup"><span data-stu-id="34e0c-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="34e0c-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span><span class="sxs-lookup"><span data-stu-id="34e0c-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="34e0c-213">For example, replacing **app.js** with **server.js**.</span><span class="sxs-lookup"><span data-stu-id="34e0c-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="34e0c-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="34e0c-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="34e0c-215">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="34e0c-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="34e0c-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="34e0c-216">Next steps</span></span>
<span data-ttu-id="34e0c-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="34e0c-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="34e0c-218">You can also host this application as an Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="34e0c-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="34e0c-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span><span class="sxs-lookup"><span data-stu-id="34e0c-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="34e0c-220">For more information, see also the [Node.js Developer Center].</span><span class="sxs-lookup"><span data-stu-id="34e0c-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="34e0c-221">What's changed</span><span class="sxs-lookup"><span data-stu-id="34e0c-221">What's changed</span></span>
* <span data-ttu-id="34e0c-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span><span class="sxs-lookup"><span data-stu-id="34e0c-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Azure Redis Cache]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643
[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js Developer Center]: /develop/nodejs/
[Try App Service]: https://azure.microsoft.com/try/app-service/
[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub repository]: https://github.com/socketio/socket.io
[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
