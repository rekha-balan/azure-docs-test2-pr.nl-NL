---
title: Use Azure CDN in Azure App Service
description: A tutorial that teaches you how to deploy a web app to Azure App Service that serves content from an integrated Azure CDN endpoint
services: app-service\web,cdn
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: b81ee930-dd6d-4b65-971f-c4cb7902168c
ms.service: app-service
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 235fb37082e3add2a544b29f78ece5d2c92545b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669303"
---
# <a name="use-azure-cdn-in-azure-app-service"></a><span data-ttu-id="35832-103">Use Azure CDN in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="35832-103">Use Azure CDN in Azure App Service</span></span>
<span data-ttu-id="35832-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) can be integrated with [Azure CDN](/services/cdn/), adding to the global scaling capabilities inherent in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by serving your web app content globally from server nodes near your customers (an updated list of all current node locations can be found [here](http://msdn.microsoft.com/library/azure/gg680302.aspx)).</span><span class="sxs-lookup"><span data-stu-id="35832-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) can be integrated with [Azure CDN](/services/cdn/), adding to the global scaling capabilities inherent in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by serving your web app content globally from server nodes near your customers (an updated list of all current node locations can be found [here](http://msdn.microsoft.com/library/azure/gg680302.aspx)).</span></span> <span data-ttu-id="35832-105">In scenarios like serving static images, this integration can dramatically increase the performance of your Azure App Service Web Apps and significantly improves your web app's user experience worldwide.</span><span class="sxs-lookup"><span data-stu-id="35832-105">In scenarios like serving static images, this integration can dramatically increase the performance of your Azure App Service Web Apps and significantly improves your web app's user experience worldwide.</span></span> 

<span data-ttu-id="35832-106">Integrating Web Apps with Azure CDN gives you the following advantages:</span><span class="sxs-lookup"><span data-stu-id="35832-106">Integrating Web Apps with Azure CDN gives you the following advantages:</span></span>

* <span data-ttu-id="35832-107">Integrate content deployment (images, scripts, and stylesheets) as part of your web app's [continuous deployment](app-service-continuous-deployment.md) process</span><span class="sxs-lookup"><span data-stu-id="35832-107">Integrate content deployment (images, scripts, and stylesheets) as part of your web app's [continuous deployment](app-service-continuous-deployment.md) process</span></span>
* <span data-ttu-id="35832-108">Easily upgrade the NuGet packages in your web app in Azure App Service, such as jQuery or Bootstrap versions</span><span class="sxs-lookup"><span data-stu-id="35832-108">Easily upgrade the NuGet packages in your web app in Azure App Service, such as jQuery or Bootstrap versions</span></span> 
* <span data-ttu-id="35832-109">Manage your Web application and your CDN-served content from the same Visual Studio interface</span><span class="sxs-lookup"><span data-stu-id="35832-109">Manage your Web application and your CDN-served content from the same Visual Studio interface</span></span>
* <span data-ttu-id="35832-110">Integrate ASP.NET bundling and minification with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="35832-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-build"></a><span data-ttu-id="35832-111">What you will build</span><span class="sxs-lookup"><span data-stu-id="35832-111">What you will build</span></span>
<span data-ttu-id="35832-112">You will deploy a web app to Azure App Service using the default ASP.NET MVC template in Visual Studio, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span><span class="sxs-lookup"><span data-stu-id="35832-112">You will deploy a web app to Azure App Service using the default ASP.NET MVC template in Visual Studio, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="35832-113">What you will need</span><span class="sxs-lookup"><span data-stu-id="35832-113">What you will need</span></span>
<span data-ttu-id="35832-114">This tutorial has the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="35832-114">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="35832-115">An active [Microsoft Azure account](/account/)</span><span class="sxs-lookup"><span data-stu-id="35832-115">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="35832-116">Visual Studio 2015 with the [Azure SDK for .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="35832-116">Visual Studio 2015 with the [Azure SDK for .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409).</span></span> <span data-ttu-id="35832-117">If you use Visual Studio, the steps may vary.</span><span class="sxs-lookup"><span data-stu-id="35832-117">If you use Visual Studio, the steps may vary.</span></span>

> [!NOTE]
> <span data-ttu-id="35832-118">You need an Azure account to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="35832-118">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="35832-119">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span><span class="sxs-lookup"><span data-stu-id="35832-119">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="35832-120">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="35832-120">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> <span data-ttu-id="35832-121">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="35832-121">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="35832-122">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="35832-122">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint"></a><span data-ttu-id="35832-123">Deploy a web app to Azure with an integrated CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="35832-123">Deploy a web app to Azure with an integrated CDN endpoint</span></span>
<span data-ttu-id="35832-124">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to App Service, and then integrate it with a new CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="35832-124">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to App Service, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="35832-125">Follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="35832-125">Follow the instructions below:</span></span>

1. <span data-ttu-id="35832-126">In Visual Studio 2015, create a new ASP.NET web application from the menu bar by going to **File > New > Project > Web > ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="35832-126">In Visual Studio 2015, create a new ASP.NET web application from the menu bar by going to **File > New > Project > Web > ASP.NET Web Application**.</span></span> <span data-ttu-id="35832-127">Give it a name and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35832-127">Give it a name and click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/1-new-project.png)
2. <span data-ttu-id="35832-128">Select **MVC** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35832-128">Select **MVC** and click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/2-webapp-template.png)
3. <span data-ttu-id="35832-129">If you haven't logged into your Azure account yet, click the account icon in the upper-right corner and follow the dialog to log into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="35832-129">If you haven't logged into your Azure account yet, click the account icon in the upper-right corner and follow the dialog to log into your Azure account.</span></span> <span data-ttu-id="35832-130">Once you're done, configure your app as shown below, then click **New** to create a new App Service plan for your app.</span><span class="sxs-lookup"><span data-stu-id="35832-130">Once you're done, configure your app as shown below, then click **New** to create a new App Service plan for your app.</span></span>  
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/3-configure-webapp.png)
4. <span data-ttu-id="35832-131">Configure a new App Service plan in the dialog as shown below and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35832-131">Configure a new App Service plan in the dialog as shown below and click **OK**.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/4-app-service-plan.png)
5. <span data-ttu-id="35832-132">Click **Create** to create the web app.</span><span class="sxs-lookup"><span data-stu-id="35832-132">Click **Create** to create the web app.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/5-create-website.png)
6. <span data-ttu-id="35832-133">Once your ASP.NET application is created, publish it to Azure in the Azure App Service Activity pane by clicking **Publish `<app name>` to this Web App now**.</span><span class="sxs-lookup"><span data-stu-id="35832-133">Once your ASP.NET application is created, publish it to Azure in the Azure App Service Activity pane by clicking **Publish `<app name>` to this Web App now**.</span></span> <span data-ttu-id="35832-134">Click **Publish** to complete the process.</span><span class="sxs-lookup"><span data-stu-id="35832-134">Click **Publish** to complete the process.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/6-publish-website.png)
   
    <span data-ttu-id="35832-135">You will see your published web app in the browser when publishing is complete.</span><span class="sxs-lookup"><span data-stu-id="35832-135">You will see your published web app in the browser when publishing is complete.</span></span> 
