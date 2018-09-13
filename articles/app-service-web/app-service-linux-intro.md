---
title: Introduction to App Service on Linux | Microsoft Docs
description: Learn about App Service on Linux.
keywords: azure app service, linux, oss
services: app-service
documentationcenter: ''
author: naziml
manager: erikre
editor: ''
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 2cf0b56eea8180aad0ff99ac617262e33b8f23fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554736"
---
# <a name="introduction-to-app-service-on-linux"></a><span data-ttu-id="909f3-104">Introduction to App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="909f3-104">Introduction to App Service on Linux</span></span>
<span data-ttu-id="909f3-105">Azure App Service on Linux is currently in public preview and supports running web apps natively on Linux.</span><span class="sxs-lookup"><span data-stu-id="909f3-105">Azure App Service on Linux is currently in public preview and supports running web apps natively on Linux.</span></span>

## <a name="overview"></a><span data-ttu-id="909f3-106">Overview</span><span class="sxs-lookup"><span data-stu-id="909f3-106">Overview</span></span>
<span data-ttu-id="909f3-107">Customers can use App Service on Linux to host web apps natively on Linux for supported application stacks.</span><span class="sxs-lookup"><span data-stu-id="909f3-107">Customers can use App Service on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="909f3-108">The following section lists the application stacks that are currently supported.</span><span class="sxs-lookup"><span data-stu-id="909f3-108">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="909f3-109">Features</span><span class="sxs-lookup"><span data-stu-id="909f3-109">Features</span></span>
<span data-ttu-id="909f3-110">App Service on Linux currently supports the following application stacks:</span><span class="sxs-lookup"><span data-stu-id="909f3-110">App Service on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="909f3-111">Node.js</span><span class="sxs-lookup"><span data-stu-id="909f3-111">Node.js</span></span>
    * <span data-ttu-id="909f3-112">4.5.0</span><span class="sxs-lookup"><span data-stu-id="909f3-112">4.5.0</span></span>
    * <span data-ttu-id="909f3-113">4.4.7</span><span class="sxs-lookup"><span data-stu-id="909f3-113">4.4.7</span></span>
    * <span data-ttu-id="909f3-114">6.2.2</span><span class="sxs-lookup"><span data-stu-id="909f3-114">6.2.2</span></span>
    * <span data-ttu-id="909f3-115">6.6.0</span><span class="sxs-lookup"><span data-stu-id="909f3-115">6.6.0</span></span>
    * <span data-ttu-id="909f3-116">6.9.3</span><span class="sxs-lookup"><span data-stu-id="909f3-116">6.9.3</span></span>
* <span data-ttu-id="909f3-117">PHP</span><span class="sxs-lookup"><span data-stu-id="909f3-117">PHP</span></span>
    * <span data-ttu-id="909f3-118">5.6.23</span><span class="sxs-lookup"><span data-stu-id="909f3-118">5.6.23</span></span>
    * <span data-ttu-id="909f3-119">7.0.6</span><span class="sxs-lookup"><span data-stu-id="909f3-119">7.0.6</span></span>
* <span data-ttu-id="909f3-120">.Net Core</span><span class="sxs-lookup"><span data-stu-id="909f3-120">.Net Core</span></span>
    * <span data-ttu-id="909f3-121">1.0</span><span class="sxs-lookup"><span data-stu-id="909f3-121">1.0</span></span>
* <span data-ttu-id="909f3-122">Ruby</span><span class="sxs-lookup"><span data-stu-id="909f3-122">Ruby</span></span>
    * <span data-ttu-id="909f3-123">2.3</span><span class="sxs-lookup"><span data-stu-id="909f3-123">2.3</span></span>

<span data-ttu-id="909f3-124">Customers can deploy their applications by using:</span><span class="sxs-lookup"><span data-stu-id="909f3-124">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="909f3-125">FTP</span><span class="sxs-lookup"><span data-stu-id="909f3-125">FTP</span></span>
* <span data-ttu-id="909f3-126">Local Git</span><span class="sxs-lookup"><span data-stu-id="909f3-126">Local Git</span></span>
* <span data-ttu-id="909f3-127">GitHub</span><span class="sxs-lookup"><span data-stu-id="909f3-127">GitHub</span></span>
* <span data-ttu-id="909f3-128">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="909f3-128">Bitbucket</span></span>

<span data-ttu-id="909f3-129">For application scaling:</span><span class="sxs-lookup"><span data-stu-id="909f3-129">For application scaling:</span></span>

