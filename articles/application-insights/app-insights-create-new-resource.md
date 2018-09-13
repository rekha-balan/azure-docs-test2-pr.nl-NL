---
title: Create a new Azure Application Insights resource | Microsoft Docs
description: Manually set up Application Insights monitoring for a new live application.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: awills
ms.openlocfilehash: ba888881955e7d6f37f0e47f303933dd408d6603
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564171"
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="2481f-103">Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="2481f-103">Create an Application Insights resource</span></span>
<span data-ttu-id="2481f-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span><span class="sxs-lookup"><span data-stu-id="2481f-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="2481f-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span><span class="sxs-lookup"><span data-stu-id="2481f-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="2481f-106">In many cases, this can be done automatically by the IDE, and that's the recommended way where it's available.</span><span class="sxs-lookup"><span data-stu-id="2481f-106">In many cases, this can be done automatically by the IDE, and that's the recommended way where it's available.</span></span> <span data-ttu-id="2481f-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span><span class="sxs-lookup"><span data-stu-id="2481f-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="2481f-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span><span class="sxs-lookup"><span data-stu-id="2481f-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="2481f-109">This sends the telemetry to the resource.</span><span class="sxs-lookup"><span data-stu-id="2481f-109">This sends the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="2481f-110">Sign up to Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2481f-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="2481f-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="2481f-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="2481f-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span><span class="sxs-lookup"><span data-stu-id="2481f-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="2481f-113">You'll also need a subscription to [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="2481f-113">You'll also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="2481f-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="2481f-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="2481f-115">You're only charged for what you use, and the default basic plan allows for a certain amount of experimental use free of charge.</span><span class="sxs-lookup"><span data-stu-id="2481f-115">You're only charged for what you use, and the default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="2481f-116">When you've got access to a subscription, login to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span><span class="sxs-lookup"><span data-stu-id="2481f-116">When you've got access to a subscription, login to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="2481f-117">Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="2481f-117">Create an Application Insights resource</span></span>
<span data-ttu-id="2481f-118">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span><span class="sxs-lookup"><span data-stu-id="2481f-118">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Click New, Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="2481f-120">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="2481f-120">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="2481f-121">If you don't see your type of app, choose General.</span><span class="sxs-lookup"><span data-stu-id="2481f-121">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="2481f-122">**Subscription** is your payment account in Azure.</span><span class="sxs-lookup"><span data-stu-id="2481f-122">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="2481f-123">**Resource group** is a convenience for managing properties like access control.</span><span class="sxs-lookup"><span data-stu-id="2481f-123">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="2481f-124">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span><span class="sxs-lookup"><span data-stu-id="2481f-124">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="2481f-125">**Location** is where we keep your data.</span><span class="sxs-lookup"><span data-stu-id="2481f-125">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="2481f-126">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span><span class="sxs-lookup"><span data-stu-id="2481f-126">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="2481f-127">Recommended.</span><span class="sxs-lookup"><span data-stu-id="2481f-127">Recommended.</span></span>

<span data-ttu-id="2481f-128">When your app has been created, a new blade opens.</span><span class="sxs-lookup"><span data-stu-id="2481f-128">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="2481f-129">This is where you'll see performance and usage data about your app.</span><span class="sxs-lookup"><span data-stu-id="2481f-129">This is where you'll see performance and usage data about your app.</span></span> 

<span data-ttu-id="2481f-130">To get back to it next time you login to Azure, look for your app's quick-start tile on the start board (home screen).</span><span class="sxs-lookup"><span data-stu-id="2481f-130">To get back to it next time you login to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="2481f-131">Or click Browse to find it.</span><span class="sxs-lookup"><span data-stu-id="2481f-131">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="2481f-132">Copy the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="2481f-132">Copy the instrumentation key</span></span>
<span data-ttu-id="2481f-133">The instrumentation key identifies the resource that you created.</span><span class="sxs-lookup"><span data-stu-id="2481f-133">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="2481f-134">You'll need it to give to the SDK.</span><span class="sxs-lookup"><span data-stu-id="2481f-134">You'll need it to give to the SDK.</span></span>

![Click Essentials, click the Instrumentation Key, CTRL+C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="2481f-136">Install the SDK in your app</span><span class="sxs-lookup"><span data-stu-id="2481f-136">Install the SDK in your app</span></span>
<span data-ttu-id="2481f-137">Install the Application Insights SDK in your app.</span><span class="sxs-lookup"><span data-stu-id="2481f-137">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="2481f-138">This step depends heavily on the type of your application.</span><span class="sxs-lookup"><span data-stu-id="2481f-138">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="2481f-139">Use the instrumentation key to configure [the SDK that you install in your application][start].</span><span class="sxs-lookup"><span data-stu-id="2481f-139">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="2481f-140">The SDK includes standard modules that send telemetry without you having to write any code.</span><span class="sxs-lookup"><span data-stu-id="2481f-140">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="2481f-141">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span><span class="sxs-lookup"><span data-stu-id="2481f-141">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <a name="monitor"></a><span data-ttu-id="2481f-142">See telemetry data</span><span class="sxs-lookup"><span data-stu-id="2481f-142">See telemetry data</span></span>
<span data-ttu-id="2481f-143">Close the quick start blade to return to your application blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2481f-143">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="2481f-144">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events will appear.</span><span class="sxs-lookup"><span data-stu-id="2481f-144">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events will appear.</span></span> 

<span data-ttu-id="2481f-145">Click Refresh after a few seconds if you're expecting more data.</span><span class="sxs-lookup"><span data-stu-id="2481f-145">Click Refresh after a few seconds if you're expecting more data.</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="2481f-146">Creating a resource automatically</span><span class="sxs-lookup"><span data-stu-id="2481f-146">Creating a resource automatically</span></span>
<span data-ttu-id="2481f-147">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span><span class="sxs-lookup"><span data-stu-id="2481f-147">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2481f-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="2481f-148">Next steps</span></span>
* [<span data-ttu-id="2481f-149">Create a dashboard</span><span class="sxs-lookup"><span data-stu-id="2481f-149">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="2481f-150">Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="2481f-150">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="2481f-151">Explore metrics</span><span class="sxs-lookup"><span data-stu-id="2481f-151">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="2481f-152">Write Analytics queries</span><span class="sxs-lookup"><span data-stu-id="2481f-152">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md



