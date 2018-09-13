---
title: Create a static HTML web app in Azure | Microsoft Docs
description: Learn how to run web apps in Azure App Service by deploying a static HTML sample app.
services: app-service\web
documentationcenter: ''
author: msangapu
manager: jeconnoc
editor: ''
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: msangapu
ms.custom: mvc
ms.openlocfilehash: cee0bdffb99076903df988d30fcaa4f6cb2234c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869883"
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="4d7de-103">Create a static HTML web app in Azure</span><span class="sxs-lookup"><span data-stu-id="4d7de-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="4d7de-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="4d7de-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="4d7de-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="4d7de-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="4d7de-106">You'll complete this quickstart in [Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4d7de-106">You'll complete this quickstart in [Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), but you can also run these commands locally with [Azure CLI](/cli/azure/install-azure-cli).</span></span>

![Home page of sample app](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="install-web-app-extension-for-cloud-shell"></a><span data-ttu-id="4d7de-108">Install web app extension for Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="4d7de-108">Install web app extension for Cloud Shell</span></span>

<span data-ttu-id="4d7de-109">To complete this quickstart, you need to add the [az web app extension](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-add).</span><span class="sxs-lookup"><span data-stu-id="4d7de-109">To complete this quickstart, you need to add the [az web app extension](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-add).</span></span> <span data-ttu-id="4d7de-110">If the extension is already installed, you should update it to the latest version.</span><span class="sxs-lookup"><span data-stu-id="4d7de-110">If the extension is already installed, you should update it to the latest version.</span></span> <span data-ttu-id="4d7de-111">To update the web app extension, type `az extension update -n webapp`.</span><span class="sxs-lookup"><span data-stu-id="4d7de-111">To update the web app extension, type `az extension update -n webapp`.</span></span>

<span data-ttu-id="4d7de-112">To install the webapp extension, run the following command:</span><span class="sxs-lookup"><span data-stu-id="4d7de-112">To install the webapp extension, run the following command:</span></span>

```bash
az extension add --name webapp
```

<span data-ttu-id="4d7de-113">When the extension has been installed, the Cloud Shell shows information to the following example:</span><span class="sxs-lookup"><span data-stu-id="4d7de-113">When the extension has been installed, the Cloud Shell shows information to the following example:</span></span>

```bash
The installed extension 'webapp' is in preview.
```

## <a name="download-the-sample"></a><span data-ttu-id="4d7de-114">Download the sample</span><span class="sxs-lookup"><span data-stu-id="4d7de-114">Download the sample</span></span>

<span data-ttu-id="4d7de-115">In the Cloud Shell, create a quickstart directory and then change to it.</span><span class="sxs-lookup"><span data-stu-id="4d7de-115">In the Cloud Shell, create a quickstart directory and then change to it.</span></span>

```bash
mkdir quickstart

cd quickstart
```

<span data-ttu-id="4d7de-116">Next, run the following command to clone the sample app repository to your quickstart directory.</span><span class="sxs-lookup"><span data-stu-id="4d7de-116">Next, run the following command to clone the sample app repository to your quickstart directory.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

## <a name="create-a-web-app"></a><span data-ttu-id="4d7de-117">Create a web app</span><span class="sxs-lookup"><span data-stu-id="4d7de-117">Create a web app</span></span>

<span data-ttu-id="4d7de-118">Change to the directory that contains the sample code and run the `az webapp up` command.</span><span class="sxs-lookup"><span data-stu-id="4d7de-118">Change to the directory that contains the sample code and run the `az webapp up` command.</span></span>

<span data-ttu-id="4d7de-119">In the following example, replace <app_name> with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="4d7de-119">In the following example, replace <app_name> with a unique app name.</span></span>

```bash
cd html-docs-hello-world

az webapp up --location westeurope --name <app_name>
```

<span data-ttu-id="4d7de-120">The `az webapp up` command does the following actions:</span><span class="sxs-lookup"><span data-stu-id="4d7de-120">The `az webapp up` command does the following actions:</span></span>

- <span data-ttu-id="4d7de-121">Create a default resource group.</span><span class="sxs-lookup"><span data-stu-id="4d7de-121">Create a default resource group.</span></span>

- <span data-ttu-id="4d7de-122">Create a default app service plan.</span><span class="sxs-lookup"><span data-stu-id="4d7de-122">Create a default app service plan.</span></span>

- <span data-ttu-id="4d7de-123">Create an app with the specified name.</span><span class="sxs-lookup"><span data-stu-id="4d7de-123">Create an app with the specified name.</span></span>

- <span data-ttu-id="4d7de-124">[Zip deploy](https://docs.microsoft.com/azure/app-service/app-service-deploy-zip) files from the current working directory to the web app.</span><span class="sxs-lookup"><span data-stu-id="4d7de-124">[Zip deploy](https://docs.microsoft.com/azure/app-service/app-service-deploy-zip) files from the current working directory to the web app.</span></span>

<span data-ttu-id="4d7de-125">This command may take a few minutes to run.</span><span class="sxs-lookup"><span data-stu-id="4d7de-125">This command may take a few minutes to run.</span></span> <span data-ttu-id="4d7de-126">While running, it displays information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="4d7de-126">While running, it displays information similar to the following example:</span></span>

```json
{
  "app_url": "https://<app_name>.azurewebsites.net",
  "location": "westeurope",
  "name": "<app_name>",
  "os": "Windows",
  "resourcegroup": "appsvc_rg_Windows_westeurope",
  "serverfarm": "appsvc_asp_Windows_westeurope",
  "sku": "FREE",
  "src_path": "/home/<username>/quickstart/html-docs-hello-world ",
  < JSON data removed for brevity. >
}
```

<span data-ttu-id="4d7de-127">Make a note of the `resourceGroup` value.</span><span class="sxs-lookup"><span data-stu-id="4d7de-127">Make a note of the `resourceGroup` value.</span></span> <span data-ttu-id="4d7de-128">You need it for the [clean up resources](#clean-up-resources) section.</span><span class="sxs-lookup"><span data-stu-id="4d7de-128">You need it for the [clean up resources](#clean-up-resources) section.</span></span>

## <a name="browse-to-the-app"></a><span data-ttu-id="4d7de-129">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="4d7de-129">Browse to the app</span></span>

<span data-ttu-id="4d7de-130">In a browser, go to the Azure web app URL: `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4d7de-130">In a browser, go to the Azure web app URL: `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="4d7de-131">The page is running as an Azure App Service web app.</span><span class="sxs-lookup"><span data-stu-id="4d7de-131">The page is running as an Azure App Service web app.</span></span>

![Sample app home page](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="4d7de-133">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="4d7de-133">**Congratulations!**</span></span> <span data-ttu-id="4d7de-134">You've deployed your first HTML app to App Service.</span><span class="sxs-lookup"><span data-stu-id="4d7de-134">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="4d7de-135">Update and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="4d7de-135">Update and redeploy the app</span></span>

<span data-ttu-id="4d7de-136">In the Cloud Shell, type `nano index.html` to open the nano text editor.</span><span class="sxs-lookup"><span data-stu-id="4d7de-136">In the Cloud Shell, type `nano index.html` to open the nano text editor.</span></span> <span data-ttu-id="4d7de-137">In the `<h1>` heading tag, change "Azure App Service - Sample Static HTML Site" to "Azure App Service", as shown below.</span><span class="sxs-lookup"><span data-stu-id="4d7de-137">In the `<h1>` heading tag, change "Azure App Service - Sample Static HTML Site" to "Azure App Service", as shown below.</span></span>

![Nano index.html](media/app-service-web-get-started-html/nano-index-html.png)

<span data-ttu-id="4d7de-139">Save your changes and exit nano.</span><span class="sxs-lookup"><span data-stu-id="4d7de-139">Save your changes and exit nano.</span></span> <span data-ttu-id="4d7de-140">Use the command `^O` to save and `^X` to exit.</span><span class="sxs-lookup"><span data-stu-id="4d7de-140">Use the command `^O` to save and `^X` to exit.</span></span>

<span data-ttu-id="4d7de-141">You'll now redeploy the app with the same `az webapp up` command.</span><span class="sxs-lookup"><span data-stu-id="4d7de-141">You'll now redeploy the app with the same `az webapp up` command.</span></span>

```bash
az webapp up --location westeurope --name <app_name>
```

<span data-ttu-id="4d7de-142">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="4d7de-142">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Updated sample app home page](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="4d7de-144">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="4d7de-144">Manage your new Azure web app</span></span>

<span data-ttu-id="4d7de-145">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="4d7de-145">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="4d7de-146">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="4d7de-146">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="4d7de-148">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="4d7de-148">You see your web app's Overview page.</span></span> <span data-ttu-id="4d7de-149">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="4d7de-149">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![App Service blade in Azure portal](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="4d7de-151">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="4d7de-151">The left menu provides different pages for configuring your app.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="4d7de-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4d7de-152">Clean up resources</span></span>

<span data-ttu-id="4d7de-153">In the preceding steps, you created Azure resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="4d7de-153">In the preceding steps, you created Azure resources in a resource group.</span></span> <span data-ttu-id="4d7de-154">If you don't expect to need these resources in the future, delete the resource group by running the following command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="4d7de-154">If you don't expect to need these resources in the future, delete the resource group by running the following command in the Cloud Shell.</span></span> <span data-ttu-id="4d7de-155">Remember that the resource group name was automatically generated for you in the [create a web app](#create-a-web-app) step.</span><span class="sxs-lookup"><span data-stu-id="4d7de-155">Remember that the resource group name was automatically generated for you in the [create a web app](#create-a-web-app) step.</span></span>

```bash
az group delete --name appsvc_rg_Windows_westeurope
```

<span data-ttu-id="4d7de-156">This command may take a minute to run.</span><span class="sxs-lookup"><span data-stu-id="4d7de-156">This command may take a minute to run.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d7de-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d7de-157">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4d7de-158">Map custom domain</span><span class="sxs-lookup"><span data-stu-id="4d7de-158">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
