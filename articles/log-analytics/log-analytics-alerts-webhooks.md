---
title: Webhook alert action sample in OMS Log Analytics | Microsoft Docs
description: One of the actions you can run in response to a Log Analytics alert is a *webhook*, which allows you to invoke an external process through a single HTTP request. This article walks through an example of creating a webhook action in a Log Analytics alert using Slack.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: a282d14668ca57fb4486f6916e7a81d60c9e5066
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661106"
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="89e6b-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span><span class="sxs-lookup"><span data-stu-id="89e6b-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="89e6b-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span><span class="sxs-lookup"><span data-stu-id="89e6b-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="89e6b-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="89e6b-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="89e6b-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span><span class="sxs-lookup"><span data-stu-id="89e6b-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="89e6b-108">You must have a Slack account to complete this sample.</span><span class="sxs-lookup"><span data-stu-id="89e6b-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="89e6b-109">You can sign up for a free account at [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="89e6b-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="89e6b-110">Step 1 - Enable webhooks in Slack</span><span class="sxs-lookup"><span data-stu-id="89e6b-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="89e6b-111">Sign in to Slack at [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="89e6b-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="89e6b-112">Select a channel in the **Channels** section in the left pane.</span><span class="sxs-lookup"><span data-stu-id="89e6b-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="89e6b-113">This is the channel that the message will be sent to.</span><span class="sxs-lookup"><span data-stu-id="89e6b-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="89e6b-114">You can select one of the default channels such as **general** or **random**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="89e6b-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack channels](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="89e6b-117">Click **Add an app or custom integration** to open the App Directory.</span><span class="sxs-lookup"><span data-stu-id="89e6b-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="89e6b-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack channels](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="89e6b-120">Click **Install** next to your team name.</span><span class="sxs-lookup"><span data-stu-id="89e6b-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="89e6b-121">Click **Add Configuration**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="89e6b-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="89e6b-123">Copy the **Webhook URL**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="89e6b-124">You'll be pasting this into the Alert configuration.</span><span class="sxs-lookup"><span data-stu-id="89e6b-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Slack channels](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="89e6b-126">Step 2 - Create alert rule in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="89e6b-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="89e6b-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span><span class="sxs-lookup"><span data-stu-id="89e6b-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="89e6b-128">Query: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="89e6b-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="89e6b-129">Check for this alert every: 5 minutes</span><span class="sxs-lookup"><span data-stu-id="89e6b-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="89e6b-130">The number of results is: greater than 10</span><span class="sxs-lookup"><span data-stu-id="89e6b-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="89e6b-131">Over this time window: 60 minutes</span><span class="sxs-lookup"><span data-stu-id="89e6b-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="89e6b-132">Select **Yes** for **Webhook** and **No** for the other actions.</span><span class="sxs-lookup"><span data-stu-id="89e6b-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="89e6b-133">Paste the Slack URL into the **Webhook URL** field.</span><span class="sxs-lookup"><span data-stu-id="89e6b-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="89e6b-134">Select the option to **include a custom JSON payload**.</span><span class="sxs-lookup"><span data-stu-id="89e6b-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="89e6b-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span><span class="sxs-lookup"><span data-stu-id="89e6b-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="89e6b-136">This is the text that it will display in the message it creates.</span><span class="sxs-lookup"><span data-stu-id="89e6b-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="89e6b-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span><span class="sxs-lookup"><span data-stu-id="89e6b-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![example JSON payload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="89e6b-139">Click **Save** to save the alert rule.</span><span class="sxs-lookup"><span data-stu-id="89e6b-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="89e6b-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span><span class="sxs-lookup"><span data-stu-id="89e6b-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![example webhook in Slack](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="89e6b-142">Advanced webhook payload for Slack</span><span class="sxs-lookup"><span data-stu-id="89e6b-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="89e6b-143">You can extensively customize inbound messages with Slack.</span><span class="sxs-lookup"><span data-stu-id="89e6b-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="89e6b-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span><span class="sxs-lookup"><span data-stu-id="89e6b-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="89e6b-145">Following is a more complex payload to create a rich message with formatting:</span><span class="sxs-lookup"><span data-stu-id="89e6b-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="89e6b-146">This would generate a message in Slack similar to the following.</span><span class="sxs-lookup"><span data-stu-id="89e6b-146">This would generate a message in Slack similar to the following.</span></span>

![example message in Slack](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="89e6b-148">Summary</span><span class="sxs-lookup"><span data-stu-id="89e6b-148">Summary</span></span>
<span data-ttu-id="89e6b-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span><span class="sxs-lookup"><span data-stu-id="89e6b-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="89e6b-150">This is only one example of an action that you can create in response to an alert.</span><span class="sxs-lookup"><span data-stu-id="89e6b-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="89e6b-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span><span class="sxs-lookup"><span data-stu-id="89e6b-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="89e6b-152">Next Steps</span><span class="sxs-lookup"><span data-stu-id="89e6b-152">Next Steps</span></span>
* <span data-ttu-id="89e6b-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span><span class="sxs-lookup"><span data-stu-id="89e6b-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>