7. <span data-ttu-id="35832-136">To create a CDN endpoint, log into the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="35832-136">To create a CDN endpoint, log into the [Azure portal](https://portal.azure.com).</span></span> 
8. <span data-ttu-id="35832-137">Click **+ New** > **Media + CDN** > **CDN**.</span><span class="sxs-lookup"><span data-stu-id="35832-137">Click **+ New** > **Media + CDN** > **CDN**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/create-cdn-profile.png)
9. <span data-ttu-id="35832-138">Specify the **CDN**, **Location**, **Resource group**,  **Pricing tier**, then click **Create**</span><span class="sxs-lookup"><span data-stu-id="35832-138">Specify the **CDN**, **Location**, **Resource group**,  **Pricing tier**, then click **Create**</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/7-create-cdn.png)    
10. <span data-ttu-id="35832-139">In the **CDN Profile** blade click on **+ Endpoint** button.</span><span class="sxs-lookup"><span data-stu-id="35832-139">In the **CDN Profile** blade click on **+ Endpoint** button.</span></span> <span data-ttu-id="35832-140">Give it a name, select **Web App** in the **Origin Type** dropdown and your web app in the **Origin hostname** dropdown, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="35832-140">Give it a name, select **Web App** in the **Origin Type** dropdown and your web app in the **Origin hostname** dropdown, then click **Add**.</span></span>  
    
     ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/cdn-profile-blade.png)

    > [AZURE.NOTE] <span data-ttu-id="35832-141">Once your CDN endpoint is created, the **Endpoint** blade will show you its CDN URL and the origin domain that it's integrated with.</span><span class="sxs-lookup"><span data-stu-id="35832-141">Once your CDN endpoint is created, the **Endpoint** blade will show you its CDN URL and the origin domain that it's integrated with.</span></span> <span data-ttu-id="35832-142">However, it can take a while for the new CDN endpoint's configuration to be fully propagated to all the CDN node locations.</span><span class="sxs-lookup"><span data-stu-id="35832-142">However, it can take a while for the new CDN endpoint's configuration to be fully propagated to all the CDN node locations.</span></span> 

1. <span data-ttu-id="35832-143">Back in the **Endpoint** blade, click the name of the CDN endpoint you just created.</span><span class="sxs-lookup"><span data-stu-id="35832-143">Back in the **Endpoint** blade, click the name of the CDN endpoint you just created.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/8-select-cdn.png)
2. <span data-ttu-id="35832-144">Click the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="35832-144">Click the **Configure** button.</span></span> <span data-ttu-id="35832-145">In the **Configure** blade, select **Cache every unique URL** in **Query string caching behavior** dropdown, then click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="35832-145">In the **Configure** blade, select **Cache every unique URL** in **Query string caching behavior** dropdown, then click the **Save** button.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/9-enable-query-string.png)

