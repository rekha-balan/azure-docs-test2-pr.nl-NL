---
title: CORS support in App Service | Microsoft Docs
description: Learn how to use CORS support in Azure Azure App Service.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: ''
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: d8f8224b7177219a31ff0a776f22cce104eabed7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661794"
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="cdbfb-103">Consume an API app from JavaScript using CORS</span><span class="sxs-lookup"><span data-stu-id="cdbfb-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="cdbfb-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="cdbfb-105">App Service lets you configure CORS access to your API without writing any code in your API.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="cdbfb-106">This article contains two sections:</span><span class="sxs-lookup"><span data-stu-id="cdbfb-106">This article contains two sections:</span></span>

* <span data-ttu-id="cdbfb-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="cdbfb-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="cdbfb-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <a id="corsconfig"></a> <span data-ttu-id="cdbfb-110">How to configure CORS in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cdbfb-110">How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="cdbfb-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="cdbfb-112">Configure CORS in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cdbfb-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="cdbfb-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cdbfb-114">Click **App Services**, and then click the name of your API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![Select API app in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="cdbfb-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Select CORS in Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="cdbfb-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="cdbfb-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="cdbfb-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="cdbfb-120">As an alternative, you can enter an asterisk (\*) to specify that all origin domains are accepted.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-120">As an alternative, you can enter an asterisk (\*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="cdbfb-121">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-121">Click **Save**.</span></span>
   
   ![Click Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="cdbfb-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="cdbfb-124">Configure CORS by using Azure Resource Manager tools</span><span class="sxs-lookup"><span data-stu-id="cdbfb-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="cdbfb-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="cdbfb-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="cdbfb-127">Find the section of the template that looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="cdbfb-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a> <span data-ttu-id="cdbfb-128">Continuing the .NET getting-started tutorial</span><span class="sxs-lookup"><span data-stu-id="cdbfb-128">Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="cdbfb-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="cdbfb-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="cdbfb-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="cdbfb-132">Deploy the ToDoListAngular project to a new web app</span><span class="sxs-lookup"><span data-stu-id="cdbfb-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="cdbfb-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="cdbfb-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="cdbfb-135">For the SPA to work you have to enable CORS on the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="cdbfb-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="cdbfb-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="cdbfb-138">Create a new web app for the ToDoListAngular project</span><span class="sxs-lookup"><span data-stu-id="cdbfb-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="cdbfb-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="cdbfb-140">The only difference is that the app type is **Web App** instead of **API App**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="cdbfb-141">For screen shots of the dialogs, see</span><span class="sxs-lookup"><span data-stu-id="cdbfb-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="cdbfb-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="cdbfb-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="cdbfb-144">In the **App Service** dialog box, click **New**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="cdbfb-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="cdbfb-146">Choose the Azure **Subscription** you want to work with.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="cdbfb-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="cdbfb-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="cdbfb-149">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-149">Click **Create**.</span></span>
   
    <span data-ttu-id="cdbfb-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="cdbfb-151">Don't click **Publish** yet.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="cdbfb-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="cdbfb-153">Set the middle tier URL in web app settings</span><span class="sxs-lookup"><span data-stu-id="cdbfb-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="cdbfb-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="cdbfb-155">Click **Settings > Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="cdbfb-156">In the **App settings** section, add the following key and value:</span><span class="sxs-lookup"><span data-stu-id="cdbfb-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="cdbfb-157">Key</span><span class="sxs-lookup"><span data-stu-id="cdbfb-157">Key</span></span> | <span data-ttu-id="cdbfb-158">Value</span><span class="sxs-lookup"><span data-stu-id="cdbfb-158">Value</span></span> | <span data-ttu-id="cdbfb-159">Example</span><span class="sxs-lookup"><span data-stu-id="cdbfb-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="cdbfb-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="cdbfb-160">toDoListAPIURL</span></span> |<span data-ttu-id="cdbfb-161">https://{your middle tier API app name}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="cdbfb-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |https://todolistapi0121.azurewebsites.net |
4. <span data-ttu-id="cdbfb-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-162">Click **Save**.</span></span>
   
    <span data-ttu-id="cdbfb-163">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-163">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="cdbfb-164">The code that gets the setting value is in *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="cdbfb-164">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="cdbfb-165">The code in *todoListSvc.js* uses the setting:</span><span class="sxs-lookup"><span data-stu-id="cdbfb-165">The code in *todoListSvc.js* uses the setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="cdbfb-166">Deploy the ToDoListAngular web project to the new web app</span><span class="sxs-lookup"><span data-stu-id="cdbfb-166">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="cdbfb-167">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-167">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="cdbfb-168">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-168">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="cdbfb-169">Test the application without CORS enabled</span><span class="sxs-lookup"><span data-stu-id="cdbfb-169">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="cdbfb-170">In your browser Developer Tools, open the Console window.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-170">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="cdbfb-171">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-171">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="cdbfb-172">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-172">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="cdbfb-173">The browser's Developer Tools Console window shows a cross-origin error message.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-173">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Cross-origin error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="cdbfb-175">Configure CORS for the middle tier API app</span><span class="sxs-lookup"><span data-stu-id="cdbfb-175">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="cdbfb-176">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-176">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="cdbfb-177">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-177">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="cdbfb-178">In a browser, go to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-178">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cdbfb-179">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-179">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![Select API app in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="cdbfb-181">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-181">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Select CORS in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="cdbfb-183">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-183">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="cdbfb-184">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-184">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="cdbfb-185">As an alternative, you can enter an asterisk (\*) to specify that all origin domains are accepted.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-185">As an alternative, you can enter an asterisk (\*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="cdbfb-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-186">Click **Save**.</span></span>
   
   ![Click Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="cdbfb-188">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-188">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="cdbfb-189">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-189">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="cdbfb-190">Test the application with CORS enabled</span><span class="sxs-lookup"><span data-stu-id="cdbfb-190">Test the application with CORS enabled</span></span>
* <span data-ttu-id="cdbfb-191">Open a browser to the HTTPS URL of the web app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-191">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="cdbfb-192">This time the application lets you view, add, edit, and delete to-do items.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-192">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![To Do List page of sample app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="cdbfb-194">App Service CORS versus Web API CORS</span><span class="sxs-lookup"><span data-stu-id="cdbfb-194">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="cdbfb-195">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-195">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="cdbfb-196">Web API CORS support is more flexible than App Service CORS support.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-196">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="cdbfb-197">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-197">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="cdbfb-198">Don't try to use both Web API CORS and App Service CORS in one API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-198">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="cdbfb-199">App Service CORS will take precedence and Web API CORS will have no effect.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-199">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="cdbfb-200">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-200">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="cdbfb-201">How to enable CORS in Web API code</span><span class="sxs-lookup"><span data-stu-id="cdbfb-201">How to enable CORS in Web API code</span></span>
<span data-ttu-id="cdbfb-202">The following steps summarize the process for enabling Web API CORS support.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-202">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="cdbfb-203">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-203">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="cdbfb-204">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-204">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="cdbfb-205">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-205">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="cdbfb-206">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-206">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="cdbfb-207">In the following example, CORS support applies to the entire controller.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-207">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="cdbfb-208">Using Azure API Management with API Apps</span><span class="sxs-lookup"><span data-stu-id="cdbfb-208">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="cdbfb-209">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-209">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="cdbfb-210">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="cdbfb-210">For more information, see the following resources:</span></span>

* [<span data-ttu-id="cdbfb-211">Azure API Management Overview (video: CORS starts at 12:10)</span><span class="sxs-lookup"><span data-stu-id="cdbfb-211">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="cdbfb-212">API Management cross domain policies</span><span class="sxs-lookup"><span data-stu-id="cdbfb-212">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="cdbfb-213">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="cdbfb-213">Troubleshooting</span></span>
<span data-ttu-id="cdbfb-214">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-214">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="cdbfb-215">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-215">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="cdbfb-216">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-216">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="cdbfb-217">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-217">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="cdbfb-218">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-218">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="cdbfb-219">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="cdbfb-219">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdbfb-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="cdbfb-220">Next steps</span></span>
<span data-ttu-id="cdbfb-221">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-221">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="cdbfb-222">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="cdbfb-222">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>









