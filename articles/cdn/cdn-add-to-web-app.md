---
title: Tutorial - Add Azure CDN to an Azure App Service web app | Microsoft Docs
description: In this tutorial, Azure Content Delivery Network (CDN) is added to an Azure App Service web app to cache and deliver your static files from servers close to your customers around the world.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 05/14/2018
ms.author: v-deasim
ms.custom: mvc
ms.openlocfilehash: efd8e93f32020d1ef3695e7fc6b9907374275848
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869534"
---
# <a name="tutorial-add-azure-cdn-to-an-azure-app-service-web-app"></a><span data-ttu-id="ff9ee-103">Tutorial: Add Azure CDN to an Azure App Service web app</span><span class="sxs-lookup"><span data-stu-id="ff9ee-103">Tutorial: Add Azure CDN to an Azure App Service web app</span></span>

<span data-ttu-id="ff9ee-104">This tutorial shows how to add [Azure Content Delivery Network (CDN)](cdn-overview.md) to a [web app in Azure App Service](../app-service/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-104">This tutorial shows how to add [Azure Content Delivery Network (CDN)](cdn-overview.md) to a [web app in Azure App Service](../app-service/app-service-web-overview.md).</span></span> <span data-ttu-id="ff9ee-105">Web apps is a service for hosting web applications, REST APIs, and mobile back ends.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-105">Web apps is a service for hosting web applications, REST APIs, and mobile back ends.</span></span> 

<span data-ttu-id="ff9ee-106">Here's the home page of the sample static HTML site that you'll work with:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-106">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Sample app home page](media/cdn-add-to-web-app/sample-app-home-page.png)

<span data-ttu-id="ff9ee-108">What you'll learn:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-108">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff9ee-109">Create a CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-109">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="ff9ee-110">Refresh cached assets.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-110">Refresh cached assets.</span></span>
> * <span data-ttu-id="ff9ee-111">Use query strings to control cached versions.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-111">Use query strings to control cached versions.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ff9ee-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff9ee-112">Prerequisites</span></span>

<span data-ttu-id="ff9ee-113">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-113">To complete this tutorial:</span></span>

- [<span data-ttu-id="ff9ee-114">Install Git</span><span class="sxs-lookup"><span data-stu-id="ff9ee-114">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="ff9ee-115">Install Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ff9ee-115">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="ff9ee-116">Create the web app</span><span class="sxs-lookup"><span data-stu-id="ff9ee-116">Create the web app</span></span>

<span data-ttu-id="ff9ee-117">To create the web app that you'll work with, follow the [static HTML quickstart](../app-service/app-service-web-get-started-html.md) through the **Browse to the app** step.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-117">To create the web app that you'll work with, follow the [static HTML quickstart](../app-service/app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="ff9ee-118">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ff9ee-118">Log in to the Azure portal</span></span>

<span data-ttu-id="ff9ee-119">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-119">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

### <a name="dynamic-site-acceleration-optimization"></a><span data-ttu-id="ff9ee-120">Dynamic site acceleration optimization</span><span class="sxs-lookup"><span data-stu-id="ff9ee-120">Dynamic site acceleration optimization</span></span>
<span data-ttu-id="ff9ee-121">If you want to optimize your CDN endpoint for dynamic site acceleration (DSA), you should use the [CDN portal](cdn-create-new-endpoint.md) to create your profile and endpoint.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-121">If you want to optimize your CDN endpoint for dynamic site acceleration (DSA), you should use the [CDN portal](cdn-create-new-endpoint.md) to create your profile and endpoint.</span></span> <span data-ttu-id="ff9ee-122">With [DSA optimization](cdn-dynamic-site-acceleration.md), the performance of web pages with dynamic content is measurably improved.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-122">With [DSA optimization](cdn-dynamic-site-acceleration.md), the performance of web pages with dynamic content is measurably improved.</span></span> <span data-ttu-id="ff9ee-123">For instructions about how to optimize a CDN endpoint for DSA from the CDN portal, see [CDN endpoint configuration to accelerate delivery of dynamic files](cdn-dynamic-site-acceleration.md#cdn-endpoint-configuration-to-accelerate-delivery-of-dynamic-files).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-123">For instructions about how to optimize a CDN endpoint for DSA from the CDN portal, see [CDN endpoint configuration to accelerate delivery of dynamic files](cdn-dynamic-site-acceleration.md#cdn-endpoint-configuration-to-accelerate-delivery-of-dynamic-files).</span></span> <span data-ttu-id="ff9ee-124">Otherwise, if you don't want to optimize your new endpoint, you can use the web app portal to create it by following the steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-124">Otherwise, if you don't want to optimize your new endpoint, you can use the web app portal to create it by following the steps in the next section.</span></span> <span data-ttu-id="ff9ee-125">Note that for **Azure CDN from Verizon** profiles, you cannot change the optimization of a CDN endpoint after it has been created.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-125">Note that for **Azure CDN from Verizon** profiles, you cannot change the optimization of a CDN endpoint after it has been created.</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="ff9ee-126">Create a CDN profile and endpoint</span><span class="sxs-lookup"><span data-stu-id="ff9ee-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="ff9ee-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](../app-service/app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](../app-service/app-service-web-get-started-html.md).</span></span>

![Select App Service app in the portal](media/cdn-add-to-web-app/portal-select-app-services.png)

<span data-ttu-id="ff9ee-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Select CDN in the portal](media/cdn-add-to-web-app/portal-select-cdn.png)

<span data-ttu-id="ff9ee-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Create profile and endpoint in the portal](media/cdn-add-to-web-app/portal-new-endpoint.png)

| <span data-ttu-id="ff9ee-133">Setting</span><span class="sxs-lookup"><span data-stu-id="ff9ee-133">Setting</span></span> | <span data-ttu-id="ff9ee-134">Suggested value</span><span class="sxs-lookup"><span data-stu-id="ff9ee-134">Suggested value</span></span> | <span data-ttu-id="ff9ee-135">Description</span><span class="sxs-lookup"><span data-stu-id="ff9ee-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="ff9ee-136">**CDN profile**</span><span class="sxs-lookup"><span data-stu-id="ff9ee-136">**CDN profile**</span></span> | <span data-ttu-id="ff9ee-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="ff9ee-137">myCDNProfile</span></span> | <span data-ttu-id="ff9ee-138">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-138">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="ff9ee-139">**Pricing tier**</span><span class="sxs-lookup"><span data-stu-id="ff9ee-139">**Pricing tier**</span></span> | <span data-ttu-id="ff9ee-140">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="ff9ee-140">Standard Akamai</span></span> | <span data-ttu-id="ff9ee-141">The [pricing tier](cdn-features.md) specifies the provider and available features.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-141">The [pricing tier](cdn-features.md) specifies the provider and available features.</span></span> <span data-ttu-id="ff9ee-142">This tutorial uses *Standard Akamai*.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-142">This tutorial uses *Standard Akamai*.</span></span> |
| <span data-ttu-id="ff9ee-143">**CDN endpoint name**</span><span class="sxs-lookup"><span data-stu-id="ff9ee-143">**CDN endpoint name**</span></span> | <span data-ttu-id="ff9ee-144">Any name that is unique in the azureedge.net domain</span><span class="sxs-lookup"><span data-stu-id="ff9ee-144">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="ff9ee-145">You access your cached resources at the domain *&lt;endpointname&gt;*.azureedge.net.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-145">You access your cached resources at the domain *&lt;endpointname&gt;*.azureedge.net.</span></span>

<span data-ttu-id="ff9ee-146">Select **Create** to create a CDN profile.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-146">Select **Create** to create a CDN profile.</span></span>

<span data-ttu-id="ff9ee-147">Azure creates the profile and endpoint.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-147">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="ff9ee-148">The new endpoint appears in the **Endpoints** list, and when it's provisioned, the status is **Running**.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-148">The new endpoint appears in the **Endpoints** list, and when it's provisioned, the status is **Running**.</span></span>

![New endpoint in list](media/cdn-add-to-web-app/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="ff9ee-150">Test the CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="ff9ee-150">Test the CDN endpoint</span></span>

 <span data-ttu-id="ff9ee-151">Because it takes time for the registration to propagate, the endpoint isn't immediately available for use:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-151">Because it takes time for the registration to propagate, the endpoint isn't immediately available for use:</span></span> 
   - <span data-ttu-id="ff9ee-152">For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-152">For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes.</span></span> 
   - <span data-ttu-id="ff9ee-153">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-153">For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute.</span></span> 
   - <span data-ttu-id="ff9ee-154">For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes within 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-154">For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes within 90 minutes.</span></span> 

<span data-ttu-id="ff9ee-155">The sample app has an *index.html* file and *css*, *img*, and *js* folders that contain other static assets.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-155">The sample app has an *index.html* file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="ff9ee-156">The content paths for all of these files are the same at the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-156">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="ff9ee-157">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-157">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="ff9ee-158">Navigate a browser to the following URL:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-158">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Sample app home page served from CDN](media/cdn-add-to-web-app/sample-app-home-page-cdn.png)

 <span data-ttu-id="ff9ee-160">You see the same page that you ran earlier in an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-160">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="ff9ee-161">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="ff9ee-161">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="ff9ee-162">To ensure that this page is cached in the CDN, refresh the page.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-162">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="ff9ee-163">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-163">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="ff9ee-164">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-164">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="ff9ee-165">Purge the CDN</span><span class="sxs-lookup"><span data-stu-id="ff9ee-165">Purge the CDN</span></span>

<span data-ttu-id="ff9ee-166">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-166">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="ff9ee-167">The default TTL is seven days.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-167">The default TTL is seven days.</span></span>

<span data-ttu-id="ff9ee-168">At times you might need to refresh the CDN before the TTL expiration; for example, when you deploy updated content to the web app.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-168">At times you might need to refresh the CDN before the TTL expiration; for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="ff9ee-169">To trigger a refresh, manually purge the CDN resources.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-169">To trigger a refresh, manually purge the CDN resources.</span></span> 

<span data-ttu-id="ff9ee-170">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-170">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="ff9ee-171">Deploy a change to the web app</span><span class="sxs-lookup"><span data-stu-id="ff9ee-171">Deploy a change to the web app</span></span>

<span data-ttu-id="ff9ee-172">Open the *index.html* file and add *- V2* to the H1 heading, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-172">Open the *index.html* file and add *- V2* to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="ff9ee-173">Commit your change and deploy it to the web app.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-173">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="ff9ee-174">Once deployment has completed, browse to the web app URL to see the change.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-174">Once deployment has completed, browse to the web app URL to see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 in title in web app](media/cdn-add-to-web-app/v2-in-web-app-title.png)

<span data-ttu-id="ff9ee-176">If you browse to the CDN endpoint URL for the home page, you won't see the change because the cached version in the CDN hasn't expired yet.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-176">If you browse to the CDN endpoint URL for the home page, you won't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![No V2 in title in CDN](media/cdn-add-to-web-app/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="ff9ee-178">Purge the CDN in the portal</span><span class="sxs-lookup"><span data-stu-id="ff9ee-178">Purge the CDN in the portal</span></span>

<span data-ttu-id="ff9ee-179">To trigger the CDN to update its cached version, purge the CDN.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-179">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="ff9ee-180">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-180">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Select resource group](media/cdn-add-to-web-app/portal-select-group.png)

<span data-ttu-id="ff9ee-182">In the list of resources, select your CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-182">In the list of resources, select your CDN endpoint.</span></span>

![Select endpoint](media/cdn-add-to-web-app/portal-select-endpoint.png)

<span data-ttu-id="ff9ee-184">At the top of the **Endpoint** page, select **Purge**.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-184">At the top of the **Endpoint** page, select **Purge**.</span></span>

![Select Purge](media/cdn-add-to-web-app/portal-select-purge.png)

<span data-ttu-id="ff9ee-186">Enter the content paths you want to purge.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-186">Enter the content paths you want to purge.</span></span> <span data-ttu-id="ff9ee-187">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-187">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="ff9ee-188">Because you changed *index.html*, ensure that is in one of the paths.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-188">Because you changed *index.html*, ensure that is in one of the paths.</span></span>

<span data-ttu-id="ff9ee-189">At the bottom of the page, select **Purge**.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-189">At the bottom of the page, select **Purge**.</span></span>

![Purge page](media/cdn-add-to-web-app/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="ff9ee-191">Verify that the CDN is updated</span><span class="sxs-lookup"><span data-stu-id="ff9ee-191">Verify that the CDN is updated</span></span>

<span data-ttu-id="ff9ee-192">Wait until the purge request finishes processing, which is typically a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-192">Wait until the purge request finishes processing, which is typically a couple of minutes.</span></span> <span data-ttu-id="ff9ee-193">To see the current status, select the bell icon at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-193">To see the current status, select the bell icon at the top of the page.</span></span> 

![Purge notification](media/cdn-add-to-web-app/portal-purge-notification.png)

<span data-ttu-id="ff9ee-195">When you browse to the CDN endpoint URL for *index.html*, you'll see the *V2* that you added to the title on the home page, which indicates that the CDN cache has been refreshed.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-195">When you browse to the CDN endpoint URL for *index.html*, you'll see the *V2* that you added to the title on the home page, which indicates that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 in title in CDN](media/cdn-add-to-web-app/v2-in-cdn-title.png)

<span data-ttu-id="ff9ee-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="ff9ee-198">Use query strings to version content</span><span class="sxs-lookup"><span data-stu-id="ff9ee-198">Use query strings to version content</span></span>

<span data-ttu-id="ff9ee-199">Azure CDN offers the following caching behavior options:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-199">Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="ff9ee-200">Ignore query strings</span><span class="sxs-lookup"><span data-stu-id="ff9ee-200">Ignore query strings</span></span>
* <span data-ttu-id="ff9ee-201">Bypass caching for query strings</span><span class="sxs-lookup"><span data-stu-id="ff9ee-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="ff9ee-202">Cache every unique URL</span><span class="sxs-lookup"><span data-stu-id="ff9ee-202">Cache every unique URL</span></span> 

<span data-ttu-id="ff9ee-203">The first option is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-203">The first option is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="ff9ee-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="ff9ee-205">Change the cache behavior</span><span class="sxs-lookup"><span data-stu-id="ff9ee-205">Change the cache behavior</span></span>

<span data-ttu-id="ff9ee-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="ff9ee-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="ff9ee-208">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-208">Select **Save**.</span></span>

![Select query string caching behavior](media/cdn-add-to-web-app/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="ff9ee-210">Verify that unique URLs are cached separately</span><span class="sxs-lookup"><span data-stu-id="ff9ee-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="ff9ee-211">In a browser, navigate to the home page at the CDN endpoint, and include a query string:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-211">In a browser, navigate to the home page at the CDN endpoint, and include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="ff9ee-212">Azure CDN returns the current web app content, which includes *V2* in the heading.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-212">Azure CDN returns the current web app content, which includes *V2* in the heading.</span></span> 

<span data-ttu-id="ff9ee-213">To ensure that this page is cached in the CDN, refresh the page.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="ff9ee-214">Open *index.html*, change *V2* to *V3*, then deploy the change.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-214">Open *index.html*, change *V2* to *V3*, then deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="ff9ee-215">In a browser, go to the CDN endpoint URL with a new query string, such as `q=2`.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-215">In a browser, go to the CDN endpoint URL with a new query string, such as `q=2`.</span></span> <span data-ttu-id="ff9ee-216">Azure CDN gets the current *index.html* file and displays *V3*.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-216">Azure CDN gets the current *index.html* file and displays *V3*.</span></span> <span data-ttu-id="ff9ee-217">However, if you navigate to the CDN endpoint with the `q=1` query string, you see *V2*.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-217">However, if you navigate to the CDN endpoint with the `q=1` query string, you see *V2*.</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 in title in CDN, query string 2](media/cdn-add-to-web-app/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 in title in CDN, query string 1](media/cdn-add-to-web-app/v2-in-cdn-title-qs1.png)

<span data-ttu-id="ff9ee-220">This output shows that each query string is treated differently:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="ff9ee-221">q=1 was used before, so cached contents are returned (V2).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="ff9ee-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="ff9ee-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="ff9ee-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ff9ee-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff9ee-224">Next steps</span></span>

<span data-ttu-id="ff9ee-225">What you learned:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-225">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff9ee-226">Create a CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-226">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="ff9ee-227">Refresh cached assets.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-227">Refresh cached assets.</span></span>
> * <span data-ttu-id="ff9ee-228">Use query strings to control cached versions.</span><span class="sxs-lookup"><span data-stu-id="ff9ee-228">Use query strings to control cached versions.</span></span>

<span data-ttu-id="ff9ee-229">Learn how to optimize CDN performance in the following articles:</span><span class="sxs-lookup"><span data-stu-id="ff9ee-229">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff9ee-230">Tutorial: Add a custom domain to your Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="ff9ee-230">Tutorial: Add a custom domain to your Azure CDN endpoint</span></span>](cdn-map-content-to-custom-domain.md)


