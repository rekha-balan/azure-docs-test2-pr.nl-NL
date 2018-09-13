---
title: Create a Ruby App and deploy to App Service on Linux | Microsoft Docs
description: Learn to create Ruby apps with App Service on Linux.
keywords: azure app service, linux, oss, ruby
services: app-service
documentationcenter: ''
author: SyntaxC4
manager: cfowler
editor: ''
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 89ba823c021e85e3b6f2263080e3e5c7705dc6f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866697"
---
# <a name="create-a-ruby-app-in-app-service-on-linux"></a><span data-ttu-id="64ae6-104">Create a Ruby App in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="64ae6-104">Create a Ruby App in App Service on Linux</span></span>

<span data-ttu-id="64ae6-105">[Azure App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="64ae6-105">[Azure App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="64ae6-106">This quickstart shows you how to create a basic [Ruby on Rails](https://rubyonrails.org/) application that can then be deployed to Azure as a Web App on Linux.</span><span class="sxs-lookup"><span data-stu-id="64ae6-106">This quickstart shows you how to create a basic [Ruby on Rails](https://rubyonrails.org/) application that can then be deployed to Azure as a Web App on Linux.</span></span>

![Hello-world](./media/quickstart-ruby/hello-world-updated.png)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="64ae6-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="64ae6-108">Prerequisites</span></span>

* <span data-ttu-id="64ae6-109"><a href="https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller" target="_blank">Install Ruby 2.3 or higher</a></span><span class="sxs-lookup"><span data-stu-id="64ae6-109"><a href="https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller" target="_blank">Install Ruby 2.3 or higher</a></span></span>
* <span data-ttu-id="64ae6-110"><a href="https://git-scm.com/" target="_blank">Install Git</a></span><span class="sxs-lookup"><span data-stu-id="64ae6-110"><a href="https://git-scm.com/" target="_blank">Install Git</a></span></span>

## <a name="download-the-sample"></a><span data-ttu-id="64ae6-111">Download the sample</span><span class="sxs-lookup"><span data-stu-id="64ae6-111">Download the sample</span></span>

<span data-ttu-id="64ae6-112">In a terminal window, run the following command to clone the sample app repository to your local machine:</span><span class="sxs-lookup"><span data-stu-id="64ae6-112">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

## <a name="run-the-application-locally"></a><span data-ttu-id="64ae6-113">Run the application locally</span><span class="sxs-lookup"><span data-stu-id="64ae6-113">Run the application locally</span></span>

<span data-ttu-id="64ae6-114">Run the application locally so that you see how it should look when you deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="64ae6-114">Run the application locally so that you see how it should look when you deploy it to Azure.</span></span> <span data-ttu-id="64ae6-115">Open a terminal window, change to the `hello-world` directory, and use the `rails server` command to start the server.</span><span class="sxs-lookup"><span data-stu-id="64ae6-115">Open a terminal window, change to the `hello-world` directory, and use the `rails server` command to start the server.</span></span>

<span data-ttu-id="64ae6-116">The first step is to install the required gems.</span><span class="sxs-lookup"><span data-stu-id="64ae6-116">The first step is to install the required gems.</span></span> <span data-ttu-id="64ae6-117">There's a `Gemfile` included in the sample so you don't need to specify the gems to install.</span><span class="sxs-lookup"><span data-stu-id="64ae6-117">There's a `Gemfile` included in the sample so you don't need to specify the gems to install.</span></span> <span data-ttu-id="64ae6-118">We'll use bundler for this, and we'll save the gems locally in a `.gems` directory.</span><span class="sxs-lookup"><span data-stu-id="64ae6-118">We'll use bundler for this, and we'll save the gems locally in a `.gems` directory.</span></span> <span data-ttu-id="64ae6-119">Feel free to change the name if you like:</span><span class="sxs-lookup"><span data-stu-id="64ae6-119">Feel free to change the name if you like:</span></span>

```
bundle install --path=.gems
```

<span data-ttu-id="64ae6-120">Once the gems are installed, we'll use bundler to start the app for us:</span><span class="sxs-lookup"><span data-stu-id="64ae6-120">Once the gems are installed, we'll use bundler to start the app for us:</span></span>

```bash
bundle exec rails server
```

<span data-ttu-id="64ae6-121">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span><span class="sxs-lookup"><span data-stu-id="64ae6-121">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>

![Hello World configured](./media/quickstart-ruby/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux.md)]

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="64ae6-123">Create a web app</span><span class="sxs-lookup"><span data-stu-id="64ae6-123">Create a web app</span></span>

[!INCLUDE [Create web app](../../../includes/app-service-web-create-web-app-ruby-linux-no-h.md)] 

<span data-ttu-id="64ae6-124">Browse to the site to see your newly created web app with built-in image.</span><span class="sxs-lookup"><span data-stu-id="64ae6-124">Browse to the site to see your newly created web app with built-in image.</span></span> <span data-ttu-id="64ae6-125">Replace _&lt;app name>_ with your web app name.</span><span class="sxs-lookup"><span data-stu-id="64ae6-125">Replace _&lt;app name>_ with your web app name.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="64ae6-126">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="64ae6-126">Here is what your new web app should look like:</span></span>

![Splash page](./media/quickstart-ruby/splash-page.png)

## <a name="deploy-your-application"></a><span data-ttu-id="64ae6-128">Deploy your application</span><span class="sxs-lookup"><span data-stu-id="64ae6-128">Deploy your application</span></span>

<span data-ttu-id="64ae6-129">Run the following commands to deploy the local application to your Azure website:</span><span class="sxs-lookup"><span data-stu-id="64ae6-129">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="64ae6-130">Confirm that the remote deployment operations report success.</span><span class="sxs-lookup"><span data-stu-id="64ae6-130">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="64ae6-131">The commands produce output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="64ae6-131">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="64ae6-132">Once the deployment has completed, restart your web app for the deployment to take effect by using the [`az webapp restart`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-restart) command, as shown here:</span><span class="sxs-lookup"><span data-stu-id="64ae6-132">Once the deployment has completed, restart your web app for the deployment to take effect by using the [`az webapp restart`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-restart) command, as shown here:</span></span>

```azurecli-interactive
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="64ae6-133">Navigate to your site and verify the results.</span><span class="sxs-lookup"><span data-stu-id="64ae6-133">Navigate to your site and verify the results.</span></span>

```bash
http://<app name>.azurewebsites.net
```

![updated web app](./media/quickstart-ruby/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="64ae6-135">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="64ae6-135">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="64ae6-136">It may take a few minutes to fully restart.</span><span class="sxs-lookup"><span data-stu-id="64ae6-136">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../../includes/cli-script-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="64ae6-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="64ae6-137">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64ae6-138">Ruby on Rails with MySQL</span><span class="sxs-lookup"><span data-stu-id="64ae6-138">Ruby on Rails with MySQL</span></span>](tutorial-ruby-postgres-app.md)
