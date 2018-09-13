---
title: Set up alerts for queries in Stream Analytics | Microsoft Docs
description: Understanding Stream Analytics Alerting
keywords: set up alerts
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 4fadc9f5d924e1a70d178760002c8c8f654d7057
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556457"
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="b8c86-104">Set up alerts for Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="b8c86-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="b8c86-105">Introduction: Monitor page</span><span class="sxs-lookup"><span data-stu-id="b8c86-105">Introduction: Monitor page</span></span>
<span data-ttu-id="b8c86-106">You can set up alerts to trigger an alert when a metric reaches a condition that you specify.</span><span class="sxs-lookup"><span data-stu-id="b8c86-106">You can set up alerts to trigger an alert when a metric reaches a condition that you specify.</span></span>

<span data-ttu-id="b8c86-107">For example, “If Output Events for the last 15 minutes is <100, send email notification to email id: xyz@company.com”.</span><span class="sxs-lookup"><span data-stu-id="b8c86-107">For example, “If Output Events for the last 15 minutes is <100, send email notification to email id: xyz@company.com”.</span></span>

<span data-ttu-id="b8c86-108">Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span><span class="sxs-lookup"><span data-stu-id="b8c86-108">Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-through-the-azure-classic-portal"></a><span data-ttu-id="b8c86-109">Set up alerts through the Azure Classic Portal</span><span class="sxs-lookup"><span data-stu-id="b8c86-109">Set up alerts through the Azure Classic Portal</span></span>
<span data-ttu-id="b8c86-110">There are two ways to set up alerts in the Azure Classic portal:</span><span class="sxs-lookup"><span data-stu-id="b8c86-110">There are two ways to set up alerts in the Azure Classic portal:</span></span>  

1. <span data-ttu-id="b8c86-111">The **Monitor** tab of your Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="b8c86-111">The **Monitor** tab of your Stream Analytics job</span></span>  
2. <span data-ttu-id="b8c86-112">The Operations Log in the Management services</span><span class="sxs-lookup"><span data-stu-id="b8c86-112">The Operations Log in the Management services</span></span>  

## <a name="set-up-alert-through-the-monitor-tab-of-the-job-in-the-portal"></a><span data-ttu-id="b8c86-113">Set up alert through the Monitor tab of the job in the portal</span><span class="sxs-lookup"><span data-stu-id="b8c86-113">Set up alert through the Monitor tab of the job in the portal</span></span>
1. <span data-ttu-id="b8c86-114">Select the metric in the monitor tab, and click the **Add Rule** button in the bottom of the dashboard, and setup your rules.</span><span class="sxs-lookup"><span data-stu-id="b8c86-114">Select the metric in the monitor tab, and click the **Add Rule** button in the bottom of the dashboard, and setup your rules.</span></span>  
   
   ![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/01-stream-analytics-set-up-alerts.png)  
2. <span data-ttu-id="b8c86-116">Define the name and description of the Alert</span><span class="sxs-lookup"><span data-stu-id="b8c86-116">Define the name and description of the Alert</span></span>  
   
   ![Create Rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/02-stream-analytics-set-up-alerts.png)  
3. <span data-ttu-id="b8c86-118">Enter the thresholds, alert evaluation window and the actions for the alert</span><span class="sxs-lookup"><span data-stu-id="b8c86-118">Enter the thresholds, alert evaluation window and the actions for the alert</span></span>  
   
   ![Define Conditions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/03-stream-analytics-set-up-alerts.png)  

## <a name="set-up-alerts-through-the-operations-logs"></a><span data-ttu-id="b8c86-120">Set up alerts through the Operations logs</span><span class="sxs-lookup"><span data-stu-id="b8c86-120">Set up alerts through the Operations logs</span></span>
1. <span data-ttu-id="b8c86-121">Go to the **Alerts** tab in Management Services in the [Azure Classic Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b8c86-121">Go to the **Alerts** tab in Management Services in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span>  
2. <span data-ttu-id="b8c86-122">Click **Add Rule**</span><span class="sxs-lookup"><span data-stu-id="b8c86-122">Click **Add Rule**</span></span>  
   
   ![Criteria](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/04-stream-analytics-set-up-alerts.png)  
3. <span data-ttu-id="b8c86-124">Define the name and description of the Alert.</span><span class="sxs-lookup"><span data-stu-id="b8c86-124">Define the name and description of the Alert.</span></span> <span data-ttu-id="b8c86-125">Select ‘Stream Analytics’ as Service Type, and the job name as the Service Name.</span><span class="sxs-lookup"><span data-stu-id="b8c86-125">Select ‘Stream Analytics’ as Service Type, and the job name as the Service Name.</span></span>  
   
   ![Define Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/05-stream-analytics-set-up-alerts.png)  

## <a name="set-up-alerts-in-the-azure-portal"></a><span data-ttu-id="b8c86-127">Set up alerts in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b8c86-127">Set up alerts in the Azure portal</span></span>
<span data-ttu-id="b8c86-128">In the Azure portal, browse to the Stream Analytics job you are interested in alerting on and click the **Monitoring** section.</span><span class="sxs-lookup"><span data-stu-id="b8c86-128">In the Azure portal, browse to the Stream Analytics job you are interested in alerting on and click the **Monitoring** section.</span></span>  <span data-ttu-id="b8c86-129">In the **Metric** blade that opens, click the **Add alert** command.</span><span class="sxs-lookup"><span data-stu-id="b8c86-129">In the **Metric** blade that opens, click the **Add alert** command.</span></span>

  ![Azure portal setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

<span data-ttu-id="b8c86-131">You can name your alert rule, and choose a description that will show up in the notification email.</span><span class="sxs-lookup"><span data-stu-id="b8c86-131">You can name your alert rule, and choose a description that will show up in the notification email.</span></span>

<span data-ttu-id="b8c86-132">When you select Metrics you'll choose a condition and threshold Value for the metric.</span><span class="sxs-lookup"><span data-stu-id="b8c86-132">When you select Metrics you'll choose a condition and threshold Value for the metric.</span></span>

  ![Azure portal select metric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-set-up-alerts/07-stream-analytics-set-up-alerts.png)  

<span data-ttu-id="b8c86-134">For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="b8c86-134">For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  

## <a name="get-help"></a><span data-ttu-id="b8c86-135">Get help</span><span class="sxs-lookup"><span data-stu-id="b8c86-135">Get help</span></span>
<span data-ttu-id="b8c86-136">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b8c86-136">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8c86-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8c86-137">Next steps</span></span>
* [<span data-ttu-id="b8c86-138">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b8c86-138">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b8c86-139">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b8c86-139">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="b8c86-140">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="b8c86-140">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b8c86-141">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="b8c86-141">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b8c86-142">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="b8c86-142">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)








