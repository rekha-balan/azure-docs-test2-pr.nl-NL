---
title: How to work with the .NET backend server SDK for Mobile Apps | Microsoft Docs
description: Learn how to work with the .NET backend server SDK for Azure App Service Mobile Apps.
keywords: app service, azure app service, mobile app, mobile service, scale, scalable, app deployment, azure app deployment
services: app-service\mobile
documentationcenter: ''
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 0c40621a3c38c023f25808213985592e0a6bee5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670159"
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="12cf2-104">Work with the .NET backend server SDK for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="12cf2-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="12cf2-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span><span class="sxs-lookup"><span data-stu-id="12cf2-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="12cf2-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span><span class="sxs-lookup"><span data-stu-id="12cf2-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="12cf2-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span><span class="sxs-lookup"><span data-stu-id="12cf2-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="12cf2-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span><span class="sxs-lookup"><span data-stu-id="12cf2-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
> 
> 

## <a name="reference-documentation"></a><span data-ttu-id="12cf2-109">Reference documentation</span><span class="sxs-lookup"><span data-stu-id="12cf2-109">Reference documentation</span></span>
<span data-ttu-id="12cf2-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span><span class="sxs-lookup"><span data-stu-id="12cf2-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <a name="create-app"></a><span data-ttu-id="12cf2-111">How to: Create a .NET Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="12cf2-111">How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="12cf2-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12cf2-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="12cf2-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span><span class="sxs-lookup"><span data-stu-id="12cf2-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>  

<span data-ttu-id="12cf2-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span><span class="sxs-lookup"><span data-stu-id="12cf2-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="12cf2-115">Create a .NET backend using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="12cf2-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="12cf2-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span><span class="sxs-lookup"><span data-stu-id="12cf2-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="12cf2-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="12cf2-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12cf2-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="12cf2-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="12cf2-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="12cf2-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12cf2-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="12cf2-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span><span class="sxs-lookup"><span data-stu-id="12cf2-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="12cf2-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span><span class="sxs-lookup"><span data-stu-id="12cf2-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="12cf2-123">Expand **Templates** > **Visual C#**, and select **Web**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="12cf2-124">Select **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="12cf2-125">Fill in the project name.</span><span class="sxs-lookup"><span data-stu-id="12cf2-125">Fill in the project name.</span></span> <span data-ttu-id="12cf2-126">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-126">Then click **OK**.</span></span>
5. <span data-ttu-id="12cf2-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="12cf2-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span><span class="sxs-lookup"><span data-stu-id="12cf2-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="12cf2-129">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-129">Click **OK**.</span></span>

## <a name="install-sdk"></a><span data-ttu-id="12cf2-130">How to: Download and initialize the SDK</span><span class="sxs-lookup"><span data-stu-id="12cf2-130">How to: Download and initialize the SDK</span></span>
<span data-ttu-id="12cf2-131">The SDK is available on [NuGet.org]. This package includes the base functionality required to get started using the SDK.</span><span class="sxs-lookup"><span data-stu-id="12cf2-131">The SDK is available on [NuGet.org]. This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="12cf2-132">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span><span class="sxs-lookup"><span data-stu-id="12cf2-132">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="12cf2-133">Install the SDK</span><span class="sxs-lookup"><span data-stu-id="12cf2-133">Install the SDK</span></span>
<span data-ttu-id="12cf2-134">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-134">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <a name="server-project-setup"></a> <span data-ttu-id="12cf2-135">Initialize the server project</span><span class="sxs-lookup"><span data-stu-id="12cf2-135">Initialize the server project</span></span>
<span data-ttu-id="12cf2-136">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span><span class="sxs-lookup"><span data-stu-id="12cf2-136">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="12cf2-137">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="12cf2-137">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="12cf2-138">To add this class in Visual Studio, right-click on your server project and select **Add** > 
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-138">To add this class in Visual Studio, right-click on your server project and select **Add** > 
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="12cf2-139">A class is generated with the following attribute:</span><span class="sxs-lookup"><span data-stu-id="12cf2-139">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="12cf2-140">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span><span class="sxs-lookup"><span data-stu-id="12cf2-140">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="12cf2-141">The following example initializes the server project with no added features:</span><span class="sxs-lookup"><span data-stu-id="12cf2-141">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="12cf2-142">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-142">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="12cf2-143">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span><span class="sxs-lookup"><span data-stu-id="12cf2-143">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="12cf2-144">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-144">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="12cf2-145">This equivalent to the following setup:</span><span class="sxs-lookup"><span data-stu-id="12cf2-145">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="12cf2-146">The extension methods used are:</span><span class="sxs-lookup"><span data-stu-id="12cf2-146">The extension methods used are:</span></span>

