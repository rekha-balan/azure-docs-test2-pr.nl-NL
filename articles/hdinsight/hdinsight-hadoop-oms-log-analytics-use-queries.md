---
title: Query Azure Log Analytics to monitor Azure HDInsight clusters
description: Learn how to run queries on Azure Log Analytics to monitor jobs running in an HDInsight cluster.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/15/2018
ms.author: jasonh
ms.openlocfilehash: 9550468e8bc9b93216fd4c1ecf144415badfc7dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857860"
---
# <a name="query-azure-log-analytics-to-monitor-hdinsight-clusters"></a><span data-ttu-id="616a8-103">Query Azure Log Analytics to monitor HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="616a8-103">Query Azure Log Analytics to monitor HDInsight clusters</span></span>

<span data-ttu-id="616a8-104">Learn some basic scenarios on how to use Azure Log Analytics to monitor Azure HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="616a8-104">Learn some basic scenarios on how to use Azure Log Analytics to monitor Azure HDInsight clusters:</span></span>

* [<span data-ttu-id="616a8-105">Analyze HDInsight cluster metrics</span><span class="sxs-lookup"><span data-stu-id="616a8-105">Analyze HDInsight cluster metrics</span></span>](#analyze-hdinsight-cluster-metrics)
* [<span data-ttu-id="616a8-106">Search for specific log messages</span><span class="sxs-lookup"><span data-stu-id="616a8-106">Search for specific log messages</span></span>](#search-for-specific-log-messages)
* [<span data-ttu-id="616a8-107">Create event alerts</span><span class="sxs-lookup"><span data-stu-id="616a8-107">Create event alerts</span></span>](#create-alerts-for-tracking-events)

## <a name="prerequisites"></a><span data-ttu-id="616a8-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="616a8-108">Prerequisites</span></span>

* <span data-ttu-id="616a8-109">You must have configured an HDInsight cluster to use Azure Log Analytics, and added the HDInsight cluster-specific Log Analytics management solutions to the workspace.</span><span class="sxs-lookup"><span data-stu-id="616a8-109">You must have configured an HDInsight cluster to use Azure Log Analytics, and added the HDInsight cluster-specific Log Analytics management solutions to the workspace.</span></span> <span data-ttu-id="616a8-110">For instructions, see [Use Azure Log Analytics with HDInsight clusters](hdinsight-hadoop-oms-log-analytics-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="616a8-110">For instructions, see [Use Azure Log Analytics with HDInsight clusters](hdinsight-hadoop-oms-log-analytics-tutorial.md).</span></span>

## <a name="analyze-hdinsight-cluster-metrics"></a><span data-ttu-id="616a8-111">Analyze HDInsight cluster metrics</span><span class="sxs-lookup"><span data-stu-id="616a8-111">Analyze HDInsight cluster metrics</span></span>

<span data-ttu-id="616a8-112">Learn how to look for specific metrics for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="616a8-112">Learn how to look for specific metrics for your HDInsight cluster.</span></span>

1. <span data-ttu-id="616a8-113">Open the OMS workspace that is associated to your HDInsight cluster from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="616a8-113">Open the OMS workspace that is associated to your HDInsight cluster from the Azure portal.</span></span>
2. <span data-ttu-id="616a8-114">Select the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="616a8-114">Select the **Log Search** tile.</span></span>
3. <span data-ttu-id="616a8-115">Type the following query in the search box to search for all metrics for all available metrics for all HDInsight clusters configured to use Azure Log Analytics, and then select **RUN**.</span><span class="sxs-lookup"><span data-stu-id="616a8-115">Type the following query in the search box to search for all metrics for all available metrics for all HDInsight clusters configured to use Azure Log Analytics, and then select **RUN**.</span></span>

        search *

    <span data-ttu-id="616a8-116">![Search all metrics](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-all-metrics.png "Search all metrics")</span><span class="sxs-lookup"><span data-stu-id="616a8-116">![Search all metrics](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-all-metrics.png "Search all metrics")</span></span>

    <span data-ttu-id="616a8-117">The output shall look like:</span><span class="sxs-lookup"><span data-stu-id="616a8-117">The output shall look like:</span></span>

    <span data-ttu-id="616a8-118">![Search all metrics output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-all-metrics-output.png "Search all metrics output")</span><span class="sxs-lookup"><span data-stu-id="616a8-118">![Search all metrics output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-all-metrics-output.png "Search all metrics output")</span></span>

5. <span data-ttu-id="616a8-119">From the left pane, under **Type**, select a metric that you want to dig deep into, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="616a8-119">From the left pane, under **Type**, select a metric that you want to dig deep into, and then select **Apply**.</span></span> <span data-ttu-id="616a8-120">The following screenshot shows the `metrics_resourcemanager_queue_root_default_CL` type is selected.</span><span class="sxs-lookup"><span data-stu-id="616a8-120">The following screenshot shows the `metrics_resourcemanager_queue_root_default_CL` type is selected.</span></span>

    > [!NOTE]
    > <span data-ttu-id="616a8-121">You may need to select the **[+]More** button to find the metric you are looking for.</span><span class="sxs-lookup"><span data-stu-id="616a8-121">You may need to select the **[+]More** button to find the metric you are looking for.</span></span> <span data-ttu-id="616a8-122">Also, the **Apply** button is at the bottom of the list so you must scroll down to see it.</span><span class="sxs-lookup"><span data-stu-id="616a8-122">Also, the **Apply** button is at the bottom of the list so you must scroll down to see it.</span></span>

    <span data-ttu-id="616a8-123">Notice that the query in the text box changes to one shown in the highlighted box in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="616a8-123">Notice that the query in the text box changes to one shown in the highlighted box in the following screenshot:</span></span>

    <span data-ttu-id="616a8-124">![Search for specific metrics](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-metrics.png "Search for specific metrics")</span><span class="sxs-lookup"><span data-stu-id="616a8-124">![Search for specific metrics](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-metrics.png "Search for specific metrics")</span></span>

6. <span data-ttu-id="616a8-125">To dig deeper into this specific metric.</span><span class="sxs-lookup"><span data-stu-id="616a8-125">To dig deeper into this specific metric.</span></span> <span data-ttu-id="616a8-126">For example, you can refine the existing output based on the average of resources used in a 10-minute interval, categorized by cluster name using the following query:</span><span class="sxs-lookup"><span data-stu-id="616a8-126">For example, you can refine the existing output based on the average of resources used in a 10-minute interval, categorized by cluster name using the following query:</span></span>

        search in (metrics_resourcemanager_queue_root_default_CL) * | summarize AggregatedValue = avg(UsedAMResourceMB_d) by ClusterName_s, bin(TimeGenerated, 10m)

7. <span data-ttu-id="616a8-127">Instead of refining based on the average of resources used, you can use the following query to refine the results based on when the maximum resources were used (as well as 90th and 95th percentile) in a 10-minute window:</span><span class="sxs-lookup"><span data-stu-id="616a8-127">Instead of refining based on the average of resources used, you can use the following query to refine the results based on when the maximum resources were used (as well as 90th and 95th percentile) in a 10-minute window:</span></span>

        search in (metrics_resourcemanager_queue_root_default_CL) * | summarize ["max(UsedAMResourceMB_d)"] = max(UsedAMResourceMB_d), ["pct95(UsedAMResourceMB_d)"] = percentile(UsedAMResourceMB_d, 95), ["pct90(UsedAMResourceMB_d)"] = percentile(UsedAMResourceMB_d, 90) by ClusterName_s, bin(TimeGenerated, 10m)

## <a name="search-for-specific-log-messages"></a><span data-ttu-id="616a8-128">Search for specific log messages</span><span class="sxs-lookup"><span data-stu-id="616a8-128">Search for specific log messages</span></span>

<span data-ttu-id="616a8-129">Learn how to  look error messages during a specific time window.</span><span class="sxs-lookup"><span data-stu-id="616a8-129">Learn how to  look error messages during a specific time window.</span></span> <span data-ttu-id="616a8-130">The steps here are just one example on how you can arrive at the error message you are interested in.</span><span class="sxs-lookup"><span data-stu-id="616a8-130">The steps here are just one example on how you can arrive at the error message you are interested in.</span></span> <span data-ttu-id="616a8-131">You can use any property that is available to look for the errors you are trying to find.</span><span class="sxs-lookup"><span data-stu-id="616a8-131">You can use any property that is available to look for the errors you are trying to find.</span></span>

1. <span data-ttu-id="616a8-132">Open the OMS workspace that is associated to your HDInsight cluster from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="616a8-132">Open the OMS workspace that is associated to your HDInsight cluster from the Azure portal.</span></span>
2. <span data-ttu-id="616a8-133">Select the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="616a8-133">Select the **Log Search** tile.</span></span>
3. <span data-ttu-id="616a8-134">Type the following query to search for all error messages for all HDInsight clusters configured to use Azure Log Analytics, and then select **RUN**.</span><span class="sxs-lookup"><span data-stu-id="616a8-134">Type the following query to search for all error messages for all HDInsight clusters configured to use Azure Log Analytics, and then select **RUN**.</span></span> 

         search "Error"

    <span data-ttu-id="616a8-135">You shall see an output like the following output:</span><span class="sxs-lookup"><span data-stu-id="616a8-135">You shall see an output like the following output:</span></span>

    <span data-ttu-id="616a8-136">![Search all errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-all-errors-output.png "Search all errors output")</span><span class="sxs-lookup"><span data-stu-id="616a8-136">![Search all errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-all-errors-output.png "Search all errors output")</span></span>

4. <span data-ttu-id="616a8-137">From the left pane, under **Type** category, select an error type that you want to dig deep into, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="616a8-137">From the left pane, under **Type** category, select an error type that you want to dig deep into, and then select **Apply**.</span></span>  <span data-ttu-id="616a8-138">Notice the results are refined to only show the error of the type you selected.</span><span class="sxs-lookup"><span data-stu-id="616a8-138">Notice the results are refined to only show the error of the type you selected.</span></span>
5. <span data-ttu-id="616a8-139">You can dig deeper into this specific error list by using the options available in the left pane.</span><span class="sxs-lookup"><span data-stu-id="616a8-139">You can dig deeper into this specific error list by using the options available in the left pane.</span></span> <span data-ttu-id="616a8-140">For example:</span><span class="sxs-lookup"><span data-stu-id="616a8-140">For example:</span></span>

    - <span data-ttu-id="616a8-141">To see error messages from a specific worker node:</span><span class="sxs-lookup"><span data-stu-id="616a8-141">To see error messages from a specific worker node:</span></span>

        <span data-ttu-id="616a8-142">![Search for specific errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-error-refined.png "Search for specific errors output")</span><span class="sxs-lookup"><span data-stu-id="616a8-142">![Search for specific errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-error-refined.png "Search for specific errors output")</span></span>

    - <span data-ttu-id="616a8-143">To see an error occurred at a certain time:</span><span class="sxs-lookup"><span data-stu-id="616a8-143">To see an error occurred at a certain time:</span></span>

        <span data-ttu-id="616a8-144">![Search for specific errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-error-time.png "Search for specific errors output")</span><span class="sxs-lookup"><span data-stu-id="616a8-144">![Search for specific errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-error-time.png "Search for specific errors output")</span></span>

6. <span data-ttu-id="616a8-145">To see the specific error.</span><span class="sxs-lookup"><span data-stu-id="616a8-145">To see the specific error.</span></span> <span data-ttu-id="616a8-146">You can select **[+]show more** to look at the actual error message.</span><span class="sxs-lookup"><span data-stu-id="616a8-146">You can select **[+]show more** to look at the actual error message.</span></span>

    <span data-ttu-id="616a8-147">![Search for specific errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-error-arrived.png "Search for specific errors output")</span><span class="sxs-lookup"><span data-stu-id="616a8-147">![Search for specific errors output](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-search-specific-error-arrived.png "Search for specific errors output")</span></span>

## <a name="create-alerts-for-tracking-events"></a><span data-ttu-id="616a8-148">Create alerts for tracking events</span><span class="sxs-lookup"><span data-stu-id="616a8-148">Create alerts for tracking events</span></span>

<span data-ttu-id="616a8-149">The first step to create an alert is to arrive at a query based on which the alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="616a8-149">The first step to create an alert is to arrive at a query based on which the alert is triggered.</span></span> <span data-ttu-id="616a8-150">You can use any query that you want to create an alert.</span><span class="sxs-lookup"><span data-stu-id="616a8-150">You can use any query that you want to create an alert.</span></span>

1. <span data-ttu-id="616a8-151">Open the Log Analytics workspace that is associated to your HDInsight cluster from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="616a8-151">Open the Log Analytics workspace that is associated to your HDInsight cluster from the Azure portal.</span></span>
2. <span data-ttu-id="616a8-152">Select the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="616a8-152">Select the **Log Search** tile.</span></span>
3. <span data-ttu-id="616a8-153">Run the following query on which you want to create an alert, and then select **RUN**.</span><span class="sxs-lookup"><span data-stu-id="616a8-153">Run the following query on which you want to create an alert, and then select **RUN**.</span></span>

        metrics_resourcemanager_queue_root_default_CL | where AppsFailed_d > 0

    <span data-ttu-id="616a8-154">The query provides list of failed applications running on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="616a8-154">The query provides list of failed applications running on HDInsight clusters.</span></span>

4. <span data-ttu-id="616a8-155">Select **New Alert Rule** on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="616a8-155">Select **New Alert Rule** on the top of the page.</span></span>

    <span data-ttu-id="616a8-156">![Enter query to create an alert](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-create-alert-query.png "Enter query to create an alert")</span><span class="sxs-lookup"><span data-stu-id="616a8-156">![Enter query to create an alert](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-create-alert-query.png "Enter query to create an alert")</span></span>

5. <span data-ttu-id="616a8-157">In the **Create rule** window, enter the query and other details to create an alert, and then select **Create alert rule**.</span><span class="sxs-lookup"><span data-stu-id="616a8-157">In the **Create rule** window, enter the query and other details to create an alert, and then select **Create alert rule**.</span></span>

    <span data-ttu-id="616a8-158">![Enter query to create an alert](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-create-alert.png "Enter query to create an alert")</span><span class="sxs-lookup"><span data-stu-id="616a8-158">![Enter query to create an alert](./media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-create-alert.png "Enter query to create an alert")</span></span>

<span data-ttu-id="616a8-159">To edit or delete an existing alert:</span><span class="sxs-lookup"><span data-stu-id="616a8-159">To edit or delete an existing alert:</span></span>

1. <span data-ttu-id="616a8-160">Open the Log Analytics workspace from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="616a8-160">Open the Log Analytics workspace from the Azure portal.</span></span>
2. <span data-ttu-id="616a8-161">From the left menu, select **Alert**.</span><span class="sxs-lookup"><span data-stu-id="616a8-161">From the left menu, select **Alert**.</span></span>
3. <span data-ttu-id="616a8-162">Select the alert you want to edit or delete.</span><span class="sxs-lookup"><span data-stu-id="616a8-162">Select the alert you want to edit or delete.</span></span>
4. <span data-ttu-id="616a8-163">You have the following options: **Save**, **Discard**, **Disable**, and **Delete**.</span><span class="sxs-lookup"><span data-stu-id="616a8-163">You have the following options: **Save**, **Discard**, **Disable**, and **Delete**.</span></span>

    ![HDInsight Log Analytics OMS alert delete edit](media/hdinsight-hadoop-oms-log-analytics-use-queries/hdinsight-log-analytics-edit-alert.png)

<span data-ttu-id="616a8-165">For more information, see [Working with alert rules in Log Analytics](../log-analytics/log-analytics-alerts-creating.md).</span><span class="sxs-lookup"><span data-stu-id="616a8-165">For more information, see [Working with alert rules in Log Analytics](../log-analytics/log-analytics-alerts-creating.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="616a8-166">See also</span><span class="sxs-lookup"><span data-stu-id="616a8-166">See also</span></span>

* [<span data-ttu-id="616a8-167">Working with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="616a8-167">Working with Log Analytics</span></span>](https://blogs.msdn.microsoft.com/wei_out_there_with_system_center/2016/07/03/oms-log-analytics-create-tiles-drill-ins-and-dashboards-with-the-view-designer/)
* [<span data-ttu-id="616a8-168">Create alert rules in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="616a8-168">Create alert rules in Log Analytics</span></span>](../log-analytics/log-analytics-alerts-creating.md)
