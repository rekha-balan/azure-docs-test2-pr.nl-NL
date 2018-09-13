---
title: Advanced Configuration for Windows Universal Apps Engagement SDK
description: Advanced Configuration options for Azure Mobile Engagement with Windows Universal Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563709"
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="5a825-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="5a825-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="5a825-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span><span class="sxs-lookup"><span data-stu-id="5a825-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a825-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5a825-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="5a825-110">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="5a825-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="5a825-111">Disable automatic crash reporting</span><span class="sxs-lookup"><span data-stu-id="5a825-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="5a825-112">You can disable the automatic crash reporting feature of Engagement.</span><span class="sxs-lookup"><span data-stu-id="5a825-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="5a825-113">Then, when an unhandled exception occurs, Engagement does nothing.</span><span class="sxs-lookup"><span data-stu-id="5a825-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.
> 
> 

<span data-ttu-id="5a825-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span><span class="sxs-lookup"><span data-stu-id="5a825-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="5a825-116">From `EngagementConfiguration.xml` file</span><span class="sxs-lookup"><span data-stu-id="5a825-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="5a825-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span><span class="sxs-lookup"><span data-stu-id="5a825-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="5a825-118">From `EngagementConfiguration` object at run time</span><span class="sxs-lookup"><span data-stu-id="5a825-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="5a825-119">Set report crash to false using your EngagementConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="5a825-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="5a825-120">Disable real time reporting</span><span class="sxs-lookup"><span data-stu-id="5a825-120">Disable real time reporting</span></span>
<span data-ttu-id="5a825-121">By default, the Engagement service reports logs in real time.</span><span class="sxs-lookup"><span data-stu-id="5a825-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="5a825-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span><span class="sxs-lookup"><span data-stu-id="5a825-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="5a825-123">This is called “burst mode”.</span><span class="sxs-lookup"><span data-stu-id="5a825-123">This is called “burst mode”.</span></span>

<span data-ttu-id="5a825-124">To do so, call the method:</span><span class="sxs-lookup"><span data-stu-id="5a825-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="5a825-125">The argument is a value in **milliseconds**.</span><span class="sxs-lookup"><span data-stu-id="5a825-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="5a825-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span><span class="sxs-lookup"><span data-stu-id="5a825-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="5a825-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span><span class="sxs-lookup"><span data-stu-id="5a825-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="5a825-128">We recommend using a burst threshold no longer than 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="5a825-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="5a825-129">Saved logs are limited to 300 items.</span><span class="sxs-lookup"><span data-stu-id="5a825-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="5a825-130">If sending is too long, you can lose some logs.</span><span class="sxs-lookup"><span data-stu-id="5a825-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> The burst threshold cannot be configured to a period less than one second. If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds. This triggers the SDK to report the logs in real-time.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
