---
title: Get started with API Apps and ASP.NET in App Service | Microsoft Docs
description: Learn how to create, deploy, and consume an ASP.NET API app in Azure App Service, by using Visual Studio 2015.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: ''
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: da399fc45be35c3e94093f984ee84bd0d49e3af2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553775"
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="ed4ed-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ed4ed-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="ed4ed-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="ed4ed-105">This tutorial covers support for API metadata in Swagger format.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="ed4ed-106">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-106">You'll learn:</span></span>

* <span data-ttu-id="ed4ed-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="ed4ed-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="ed4ed-109">How to use Swagger API metadata to automatically generate client code for an API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="ed4ed-110">Sample application overview</span><span class="sxs-lookup"><span data-stu-id="ed4ed-110">Sample application overview</span></span>
<span data-ttu-id="ed4ed-111">In this tutorial, you work with a simple to-do list sample application.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="ed4ed-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![API Apps sample application diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="ed4ed-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![API Apps sample application to do list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="ed4ed-116">The Visual Studio solution includes three projects:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-116">The Visual Studio solution includes three projects:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="ed4ed-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="ed4ed-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="ed4ed-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="ed4ed-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="ed4ed-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="ed4ed-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="ed4ed-123">The next tutorial in the series deploys the SPA front end to the cloud.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed4ed-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ed4ed-124">Prerequisites</span></span>
* <span data-ttu-id="ed4ed-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="ed4ed-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="ed4ed-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="ed4ed-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="ed4ed-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="ed4ed-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Azure App Tools vesion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="ed4ed-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="ed4ed-133">Download the sample application</span><span class="sxs-lookup"><span data-stu-id="ed4ed-133">Download the sample application</span></span>
1. <span data-ttu-id="ed4ed-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="ed4ed-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="ed4ed-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="ed4ed-137">You will need to trust each solution.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="ed4ed-138">![Security Warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-138">![Security Warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="ed4ed-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="ed4ed-140">If you want to see the application in operation before you deploy it, you can run it locally.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="ed4ed-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="ed4ed-142">You should expect to see a HTTP 403 error in your browser.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="ed4ed-143">Use Swagger API metadata and UI</span><span class="sxs-lookup"><span data-stu-id="ed4ed-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="ed4ed-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="ed4ed-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="ed4ed-146">The metadata returned from that endpoint can be used to generate client code.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="ed4ed-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="ed4ed-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="ed4ed-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="ed4ed-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![Set ToDoDataAPI as Startup Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="ed4ed-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="ed4ed-153">The browser opens and shows the HTTP 403 error page.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="ed4ed-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="ed4ed-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="ed4ed-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="ed4ed-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![Download JSON metadata in IE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="ed4ed-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="ed4ed-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![JSON metadata in Chrome](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="ed4ed-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="ed4ed-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="ed4ed-164">Close the browser and stop Visual Studio debugging.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="ed4ed-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="ed4ed-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="ed4ed-167">The file provides a number of ways to configure Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="ed4ed-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="ed4ed-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="ed4ed-170">Run the project again.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-170">Run the project again.</span></span>
7. <span data-ttu-id="ed4ed-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="ed4ed-172">(The URL is `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="ed4ed-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Swagger UI available methods](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="ed4ed-175">Click the first **Get** button in the list.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="ed4ed-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="ed4ed-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="ed4ed-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Swagger UI try it out](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="ed4ed-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Swagger UI try it out results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="ed4ed-182">Click **Post**, and then click the box under **Model Schema**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="ed4ed-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="ed4ed-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Swagger UI try it out Post](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="ed4ed-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="ed4ed-187">Click **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="ed4ed-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="ed4ed-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="ed4ed-190">The Get method response now includes the new to do item.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="ed4ed-191">Optional: Try also the Put, Delete, and Get by ID methods.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="ed4ed-192">Close the browser and stop Visual Studio debugging.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="ed4ed-193">Swashbuckle works with any ASP.NET Web API project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="ed4ed-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="ed4ed-195">Swagger metadata includes a unique ID for each API operation.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="ed4ed-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="ed4ed-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="ed4ed-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="ed4ed-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <a id="createapiapp"></a> <span data-ttu-id="ed4ed-200">Create an API app in Azure and deploy code to it</span><span class="sxs-lookup"><span data-stu-id="ed4ed-200">Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="ed4ed-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="ed4ed-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="ed4ed-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Click Publish in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="ed4ed-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Click Azure App Service in Publish Web](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="ed4ed-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="ed4ed-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Click New in App Service dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="ed4ed-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="ed4ed-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="ed4ed-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![App type in App Service dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="ed4ed-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="ed4ed-215">You can accept the default name that Visual Studio proposes.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="ed4ed-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="ed4ed-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="ed4ed-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="ed4ed-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="ed4ed-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="ed4ed-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="ed4ed-222">Click the **New** button next to the **App Service Plan** drop-down.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="ed4ed-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Create App Service dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="ed4ed-225">In the following steps you create an App Service plan for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="ed4ed-226">An App Service plan specifies the compute resources that your API app runs on.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="ed4ed-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="ed4ed-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="ed4ed-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="ed4ed-230">In the **Location** drop-down list, choose the location that is closest to you.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="ed4ed-231">This setting specifies which Azure datacenter your app will run in.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="ed4ed-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="ed4ed-233">In the **Size** drop-down, click **Free**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="ed4ed-234">For this tutorial, the free pricing tier will provide sufficient performance.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="ed4ed-235">In the **Configure App Service Plan** dialog, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Click OK in Configure App Service Plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="ed4ed-237">In the **Create App Service** dialog box, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Click Create in Create App Service dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="ed4ed-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="ed4ed-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="ed4ed-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="ed4ed-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="ed4ed-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="ed4ed-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="ed4ed-245">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-245">Click **Next**.</span></span>
    
    ![Click Next in Connection tab of Publish Web](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="ed4ed-247">The next tab is the **Settings** tab (shown below).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="ed4ed-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="ed4ed-249">The tab also offers several **File Publish Options**:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="ed4ed-250">Remove additional files at destination</span><span class="sxs-lookup"><span data-stu-id="ed4ed-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="ed4ed-251">Precompile during publishing</span><span class="sxs-lookup"><span data-stu-id="ed4ed-251">Precompile during publishing</span></span>
    * <span data-ttu-id="ed4ed-252">Exclude files from the App_Data folder</span><span class="sxs-lookup"><span data-stu-id="ed4ed-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="ed4ed-253">For this tutorial you don't need any of these.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="ed4ed-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="ed4ed-255">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-255">Click **Next**.</span></span>
    
    ![Click Next in Settings tab of Publish Web](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="ed4ed-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="ed4ed-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="ed4ed-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="ed4ed-260">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-260">Click **Publish**.</span></span>
    
    ![Click Publish in Preview tab of Publish Web](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="ed4ed-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="ed4ed-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Output window successful deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![New API app successfully created page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="ed4ed-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="ed4ed-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="ed4ed-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="ed4ed-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="ed4ed-270">The changes you made earlier were saved in memory in the local machine.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="ed4ed-271">Open the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="ed4ed-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="ed4ed-273">Click **More Services > App Services**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-273">Click **More Services > App Services**.</span></span>
    
    ![Browse App Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="ed4ed-275">In the **App Services** blade, find and click your new API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="ed4ed-276">(In the Azure portal, windows that open to the right are called *blades*.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![App Services blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="ed4ed-278">Two blades open.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-278">Two blades open.</span></span> <span data-ttu-id="ed4ed-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="ed4ed-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![API Definition in Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="ed4ed-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="ed4ed-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![API definition URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="ed4ed-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <a id="codegen"></a> <span data-ttu-id="ed4ed-286">Generate client code for the data tier</span><span class="sxs-lookup"><span data-stu-id="ed4ed-286">Generate client code for the data tier</span></span>
<span data-ttu-id="ed4ed-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="ed4ed-288">Generated client classes make it easier to write code that calls an API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="ed4ed-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="ed4ed-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="ed4ed-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Delete generated client code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="ed4ed-293">This folder was created by using the code generation process that you're about to go through.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="ed4ed-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Add REST API client in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="ed4ed-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Select Azure Asset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="ed4ed-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Select API app for code generation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="ed4ed-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![API Definition URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="ed4ed-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="ed4ed-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="ed4ed-304">In the **Add REST API Client** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="ed4ed-305">Visual Studio creates a folder named after the API app and generates client classes.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Code files for generated client](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="ed4ed-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="ed4ed-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="ed4ed-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="ed4ed-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="ed4ed-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="ed4ed-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="ed4ed-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="ed4ed-314">to this:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="ed4ed-315">Create an API app to host the middle tier</span><span class="sxs-lookup"><span data-stu-id="ed4ed-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="ed4ed-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="ed4ed-317">Now you follow the same procedure for the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="ed4ed-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Click Publish in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="ed4ed-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="ed4ed-321">In the **App Service** dialog box, click **New**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="ed4ed-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="ed4ed-323">Choose the Azure **Subscription** you have been using.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="ed4ed-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="ed4ed-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="ed4ed-326">It will default to that value.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-326">It will default to that value.</span></span>
8. <span data-ttu-id="ed4ed-327">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-327">Click **Create**.</span></span>
   
    <span data-ttu-id="ed4ed-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="ed4ed-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="ed4ed-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="ed4ed-331">The "successfully created" page appears.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="ed4ed-332">Configure the middle tier to call the data tier</span><span class="sxs-lookup"><span data-stu-id="ed4ed-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="ed4ed-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="ed4ed-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="ed4ed-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="ed4ed-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="ed4ed-337">In the API App's **Settings** blade, click **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="ed4ed-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="ed4ed-339">The value will be the URL of the first API App you published in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="ed4ed-340">**Key**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-340">**Key**</span></span> | <span data-ttu-id="ed4ed-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="ed4ed-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="ed4ed-342">**Value**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-342">**Value**</span></span> |<span data-ttu-id="ed4ed-343">https://{your data tier API app name}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ed4ed-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="ed4ed-344">**Example**</span><span class="sxs-lookup"><span data-stu-id="ed4ed-344">**Example**</span></span> |https://todolistdataapi.azurewebsites.net |
4. <span data-ttu-id="ed4ed-345">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-345">Click **Save**.</span></span>
   
    ![Click Save for App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="ed4ed-347">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-347">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="ed4ed-348">Test</span><span class="sxs-lookup"><span data-stu-id="ed4ed-348">Test</span></span>
1. <span data-ttu-id="ed4ed-349">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-349">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="ed4ed-350">You can get there by clicking the URL in the API app's main blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-350">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="ed4ed-351">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-351">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="ed4ed-352">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-352">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="ed4ed-353">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-353">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="ed4ed-354">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span><span class="sxs-lookup"><span data-stu-id="ed4ed-354">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="ed4ed-355">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-355">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Swagger UI Get method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="ed4ed-357">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ed4ed-357">Troubleshooting</span></span>
<span data-ttu-id="ed4ed-358">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span><span class="sxs-lookup"><span data-stu-id="ed4ed-358">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="ed4ed-359">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-359">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="ed4ed-360">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-360">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="ed4ed-361">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-361">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="ed4ed-362">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-362">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="ed4ed-363">If you can't open those ports, you can use other deployment methods.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-363">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="ed4ed-364">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-364">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="ed4ed-365">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-365">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="ed4ed-366">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-366">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="ed4ed-367">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-367">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="ed4ed-368">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-368">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed4ed-369">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed4ed-369">Next steps</span></span>
<span data-ttu-id="ed4ed-370">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-370">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="ed4ed-371">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-371">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="ed4ed-372">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-372">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="ed4ed-373">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="ed4ed-373">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="ed4ed-374">If you want to create new API app projects from scratch, use the **Azure API App** template.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-374">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![API App template in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="ed4ed-376">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-376">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="ed4ed-377">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-377">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="ed4ed-378">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed4ed-378">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>







































