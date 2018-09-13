---
title: Azure CDN real-time alerts | Microsoft Docs
description: Real-time alerts in Microsoft Azure CDN. Real-time alerts provide notifications about the performance of the endpoints in your CDN profile.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 99da40ba7209b022e858dc520c05a24cb8e88c94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669362"
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="44f02-104">Real-time alerts in Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="44f02-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="44f02-105">Overview</span><span class="sxs-lookup"><span data-stu-id="44f02-105">Overview</span></span>
<span data-ttu-id="44f02-106">This document explains real-time alerts in Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="44f02-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="44f02-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="44f02-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="44f02-108">You can set up email or HTTP alerts based on:</span><span class="sxs-lookup"><span data-stu-id="44f02-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="44f02-109">Bandwidth</span><span class="sxs-lookup"><span data-stu-id="44f02-109">Bandwidth</span></span>
* <span data-ttu-id="44f02-110">Status Codes</span><span class="sxs-lookup"><span data-stu-id="44f02-110">Status Codes</span></span>
* <span data-ttu-id="44f02-111">Cache Statuses</span><span class="sxs-lookup"><span data-stu-id="44f02-111">Cache Statuses</span></span>
* <span data-ttu-id="44f02-112">Connections</span><span class="sxs-lookup"><span data-stu-id="44f02-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="44f02-113">Creating a real-time alert</span><span class="sxs-lookup"><span data-stu-id="44f02-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="44f02-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="44f02-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN profile blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="44f02-116">From the CDN profile blade, click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="44f02-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="44f02-118">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="44f02-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="44f02-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span><span class="sxs-lookup"><span data-stu-id="44f02-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="44f02-120">Click on **Real-Time Alerts**.</span><span class="sxs-lookup"><span data-stu-id="44f02-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN management portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="44f02-122">The list of existing alert configurations (if any) is displayed.</span><span class="sxs-lookup"><span data-stu-id="44f02-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="44f02-123">Click the **Add Alert** button.</span><span class="sxs-lookup"><span data-stu-id="44f02-123">Click the **Add Alert** button.</span></span>
   
    ![Add Alert button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="44f02-125">A form for creating a new alert is displayed.</span><span class="sxs-lookup"><span data-stu-id="44f02-125">A form for creating a new alert is displayed.</span></span>
   
    ![New Alert form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="44f02-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span><span class="sxs-lookup"><span data-stu-id="44f02-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="44f02-128">Enter a descriptive name for your alert in the **Name** field.</span><span class="sxs-lookup"><span data-stu-id="44f02-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="44f02-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="44f02-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Media Type with HTTP Large Object selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="44f02-131">You must select **HTTP Large Object** as the **Media Type**.</span><span class="sxs-lookup"><span data-stu-id="44f02-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="44f02-132">The other choices are not used by **Azure CDN from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="44f02-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="44f02-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span><span class="sxs-lookup"><span data-stu-id="44f02-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="44f02-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span><span class="sxs-lookup"><span data-stu-id="44f02-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="44f02-135">For **Metric**, select the type of condition you want monitored.</span><span class="sxs-lookup"><span data-stu-id="44f02-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="44f02-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span><span class="sxs-lookup"><span data-stu-id="44f02-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="44f02-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span><span class="sxs-lookup"><span data-stu-id="44f02-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="44f02-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="44f02-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="44f02-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span><span class="sxs-lookup"><span data-stu-id="44f02-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="44f02-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span><span class="sxs-lookup"><span data-stu-id="44f02-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="44f02-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span><span class="sxs-lookup"><span data-stu-id="44f02-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Real-time alert sample expression](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="44f02-143">For **Interval**, enter how frequently you would like the expression evaluated.</span><span class="sxs-lookup"><span data-stu-id="44f02-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="44f02-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span><span class="sxs-lookup"><span data-stu-id="44f02-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="44f02-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span><span class="sxs-lookup"><span data-stu-id="44f02-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="44f02-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span><span class="sxs-lookup"><span data-stu-id="44f02-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="44f02-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span><span class="sxs-lookup"><span data-stu-id="44f02-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="44f02-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span><span class="sxs-lookup"><span data-stu-id="44f02-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="44f02-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span><span class="sxs-lookup"><span data-stu-id="44f02-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="44f02-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span><span class="sxs-lookup"><span data-stu-id="44f02-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="44f02-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span><span class="sxs-lookup"><span data-stu-id="44f02-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Notify by Email form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="44f02-153">In the **To** field, enter the email address you where you want notifications sent.</span><span class="sxs-lookup"><span data-stu-id="44f02-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="44f02-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span><span class="sxs-lookup"><span data-stu-id="44f02-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="44f02-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span><span class="sxs-lookup"><span data-stu-id="44f02-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="44f02-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span><span class="sxs-lookup"><span data-stu-id="44f02-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Notify by HTTP Post form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="44f02-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span><span class="sxs-lookup"><span data-stu-id="44f02-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="44f02-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span><span class="sxs-lookup"><span data-stu-id="44f02-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="44f02-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span><span class="sxs-lookup"><span data-stu-id="44f02-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="44f02-161">**Headers** and **Body** default to an XML payload similar to the below example.</span><span class="sxs-lookup"><span data-stu-id="44f02-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="44f02-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span><span class="sxs-lookup"><span data-stu-id="44f02-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="44f02-163">Click the **Save** button to save your alert configuration.</span><span class="sxs-lookup"><span data-stu-id="44f02-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="44f02-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span><span class="sxs-lookup"><span data-stu-id="44f02-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44f02-165">Next Steps</span><span class="sxs-lookup"><span data-stu-id="44f02-165">Next Steps</span></span>
* <span data-ttu-id="44f02-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="44f02-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="44f02-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="44f02-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="44f02-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="44f02-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>










