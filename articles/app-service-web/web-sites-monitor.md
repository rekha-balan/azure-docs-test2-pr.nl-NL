---
title: Monitor Apps in Azure App Service | Microsoft Docs
description: Learn how to monitor Apps in Azure App Service by using the Azure Portal.
services: app-service
documentationcenter: ''
author: btardif
manager: erikre
editor: ''
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 9bfbbfe4263de0d9f181efdfde59bc5cc59ba5f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669059"
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="91563-103">How to: Monitor Apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="91563-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="91563-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91563-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="91563-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span><span class="sxs-lookup"><span data-stu-id="91563-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="91563-106">Understanding Quotas and Metrics</span><span class="sxs-lookup"><span data-stu-id="91563-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="91563-107">Quotas</span><span class="sxs-lookup"><span data-stu-id="91563-107">Quotas</span></span>
<span data-ttu-id="91563-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span><span class="sxs-lookup"><span data-stu-id="91563-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="91563-109">The limits are defined by the **App Service plan** associated with the app.</span><span class="sxs-lookup"><span data-stu-id="91563-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="91563-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span><span class="sxs-lookup"><span data-stu-id="91563-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="91563-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span><span class="sxs-lookup"><span data-stu-id="91563-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="91563-112">**Quotas** for **Free** or **Shared** apps are:</span><span class="sxs-lookup"><span data-stu-id="91563-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="91563-113">**CPU(Short)**</span><span class="sxs-lookup"><span data-stu-id="91563-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="91563-114">Amount of CPU allowed for this application in a 3-minute interval.</span><span class="sxs-lookup"><span data-stu-id="91563-114">Amount of CPU allowed for this application in a 3-minute interval.</span></span> <span data-ttu-id="91563-115">This quota re-sets every 3 minutes.</span><span class="sxs-lookup"><span data-stu-id="91563-115">This quota re-sets every 3 minutes.</span></span>
* <span data-ttu-id="91563-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="91563-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="91563-117">Total amount of CPU allowed for this application in a day.</span><span class="sxs-lookup"><span data-stu-id="91563-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="91563-118">This quota re-sets every 24 hours at midnight UTC.</span><span class="sxs-lookup"><span data-stu-id="91563-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="91563-119">**Memory**</span><span class="sxs-lookup"><span data-stu-id="91563-119">**Memory**</span></span>
  * <span data-ttu-id="91563-120">Total amount of memory allowed for this application.</span><span class="sxs-lookup"><span data-stu-id="91563-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="91563-121">**Bandwidth**</span><span class="sxs-lookup"><span data-stu-id="91563-121">**Bandwidth**</span></span>
  * <span data-ttu-id="91563-122">Total amount of outgoing bandwidth allowed for this application in a day.</span><span class="sxs-lookup"><span data-stu-id="91563-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="91563-123">This quota re-sets every 24 hours at midnight UTC.</span><span class="sxs-lookup"><span data-stu-id="91563-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="91563-124">**Filesystem**</span><span class="sxs-lookup"><span data-stu-id="91563-124">**Filesystem**</span></span>
  * <span data-ttu-id="91563-125">Total amount of storage allowed.</span><span class="sxs-lookup"><span data-stu-id="91563-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="91563-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span><span class="sxs-lookup"><span data-stu-id="91563-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="91563-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="91563-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="91563-128">Quota Enforcement</span><span class="sxs-lookup"><span data-stu-id="91563-128">Quota Enforcement</span></span>