* <span data-ttu-id="12cf2-147">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span><span class="sxs-lookup"><span data-stu-id="12cf2-147">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="12cf2-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span><span class="sxs-lookup"><span data-stu-id="12cf2-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="12cf2-149">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span><span class="sxs-lookup"><span data-stu-id="12cf2-149">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="12cf2-150">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span><span class="sxs-lookup"><span data-stu-id="12cf2-150">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="12cf2-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="12cf2-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="12cf2-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span><span class="sxs-lookup"><span data-stu-id="12cf2-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="12cf2-153">SDK extensions</span><span class="sxs-lookup"><span data-stu-id="12cf2-153">SDK extensions</span></span>
<span data-ttu-id="12cf2-154">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span><span class="sxs-lookup"><span data-stu-id="12cf2-154">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="12cf2-155">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span><span class="sxs-lookup"><span data-stu-id="12cf2-155">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="12cf2-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span><span class="sxs-lookup"><span data-stu-id="12cf2-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="12cf2-157">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span><span class="sxs-lookup"><span data-stu-id="12cf2-157">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="12cf2-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span><span class="sxs-lookup"><span data-stu-id="12cf2-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="12cf2-159">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="12cf2-159">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="12cf2-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span><span class="sxs-lookup"><span data-stu-id="12cf2-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="12cf2-161">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-161">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="12cf2-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span><span class="sxs-lookup"><span data-stu-id="12cf2-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="12cf2-163">Add to the configuration by calling the **AddTables** extension method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-163">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="12cf2-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="12cf2-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="12cf2-165">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-165">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="12cf2-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span><span class="sxs-lookup"><span data-stu-id="12cf2-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="12cf2-167">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span><span class="sxs-lookup"><span data-stu-id="12cf2-167">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="12cf2-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span><span class="sxs-lookup"><span data-stu-id="12cf2-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="12cf2-169">Add to the configuration by calling the **AddPushNotifications** extension method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-169">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="12cf2-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span><span class="sxs-lookup"><span data-stu-id="12cf2-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="12cf2-171">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-171">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="12cf2-172">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span><span class="sxs-lookup"><span data-stu-id="12cf2-172">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>   

## <a name="publish-server-project"></a><span data-ttu-id="12cf2-173">How to: Publish the server project</span><span class="sxs-lookup"><span data-stu-id="12cf2-173">How to: Publish the server project</span></span>
<span data-ttu-id="12cf2-174">This section shows you how to publish your .NET backend project from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12cf2-174">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="12cf2-175">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="12cf2-175">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="12cf2-176">In Visual Studio, rebuild the project to restore NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="12cf2-176">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="12cf2-177">In Solution Explorer, right-click the project, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-177">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="12cf2-178">The first time you publish, you need to define a publishing profile.</span><span class="sxs-lookup"><span data-stu-id="12cf2-178">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="12cf2-179">When you already have a profile defined, you can select it and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="12cf2-180">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="12cf2-180">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span> 
   <span data-ttu-id="12cf2-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span><span class="sxs-lookup"><span data-stu-id="12cf2-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="12cf2-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="12cf2-183">Verify the publish profile information and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-183">Verify the publish profile information and click **Publish**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)
   
    <span data-ttu-id="12cf2-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span><span class="sxs-lookup"><span data-stu-id="12cf2-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> <span data-ttu-id="12cf2-185">How to: Define a table controller</span><span class="sxs-lookup"><span data-stu-id="12cf2-185">How to: Define a table controller</span></span>
