---
title: Authenticate and authorize users end-to-end in Azure App Service | Microsoft Docs
description: Learn how to use App Service authentication and authorization to secure your App Service apps, including access to remote APIs.
keywords: app service, azure app service, authN, authZ, secure, security, multi-tiered, azure active directory, azure ad
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 08/07/2018
ms.author: cephalin
ms.openlocfilehash: e597ba5236fb2d7fea8649f423c4a952b01f87ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969531"
---
# <a name="tutorial-authenticate-and-authorize-users-end-to-end-in-azure-app-service"></a><span data-ttu-id="5ecfb-104">Tutorial: Authenticate and authorize users end-to-end in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5ecfb-104">Tutorial: Authenticate and authorize users end-to-end in Azure App Service</span></span>

<span data-ttu-id="5ecfb-105">[Azure App Service](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-105">[Azure App Service](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5ecfb-106">In addition, App Service has built-in support for [user authentication and authorization](app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-106">In addition, App Service has built-in support for [user authentication and authorization](app-service-authentication-overview.md).</span></span> <span data-ttu-id="5ecfb-107">This tutorial shows how to secure your apps with App Service authentication and authorization.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-107">This tutorial shows how to secure your apps with App Service authentication and authorization.</span></span> <span data-ttu-id="5ecfb-108">It uses an ASP.NET Core app with an Angular.js front end, but it is only for an example.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-108">It uses an ASP.NET Core app with an Angular.js front end, but it is only for an example.</span></span> <span data-ttu-id="5ecfb-109">App Service authentication and authorization support all language runtimes, and you can learn how to apply it to your preferred language by following the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-109">App Service authentication and authorization support all language runtimes, and you can learn how to apply it to your preferred language by following the tutorial.</span></span>

<span data-ttu-id="5ecfb-110">The tutorial uses the sample app to show you how to secure a self-contained app (in [Enable authentication and authorization for back-end app](#enable-authentication-and-authorization-for-back-end-app)).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-110">The tutorial uses the sample app to show you how to secure a self-contained app (in [Enable authentication and authorization for back-end app](#enable-authentication-and-authorization-for-back-end-app)).</span></span>

![Simple authentication and authorization](./media/app-service-web-tutorial-auth-aad/simple-auth.png)

<span data-ttu-id="5ecfb-112">It also shows you how to secure a multi-tiered app, by accessing a secured back-end API on behalf of the authenticated user, both [from server code](#call-api-securely-from-server-code) and [from browser code](#call-api-securely-from-browser-code).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-112">It also shows you how to secure a multi-tiered app, by accessing a secured back-end API on behalf of the authenticated user, both [from server code](#call-api-securely-from-server-code) and [from browser code](#call-api-securely-from-browser-code).</span></span>

![Advanced authentication and authorization](./media/app-service-web-tutorial-auth-aad/advanced-auth.png)

<span data-ttu-id="5ecfb-114">These are only some of the possible authentication and authorization scenarios in App Service.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-114">These are only some of the possible authentication and authorization scenarios in App Service.</span></span> 

<span data-ttu-id="5ecfb-115">Here's a more comprehensive list of things you learn in the tutorial:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-115">Here's a more comprehensive list of things you learn in the tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ecfb-116">Enable built-in authentication and authorization</span><span class="sxs-lookup"><span data-stu-id="5ecfb-116">Enable built-in authentication and authorization</span></span>
> * <span data-ttu-id="5ecfb-117">Secure apps against unauthenticated requests</span><span class="sxs-lookup"><span data-stu-id="5ecfb-117">Secure apps against unauthenticated requests</span></span>
> * <span data-ttu-id="5ecfb-118">Use Azure Active Directory as the identity provider</span><span class="sxs-lookup"><span data-stu-id="5ecfb-118">Use Azure Active Directory as the identity provider</span></span>
> * <span data-ttu-id="5ecfb-119">Access a remote app on behalf of the signed-in user</span><span class="sxs-lookup"><span data-stu-id="5ecfb-119">Access a remote app on behalf of the signed-in user</span></span>
> * <span data-ttu-id="5ecfb-120">Secure service-to-service calls with token authentication</span><span class="sxs-lookup"><span data-stu-id="5ecfb-120">Secure service-to-service calls with token authentication</span></span>
> * <span data-ttu-id="5ecfb-121">Use access tokens from server code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-121">Use access tokens from server code</span></span>
> * <span data-ttu-id="5ecfb-122">Use access tokens from client (browser) code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-122">Use access tokens from client (browser) code</span></span>

<span data-ttu-id="5ecfb-123">You can follow the steps in this tutorial on macOS, Linux, Windows.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-123">You can follow the steps in this tutorial on macOS, Linux, Windows.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="5ecfb-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ecfb-124">Prerequisites</span></span>

<span data-ttu-id="5ecfb-125">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-125">To complete this tutorial:</span></span>

* <span data-ttu-id="5ecfb-126">[Install Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-126">[Install Git](https://git-scm.com/).</span></span>
* <span data-ttu-id="5ecfb-127">[Install .NET Core](https://www.microsoft.com/net/core/).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-127">[Install .NET Core](https://www.microsoft.com/net/core/).</span></span>

## <a name="create-local-net-core-app"></a><span data-ttu-id="5ecfb-128">Create local .NET Core app</span><span class="sxs-lookup"><span data-stu-id="5ecfb-128">Create local .NET Core app</span></span>

<span data-ttu-id="5ecfb-129">In this step, you set up the local .NET Core project.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-129">In this step, you set up the local .NET Core project.</span></span> <span data-ttu-id="5ecfb-130">You use the same project to deploy a back-end API app and a front-end web app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-130">You use the same project to deploy a back-end API app and a front-end web app.</span></span>

### <a name="clone-and-run-the-sample-application"></a><span data-ttu-id="5ecfb-131">Clone and run the sample application</span><span class="sxs-lookup"><span data-stu-id="5ecfb-131">Clone and run the sample application</span></span>

<span data-ttu-id="5ecfb-132">Run the following commands to clone the sample repository and run it.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-132">Run the following commands to clone the sample repository and run it.</span></span>

```bash
git clone https://github.com/Azure-Samples/dotnet-core-api
cd dotnet-core-api
dotnet run
```

<span data-ttu-id="5ecfb-133">Navigate to `http://localhost:5000` and try adding, editing, and removing todo items.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-133">Navigate to `http://localhost:5000` and try adding, editing, and removing todo items.</span></span> 

![ASP.NET Core API running locally](./media/app-service-web-tutorial-auth-aad/local-run.png)

<span data-ttu-id="5ecfb-135">To stop ASP.NET Core at any time, press `Ctrl+C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-135">To stop ASP.NET Core at any time, press `Ctrl+C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="deploy-apps-to-azure"></a><span data-ttu-id="5ecfb-136">Deploy apps to Azure</span><span class="sxs-lookup"><span data-stu-id="5ecfb-136">Deploy apps to Azure</span></span>

<span data-ttu-id="5ecfb-137">In this step, you deploy the project to two App Service apps.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-137">In this step, you deploy the project to two App Service apps.</span></span> <span data-ttu-id="5ecfb-138">One is the front-end app and the other is the back-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-138">One is the front-end app and the other is the back-end app.</span></span>

### <a name="create-azure-resources"></a><span data-ttu-id="5ecfb-139">Create Azure resources</span><span class="sxs-lookup"><span data-stu-id="5ecfb-139">Create Azure resources</span></span>

<span data-ttu-id="5ecfb-140">In the Cloud Shell, run the following commands to create two web apps.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-140">In the Cloud Shell, run the following commands to create two web apps.</span></span> <span data-ttu-id="5ecfb-141">Replace _&lt;front\_end\_app\_name>_ and _&lt;back\_end\_app\_name>_ with two globally unique app names (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-141">Replace _&lt;front\_end\_app\_name>_ and _&lt;back\_end\_app\_name>_ with two globally unique app names (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="5ecfb-142">For more information on each command, see [RESTful API with CORS in Azure App Service](app-service-web-tutorial-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-142">For more information on each command, see [RESTful API with CORS in Azure App Service](app-service-web-tutorial-rest-api.md).</span></span>

```azurecli-interactive
az group create --name myAuthResourceGroup --location "West Europe"
az appservice plan create --name myAuthAppServicePlan --resource-group myAuthResourceGroup --sku FREE
az webapp create --resource-group myAuthResourceGroup --plan myAuthAppServicePlan --name <front_end_app_name> --deployment-local-git --query deploymentLocalGitUrl
az webapp create --resource-group myAuthResourceGroup --plan myAuthAppServicePlan --name <back_end_app_name> --deployment-local-git --query deploymentLocalGitUrl
```

> [!NOTE]
> <span data-ttu-id="5ecfb-143">Save the URLs of the Git remotes for your front-end app and back-end app, which are shown in the output from `az webapp create`.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-143">Save the URLs of the Git remotes for your front-end app and back-end app, which are shown in the output from `az webapp create`.</span></span>
>

### <a name="push-to-azure-from-git"></a><span data-ttu-id="5ecfb-144">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="5ecfb-144">Push to Azure from Git</span></span>

<span data-ttu-id="5ecfb-145">Back in the _local terminal window_, run the following Git commands to deploy to the back-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-145">Back in the _local terminal window_, run the following Git commands to deploy to the back-end app.</span></span> <span data-ttu-id="5ecfb-146">Replace _&lt;deploymentLocalGitUrl-of-back-end-app>_ with the URL of the Git remote that you saved from [Create Azure resources](#create-azure-resources).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-146">Replace _&lt;deploymentLocalGitUrl-of-back-end-app>_ with the URL of the Git remote that you saved from [Create Azure resources](#create-azure-resources).</span></span> <span data-ttu-id="5ecfb-147">When prompted for credentials by Git Credential Manager, make sure that you enter [your deployment credentials](app-service-deployment-credentials.md), not the credentials you use to log in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-147">When prompted for credentials by Git Credential Manager, make sure that you enter [your deployment credentials](app-service-deployment-credentials.md), not the credentials you use to log in to the Azure portal.</span></span>

```bash
git remote add backend <deploymentLocalGitUrl-of-back-end-app>
git push backend master
```

<span data-ttu-id="5ecfb-148">In the local terminal window, run the following Git commands to deploy the same code to the front-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-148">In the local terminal window, run the following Git commands to deploy the same code to the front-end app.</span></span> <span data-ttu-id="5ecfb-149">Replace _&lt;deploymentLocalGitUrl-of-front-end-app>_ with the URL of the Git remote that you saved from [Create Azure resources](#create-azure-resources).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-149">Replace _&lt;deploymentLocalGitUrl-of-front-end-app>_ with the URL of the Git remote that you saved from [Create Azure resources](#create-azure-resources).</span></span>

```bash
git remote add frontend <deploymentLocalGitUrl-of-front-end-app>
git push frontend master
```

### <a name="browse-to-the-azure-web-apps"></a><span data-ttu-id="5ecfb-150">Browse to the Azure web apps</span><span class="sxs-lookup"><span data-stu-id="5ecfb-150">Browse to the Azure web apps</span></span>

<span data-ttu-id="5ecfb-151">Navigate to the following URLs in a browser and see the two apps working.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-151">Navigate to the following URLs in a browser and see the two apps working.</span></span>

```
http://<back_end_app_name>.azurewebsites.net
http://<front_end_app_name>.azurewebsites.net
```

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/azure-run.png)

> [!NOTE]
> <span data-ttu-id="5ecfb-153">If your app restarts, you may have noticed that new data has been erased.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-153">If your app restarts, you may have noticed that new data has been erased.</span></span> <span data-ttu-id="5ecfb-154">This behavior by design because the sample ASP.NET Core app uses an in-memory database.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-154">This behavior by design because the sample ASP.NET Core app uses an in-memory database.</span></span>
>
>

## <a name="call-back-end-api-from-front-end"></a><span data-ttu-id="5ecfb-155">Call back-end API from front end</span><span class="sxs-lookup"><span data-stu-id="5ecfb-155">Call back-end API from front end</span></span>

<span data-ttu-id="5ecfb-156">In this step, you point the front-end app's server code to access the back-end API.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-156">In this step, you point the front-end app's server code to access the back-end API.</span></span> <span data-ttu-id="5ecfb-157">Later, you enable authenticated access from the front end to the back end.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-157">Later, you enable authenticated access from the front end to the back end.</span></span>

### <a name="modify-front-end-code"></a><span data-ttu-id="5ecfb-158">Modify front-end code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-158">Modify front-end code</span></span>

<span data-ttu-id="5ecfb-159">In the local repository, open _Controllers/TodoController.cs_.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-159">In the local repository, open _Controllers/TodoController.cs_.</span></span> <span data-ttu-id="5ecfb-160">At the beginning of the `TodoController` class, add the following lines and replace _&lt;back\_end\_app\_name>_ with the name of your back-end app:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-160">At the beginning of the `TodoController` class, add the following lines and replace _&lt;back\_end\_app\_name>_ with the name of your back-end app:</span></span>

```cs
private static readonly HttpClient _client = new HttpClient();
private static readonly string _remoteUrl = "https://<back_end_app_name>.azurewebsites.net";
```

<span data-ttu-id="5ecfb-161">Find the `GetAll()` method and replace the code inside the curly braces with:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-161">Find the `GetAll()` method and replace the code inside the curly braces with:</span></span>

```cs
var data = _client.GetStringAsync($"{_remoteUrl}/api/Todo").Result;
return JsonConvert.DeserializeObject<List<TodoItem>>(data);
```

<span data-ttu-id="5ecfb-162">The first line makes a `GET /api/Todo` call to the back-end API app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-162">The first line makes a `GET /api/Todo` call to the back-end API app.</span></span>

<span data-ttu-id="5ecfb-163">Next, find the `GetById(long id)` method and replace the code inside the curly braces with:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-163">Next, find the `GetById(long id)` method and replace the code inside the curly braces with:</span></span>

```cs
var data = _client.GetStringAsync($"{_remoteUrl}/api/Todo/{id}").Result;
return Content(data, "application/json");
```

<span data-ttu-id="5ecfb-164">The first line makes a `GET /api/Todo/{id}` call to the back-end API app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-164">The first line makes a `GET /api/Todo/{id}` call to the back-end API app.</span></span>

<span data-ttu-id="5ecfb-165">Next, find the `Create([FromBody] TodoItem item)`  method and replace the code inside the curly braces with:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-165">Next, find the `Create([FromBody] TodoItem item)`  method and replace the code inside the curly braces with:</span></span>

```cs
var response = _client.PostAsJsonAsync($"{_remoteUrl}/api/Todo", item).Result;
var data = response.Content.ReadAsStringAsync().Result;
return Content(data, "application/json");
```

<span data-ttu-id="5ecfb-166">The first line makes a `POST /api/Todo` call to the back-end API app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-166">The first line makes a `POST /api/Todo` call to the back-end API app.</span></span>

<span data-ttu-id="5ecfb-167">Next, find the `Update(long id, [FromBody] TodoItem item)`  method and replace the code inside the curly braces with:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-167">Next, find the `Update(long id, [FromBody] TodoItem item)`  method and replace the code inside the curly braces with:</span></span>

```cs
var res = _client.PutAsJsonAsync($"{_remoteUrl}/api/Todo/{id}", item).Result;
return new NoContentResult();
```

<span data-ttu-id="5ecfb-168">The first line makes a `PUT /api/Todo/{id}` call to the back-end API app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-168">The first line makes a `PUT /api/Todo/{id}` call to the back-end API app.</span></span>

<span data-ttu-id="5ecfb-169">Next, find the `Delete(long id)`  method and replace the code inside the curly braces with:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-169">Next, find the `Delete(long id)`  method and replace the code inside the curly braces with:</span></span>

```cs
var res = _client.DeleteAsync($"{_remoteUrl}/api/Todo/{id}").Result;
return new NoContentResult();
```

<span data-ttu-id="5ecfb-170">The first line makes a `DELETE /api/Todo/{id}` call to the back-end API app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-170">The first line makes a `DELETE /api/Todo/{id}` call to the back-end API app.</span></span>

<span data-ttu-id="5ecfb-171">Save your all your changes.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-171">Save your all your changes.</span></span> <span data-ttu-id="5ecfb-172">In the local terminal window, deploy your changes to the front-end app with the following Git commands:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-172">In the local terminal window, deploy your changes to the front-end app with the following Git commands:</span></span>

```bash
git add .
git commit -m "call back-end API"
git push frontend master
```

### <a name="check-your-changes"></a><span data-ttu-id="5ecfb-173">Check your changes</span><span class="sxs-lookup"><span data-stu-id="5ecfb-173">Check your changes</span></span>

<span data-ttu-id="5ecfb-174">Navigate to `http://<front_end_app_name>.azurewebsites.net` and add a few items, such as `from front end 1` and `from front end 2`.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-174">Navigate to `http://<front_end_app_name>.azurewebsites.net` and add a few items, such as `from front end 1` and `from front end 2`.</span></span>

<span data-ttu-id="5ecfb-175">Navigate to `http://<back_end_app_name>.azurewebsites.net` to see the items added from the front-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-175">Navigate to `http://<back_end_app_name>.azurewebsites.net` to see the items added from the front-end app.</span></span> <span data-ttu-id="5ecfb-176">Also, add a few items, such as `from back end 1` and `from back end 2`, then refresh the front-end app to see if it reflects the changes.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-176">Also, add a few items, such as `from back end 1` and `from back end 2`, then refresh the front-end app to see if it reflects the changes.</span></span>

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/remote-api-call-run.png)

## <a name="configure-auth"></a><span data-ttu-id="5ecfb-178">Configure auth</span><span class="sxs-lookup"><span data-stu-id="5ecfb-178">Configure auth</span></span>

<span data-ttu-id="5ecfb-179">In this step, you enable authentication and authorization for the two apps.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-179">In this step, you enable authentication and authorization for the two apps.</span></span> <span data-ttu-id="5ecfb-180">You also configure the front-end app to generate an access token that you can use to make authenticated calls to the back-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-180">You also configure the front-end app to generate an access token that you can use to make authenticated calls to the back-end app.</span></span>

<span data-ttu-id="5ecfb-181">You use Azure Active Directory as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-181">You use Azure Active Directory as the identity provider.</span></span> <span data-ttu-id="5ecfb-182">For more information, see [Configure Azure Active Directory authentication for your App Services application](app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-182">For more information, see [Configure Azure Active Directory authentication for your App Services application](app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

### <a name="enable-authentication-and-authorization-for-back-end-app"></a><span data-ttu-id="5ecfb-183">Enable authentication and authorization for back-end app</span><span class="sxs-lookup"><span data-stu-id="5ecfb-183">Enable authentication and authorization for back-end app</span></span>

<span data-ttu-id="5ecfb-184">In the [Azure portal](https://portal.azure.com), open your back-end app's management page by clicking from the left menu: **Resource groups** > **myAuthResourceGroup** > _\<back\_end\_app\_name>_.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-184">In the [Azure portal](https://portal.azure.com), open your back-end app's management page by clicking from the left menu: **Resource groups** > **myAuthResourceGroup** > _\<back\_end\_app\_name>_.</span></span>

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/portal-navigate-back-end.png)

<span data-ttu-id="5ecfb-186">In your back-end app's left menu, click **Authentication / Authorization**, then enable App Service Authentication by clicking **On**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-186">In your back-end app's left menu, click **Authentication / Authorization**, then enable App Service Authentication by clicking **On**.</span></span>

<span data-ttu-id="5ecfb-187">In **Action to take when request is not authenticated**, select **Log in with Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-187">In **Action to take when request is not authenticated**, select **Log in with Azure Active Directory**.</span></span>

<span data-ttu-id="5ecfb-188">Under **Authentication Providers**, click **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="5ecfb-188">Under **Authentication Providers**, click **Azure Active Directory**</span></span> 

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/configure-auth-back-end.png)

<span data-ttu-id="5ecfb-190">Click **Express**, then accept the default settings to create a new AD app and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-190">Click **Express**, then accept the default settings to create a new AD app and click **OK**.</span></span>

<span data-ttu-id="5ecfb-191">In the **Authentication / Authorization** page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-191">In the **Authentication / Authorization** page, click **Save**.</span></span> 

<span data-ttu-id="5ecfb-192">Once you see the notification with the message `Successfully saved the Auth Settings for <back_end_app_name> App`, refresh the page.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-192">Once you see the notification with the message `Successfully saved the Auth Settings for <back_end_app_name> App`, refresh the page.</span></span>

<span data-ttu-id="5ecfb-193">Click **Azure Active Directory** again, and then click **Manage Application**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-193">Click **Azure Active Directory** again, and then click **Manage Application**.</span></span>

<span data-ttu-id="5ecfb-194">From the management page of the AD application, copy the **Application ID** to a notepad.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-194">From the management page of the AD application, copy the **Application ID** to a notepad.</span></span> <span data-ttu-id="5ecfb-195">You need this value later.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-195">You need this value later.</span></span>

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/get-application-id-back-end.png)

### <a name="enable-authentication-and-authorization-for-front-end-app"></a><span data-ttu-id="5ecfb-197">Enable authentication and authorization for front-end app</span><span class="sxs-lookup"><span data-stu-id="5ecfb-197">Enable authentication and authorization for front-end app</span></span>

<span data-ttu-id="5ecfb-198">Follow the same steps for the front-end app, but skip the last step.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-198">Follow the same steps for the front-end app, but skip the last step.</span></span> <span data-ttu-id="5ecfb-199">You don't need the **Application ID** for the front-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-199">You don't need the **Application ID** for the front-end app.</span></span> <span data-ttu-id="5ecfb-200">Keep the **Azure Active Directory Settings** page open.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-200">Keep the **Azure Active Directory Settings** page open.</span></span>

<span data-ttu-id="5ecfb-201">If you like, navigate to `http://<front_end_app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-201">If you like, navigate to `http://<front_end_app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="5ecfb-202">It should now direct you to a secured sign-in page.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-202">It should now direct you to a secured sign-in page.</span></span> <span data-ttu-id="5ecfb-203">After you sign in, you still can't access the data from the back-end app, because you still need to do three things:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-203">After you sign in, you still can't access the data from the back-end app, because you still need to do three things:</span></span>

- <span data-ttu-id="5ecfb-204">Grant the front end access to the back end</span><span class="sxs-lookup"><span data-stu-id="5ecfb-204">Grant the front end access to the back end</span></span>
- <span data-ttu-id="5ecfb-205">Configure App Service to return a usable token</span><span class="sxs-lookup"><span data-stu-id="5ecfb-205">Configure App Service to return a usable token</span></span>
- <span data-ttu-id="5ecfb-206">Use the token in your code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-206">Use the token in your code</span></span>

> [!TIP]
> <span data-ttu-id="5ecfb-207">If you run into errors and reconfigure your app's authentication/authorization settings, the tokens in the token store may not be regenerated from the new settings.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-207">If you run into errors and reconfigure your app's authentication/authorization settings, the tokens in the token store may not be regenerated from the new settings.</span></span> <span data-ttu-id="5ecfb-208">To make sure your tokens are regenerated, you need to sign out and sign back in to your app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-208">To make sure your tokens are regenerated, you need to sign out and sign back in to your app.</span></span> <span data-ttu-id="5ecfb-209">An easy way to do it is to use your browser in private mode, and close and reopen the browser in private mode after changing the settings in your apps.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-209">An easy way to do it is to use your browser in private mode, and close and reopen the browser in private mode after changing the settings in your apps.</span></span>

### <a name="grant-front-end-app-access-to-back-end"></a><span data-ttu-id="5ecfb-210">Grant front-end app access to back end</span><span class="sxs-lookup"><span data-stu-id="5ecfb-210">Grant front-end app access to back end</span></span>

<span data-ttu-id="5ecfb-211">Now that you've enabled authentication and authorization to both of your apps, each of them is backed by an AD application.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-211">Now that you've enabled authentication and authorization to both of your apps, each of them is backed by an AD application.</span></span> <span data-ttu-id="5ecfb-212">In this step, you give the front-end app permissions to access the back end on the user's behalf.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-212">In this step, you give the front-end app permissions to access the back end on the user's behalf.</span></span> <span data-ttu-id="5ecfb-213">(Technically, you give the front end's _AD application_ the permissions to access the back end's _AD application_ on the user's behalf.)</span><span class="sxs-lookup"><span data-stu-id="5ecfb-213">(Technically, you give the front end's _AD application_ the permissions to access the back end's _AD application_ on the user's behalf.)</span></span>

<span data-ttu-id="5ecfb-214">At this point, you should be in the **Azure Active Directory Settings** page for the front-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-214">At this point, you should be in the **Azure Active Directory Settings** page for the front-end app.</span></span> <span data-ttu-id="5ecfb-215">If not, go back to that page.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-215">If not, go back to that page.</span></span> 

<span data-ttu-id="5ecfb-216">Click **Manage Permissions** > **Add** > **Select an API**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-216">Click **Manage Permissions** > **Add** > **Select an API**.</span></span>

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/add-api-access-front-end.png)

<span data-ttu-id="5ecfb-218">In the **Select an API** page, type the AD application name of your back-end app, which is the same as your back-end app name by default.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-218">In the **Select an API** page, type the AD application name of your back-end app, which is the same as your back-end app name by default.</span></span> <span data-ttu-id="5ecfb-219">Select it in the list and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-219">Select it in the list and click **Select**.</span></span>

<span data-ttu-id="5ecfb-220">Select the checkbox next to **Access _&lt;AD\_application\_name>_**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-220">Select the checkbox next to **Access _&lt;AD\_application\_name>_**.</span></span> <span data-ttu-id="5ecfb-221">Click **Select** > **Done**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-221">Click **Select** > **Done**.</span></span>

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/select-permission-front-end.png)

### <a name="configure-app-service-to-return-a-usable-access-token"></a><span data-ttu-id="5ecfb-223">Configure App Service to return a usable access token</span><span class="sxs-lookup"><span data-stu-id="5ecfb-223">Configure App Service to return a usable access token</span></span>

<span data-ttu-id="5ecfb-224">The front-end app now has the required permissions.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-224">The front-end app now has the required permissions.</span></span> <span data-ttu-id="5ecfb-225">In this step, you configure App Service authentication and authorization to give you a usable access token for accessing the back end.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-225">In this step, you configure App Service authentication and authorization to give you a usable access token for accessing the back end.</span></span> <span data-ttu-id="5ecfb-226">For this step, you need the back end's Application ID, which you copied from [Enable authentication and authorization for back-end app](#enable-authentication-and-authorization-for-back-end-app).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-226">For this step, you need the back end's Application ID, which you copied from [Enable authentication and authorization for back-end app](#enable-authentication-and-authorization-for-back-end-app).</span></span>

<span data-ttu-id="5ecfb-227">Sign in to [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-227">Sign in to [Azure Resource Explorer](https://resources.azure.com).</span></span> <span data-ttu-id="5ecfb-228">At the top of the page, click **Read/Write** to enable editing of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-228">At the top of the page, click **Read/Write** to enable editing of your Azure resources.</span></span>

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/resources-enable-write.png)

<span data-ttu-id="5ecfb-230">In the left browser, click **subscriptions** > **_&lt;your\_subscription>_** > **resourceGroups** > **myAuthResourceGroup** > **providers** > **Microsoft.Web** > **sites** > **_\<front\_end\_app\_name>_** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-230">In the left browser, click **subscriptions** > **_&lt;your\_subscription>_** > **resourceGroups** > **myAuthResourceGroup** > **providers** > **Microsoft.Web** > **sites** > **_\<front\_end\_app\_name>_** > **config** > **authsettings**.</span></span>

<span data-ttu-id="5ecfb-231">In the **authsettings** view, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-231">In the **authsettings** view, click **Edit**.</span></span> <span data-ttu-id="5ecfb-232">Set `additionalLoginParams` to the following JSON string, using the Application ID you copied.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-232">Set `additionalLoginParams` to the following JSON string, using the Application ID you copied.</span></span> 

```json
"additionalLoginParams": ["response_type=code id_token","resource=<back_end_application_id>"],
```

![ASP.NET Core API running in Azure App Service](./media/app-service-web-tutorial-auth-aad/additional-login-params-front-end.png)

<span data-ttu-id="5ecfb-234">Save your settings by clicking **PUT**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-234">Save your settings by clicking **PUT**.</span></span>

<span data-ttu-id="5ecfb-235">Your apps are now configured.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-235">Your apps are now configured.</span></span> <span data-ttu-id="5ecfb-236">The front end is now ready to access the back end with a proper access token.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-236">The front end is now ready to access the back end with a proper access token.</span></span>

<span data-ttu-id="5ecfb-237">For information on how to configure this for other providers, see [Refresh access tokens](app-service-authentication-how-to.md#refresh-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-237">For information on how to configure this for other providers, see [Refresh access tokens](app-service-authentication-how-to.md#refresh-access-tokens).</span></span>

## <a name="call-api-securely-from-server-code"></a><span data-ttu-id="5ecfb-238">Call API securely from server code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-238">Call API securely from server code</span></span>

<span data-ttu-id="5ecfb-239">In this step, you enable your previously modified server code to make authenticated calls to the back-end API.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-239">In this step, you enable your previously modified server code to make authenticated calls to the back-end API.</span></span>

<span data-ttu-id="5ecfb-240">Your front-end app now has the required permission and also adds the back end's Application ID to the login parameters.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-240">Your front-end app now has the required permission and also adds the back end's Application ID to the login parameters.</span></span> <span data-ttu-id="5ecfb-241">Therefore, it can obtain an access token for authentication with the back-end app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-241">Therefore, it can obtain an access token for authentication with the back-end app.</span></span> <span data-ttu-id="5ecfb-242">App Service supplies this token to your server code by injecting a `X-MS-TOKEN-AAD-ACCESS-TOKEN` header to each authenticated request (see [Retrieve tokens in app code](app-service-authentication-how-to.md#retrieve-tokens-in-app-code)).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-242">App Service supplies this token to your server code by injecting a `X-MS-TOKEN-AAD-ACCESS-TOKEN` header to each authenticated request (see [Retrieve tokens in app code](app-service-authentication-how-to.md#retrieve-tokens-in-app-code)).</span></span>

> [!NOTE]
> <span data-ttu-id="5ecfb-243">These headers are injected for all supported languages.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-243">These headers are injected for all supported languages.</span></span> <span data-ttu-id="5ecfb-244">You access them using the standard pattern for each respective language.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-244">You access them using the standard pattern for each respective language.</span></span>

<span data-ttu-id="5ecfb-245">In the local repository, open _Controllers/TodoController.cs_ again.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-245">In the local repository, open _Controllers/TodoController.cs_ again.</span></span> <span data-ttu-id="5ecfb-246">Under the `TodoController(TodoContext context)` constructor, add the following code:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-246">Under the `TodoController(TodoContext context)` constructor, add the following code:</span></span>

```cs
public override void OnActionExecuting(ActionExecutingContext context)
{
    base.OnActionExecuting(context);

    _client.DefaultRequestHeaders.Accept.Clear();
    _client.DefaultRequestHeaders.Authorization =
        new AuthenticationHeaderValue("Bearer", Request.Headers["X-MS-TOKEN-AAD-ACCESS-TOKEN"]);
}
```

<span data-ttu-id="5ecfb-247">This code adds the standard HTTP header `Authorization: Bearer <access_token>` to all remote API calls.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-247">This code adds the standard HTTP header `Authorization: Bearer <access_token>` to all remote API calls.</span></span> <span data-ttu-id="5ecfb-248">In the ASP.NET Core MVC request execution pipeline, `OnActionExecuting` executes just before the respective action method (such as `GetAll()`) does, so each of your outgoing API call now presents the access token.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-248">In the ASP.NET Core MVC request execution pipeline, `OnActionExecuting` executes just before the respective action method (such as `GetAll()`) does, so each of your outgoing API call now presents the access token.</span></span>

<span data-ttu-id="5ecfb-249">Save your all your changes.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-249">Save your all your changes.</span></span> <span data-ttu-id="5ecfb-250">In the local terminal window, deploy your changes to the front-end app with the following Git commands:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-250">In the local terminal window, deploy your changes to the front-end app with the following Git commands:</span></span>

```bash
git add .
git commit -m "add authorization header for server code"
git push frontend master
```

<span data-ttu-id="5ecfb-251">Sign in to `https://<front_end_app_name>.azurewebsites.net` again.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-251">Sign in to `https://<front_end_app_name>.azurewebsites.net` again.</span></span> <span data-ttu-id="5ecfb-252">At the user data usage agreement page, click **Accept**.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-252">At the user data usage agreement page, click **Accept**.</span></span>

<span data-ttu-id="5ecfb-253">You should now be able to create, read, update, and delete data from the back-end app as before.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-253">You should now be able to create, read, update, and delete data from the back-end app as before.</span></span> <span data-ttu-id="5ecfb-254">The only difference now is that both apps are now secured by App Service authentication and authorization, including the service-to-service calls.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-254">The only difference now is that both apps are now secured by App Service authentication and authorization, including the service-to-service calls.</span></span>

<span data-ttu-id="5ecfb-255">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="5ecfb-255">Congratulations!</span></span> <span data-ttu-id="5ecfb-256">Your server code is now accessing the back-end data on behalf of the authenticated user.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-256">Your server code is now accessing the back-end data on behalf of the authenticated user.</span></span>

## <a name="call-api-securely-from-browser-code"></a><span data-ttu-id="5ecfb-257">Call API securely from browser code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-257">Call API securely from browser code</span></span>

<span data-ttu-id="5ecfb-258">In this step, you point the front-end Angular.js app to the back-end API.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-258">In this step, you point the front-end Angular.js app to the back-end API.</span></span> <span data-ttu-id="5ecfb-259">This way, you learn how to retrieve the access token and make API calls to the back-end app with it.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-259">This way, you learn how to retrieve the access token and make API calls to the back-end app with it.</span></span>

<span data-ttu-id="5ecfb-260">While the server code has access to request headers, client code can access `GET /.auth/me` to get the same access tokens (see [Retrieve tokens in app code](app-service-authentication-how-to.md#retrieve-tokens-in-app-code)).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-260">While the server code has access to request headers, client code can access `GET /.auth/me` to get the same access tokens (see [Retrieve tokens in app code](app-service-authentication-how-to.md#retrieve-tokens-in-app-code)).</span></span>

> [!TIP]
> <span data-ttu-id="5ecfb-261">This section uses the standard HTTP methods to demonstrate the secure HTTP calls.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-261">This section uses the standard HTTP methods to demonstrate the secure HTTP calls.</span></span> <span data-ttu-id="5ecfb-262">However, you can use [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) to help simplify the Angular.js application pattern.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-262">However, you can use [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) to help simplify the Angular.js application pattern.</span></span>
>

### <a name="configure-cors"></a><span data-ttu-id="5ecfb-263">Configure CORS</span><span class="sxs-lookup"><span data-stu-id="5ecfb-263">Configure CORS</span></span>

<span data-ttu-id="5ecfb-264">In the Cloud Shell, enable CORS to your client's URL by using the [`az resource update`](/cli/azure/resource#az-resource-update) command.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-264">In the Cloud Shell, enable CORS to your client's URL by using the [`az resource update`](/cli/azure/resource#az-resource-update) command.</span></span> <span data-ttu-id="5ecfb-265">Replace the _\<back\_end\_app\_name>_ and _\<front\_end\_app\_name>_ placeholders.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-265">Replace the _\<back\_end\_app\_name>_ and _\<front\_end\_app\_name>_ placeholders.</span></span>

```azurecli-interactive
az resource update --name web --resource-group myAuthResourceGroup --namespace Microsoft.Web --resource-type config --parent sites/<back_end_app_name> --set properties.cors.allowedOrigins="['https://<front_end_app_name>.azurewebsites.net']" --api-version 2015-06-01
```

<span data-ttu-id="5ecfb-266">This step is not related to authentication and authorization.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-266">This step is not related to authentication and authorization.</span></span> <span data-ttu-id="5ecfb-267">However, you need it so that your browser allows the cross-domain API calls from your Angular.js app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-267">However, you need it so that your browser allows the cross-domain API calls from your Angular.js app.</span></span> <span data-ttu-id="5ecfb-268">For more information, see [Add CORS functionality](app-service-web-tutorial-rest-api.md#add-cors-functionality).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-268">For more information, see [Add CORS functionality](app-service-web-tutorial-rest-api.md#add-cors-functionality).</span></span>

### <a name="point-angularjs-app-to-back-end-api"></a><span data-ttu-id="5ecfb-269">Point Angular.js app to back-end API</span><span class="sxs-lookup"><span data-stu-id="5ecfb-269">Point Angular.js app to back-end API</span></span>

<span data-ttu-id="5ecfb-270">In the local repository, open _wwwroot/index.html_.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-270">In the local repository, open _wwwroot/index.html_.</span></span>

<span data-ttu-id="5ecfb-271">In Line 51, set the `apiEndpoint` variable to the URL of your back-end app (`https://<back_end_app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-271">In Line 51, set the `apiEndpoint` variable to the URL of your back-end app (`https://<back_end_app_name>.azurewebsites.net`).</span></span> <span data-ttu-id="5ecfb-272">Replace _\<back\_end\_app\_name>_ with your app name in App Service.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-272">Replace _\<back\_end\_app\_name>_ with your app name in App Service.</span></span>

<span data-ttu-id="5ecfb-273">In the local repository, open _wwwroot/app/scripts/todoListSvc.js_ and see that `apiEndpoint` is prepended to all the API calls.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-273">In the local repository, open _wwwroot/app/scripts/todoListSvc.js_ and see that `apiEndpoint` is prepended to all the API calls.</span></span> <span data-ttu-id="5ecfb-274">Your Angular.js app is now calling the back-end APIs.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-274">Your Angular.js app is now calling the back-end APIs.</span></span> 

### <a name="add-access-token-to-api-calls"></a><span data-ttu-id="5ecfb-275">Add access token to API calls</span><span class="sxs-lookup"><span data-stu-id="5ecfb-275">Add access token to API calls</span></span>

<span data-ttu-id="5ecfb-276">In _wwwroot/app/scripts/todoListSvc.js_, above the list of API calls (above the line `getItems : function(){`), add the following function to the list:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-276">In _wwwroot/app/scripts/todoListSvc.js_, above the list of API calls (above the line `getItems : function(){`), add the following function to the list:</span></span>

```javascript
setAuth: function (token) {
    $http.defaults.headers.common['Authorization'] = 'Bearer ' + token;
},
```

<span data-ttu-id="5ecfb-277">This function is called to set the default `Authorization` header with the access token.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-277">This function is called to set the default `Authorization` header with the access token.</span></span> <span data-ttu-id="5ecfb-278">You call it in the next step.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-278">You call it in the next step.</span></span>

<span data-ttu-id="5ecfb-279">In the local repository, open _wwwroot/app/scripts/app.js_ and find the following code:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-279">In the local repository, open _wwwroot/app/scripts/app.js_ and find the following code:</span></span>

```javascript
$routeProvider.when("/Home", {
    controller: "todoListCtrl",
    templateUrl: "/App/Views/TodoList.html",
}).otherwise({ redirectTo: "/Home" });
```

<span data-ttu-id="5ecfb-280">Replace the entire code block with the following code:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-280">Replace the entire code block with the following code:</span></span>

```javascript
$routeProvider.when("/Home", {
    controller: "todoListCtrl",
    templateUrl: "/App/Views/TodoList.html",
    resolve: {
        token: ['$http', 'todoListSvc', function ($http, todoListSvc) {
            return $http.get('/.auth/me').then(function (response) {
                todoListSvc.setAuth(response.data[0].access_token);
                return response.data[0].access_token;
            });
        }]
    },
}).otherwise({ redirectTo: "/Home" });
```

<span data-ttu-id="5ecfb-281">The new change adds the `revolve` mapping that calls `/.auth/me` and sets the access token.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-281">The new change adds the `revolve` mapping that calls `/.auth/me` and sets the access token.</span></span> <span data-ttu-id="5ecfb-282">It makes sure you have the access token before instantiating the `todoListCtrl` controller.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-282">It makes sure you have the access token before instantiating the `todoListCtrl` controller.</span></span> <span data-ttu-id="5ecfb-283">That way all API calls by the controller includes the token.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-283">That way all API calls by the controller includes the token.</span></span>

### <a name="deploy-updates-and-test"></a><span data-ttu-id="5ecfb-284">Deploy updates and test</span><span class="sxs-lookup"><span data-stu-id="5ecfb-284">Deploy updates and test</span></span>

<span data-ttu-id="5ecfb-285">Save your all your changes.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-285">Save your all your changes.</span></span> <span data-ttu-id="5ecfb-286">In the local terminal window, deploy your changes to the front-end app with the following Git commands:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-286">In the local terminal window, deploy your changes to the front-end app with the following Git commands:</span></span>

```bash
git add .
git commit -m "add authorization header for Angular"
git push frontend master
```

<span data-ttu-id="5ecfb-287">Navigate to `https://<front_end_app_name>.azurewebsites.net` again.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-287">Navigate to `https://<front_end_app_name>.azurewebsites.net` again.</span></span> <span data-ttu-id="5ecfb-288">You should now be able to create, read, update, and delete data from the back-end app, directly in the Angular.js app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-288">You should now be able to create, read, update, and delete data from the back-end app, directly in the Angular.js app.</span></span>

<span data-ttu-id="5ecfb-289">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="5ecfb-289">Congratulations!</span></span> <span data-ttu-id="5ecfb-290">Your client code is now accessing the back-end data on behalf of the authenticated user.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-290">Your client code is now accessing the back-end data on behalf of the authenticated user.</span></span>

## <a name="when-access-tokens-expire"></a><span data-ttu-id="5ecfb-291">When access tokens expire</span><span class="sxs-lookup"><span data-stu-id="5ecfb-291">When access tokens expire</span></span>

<span data-ttu-id="5ecfb-292">Your access token expires after some time.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-292">Your access token expires after some time.</span></span> <span data-ttu-id="5ecfb-293">For information on how to refresh your access tokens without requiring users to reauthenticate with your app, see [Refresh access tokens](app-service-authentication-how-to.md#refresh-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="5ecfb-293">For information on how to refresh your access tokens without requiring users to reauthenticate with your app, see [Refresh access tokens](app-service-authentication-how-to.md#refresh-access-tokens).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5ecfb-294">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="5ecfb-294">Clean up resources</span></span>

<span data-ttu-id="5ecfb-295">In the preceding steps, you created Azure resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-295">In the preceding steps, you created Azure resources in a resource group.</span></span> <span data-ttu-id="5ecfb-296">If you don't expect to need these resources in the future, delete the resource group by running the following command in the Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-296">If you don't expect to need these resources in the future, delete the resource group by running the following command in the Cloud Shell:</span></span>

```azurecli-interactive
az group delete --name myAuthResourceGroup
```

<span data-ttu-id="5ecfb-297">This command may take a minute to run.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-297">This command may take a minute to run.</span></span>

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="5ecfb-298">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ecfb-298">Next steps</span></span>

<span data-ttu-id="5ecfb-299">What you learned:</span><span class="sxs-lookup"><span data-stu-id="5ecfb-299">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ecfb-300">Enable built-in authentication and authorization</span><span class="sxs-lookup"><span data-stu-id="5ecfb-300">Enable built-in authentication and authorization</span></span>
> * <span data-ttu-id="5ecfb-301">Secure apps against unauthenticated requests</span><span class="sxs-lookup"><span data-stu-id="5ecfb-301">Secure apps against unauthenticated requests</span></span>
> * <span data-ttu-id="5ecfb-302">Use Azure Active Directory as the identity provider</span><span class="sxs-lookup"><span data-stu-id="5ecfb-302">Use Azure Active Directory as the identity provider</span></span>
> * <span data-ttu-id="5ecfb-303">Access a remote app on behalf of the signed-in user</span><span class="sxs-lookup"><span data-stu-id="5ecfb-303">Access a remote app on behalf of the signed-in user</span></span>
> * <span data-ttu-id="5ecfb-304">Secure service-to-service calls with token authentication</span><span class="sxs-lookup"><span data-stu-id="5ecfb-304">Secure service-to-service calls with token authentication</span></span>
> * <span data-ttu-id="5ecfb-305">Use access tokens from server code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-305">Use access tokens from server code</span></span>
> * <span data-ttu-id="5ecfb-306">Use access tokens from client (browser) code</span><span class="sxs-lookup"><span data-stu-id="5ecfb-306">Use access tokens from client (browser) code</span></span>

<span data-ttu-id="5ecfb-307">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span><span class="sxs-lookup"><span data-stu-id="5ecfb-307">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ecfb-308">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="5ecfb-308">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