<span data-ttu-id="35832-146">Once you enable this, the same link accessed with different query strings will be cached as separate entries.</span><span class="sxs-lookup"><span data-stu-id="35832-146">Once you enable this, the same link accessed with different query strings will be cached as separate entries.</span></span>

> [!NOTE]
> <span data-ttu-id="35832-147">While enabling the query string is not necessary for this tutorial section, you want to do this as early as possible for convenience since any change here is going to take time to propagate to all the CDN nodes, and you don't want any non-query-string-enabled content to clog up the CDN cache (updating CDN content will be discussed later).</span><span class="sxs-lookup"><span data-stu-id="35832-147">While enabling the query string is not necessary for this tutorial section, you want to do this as early as possible for convenience since any change here is going to take time to propagate to all the CDN nodes, and you don't want any non-query-string-enabled content to clog up the CDN cache (updating CDN content will be discussed later).</span></span>
> 
> 

1. <span data-ttu-id="35832-148">Now, navigate to the CDN endpoint address.</span><span class="sxs-lookup"><span data-stu-id="35832-148">Now, navigate to the CDN endpoint address.</span></span> <span data-ttu-id="35832-149">If the endpoint is ready, you should see your web app displayed.</span><span class="sxs-lookup"><span data-stu-id="35832-149">If the endpoint is ready, you should see your web app displayed.</span></span> <span data-ttu-id="35832-150">If you get an **HTTP 404** error, the CDN endpoint is not ready.</span><span class="sxs-lookup"><span data-stu-id="35832-150">If you get an **HTTP 404** error, the CDN endpoint is not ready.</span></span> <span data-ttu-id="35832-151">You may need to wait up to an hour for the CDN configuration to be propagated to all the edge nodes.</span><span class="sxs-lookup"><span data-stu-id="35832-151">You may need to wait up to an hour for the CDN configuration to be propagated to all the edge nodes.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/11-access-success.png)
2. <span data-ttu-id="35832-152">Next, try to access the **~/Content/bootstrap.css** file in your ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="35832-152">Next, try to access the **~/Content/bootstrap.css** file in your ASP.NET project.</span></span> <span data-ttu-id="35832-153">In the browser window, navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="35832-153">In the browser window, navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="35832-154">In my setup, this URL is:</span><span class="sxs-lookup"><span data-stu-id="35832-154">In my setup, this URL is:</span></span>
   
        http://az673227.azureedge.net/Content/bootstrap.css
   
    <span data-ttu-id="35832-155">Which corresponds to the following origin URL at the CDN endpoint:</span><span class="sxs-lookup"><span data-stu-id="35832-155">Which corresponds to the following origin URL at the CDN endpoint:</span></span>
   
        http://cdnwebapp.azurewebsites.net/Content/bootstrap.css
   
    <span data-ttu-id="35832-156">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, you will be prompted to download the bootstrap.css that came from your web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="35832-156">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, you will be prompted to download the bootstrap.css that came from your web app in Azure.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/12-file-access.png)

<span data-ttu-id="35832-157">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="35832-157">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="35832-158">For example:</span><span class="sxs-lookup"><span data-stu-id="35832-158">For example:</span></span>

* <span data-ttu-id="35832-159">A .js file from the /Script path</span><span class="sxs-lookup"><span data-stu-id="35832-159">A .js file from the /Script path</span></span>
* <span data-ttu-id="35832-160">Any content file from the /Content path</span><span class="sxs-lookup"><span data-stu-id="35832-160">Any content file from the /Content path</span></span>
* <span data-ttu-id="35832-161">Any controller/action</span><span class="sxs-lookup"><span data-stu-id="35832-161">Any controller/action</span></span> 
* <span data-ttu-id="35832-162">If the query string is enabled at your CDN endpoint, any URL with query strings</span><span class="sxs-lookup"><span data-stu-id="35832-162">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>
* <span data-ttu-id="35832-163">The entire Azure web app, if all content is public</span><span class="sxs-lookup"><span data-stu-id="35832-163">The entire Azure web app, if all content is public</span></span>

<span data-ttu-id="35832-164">Note that it may not be always a good idea (or generally a good idea) to serve an entire Azure web app through Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-164">Note that it may not be always a good idea (or generally a good idea) to serve an entire Azure web app through Azure CDN.</span></span> <span data-ttu-id="35832-165">Some of the caveats are:</span><span class="sxs-lookup"><span data-stu-id="35832-165">Some of the caveats are:</span></span>

