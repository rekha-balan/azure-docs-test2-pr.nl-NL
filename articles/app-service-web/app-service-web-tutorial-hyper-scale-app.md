---
title: Build a hyper-scale app in Azure | Microsoft Docs
description: Learn how to use different Azure services to maximize the performance of an ASP.NET app in Azure.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: ''
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 186f3f49ccad8854199a5b478e325e1a3daf327d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553427"
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="b1856-103">Build a hyper-scale web app in Azure</span><span class="sxs-lookup"><span data-stu-id="b1856-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="b1856-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span><span class="sxs-lookup"><span data-stu-id="b1856-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="b1856-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span><span class="sxs-lookup"><span data-stu-id="b1856-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="b1856-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine run the sample application.</span><span class="sxs-lookup"><span data-stu-id="b1856-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="b1856-107">Step 1 - Get sample application</span><span class="sxs-lookup"><span data-stu-id="b1856-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="b1856-108">In this step, you set up the local ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="b1856-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="b1856-109">Clone the application repository</span><span class="sxs-lookup"><span data-stu-id="b1856-109">Clone the application repository</span></span>

<span data-ttu-id="b1856-110">Open the command-line terminal of your choice and `CD` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="b1856-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="b1856-111">Then, run the following commands to clone the sample application.</span><span class="sxs-lookup"><span data-stu-id="b1856-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="b1856-112">Run the sample application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b1856-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="b1856-113">Open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b1856-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="b1856-114">Type `F5` to run the application.</span><span class="sxs-lookup"><span data-stu-id="b1856-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="b1856-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span><span class="sxs-lookup"><span data-stu-id="b1856-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="b1856-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="b1856-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="b1856-117">The `Index()` method adds a piece of data to the session.</span><span class="sxs-lookup"><span data-stu-id="b1856-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="b1856-118">And the `About()` and `Contact()` methods cache their output.</span><span class="sxs-lookup"><span data-stu-id="b1856-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="b1856-119">Step 2 - Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="b1856-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="b1856-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span><span class="sxs-lookup"><span data-stu-id="b1856-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="b1856-121">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="b1856-121">Create a resource group</span></span>   
<span data-ttu-id="b1856-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span><span class="sxs-lookup"><span data-stu-id="b1856-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="b1856-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span><span class="sxs-lookup"><span data-stu-id="b1856-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="b1856-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span><span class="sxs-lookup"><span data-stu-id="b1856-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="b1856-125">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="b1856-125">Create an App Service plan</span></span>
<span data-ttu-id="b1856-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1856-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="b1856-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b1856-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="b1856-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="b1856-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="b1856-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span><span class="sxs-lookup"><span data-stu-id="b1856-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="b1856-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span><span class="sxs-lookup"><span data-stu-id="b1856-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="b1856-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="b1856-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="b1856-132">Create a web app</span><span class="sxs-lookup"><span data-stu-id="b1856-132">Create a web app</span></span>
<span data-ttu-id="b1856-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span><span class="sxs-lookup"><span data-stu-id="b1856-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="b1856-134">Set deployment credentials</span><span class="sxs-lookup"><span data-stu-id="b1856-134">Set deployment credentials</span></span>
<span data-ttu-id="b1856-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span><span class="sxs-lookup"><span data-stu-id="b1856-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="b1856-136">Configure Git deployment</span><span class="sxs-lookup"><span data-stu-id="b1856-136">Configure Git deployment</span></span>
<span data-ttu-id="b1856-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span><span class="sxs-lookup"><span data-stu-id="b1856-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="b1856-138">This command gives you an output that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="b1856-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="b1856-139">Use the returned URL to configure your Git remote.</span><span class="sxs-lookup"><span data-stu-id="b1856-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="b1856-140">The following command uses the preceding output example.</span><span class="sxs-lookup"><span data-stu-id="b1856-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="b1856-141">Deploy the sample application</span><span class="sxs-lookup"><span data-stu-id="b1856-141">Deploy the sample application</span></span>
<span data-ttu-id="b1856-142">You are now ready to deploy your sample application.</span><span class="sxs-lookup"><span data-stu-id="b1856-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="b1856-143">Run `git push`.</span><span class="sxs-lookup"><span data-stu-id="b1856-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="b1856-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="b1856-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="b1856-145">Browse to Azure web app</span><span class="sxs-lookup"><span data-stu-id="b1856-145">Browse to Azure web app</span></span>
<span data-ttu-id="b1856-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span><span class="sxs-lookup"><span data-stu-id="b1856-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="b1856-147">Step 3 - Connect to Redis</span><span class="sxs-lookup"><span data-stu-id="b1856-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="b1856-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b1856-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="b1856-149">You can quickly utilize Redis to cache your page output.</span><span class="sxs-lookup"><span data-stu-id="b1856-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="b1856-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span><span class="sxs-lookup"><span data-stu-id="b1856-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="b1856-151">Create an Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="b1856-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="b1856-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span><span class="sxs-lookup"><span data-stu-id="b1856-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="b1856-153">Use a unique name in `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="b1856-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="b1856-154">Configure the application to use Redis</span><span class="sxs-lookup"><span data-stu-id="b1856-154">Configure the application to use Redis</span></span>
<span data-ttu-id="b1856-155">Format the connection string for your cache.</span><span class="sxs-lookup"><span data-stu-id="b1856-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="b1856-156">The second line should give you an output that looks like this:</span><span class="sxs-lookup"><span data-stu-id="b1856-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="b1856-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span><span class="sxs-lookup"><span data-stu-id="b1856-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="b1856-158">In `value`, use the connection string from the PowerShell output.</span><span class="sxs-lookup"><span data-stu-id="b1856-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="b1856-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span><span class="sxs-lookup"><span data-stu-id="b1856-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="b1856-160">That way your sensitive information is kept safe.</span><span class="sxs-lookup"><span data-stu-id="b1856-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="b1856-161">Open `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="b1856-161">Open `Web.config`.</span></span> <span data-ttu-id="b1856-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="b1856-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="b1856-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="b1856-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="b1856-164">Uncomment this section.</span><span class="sxs-lookup"><span data-stu-id="b1856-164">Uncomment this section.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="b1856-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="b1856-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="b1856-166">Your application now uses Redis to manage sessions and caching.</span><span class="sxs-lookup"><span data-stu-id="b1856-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="b1856-167">Type `F5` to run the application.</span><span class="sxs-lookup"><span data-stu-id="b1856-167">Type `F5` to run the application.</span></span> <span data-ttu-id="b1856-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span><span class="sxs-lookup"><span data-stu-id="b1856-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="b1856-169">Configure the connection string in Azure</span><span class="sxs-lookup"><span data-stu-id="b1856-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="b1856-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b1856-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="b1856-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span><span class="sxs-lookup"><span data-stu-id="b1856-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="b1856-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="b1856-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="b1856-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1856-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="b1856-174">Remember that `$connstring` contains the formatted connection string.</span><span class="sxs-lookup"><span data-stu-id="b1856-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="b1856-175">Redeploy the application to Azure</span><span class="sxs-lookup"><span data-stu-id="b1856-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="b1856-176">Use Git commands to push your changes to Azure</span><span class="sxs-lookup"><span data-stu-id="b1856-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="b1856-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="b1856-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="b1856-178">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="b1856-178">Browse to the Azure web app</span></span>
<span data-ttu-id="b1856-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1856-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="b1856-180">Step 4 - Scale to multiple instances</span><span class="sxs-lookup"><span data-stu-id="b1856-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="b1856-181">The App Service plan is the scale unit for your Azure web apps.</span><span class="sxs-lookup"><span data-stu-id="b1856-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="b1856-182">To scale out your web app, you scale the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b1856-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="b1856-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b1856-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="b1856-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span><span class="sxs-lookup"><span data-stu-id="b1856-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="b1856-185">Step 5 - Scale geographically</span><span class="sxs-lookup"><span data-stu-id="b1856-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="b1856-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="b1856-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="b1856-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span><span class="sxs-lookup"><span data-stu-id="b1856-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="b1856-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="b1856-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="b1856-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span><span class="sxs-lookup"><span data-stu-id="b1856-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="b1856-190">Both apps will be served from the same Traffic Manager URL.</span><span class="sxs-lookup"><span data-stu-id="b1856-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="b1856-191">Scale up the Europe app to Standard tier</span><span class="sxs-lookup"><span data-stu-id="b1856-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="b1856-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b1856-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="b1856-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span><span class="sxs-lookup"><span data-stu-id="b1856-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="b1856-194">Create a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="b1856-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="b1856-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span><span class="sxs-lookup"><span data-stu-id="b1856-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="b1856-196">Use a unique DNS name in $dnsName.</span><span class="sxs-lookup"><span data-stu-id="b1856-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="b1856-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="b1856-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="b1856-198">Get the resource ID of the Europe app</span><span class="sxs-lookup"><span data-stu-id="b1856-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="b1856-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span><span class="sxs-lookup"><span data-stu-id="b1856-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="b1856-200">Add a Traffic Manager endpoint for the Europe app</span><span class="sxs-lookup"><span data-stu-id="b1856-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="b1856-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span><span class="sxs-lookup"><span data-stu-id="b1856-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="b1856-202">Get the Traffic Manager endpoint URL</span><span class="sxs-lookup"><span data-stu-id="b1856-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="b1856-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span><span class="sxs-lookup"><span data-stu-id="b1856-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="b1856-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span><span class="sxs-lookup"><span data-stu-id="b1856-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="b1856-205">Copy the output into your browser.</span><span class="sxs-lookup"><span data-stu-id="b1856-205">Copy the output into your browser.</span></span> <span data-ttu-id="b1856-206">You should see your web app again.</span><span class="sxs-lookup"><span data-stu-id="b1856-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="b1856-207">Create an Azure Redis Cache in Asia</span><span class="sxs-lookup"><span data-stu-id="b1856-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="b1856-208">Now, you replicate your Azure web app to the Southeast Asia region.</span><span class="sxs-lookup"><span data-stu-id="b1856-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="b1856-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span><span class="sxs-lookup"><span data-stu-id="b1856-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="b1856-210">This cache needs to be colocated with your app in Asia.</span><span class="sxs-lookup"><span data-stu-id="b1856-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="b1856-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span><span class="sxs-lookup"><span data-stu-id="b1856-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="b1856-212">Create an App Service plan in Asia</span><span class="sxs-lookup"><span data-stu-id="b1856-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="b1856-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span><span class="sxs-lookup"><span data-stu-id="b1856-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="b1856-214">Create a web app in Asia</span><span class="sxs-lookup"><span data-stu-id="b1856-214">Create a web app in Asia</span></span>
<span data-ttu-id="b1856-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span><span class="sxs-lookup"><span data-stu-id="b1856-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="b1856-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span><span class="sxs-lookup"><span data-stu-id="b1856-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="b1856-217">Configure the connection string for Redis</span><span class="sxs-lookup"><span data-stu-id="b1856-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="b1856-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span><span class="sxs-lookup"><span data-stu-id="b1856-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="b1856-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1856-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="b1856-220">Configure Git deployment for the Asia app.</span><span class="sxs-lookup"><span data-stu-id="b1856-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="b1856-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span><span class="sxs-lookup"><span data-stu-id="b1856-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="b1856-222">This command gives you an output that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="b1856-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="b1856-223">Use the returned URL to configure a second Git remote for your local repository.</span><span class="sxs-lookup"><span data-stu-id="b1856-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="b1856-224">The following command uses the preceding output example.</span><span class="sxs-lookup"><span data-stu-id="b1856-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="b1856-225">Deploy your sample application</span><span class="sxs-lookup"><span data-stu-id="b1856-225">Deploy your sample application</span></span>
<span data-ttu-id="b1856-226">Run `git push` to deploy your sample application to the second Git remote.</span><span class="sxs-lookup"><span data-stu-id="b1856-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="b1856-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="b1856-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="b1856-228">Browse to the Asia app</span><span class="sxs-lookup"><span data-stu-id="b1856-228">Browse to the Asia app</span></span>
<span data-ttu-id="b1856-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1856-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="b1856-230">Get the resource ID of the Asia app</span><span class="sxs-lookup"><span data-stu-id="b1856-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="b1856-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span><span class="sxs-lookup"><span data-stu-id="b1856-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="b1856-232">Add a Traffic Manager endpoint for the Asia app</span><span class="sxs-lookup"><span data-stu-id="b1856-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="b1856-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="b1856-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="b1856-234">Add region identifier to web apps</span><span class="sxs-lookup"><span data-stu-id="b1856-234">Add region identifier to web apps</span></span>
<span data-ttu-id="b1856-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span><span class="sxs-lookup"><span data-stu-id="b1856-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="b1856-236">Your application code already uses this application setting.</span><span class="sxs-lookup"><span data-stu-id="b1856-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="b1856-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b1856-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="b1856-238">Complete!</span><span class="sxs-lookup"><span data-stu-id="b1856-238">Complete!</span></span>

<span data-ttu-id="b1856-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span><span class="sxs-lookup"><span data-stu-id="b1856-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="b1856-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span><span class="sxs-lookup"><span data-stu-id="b1856-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="b1856-241">More resources</span><span class="sxs-lookup"><span data-stu-id="b1856-241">More resources</span></span>