<span data-ttu-id="91563-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span><span class="sxs-lookup"><span data-stu-id="91563-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="91563-130">During this time, all incoming requests will result in an **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="91563-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="91563-131">If the application **memory** quota is exceeded, then the application will be re-started.</span><span class="sxs-lookup"><span data-stu-id="91563-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="91563-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span><span class="sxs-lookup"><span data-stu-id="91563-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="91563-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span><span class="sxs-lookup"><span data-stu-id="91563-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="91563-134">Metrics</span><span class="sxs-lookup"><span data-stu-id="91563-134">Metrics</span></span>
<span data-ttu-id="91563-135">**Metrics** provide information about the app, or App Service plan's behavior.</span><span class="sxs-lookup"><span data-stu-id="91563-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="91563-136">For an **Application**, the available metrics are:</span><span class="sxs-lookup"><span data-stu-id="91563-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="91563-137">**Average Response Time**</span><span class="sxs-lookup"><span data-stu-id="91563-137">**Average Response Time**</span></span>
  * <span data-ttu-id="91563-138">The average time taken for the app to serve requests in ms.</span><span class="sxs-lookup"><span data-stu-id="91563-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="91563-139">**Average memory working set**</span><span class="sxs-lookup"><span data-stu-id="91563-139">**Average memory working set**</span></span>
  * <span data-ttu-id="91563-140">The average amount of memory in MiBs used by the app.</span><span class="sxs-lookup"><span data-stu-id="91563-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="91563-141">**CPU Time**</span><span class="sxs-lookup"><span data-stu-id="91563-141">**CPU Time**</span></span>
  * <span data-ttu-id="91563-142">The amount of CPU in seconds consumed by the app.</span><span class="sxs-lookup"><span data-stu-id="91563-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="91563-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="91563-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="91563-144">**Data In**</span><span class="sxs-lookup"><span data-stu-id="91563-144">**Data In**</span></span>
  * <span data-ttu-id="91563-145">The amount of incoming bandwidth consumed by the app in MiBs.</span><span class="sxs-lookup"><span data-stu-id="91563-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="91563-146">**Data Out**</span><span class="sxs-lookup"><span data-stu-id="91563-146">**Data Out**</span></span>
  * <span data-ttu-id="91563-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span><span class="sxs-lookup"><span data-stu-id="91563-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="91563-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="91563-148">**Http 2xx**</span></span>
  * <span data-ttu-id="91563-149">Count of requests resulting in a http status code >= 200 but < 300.</span><span class="sxs-lookup"><span data-stu-id="91563-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="91563-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="91563-150">**Http 3xx**</span></span>
  * <span data-ttu-id="91563-151">Count of requests resulting in a http status code >= 300 but < 400.</span><span class="sxs-lookup"><span data-stu-id="91563-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="91563-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="91563-152">**Http 401**</span></span>
  * <span data-ttu-id="91563-153">Count of requests resulting in HTTP 401 status code.</span><span class="sxs-lookup"><span data-stu-id="91563-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="91563-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="91563-154">**Http 403**</span></span>
  * <span data-ttu-id="91563-155">Count of requests resulting in HTTP 403 status code.</span><span class="sxs-lookup"><span data-stu-id="91563-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="91563-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="91563-156">**Http 404**</span></span>
  * <span data-ttu-id="91563-157">Count of requests resulting in HTTP 404 status code.</span><span class="sxs-lookup"><span data-stu-id="91563-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="91563-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="91563-158">**Http 406**</span></span>
  * <span data-ttu-id="91563-159">Count of requests resulting in HTTP 406 status code.</span><span class="sxs-lookup"><span data-stu-id="91563-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="91563-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="91563-160">**Http 4xx**</span></span>
  * <span data-ttu-id="91563-161">Count of requests resulting in a http status code >= 400 but < 500.</span><span class="sxs-lookup"><span data-stu-id="91563-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="91563-162">**Http Server Errors**</span><span class="sxs-lookup"><span data-stu-id="91563-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="91563-163">Count of requests resulting in a http status code >= 500 but < 600.</span><span class="sxs-lookup"><span data-stu-id="91563-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="91563-164">**Memory working set**</span><span class="sxs-lookup"><span data-stu-id="91563-164">**Memory working set**</span></span>
  * <span data-ttu-id="91563-165">Current amount of memory used by the app in MiBs.</span><span class="sxs-lookup"><span data-stu-id="91563-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="91563-166">**Requests**</span><span class="sxs-lookup"><span data-stu-id="91563-166">**Requests**</span></span>
  * <span data-ttu-id="91563-167">Total number of requests regardless of their resulting HTTP status code.</span><span class="sxs-lookup"><span data-stu-id="91563-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="91563-168">For an **App Service plan**, the available metrics are:</span><span class="sxs-lookup"><span data-stu-id="91563-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="91563-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span><span class="sxs-lookup"><span data-stu-id="91563-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="91563-170">**CPU Percentage**</span><span class="sxs-lookup"><span data-stu-id="91563-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="91563-171">The average CPU used across all instances of the plan.</span><span class="sxs-lookup"><span data-stu-id="91563-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="91563-172">**Memory Percentage**</span><span class="sxs-lookup"><span data-stu-id="91563-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="91563-173">The average memory used across all instances of the plan.</span><span class="sxs-lookup"><span data-stu-id="91563-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="91563-174">**Data In**</span><span class="sxs-lookup"><span data-stu-id="91563-174">**Data In**</span></span>
  * <span data-ttu-id="91563-175">The average incoming bandwidth used across all instances of the plan.</span><span class="sxs-lookup"><span data-stu-id="91563-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="91563-176">**Data Out**</span><span class="sxs-lookup"><span data-stu-id="91563-176">**Data Out**</span></span>
  * <span data-ttu-id="91563-177">The average outgoing bandwidth used across all instances of the plan.</span><span class="sxs-lookup"><span data-stu-id="91563-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="91563-178">**Disk Queue Length**</span><span class="sxs-lookup"><span data-stu-id="91563-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="91563-179">The average number of both read and write requests that were queued on storage.</span><span class="sxs-lookup"><span data-stu-id="91563-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="91563-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span><span class="sxs-lookup"><span data-stu-id="91563-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="91563-181">**Http Queue Length**</span><span class="sxs-lookup"><span data-stu-id="91563-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="91563-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span><span class="sxs-lookup"><span data-stu-id="91563-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="91563-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span><span class="sxs-lookup"><span data-stu-id="91563-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="91563-184">CPU time vs CPU percentage</span><span class="sxs-lookup"><span data-stu-id="91563-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="91563-185">There are 2 metrics that reflect CPU usage.</span><span class="sxs-lookup"><span data-stu-id="91563-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="91563-186">**CPU time** and **CPU percentage**</span><span class="sxs-lookup"><span data-stu-id="91563-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="91563-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span><span class="sxs-lookup"><span data-stu-id="91563-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="91563-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span><span class="sxs-lookup"><span data-stu-id="91563-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="91563-189">Metrics Granularity and Retention Policy</span><span class="sxs-lookup"><span data-stu-id="91563-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="91563-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span><span class="sxs-lookup"><span data-stu-id="91563-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="91563-191">**Minute** granularity metrics are retained for **48 hours**</span><span class="sxs-lookup"><span data-stu-id="91563-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="91563-192">**Hour** granularity metrics are retained for **30 days**</span><span class="sxs-lookup"><span data-stu-id="91563-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="91563-193">**Day** granularity metrics are retained for **90 days**</span><span class="sxs-lookup"><span data-stu-id="91563-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="91563-194">Monitoring Quotas and Metrics in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="91563-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="91563-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91563-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="91563-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span><span class="sxs-lookup"><span data-stu-id="91563-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="91563-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span><span class="sxs-lookup"><span data-stu-id="91563-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="91563-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span><span class="sxs-lookup"><span data-stu-id="91563-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="91563-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span><span class="sxs-lookup"><span data-stu-id="91563-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="91563-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span><span class="sxs-lookup"><span data-stu-id="91563-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="91563-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="91563-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="91563-202">Alerts and Autoscale</span><span class="sxs-lookup"><span data-stu-id="91563-202">Alerts and Autoscale</span></span>
<span data-ttu-id="91563-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="91563-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="91563-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span><span class="sxs-lookup"><span data-stu-id="91563-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="91563-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span><span class="sxs-lookup"><span data-stu-id="91563-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="91563-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="91563-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="91563-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="91563-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="91563-208">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="91563-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="91563-209">What's changed</span><span class="sxs-lookup"><span data-stu-id="91563-209">What's changed</span></span>
* <span data-ttu-id="91563-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="91563-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-monitor/http403.png
[quotas]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-monitor/quotas.png
[metrics]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-monitor/metrics.png



