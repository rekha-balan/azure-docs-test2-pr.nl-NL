---
title: Node.js application using Socket.io | Microsoft Docs
description: Learn how to use socket.io in a node.js application hosted on Azure.
services: cloud-services
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: c8e91db2dbcd71770dd38bae2b4fd46c6f2a997d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552449"
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="2f8c7-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="2f8c7-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="2f8c7-104">Socket.IO provides realtime communication between between your node.js server and clients.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="2f8c7-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="2f8c7-106">For more information on Socket.IO, see <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="2f8c7-107">A screenshot of the completed application is below:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-107">A screenshot of the completed application is below:</span></span>

![A browser window displaying the service hosted on Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="2f8c7-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f8c7-109">Prerequisites</span></span>
<span data-ttu-id="2f8c7-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span></span>

* <span data-ttu-id="2f8c7-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="2f8c7-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="2f8c7-112">Install [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="2f8c7-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="2f8c7-113">Install [Python version 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="2f8c7-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="2f8c7-114">Create a Cloud Service Project</span><span class="sxs-lookup"><span data-stu-id="2f8c7-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="2f8c7-115">The following steps create the cloud service project that will host the Socket.IO application.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-115">The following steps create the cloud service project that will host the Socket.IO application.</span></span>

1. <span data-ttu-id="2f8c7-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="2f8c7-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell icon][powershell-menu]
2. <span data-ttu-id="2f8c7-119">Create a directory called **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="2f8c7-120">Change directories to the **c:\\node** directory</span><span class="sxs-lookup"><span data-stu-id="2f8c7-120">Change directories to the **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="2f8c7-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="2f8c7-122">You will see the following response:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-122">You will see the following response:</span></span>
   
    ![The output of the new-azureservice and add-azurenodeworkerrolecmdlets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-the-chat-example"></a><span data-ttu-id="2f8c7-124">Download the Chat Example</span><span class="sxs-lookup"><span data-stu-id="2f8c7-124">Download the Chat Example</span></span>
<span data-ttu-id="2f8c7-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span><span class="sxs-lookup"><span data-stu-id="2f8c7-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="2f8c7-126">Perform the following steps to download the example and add it to the project you previously created.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-126">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="2f8c7-127">Create a local copy of the repository by using the **Clone** button.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-127">Create a local copy of the repository by using the **Clone** button.</span></span> <span data-ttu-id="2f8c7-128">You may also use the **ZIP** button to download the project.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-128">You may also use the **ZIP** button to download the project.</span></span>
   
   ![A browser window viewing https://github.com/LearnBoost/socket.io/tree/master/examples/chat, with the ZIP download icon highlighted][chat-example-view]
2. <span data-ttu-id="2f8c7-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span></span> <span data-ttu-id="2f8c7-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Explorer, displaying the contents of the examples\\chat directory extracted from the archive][chat-contents]
   
   <span data-ttu-id="2f8c7-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span><span class="sxs-lookup"><span data-stu-id="2f8c7-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span></span>
3. <span data-ttu-id="2f8c7-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span></span> <span data-ttu-id="2f8c7-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="2f8c7-136">Modify Server.js and Install Modules</span><span class="sxs-lookup"><span data-stu-id="2f8c7-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="2f8c7-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="2f8c7-138">Perform the following steps to the server.js file:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-138">Perform the following steps to the server.js file:</span></span>

1. <span data-ttu-id="2f8c7-139">Open the **server.js** file in Visual Studio or any text editor.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-139">Open the **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="2f8c7-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
3. <span data-ttu-id="2f8c7-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="2f8c7-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span></span>

1. <span data-ttu-id="2f8c7-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="2f8c7-144">This will install the modules listed in the package.json file.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-144">This will install the modules listed in the package.json file.</span></span> <span data-ttu-id="2f8c7-145">After the command completes, you should see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-145">After the command completes, you should see output similar to the following:</span></span>
   
   ![The output of the npm install command][The-output-of-the-npm-install-command]
2. <span data-ttu-id="2f8c7-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="2f8c7-148">Test and Deploy</span><span class="sxs-lookup"><span data-stu-id="2f8c7-148">Test and Deploy</span></span>
1. <span data-ttu-id="2f8c7-149">Launch the emulator by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-149">Launch the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
2. <span data-ttu-id="2f8c7-150">Open a browser and navigate to **http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-150">Open a browser and navigate to **http://127.0.0.1**.</span></span>
3. <span data-ttu-id="2f8c7-151">When the browser window opens, enter a nickname and then hit enter.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-151">When the browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="2f8c7-152">This will all you to post messages as a specific nickname.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-152">This will all you to post messages as a specific nickname.</span></span> <span data-ttu-id="2f8c7-153">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-153">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Two browser windows displaying chat messages from User1 and User2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="2f8c7-155">After testing the application, stop the emulator by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-155">After testing the application, stop the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="2f8c7-156">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-156">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="2f8c7-157">For example:</span><span class="sxs-lookup"><span data-stu-id="2f8c7-157">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="2f8c7-158">Be sure to use a unique name, otherwise the publish process will fail.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-158">Be sure to use a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="2f8c7-159">After the deployment has completed, the browser will open and navigate to the deployed service.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-159">After the deployment has completed, the browser will open and navigate to the deployed service.</span></span>
   > 
   > <span data-ttu-id="2f8c7-160">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-160">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="2f8c7-161">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="2f8c7-161">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![A browser window displaying the service hosted on Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="2f8c7-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="2f8c7-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="2f8c7-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="2f8c7-165">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-165">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="2f8c7-166">For simplicity, this sample is limited to chatting between users connected to the same instance.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-166">For simplicity, this sample is limited to chatting between users connected to the same instance.</span></span> <span data-ttu-id="2f8c7-167">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-167">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span></span> <span data-ttu-id="2f8c7-168">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-168">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span></span> <span data-ttu-id="2f8c7-169">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="2f8c7-169">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2f8c7-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f8c7-170">Next steps</span></span>
<span data-ttu-id="2f8c7-171">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="2f8c7-171">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="2f8c7-172">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="2f8c7-172">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="2f8c7-173">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="2f8c7-173">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub repository]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting the Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png









