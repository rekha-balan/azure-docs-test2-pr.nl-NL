---
title: Get started with test in production for Web Apps
description: Learn about the Test in Production (TiP) feature in Azure App Service Web Apps.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 6ed4477b03dceea81c4e514078120872d49953b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551129"
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="8cd1b-103">Get started with test in production for Web Apps</span><span class="sxs-lookup"><span data-stu-id="8cd1b-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="8cd1b-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="8cd1b-105">It enables you to test the quality of your apps with live user traffic in your production environment, as opposed to synthesized data in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-105">It enables you to test the quality of your apps with live user traffic in your production environment, as opposed to synthesized data in a test environment.</span></span> <span data-ttu-id="8cd1b-106">By exposing your new app to real users, you can be informed on the real problems your app may face once it is deployed.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-106">By exposing your new app to real users, you can be informed on the real problems your app may face once it is deployed.</span></span> <span data-ttu-id="8cd1b-107">You can verify the functionality, performance, and value of your app updates against the volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-107">You can verify the functionality, performance, and value of your app updates against the volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="8cd1b-108">Traffic Routing in App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="8cd1b-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="8cd1b-109">With the Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic to one or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) to validate your change.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-109">With the Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic to one or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) to validate your change.</span></span> <span data-ttu-id="8cd1b-110">For example, you can implement the following scenarios with App Service:</span><span class="sxs-lookup"><span data-stu-id="8cd1b-110">For example, you can implement the following scenarios with App Service:</span></span>

* <span data-ttu-id="8cd1b-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior to site-wide deployment</span><span class="sxs-lookup"><span data-stu-id="8cd1b-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior to site-wide deployment</span></span>
* <span data-ttu-id="8cd1b-112">Perform "controlled test flights" of your changes by measuring usability metrics on the beta app</span><span class="sxs-lookup"><span data-stu-id="8cd1b-112">Perform "controlled test flights" of your changes by measuring usability metrics on the beta app</span></span>
* <span data-ttu-id="8cd1b-113">Gradually ramp up to a new update, and gracefully back down to the current version if an error occurs</span><span class="sxs-lookup"><span data-stu-id="8cd1b-113">Gradually ramp up to a new update, and gracefully back down to the current version if an error occurs</span></span> 
* <span data-ttu-id="8cd1b-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span><span class="sxs-lookup"><span data-stu-id="8cd1b-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="8cd1b-115">Requirements for using Traffic Routing in Web Apps</span><span class="sxs-lookup"><span data-stu-id="8cd1b-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="8cd1b-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="8cd1b-117">In order to work properly, Traffic Routing requires cookies to be enabled in the users' browser.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-117">In order to work properly, Traffic Routing requires cookies to be enabled in the users' browser.</span></span> <span data-ttu-id="8cd1b-118">Traffic Routing uses cookies to pin a client browser to a deployment slot for the life the client session.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-118">Traffic Routing uses cookies to pin a client browser to a deployment slot for the life the client session.</span></span>
* <span data-ttu-id="8cd1b-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-to-a-deployment-slot"></a><span data-ttu-id="8cd1b-120">Route traffic segment to a deployment slot</span><span class="sxs-lookup"><span data-stu-id="8cd1b-120">Route traffic segment to a deployment slot</span></span>
<span data-ttu-id="8cd1b-121">At the basic level in every TiP scenario, you route a predefined percentage of your live traffic to a non-production deployment slot.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-121">At the basic level in every TiP scenario, you route a predefined percentage of your live traffic to a non-production deployment slot.</span></span> <span data-ttu-id="8cd1b-122">To do this, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="8cd1b-122">To do this, follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="8cd1b-123">The steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that the desired web app content is already [deployed](web-sites-deploy.md) to it.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-123">The steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that the desired web app content is already [deployed](web-sites-deploy.md) to it.</span></span>
> 
> 

