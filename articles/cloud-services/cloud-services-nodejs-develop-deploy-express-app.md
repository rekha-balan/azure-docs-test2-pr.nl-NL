---
title: Web App with Express (Node.js) | Microsoft Docs
description: A tutorial that builds on the cloud service tutorial, and demonstrates how to use the Express module.
services: cloud-services
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 33f0a555c0dd8c2561a165e58a28bc7f554eeb11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553181"
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="3fd3f-103">Build a Node.js web application using Express on an Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="3fd3f-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="3fd3f-104">Node.js includes a minimal set of functionality in the core runtime.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="3fd3f-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="3fd3f-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="3fd3f-107">A screenshot of the completed application is below:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-107">A screenshot of the completed application is below:</span></span>

![A web browser displaying Welcome to Express in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="3fd3f-109">Create a Cloud Service Project</span><span class="sxs-lookup"><span data-stu-id="3fd3f-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="3fd3f-110">Perform the following steps to create a new cloud service project named 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="3fd3f-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="3fd3f-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="3fd3f-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="3fd3f-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="3fd3f-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="3fd3f-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="3fd3f-117">Note the parameters are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="3fd3f-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="3fd3f-119">Install Express</span><span class="sxs-lookup"><span data-stu-id="3fd3f-119">Install Express</span></span>
1. <span data-ttu-id="3fd3f-120">Install the Express generator by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="3fd3f-121">The output of the npm command should look similar to the result below.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell displaying the output of the npm install express command.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="3fd3f-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="3fd3f-124">You will be prompted to overwrite your earlier application.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="3fd3f-125">Enter **y** or **yes** to continue.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="3fd3f-126">Express will generate the app.js file and a folder structure for building your application.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![The output of the express command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="3fd3f-128">To install additional dependencies defined in the package.json file, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![The output of the npm install command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="3fd3f-130">Use the following command to copy the **bin/www** file to **server.js**.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="3fd3f-131">This is so the cloud service can find the entry point for this application.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="3fd3f-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="3fd3f-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="3fd3f-134">After making this modification, the line should appear as follows.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="3fd3f-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="3fd3f-136">After making this change, save the **server.js** file.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="3fd3f-137">Use the following command to run the application in the Azure emulator:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![A web page containing welcome to express.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="3fd3f-139">Modifying the View</span><span class="sxs-lookup"><span data-stu-id="3fd3f-139">Modifying the View</span></span>
<span data-ttu-id="3fd3f-140">Now modify the view to display the message "Welcome to Express in Azure".</span><span class="sxs-lookup"><span data-stu-id="3fd3f-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="3fd3f-141">Enter the following command to open the index.jade file:</span><span class="sxs-lookup"><span data-stu-id="3fd3f-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![The contents of the index.jade file.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="3fd3f-143">Jade is the default view engine used by Express applications.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="3fd3f-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="3fd3f-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="3fd3f-145">Modify the last line of text by appending **in Azure**.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![The index.jade file, the last line reads: p Welcome to \#{title} in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="3fd3f-147">Save the file and exit Notepad.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="3fd3f-148">Refresh your browser and you will see your changes.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-148">Refresh your browser and you will see your changes.</span></span>
   
   ![A browser window, the page contains Welcome to Express in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="3fd3f-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="3fd3f-151">Publishing the Application to Azure</span><span class="sxs-lookup"><span data-stu-id="3fd3f-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="3fd3f-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span><span class="sxs-lookup"><span data-stu-id="3fd3f-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="3fd3f-153">Once the deployment operation completes, your browser will open and display the web page.</span><span class="sxs-lookup"><span data-stu-id="3fd3f-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![A web browser displaying the Express page.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="3fd3f-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fd3f-156">Next steps</span></span>
<span data-ttu-id="3fd3f-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="3fd3f-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com












