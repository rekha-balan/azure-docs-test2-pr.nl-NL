---
title: Create a PHP web app in Azure | Microsoft Docs
description: Deploy your first PHP Hello World in Azure App Service Web Apps in minutes.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: cephalin;cfowler
ms.custom: mvc
ms.openlocfilehash: 0dd8f90a39abc18263fcaa5bdb63a5b743728952
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866189"
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="b0b70-103">Create a PHP web app in Azure</span><span class="sxs-lookup"><span data-stu-id="b0b70-103">Create a PHP web app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="b0b70-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="b0b70-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="b0b70-105">To deploy to App Service on _Linux_, see [Create a PHP web app in App Service on Linux](./containers/quickstart-php.md).</span><span class="sxs-lookup"><span data-stu-id="b0b70-105">To deploy to App Service on _Linux_, see [Create a PHP web app in App Service on Linux](./containers/quickstart-php.md).</span></span>
>

<span data-ttu-id="b0b70-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="b0b70-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="b0b70-107">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="b0b70-107">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="b0b70-108">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span><span class="sxs-lookup"><span data-stu-id="b0b70-108">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

![Sample app running in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="b0b70-110">You can follow the steps here using a Mac, Windows, or Linux machine.</span><span class="sxs-lookup"><span data-stu-id="b0b70-110">You can follow the steps here using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="b0b70-111">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span><span class="sxs-lookup"><span data-stu-id="b0b70-111">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="b0b70-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0b70-112">Prerequisites</span></span>

<span data-ttu-id="b0b70-113">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="b0b70-113">To complete this quickstart:</span></span>

* <span data-ttu-id="b0b70-114"><a href="https://git-scm.com/" target="_blank">Install Git</a></span><span class="sxs-lookup"><span data-stu-id="b0b70-114"><a href="https://git-scm.com/" target="_blank">Install Git</a></span></span>
* <span data-ttu-id="b0b70-115"><a href="http://php.net/manual/install.php" target="_blank">Install PHP</a></span><span class="sxs-lookup"><span data-stu-id="b0b70-115"><a href="http://php.net/manual/install.php" target="_blank">Install PHP</a></span></span>

## <a name="download-the-sample-locally"></a><span data-ttu-id="b0b70-116">Download the sample locally</span><span class="sxs-lookup"><span data-stu-id="b0b70-116">Download the sample locally</span></span>

<span data-ttu-id="b0b70-117">In a terminal window, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="b0b70-117">In a terminal window, run the following commands.</span></span> <span data-ttu-id="b0b70-118">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span><span class="sxs-lookup"><span data-stu-id="b0b70-118">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span> 

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="b0b70-119">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="b0b70-119">Run the app locally</span></span>

<span data-ttu-id="b0b70-120">Run the application locally so that you see how it should look when you deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b70-120">Run the application locally so that you see how it should look when you deploy it to Azure.</span></span> <span data-ttu-id="b0b70-121">Open a terminal window and use the `php` command to launch the built-in PHP web server.</span><span class="sxs-lookup"><span data-stu-id="b0b70-121">Open a terminal window and use the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="b0b70-122">Open a web browser, and navigate to the sample app at `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="b0b70-122">Open a web browser, and navigate to the sample app at `http://localhost:8080`.</span></span>

<span data-ttu-id="b0b70-123">You see the **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="b0b70-123">You see the **Hello World!**</span></span> <span data-ttu-id="b0b70-124">message from the sample app displayed in the page.</span><span class="sxs-lookup"><span data-stu-id="b0b70-124">message from the sample app displayed in the page.</span></span>

![Sample app running locally](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="b0b70-126">In your terminal window, press **Ctrl+C** to exit the web server.</span><span class="sxs-lookup"><span data-stu-id="b0b70-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="b0b70-127">Create a web app</span><span class="sxs-lookup"><span data-stu-id="b0b70-127">Create a web app</span></span>

<span data-ttu-id="b0b70-128">In the Cloud Shell, create a web app in the `myAppServicePlan` App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="b0b70-128">In the Cloud Shell, create a web app in the `myAppServicePlan` App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> 

<span data-ttu-id="b0b70-129">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="b0b70-129">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="b0b70-130">The runtime is set to `PHP|7.0`.</span><span class="sxs-lookup"><span data-stu-id="b0b70-130">The runtime is set to `PHP|7.0`.</span></span> <span data-ttu-id="b0b70-131">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-list-runtimes).</span><span class="sxs-lookup"><span data-stu-id="b0b70-131">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-list-runtimes).</span></span> 

```azurecli-interactive
# Bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "PHP|7.0" --deployment-local-git
# PowerShell
az --% webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "PHP|7.0" --deployment-local-git
```

<span data-ttu-id="b0b70-132">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="b0b70-132">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

```json
Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'
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
<span data-ttu-id="b0b70-133">You’ve created an empty new web app, with git deployment enabled.</span><span class="sxs-lookup"><span data-stu-id="b0b70-133">You’ve created an empty new web app, with git deployment enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="b0b70-134">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span><span class="sxs-lookup"><span data-stu-id="b0b70-134">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span></span> <span data-ttu-id="b0b70-135">Save this URL as you need it later.</span><span class="sxs-lookup"><span data-stu-id="b0b70-135">Save this URL as you need it later.</span></span>
>

<span data-ttu-id="b0b70-136">Browse to your newly created web app.</span><span class="sxs-lookup"><span data-stu-id="b0b70-136">Browse to your newly created web app.</span></span> <span data-ttu-id="b0b70-137">Replace _&lt;app name>_ with your unique app name created in the prior step.</span><span class="sxs-lookup"><span data-stu-id="b0b70-137">Replace _&lt;app name>_ with your unique app name created in the prior step.</span></span>

```bash
http://<app name>.azurewebsites.net
```

<span data-ttu-id="b0b70-138">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="b0b70-138">Here is what your new web app should look like:</span></span>

![Empty web app page](media/app-service-web-get-started-php/app-service-web-service-created.png)

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="b0b70-140">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="b0b70-140">Browse to the app</span></span>

<span data-ttu-id="b0b70-141">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="b0b70-141">Browse to the deployed application using your web browser.</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="b0b70-142">The PHP sample code is running in an Azure App Service web app.</span><span class="sxs-lookup"><span data-stu-id="b0b70-142">The PHP sample code is running in an Azure App Service web app.</span></span>

![Sample app running in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="b0b70-144">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="b0b70-144">**Congratulations!**</span></span> <span data-ttu-id="b0b70-145">You've deployed your first PHP app to App Service.</span><span class="sxs-lookup"><span data-stu-id="b0b70-145">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="b0b70-146">Update locally and redeploy the code</span><span class="sxs-lookup"><span data-stu-id="b0b70-146">Update locally and redeploy the code</span></span>

<span data-ttu-id="b0b70-147">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span><span class="sxs-lookup"><span data-stu-id="b0b70-147">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="b0b70-148">In the local terminal window, commit your changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b70-148">In the local terminal window, commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="b0b70-149">Once deployment has completed, return to the browser window that opened during the **Browse to the app** step, and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="b0b70-149">Once deployment has completed, return to the browser window that opened during the **Browse to the app** step, and refresh the page.</span></span>

![Updated sample app running in Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="b0b70-151">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="b0b70-151">Manage your new Azure web app</span></span>

<span data-ttu-id="b0b70-152">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="b0b70-152">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="b0b70-153">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b0b70-153">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="b0b70-155">Your web app's Overview page will be displayed.</span><span class="sxs-lookup"><span data-stu-id="b0b70-155">Your web app's Overview page will be displayed.</span></span> <span data-ttu-id="b0b70-156">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="b0b70-156">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![App Service page in Azure portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="b0b70-158">The left menu provides different options for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="b0b70-158">The left menu provides different options for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="b0b70-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0b70-159">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b0b70-160">PHP with MySQL</span><span class="sxs-lookup"><span data-stu-id="b0b70-160">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