<span data-ttu-id="12cf2-186">Define a Table Controller to expose a SQL table to mobile clients.</span><span class="sxs-lookup"><span data-stu-id="12cf2-186">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="12cf2-187">Configuring a Table Controller requires three steps:</span><span class="sxs-lookup"><span data-stu-id="12cf2-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="12cf2-188">Create a Data Transfer Object (DTO) class.</span><span class="sxs-lookup"><span data-stu-id="12cf2-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="12cf2-189">Configure a table reference in the Mobile DbContext class.</span><span class="sxs-lookup"><span data-stu-id="12cf2-189">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="12cf2-190">Create a table controller.</span><span class="sxs-lookup"><span data-stu-id="12cf2-190">Create a table controller.</span></span>

<span data-ttu-id="12cf2-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="12cf2-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="12cf2-192">For example:</span><span class="sxs-lookup"><span data-stu-id="12cf2-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="12cf2-193">The DTO is used to define the table within the SQL database.</span><span class="sxs-lookup"><span data-stu-id="12cf2-193">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="12cf2-194">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span><span class="sxs-lookup"><span data-stu-id="12cf2-194">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="12cf2-195">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="12cf2-195">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="12cf2-196">If you have the Azure SDK installed, you can now create a template table controller as follows:</span><span class="sxs-lookup"><span data-stu-id="12cf2-196">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="12cf2-197">Right-click on the Controllers folder and select **Add** > **Controller...**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-197">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="12cf2-198">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-198">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="12cf2-199">In the **Add Controller** dialog:</span><span class="sxs-lookup"><span data-stu-id="12cf2-199">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="12cf2-200">In the **Model class** dropdown, select your new DTO.</span><span class="sxs-lookup"><span data-stu-id="12cf2-200">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="12cf2-201">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span><span class="sxs-lookup"><span data-stu-id="12cf2-201">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="12cf2-202">The Controller name is created for you.</span><span class="sxs-lookup"><span data-stu-id="12cf2-202">The Controller name is created for you.</span></span>
4. <span data-ttu-id="12cf2-203">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-203">Click **Add**.</span></span>

<span data-ttu-id="12cf2-204">The quickstart server project contains an example for a simple **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-204">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <a name="how-to-adjust-the-table-paging-size"></a><span data-ttu-id="12cf2-205">How to: Adjust the table paging size</span><span class="sxs-lookup"><span data-stu-id="12cf2-205">How to: Adjust the table paging size</span></span>
<span data-ttu-id="12cf2-206">By default, Azure Mobile Apps returns 50 records per request.</span><span class="sxs-lookup"><span data-stu-id="12cf2-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="12cf2-207">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span><span class="sxs-lookup"><span data-stu-id="12cf2-207">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="12cf2-208">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span><span class="sxs-lookup"><span data-stu-id="12cf2-208">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="12cf2-209">Ensure the PageSize is the same or larger than the size requested by the client.</span><span class="sxs-lookup"><span data-stu-id="12cf2-209">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="12cf2-210">Refer to the specific client HOWTO documentation for details on changing the client page size.</span><span class="sxs-lookup"><span data-stu-id="12cf2-210">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="12cf2-211">How to: Define a custom API controller</span><span class="sxs-lookup"><span data-stu-id="12cf2-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="12cf2-212">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span><span class="sxs-lookup"><span data-stu-id="12cf2-212">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="12cf2-213">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span><span class="sxs-lookup"><span data-stu-id="12cf2-213">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="12cf2-214">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="12cf2-214">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="12cf2-215">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-215">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="12cf2-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="12cf2-217">In the new controller class file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="12cf2-217">In the new controller class file, add the following using statement:</span></span>
   
        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="12cf2-218">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="12cf2-218">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>
   
        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="12cf2-219">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="12cf2-219">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>
   
        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="12cf2-220">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="12cf2-220">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="12cf2-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span><span class="sxs-lookup"><span data-stu-id="12cf2-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="12cf2-222">How to: Work with authentication</span><span class="sxs-lookup"><span data-stu-id="12cf2-222">How to: Work with authentication</span></span>
