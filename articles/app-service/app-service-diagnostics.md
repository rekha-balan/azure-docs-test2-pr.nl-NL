---
title: Azure App Service diagnostics overview | Microsoft Docs
description: Learn how you can troubleshoot issues with your web app with App Service diagnostics.
keywords: app service, azure app service, diagnostics, support, web app, troubleshooting, self-help
services: app-service
documentationcenter: ''
author: jen7714
manager: cfowler
editor: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/10/2017
ms.author: jennile
ms.openlocfilehash: 7ad205c75a02b496abe2cb910c7eb459cdb16c97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967967"
---
# <a name="azure-app-service-diagnostics-overview"></a><span data-ttu-id="698eb-104">Azure App Service diagnostics overview</span><span class="sxs-lookup"><span data-stu-id="698eb-104">Azure App Service diagnostics overview</span></span> 

<span data-ttu-id="698eb-105">When you’re running a web application, you want to be prepared for any issues that may arise, from 500 errors to your users telling you that your site is down.</span><span class="sxs-lookup"><span data-stu-id="698eb-105">When you’re running a web application, you want to be prepared for any issues that may arise, from 500 errors to your users telling you that your site is down.</span></span> <span data-ttu-id="698eb-106">App Service diagnostics is an intelligent and interactive experience to help you troubleshoot your web app with no configuration required.</span><span class="sxs-lookup"><span data-stu-id="698eb-106">App Service diagnostics is an intelligent and interactive experience to help you troubleshoot your web app with no configuration required.</span></span> <span data-ttu-id="698eb-107">When you do run into issues with your web app, App Service diagnostics will point out what’s wrong to guide you to the right information to more easily and quickly troubleshoot and resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="698eb-107">When you do run into issues with your web app, App Service diagnostics will point out what’s wrong to guide you to the right information to more easily and quickly troubleshoot and resolve the issue.</span></span> 
 
<span data-ttu-id="698eb-108">Although this experience is most helpful when you’re having issues with your web app within the last 24 hours, all the diagnostic graphs will be available for you to analyze at all times.</span><span class="sxs-lookup"><span data-stu-id="698eb-108">Although this experience is most helpful when you’re having issues with your web app within the last 24 hours, all the diagnostic graphs will be available for you to analyze at all times.</span></span> <span data-ttu-id="698eb-109">Additional troubleshooting tools and links to helpful documentation and forums are located on the right-hand column.</span><span class="sxs-lookup"><span data-stu-id="698eb-109">Additional troubleshooting tools and links to helpful documentation and forums are located on the right-hand column.</span></span>

