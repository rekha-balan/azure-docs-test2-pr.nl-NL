---
title: Configure metrics alerts for Azure Database for MySQL in Azure portal
description: This article describes how to configure and access metric alerts for Azure Database for MySQL from the Azure portal.
services: mysql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 3accc31f433e6db40c7d1de2b56dfbd4180b4933
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966524"
---
# <a name="use-the-azure-portal-to-set-up-alerts-on-metrics-for-azure-database-for-mysql"></a><span data-ttu-id="bc727-103">Use the Azure portal to set up alerts on metrics for Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="bc727-103">Use the Azure portal to set up alerts on metrics for Azure Database for MySQL</span></span> 

<span data-ttu-id="bc727-104">This article shows you how to set up Azure Database for MySQL alerts using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bc727-104">This article shows you how to set up Azure Database for MySQL alerts using the Azure portal.</span></span> <span data-ttu-id="bc727-105">You can receive an alert based on monitoring metrics for your Azure services.</span><span class="sxs-lookup"><span data-stu-id="bc727-105">You can receive an alert based on monitoring metrics for your Azure services.</span></span>

<span data-ttu-id="bc727-106">The alert triggers when the value of a specified metric crosses a threshold you assign.</span><span class="sxs-lookup"><span data-stu-id="bc727-106">The alert triggers when the value of a specified metric crosses a threshold you assign.</span></span> <span data-ttu-id="bc727-107">The alert triggers both when the condition is first met, and then afterwards when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="bc727-107">The alert triggers both when the condition is first met, and then afterwards when that condition is no longer being met.</span></span> 

<span data-ttu-id="bc727-108">You can configure an alert to do the following actions when it triggers:</span><span class="sxs-lookup"><span data-stu-id="bc727-108">You can configure an alert to do the following actions when it triggers:</span></span>
* <span data-ttu-id="bc727-109">Send email notifications to the service administrator and co-administrators</span><span class="sxs-lookup"><span data-stu-id="bc727-109">Send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="bc727-110">Send email to additional emails that you specify.</span><span class="sxs-lookup"><span data-stu-id="bc727-110">Send email to additional emails that you specify.</span></span>
* <span data-ttu-id="bc727-111">Call a webhook</span><span class="sxs-lookup"><span data-stu-id="bc727-111">Call a webhook</span></span>