* <span data-ttu-id="35832-166">This approach requires your entire site to be public, because Azure CDN cannot serve any private content.</span><span class="sxs-lookup"><span data-stu-id="35832-166">This approach requires your entire site to be public, because Azure CDN cannot serve any private content.</span></span>
* <span data-ttu-id="35832-167">If the CDN endpoint goes offline for any reason, whether scheduled maintenance or user error, your entire web app goes offline unless the customers can be redirected to the origin URL **http://*&lt;sitename>*.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="35832-167">If the CDN endpoint goes offline for any reason, whether scheduled maintenance or user error, your entire web app goes offline unless the customers can be redirected to the origin URL **http://*&lt;sitename>*.azurewebsites.net/**.</span></span> 
* <span data-ttu-id="35832-168">Even with the custom Cache-Control settings (see [Configure caching options for static files in your Azure web app](#configure-caching-options-for-static-files-in-your-azure-web-app)), a CDN endpoint does not improve the performance of highly-dynamic content.</span><span class="sxs-lookup"><span data-stu-id="35832-168">Even with the custom Cache-Control settings (see [Configure caching options for static files in your Azure web app](#configure-caching-options-for-static-files-in-your-azure-web-app)), a CDN endpoint does not improve the performance of highly-dynamic content.</span></span> <span data-ttu-id="35832-169">If you tried to load the home page from your CDN endpoint as shown above, notice that it took at least 5 seconds to load the default home page the first time, which is a fairly simple page.</span><span class="sxs-lookup"><span data-stu-id="35832-169">If you tried to load the home page from your CDN endpoint as shown above, notice that it took at least 5 seconds to load the default home page the first time, which is a fairly simple page.</span></span> <span data-ttu-id="35832-170">Imagine what would happen to the client experience if this page contains dynamic content that must update every minute.</span><span class="sxs-lookup"><span data-stu-id="35832-170">Imagine what would happen to the client experience if this page contains dynamic content that must update every minute.</span></span> <span data-ttu-id="35832-171">Serving dynamic content from a CDN endpoint requires short cache expiration, which translates to frequent cache misses at the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="35832-171">Serving dynamic content from a CDN endpoint requires short cache expiration, which translates to frequent cache misses at the CDN endpoint.</span></span> <span data-ttu-id="35832-172">This hurts the performance of your Azure web app and defeats the purpose of a CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-172">This hurts the performance of your Azure web app and defeats the purpose of a CDN.</span></span>

<span data-ttu-id="35832-173">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="35832-173">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your Azure web app.</span></span> <span data-ttu-id="35832-174">To that end, you have already seen how to access individual content files from the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="35832-174">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="35832-175">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#serve-content-from-controller-actions-through-azure-cdn).</span><span class="sxs-lookup"><span data-stu-id="35832-175">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#serve-content-from-controller-actions-through-azure-cdn).</span></span>

## <a name="configure-caching-options-for-static-files-in-your-azure-web-app"></a><span data-ttu-id="35832-176">Configure caching options for static files in your Azure web app</span><span class="sxs-lookup"><span data-stu-id="35832-176">Configure caching options for static files in your Azure web app</span></span>
<span data-ttu-id="35832-177">With Azure CDN integration in your Azure web app, you can specify how you want static content to be cached in the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="35832-177">With Azure CDN integration in your Azure web app, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="35832-178">To do this, open *Web.config* from your ASP.NET project (e.g. **cdnwebapp**) and add a `<staticContent>` element to `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="35832-178">To do this, open *Web.config* from your ASP.NET project (e.g. **cdnwebapp**) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="35832-179">The XML below configures the cache to expire in 3 days.</span><span class="sxs-lookup"><span data-stu-id="35832-179">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="35832-180">Once you do this, all static files in your Azure web app will observe the same rule in your CDN cache.</span><span class="sxs-lookup"><span data-stu-id="35832-180">Once you do this, all static files in your Azure web app will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="35832-181">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span><span class="sxs-lookup"><span data-stu-id="35832-181">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="35832-182">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span><span class="sxs-lookup"><span data-stu-id="35832-182">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="35832-183">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span><span class="sxs-lookup"><span data-stu-id="35832-183">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="35832-184">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="35832-184">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="35832-185">In the next section, I will also show you how you can configure cache settings for controller action results in the CDN cache.</span><span class="sxs-lookup"><span data-stu-id="35832-185">In the next section, I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="35832-186">Serve content from controller actions through Azure CDN</span><span class="sxs-lookup"><span data-stu-id="35832-186">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="35832-187">When you integrate Web Apps with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-187">When you integrate Web Apps with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="35832-188">Again, if you decide to serve the entire Azure web app through your CDN, you don't need to do this at all since all the controller actions are reachable through the CDN already.</span><span class="sxs-lookup"><span data-stu-id="35832-188">Again, if you decide to serve the entire Azure web app through your CDN, you don't need to do this at all since all the controller actions are reachable through the CDN already.</span></span> <span data-ttu-id="35832-189">But for the reasons I already pointed out in [Deploy an Azure web app with an integrated CDN endpoint](#deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint), you may decide against this and choose instead to select the controller action you want to serve from Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-189">But for the reasons I already pointed out in [Deploy an Azure web app with an integrated CDN endpoint](#deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint), you may decide against this and choose instead to select the controller action you want to serve from Azure CDN.</span></span> <span data-ttu-id="35832-190">[Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="35832-190">[Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="35832-191">I will simply reproduce it here.</span><span class="sxs-lookup"><span data-stu-id="35832-191">I will simply reproduce it here.</span></span>

<span data-ttu-id="35832-192">Suppose in your web app you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span><span class="sxs-lookup"><span data-stu-id="35832-192">Suppose in your web app you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="35832-193">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span><span class="sxs-lookup"><span data-stu-id="35832-193">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="35832-194">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span><span class="sxs-lookup"><span data-stu-id="35832-194">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="35832-195">This is a good example of serving semi-dynamic content with Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-195">This is a good example of serving semi-dynamic content with Azure CDN.</span></span> 

<span data-ttu-id="35832-196">Follow the steps above to setup this controller action:</span><span class="sxs-lookup"><span data-stu-id="35832-196">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="35832-197">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span><span class="sxs-lookup"><span data-stu-id="35832-197">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="35832-198">Substitute your file path for `~/Content/chuck.bmp` and your CDN name for `yourCDNName`.</span><span class="sxs-lookup"><span data-stu-id="35832-198">Substitute your file path for `~/Content/chuck.bmp` and your CDN name for `yourCDNName`.</span></span>

        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;

        namespace cdnwebapp.Controllers
        {
          public class MemeGeneratorController : Controller
          {
            static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();

            public ActionResult Index()
            {
              return View();
            }

            [HttpPost, ActionName("Index")]
            public ActionResult Index_Post(string top, string bottom)
            {
              var identifier = Guid.NewGuid().ToString();
              if (!Memes.ContainsKey(identifier))
              {
                Memes.Add(identifier, new Tuple<string, string>(top, bottom));
              }

              return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
            }

            [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
            public ActionResult Show(string id)
            {
              Tuple<string, string> data = null;
              if (!Memes.TryGetValue(id, out data))
              {
                return new HttpStatusCodeResult(HttpStatusCode.NotFound);
              }

              if (Debugger.IsAttached) // Preserve the debug experience
              {
                return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
              }
              else // Get content from Azure CDN
              {
                return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
              }
            }

            [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
            public ActionResult Generate(string top, string bottom)
            {
              string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
              Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);

              using (Graphics graphics = Graphics.FromImage(bitmap))
              {
                SizeF size = new SizeF();
                using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                {
                    graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                }
                using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                {
                    graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                }
              }
              MemoryStream ms = new MemoryStream();
              bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
              return File(ms.ToArray(), "image/png");
            }

            private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
            {
              // Compute actual size, shrink if needed
              while (true)
              {
                size = g.MeasureString(text, font);

                // It fits, back out
                if (size.Height < i.Height &&
                     size.Width < i.Width) { return font; }

                // Try a smaller font (90% of old size)
                Font oldFont = font;
                font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                oldFont.Dispose();
              }
            }
          }
        }

1. <span data-ttu-id="35832-199">Right-click in the default `Index()` action and select **Add View**.</span><span class="sxs-lookup"><span data-stu-id="35832-199">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/cdn-6-addview.PNG)
2. <span data-ttu-id="35832-200">Accept the settings below and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="35832-200">Accept the settings below and click **Add**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/cdn-7-configureview.PNG)
3. <span data-ttu-id="35832-201">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span><span class="sxs-lookup"><span data-stu-id="35832-201">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
4. <span data-ttu-id="35832-202">Publish to the Azure web app again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span><span class="sxs-lookup"><span data-stu-id="35832-202">Publish to the Azure web app again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span> 

<span data-ttu-id="35832-203">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span><span class="sxs-lookup"><span data-stu-id="35832-203">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="35832-204">When you click the link, you reach the following code:</span><span class="sxs-lookup"><span data-stu-id="35832-204">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
      Tuple<string, string> data = null;
      if (!Memes.TryGetValue(id, out data))
      {
        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
      }

      if (Debugger.IsAttached) // Preserve the debug experience
      {
        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
      }
      else // Get content from Azure CDN
      {
        return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
      }
    }

<span data-ttu-id="35832-205">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span><span class="sxs-lookup"><span data-stu-id="35832-205">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="35832-206">If it's running in the Azure web app, then it will redirect to:</span><span class="sxs-lookup"><span data-stu-id="35832-206">If it's running in the Azure web app, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="35832-207">Which corresponds to the following origin URL at your CDN endpoint:</span><span class="sxs-lookup"><span data-stu-id="35832-207">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<yourSiteName>.azurewebsites.net/cdn/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="35832-208">After URL rewrite rule previously applied, the actual file that gets cached to your CDN endpoint is:</span><span class="sxs-lookup"><span data-stu-id="35832-208">After URL rewrite rule previously applied, the actual file that gets cached to your CDN endpoint is:</span></span>

    http://<yourSiteName>.azurewebsites.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="35832-209">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span><span class="sxs-lookup"><span data-stu-id="35832-209">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="35832-210">The code below specify a cache expiration of 1 hour (3,600 seconds).</span><span class="sxs-lookup"><span data-stu-id="35832-210">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="35832-211">Likewise, you can serve up content from any controller action in your Azure web app through your Azure CDN, with the desired caching option.</span><span class="sxs-lookup"><span data-stu-id="35832-211">Likewise, you can serve up content from any controller action in your Azure web app through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="35832-212">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-212">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span> 

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="35832-213">Integrate ASP.NET bundling and minification with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="35832-213">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="35832-214">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span><span class="sxs-lookup"><span data-stu-id="35832-214">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="35832-215">Serving the entire web app through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-215">Serving the entire web app through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="35832-216">However, as you may elect against this approach for the reasons described in [Integrate an Azure CDN endpoint with your Azure web app and serve static content in your Web pages from Azure CDN](#deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint), I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span><span class="sxs-lookup"><span data-stu-id="35832-216">However, as you may elect against this approach for the reasons described in [Integrate an Azure CDN endpoint with your Azure web app and serve static content in your Web pages from Azure CDN](#deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint), I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="35832-217">Great debug mode experience</span><span class="sxs-lookup"><span data-stu-id="35832-217">Great debug mode experience</span></span>
* <span data-ttu-id="35832-218">Streamlined deployment</span><span class="sxs-lookup"><span data-stu-id="35832-218">Streamlined deployment</span></span>
* <span data-ttu-id="35832-219">Immediate updates to clients for script/CSS version upgrades</span><span class="sxs-lookup"><span data-stu-id="35832-219">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="35832-220">Fallback mechanism when your CDN endpoint fails</span><span class="sxs-lookup"><span data-stu-id="35832-220">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="35832-221">Minimize code modification</span><span class="sxs-lookup"><span data-stu-id="35832-221">Minimize code modification</span></span>

<span data-ttu-id="35832-222">In the ASP.NET project that you created in [Integrate an Azure CDN endpoint with your Azure web app and serve static content in your Web pages from Azure CDN](#deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span><span class="sxs-lookup"><span data-stu-id="35832-222">In the ASP.NET project that you created in [Integrate an Azure CDN endpoint with your Azure web app and serve static content in your Web pages from Azure CDN](#deploy-a-web-app-to-azure-with-an-integrated-cdn-endpoint), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="35832-223">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="35832-223">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="35832-224">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span><span class="sxs-lookup"><span data-stu-id="35832-224">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="35832-225">You should be able to find the following line of Razor code:</span><span class="sxs-lookup"><span data-stu-id="35832-225">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="35832-226">When this Razor code is run in the Azure web app, it will render a `<script>` tag for the script bundle similar to the following:</span><span class="sxs-lookup"><span data-stu-id="35832-226">When this Razor code is run in the Azure web app, it will render a `<script>` tag for the script bundle similar to the following:</span></span> 

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="35832-227">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span><span class="sxs-lookup"><span data-stu-id="35832-227">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="35832-228">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span><span class="sxs-lookup"><span data-stu-id="35832-228">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="35832-229">It's a great feature to preserve with Azure CDN integration.</span><span class="sxs-lookup"><span data-stu-id="35832-229">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="35832-230">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so that whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="35832-230">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so that whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="35832-231">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="35832-231">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="35832-232">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span><span class="sxs-lookup"><span data-stu-id="35832-232">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="35832-233">To do this, replace the `RegisterBundles` method definition with the following code:</span><span class="sxs-lookup"><span data-stu-id="35832-233">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
          bundles.UseCdn = true;
          var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
            .GetName().Version.ToString();
          var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?" + version;
   
          bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                "~/Scripts/jquery-{version}.js"));
   
          bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                "~/Scripts/jquery.validate*"));
   
          // Use the development version of Modernizr to develop with and learn from. Then, when you're
          // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
          bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizr")).Include(
                "~/Scripts/modernizr-*"));
   
          bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                "~/Scripts/bootstrap.js",
                "~/Scripts/respond.js"));
   
          bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                "~/Content/bootstrap.css",
                "~/Content/site.css"));
        }

    <span data-ttu-id="35832-234">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-234">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>

    <span data-ttu-id="35832-235">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span><span class="sxs-lookup"><span data-stu-id="35832-235">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="35832-236">For example, the first constructor in the code:</span><span class="sxs-lookup"><span data-stu-id="35832-236">For example, the first constructor in the code:</span></span>

        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))

    <span data-ttu-id="35832-237">is the same as:</span><span class="sxs-lookup"><span data-stu-id="35832-237">is the same as:</span></span> 

        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?<W.X.Y.Z>"))

    <span data-ttu-id="35832-238">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span><span class="sxs-lookup"><span data-stu-id="35832-238">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="35832-239">However, note two important characteristics with this carefully crafted CDN URL:</span><span class="sxs-lookup"><span data-stu-id="35832-239">However, note two important characteristics with this carefully crafted CDN URL:</span></span>

    - <span data-ttu-id="35832-240">The origin for this CDN URL is `http://<yourSiteName>.azurewebsites.net/bundles/jquery?<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your Web application.</span><span class="sxs-lookup"><span data-stu-id="35832-240">The origin for this CDN URL is `http://<yourSiteName>.azurewebsites.net/bundles/jquery?<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your Web application.</span></span>
    - <span data-ttu-id="35832-241">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span><span class="sxs-lookup"><span data-stu-id="35832-241">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="35832-242">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="35832-242">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="35832-243">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span><span class="sxs-lookup"><span data-stu-id="35832-243">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>

1. <span data-ttu-id="35832-244">The query string `<W.X.Y.Z>` pulls from *Properties\AssemblyInfo.cs* in your ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="35832-244">The query string `<W.X.Y.Z>` pulls from *Properties\AssemblyInfo.cs* in your ASP.NET project.</span></span> <span data-ttu-id="35832-245">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span><span class="sxs-lookup"><span data-stu-id="35832-245">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="35832-246">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '\*'.</span><span class="sxs-lookup"><span data-stu-id="35832-246">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '\*'.</span></span> <span data-ttu-id="35832-247">For example, change `AssemblyVersion` as shown below:</span><span class="sxs-lookup"><span data-stu-id="35832-247">For example, change `AssemblyVersion` as shown below:</span></span>
   
        [assembly: AssemblyVersion("1.0.0.*")]
   
    <span data-ttu-id="35832-248">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span><span class="sxs-lookup"><span data-stu-id="35832-248">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="35832-249">Republish the ASP.NET application and access the home page.</span><span class="sxs-lookup"><span data-stu-id="35832-249">Republish the ASP.NET application and access the home page.</span></span>
3. <span data-ttu-id="35832-250">View the HTML code for the page.</span><span class="sxs-lookup"><span data-stu-id="35832-250">View the HTML code for the page.</span></span> <span data-ttu-id="35832-251">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="35832-251">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your Azure web app.</span></span> <span data-ttu-id="35832-252">For example:</span><span class="sxs-lookup"><span data-stu-id="35832-252">For example:</span></span>  
   
        ...
        <link href="http://az673227.azureedge.net/Content/css?1.0.0.25449" rel="stylesheet"/>
        <script src="http://az673227.azureedge.net/bundles/modernizer?1.0.0.25449"></script>
        ...
        <script src="http://az673227.azureedge.net/bundles/jquery?1.0.0.25449"></script>
        <script src="http://az673227.azureedge.net/bundles/bootstrap?1.0.0.25449"></script>
        ...
4. <span data-ttu-id="35832-253">In Visual Studio, debug the ASP.NET application in Visual Studio by typing `F5`.,</span><span class="sxs-lookup"><span data-stu-id="35832-253">In Visual Studio, debug the ASP.NET application in Visual Studio by typing `F5`.,</span></span> 
5. <span data-ttu-id="35832-254">View the HTML code for the page.</span><span class="sxs-lookup"><span data-stu-id="35832-254">View the HTML code for the page.</span></span> <span data-ttu-id="35832-255">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35832-255">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
        <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
        <script src="/Scripts/modernizr-2.6.2.js"></script>
        ...
        <script src="/Scripts/jquery-1.10.2.js"></script>
        <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
        ...    

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="35832-256">Fallback mechanism for CDN URLs</span><span class="sxs-lookup"><span data-stu-id="35832-256">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="35832-257">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="35832-257">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="35832-258">It's serious enough to lose images on your web app due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span><span class="sxs-lookup"><span data-stu-id="35832-258">It's serious enough to lose images on your web app due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="35832-259">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span><span class="sxs-lookup"><span data-stu-id="35832-259">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="35832-260">To use this property, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="35832-260">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="35832-261">In your ASP.NET project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and add `CdnFallbackExpression` code in four places as shown to add a fallback mechanism to the default bundles.</span><span class="sxs-lookup"><span data-stu-id="35832-261">In your ASP.NET project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and add `CdnFallbackExpression` code in four places as shown to add a fallback mechanism to the default bundles.</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
          var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
            .GetName().Version.ToString();
          var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
          bundles.UseCdn = true;
   
          bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")) 
                { CdnFallbackExpression = "window.jquery" }
                .Include("~/Scripts/jquery-{version}.js"));
   
          bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")) 
                { CdnFallbackExpression = "$.validator" }
                .Include("~/Scripts/jquery.validate*"));
   
          // Use the development version of Modernizr to develop with and learn from. Then, when you're
          // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
          bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")) 
                { CdnFallbackExpression = "window.Modernizr" }
                .Include("~/Scripts/modernizr-*"));
   
          bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                { CdnFallbackExpression = "$.fn.modal" }
                .Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
          bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                "~/Content/bootstrap.css",
                "~/Content/site.css"));
        }
   
    <span data-ttu-id="35832-262">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span><span class="sxs-lookup"><span data-stu-id="35832-262">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="35832-263">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span><span class="sxs-lookup"><span data-stu-id="35832-263">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="35832-264">The expression needed to test each bundle differs according to the content.</span><span class="sxs-lookup"><span data-stu-id="35832-264">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="35832-265">For the default bundles above:</span><span class="sxs-lookup"><span data-stu-id="35832-265">For the default bundles above:</span></span>
   
   * <span data-ttu-id="35832-266">`window.jquery` is defined in jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="35832-266">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="35832-267">`$.validator` is defined in jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="35832-267">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="35832-268">`window.Modernizr` is defined in modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="35832-268">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="35832-269">`$.fn.modal` is defined in bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="35832-269">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="35832-270">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span><span class="sxs-lookup"><span data-stu-id="35832-270">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="35832-271">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span><span class="sxs-lookup"><span data-stu-id="35832-271">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="35832-272">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="35832-272">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span> 