<span data-ttu-id="12cf2-223">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span><span class="sxs-lookup"><span data-stu-id="12cf2-223">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="12cf2-224">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span><span class="sxs-lookup"><span data-stu-id="12cf2-224">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="12cf2-225">How to: Add authentication to a server project</span><span class="sxs-lookup"><span data-stu-id="12cf2-225">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="12cf2-226">How to: Use custom authentication for your application</span><span class="sxs-lookup"><span data-stu-id="12cf2-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="12cf2-227">How to: Retrieve authenticated user information</span><span class="sxs-lookup"><span data-stu-id="12cf2-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="12cf2-228">How to: Restrict data access for authorized users</span><span class="sxs-lookup"><span data-stu-id="12cf2-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <a name="add-auth"></a><span data-ttu-id="12cf2-229">How to: Add authentication to a server project</span><span class="sxs-lookup"><span data-stu-id="12cf2-229">How to: Add authentication to a server project</span></span>
<span data-ttu-id="12cf2-230">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span><span class="sxs-lookup"><span data-stu-id="12cf2-230">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="12cf2-231">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span><span class="sxs-lookup"><span data-stu-id="12cf2-231">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="12cf2-232">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span><span class="sxs-lookup"><span data-stu-id="12cf2-232">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="12cf2-233">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span><span class="sxs-lookup"><span data-stu-id="12cf2-233">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>
   
        app.UseAppServiceAuthentication(config);
   
    <span data-ttu-id="12cf2-234">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span><span class="sxs-lookup"><span data-stu-id="12cf2-234">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="12cf2-235">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span><span class="sxs-lookup"><span data-stu-id="12cf2-235">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span> 

<span data-ttu-id="12cf2-236">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="12cf2-236">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <a name="custom-auth"></a><span data-ttu-id="12cf2-237">How to: Use custom authentication for your application</span><span class="sxs-lookup"><span data-stu-id="12cf2-237">How to: Use custom authentication for your application</span></span>
<span data-ttu-id="12cf2-238">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span><span class="sxs-lookup"><span data-stu-id="12cf2-238">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="12cf2-239">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span><span class="sxs-lookup"><span data-stu-id="12cf2-239">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="12cf2-240">Provide your own code for validating user credentials.</span><span class="sxs-lookup"><span data-stu-id="12cf2-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="12cf2-241">For example, you might check against salted and hashed passwords in a database.</span><span class="sxs-lookup"><span data-stu-id="12cf2-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="12cf2-242">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span><span class="sxs-lookup"><span data-stu-id="12cf2-242">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="12cf2-243">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span><span class="sxs-lookup"><span data-stu-id="12cf2-243">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="12cf2-244">The client should use a custom UI to collect the information from the user.</span><span class="sxs-lookup"><span data-stu-id="12cf2-244">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="12cf2-245">The information is then submitted to the API with a standard HTTP POST call.</span><span class="sxs-lookup"><span data-stu-id="12cf2-245">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="12cf2-246">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-246">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="12cf2-247">The ApiController **should not** use the `[MobileAppController]` attribute.</span><span class="sxs-lookup"><span data-stu-id="12cf2-247">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span> 

<span data-ttu-id="12cf2-248">An example `login` action:</span><span class="sxs-lookup"><span data-stu-id="12cf2-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="12cf2-249">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span><span class="sxs-lookup"><span data-stu-id="12cf2-249">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="12cf2-250">The client expects login responses to be returned as JSON objects of the form:</span><span class="sxs-lookup"><span data-stu-id="12cf2-250">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="12cf2-251">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span><span class="sxs-lookup"><span data-stu-id="12cf2-251">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="12cf2-252">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="12cf2-252">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="12cf2-253">Similarly you should set *secretKey* to be the value of your application's signing key.</span><span class="sxs-lookup"><span data-stu-id="12cf2-253">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="12cf2-254">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span><span class="sxs-lookup"><span data-stu-id="12cf2-254">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="12cf2-255">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span><span class="sxs-lookup"><span data-stu-id="12cf2-255">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="12cf2-256">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span><span class="sxs-lookup"><span data-stu-id="12cf2-256">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="12cf2-257">The issued token may also include other claims and an expiry date.</span><span class="sxs-lookup"><span data-stu-id="12cf2-257">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="12cf2-258">Minimally, the issued token must include a subject (**sub**) claim.</span><span class="sxs-lookup"><span data-stu-id="12cf2-258">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="12cf2-259">You can support the standard client `loginAsync()` method by overloading the authentication route.</span><span class="sxs-lookup"><span data-stu-id="12cf2-259">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="12cf2-260">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="12cf2-260">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="12cf2-261">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="12cf2-261">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="12cf2-262">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span><span class="sxs-lookup"><span data-stu-id="12cf2-262">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
> 
> 

