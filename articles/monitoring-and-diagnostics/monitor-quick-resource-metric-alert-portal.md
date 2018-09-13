---
title: Receive a notification when a metric value meets a condition
description: A quickstart guide to help users create a metric for a Logic App
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: quickstart
ms.date: 02/08/2018
ms.author: ancav
ms.custom: mvc
ms.component: alerts
ms.openlocfilehash: 01955ba7a61b3eb46be6bad72c7243c4918add12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864659"
---
# <a name="receive-a-notification-when-a-metric-value-meets-a-condition"></a><span data-ttu-id="58ae1-103">Receive a notification when a metric value meets a condition</span><span class="sxs-lookup"><span data-stu-id="58ae1-103">Receive a notification when a metric value meets a condition</span></span>

<span data-ttu-id="58ae1-104">Azure Monitor makes metrics available for many Azure resources.</span><span class="sxs-lookup"><span data-stu-id="58ae1-104">Azure Monitor makes metrics available for many Azure resources.</span></span> <span data-ttu-id="58ae1-105">These metrics convey the performance and health of those resources.</span><span class="sxs-lookup"><span data-stu-id="58ae1-105">These metrics convey the performance and health of those resources.</span></span> <span data-ttu-id="58ae1-106">In many cases metric values can point to something being wrong with a resource.</span><span class="sxs-lookup"><span data-stu-id="58ae1-106">In many cases metric values can point to something being wrong with a resource.</span></span> <span data-ttu-id="58ae1-107">You can create metric alerts to monitor for abnormal behavior and be notified if it occurs.</span><span class="sxs-lookup"><span data-stu-id="58ae1-107">You can create metric alerts to monitor for abnormal behavior and be notified if it occurs.</span></span> <span data-ttu-id="58ae1-108">This Quickstart steps through creating a Logic App, creating a job, and visualizing the metrics for the logic app.</span><span class="sxs-lookup"><span data-stu-id="58ae1-108">This Quickstart steps through creating a Logic App, creating a job, and visualizing the metrics for the logic app.</span></span> <span data-ttu-id="58ae1-109">It then goes through creating an alert, and receiving a notification for a metric for the Logic App resource.</span><span class="sxs-lookup"><span data-stu-id="58ae1-109">It then goes through creating an alert, and receiving a notification for a metric for the Logic App resource.</span></span>

