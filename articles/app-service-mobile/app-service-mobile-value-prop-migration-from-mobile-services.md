---
title: I use Mobile Services, how does App Service help?
description: Learn what advantages does App Service bring to your existing Mobile Services projects.
services: app-service\mobile
documentationcenter: ios
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: b3809320a113ac7913229bfb99be170cc53999da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555713"
---
# <span data-ttu-id="14713-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span><span class="sxs-lookup"><span data-stu-id="14713-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="14713-104">Overview</span><span class="sxs-lookup"><span data-stu-id="14713-104">Overview</span></span>
<span data-ttu-id="14713-105">Your existing Mobile Service is safe and will remain supported.</span><span class="sxs-lookup"><span data-stu-id="14713-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="14713-106">However there are number of advantages the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="14713-106">However there are number of advantages the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="14713-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span><span class="sxs-lookup"><span data-stu-id="14713-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="14713-108">New host features including Web Jobs, custom CNames, better monitoring</span><span class="sxs-lookup"><span data-stu-id="14713-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="14713-109">Turnkey integration with Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="14713-109">Turnkey integration with Traffic Manager</span></span>
* <span data-ttu-id="14713-110">Connectivity to your on-premise resources and VPNs using VNet in addition to Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="14713-110">Connectivity to your on-premise resources and VPNs using VNet in addition to Hybrid Connections</span></span>
* <span data-ttu-id="14713-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span><span class="sxs-lookup"><span data-stu-id="14713-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span></span>
* <span data-ttu-id="14713-112">Richer spectrum of the underlying compute resources and pricing</span><span class="sxs-lookup"><span data-stu-id="14713-112">Richer spectrum of the underlying compute resources and pricing</span></span>
* <span data-ttu-id="14713-113">Built-in auto scale, load balancing, and performance monitoring.</span><span class="sxs-lookup"><span data-stu-id="14713-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="14713-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span><span class="sxs-lookup"><span data-stu-id="14713-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="14713-115">New hosting features</span><span class="sxs-lookup"><span data-stu-id="14713-115">New hosting features</span></span>
<span data-ttu-id="14713-116">In *Azure App Service* the *Mobile App* backend code runs in the same container as Web App and API App.</span><span class="sxs-lookup"><span data-stu-id="14713-116">In *Azure App Service* the *Mobile App* backend code runs in the same container as Web App and API App.</span></span> <span data-ttu-id="14713-117">As such you can take advantage of all the features in this container, including some of those that are not currently present in Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="14713-117">As such you can take advantage of all the features in this container, including some of those that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="14713-118">Add continuously running backend logic via Web Jobs</span><span class="sxs-lookup"><span data-stu-id="14713-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="14713-119">Ensure your backend code is always running</span><span class="sxs-lookup"><span data-stu-id="14713-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="14713-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span><span class="sxs-lookup"><span data-stu-id="14713-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span></span>
* <span data-ttu-id="14713-121">Geo-scale your app with Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="14713-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="14713-122">Include any libraries and packages you want.</span><span class="sxs-lookup"><span data-stu-id="14713-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="14713-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span><span class="sxs-lookup"><span data-stu-id="14713-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="14713-124">(For Node.js) Leverage any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span><span class="sxs-lookup"><span data-stu-id="14713-124">(For Node.js) Leverage any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="14713-125">Access on-premises data using VNet</span><span class="sxs-lookup"><span data-stu-id="14713-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="14713-126">With Mobile Services today you can already use Hybrid Connections to access on-premise resources.</span><span class="sxs-lookup"><span data-stu-id="14713-126">With Mobile Services today you can already use Hybrid Connections to access on-premise resources.</span></span> <span data-ttu-id="14713-127">However there are situations where a VPN solution is preferred.</span><span class="sxs-lookup"><span data-stu-id="14713-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="14713-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span><span class="sxs-lookup"><span data-stu-id="14713-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="14713-129">Use your favorite backend language</span><span class="sxs-lookup"><span data-stu-id="14713-129">Use your favorite backend language</span></span>
<span data-ttu-id="14713-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span><span class="sxs-lookup"><span data-stu-id="14713-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="14713-131">Set up automatic scale</span><span class="sxs-lookup"><span data-stu-id="14713-131">Set up automatic scale</span></span>
<span data-ttu-id="14713-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span><span class="sxs-lookup"><span data-stu-id="14713-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="14713-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span><span class="sxs-lookup"><span data-stu-id="14713-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="14713-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span><span class="sxs-lookup"><span data-stu-id="14713-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-the-know"></a><span data-ttu-id="14713-135">Be in the “know”</span><span class="sxs-lookup"><span data-stu-id="14713-135">Be in the “know”</span></span>
<span data-ttu-id="14713-136">React to issues in real-time with monitoring and alerts to automatically notify you and your team.</span><span class="sxs-lookup"><span data-stu-id="14713-136">React to issues in real-time with monitoring and alerts to automatically notify you and your team.</span></span> <span data-ttu-id="14713-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights to get even richer insight into how your Mobile app is performing.</span><span class="sxs-lookup"><span data-stu-id="14713-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights to get even richer insight into how your Mobile app is performing.</span></span> <span data-ttu-id="14713-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="14713-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via the Azure Portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="14713-139">Keep your assets safe</span><span class="sxs-lookup"><span data-stu-id="14713-139">Keep your assets safe</span></span>
<span data-ttu-id="14713-140">Automatically back up your backend and database.</span><span class="sxs-lookup"><span data-stu-id="14713-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="14713-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span><span class="sxs-lookup"><span data-stu-id="14713-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="14713-142">Ready, Stage, Go!</span><span class="sxs-lookup"><span data-stu-id="14713-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="14713-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span><span class="sxs-lookup"><span data-stu-id="14713-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="14713-144">Use them to perform testing before you deploy.</span><span class="sxs-lookup"><span data-stu-id="14713-144">Use them to perform testing before you deploy.</span></span> <span data-ttu-id="14713-145">Swap to production with no downtime.</span><span class="sxs-lookup"><span data-stu-id="14713-145">Swap to production with no downtime.</span></span> <span data-ttu-id="14713-146">Web apps are pre-loaded, ensuring the best customer experience.</span><span class="sxs-lookup"><span data-stu-id="14713-146">Web apps are pre-loaded, ensuring the best customer experience.</span></span>

<span data-ttu-id="14713-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="14713-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>