### <a name="user-info"></a><span data-ttu-id="12cf2-263">How to: Retrieve authenticated user information</span><span class="sxs-lookup"><span data-stu-id="12cf2-263">How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="12cf2-264">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span><span class="sxs-lookup"><span data-stu-id="12cf2-264">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="12cf2-265">The user information can be used for making authorization decisions in the backend.</span><span class="sxs-lookup"><span data-stu-id="12cf2-265">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="12cf2-266">The following code obtains the user ID associated with a request:</span><span class="sxs-lookup"><span data-stu-id="12cf2-266">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="12cf2-267">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span><span class="sxs-lookup"><span data-stu-id="12cf2-267">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="12cf2-268">The SID is null for invalid authentication tokens.</span><span class="sxs-lookup"><span data-stu-id="12cf2-268">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="12cf2-269">App Service also lets you request specific claims from your login provider.</span><span class="sxs-lookup"><span data-stu-id="12cf2-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="12cf2-270">Each identity provider can provide more information using the identity provider SDK.</span><span class="sxs-lookup"><span data-stu-id="12cf2-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="12cf2-271">For example, you can use the Facebook Graph API for friends information.</span><span class="sxs-lookup"><span data-stu-id="12cf2-271">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="12cf2-272">You can specify claims that are requested in the provider blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="12cf2-272">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="12cf2-273">Some claims require additional configuration with the identity provider.</span><span class="sxs-lookup"><span data-stu-id="12cf2-273">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="12cf2-274">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span><span class="sxs-lookup"><span data-stu-id="12cf2-274">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="12cf2-275">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span><span class="sxs-lookup"><span data-stu-id="12cf2-275">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <a name="authorize"></a><span data-ttu-id="12cf2-276">How to: Restrict data access for authorized users</span><span class="sxs-lookup"><span data-stu-id="12cf2-276">How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="12cf2-277">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="12cf2-277">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="12cf2-278">You can restrict access to data and other resources based on this value.</span><span class="sxs-lookup"><span data-stu-id="12cf2-278">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="12cf2-279">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span><span class="sxs-lookup"><span data-stu-id="12cf2-279">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="12cf2-280">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span><span class="sxs-lookup"><span data-stu-id="12cf2-280">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="12cf2-281">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span><span class="sxs-lookup"><span data-stu-id="12cf2-281">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="12cf2-282">How to: Add push notifications to a server project</span><span class="sxs-lookup"><span data-stu-id="12cf2-282">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="12cf2-283">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span><span class="sxs-lookup"><span data-stu-id="12cf2-283">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="12cf2-284">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-284">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span> 
2. <span data-ttu-id="12cf2-285">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span><span class="sxs-lookup"><span data-stu-id="12cf2-285">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="12cf2-286">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span><span class="sxs-lookup"><span data-stu-id="12cf2-286">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>
   
        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="12cf2-287">Add the following code that creates a Notification Hubs client:</span><span class="sxs-lookup"><span data-stu-id="12cf2-287">Add the following code that creates a Notification Hubs client:</span></span>
   
        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();
   
        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;
   
        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="12cf2-288">You can now use the Notification Hubs client to send push notifications to registered devices.</span><span class="sxs-lookup"><span data-stu-id="12cf2-288">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="12cf2-289">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="12cf2-289">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="12cf2-290">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12cf2-290">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <a name="tags"></a><span data-ttu-id="12cf2-291">How to: Enable targeted push using Tags</span><span class="sxs-lookup"><span data-stu-id="12cf2-291">How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="12cf2-292">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span><span class="sxs-lookup"><span data-stu-id="12cf2-292">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="12cf2-293">Several tags are created automatically:</span><span class="sxs-lookup"><span data-stu-id="12cf2-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="12cf2-294">The Installation ID identifies a specific device.</span><span class="sxs-lookup"><span data-stu-id="12cf2-294">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="12cf2-295">The User Id based on the authenticated SID identifies a specific user.</span><span class="sxs-lookup"><span data-stu-id="12cf2-295">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="12cf2-296">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-296">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="12cf2-297">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span><span class="sxs-lookup"><span data-stu-id="12cf2-297">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="12cf2-298">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span><span class="sxs-lookup"><span data-stu-id="12cf2-298">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="12cf2-299">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span><span class="sxs-lookup"><span data-stu-id="12cf2-299">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span> 