2. <span data-ttu-id="35832-273">To use the workaround for CSS, create a new .cs file in your ASP.NET project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="35832-273">To use the workaround for CSS, create a new .cs file in your ASP.NET project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span> 
3. <span data-ttu-id="35832-274">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your ASP.NET application's namespace (e.g. **cdnwebapp**).</span><span class="sxs-lookup"><span data-stu-id="35832-274">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your ASP.NET application's namespace (e.g. **cdnwebapp**).</span></span> 
4. <span data-ttu-id="35832-275">Go back to `App_Start\BundleConfig.cs` and replace the last `bundles.Add` statement with the following code:</span><span class="sxs-lookup"><span data-stu-id="35832-275">Go back to `App_Start\BundleConfig.cs` and replace the last `bundles.Add` statement with the following code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
          .IncludeFallback("~/Content/css", "sr-only", "width", "1px")
          .Include(
            "~/Content/bootstrap.css",
            "~/Content/site.css"));
   
    <span data-ttu-id="35832-276">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span><span class="sxs-lookup"><span data-stu-id="35832-276">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="35832-277">Publish to your Azure web app again and access the home page.</span><span class="sxs-lookup"><span data-stu-id="35832-277">Publish to your Azure web app again and access the home page.</span></span> 
6. <span data-ttu-id="35832-278">View the HTML code for the page.</span><span class="sxs-lookup"><span data-stu-id="35832-278">View the HTML code for the page.</span></span> <span data-ttu-id="35832-279">You should find injected scripts similar to the following:</span><span class="sxs-lookup"><span data-stu-id="35832-279">You should find injected scripts similar to the following:</span></span>    
   
    ```
    ...
    <link href="http://az673227.azureedge.net/Content/css?1.0.0.25474" rel="stylesheet"/>
   <script>(function() {
                var loadFallback,
                    len = document.styleSheets.length;
                for (var i = 0; i < len; i++) {
                    var sheet = document.styleSheets[i];
                    if (sheet.href.indexOf('http://az673227.azureedge.net/Content/css?1.0.0.25474') !== -1) {
                        var meta = document.createElement('meta');
                        meta.className = 'sr-only';
                        document.head.appendChild(meta);
                        var value = window.getComputedStyle(meta).getPropertyValue('width');
                        document.head.removeChild(meta);
                        if (value !== '1px') {
                            document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                        }
                    }
                }
                return true;
            }())||document.write('<script src="/Content/css"><\/script>');</script>
   
    <script src="http://az673227.azureedge.net/bundles/modernizer?1.0.0.25474"></script>
     <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
    ... 
    <script src="http://az673227.azureedge.net/bundles/jquery?1.0.0.25474"></script>
    <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
     <script src="http://az673227.azureedge.net/bundles/bootstrap?1.0.0.25474"></script>
     <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
    ...
    ```
   
    <span data-ttu-id="35832-280">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span><span class="sxs-lookup"><span data-stu-id="35832-280">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>
   
        }())||document.write('<script src="/Content/css"><\/script>');</script>
   
    <span data-ttu-id="35832-281">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span><span class="sxs-lookup"><span data-stu-id="35832-281">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>