<span data-ttu-id="698eb-110">App Service diagnostics works for not only your app on Windows, but also apps on [Linux/containers](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro), [App Service Environment](https://docs.microsoft.com/azure/app-service/environment/intro), and [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="698eb-110">App Service diagnostics works for not only your app on Windows, but also apps on [Linux/containers](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro), [App Service Environment](https://docs.microsoft.com/azure/app-service/environment/intro), and [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span> 

## <a name="open-app-service-diagnostics"></a><span data-ttu-id="698eb-111">Open App Service diagnostics</span><span class="sxs-lookup"><span data-stu-id="698eb-111">Open App Service diagnostics</span></span>

<span data-ttu-id="698eb-112">To access App Service diagnostics, navigate to your App Service app or App Service Environment in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="698eb-112">To access App Service diagnostics, navigate to your App Service app or App Service Environment in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="698eb-113">In the left navigation, click on **Diagnose and solve problems**.</span><span class="sxs-lookup"><span data-stu-id="698eb-113">In the left navigation, click on **Diagnose and solve problems**.</span></span> 

<span data-ttu-id="698eb-114">For Azure Functions, navigate to your function app, and in the top navigation, click on **Platform features** and select **Diagnose and solve problems** from the **Monitoring** section.</span><span class="sxs-lookup"><span data-stu-id="698eb-114">For Azure Functions, navigate to your function app, and in the top navigation, click on **Platform features** and select **Diagnose and solve problems** from the **Monitoring** section.</span></span> 

![Homepage](./media/app-service-diagnostics/Homepage1.png)

## <a name="health-checkup"></a><span data-ttu-id="698eb-116">Health checkup</span><span class="sxs-lookup"><span data-stu-id="698eb-116">Health checkup</span></span>

<span data-ttu-id="698eb-117">If you don't know what’s wrong with your web app or don’t know where to start troubleshooting your issues, the health checkup is a good place to start.</span><span class="sxs-lookup"><span data-stu-id="698eb-117">If you don't know what’s wrong with your web app or don’t know where to start troubleshooting your issues, the health checkup is a good place to start.</span></span> <span data-ttu-id="698eb-118">The health checkup will analyze your web applications to give you a quick, interactive overview that points out what’s healthy and what’s wrong, telling you where to look to investigate the issue.</span><span class="sxs-lookup"><span data-stu-id="698eb-118">The health checkup will analyze your web applications to give you a quick, interactive overview that points out what’s healthy and what’s wrong, telling you where to look to investigate the issue.</span></span> <span data-ttu-id="698eb-119">Its intelligent and interactive interface provides you with guidance through the troubleshooting process.</span><span class="sxs-lookup"><span data-stu-id="698eb-119">Its intelligent and interactive interface provides you with guidance through the troubleshooting process.</span></span>  

![Health checkup](./media/app-service-diagnostics/HealthCheckup2.png)

<span data-ttu-id="698eb-121">If an issue is detected with a specific problem category within the last 24 hours, you can view the full diagnostic report and App Service diagnostics may prompt you to view more troubleshooting advice and next steps for a more guided experience.</span><span class="sxs-lookup"><span data-stu-id="698eb-121">If an issue is detected with a specific problem category within the last 24 hours, you can view the full diagnostic report and App Service diagnostics may prompt you to view more troubleshooting advice and next steps for a more guided experience.</span></span>

![Troubleshooting and next steps](./media/app-service-diagnostics/Troubleshooting3.png)

## <a name="tile-shortcuts"></a><span data-ttu-id="698eb-123">Tile shortcuts</span><span class="sxs-lookup"><span data-stu-id="698eb-123">Tile shortcuts</span></span>

<span data-ttu-id="698eb-124">If you know exactly what kind of troubleshooting information you’re looking for, the tile shortcuts will take you directly to the full diagnostic report of the problem category that you’re interested in.</span><span class="sxs-lookup"><span data-stu-id="698eb-124">If you know exactly what kind of troubleshooting information you’re looking for, the tile shortcuts will take you directly to the full diagnostic report of the problem category that you’re interested in.</span></span> <span data-ttu-id="698eb-125">Compared to the health checkup, the tile shortcuts are the more direct, but less guided way of accessing your diagnostic metrics.</span><span class="sxs-lookup"><span data-stu-id="698eb-125">Compared to the health checkup, the tile shortcuts are the more direct, but less guided way of accessing your diagnostic metrics.</span></span> <span data-ttu-id="698eb-126">As a part of tile shortcuts, this is also where you will find **Diagnostic Tools**  which are more advanced tools that will help you investigate issues related to application code issues, slowness, connection strings, and more.</span><span class="sxs-lookup"><span data-stu-id="698eb-126">As a part of tile shortcuts, this is also where you will find **Diagnostic Tools**  which are more advanced tools that will help you investigate issues related to application code issues, slowness, connection strings, and more.</span></span> 

![Tile shortcuts](./media/app-service-diagnostics/TileShortcuts4.png)

## <a name="diagnostic-report"></a><span data-ttu-id="698eb-128">Diagnostic report</span><span class="sxs-lookup"><span data-stu-id="698eb-128">Diagnostic report</span></span>

<span data-ttu-id="698eb-129">Whether you want more information after running a [health checkup](#health-checkup) or you clicked on one of the [tile shortcuts](#tile-shortcuts), the full diagnostic report will show you relevant graphed metrics from the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="698eb-129">Whether you want more information after running a [health checkup](#health-checkup) or you clicked on one of the [tile shortcuts](#tile-shortcuts), the full diagnostic report will show you relevant graphed metrics from the last 24 hours.</span></span> <span data-ttu-id="698eb-130">If your app experiences any downtime, it's represented by an orange bar underneath the timeline.</span><span class="sxs-lookup"><span data-stu-id="698eb-130">If your app experiences any downtime, it's represented by an orange bar underneath the timeline.</span></span> <span data-ttu-id="698eb-131">You can select one of the orange bars to select the downtime to see observations about that downtime and the suggested troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="698eb-131">You can select one of the orange bars to select the downtime to see observations about that downtime and the suggested troubleshooting steps.</span></span> 

![Diagnostic report](./media/app-service-diagnostics/DiagnosticReport5.png)


## <a name="investigating-application-code-issues"></a><span data-ttu-id="698eb-133">Investigating application code issues</span><span class="sxs-lookup"><span data-stu-id="698eb-133">Investigating application code issues</span></span>

<span data-ttu-id="698eb-134">Because many app issues are related to issues in your application code, App Service diagnostics integrates with [Application Insights](https://azure.microsoft.com/services/application-insights/) to highlight exceptions and dependency issues to correlate with the selected downtime.</span><span class="sxs-lookup"><span data-stu-id="698eb-134">Because many app issues are related to issues in your application code, App Service diagnostics integrates with [Application Insights](https://azure.microsoft.com/services/application-insights/) to highlight exceptions and dependency issues to correlate with the selected downtime.</span></span> <span data-ttu-id="698eb-135">Application Insights does have to be enabled separately.</span><span class="sxs-lookup"><span data-stu-id="698eb-135">Application Insights does have to be enabled separately.</span></span> 

<span data-ttu-id="698eb-136">To view Application Insights exceptions and dependencies, select the **Web App Down** or **Web App Slow** tile shortcuts.</span><span class="sxs-lookup"><span data-stu-id="698eb-136">To view Application Insights exceptions and dependencies, select the **Web App Down** or **Web App Slow** tile shortcuts.</span></span> 

![Application insights](./media/app-service-diagnostics/AppInsights6.png)