<span data-ttu-id="bc727-112">You can configure and get information about alert rules using:</span><span class="sxs-lookup"><span data-stu-id="bc727-112">You can configure and get information about alert rules using:</span></span>
* [<span data-ttu-id="bc727-113">Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc727-113">Azure portal</span></span>](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [<span data-ttu-id="bc727-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc727-114">PowerShell</span></span>](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [<span data-ttu-id="bc727-115">Command-line interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="bc727-115">Command-line interface (CLI)</span></span>](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [<span data-ttu-id="bc727-116">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="bc727-116">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-from-the-azure-portal"></a><span data-ttu-id="bc727-117">Create an alert rule on a metric from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc727-117">Create an alert rule on a metric from the Azure portal</span></span>
1. <span data-ttu-id="bc727-118">In the [Azure portal](https://portal.azure.com/), select the Azure Database for MySQL server you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="bc727-118">In the [Azure portal](https://portal.azure.com/), select the Azure Database for MySQL server you want to monitor.</span></span>

2. <span data-ttu-id="bc727-119">Under the **Monitoring** section of the sidebar, select **Alert rules** as shown:</span><span class="sxs-lookup"><span data-stu-id="bc727-119">Under the **Monitoring** section of the sidebar, select **Alert rules** as shown:</span></span>

   ![Select Alert Rules](./media/howto-alert-on-metric/1-alert-rules.png)

3. <span data-ttu-id="bc727-121">Select **Add metric alert** (+ icon).</span><span class="sxs-lookup"><span data-stu-id="bc727-121">Select **Add metric alert** (+ icon).</span></span> 

4. <span data-ttu-id="bc727-122">The **Add rule** page opens as shown below.</span><span class="sxs-lookup"><span data-stu-id="bc727-122">The **Add rule** page opens as shown below.</span></span>  <span data-ttu-id="bc727-123">Fill in the required information:</span><span class="sxs-lookup"><span data-stu-id="bc727-123">Fill in the required information:</span></span>

   ![Add metric alert form](./media/howto-alert-on-metric/2-add-rule-form.png)

   | <span data-ttu-id="bc727-125">Setting</span><span class="sxs-lookup"><span data-stu-id="bc727-125">Setting</span></span> | <span data-ttu-id="bc727-126">Description</span><span class="sxs-lookup"><span data-stu-id="bc727-126">Description</span></span>  |
   |---------|---------|
   | <span data-ttu-id="bc727-127">Name</span><span class="sxs-lookup"><span data-stu-id="bc727-127">Name</span></span> | <span data-ttu-id="bc727-128">Provide a name for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="bc727-128">Provide a name for the alert rule.</span></span> <span data-ttu-id="bc727-129">This value is sent in the alert notification email.</span><span class="sxs-lookup"><span data-stu-id="bc727-129">This value is sent in the alert notification email.</span></span> |
   | <span data-ttu-id="bc727-130">Description</span><span class="sxs-lookup"><span data-stu-id="bc727-130">Description</span></span> | <span data-ttu-id="bc727-131">Provide a short description of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="bc727-131">Provide a short description of the alert rule.</span></span> <span data-ttu-id="bc727-132">This value is sent in the alert notification email.</span><span class="sxs-lookup"><span data-stu-id="bc727-132">This value is sent in the alert notification email.</span></span> |
   | <span data-ttu-id="bc727-133">Alert on</span><span class="sxs-lookup"><span data-stu-id="bc727-133">Alert on</span></span> | <span data-ttu-id="bc727-134">Choose **Metrics** for this kind of alert.</span><span class="sxs-lookup"><span data-stu-id="bc727-134">Choose **Metrics** for this kind of alert.</span></span> |
   | <span data-ttu-id="bc727-135">Subscription</span><span class="sxs-lookup"><span data-stu-id="bc727-135">Subscription</span></span> | <span data-ttu-id="bc727-136">This field is prepopulated with the subscription that hosts your Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="bc727-136">This field is prepopulated with the subscription that hosts your Azure Database for MySQL.</span></span> |
   | <span data-ttu-id="bc727-137">Resource group</span><span class="sxs-lookup"><span data-stu-id="bc727-137">Resource group</span></span> | <span data-ttu-id="bc727-138">This field is prepopulated with the resource group of your Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="bc727-138">This field is prepopulated with the resource group of your Azure Database for MySQL.</span></span> |
   | <span data-ttu-id="bc727-139">Resource</span><span class="sxs-lookup"><span data-stu-id="bc727-139">Resource</span></span> | <span data-ttu-id="bc727-140">This field is prepopulated with the name of your Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="bc727-140">This field is prepopulated with the name of your Azure Database for MySQL.</span></span> |
   | <span data-ttu-id="bc727-141">Metric</span><span class="sxs-lookup"><span data-stu-id="bc727-141">Metric</span></span> | <span data-ttu-id="bc727-142">Select the metric that you want to issue an alert for.</span><span class="sxs-lookup"><span data-stu-id="bc727-142">Select the metric that you want to issue an alert for.</span></span> <span data-ttu-id="bc727-143">For example, **Storage percentage**.</span><span class="sxs-lookup"><span data-stu-id="bc727-143">For example, **Storage percentage**.</span></span> |
   | <span data-ttu-id="bc727-144">Condition</span><span class="sxs-lookup"><span data-stu-id="bc727-144">Condition</span></span> | <span data-ttu-id="bc727-145">Choose the condition for the metric to be compared with.</span><span class="sxs-lookup"><span data-stu-id="bc727-145">Choose the condition for the metric to be compared with.</span></span> <span data-ttu-id="bc727-146">For example, **Greater than**.</span><span class="sxs-lookup"><span data-stu-id="bc727-146">For example, **Greater than**.</span></span> |
   | <span data-ttu-id="bc727-147">Threshold</span><span class="sxs-lookup"><span data-stu-id="bc727-147">Threshold</span></span> | <span data-ttu-id="bc727-148">Threshold value for the metric, for example 85 (percent).</span><span class="sxs-lookup"><span data-stu-id="bc727-148">Threshold value for the metric, for example 85 (percent).</span></span> |
   | <span data-ttu-id="bc727-149">Period</span><span class="sxs-lookup"><span data-stu-id="bc727-149">Period</span></span> | <span data-ttu-id="bc727-150">The period of time that the metric rule must be satisfied before the alert triggers.</span><span class="sxs-lookup"><span data-stu-id="bc727-150">The period of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="bc727-151">For example, **Over the last 30 minutes**.</span><span class="sxs-lookup"><span data-stu-id="bc727-151">For example, **Over the last 30 minutes**.</span></span> |

   <span data-ttu-id="bc727-152">Based on the example, the alert looks for Storage percentage above 85% over a 30-minute period.</span><span class="sxs-lookup"><span data-stu-id="bc727-152">Based on the example, the alert looks for Storage percentage above 85% over a 30-minute period.</span></span> <span data-ttu-id="bc727-153">That alert triggers when the average Storage percentage has been above 85% for 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="bc727-153">That alert triggers when the average Storage percentage has been above 85% for 30 minutes.</span></span> <span data-ttu-id="bc727-154">Once the first trigger occurs, it triggers again when the average Storage percentage is below 85% over 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="bc727-154">Once the first trigger occurs, it triggers again when the average Storage percentage is below 85% over 30 minutes.</span></span>

5. <span data-ttu-id="bc727-155">Choose the notification method you want for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="bc727-155">Choose the notification method you want for the alert rule.</span></span> 

   <span data-ttu-id="bc727-156">Check **Email owners, contributors, and readers** option if you want the subscription administrators and co-administrators to be emailed when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="bc727-156">Check **Email owners, contributors, and readers** option if you want the subscription administrators and co-administrators to be emailed when the alert fires.</span></span>

   <span data-ttu-id="bc727-157">If you want additional emails to receive a notification when the alert fires, add them in the **Additional administrator email(s)** field.</span><span class="sxs-lookup"><span data-stu-id="bc727-157">If you want additional emails to receive a notification when the alert fires, add them in the **Additional administrator email(s)** field.</span></span> <span data-ttu-id="bc727-158">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="bc727-158">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

   <span data-ttu-id="bc727-159">Optionally, provide a valid URI in the **Webhook** field if you want it called when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="bc727-159">Optionally, provide a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

6. <span data-ttu-id="bc727-160">Select **OK** to create the alert.</span><span class="sxs-lookup"><span data-stu-id="bc727-160">Select **OK** to create the alert.</span></span>

   <span data-ttu-id="bc727-161">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="bc727-161">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="bc727-162">Manage your alerts</span><span class="sxs-lookup"><span data-stu-id="bc727-162">Manage your alerts</span></span>
<span data-ttu-id="bc727-163">Once you have created an alert, you can select it and do the following actions:</span><span class="sxs-lookup"><span data-stu-id="bc727-163">Once you have created an alert, you can select it and do the following actions:</span></span>

* <span data-ttu-id="bc727-164">View a graph showing the metric threshold and the actual values from the previous day relevant to this alert.</span><span class="sxs-lookup"><span data-stu-id="bc727-164">View a graph showing the metric threshold and the actual values from the previous day relevant to this alert.</span></span>
* <span data-ttu-id="bc727-165">**Edit** or **Delete** the alert rule.</span><span class="sxs-lookup"><span data-stu-id="bc727-165">**Edit** or **Delete** the alert rule.</span></span>
* <span data-ttu-id="bc727-166">**Disable** or **Enable** the alert, if you want to temporarily stop or resume receiving notifications.</span><span class="sxs-lookup"><span data-stu-id="bc727-166">**Disable** or **Enable** the alert, if you want to temporarily stop or resume receiving notifications.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bc727-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc727-167">Next steps</span></span>
* <span data-ttu-id="bc727-168">Learn more about [configuring webhooks in alerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bc727-168">Learn more about [configuring webhooks in alerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="bc727-169">Get an [overview of metrics collection](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="bc727-169">Get an [overview of metrics collection](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
