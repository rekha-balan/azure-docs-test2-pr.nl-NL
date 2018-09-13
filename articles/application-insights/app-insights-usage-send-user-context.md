---
title: Send user context IDs to enable usage experiences in Azure Application Insights | Microsoft Docs
description: Track how users move through your service by assigning each of them a unique, persistent ID string in Application Insights.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: conceptual
ms.date: 08/02/2017
ms.reviewer: abgreg
ms.author: mbullwin
ms.openlocfilehash: 14322162d3f78f0cb90ecaf077d1d85f7cbba581
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866698"
---
#  <a name="send-user-context-ids-to-enable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="edddf-103">Send user context IDs to enable usage experiences in Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="edddf-103">Send user context IDs to enable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="edddf-104">Tracking users</span><span class="sxs-lookup"><span data-stu-id="edddf-104">Tracking users</span></span>

<span data-ttu-id="edddf-105">Application Insights enables you to monitor and track your users through a set of product usage tools:</span><span class="sxs-lookup"><span data-stu-id="edddf-105">Application Insights enables you to monitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="edddf-106">Users, Sessions, Events</span><span class="sxs-lookup"><span data-stu-id="edddf-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="edddf-107">Funnels</span><span class="sxs-lookup"><span data-stu-id="edddf-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="edddf-108">Retention</span><span class="sxs-lookup"><span data-stu-id="edddf-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="edddf-109">Cohorts</span><span class="sxs-lookup"><span data-stu-id="edddf-109">Cohorts</span></span>
* [<span data-ttu-id="edddf-110">Workbooks</span><span class="sxs-lookup"><span data-stu-id="edddf-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="edddf-111">In order to track what a user does over time, Application Insights needs an ID for each user or session.</span><span class="sxs-lookup"><span data-stu-id="edddf-111">In order to track what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="edddf-112">Include the following IDs in every custom event or page view.</span><span class="sxs-lookup"><span data-stu-id="edddf-112">Include the following IDs in every custom event or page view.</span></span>
- <span data-ttu-id="edddf-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span><span class="sxs-lookup"><span data-stu-id="edddf-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="edddf-114">Sessions: Include session ID.</span><span class="sxs-lookup"><span data-stu-id="edddf-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="edddf-115">If your app is integrated with the [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span><span class="sxs-lookup"><span data-stu-id="edddf-115">If your app is integrated with the [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="edddf-116">Choosing user IDs</span><span class="sxs-lookup"><span data-stu-id="edddf-116">Choosing user IDs</span></span>

<span data-ttu-id="edddf-117">User IDs should persist across user sessions to track how users behave over time.</span><span class="sxs-lookup"><span data-stu-id="edddf-117">User IDs should persist across user sessions to track how users behave over time.</span></span> <span data-ttu-id="edddf-118">There are various approaches for persisting the ID.</span><span class="sxs-lookup"><span data-stu-id="edddf-118">There are various approaches for persisting the ID.</span></span>
- <span data-ttu-id="edddf-119">A definition of a user that you already have in your service.</span><span class="sxs-lookup"><span data-stu-id="edddf-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="edddf-120">If the service has access to a browser, it can pass the browser a cookie with an ID in it.</span><span class="sxs-lookup"><span data-stu-id="edddf-120">If the service has access to a browser, it can pass the browser a cookie with an ID in it.</span></span> <span data-ttu-id="edddf-121">The ID will persist for as long as the cookie remains in the user's browser.</span><span class="sxs-lookup"><span data-stu-id="edddf-121">The ID will persist for as long as the cookie remains in the user's browser.</span></span>
- <span data-ttu-id="edddf-122">If necessary, you can use a new ID each session, but the results about users will be limited.</span><span class="sxs-lookup"><span data-stu-id="edddf-122">If necessary, you can use a new ID each session, but the results about users will be limited.</span></span> <span data-ttu-id="edddf-123">For example, you won't be able to see how a user's behavior changes over time.</span><span class="sxs-lookup"><span data-stu-id="edddf-123">For example, you won't be able to see how a user's behavior changes over time.</span></span>

<span data-ttu-id="edddf-124">The ID should be a Guid or another string complex enough to identify each user uniquely.</span><span class="sxs-lookup"><span data-stu-id="edddf-124">The ID should be a Guid or another string complex enough to identify each user uniquely.</span></span> <span data-ttu-id="edddf-125">For example, it could be a long random number.</span><span class="sxs-lookup"><span data-stu-id="edddf-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="edddf-126">If the ID contains personally identifying information about the user, it is not an appropriate value to send to Application Insights as a user ID.</span><span class="sxs-lookup"><span data-stu-id="edddf-126">If the ID contains personally identifying information about the user, it is not an appropriate value to send to Application Insights as a user ID.</span></span> <span data-ttu-id="edddf-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill the user ID requirement for usage scenarios.</span><span class="sxs-lookup"><span data-stu-id="edddf-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill the user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-setting-the-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="edddf-128">ASP.NET apps: Setting the user context in an ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="edddf-128">ASP.NET apps: Setting the user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="edddf-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set the Context.User.Id and the Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="edddf-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set the Context.User.Id and the Context.Session.Id.</span></span>

<span data-ttu-id="edddf-130">This example sets the user ID to an identifier that expires after the session.</span><span class="sxs-lookup"><span data-stu-id="edddf-130">This example sets the user ID to an identifier that expires after the session.</span></span> <span data-ttu-id="edddf-131">If possible, use a user ID that persists across sessions.</span><span class="sxs-lookup"><span data-stu-id="edddf-131">If possible, use a user ID that persists across sessions.</span></span>

```csharp

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets the user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on the HttpContext Session.
            // Set the user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set the user id on the Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set the session id on the Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="edddf-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="edddf-132">Next steps</span></span>
- <span data-ttu-id="edddf-133">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="edddf-133">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="edddf-134">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span><span class="sxs-lookup"><span data-stu-id="edddf-134">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    * [<span data-ttu-id="edddf-135">Usage overview</span><span class="sxs-lookup"><span data-stu-id="edddf-135">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="edddf-136">Users, Sessions, and Events</span><span class="sxs-lookup"><span data-stu-id="edddf-136">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="edddf-137">Funnels</span><span class="sxs-lookup"><span data-stu-id="edddf-137">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="edddf-138">Retention</span><span class="sxs-lookup"><span data-stu-id="edddf-138">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="edddf-139">Workbooks</span><span class="sxs-lookup"><span data-stu-id="edddf-139">Workbooks</span></span>](app-insights-usage-workbooks.md)
