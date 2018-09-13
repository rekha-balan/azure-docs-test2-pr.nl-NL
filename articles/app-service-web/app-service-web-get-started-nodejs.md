---
title: Create a Node.js Application on Web App | Microsoft Docs
description: Deploy your first Node.js Hello World in App Service Web App in minutes.
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/28/2017
ms.author: cfowler
ms.openlocfilehash: 29ed8ec15e2c66c8e24e59feea36092688b0ad78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564016"
---
# <a name="create-a-nodejs-application-on-web-app"></a><span data-ttu-id="f1243-103">Create a Node.js Application on Web App</span><span class="sxs-lookup"><span data-stu-id="f1243-103">Create a Node.js Application on Web App</span></span>

<span data-ttu-id="f1243-104">This quickstart tutorial walks through how to develop and deploy a Node.js app to Azure.</span><span class="sxs-lookup"><span data-stu-id="f1243-104">This quickstart tutorial walks through how to develop and deploy a Node.js app to Azure.</span></span> <span data-ttu-id="f1243-105">We’ll run the app using a Linux-based Azure App Service, and create and configure a new Web App within it using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f1243-105">We’ll run the app using a Linux-based Azure App Service, and create and configure a new Web App within it using the Azure CLI.</span></span> <span data-ttu-id="f1243-106">We’ll then use git to deploy our Node.js app to Azure.</span><span class="sxs-lookup"><span data-stu-id="f1243-106">We’ll then use git to deploy our Node.js app to Azure.</span></span>