1. <span data-ttu-id="8cd1b-124">Log into the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8cd1b-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8cd1b-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="8cd1b-126">Select the slot that you want to route traffic to and the percentage of the total traffic you desire, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-126">Select the slot that you want to route traffic to and the percentage of the total traffic you desire, then click **Save**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="8cd1b-127">Go to the deployment slot's blade.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-127">Go to the deployment slot's blade.</span></span> <span data-ttu-id="8cd1b-128">You should now see live traffic being routed to it.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-128">You should now see live traffic being routed to it.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="8cd1b-129">Once Traffic Routing is configured, the specified percentage of clients will be randomly routed to your non-production slot.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-129">Once Traffic Routing is configured, the specified percentage of clients will be randomly routed to your non-production slot.</span></span> <span data-ttu-id="8cd1b-130">However, it is important to note that once a client is automatically routed to a specific slot, it will be "pinned" to that slot for the life of that client session.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-130">However, it is important to note that once a client is automatically routed to a specific slot, it will be "pinned" to that slot for the life of that client session.</span></span> <span data-ttu-id="8cd1b-131">This done using a cookie to pin the user session.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-131">This done using a cookie to pin the user session.</span></span> <span data-ttu-id="8cd1b-132">If you inspect the HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-132">If you inspect the HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a><span data-ttu-id="8cd1b-133">Force client requests to a specific slot</span><span class="sxs-lookup"><span data-stu-id="8cd1b-133">Force client requests to a specific slot</span></span>
<span data-ttu-id="8cd1b-134">In addition to automatic traffic routing, App Service is able to route requests to a specific slot.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-134">In addition to automatic traffic routing, App Service is able to route requests to a specific slot.</span></span> <span data-ttu-id="8cd1b-135">This is useful when you want your users to be able to opt-into or opt-out of your beta app.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-135">This is useful when you want your users to be able to opt-into or opt-out of your beta app.</span></span> <span data-ttu-id="8cd1b-136">To do this, you use the `x-ms-routing-name` query parameter.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-136">To do this, you use the `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="8cd1b-137">To reroute users to a specific slot using `x-ms-routing-name`, you must make sure that the slot is already added to the Traffic Routing list.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-137">To reroute users to a specific slot using `x-ms-routing-name`, you must make sure that the slot is already added to the Traffic Routing list.</span></span> <span data-ttu-id="8cd1b-138">Since you want to route to a slot explicitly, the actual routing percentage you set doesn't matter.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-138">Since you want to route to a slot explicitly, the actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="8cd1b-139">If you want, you can craft a "beta link" that users can click to access the beta app.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-139">If you want, you can craft a "beta link" that users can click to access the beta app.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="8cd1b-140">Opt users out of beta app</span><span class="sxs-lookup"><span data-stu-id="8cd1b-140">Opt users out of beta app</span></span>
<span data-ttu-id="8cd1b-141">To let users opt out of your beta app, for example, you can put this link in your web page:</span><span class="sxs-lookup"><span data-stu-id="8cd1b-141">To let users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

<span data-ttu-id="8cd1b-142">The string `x-ms-routing-name=self` specifies the production slot.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-142">The string `x-ms-routing-name=self` specifies the production slot.</span></span> <span data-ttu-id="8cd1b-143">Once the client browser access the link, not only is it redirected to the production slot, but every subsequent request will contain the `x-ms-routing-name=self` cookie that pins the session to the production slot.</span><span class="sxs-lookup"><span data-stu-id="8cd1b-143">Once the client browser access the link, not only is it redirected to the production slot, but every subsequent request will contain the `x-ms-routing-name=self` cookie that pins the session to the production slot.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a><span data-ttu-id="8cd1b-144">Opt users in to beta app</span><span class="sxs-lookup"><span data-stu-id="8cd1b-144">Opt users in to beta app</span></span>
<span data-ttu-id="8cd1b-145">To let users opt in to your beta app, set the same query parameter to the name of the non-production slot, for example:</span><span class="sxs-lookup"><span data-stu-id="8cd1b-145">To let users opt in to your beta app, set the same query parameter to the name of the non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="8cd1b-146">More resources</span><span class="sxs-lookup"><span data-stu-id="8cd1b-146">More resources</span></span>
* [<span data-ttu-id="8cd1b-147">Set up staging environments for web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8cd1b-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="8cd1b-148">Deploy a complex application predictably in Azure</span><span class="sxs-lookup"><span data-stu-id="8cd1b-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="8cd1b-149">Agile software development with Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8cd1b-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="8cd1b-150">Use DevOps environments effectively for your web apps</span><span class="sxs-lookup"><span data-stu-id="8cd1b-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)