* <span data-ttu-id="909f3-130">Customers can scale web apps up and down by changing the tier in their App Service plan.</span><span class="sxs-lookup"><span data-stu-id="909f3-130">Customers can scale web apps up and down by changing the tier in their App Service plan.</span></span>
* <span data-ttu-id="909f3-131">Customers can scale out applications and run multiple app instances within the confines of their SKU.</span><span class="sxs-lookup"><span data-stu-id="909f3-131">Customers can scale out applications and run multiple app instances within the confines of their SKU.</span></span>

<span data-ttu-id="909f3-132">For Kudu, some of the basic functionality works with the following:</span><span class="sxs-lookup"><span data-stu-id="909f3-132">For Kudu, some of the basic functionality works with the following:</span></span>

* <span data-ttu-id="909f3-133">Environments</span><span class="sxs-lookup"><span data-stu-id="909f3-133">Environments</span></span>
* <span data-ttu-id="909f3-134">Deployments</span><span class="sxs-lookup"><span data-stu-id="909f3-134">Deployments</span></span>
* <span data-ttu-id="909f3-135">Basic consoles</span><span class="sxs-lookup"><span data-stu-id="909f3-135">Basic consoles</span></span>

## <a name="limitations"></a><span data-ttu-id="909f3-136">Limitations</span><span class="sxs-lookup"><span data-stu-id="909f3-136">Limitations</span></span>
<span data-ttu-id="909f3-137">The Azure portal shows only features that currently work for App Service on Linux and hides the rest.</span><span class="sxs-lookup"><span data-stu-id="909f3-137">The Azure portal shows only features that currently work for App Service on Linux and hides the rest.</span></span> <span data-ttu-id="909f3-138">As we enable more features, they will be visible on the portal.</span><span class="sxs-lookup"><span data-stu-id="909f3-138">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="909f3-139">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not complete.</span><span class="sxs-lookup"><span data-stu-id="909f3-139">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not complete.</span></span> <span data-ttu-id="909f3-140">Once we complete these features, we will update our documentation and blog about the changes.</span><span class="sxs-lookup"><span data-stu-id="909f3-140">Once we complete these features, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="909f3-141">This public preview is currently only available in the following regions:</span><span class="sxs-lookup"><span data-stu-id="909f3-141">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="909f3-142">West US</span><span class="sxs-lookup"><span data-stu-id="909f3-142">West US</span></span>
* <span data-ttu-id="909f3-143">West Europe</span><span class="sxs-lookup"><span data-stu-id="909f3-143">West Europe</span></span> 
* <span data-ttu-id="909f3-144">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="909f3-144">Southeast Asia</span></span>

<span data-ttu-id="909f3-145">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span><span class="sxs-lookup"><span data-stu-id="909f3-145">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="909f3-146">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span><span class="sxs-lookup"><span data-stu-id="909f3-146">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="909f3-147">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span><span class="sxs-lookup"><span data-stu-id="909f3-147">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

<span data-ttu-id="909f3-148">Web Apps on Linux does not yet support deployment of .NET Core apps from uncompiled source.</span><span class="sxs-lookup"><span data-stu-id="909f3-148">Web Apps on Linux does not yet support deployment of .NET Core apps from uncompiled source.</span></span> <span data-ttu-id="909f3-149">You need to publish/compile your .NET Core app locally first, and then push the published site bits to your app.</span><span class="sxs-lookup"><span data-stu-id="909f3-149">You need to publish/compile your .NET Core app locally first, and then push the published site bits to your app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="909f3-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="909f3-150">Next steps</span></span>
<span data-ttu-id="909f3-151">See the following links to get started with App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="909f3-151">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="909f3-152">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="909f3-152">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="909f3-153">Creating Web Apps in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="909f3-153">Creating Web Apps in App Service on Linux</span></span>](app-service-linux-how-to-create-a-web-app.md)
* [<span data-ttu-id="909f3-154">How to use a custom Docker image for App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="909f3-154">How to use a custom Docker image for App Service on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="909f3-155">Using PM2 Configuration for Node.js in Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="909f3-155">Using PM2 Configuration for Node.js in Web Apps on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="909f3-156">Using .NET Core in Azure App Service Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="909f3-156">Using .NET Core in Azure App Service Web Apps on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="909f3-157">Using Ruby in Azure App Service Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="909f3-157">Using Ruby in Azure App Service Web Apps on Linux</span></span>](app-service-linux-using-ruby.md)
* [<span data-ttu-id="909f3-158">Azure App Service Web Apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="909f3-158">Azure App Service Web Apps on Linux FAQ</span></span>](app-service-linux-faq.md)