<span data-ttu-id="12cf2-300">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span><span class="sxs-lookup"><span data-stu-id="12cf2-300">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <a name="push-user"></a><span data-ttu-id="12cf2-301">How to: Send push notifications to an authenticated user</span><span class="sxs-lookup"><span data-stu-id="12cf2-301">How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="12cf2-302">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span><span class="sxs-lookup"><span data-stu-id="12cf2-302">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="12cf2-303">By using this tag, you can send push notifications to all devices registered by that person.</span><span class="sxs-lookup"><span data-stu-id="12cf2-303">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="12cf2-304">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span><span class="sxs-lookup"><span data-stu-id="12cf2-304">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="12cf2-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span><span class="sxs-lookup"><span data-stu-id="12cf2-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="12cf2-306">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span><span class="sxs-lookup"><span data-stu-id="12cf2-306">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="12cf2-307">How to: Debug and troubleshoot the .NET Server SDK</span><span class="sxs-lookup"><span data-stu-id="12cf2-307">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="12cf2-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span><span class="sxs-lookup"><span data-stu-id="12cf2-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="12cf2-309">Monitoring an Azure App Service</span><span class="sxs-lookup"><span data-stu-id="12cf2-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="12cf2-310">Enable Diagnostic Logging in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="12cf2-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="12cf2-311">Troubleshoot an Azure App Service in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12cf2-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="12cf2-312">Logging</span><span class="sxs-lookup"><span data-stu-id="12cf2-312">Logging</span></span>
<span data-ttu-id="12cf2-313">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span><span class="sxs-lookup"><span data-stu-id="12cf2-313">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="12cf2-314">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="12cf2-314">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="12cf2-315">To enable diagnostics and write to the logs:</span><span class="sxs-lookup"><span data-stu-id="12cf2-315">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="12cf2-316">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="12cf2-316">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="12cf2-317">Add the following using statement in your code file:</span><span class="sxs-lookup"><span data-stu-id="12cf2-317">Add the following using statement in your code file:</span></span>
   
        using System.Web.Http.Tracing;
3. <span data-ttu-id="12cf2-318">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span><span class="sxs-lookup"><span data-stu-id="12cf2-318">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>
   
        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="12cf2-319">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span><span class="sxs-lookup"><span data-stu-id="12cf2-319">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="12cf2-320">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="12cf2-320">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <a name="local-debug"></a><span data-ttu-id="12cf2-321">Local debugging with authentication</span><span class="sxs-lookup"><span data-stu-id="12cf2-321">Local debugging with authentication</span></span>
<span data-ttu-id="12cf2-322">You can run your application locally to test changes before publishing them to the cloud.</span><span class="sxs-lookup"><span data-stu-id="12cf2-322">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="12cf2-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12cf2-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="12cf2-324">However, there are some additional considerations when using authentication.</span><span class="sxs-lookup"><span data-stu-id="12cf2-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="12cf2-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span><span class="sxs-lookup"><span data-stu-id="12cf2-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="12cf2-326">See the documentation for your client platform for the specific steps required.</span><span class="sxs-lookup"><span data-stu-id="12cf2-326">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="12cf2-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span><span class="sxs-lookup"><span data-stu-id="12cf2-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="12cf2-328">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="12cf2-328">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="12cf2-329">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="12cf2-329">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="12cf2-330">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span><span class="sxs-lookup"><span data-stu-id="12cf2-330">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="12cf2-331">To obtain the signing key:</span><span class="sxs-lookup"><span data-stu-id="12cf2-331">To obtain the signing key:</span></span>

1. <span data-ttu-id="12cf2-332">Navigate to your app within the [Azure portal]</span><span class="sxs-lookup"><span data-stu-id="12cf2-332">Navigate to your app within the [Azure portal]</span></span> 
2. <span data-ttu-id="12cf2-333">Click **Tools**, **Kudu**, **Go**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="12cf2-334">In the Kudu Management site, click **Environment**.</span><span class="sxs-lookup"><span data-stu-id="12cf2-334">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="12cf2-335">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="12cf2-335">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span> 

<span data-ttu-id="12cf2-336">Use the signing key for the *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span><span class="sxs-lookup"><span data-stu-id="12cf2-336">Use the signing key for the *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure portal]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx





