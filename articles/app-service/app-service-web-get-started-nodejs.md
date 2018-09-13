---
title: Create a Node.js web app in Azure | Microsoft Docs
description: Deploy your first Node.js Hello World in Azure App Service Web Apps in minutes.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: cephalin;cfowler
ms.custom: mvc, devcenter
ms.openlocfilehash: 63e65ffc17ba71a5d2cf00cb5f04e3e0f87c1bfe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867111"
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="bcd14-103">Create a Node.js web app in Azure</span><span class="sxs-lookup"><span data-stu-id="bcd14-103">Create a Node.js web app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="bcd14-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="bcd14-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="bcd14-105">To deploy to App Service on _Linux_, see [Create a Node.js web app in Azure App Service on Linux](./containers/quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bcd14-105">To deploy to App Service on _Linux_, see [Create a Node.js web app in Azure App Service on Linux](./containers/quickstart-nodejs.md).</span></span>
>

<span data-ttu-id="bcd14-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="bcd14-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="bcd14-107">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="bcd14-107">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="bcd14-108">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span><span class="sxs-lookup"><span data-stu-id="bcd14-108">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![Sample app running in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="bcd14-110">You can follow the steps here using a Mac, Windows, or Linux machine.</span><span class="sxs-lookup"><span data-stu-id="bcd14-110">You can follow the steps here using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="bcd14-111">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span><span class="sxs-lookup"><span data-stu-id="bcd14-111">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="bcd14-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bcd14-112">Prerequisites</span></span>

<span data-ttu-id="bcd14-113">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="bcd14-113">To complete this quickstart:</span></span>

* <span data-ttu-id="bcd14-114"><a href="https://nodejs.org/" target="_blank">Install Node.js and NPM</a></span><span class="sxs-lookup"><span data-stu-id="bcd14-114"><a href="https://nodejs.org/" target="_blank">Install Node.js and NPM</a></span></span>

## <a name="download-the-sample"></a><span data-ttu-id="bcd14-115">Download the sample</span><span class="sxs-lookup"><span data-stu-id="bcd14-115">Download the sample</span></span>

<span data-ttu-id="bcd14-116">Download the sample Node.js project from [https://github.com/Azure-Samples/nodejs-docs-hello-world/archive/master.zip](https://github.com/Azure-Samples/nodejs-docs-hello-world/archive/master.zip) and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="bcd14-116">Download the sample Node.js project from [https://github.com/Azure-Samples/nodejs-docs-hello-world/archive/master.zip](https://github.com/Azure-Samples/nodejs-docs-hello-world/archive/master.zip) and extract the ZIP archive.</span></span>

<span data-ttu-id="bcd14-117">In a terminal window, navigate to the root directory of the sample Node.js project (the one that contains _index.js_).</span><span class="sxs-lookup"><span data-stu-id="bcd14-117">In a terminal window, navigate to the root directory of the sample Node.js project (the one that contains _index.js_).</span></span>

## <a name="run-the-app-locally"></a><span data-ttu-id="bcd14-118">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="bcd14-118">Run the app locally</span></span>

<span data-ttu-id="bcd14-119">Run the application locally so that you see how it should look when you deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd14-119">Run the application locally so that you see how it should look when you deploy it to Azure.</span></span> <span data-ttu-id="bcd14-120">Open a terminal window and use the `npm start` script to launch the built in Node.js HTTP server.</span><span class="sxs-lookup"><span data-stu-id="bcd14-120">Open a terminal window and use the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="bcd14-121">Open a web browser, and navigate to the sample app at `http://localhost:1337`.</span><span class="sxs-lookup"><span data-stu-id="bcd14-121">Open a web browser, and navigate to the sample app at `http://localhost:1337`.</span></span>

<span data-ttu-id="bcd14-122">You see the **Hello World** message from the sample app displayed in the page.</span><span class="sxs-lookup"><span data-stu-id="bcd14-122">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Sample app running locally](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="bcd14-124">In your terminal window, press **Ctrl+C** to exit the web server.</span><span class="sxs-lookup"><span data-stu-id="bcd14-124">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

> [!NOTE]
> <span data-ttu-id="bcd14-125">In Azure App Service, the app is run in IIS using [iisnode](https://github.com/tjanczuk/iisnode).</span><span class="sxs-lookup"><span data-stu-id="bcd14-125">In Azure App Service, the app is run in IIS using [iisnode](https://github.com/tjanczuk/iisnode).</span></span> <span data-ttu-id="bcd14-126">To enable the app to run with iisnode, the root app directory contains a web.config file.</span><span class="sxs-lookup"><span data-stu-id="bcd14-126">To enable the app to run with iisnode, the root app directory contains a web.config file.</span></span> <span data-ttu-id="bcd14-127">The file is readable by IIS, and the iisnode-related settings are documented in [the iisnode GitHub repository](https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config).</span><span class="sxs-lookup"><span data-stu-id="bcd14-127">The file is readable by IIS, and the iisnode-related settings are documented in [the iisnode GitHub repository](https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config).</span></span>

[!INCLUDE [Create ZIP file](../../includes/app-service-web-create-zip.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

## <a name="create-a-web-app"></a><span data-ttu-id="bcd14-128">Create a web app</span><span class="sxs-lookup"><span data-stu-id="bcd14-128">Create a web app</span></span>

<span data-ttu-id="bcd14-129">In the Cloud Shell, create a web app in the `myAppServicePlan` App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="bcd14-129">In the Cloud Shell, create a web app in the `myAppServicePlan` App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> 

<span data-ttu-id="bcd14-130">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="bcd14-130">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="bcd14-131">The runtime is set to `NODE|6.9`.</span><span class="sxs-lookup"><span data-stu-id="bcd14-131">The runtime is set to `NODE|6.9`.</span></span> <span data-ttu-id="bcd14-132">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-list-runtimes).</span><span class="sxs-lookup"><span data-stu-id="bcd14-132">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-list-runtimes).</span></span> 

```azurecli-interactive
# Bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "NODE|6.9"
# PowerShell
az --% webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "NODE|6.9"
```

<span data-ttu-id="bcd14-133">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="bcd14-133">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

<span data-ttu-id="bcd14-134">Browse to your newly created web app.</span><span class="sxs-lookup"><span data-stu-id="bcd14-134">Browse to your newly created web app.</span></span> <span data-ttu-id="bcd14-135">Replace _&lt;app name>_ with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="bcd14-135">Replace _&lt;app name>_ with a unique app name.</span></span>

```bash
http://<app name>.azurewebsites.net
```

<span data-ttu-id="bcd14-136">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="bcd14-136">Here is what your new web app should look like:</span></span>

![Empty web app page](media/app-service-web-get-started-php/app-service-web-service-created.png)

[!INCLUDE [Deploy ZIP file](../../includes/app-service-web-deploy-zip.md)]

## <a name="browse-to-the-app"></a><span data-ttu-id="bcd14-138">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="bcd14-138">Browse to the app</span></span>

<span data-ttu-id="bcd14-139">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="bcd14-139">Browse to the deployed application using your web browser.</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="bcd14-140">The Node.js sample code is running in an Azure App Service web app.</span><span class="sxs-lookup"><span data-stu-id="bcd14-140">The Node.js sample code is running in an Azure App Service web app.</span></span>

![Sample app running in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="bcd14-142">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="bcd14-142">**Congratulations!**</span></span> <span data-ttu-id="bcd14-143">You've deployed your first Node.js app to App Service.</span><span class="sxs-lookup"><span data-stu-id="bcd14-143">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="bcd14-144">Update and redeploy the code</span><span class="sxs-lookup"><span data-stu-id="bcd14-144">Update and redeploy the code</span></span>

<span data-ttu-id="bcd14-145">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span><span class="sxs-lookup"><span data-stu-id="bcd14-145">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="bcd14-146">In the local terminal window, navigate to your application's root directory, create a new ZIP file for your updated project.</span><span class="sxs-lookup"><span data-stu-id="bcd14-146">In the local terminal window, navigate to your application's root directory, create a new ZIP file for your updated project.</span></span>

```
# Bash
zip -r myUpdatedAppFiles.zip .

# PowerShell
Compress-Archive -Path * -DestinationPath myUpdatedAppFiles.zip
``` 

<span data-ttu-id="bcd14-147">Deploy this new ZIP file to App Service, using the same steps in [Upload the ZIP file](#upload-the-zip-file).</span><span class="sxs-lookup"><span data-stu-id="bcd14-147">Deploy this new ZIP file to App Service, using the same steps in [Upload the ZIP file](#upload-the-zip-file).</span></span>

<span data-ttu-id="bcd14-148">Switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="bcd14-148">Switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Updated sample app running in Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="bcd14-150">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="bcd14-150">Manage your new Azure web app</span></span>

<span data-ttu-id="bcd14-151">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="bcd14-151">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="bcd14-152">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="bcd14-152">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="bcd14-154">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="bcd14-154">You see your web app's Overview page.</span></span> <span data-ttu-id="bcd14-155">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="bcd14-155">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service page in Azure portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="bcd14-157">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="bcd14-157">The left menu provides different pages for configuring your app.</span></span> 

## <a name="video"></a><span data-ttu-id="bcd14-158">Video</span><span class="sxs-lookup"><span data-stu-id="bcd14-158">Video</span></span>

<span data-ttu-id="bcd14-159">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first Node.js app on Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd14-159">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first Node.js app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="bcd14-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="bcd14-160">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bcd14-161">Node.js with MongoDB</span><span class="sxs-lookup"><span data-stu-id="bcd14-161">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
