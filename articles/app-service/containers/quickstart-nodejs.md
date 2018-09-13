---
title: Create a Node.js in Azure App Service on Linux | Microsoft Docs
description: Deploy your first Node.js Hello World in Azure App Service on Linux in minutes.
services: app-service\web
documentationcenter: ''
author: msangapu
manager: cfowler
editor: ''
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/07/2017
ms.author: msangapu
ms.custom: mvc
ms.openlocfilehash: 44c3f8ce05854e993ad551a025eec447d882c326
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867443"
---
# <a name="create-a-nodejs-web-app-in-azure-app-service-on-linux"></a><span data-ttu-id="9442a-103">Create a Node.js web app in Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="9442a-103">Create a Node.js web app in Azure App Service on Linux</span></span>

> [!NOTE]
> <span data-ttu-id="9442a-104">This article deploys an app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="9442a-104">This article deploys an app to App Service on Linux.</span></span> <span data-ttu-id="9442a-105">To deploy to App Service on _Windows_, see [Create a Node.js web app in Azure](../app-service-web-get-started-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9442a-105">To deploy to App Service on _Windows_, see [Create a Node.js web app in Azure](../app-service-web-get-started-nodejs.md).</span></span>
>

<span data-ttu-id="9442a-106">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="9442a-106">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="9442a-107">This quickstart shows how to deploy a Node.js app to App Service on Linux using the [Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="9442a-107">This quickstart shows how to deploy a Node.js app to App Service on Linux using the [Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

<span data-ttu-id="9442a-108">You'll complete this quickstart in Cloud Shell, but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9442a-108">You'll complete this quickstart in Cloud Shell, but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli).</span></span>

![Sample app running in Azure](media/quickstart-nodejs/hello-world-in-browser.png)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="install-web-app-extension-for-cloud-shell"></a><span data-ttu-id="9442a-110">Install web app extension for Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="9442a-110">Install web app extension for Cloud Shell</span></span>

<span data-ttu-id="9442a-111">To complete this quickstart, you will need to add the [az web app extension](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-add).</span><span class="sxs-lookup"><span data-stu-id="9442a-111">To complete this quickstart, you will need to add the [az web app extension](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-add).</span></span> <span data-ttu-id="9442a-112">If the extension is already installed, you should update it to the latest version.</span><span class="sxs-lookup"><span data-stu-id="9442a-112">If the extension is already installed, you should update it to the latest version.</span></span> <span data-ttu-id="9442a-113">To update the web app extension, type `az extension update -n webapp`.</span><span class="sxs-lookup"><span data-stu-id="9442a-113">To update the web app extension, type `az extension update -n webapp`.</span></span>

<span data-ttu-id="9442a-114">To install the webapp extension, run the following command:</span><span class="sxs-lookup"><span data-stu-id="9442a-114">To install the webapp extension, run the following command:</span></span>

```bash
az extension add -n webapp
```

<span data-ttu-id="9442a-115">When the extension has been installed, the Cloud Shell shows information to the following example:</span><span class="sxs-lookup"><span data-stu-id="9442a-115">When the extension has been installed, the Cloud Shell shows information to the following example:</span></span>

```bash
The installed extension 'webapp' is in preview.
```

## <a name="download-the-sample"></a><span data-ttu-id="9442a-116">Download the sample</span><span class="sxs-lookup"><span data-stu-id="9442a-116">Download the sample</span></span>

<span data-ttu-id="9442a-117">In the Cloud Shell, create a quickstart directory and then change to it.</span><span class="sxs-lookup"><span data-stu-id="9442a-117">In the Cloud Shell, create a quickstart directory and then change to it.</span></span>

```bash
mkdir quickstart

cd quickstart
```

<span data-ttu-id="9442a-118">Next, run the following command to clone the sample app repository to your quickstart directory.</span><span class="sxs-lookup"><span data-stu-id="9442a-118">Next, run the following command to clone the sample app repository to your quickstart directory.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="9442a-119">While running, it displays information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="9442a-119">While running, it displays information similar to the following example:</span></span>

```bash
Cloning into 'nodejs-docs-hello-world'...
remote: Counting objects: 40, done.
remote: Total 40 (delta 0), reused 0 (delta 0), pack-reused 40
Unpacking objects: 100% (40/40), done.
Checking connectivity... done.
````

## <a name="create-a-web-app"></a><span data-ttu-id="9442a-120">Create a web app</span><span class="sxs-lookup"><span data-stu-id="9442a-120">Create a web app</span></span>

<span data-ttu-id="9442a-121">Change to the directory that contains the sample code and run the `az webapp up` command.</span><span class="sxs-lookup"><span data-stu-id="9442a-121">Change to the directory that contains the sample code and run the `az webapp up` command.</span></span>

<span data-ttu-id="9442a-122">In the following example, replace <app_name> with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="9442a-122">In the following example, replace <app_name> with a unique app name.</span></span>

```bash
cd nodejs-docs-hello-world

az webapp up -n <app_name>
```

<span data-ttu-id="9442a-123">This command may take a few minutes to run.</span><span class="sxs-lookup"><span data-stu-id="9442a-123">This command may take a few minutes to run.</span></span> <span data-ttu-id="9442a-124">While running, it displays information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="9442a-124">While running, it displays information similar to the following example:</span></span>

```json
Creating Resource group 'appsvc_rg_Linux_CentralUS' ...
Resource group creation complete
Creating App service plan 'appsvc_asp_Linux_CentralUS' ...
App service plan creation complete
Creating app '<app_name>' ....
Webapp creation complete
Updating app settings to enable build after deployment
Creating zip with contents of dir /home/username/quickstart/nodejs-docs-hello-world ...
Preparing to deploy and build contents to app.
Fetching changes.

Generating deployment script.
Generating deployment script.
Generating deployment script.
Running deployment command...
Running deployment command...
Running deployment command...
Deployment successful.
All done.
{
  "app_url": "https://<app_name>.azurewebsites.net",
  "location": "Central US",
  "name": "<app_name>",
  "os": "Linux",
  "resourcegroup": "appsvc_rg_Linux_CentralUS ",
  "serverfarm": "appsvc_asp_Linux_CentralUS",
  "sku": "STANDARD",
  "src_path": "/home/username/quickstart/nodejs-docs-hello-world ",
  "version_detected": "6.9",
  "version_to_create": "node|6.9"
}
```

<span data-ttu-id="9442a-125">The `az webapp up` command does the following actions:</span><span class="sxs-lookup"><span data-stu-id="9442a-125">The `az webapp up` command does the following actions:</span></span>

- <span data-ttu-id="9442a-126">Create a default resource group.</span><span class="sxs-lookup"><span data-stu-id="9442a-126">Create a default resource group.</span></span>

- <span data-ttu-id="9442a-127">Create a default app service plan.</span><span class="sxs-lookup"><span data-stu-id="9442a-127">Create a default app service plan.</span></span>

- <span data-ttu-id="9442a-128">Create an app with the specified name.</span><span class="sxs-lookup"><span data-stu-id="9442a-128">Create an app with the specified name.</span></span>

- <span data-ttu-id="9442a-129">[Zip deploy](https://docs.microsoft.com/azure/app-service/app-service-deploy-zip) files from the current working directory to the web app.</span><span class="sxs-lookup"><span data-stu-id="9442a-129">[Zip deploy](https://docs.microsoft.com/azure/app-service/app-service-deploy-zip) files from the current working directory to the web app.</span></span>

## <a name="browse-to-the-app"></a><span data-ttu-id="9442a-130">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="9442a-130">Browse to the app</span></span>

<span data-ttu-id="9442a-131">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="9442a-131">Browse to the deployed application using your web browser.</span></span> <span data-ttu-id="9442a-132">Replace <app_name> with your web app name.</span><span class="sxs-lookup"><span data-stu-id="9442a-132">Replace <app_name> with your web app name.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="9442a-133">The Node.js sample code is running in a web app with built-in image.</span><span class="sxs-lookup"><span data-stu-id="9442a-133">The Node.js sample code is running in a web app with built-in image.</span></span>

![Sample app running in Azure](media/quickstart-nodejs/hello-world-in-browser.png)

<span data-ttu-id="9442a-135">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="9442a-135">**Congratulations!**</span></span> <span data-ttu-id="9442a-136">You've deployed your first Node.js app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="9442a-136">You've deployed your first Node.js app to App Service on Linux.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="9442a-137">Update and redeploy the code</span><span class="sxs-lookup"><span data-stu-id="9442a-137">Update and redeploy the code</span></span>

<span data-ttu-id="9442a-138">In the Cloud Shell, type `nano index.js` to open the nano text editor.</span><span class="sxs-lookup"><span data-stu-id="9442a-138">In the Cloud Shell, type `nano index.js` to open the nano text editor.</span></span>

![Nano index.js](media/quickstart-nodejs/nano-indexjs.png)

 <span data-ttu-id="9442a-140">Make a small change to the text in the call to `response.end`:</span><span class="sxs-lookup"><span data-stu-id="9442a-140">Make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="9442a-141">Save your changes and exit nano.</span><span class="sxs-lookup"><span data-stu-id="9442a-141">Save your changes and exit nano.</span></span> <span data-ttu-id="9442a-142">Use the command `^O` to save and `^X` to exit.</span><span class="sxs-lookup"><span data-stu-id="9442a-142">Use the command `^O` to save and `^X` to exit.</span></span>

<span data-ttu-id="9442a-143">You'll now redeploy the app.</span><span class="sxs-lookup"><span data-stu-id="9442a-143">You'll now redeploy the app.</span></span> <span data-ttu-id="9442a-144">Substitute `<app_name>` with your web app.</span><span class="sxs-lookup"><span data-stu-id="9442a-144">Substitute `<app_name>` with your web app.</span></span>

```bash
az webapp up -n <app_name>
```

<span data-ttu-id="9442a-145">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="9442a-145">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Updated sample app running in Azure](media/quickstart-nodejs/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="9442a-147">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="9442a-147">Manage your new Azure web app</span></span>

<span data-ttu-id="9442a-148">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="9442a-148">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="9442a-149">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="9442a-149">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/quickstart-nodejs/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="9442a-151">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="9442a-151">You see your web app's Overview page.</span></span> <span data-ttu-id="9442a-152">Here, you can complete basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="9442a-152">Here, you can complete basic management tasks like browse, stop, start, restart, and delete.</span></span>

![App Service page in Azure portal](media/quickstart-nodejs/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="9442a-154">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="9442a-154">The left menu provides different pages for configuring your app.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9442a-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9442a-155">Clean up resources</span></span>

<span data-ttu-id="9442a-156">In the preceding steps, you created Azure resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="9442a-156">In the preceding steps, you created Azure resources in a resource group.</span></span> <span data-ttu-id="9442a-157">If you don't expect to need these resources in the future, delete the resource group from the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9442a-157">If you don't expect to need these resources in the future, delete the resource group from the Cloud Shell.</span></span> <span data-ttu-id="9442a-158">If you modified the region, update the resource group name `appsvc_rg_Linux_CentralUS` to the resource group specific to your app.</span><span class="sxs-lookup"><span data-stu-id="9442a-158">If you modified the region, update the resource group name `appsvc_rg_Linux_CentralUS` to the resource group specific to your app.</span></span>

```azurecli-interactive
az group delete --name appsvc_rg_Linux_CentralUS
```

<span data-ttu-id="9442a-159">This command may take a minute to run.</span><span class="sxs-lookup"><span data-stu-id="9442a-159">This command may take a minute to run.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9442a-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="9442a-160">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9442a-161">Node.js with MongoDB</span><span class="sxs-lookup"><span data-stu-id="9442a-161">Node.js with MongoDB</span></span>](tutorial-nodejs-mongodb-app.md)