![hello-world-in-browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="f1243-108">You can follow the steps below using a Mac, Windows or Linux machine.</span><span class="sxs-lookup"><span data-stu-id="f1243-108">You can follow the steps below using a Mac, Windows or Linux machine.</span></span> <span data-ttu-id="f1243-109">It should take you only about 5 minutes to complete all of the steps below.</span><span class="sxs-lookup"><span data-stu-id="f1243-109">It should take you only about 5 minutes to complete all of the steps below.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f1243-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f1243-110">Before you begin</span></span>

<span data-ttu-id="f1243-111">Before running this sample, install the following prerequisites locally:</span><span class="sxs-lookup"><span data-stu-id="f1243-111">Before running this sample, install the following prerequisites locally:</span></span>

1. [<span data-ttu-id="f1243-112">Download and install git</span><span class="sxs-lookup"><span data-stu-id="f1243-112">Download and install git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="f1243-113">Download and install Node.js and NPM</span><span class="sxs-lookup"><span data-stu-id="f1243-113">Download and install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="f1243-114">Download and install the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="f1243-114">Download and install the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="f1243-115">Download the sample</span><span class="sxs-lookup"><span data-stu-id="f1243-115">Download the sample</span></span>

<span data-ttu-id="f1243-116">Clone the Hello World sample app repository to your local machine.</span><span class="sxs-lookup"><span data-stu-id="f1243-116">Clone the Hello World sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

> [!TIP]
> <span data-ttu-id="f1243-117">Alternatively, you can [download the sample](https://github.com/Azure-Samples/nodejs-docs-hello-world/archive/master.zip) as a zip file and extract it.</span><span class="sxs-lookup"><span data-stu-id="f1243-117">Alternatively, you can [download the sample](https://github.com/Azure-Samples/nodejs-docs-hello-world/archive/master.zip) as a zip file and extract it.</span></span>

<span data-ttu-id="f1243-118">Change to the directory that contains the sample code.</span><span class="sxs-lookup"><span data-stu-id="f1243-118">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="f1243-119">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="f1243-119">Run the app locally</span></span>

<span data-ttu-id="f1243-120">Run the application locally by opening a terminal window and using the `npm start` script for the sample to launch the built in Node.js http server.</span><span class="sxs-lookup"><span data-stu-id="f1243-120">Run the application locally by opening a terminal window and using the `npm start` script for the sample to launch the built in Node.js http server.</span></span>

```bash
npm start
```

<span data-ttu-id="f1243-121">Open a web browser, and navigate to the sample.</span><span class="sxs-lookup"><span data-stu-id="f1243-121">Open a web browser, and navigate to the sample.</span></span>

```bash
http://localhost:1337
```

<span data-ttu-id="f1243-122">You can see the **Hello World** message from the sample app displayed in the page.</span><span class="sxs-lookup"><span data-stu-id="f1243-122">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![localhost-hello-world-in-browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="f1243-124">In your terminal window, press **Ctrl+C** to exit the web server.</span><span class="sxs-lookup"><span data-stu-id="f1243-124">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="f1243-125">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="f1243-125">Log in to Azure</span></span>

<span data-ttu-id="f1243-126">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1243-126">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span> <span data-ttu-id="f1243-127">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="f1243-127">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="configure-a-deployment-user"></a><span data-ttu-id="f1243-128">Configure a Deployment User</span><span class="sxs-lookup"><span data-stu-id="f1243-128">Configure a Deployment User</span></span>

<span data-ttu-id="f1243-129">For FTP and local Git it is necessary to have a deployment user configured on the server to authenicate your deployment.</span><span class="sxs-lookup"><span data-stu-id="f1243-129">For FTP and local Git it is necessary to have a deployment user configured on the server to authenicate your deployment.</span></span> <span data-ttu-id="f1243-130">Creating a deployment user is a one time configuration, take a note of the username and password as they will be used in a step below.</span><span class="sxs-lookup"><span data-stu-id="f1243-130">Creating a deployment user is a one time configuration, take a note of the username and password as they will be used in a step below.</span></span>

> [!NOTE]
> <span data-ttu-id="f1243-131">A deployment user is required for FTP and Local Git deployment to a Web App.</span><span class="sxs-lookup"><span data-stu-id="f1243-131">A deployment user is required for FTP and Local Git deployment to a Web App.</span></span>
> <span data-ttu-id="f1243-132">The `username` and `password` are account-level, as such, are different from your Azure Subscription credentials.</span><span class="sxs-lookup"><span data-stu-id="f1243-132">The `username` and `password` are account-level, as such, are different from your Azure Subscription credentials.</span></span> <span data-ttu-id="f1243-133">These credentials are only required to be created once.</span><span class="sxs-lookup"><span data-stu-id="f1243-133">These credentials are only required to be created once.</span></span>
>

<span data-ttu-id="f1243-134">Use the [az appservice web deployment user set](/cli/azure/appservice/web/deployment/user#set) command to create your account-level credentials.</span><span class="sxs-lookup"><span data-stu-id="f1243-134">Use the [az appservice web deployment user set](/cli/azure/appservice/web/deployment/user#set) command to create your account-level credentials.</span></span>

```azurecli
az appservice web deployment user set --user-name <username> --password <password>
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f1243-135">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f1243-135">Create a resource group</span></span>

<span data-ttu-id="f1243-136">Create a resource group with the [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f1243-136">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f1243-137">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f1243-137">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

## <a name="create-an-azure-app-service"></a><span data-ttu-id="f1243-138">Create an Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f1243-138">Create an Azure App Service</span></span>

<span data-ttu-id="f1243-139">Create a Linux-based App Service Plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span><span class="sxs-lookup"><span data-stu-id="f1243-139">Create a Linux-based App Service Plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="f1243-140">An App Service plan represents the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="f1243-140">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="f1243-141">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="f1243-141">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="f1243-142">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="f1243-142">App Service plans define:</span></span>
> * <span data-ttu-id="f1243-143">Region (North Europe, East US, Southeast Asia)</span><span class="sxs-lookup"><span data-stu-id="f1243-143">Region (North Europe, East US, Southeast Asia)</span></span>
> * <span data-ttu-id="f1243-144">Instance Size (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="f1243-144">Instance Size (Small, Medium, Large)</span></span>
> * <span data-ttu-id="f1243-145">Scale Count (one, two or three instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="f1243-145">Scale Count (one, two or three instances, etc.)</span></span>
> * <span data-ttu-id="f1243-146">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="f1243-146">SKU (Free, Shared, Basic, Standard, Premium)</span></span>
>

<span data-ttu-id="f1243-147">The following example creates an App Service Plan on Linux Workers named `quickStartPlan` using the **Standard** pricing tier.</span><span class="sxs-lookup"><span data-stu-id="f1243-147">The following example creates an App Service Plan on Linux Workers named `quickStartPlan` using the **Standard** pricing tier.</span></span>

```azurecli
az appservice plan create --name quickStartPlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="f1243-148">When the App Service Plan has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f1243-148">When the App Service Plan has been created, the Azure CLI shows information similar to the following example.</span></span>

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/quickStartPlan",
    "kind": "linux",
    "location": "West Europe",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```

## <a name="create-a-web-app"></a><span data-ttu-id="f1243-149">Create a web app</span><span class="sxs-lookup"><span data-stu-id="f1243-149">Create a web app</span></span>

<span data-ttu-id="f1243-150">Now that an App Service plan has been created, create a Web App within the `quickStartPlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f1243-150">Now that an App Service plan has been created, create a Web App within the `quickStartPlan` App Service plan.</span></span> <span data-ttu-id="f1243-151">The web app gives us a hosting space to deploy our code as well as provides a URL for us to view the deployed application.</span><span class="sxs-lookup"><span data-stu-id="f1243-151">The web app gives us a hosting space to deploy our code as well as provides a URL for us to view the deployed application.</span></span> <span data-ttu-id="f1243-152">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the Web App.</span><span class="sxs-lookup"><span data-stu-id="f1243-152">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the Web App.</span></span>

<span data-ttu-id="f1243-153">In the command below please substitute your own unique app name where you see the <app_name> placeholder.</span><span class="sxs-lookup"><span data-stu-id="f1243-153">In the command below please substitute your own unique app name where you see the <app_name> placeholder.</span></span> <span data-ttu-id="f1243-154">The <app_name> will be used as the default DNS site for the web app, and so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1243-154">The <app_name> will be used as the default DNS site for the web app, and so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="f1243-155">You can later map any custom DNS entry to the web app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="f1243-155">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span>

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan quickStartPlan
```

<span data-ttu-id="f1243-156">When the Web App has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f1243-156">When the Web App has been created, the Azure CLI shows information similar to the following example.</span></span>

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<app_name>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "West Europe",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/quickStartPlan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

<span data-ttu-id="f1243-157">Browse to the site to see your newly created Web App.</span><span class="sxs-lookup"><span data-stu-id="f1243-157">Browse to the site to see your newly created Web App.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

![app-service-web-service-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-nodejs-poc/app-service-web-service-created.png)

<span data-ttu-id="f1243-159">We’ve now created an empty new Web App in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1243-159">We’ve now created an empty new Web App in Azure.</span></span> <span data-ttu-id="f1243-160">Let’s now configure our Web App to use Node.js and deploy our app to it.</span><span class="sxs-lookup"><span data-stu-id="f1243-160">Let’s now configure our Web App to use Node.js and deploy our app to it.</span></span>

## <a name="configure-to-use-nodejs"></a><span data-ttu-id="f1243-161">Configure to use Node.js</span><span class="sxs-lookup"><span data-stu-id="f1243-161">Configure to use Node.js</span></span>

<span data-ttu-id="f1243-162">Use the [az appservice web config update](/cli/azure/app-service/web/config#update) command to configure the Web App to use Node.js version `6.9.3`.</span><span class="sxs-lookup"><span data-stu-id="f1243-162">Use the [az appservice web config update](/cli/azure/app-service/web/config#update) command to configure the Web App to use Node.js version `6.9.3`.</span></span>

> [!TIP]
> <span data-ttu-id="f1243-163">Setting the node.js version this way uses a default container provided by the platform, if you would like to use your own container refer to the CLI reference for the [az appservice web config container update](/cli/azure/appservice/web/config/container#update) command.</span><span class="sxs-lookup"><span data-stu-id="f1243-163">Setting the node.js version this way uses a default container provided by the platform, if you would like to use your own container refer to the CLI reference for the [az appservice web config container update](/cli/azure/appservice/web/config/container#update) command.</span></span>

```azurecli
az appservice web config update --linux-fx-version "NODE|6.9.3" --startup-file process.json --name <app_name> --resource-group myResourceGroup
```

## <a name="configure-local-git-deployment"></a><span data-ttu-id="f1243-164">Configure local git deployment</span><span class="sxs-lookup"><span data-stu-id="f1243-164">Configure local git deployment</span></span>

<span data-ttu-id="f1243-165">You can deploy to your Web App in a variety of ways including FTP, local Git as well as GitHub, Visual Studio Team Services and Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="f1243-165">You can deploy to your Web App in a variety of ways including FTP, local Git as well as GitHub, Visual Studio Team Services and Bitbucket.</span></span>

<span data-ttu-id="f1243-166">Use the [az appservice web source-control config-local-git](/cli/azure/appservice/web/source-control#config-local-git) command to configure local git access to the Web App.</span><span class="sxs-lookup"><span data-stu-id="f1243-166">Use the [az appservice web source-control config-local-git](/cli/azure/appservice/web/source-control#config-local-git) command to configure local git access to the Web App.</span></span>

```azurecli
az appservice web source-control config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="f1243-167">Copy the output from the terminal as it will be used in the next step.</span><span class="sxs-lookup"><span data-stu-id="f1243-167">Copy the output from the terminal as it will be used in the next step.</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

## <a name="push-to-azure-from-git"></a><span data-ttu-id="f1243-168">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="f1243-168">Push to Azure from Git</span></span>

<span data-ttu-id="f1243-169">Add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="f1243-169">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste-previous-command-output-here>
```

<span data-ttu-id="f1243-170">Push to the Azure remote to deploy your application.</span><span class="sxs-lookup"><span data-stu-id="f1243-170">Push to the Azure remote to deploy your application.</span></span> <span data-ttu-id="f1243-171">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span><span class="sxs-lookup"><span data-stu-id="f1243-171">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```azurecli
git push azure master
```

<span data-ttu-id="f1243-172">During deployment, Azure App Service will communicate it's progress with Git.</span><span class="sxs-lookup"><span data-stu-id="f1243-172">During deployment, Azure App Service will communicate it's progress with Git.</span></span>

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="f1243-173">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="f1243-173">Browse to the app</span></span>

<span data-ttu-id="f1243-174">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="f1243-174">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="f1243-175">This time, the page that displays the Hello World message is running using our Node.js code running as an Azure App Service web app.</span><span class="sxs-lookup"><span data-stu-id="f1243-175">This time, the page that displays the Hello World message is running using our Node.js code running as an Azure App Service web app.</span></span>

## <a name="updating-and-deploying-the-code"></a><span data-ttu-id="f1243-176">Updating and Deploying the Code</span><span class="sxs-lookup"><span data-stu-id="f1243-176">Updating and Deploying the Code</span></span>

<span data-ttu-id="f1243-177">Using a local text editor, open the `index.js` file within the Node.js app, and make a small change to the text within the call to `response.end`:</span><span class="sxs-lookup"><span data-stu-id="f1243-177">Using a local text editor, open the `index.js` file within the Node.js app, and make a small change to the text within the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="f1243-178">Commit your changes in git, then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="f1243-178">Commit your changes in git, then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="f1243-179">Once deployment has completed, switch back to the browser window that opened in the Browse to the app step, and hit refresh.</span><span class="sxs-lookup"><span data-stu-id="f1243-179">Once deployment has completed, switch back to the browser window that opened in the Browse to the app step, and hit refresh.</span></span>

![hello-world-in-browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="f1243-181">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="f1243-181">Manage your new Azure web app</span></span>

<span data-ttu-id="f1243-182">Go to the Azure portal to take a look at the web app you just created.</span><span class="sxs-lookup"><span data-stu-id="f1243-182">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="f1243-183">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1243-183">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="f1243-184">From the left menu, click **App Service**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f1243-184">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="f1243-186">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="f1243-186">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span></span>

<span data-ttu-id="f1243-187">By default, your web app's blade shows the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="f1243-187">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="f1243-188">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="f1243-188">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="f1243-189">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="f1243-189">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="f1243-190">The tabs on the left side of the blade shows the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="f1243-190">The tabs on the left side of the blade shows the different configuration pages you can open.</span></span>

![App Service blade in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="f1243-192">These tabs in the blade show the many great features you can add to your web app.</span><span class="sxs-lookup"><span data-stu-id="f1243-192">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="f1243-193">The following list gives you just a few of the possibilities:</span><span class="sxs-lookup"><span data-stu-id="f1243-193">The following list gives you just a few of the possibilities:</span></span>

* <span data-ttu-id="f1243-194">Map a custom DNS name</span><span class="sxs-lookup"><span data-stu-id="f1243-194">Map a custom DNS name</span></span>
* <span data-ttu-id="f1243-195">Bind a custom SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f1243-195">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="f1243-196">Configure continuous deployment</span><span class="sxs-lookup"><span data-stu-id="f1243-196">Configure continuous deployment</span></span>
* <span data-ttu-id="f1243-197">Scale up and out</span><span class="sxs-lookup"><span data-stu-id="f1243-197">Scale up and out</span></span>
* <span data-ttu-id="f1243-198">Add user authentication</span><span class="sxs-lookup"><span data-stu-id="f1243-198">Add user authentication</span></span>

<span data-ttu-id="f1243-199">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="f1243-199">**Congratulations!**</span></span> <span data-ttu-id="f1243-200">You've deployed your first Node.js app to App Service.</span><span class="sxs-lookup"><span data-stu-id="f1243-200">You've deployed your first Node.js app to App Service.</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="f1243-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1243-201">Next steps</span></span>

<span data-ttu-id="f1243-202">Explore pre-created [Web Apps CLI scripts](app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f1243-202">Explore pre-created [Web Apps CLI scripts](app-service-cli-samples.md).</span></span>





