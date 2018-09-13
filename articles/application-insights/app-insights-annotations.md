---
title: Release annotations for Application Insights | Microsoft Docs
description: Add deployment or build markers to your metrics explorer charts in Application Insights.
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: douge
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: awills
ms.openlocfilehash: 8cf734823a0c7712c233d629fb72f369f3b000d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671479"
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="f3db5-103">Annotations on metric charts in Application Insights</span><span class="sxs-lookup"><span data-stu-id="f3db5-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="f3db5-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span><span class="sxs-lookup"><span data-stu-id="f3db5-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="f3db5-105">They make it easy to see whether your changes had any effect on your application's performance.</span><span class="sxs-lookup"><span data-stu-id="f3db5-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="f3db5-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="f3db5-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="f3db5-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="f3db5-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Example of annotations with visible correlation with server response time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="f3db5-109">Release annotations with VSTS build</span><span class="sxs-lookup"><span data-stu-id="f3db5-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="f3db5-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f3db5-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="f3db5-111">Install the Annotations extension (one time)</span><span class="sxs-lookup"><span data-stu-id="f3db5-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="f3db5-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f3db5-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="f3db5-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span><span class="sxs-lookup"><span data-stu-id="f3db5-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="f3db5-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span><span class="sxs-lookup"><span data-stu-id="f3db5-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![At top right of Team Services web page, open Marketplace.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/10.png)

<span data-ttu-id="f3db5-117">You only need to do this once for your Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="f3db5-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="f3db5-118">Release annotations can now be configured for any project in your account.</span><span class="sxs-lookup"><span data-stu-id="f3db5-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="f3db5-119">Configure release annotations</span><span class="sxs-lookup"><span data-stu-id="f3db5-119">Configure release annotations</span></span>

<span data-ttu-id="f3db5-120">You need to get a separate API key for each VSTS release template.</span><span class="sxs-lookup"><span data-stu-id="f3db5-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="f3db5-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span><span class="sxs-lookup"><span data-stu-id="f3db5-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="f3db5-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span><span class="sxs-lookup"><span data-stu-id="f3db5-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="f3db5-123">Open **API Access**,  **Application Insights Id**.</span><span class="sxs-lookup"><span data-stu-id="f3db5-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![In portal.azure.com, open your Application Insights resource and choose Settings.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/20.png)

4. <span data-ttu-id="f3db5-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f3db5-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="f3db5-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span><span class="sxs-lookup"><span data-stu-id="f3db5-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="f3db5-129">Paste the **Application Id** that you copied from the API Access blade.</span><span class="sxs-lookup"><span data-stu-id="f3db5-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![In Visual Studio Team Services, open Release, select a release definition, and choose Edit.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/30.png)
4. <span data-ttu-id="f3db5-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="f3db5-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="f3db5-134">Back in the Azure window, create a new API Key and take a copy of it.</span><span class="sxs-lookup"><span data-stu-id="f3db5-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![In the API Access blade in the Azure window, click Create API Key.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/40.png)

6. <span data-ttu-id="f3db5-138">Open the Configuration tab of the release template.</span><span class="sxs-lookup"><span data-stu-id="f3db5-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="f3db5-139">Create a variable definition for `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="f3db5-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="f3db5-140">Paste your API key to the ApiKey variable definition.</span><span class="sxs-lookup"><span data-stu-id="f3db5-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![In the Team Services window, select the Configuration tab and click Add Variable.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/50.png)
7. <span data-ttu-id="f3db5-143">Finally, **Save** the release definition.</span><span class="sxs-lookup"><span data-stu-id="f3db5-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="f3db5-144">View annotations</span><span class="sxs-lookup"><span data-stu-id="f3db5-144">View annotations</span></span>
<span data-ttu-id="f3db5-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f3db5-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="f3db5-146">The annotations will appear on charts in Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="f3db5-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="f3db5-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span><span class="sxs-lookup"><span data-stu-id="f3db5-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Click any release annotation marker.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="f3db5-149">Create custom annotations from PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3db5-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="f3db5-150">You can also create annotations from any process you like (without using VS Team System).</span><span class="sxs-lookup"><span data-stu-id="f3db5-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="f3db5-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="f3db5-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="f3db5-152">Get the Application ID and create an API key from the API Access blade.</span><span class="sxs-lookup"><span data-stu-id="f3db5-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="f3db5-153">Call the script like this:</span><span class="sxs-lookup"><span data-stu-id="f3db5-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="f3db5-154">It's easy to modify the script, for example to create annotations for the past.</span><span class="sxs-lookup"><span data-stu-id="f3db5-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3db5-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3db5-155">Next steps</span></span>

* [<span data-ttu-id="f3db5-156">Create work items</span><span class="sxs-lookup"><span data-stu-id="f3db5-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="f3db5-157">Automation with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3db5-157">Automation with PowerShell</span></span>](app-insights-powershell.md)