7. <span data-ttu-id="35832-282">To test whether the fallback script is working, go back to the your CDN endpoint's blade and click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="35832-282">To test whether the fallback script is working, go back to the your CDN endpoint's blade and click **Stop**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/cdn-websites-with-cdn/13-test-fallback.png)
8. <span data-ttu-id="35832-283">Refresh your browser window for the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="35832-283">Refresh your browser window for the Azure web app.</span></span> <span data-ttu-id="35832-284">You should now see that the all scripts and stylesheets are properly loaded.</span><span class="sxs-lookup"><span data-stu-id="35832-284">You should now see that the all scripts and stylesheets are properly loaded.</span></span>

## <a name="more-information"></a><span data-ttu-id="35832-285">More Information</span><span class="sxs-lookup"><span data-stu-id="35832-285">More Information</span></span>
* [<span data-ttu-id="35832-286">Overview of the Azure Content Delivery Network (CDN)</span><span class="sxs-lookup"><span data-stu-id="35832-286">Overview of the Azure Content Delivery Network (CDN)</span></span>](../cdn/cdn-overview.md)
* [<span data-ttu-id="35832-287">Using Azure CDN</span><span class="sxs-lookup"><span data-stu-id="35832-287">Using Azure CDN</span></span>](../cdn/cdn-create-new-endpoint.md)
* [<span data-ttu-id="35832-288">Integrate a cloud service with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="35832-288">Integrate a cloud service with Azure CDN</span></span>](../cdn/cdn-cloud-service-with-cdn.md)
* [<span data-ttu-id="35832-289">ASP.NET Bundling and Minification</span><span class="sxs-lookup"><span data-stu-id="35832-289">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)


















