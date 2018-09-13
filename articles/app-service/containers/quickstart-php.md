---
title: Create a PHP web app and deploy to App Service on Linux | Microsoft Docs
description: Deploy your first PHP Hello World in App Service on Linux in minutes.
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/30/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5fdf277eb8f99f2d52600140601b413b51bcdfd8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968200"
---
# <a name="create-a-php-web-app-in-app-service-on-linux"></a><span data-ttu-id="30808-103">Create a PHP web app in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="30808-103">Create a PHP web app in App Service on Linux</span></span>

> [!NOTE]
> <span data-ttu-id="30808-104">This article deploys an app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="30808-104">This article deploys an app to App Service on Linux.</span></span> <span data-ttu-id="30808-105">To deploy to App Service on _Windows_, see [Create a PHP web app in Azure](../app-service-web-get-started-php.md).</span><span class="sxs-lookup"><span data-stu-id="30808-105">To deploy to App Service on _Windows_, see [Create a PHP web app in Azure](../app-service-web-get-started-php.md).</span></span>
>

<span data-ttu-id="30808-106">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="30808-106">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="30808-107">This quickstart tutorial shows how to deploy a PHP app to Azure App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="30808-107">This quickstart tutorial shows how to deploy a PHP app to Azure App Service on Linux.</span></span> <span data-ttu-id="30808-108">You create the web app with built-in image using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy the PHP code to the web app.</span><span class="sxs-lookup"><span data-stu-id="30808-108">You create the web app with built-in image using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy the PHP code to the web app.</span></span>

![Sample app running in Azure](media/quickstart-php/hello-world-in-browser.png)

<span data-ttu-id="30808-110">You can follow the steps in this article using a Mac, Windows, or Linux machine.</span><span class="sxs-lookup"><span data-stu-id="30808-110">You can follow the steps in this article using a Mac, Windows, or Linux machine.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="30808-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="30808-111">Prerequisites</span></span>

<span data-ttu-id="30808-112">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="30808-112">To complete this quickstart:</span></span>

* <span data-ttu-id="30808-113"><a href="https://git-scm.com/" target="_blank">Install Git</a></span><span class="sxs-lookup"><span data-stu-id="30808-113"><a href="https://git-scm.com/" target="_blank">Install Git</a></span></span>
* <span data-ttu-id="30808-114"><a href="https://php.net" target="_blank">Install PHP</a></span><span class="sxs-lookup"><span data-stu-id="30808-114"><a href="https://php.net" target="_blank">Install PHP</a></span></span>

## <a name="download-the-sample"></a><span data-ttu-id="30808-115">Download the sample</span><span class="sxs-lookup"><span data-stu-id="30808-115">Download the sample</span></span>

<span data-ttu-id="30808-116">In a terminal window, run the following commands to clone the sample application to your local machine, and navigate to the directory containing the sample code.</span><span class="sxs-lookup"><span data-stu-id="30808-116">In a terminal window, run the following commands to clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="30808-117">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="30808-117">Run the app locally</span></span>

<span data-ttu-id="30808-118">Run the application locally so that you see how it should look when you deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="30808-118">Run the application locally so that you see how it should look when you deploy it to Azure.</span></span> <span data-ttu-id="30808-119">Open a terminal window and use the `php` command to launch the built-in PHP web server.</span><span class="sxs-lookup"><span data-stu-id="30808-119">Open a terminal window and use the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="30808-120">Open a web browser, and navigate to the sample app at `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="30808-120">Open a web browser, and navigate to the sample app at `http://localhost:8080`.</span></span>

<span data-ttu-id="30808-121">You see the **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="30808-121">You see the **Hello World!**</span></span> <span data-ttu-id="30808-122">message from the sample app displayed in the page.</span><span class="sxs-lookup"><span data-stu-id="30808-122">message from the sample app displayed in the page.</span></span>

![Sample app running locally](media/quickstart-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="30808-124">In your terminal window, press **Ctrl+C** to exit the web server.</span><span class="sxs-lookup"><span data-stu-id="30808-124">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux.md)]

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="30808-125">Create a web app</span><span class="sxs-lookup"><span data-stu-id="30808-125">Create a web app</span></span>

[!INCLUDE [Create web app](../../../includes/app-service-web-create-web-app-php-linux-no-h.md)] 

<span data-ttu-id="30808-126">Browse to the site to see your newly created web app with built-in image.</span><span class="sxs-lookup"><span data-stu-id="30808-126">Browse to the site to see your newly created web app with built-in image.</span></span> <span data-ttu-id="30808-127">Replace _&lt;app name>_ with your web app name.</span><span class="sxs-lookup"><span data-stu-id="30808-127">Replace _&lt;app name>_ with your web app name.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="30808-128">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="30808-128">Here is what your new web app should look like:</span></span>

![Empty web app page](media/quickstart-php/app-service-web-service-created.png)

[!INCLUDE [Push to Azure](../../../includes/app-service-web-git-push-to-azure.md)] 

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

## <a name="browse-to-the-app"></a><span data-ttu-id="30808-130">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="30808-130">Browse to the app</span></span>

<span data-ttu-id="30808-131">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="30808-131">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="30808-132">The PHP sample code is running in a web app with built-in image.</span><span class="sxs-lookup"><span data-stu-id="30808-132">The PHP sample code is running in a web app with built-in image.</span></span>

![Sample app running in Azure](media/quickstart-php/hello-world-in-browser.png)

<span data-ttu-id="30808-134">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="30808-134">**Congratulations!**</span></span> <span data-ttu-id="30808-135">You've deployed your first PHP app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="30808-135">You've deployed your first PHP app to App Service on Linux.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="30808-136">Update locally and redeploy the code</span><span class="sxs-lookup"><span data-stu-id="30808-136">Update locally and redeploy the code</span></span>

<span data-ttu-id="30808-137">In the local directory, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span><span class="sxs-lookup"><span data-stu-id="30808-137">In the local directory, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="30808-138">Commit your changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="30808-138">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="30808-139">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="30808-139">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Updated sample app running in Azure](media/quickstart-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="30808-141">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="30808-141">Manage your new Azure web app</span></span>

<span data-ttu-id="30808-142">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="30808-142">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="30808-143">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="30808-143">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/quickstart-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="30808-145">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="30808-145">You see your web app's Overview page.</span></span> <span data-ttu-id="30808-146">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="30808-146">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![App Service page in Azure portal](media/quickstart-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="30808-148">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="30808-148">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="30808-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="30808-149">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30808-150">PHP with MySQL</span><span class="sxs-lookup"><span data-stu-id="30808-150">PHP with MySQL</span></span>](tutorial-php-mysql-app.md)
