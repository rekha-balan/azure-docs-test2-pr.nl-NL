---
title: I use Mobile Services, how does App Service help?
description: Learn what advantages does App Service bring to your existing Mobile Services projects.
services: app-service\mobile
documentationcenter: ios
author: conceptdev
manager: crdun
editor: ''
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: 365f00ced38a1ddc20df211121fba43efff8ea87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779043"
---
# <span data-ttu-id="1bdc1-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span><span class="sxs-lookup"><span data-stu-id="1bdc1-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="1bdc1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1bdc1-104">Overview</span></span>
<span data-ttu-id="1bdc1-105">Your existing Mobile Service is safe and will remain supported.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="1bdc1-106">However, there are advantages that the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-106">However, there are advantages that the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="1bdc1-107">Simpler, easier, and more cost effective offering for apps that include both web and mobile clients</span><span class="sxs-lookup"><span data-stu-id="1bdc1-107">Simpler, easier, and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="1bdc1-108">New host features including Web Jobs, custom CNames, better monitoring</span><span class="sxs-lookup"><span data-stu-id="1bdc1-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="1bdc1-109">Integration with Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="1bdc1-109">Integration with Traffic Manager</span></span>
* <span data-ttu-id="1bdc1-110">Connectivity to your on-premises resources and VPNs using VNet in addition to Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="1bdc1-110">Connectivity to your on-premises resources and VPNs using VNet in addition to Hybrid Connections</span></span>
* <span data-ttu-id="1bdc1-111">Monitoring, alerting and  troubleshooting for your app using AppInsights</span><span class="sxs-lookup"><span data-stu-id="1bdc1-111">Monitoring, alerting and  troubleshooting for your app using AppInsights</span></span>
* <span data-ttu-id="1bdc1-112">Richer spectrum of the underlying compute resources and pricing</span><span class="sxs-lookup"><span data-stu-id="1bdc1-112">Richer spectrum of the underlying compute resources and pricing</span></span>
* <span data-ttu-id="1bdc1-113">Built-in auto scale, load balancing, and performance monitoring.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="1bdc1-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span><span class="sxs-lookup"><span data-stu-id="1bdc1-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="1bdc1-115">New hosting features</span><span class="sxs-lookup"><span data-stu-id="1bdc1-115">New hosting features</span></span>
<span data-ttu-id="1bdc1-116">In *Azure App Service*, the *Mobile App* backend code runs in the same container as Web App and API App.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-116">In *Azure App Service*, the *Mobile App* backend code runs in the same container as Web App and API App.</span></span> <span data-ttu-id="1bdc1-117">You can take advantage of all the features in this container, including some that are not currently present in Mobile Services:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-117">You can take advantage of all the features in this container, including some that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="1bdc1-118">Add continuously running backend logic via Web Jobs</span><span class="sxs-lookup"><span data-stu-id="1bdc1-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="1bdc1-119">Ensure your backend code is always running</span><span class="sxs-lookup"><span data-stu-id="1bdc1-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="1bdc1-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span><span class="sxs-lookup"><span data-stu-id="1bdc1-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span></span>
* <span data-ttu-id="1bdc1-121">Geo-scale your app with Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="1bdc1-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="1bdc1-122">Include any libraries and packages you want.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="1bdc1-123">(For .NET) Use any feature of ASP.NET, including MVC</span><span class="sxs-lookup"><span data-stu-id="1bdc1-123">(For .NET) Use any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="1bdc1-124">(For Node.js) Use any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-124">(For Node.js) Use any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="1bdc1-125">Access on-premises data using VNet</span><span class="sxs-lookup"><span data-stu-id="1bdc1-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="1bdc1-126">With Mobile Services today, you can already use Hybrid Connections to access on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-126">With Mobile Services today, you can already use Hybrid Connections to access on-premises resources.</span></span> <span data-ttu-id="1bdc1-127">However there are situations where a VPN solution is preferred.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="1bdc1-128">With *Azure App Service*, you can use Azure VNet for your Mobile App backend code.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-128">With *Azure App Service*, you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="1bdc1-129">Use your favorite backend language</span><span class="sxs-lookup"><span data-stu-id="1bdc1-129">Use your favorite backend language</span></span>
<span data-ttu-id="1bdc1-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="1bdc1-131">Set up automatic scale</span><span class="sxs-lookup"><span data-stu-id="1bdc1-131">Set up automatic scale</span></span>
<span data-ttu-id="1bdc1-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="1bdc1-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="1bdc1-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-the-know"></a><span data-ttu-id="1bdc1-135">Be in the “know”</span><span class="sxs-lookup"><span data-stu-id="1bdc1-135">Be in the “know”</span></span>
<span data-ttu-id="1bdc1-136">React to issues in real time with monitoring and alerts to automatically notify you and your team.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-136">React to issues in real time with monitoring and alerts to automatically notify you and your team.</span></span> <span data-ttu-id="1bdc1-137">Integrate advanced app analytics and monitoring functionality from AppInsights to get insight into how your mobile app is performing.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-137">Integrate advanced app analytics and monitoring functionality from AppInsights to get insight into how your mobile app is performing.</span></span> <span data-ttu-id="1bdc1-138">With *Azure App Service*, you can now set up alerts based on variety of performance metrics, either programmatically and via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-138">With *Azure App Service*, you can now set up alerts based on variety of performance metrics, either programmatically and via the Azure portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="1bdc1-139">Keep your assets safe</span><span class="sxs-lookup"><span data-stu-id="1bdc1-139">Keep your assets safe</span></span>
<span data-ttu-id="1bdc1-140">Automatically back up your backend and database.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="1bdc1-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="1bdc1-142">Ready, Stage, Go!</span><span class="sxs-lookup"><span data-stu-id="1bdc1-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="1bdc1-143">With *Azure App Service*, you can now create multiple private testing and staging environments for your mobile apps.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-143">With *Azure App Service*, you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="1bdc1-144">Use them to perform testing before you deploy.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-144">Use them to perform testing before you deploy.</span></span> <span data-ttu-id="1bdc1-145">Swap to production with no downtime.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-145">Swap to production with no downtime.</span></span> <span data-ttu-id="1bdc1-146">Web apps are pre-loaded, ensuring the best customer experience.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-146">Web apps are pre-loaded, ensuring the best customer experience.</span></span>

<span data-ttu-id="1bdc1-147">You can start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc1-147">You can start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>