<span data-ttu-id="58ae1-110">For more information on metrics and metric alerts, see  [Azure Monitor metrics overview](./monitoring-overview-metrics.md) and [Azure Monitor alerts overview](./monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="58ae1-110">For more information on metrics and metric alerts, see  [Azure Monitor metrics overview](./monitoring-overview-metrics.md) and [Azure Monitor alerts overview](./monitoring-overview-alerts.md).</span></span> 

<span data-ttu-id="58ae1-111">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="58ae1-111">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="58ae1-112">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="58ae1-112">Sign in to the Azure portal</span></span>

<span data-ttu-id="58ae1-113">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="58ae1-113">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="58ae1-114">Create a Logic App</span><span class="sxs-lookup"><span data-stu-id="58ae1-114">Create a Logic App</span></span>

1. <span data-ttu-id="58ae1-115">Click the **Create a resource** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="58ae1-115">Click the **Create a resource** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="58ae1-116">Search for and select **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-116">Search for and select **Logic App**.</span></span> <span data-ttu-id="58ae1-117">Click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="58ae1-117">Click the **Create** button.</span></span>

3. <span data-ttu-id="58ae1-118">Enter the name myLogicApp and the Resource Group myResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="58ae1-118">Enter the name myLogicApp and the Resource Group myResourceGroup.</span></span> <span data-ttu-id="58ae1-119">Use your subscription.</span><span class="sxs-lookup"><span data-stu-id="58ae1-119">Use your subscription.</span></span>  <span data-ttu-id="58ae1-120">Use the default location.</span><span class="sxs-lookup"><span data-stu-id="58ae1-120">Use the default location.</span></span> <span data-ttu-id="58ae1-121">Check the **Pin to Dashboard** option.</span><span class="sxs-lookup"><span data-stu-id="58ae1-121">Check the **Pin to Dashboard** option.</span></span>  <span data-ttu-id="58ae1-122">When complete, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-122">When complete, click **Create**.</span></span> 

    ![Enter basic information about your logic app in the portal](./media/monitor-quick-resource-metric-alert-portal/create-logic-app-portal.png)  


4. <span data-ttu-id="58ae1-124">The logic app should be pinned to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="58ae1-124">The logic app should be pinned to your dashboard.</span></span> <span data-ttu-id="58ae1-125">Navigate to the logic app by clicking on it.</span><span class="sxs-lookup"><span data-stu-id="58ae1-125">Navigate to the logic app by clicking on it.</span></span>

5. <span data-ttu-id="58ae1-126">In the Logic App panel, select the **Logic App Designer**</span><span class="sxs-lookup"><span data-stu-id="58ae1-126">In the Logic App panel, select the **Logic App Designer**</span></span>

     ![Created a recurrence trigger in the logic app designer in the portal panel](./media/monitor-quick-resource-metric-alert-portal/logic-app-designer.png)  

6. <span data-ttu-id="58ae1-128">Set up you values as seen in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="58ae1-128">Set up you values as seen in the following diagram.</span></span>

    ![Configure the logic app trigger in the portal panel](./media/monitor-quick-resource-metric-alert-portal/create-logic-app-triggers.png)<span data-ttu-id="58ae1-130">.</span><span class="sxs-lookup"><span data-stu-id="58ae1-130">.</span></span> 

7. <span data-ttu-id="58ae1-131">In the designer, select the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="58ae1-131">In the designer, select the **Recurrence** trigger.</span></span>

8. <span data-ttu-id="58ae1-132">Set an interval of 20 and a frequency of second to ensure your logic app is triggered every 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="58ae1-132">Set an interval of 20 and a frequency of second to ensure your logic app is triggered every 20 seconds.</span></span>

9. <span data-ttu-id="58ae1-133">Click the **New Step** button, and select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-133">Click the **New Step** button, and select **Add an action**.</span></span>

10. <span data-ttu-id="58ae1-134">Choose the **HTTP** option, and select **HTTP-HTTP**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-134">Choose the **HTTP** option, and select **HTTP-HTTP**.</span></span>

11. <span data-ttu-id="58ae1-135">Set the **Method** as POST and the **Uri** to a web address of your choice.</span><span class="sxs-lookup"><span data-stu-id="58ae1-135">Set the **Method** as POST and the **Uri** to a web address of your choice.</span></span>

12. <span data-ttu-id="58ae1-136">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-136">Click **Save**.</span></span>

13. <span data-ttu-id="58ae1-137">It may take up to 5 minutes for the logic app run actions to occur.</span><span class="sxs-lookup"><span data-stu-id="58ae1-137">It may take up to 5 minutes for the logic app run actions to occur.</span></span>  

## <a name="view-metrics-for-your-logic-app"></a><span data-ttu-id="58ae1-138">View metrics for your logic app</span><span class="sxs-lookup"><span data-stu-id="58ae1-138">View metrics for your logic app</span></span>

1. <span data-ttu-id="58ae1-139">Click the **Monitor** option in the left-hand navigation pane.</span><span class="sxs-lookup"><span data-stu-id="58ae1-139">Click the **Monitor** option in the left-hand navigation pane.</span></span>

2. <span data-ttu-id="58ae1-140">Select the **Metrics** tab, fill in the **Subscription**, **Resource Group**, **Resource Type** and **Resource** information for your logic app.</span><span class="sxs-lookup"><span data-stu-id="58ae1-140">Select the **Metrics** tab, fill in the **Subscription**, **Resource Group**, **Resource Type** and **Resource** information for your logic app.</span></span>

3. <span data-ttu-id="58ae1-141">From the list of metrics, choose **Runs Failed**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-141">From the list of metrics, choose **Runs Failed**.</span></span>

4. <span data-ttu-id="58ae1-142">Modify the **Time range** of the chart to display data for the past hour.</span><span class="sxs-lookup"><span data-stu-id="58ae1-142">Modify the **Time range** of the chart to display data for the past hour.</span></span>

5. <span data-ttu-id="58ae1-143">You should now see a chart plotting the total number of runs your logic app has started over the past hour.</span><span class="sxs-lookup"><span data-stu-id="58ae1-143">You should now see a chart plotting the total number of runs your logic app has started over the past hour.</span></span> <span data-ttu-id="58ae1-144">If you do not see any, make sure you have waited at least 5 minutes from the step above.</span><span class="sxs-lookup"><span data-stu-id="58ae1-144">If you do not see any, make sure you have waited at least 5 minutes from the step above.</span></span> <span data-ttu-id="58ae1-145">Then refresh your browser.</span><span class="sxs-lookup"><span data-stu-id="58ae1-145">Then refresh your browser.</span></span> 

    ![Plot a metric chart for the logic app resource](./media/monitor-quick-resource-metric-alert-portal/logic-app-metric-chart.png)

## <a name="create-a-metric-alert-for-your-logic-app"></a><span data-ttu-id="58ae1-147">Create a metric alert for your logic app</span><span class="sxs-lookup"><span data-stu-id="58ae1-147">Create a metric alert for your logic app</span></span>

1.  <span data-ttu-id="58ae1-148">In the top right portion of the metrics panel click the **Add metric alert** button.</span><span class="sxs-lookup"><span data-stu-id="58ae1-148">In the top right portion of the metrics panel click the **Add metric alert** button.</span></span>

2. <span data-ttu-id="58ae1-149">Name your metric alert 'myLogicAppAlert', and provide a brief description for the alert.</span><span class="sxs-lookup"><span data-stu-id="58ae1-149">Name your metric alert 'myLogicAppAlert', and provide a brief description for the alert.</span></span>

3. <span data-ttu-id="58ae1-150">Set the **Condition** for the metric alert as 'Greater than', set the **Threshold** as '10', and set the **Period** as 'Over the last 5 minutes'.</span><span class="sxs-lookup"><span data-stu-id="58ae1-150">Set the **Condition** for the metric alert as 'Greater than', set the **Threshold** as '10', and set the **Period** as 'Over the last 5 minutes'.</span></span>

4. <span data-ttu-id="58ae1-151">Finally, under **Additional administrator email(s)** enter your email address.</span><span class="sxs-lookup"><span data-stu-id="58ae1-151">Finally, under **Additional administrator email(s)** enter your email address.</span></span> <span data-ttu-id="58ae1-152">This alert ensures that you receive an email in the event your logic app has more than 10 failed runs within a period of 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="58ae1-152">This alert ensures that you receive an email in the event your logic app has more than 10 failed runs within a period of 5 minutes.</span></span>

    ![Configure the logic app alert in the portal panel](./media/monitor-quick-resource-metric-alert-portal/logic-app-metrics-alert-portal.png)

## <a name="receive-metric-alert-notifications-for-your-logic-app"></a><span data-ttu-id="58ae1-154">Receive metric alert notifications for your logic app</span><span class="sxs-lookup"><span data-stu-id="58ae1-154">Receive metric alert notifications for your logic app</span></span>
1. <span data-ttu-id="58ae1-155">Within a few moments, you should receive an email from 'Microsoft Azure Alerts' to inform you the alert has been 'activated'.</span><span class="sxs-lookup"><span data-stu-id="58ae1-155">Within a few moments, you should receive an email from 'Microsoft Azure Alerts' to inform you the alert has been 'activated'.</span></span>

2. <span data-ttu-id="58ae1-156">Navigate back to your logic app and modify the recurrence trigger to an interval of 1 and frequency of hour.</span><span class="sxs-lookup"><span data-stu-id="58ae1-156">Navigate back to your logic app and modify the recurrence trigger to an interval of 1 and frequency of hour.</span></span>

3. <span data-ttu-id="58ae1-157">Within a few minutes, you should receive an email from 'Microsoft Azure Alerts' informing you the alert has been 'resolved'.</span><span class="sxs-lookup"><span data-stu-id="58ae1-157">Within a few minutes, you should receive an email from 'Microsoft Azure Alerts' informing you the alert has been 'resolved'.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="58ae1-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="58ae1-158">Clean up resources</span></span>

<span data-ttu-id="58ae1-159">Other quick starts in this collection build upon this quickstart.</span><span class="sxs-lookup"><span data-stu-id="58ae1-159">Other quick starts in this collection build upon this quickstart.</span></span> <span data-ttu-id="58ae1-160">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="58ae1-160">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="58ae1-161">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="58ae1-161">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure portal.</span></span>

1. <span data-ttu-id="58ae1-162">From the left-hand menu in the Azure portal, click on **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-162">From the left-hand menu in the Azure portal, click on **Monitor**.</span></span>

2. <span data-ttu-id="58ae1-163">Select the **Alerts** tab, find the alert you created in this quickstart guide and click on it.</span><span class="sxs-lookup"><span data-stu-id="58ae1-163">Select the **Alerts** tab, find the alert you created in this quickstart guide and click on it.</span></span>

3. <span data-ttu-id="58ae1-164">In the metric alert panel, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-164">In the metric alert panel, click **Delete**.</span></span>

4. <span data-ttu-id="58ae1-165">From the left-hand menu in the Azure portal, search for **Logic App** and then click **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-165">From the left-hand menu in the Azure portal, search for **Logic App** and then click **Logic apps**.</span></span>

5. <span data-ttu-id="58ae1-166">On the panel, click the logic app you created in this quickstart in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="58ae1-166">On the panel, click the logic app you created in this quickstart in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58ae1-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="58ae1-167">Next steps</span></span>

<span data-ttu-id="58ae1-168">In this quickstart, you’ve learned how to create a metric alert for your resources.</span><span class="sxs-lookup"><span data-stu-id="58ae1-168">In this quickstart, you’ve learned how to create a metric alert for your resources.</span></span> <span data-ttu-id="58ae1-169">For more information on metric alerts, click through to our overview on alerts.</span><span class="sxs-lookup"><span data-stu-id="58ae1-169">For more information on metric alerts, click through to our overview on alerts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="58ae1-170">Azure Monitor subscription action alerts</span><span class="sxs-lookup"><span data-stu-id="58ae1-170">Azure Monitor subscription action alerts</span></span>](./monitor-quick-audit-notify-action-in-subscription.md )
