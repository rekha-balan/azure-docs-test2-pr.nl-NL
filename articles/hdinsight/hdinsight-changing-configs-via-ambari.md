---
title: Optimize cluster configurations with Ambari - Azure HDInsight
description: Use the Ambari web UI to configure and optimize HDInsight clusters.
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: ashish
ms.openlocfilehash: 73fdd3f221e35bc1e0b0904bdbbaa63525ba4be3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866702"
---
# <a name="use-ambari-to-optimize-hdinsight-cluster-configurations"></a><span data-ttu-id="b94a8-103">Use Ambari to optimize HDInsight cluster configurations</span><span class="sxs-lookup"><span data-stu-id="b94a8-103">Use Ambari to optimize HDInsight cluster configurations</span></span>

<span data-ttu-id="b94a8-104">HDInsight provides Apache Hadoop clusters for large-scale data processing applications.</span><span class="sxs-lookup"><span data-stu-id="b94a8-104">HDInsight provides Apache Hadoop clusters for large-scale data processing applications.</span></span> <span data-ttu-id="b94a8-105">Managing,  monitoring, and optimizing these complex multi-node clusters can be challenging.</span><span class="sxs-lookup"><span data-stu-id="b94a8-105">Managing,  monitoring, and optimizing these complex multi-node clusters can be challenging.</span></span> <span data-ttu-id="b94a8-106">[Apache Ambari](http://ambari.apache.org/) is a web interface to  manage and monitor HDInsight Linux clusters.</span><span class="sxs-lookup"><span data-stu-id="b94a8-106">[Apache Ambari](http://ambari.apache.org/) is a web interface to  manage and monitor HDInsight Linux clusters.</span></span>  <span data-ttu-id="b94a8-107">For Windows clusters, use the Ambari [REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="b94a8-107">For Windows clusters, use the Ambari [REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

<span data-ttu-id="b94a8-108">For an introduction to using the Ambari Web UI, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="b94a8-108">For an introduction to using the Ambari Web UI, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="b94a8-109">Log in to  Ambari at `https://CLUSTERNAME.azurehdidnsight.net` with your cluster credentials.</span><span class="sxs-lookup"><span data-stu-id="b94a8-109">Log in to  Ambari at `https://CLUSTERNAME.azurehdidnsight.net` with your cluster credentials.</span></span> <span data-ttu-id="b94a8-110">The initial screen  displays an overview dashboard.</span><span class="sxs-lookup"><span data-stu-id="b94a8-110">The initial screen  displays an overview dashboard.</span></span>

![Ambari dashboard](./media/hdinsight-changing-configs-via-ambari/ambari-dashboard.png)

<span data-ttu-id="b94a8-112">The Ambari web UI can be used to manage hosts, services, alerts, configurations, and views.</span><span class="sxs-lookup"><span data-stu-id="b94a8-112">The Ambari web UI can be used to manage hosts, services, alerts, configurations, and views.</span></span> <span data-ttu-id="b94a8-113">Ambari can't be used to create an HDInsight cluster, upgrade services, manage stacks and versions, decommission or recommission hosts, or add services to the cluster.</span><span class="sxs-lookup"><span data-stu-id="b94a8-113">Ambari can't be used to create an HDInsight cluster, upgrade services, manage stacks and versions, decommission or recommission hosts, or add services to the cluster.</span></span>

## <a name="manage-your-clusters-configuration"></a><span data-ttu-id="b94a8-114">Manage your cluster's configuration</span><span class="sxs-lookup"><span data-stu-id="b94a8-114">Manage your cluster's configuration</span></span>

<span data-ttu-id="b94a8-115">Configuration settings help tune a particular service.</span><span class="sxs-lookup"><span data-stu-id="b94a8-115">Configuration settings help tune a particular service.</span></span> <span data-ttu-id="b94a8-116">To modify a service's configuration settings, select the service from the **Services** sidebar (on the left), and then navigate to the **Configs** tab in the service detail page.</span><span class="sxs-lookup"><span data-stu-id="b94a8-116">To modify a service's configuration settings, select the service from the **Services** sidebar (on the left), and then navigate to the **Configs** tab in the service detail page.</span></span>

![Services sidebar](./media/hdinsight-changing-configs-via-ambari/services-sidebar.png)

### <a name="modify-namenode-java-heap-size"></a><span data-ttu-id="b94a8-118">Modify NameNode Java heap size</span><span class="sxs-lookup"><span data-stu-id="b94a8-118">Modify NameNode Java heap size</span></span>

<span data-ttu-id="b94a8-119">The NameNode Java heap size depends on many factors such as the load on the cluster, the numbers of files, and the numbers of blocks.</span><span class="sxs-lookup"><span data-stu-id="b94a8-119">The NameNode Java heap size depends on many factors such as the load on the cluster, the numbers of files, and the numbers of blocks.</span></span> <span data-ttu-id="b94a8-120">The default size of 1 GB works well with most clusters, although some workloads can require more or less memory.</span><span class="sxs-lookup"><span data-stu-id="b94a8-120">The default size of 1 GB works well with most clusters, although some workloads can require more or less memory.</span></span> 

<span data-ttu-id="b94a8-121">To modify the NameNode Java heap size:</span><span class="sxs-lookup"><span data-stu-id="b94a8-121">To modify the NameNode Java heap size:</span></span>

1. <span data-ttu-id="b94a8-122">Select **HDFS** from the Services sidebar and navigate to the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="b94a8-122">Select **HDFS** from the Services sidebar and navigate to the **Configs** tab.</span></span>

    ![HDFS configuration](./media/hdinsight-changing-configs-via-ambari/hdfs-config.png)

1. <span data-ttu-id="b94a8-124">Find the setting **NameNode Java heap size**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-124">Find the setting **NameNode Java heap size**.</span></span> <span data-ttu-id="b94a8-125">You can also use the **filter** text box to type and find a particular setting.</span><span class="sxs-lookup"><span data-stu-id="b94a8-125">You can also use the **filter** text box to type and find a particular setting.</span></span> <span data-ttu-id="b94a8-126">Select the **pen** icon beside the setting name.</span><span class="sxs-lookup"><span data-stu-id="b94a8-126">Select the **pen** icon beside the setting name.</span></span>

    ![NameNode Java heap size](./media/hdinsight-changing-configs-via-ambari/java-heap-size.png)

1. <span data-ttu-id="b94a8-128">Type the new value in the text box, and then press **Enter** to save the change.</span><span class="sxs-lookup"><span data-stu-id="b94a8-128">Type the new value in the text box, and then press **Enter** to save the change.</span></span>

    ![Edit NameNode Java heap size](./media/hdinsight-changing-configs-via-ambari/java-heap-size-edit.png)

1. <span data-ttu-id="b94a8-130">The NameNode Java heap size is changed to 2 GB from 1 GB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-130">The NameNode Java heap size is changed to 2 GB from 1 GB.</span></span>

    ![Edited NameNode Java heap size](./media/hdinsight-changing-configs-via-ambari/java-heap-size-edited.png)

1. <span data-ttu-id="b94a8-132">Save your changes by clicking on the green **Save** button on the top of the configuration screen.</span><span class="sxs-lookup"><span data-stu-id="b94a8-132">Save your changes by clicking on the green **Save** button on the top of the configuration screen.</span></span>

    ![Save changes](./media/hdinsight-changing-configs-via-ambari/save-changes.png)

## <a name="hive-optimization"></a><span data-ttu-id="b94a8-134">Hive optimization</span><span class="sxs-lookup"><span data-stu-id="b94a8-134">Hive optimization</span></span>

<span data-ttu-id="b94a8-135">The following sections describe configuration options for optimizing overall Hive performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-135">The following sections describe configuration options for optimizing overall Hive performance.</span></span>

1. <span data-ttu-id="b94a8-136">To modify Hive configuration parameters, select **Hive** from the Services sidebar.</span><span class="sxs-lookup"><span data-stu-id="b94a8-136">To modify Hive configuration parameters, select **Hive** from the Services sidebar.</span></span>
1. <span data-ttu-id="b94a8-137">Navigate to the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="b94a8-137">Navigate to the **Configs** tab.</span></span>

### <a name="set-the-hive-execution-engine"></a><span data-ttu-id="b94a8-138">Set the Hive execution engine</span><span class="sxs-lookup"><span data-stu-id="b94a8-138">Set the Hive execution engine</span></span>

<span data-ttu-id="b94a8-139">Hive provides two execution engines: MapReduce and Tez.</span><span class="sxs-lookup"><span data-stu-id="b94a8-139">Hive provides two execution engines: MapReduce and Tez.</span></span> <span data-ttu-id="b94a8-140">Tez is faster than MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b94a8-140">Tez is faster than MapReduce.</span></span> <span data-ttu-id="b94a8-141">HDInsight Linux clusters have Tez as the default execution engine.</span><span class="sxs-lookup"><span data-stu-id="b94a8-141">HDInsight Linux clusters have Tez as the default execution engine.</span></span> <span data-ttu-id="b94a8-142">To change the execution engine:</span><span class="sxs-lookup"><span data-stu-id="b94a8-142">To change the execution engine:</span></span>

1. <span data-ttu-id="b94a8-143">In the Hive **Configs** tab, type **execution engine** in the filter box.</span><span class="sxs-lookup"><span data-stu-id="b94a8-143">In the Hive **Configs** tab, type **execution engine** in the filter box.</span></span>

    ![Search execution engine](./media/hdinsight-changing-configs-via-ambari/search-execution.png)

1. <span data-ttu-id="b94a8-145">The **Optimization** property's default value is **Tez**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-145">The **Optimization** property's default value is **Tez**.</span></span>

    ![Optimization - Tez](./media/hdinsight-changing-configs-via-ambari/optimization-tez.png)

### <a name="tune-mappers"></a><span data-ttu-id="b94a8-147">Tune mappers</span><span class="sxs-lookup"><span data-stu-id="b94a8-147">Tune mappers</span></span>

<span data-ttu-id="b94a8-148">Hadoop tries to split (*map*) a single file into multiple files and process the resulting files in parallel.</span><span class="sxs-lookup"><span data-stu-id="b94a8-148">Hadoop tries to split (*map*) a single file into multiple files and process the resulting files in parallel.</span></span> <span data-ttu-id="b94a8-149">The number of mappers depends on the number of splits.</span><span class="sxs-lookup"><span data-stu-id="b94a8-149">The number of mappers depends on the number of splits.</span></span> <span data-ttu-id="b94a8-150">The following two configuration parameters drive the number of splits for the Tez execution engine:</span><span class="sxs-lookup"><span data-stu-id="b94a8-150">The following two configuration parameters drive the number of splits for the Tez execution engine:</span></span>

* <span data-ttu-id="b94a8-151">`tez.grouping.min-size`: Lower limit on the size of a grouped split, with a default value of 16 MB (16,777,216 bytes).</span><span class="sxs-lookup"><span data-stu-id="b94a8-151">`tez.grouping.min-size`: Lower limit on the size of a grouped split, with a default value of 16 MB (16,777,216 bytes).</span></span>
* <span data-ttu-id="b94a8-152">`tez.grouping.max-size`: Upper limit on the size of a grouped split, with a default value of 1 GB (1,073,741,824 bytes).</span><span class="sxs-lookup"><span data-stu-id="b94a8-152">`tez.grouping.max-size`: Upper limit on the size of a grouped split, with a default value of 1 GB (1,073,741,824 bytes).</span></span>

<span data-ttu-id="b94a8-153">As a performance rule of thumb, decrease both of these parameters to improve latency, increase for more throughput.</span><span class="sxs-lookup"><span data-stu-id="b94a8-153">As a performance rule of thumb, decrease both of these parameters to improve latency, increase for more throughput.</span></span>

<span data-ttu-id="b94a8-154">For example, to set four mapper tasks for a data size of 128 MB, you would set both parameters to 32 MB each (33,554,432 bytes).</span><span class="sxs-lookup"><span data-stu-id="b94a8-154">For example, to set four mapper tasks for a data size of 128 MB, you would set both parameters to 32 MB each (33,554,432 bytes).</span></span>

1. <span data-ttu-id="b94a8-155">To modify the limit parameters, navigate to the **Configs** tab of the Tez service.</span><span class="sxs-lookup"><span data-stu-id="b94a8-155">To modify the limit parameters, navigate to the **Configs** tab of the Tez service.</span></span> <span data-ttu-id="b94a8-156">Expand the **General** panel, and  locate the `tez.grouping.max-size` and `tez.grouping.min-size` parameters.</span><span class="sxs-lookup"><span data-stu-id="b94a8-156">Expand the **General** panel, and  locate the `tez.grouping.max-size` and `tez.grouping.min-size` parameters.</span></span>

1. <span data-ttu-id="b94a8-157">Set both parameters to **33,554,432** bytes (32 MB).</span><span class="sxs-lookup"><span data-stu-id="b94a8-157">Set both parameters to **33,554,432** bytes (32 MB).</span></span>

    ![Tez grouping sizes](./media/hdinsight-changing-configs-via-ambari/tez-grouping-size.png)
 
<span data-ttu-id="b94a8-159">These changes  affect all Tez jobs across the server.</span><span class="sxs-lookup"><span data-stu-id="b94a8-159">These changes  affect all Tez jobs across the server.</span></span> <span data-ttu-id="b94a8-160">To get an optimal result, choose appropriate parameter values.</span><span class="sxs-lookup"><span data-stu-id="b94a8-160">To get an optimal result, choose appropriate parameter values.</span></span>

### <a name="tune-reducers"></a><span data-ttu-id="b94a8-161">Tune reducers</span><span class="sxs-lookup"><span data-stu-id="b94a8-161">Tune reducers</span></span>

<span data-ttu-id="b94a8-162">ORC and Snappy both offer high performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-162">ORC and Snappy both offer high performance.</span></span> <span data-ttu-id="b94a8-163">However, Hive may have too few reducers by default, causing bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="b94a8-163">However, Hive may have too few reducers by default, causing bottlenecks.</span></span>

<span data-ttu-id="b94a8-164">For example, say you have an input data size of 50 GB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-164">For example, say you have an input data size of 50 GB.</span></span> <span data-ttu-id="b94a8-165">That data in ORC format with Snappy compression is 1 GB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-165">That data in ORC format with Snappy compression is 1 GB.</span></span> <span data-ttu-id="b94a8-166">Hive estimates the number of reducers needed as:     (number of bytes input to mappers / `hive.exec.reducers.bytes.per.reducer`).</span><span class="sxs-lookup"><span data-stu-id="b94a8-166">Hive estimates the number of reducers needed as:     (number of bytes input to mappers / `hive.exec.reducers.bytes.per.reducer`).</span></span>

<span data-ttu-id="b94a8-167">With the default settings, this example is 4 reducers.</span><span class="sxs-lookup"><span data-stu-id="b94a8-167">With the default settings, this example is 4 reducers.</span></span>

<span data-ttu-id="b94a8-168">The `hive.exec.reducers.bytes.per.reducer` parameter specifies the number of bytes processed per reducer.</span><span class="sxs-lookup"><span data-stu-id="b94a8-168">The `hive.exec.reducers.bytes.per.reducer` parameter specifies the number of bytes processed per reducer.</span></span> <span data-ttu-id="b94a8-169">The default value is 64 MB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-169">The default value is 64 MB.</span></span> <span data-ttu-id="b94a8-170">Tuning this value down increases parallelism and may improve performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-170">Tuning this value down increases parallelism and may improve performance.</span></span> <span data-ttu-id="b94a8-171">Tuning it too low could also produce too many reducers, potentially adversely affecting performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-171">Tuning it too low could also produce too many reducers, potentially adversely affecting performance.</span></span> <span data-ttu-id="b94a8-172">This parameter is based on your particular data requirements, compression settings, and other environmental factors.</span><span class="sxs-lookup"><span data-stu-id="b94a8-172">This parameter is based on your particular data requirements, compression settings, and other environmental factors.</span></span>

1. <span data-ttu-id="b94a8-173">To modify the parameter, navigate to the Hive **Configs** tab and find the **Data per Reducer** parameter on the Settings page.</span><span class="sxs-lookup"><span data-stu-id="b94a8-173">To modify the parameter, navigate to the Hive **Configs** tab and find the **Data per Reducer** parameter on the Settings page.</span></span>

    ![Data per Reducer](./media/hdinsight-changing-configs-via-ambari/data-per-reducer.png)
 
1. <span data-ttu-id="b94a8-175">Select **Edit** to modify the value to 128 MB (134,217,728 bytes), and then press **Enter** to save.</span><span class="sxs-lookup"><span data-stu-id="b94a8-175">Select **Edit** to modify the value to 128 MB (134,217,728 bytes), and then press **Enter** to save.</span></span>

    ![Data per Reducer - edited](./media/hdinsight-changing-configs-via-ambari/data-per-reducer-edited.png)
  
    <span data-ttu-id="b94a8-177">Given an input size of 1,024 MB, with 128 MB of data per reducer, there are  8 reducers (1024/128).</span><span class="sxs-lookup"><span data-stu-id="b94a8-177">Given an input size of 1,024 MB, with 128 MB of data per reducer, there are  8 reducers (1024/128).</span></span>

1. <span data-ttu-id="b94a8-178">An incorrect value for the **Data per Reducer** parameter may result in a large number of reducers, adversely affecting query performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-178">An incorrect value for the **Data per Reducer** parameter may result in a large number of reducers, adversely affecting query performance.</span></span> <span data-ttu-id="b94a8-179">To limit the maximum number of reducers, set `hive.exec.reducers.max` to an appropriate value.</span><span class="sxs-lookup"><span data-stu-id="b94a8-179">To limit the maximum number of reducers, set `hive.exec.reducers.max` to an appropriate value.</span></span> <span data-ttu-id="b94a8-180">The default value is 1009.</span><span class="sxs-lookup"><span data-stu-id="b94a8-180">The default value is 1009.</span></span>

### <a name="enable-parallel-execution"></a><span data-ttu-id="b94a8-181">Enable parallel execution</span><span class="sxs-lookup"><span data-stu-id="b94a8-181">Enable parallel execution</span></span>

<span data-ttu-id="b94a8-182">A Hive query is executed in one or more stages.</span><span class="sxs-lookup"><span data-stu-id="b94a8-182">A Hive query is executed in one or more stages.</span></span> <span data-ttu-id="b94a8-183">If the independent stages can be run in parallel, that will increase query performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-183">If the independent stages can be run in parallel, that will increase query performance.</span></span>

1.  <span data-ttu-id="b94a8-184">To enable parallel query execution, navigate to the Hive **Config** tab and search for the `hive.exec.parallel` property.</span><span class="sxs-lookup"><span data-stu-id="b94a8-184">To enable parallel query execution, navigate to the Hive **Config** tab and search for the `hive.exec.parallel` property.</span></span> <span data-ttu-id="b94a8-185">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-185">The default value is false.</span></span> <span data-ttu-id="b94a8-186">Change the value to true, and then press **Enter** to save the value.</span><span class="sxs-lookup"><span data-stu-id="b94a8-186">Change the value to true, and then press **Enter** to save the value.</span></span>
 
1.  <span data-ttu-id="b94a8-187">To limit the number of jobs to be run in parallel, modify the `hive.exec.parallel.thread.number` property.</span><span class="sxs-lookup"><span data-stu-id="b94a8-187">To limit the number of jobs to be run in parallel, modify the `hive.exec.parallel.thread.number` property.</span></span> <span data-ttu-id="b94a8-188">The default value is 8.</span><span class="sxs-lookup"><span data-stu-id="b94a8-188">The default value is 8.</span></span>

    ![Hive exec parallel](./media/hdinsight-changing-configs-via-ambari/hive-exec-parallel.png)


### <a name="enable-vectorization"></a><span data-ttu-id="b94a8-190">Enable vectorization</span><span class="sxs-lookup"><span data-stu-id="b94a8-190">Enable vectorization</span></span>

<span data-ttu-id="b94a8-191">Hive processes data row by row.</span><span class="sxs-lookup"><span data-stu-id="b94a8-191">Hive processes data row by row.</span></span> <span data-ttu-id="b94a8-192">Vectorization directs Hive to process data in blocks of 1,024 rows rather than one row at a time.</span><span class="sxs-lookup"><span data-stu-id="b94a8-192">Vectorization directs Hive to process data in blocks of 1,024 rows rather than one row at a time.</span></span> <span data-ttu-id="b94a8-193">Vectorization is only applicable to the ORC file format.</span><span class="sxs-lookup"><span data-stu-id="b94a8-193">Vectorization is only applicable to the ORC file format.</span></span>

1. <span data-ttu-id="b94a8-194">To enable a vectorized query execution, navigate to the Hive **Configs** tab and search for the `hive.vectorized.execution.enabled` parameter.</span><span class="sxs-lookup"><span data-stu-id="b94a8-194">To enable a vectorized query execution, navigate to the Hive **Configs** tab and search for the `hive.vectorized.execution.enabled` parameter.</span></span> <span data-ttu-id="b94a8-195">The default value is true for Hive 0.13.0 or later.</span><span class="sxs-lookup"><span data-stu-id="b94a8-195">The default value is true for Hive 0.13.0 or later.</span></span>
 
1. <span data-ttu-id="b94a8-196">To enable vectorized execution for the reduce side of the query, set the `hive.vectorized.execution.reduce.enabled` parameter to true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-196">To enable vectorized execution for the reduce side of the query, set the `hive.vectorized.execution.reduce.enabled` parameter to true.</span></span> <span data-ttu-id="b94a8-197">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-197">The default value is false.</span></span>

    ![Hive vectorized execution](./media/hdinsight-changing-configs-via-ambari/hive-vectorized-execution.png)

### <a name="enable-cost-based-optimization-cbo"></a><span data-ttu-id="b94a8-199">Enable cost-based optimization (CBO)</span><span class="sxs-lookup"><span data-stu-id="b94a8-199">Enable cost-based optimization (CBO)</span></span>

<span data-ttu-id="b94a8-200">By default, Hive follows a set of rules to find one optimal query execution plan.</span><span class="sxs-lookup"><span data-stu-id="b94a8-200">By default, Hive follows a set of rules to find one optimal query execution plan.</span></span> <span data-ttu-id="b94a8-201">Cost-based optimization (CBO) evaluates multiple plans to execute a query and assigns a cost to each plan, then determines the cheapest plan to execute a query.</span><span class="sxs-lookup"><span data-stu-id="b94a8-201">Cost-based optimization (CBO) evaluates multiple plans to execute a query and assigns a cost to each plan, then determines the cheapest plan to execute a query.</span></span>

<span data-ttu-id="b94a8-202">To enable CBO, navigate to the Hive **Configs** tab and search for `parameter hive.cbo.enable`, then switch the toggle button to **On**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-202">To enable CBO, navigate to the Hive **Configs** tab and search for `parameter hive.cbo.enable`, then switch the toggle button to **On**.</span></span>

![CBO config](./media/hdinsight-changing-configs-via-ambari/cbo.png)

<span data-ttu-id="b94a8-204">The following additional configuration parameters increase Hive query performance when CBO is enabled:</span><span class="sxs-lookup"><span data-stu-id="b94a8-204">The following additional configuration parameters increase Hive query performance when CBO is enabled:</span></span>

* `hive.compute.query.using.stats`

    <span data-ttu-id="b94a8-205">When set to true, Hive uses statistics stored in its metastore to answer simple queries like `count(*)`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-205">When set to true, Hive uses statistics stored in its metastore to answer simple queries like `count(*)`.</span></span>

    ![CBO stats](./media/hdinsight-changing-configs-via-ambari/hive-compute-query-using-stats.png)

* `hive.stats.fetch.column.stats`

    <span data-ttu-id="b94a8-207">Column statistics are created when CBO is enabled.</span><span class="sxs-lookup"><span data-stu-id="b94a8-207">Column statistics are created when CBO is enabled.</span></span> <span data-ttu-id="b94a8-208">Hive uses column statistics, which are stored in metastore, to optimize queries.</span><span class="sxs-lookup"><span data-stu-id="b94a8-208">Hive uses column statistics, which are stored in metastore, to optimize queries.</span></span> <span data-ttu-id="b94a8-209">Fetching column statistics for each column takes longer when the number of columns is high.</span><span class="sxs-lookup"><span data-stu-id="b94a8-209">Fetching column statistics for each column takes longer when the number of columns is high.</span></span> <span data-ttu-id="b94a8-210">When set to false, this setting disables fetching column statistics from the metastore.</span><span class="sxs-lookup"><span data-stu-id="b94a8-210">When set to false, this setting disables fetching column statistics from the metastore.</span></span>

    ![Hive stats set column stats](./media/hdinsight-changing-configs-via-ambari/hive-stats-fetch-column-stats.png)

* `hive.stats.fetch.partition.stats`

    <span data-ttu-id="b94a8-212">Basic partition statistics such as number of rows, data size, and file size are stored in metastore.</span><span class="sxs-lookup"><span data-stu-id="b94a8-212">Basic partition statistics such as number of rows, data size, and file size are stored in metastore.</span></span> <span data-ttu-id="b94a8-213">When set to true, the partition stats are fetched from metastore.</span><span class="sxs-lookup"><span data-stu-id="b94a8-213">When set to true, the partition stats are fetched from metastore.</span></span> <span data-ttu-id="b94a8-214">When false, the file size is fetched from the file system, and the number of rows is fetched from the row schema.</span><span class="sxs-lookup"><span data-stu-id="b94a8-214">When false, the file size is fetched from the file system, and the number of rows is fetched from the row schema.</span></span>

    ![Hive stats set partition stats](./media/hdinsight-changing-configs-via-ambari/hive-stats-fetch-partition-stats.png)

### <a name="enable-intermediate-compression"></a><span data-ttu-id="b94a8-216">Enable intermediate compression</span><span class="sxs-lookup"><span data-stu-id="b94a8-216">Enable intermediate compression</span></span>

<span data-ttu-id="b94a8-217">Map tasks create intermediate files that are used by the reducer tasks.</span><span class="sxs-lookup"><span data-stu-id="b94a8-217">Map tasks create intermediate files that are used by the reducer tasks.</span></span> <span data-ttu-id="b94a8-218">Intermediate compression shrinks the intermediate file size.</span><span class="sxs-lookup"><span data-stu-id="b94a8-218">Intermediate compression shrinks the intermediate file size.</span></span>

<span data-ttu-id="b94a8-219">Hadoop jobs are usually I/O bottlenecked.</span><span class="sxs-lookup"><span data-stu-id="b94a8-219">Hadoop jobs are usually I/O bottlenecked.</span></span> <span data-ttu-id="b94a8-220">Compressing data can speed up I/O and overall network transfer.</span><span class="sxs-lookup"><span data-stu-id="b94a8-220">Compressing data can speed up I/O and overall network transfer.</span></span>

<span data-ttu-id="b94a8-221">The available compression types are:</span><span class="sxs-lookup"><span data-stu-id="b94a8-221">The available compression types are:</span></span>

| <span data-ttu-id="b94a8-222">Format</span><span class="sxs-lookup"><span data-stu-id="b94a8-222">Format</span></span> | <span data-ttu-id="b94a8-223">Tool</span><span class="sxs-lookup"><span data-stu-id="b94a8-223">Tool</span></span> | <span data-ttu-id="b94a8-224">Algorithm</span><span class="sxs-lookup"><span data-stu-id="b94a8-224">Algorithm</span></span> | <span data-ttu-id="b94a8-225">File Extension</span><span class="sxs-lookup"><span data-stu-id="b94a8-225">File Extension</span></span> | <span data-ttu-id="b94a8-226">Splittable?</span><span class="sxs-lookup"><span data-stu-id="b94a8-226">Splittable?</span></span> |
| -- | -- | -- | -- | -- |
| <span data-ttu-id="b94a8-227">Gzip</span><span class="sxs-lookup"><span data-stu-id="b94a8-227">Gzip</span></span> | <span data-ttu-id="b94a8-228">Gzip</span><span class="sxs-lookup"><span data-stu-id="b94a8-228">Gzip</span></span> | <span data-ttu-id="b94a8-229">DEFLATE</span><span class="sxs-lookup"><span data-stu-id="b94a8-229">DEFLATE</span></span> | <span data-ttu-id="b94a8-230">.gz</span><span class="sxs-lookup"><span data-stu-id="b94a8-230">.gz</span></span> | <span data-ttu-id="b94a8-231">No</span><span class="sxs-lookup"><span data-stu-id="b94a8-231">No</span></span> |
| <span data-ttu-id="b94a8-232">Bzip2</span><span class="sxs-lookup"><span data-stu-id="b94a8-232">Bzip2</span></span> | <span data-ttu-id="b94a8-233">Bzip2</span><span class="sxs-lookup"><span data-stu-id="b94a8-233">Bzip2</span></span> | <span data-ttu-id="b94a8-234">Bzip2</span><span class="sxs-lookup"><span data-stu-id="b94a8-234">Bzip2</span></span> |<span data-ttu-id="b94a8-235">.bz2</span><span class="sxs-lookup"><span data-stu-id="b94a8-235">.bz2</span></span> | <span data-ttu-id="b94a8-236">Yes</span><span class="sxs-lookup"><span data-stu-id="b94a8-236">Yes</span></span> |
| <span data-ttu-id="b94a8-237">LZO</span><span class="sxs-lookup"><span data-stu-id="b94a8-237">LZO</span></span> | <span data-ttu-id="b94a8-238">Lzop</span><span class="sxs-lookup"><span data-stu-id="b94a8-238">Lzop</span></span> | <span data-ttu-id="b94a8-239">LZO</span><span class="sxs-lookup"><span data-stu-id="b94a8-239">LZO</span></span> | <span data-ttu-id="b94a8-240">.lzo</span><span class="sxs-lookup"><span data-stu-id="b94a8-240">.lzo</span></span> | <span data-ttu-id="b94a8-241">Yes, if indexed</span><span class="sxs-lookup"><span data-stu-id="b94a8-241">Yes, if indexed</span></span> |
| <span data-ttu-id="b94a8-242">Snappy</span><span class="sxs-lookup"><span data-stu-id="b94a8-242">Snappy</span></span> | <span data-ttu-id="b94a8-243">N/A</span><span class="sxs-lookup"><span data-stu-id="b94a8-243">N/A</span></span> | <span data-ttu-id="b94a8-244">Snappy</span><span class="sxs-lookup"><span data-stu-id="b94a8-244">Snappy</span></span> | <span data-ttu-id="b94a8-245">Snappy</span><span class="sxs-lookup"><span data-stu-id="b94a8-245">Snappy</span></span> | <span data-ttu-id="b94a8-246">No</span><span class="sxs-lookup"><span data-stu-id="b94a8-246">No</span></span> |

<span data-ttu-id="b94a8-247">As a general rule, having the compression method splittable is important, otherwise very few mappers will be created.</span><span class="sxs-lookup"><span data-stu-id="b94a8-247">As a general rule, having the compression method splittable is important, otherwise very few mappers will be created.</span></span> <span data-ttu-id="b94a8-248">If the input data is text, `bzip2` is the best option.</span><span class="sxs-lookup"><span data-stu-id="b94a8-248">If the input data is text, `bzip2` is the best option.</span></span> <span data-ttu-id="b94a8-249">For ORC format, Snappy is the fastest compression option.</span><span class="sxs-lookup"><span data-stu-id="b94a8-249">For ORC format, Snappy is the fastest compression option.</span></span>

1. <span data-ttu-id="b94a8-250">To enable intermediate compression, navigate to the Hive **Configs** tab, and then set the `hive.exec.compress.intermediate` parameter to true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-250">To enable intermediate compression, navigate to the Hive **Configs** tab, and then set the `hive.exec.compress.intermediate` parameter to true.</span></span> <span data-ttu-id="b94a8-251">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-251">The default value is false.</span></span>

    ![Hive exec compress intermediate](./media/hdinsight-changing-configs-via-ambari/hive-exec-compress-intermediate.png)

    > [!NOTE]
    > <span data-ttu-id="b94a8-253">To compress intermediate files, choose a compression codec with lower CPU cost, even if the codec doesn't have a high compression output.</span><span class="sxs-lookup"><span data-stu-id="b94a8-253">To compress intermediate files, choose a compression codec with lower CPU cost, even if the codec doesn't have a high compression output.</span></span>

1. <span data-ttu-id="b94a8-254">To set the intermediate compression codec, add the custom property `mapred.map.output.compression.codec` to the `hive-site.xml` or `mapred-site.xml` file.</span><span class="sxs-lookup"><span data-stu-id="b94a8-254">To set the intermediate compression codec, add the custom property `mapred.map.output.compression.codec` to the `hive-site.xml` or `mapred-site.xml` file.</span></span>

1. <span data-ttu-id="b94a8-255">To add a custom setting:</span><span class="sxs-lookup"><span data-stu-id="b94a8-255">To add a custom setting:</span></span>

    <span data-ttu-id="b94a8-256">a.</span><span class="sxs-lookup"><span data-stu-id="b94a8-256">a.</span></span> <span data-ttu-id="b94a8-257">Navigate to the Hive **Configs** tab and select the **Advanced** tab.</span><span class="sxs-lookup"><span data-stu-id="b94a8-257">Navigate to the Hive **Configs** tab and select the **Advanced** tab.</span></span>

    <span data-ttu-id="b94a8-258">b.</span><span class="sxs-lookup"><span data-stu-id="b94a8-258">b.</span></span> <span data-ttu-id="b94a8-259">Under the **Advanced** tab, find and expand the **Custom hive-site** pane.</span><span class="sxs-lookup"><span data-stu-id="b94a8-259">Under the **Advanced** tab, find and expand the **Custom hive-site** pane.</span></span>

    <span data-ttu-id="b94a8-260">c.</span><span class="sxs-lookup"><span data-stu-id="b94a8-260">c.</span></span> <span data-ttu-id="b94a8-261">Click the link **Add Property** at the bottom of the Custom hive-site pane.</span><span class="sxs-lookup"><span data-stu-id="b94a8-261">Click the link **Add Property** at the bottom of the Custom hive-site pane.</span></span>

    <span data-ttu-id="b94a8-262">d.</span><span class="sxs-lookup"><span data-stu-id="b94a8-262">d.</span></span> <span data-ttu-id="b94a8-263">In the Add Property window, enter `mapred.map.output.compression.codec` as the key and `org.apache.hadoop.io.compress.SnappyCodec` as the value.</span><span class="sxs-lookup"><span data-stu-id="b94a8-263">In the Add Property window, enter `mapred.map.output.compression.codec` as the key and `org.apache.hadoop.io.compress.SnappyCodec` as the value.</span></span>

    <span data-ttu-id="b94a8-264">e.</span><span class="sxs-lookup"><span data-stu-id="b94a8-264">e.</span></span> <span data-ttu-id="b94a8-265">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-265">Click **Add**.</span></span>

    ![Hive custom property](./media/hdinsight-changing-configs-via-ambari/hive-custom-property.png)

    <span data-ttu-id="b94a8-267">This will compress the intermediate file using Snappy compression.</span><span class="sxs-lookup"><span data-stu-id="b94a8-267">This will compress the intermediate file using Snappy compression.</span></span> <span data-ttu-id="b94a8-268">Once the property is added, it appears in the Custom hive-site pane.</span><span class="sxs-lookup"><span data-stu-id="b94a8-268">Once the property is added, it appears in the Custom hive-site pane.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b94a8-269">This procedure modifies the `$HADOOP_HOME/conf/hive-site.xml` file.</span><span class="sxs-lookup"><span data-stu-id="b94a8-269">This procedure modifies the `$HADOOP_HOME/conf/hive-site.xml` file.</span></span>

### <a name="compress-final-output"></a><span data-ttu-id="b94a8-270">Compress final output</span><span class="sxs-lookup"><span data-stu-id="b94a8-270">Compress final output</span></span>

<span data-ttu-id="b94a8-271">The final Hive output can also be compressed.</span><span class="sxs-lookup"><span data-stu-id="b94a8-271">The final Hive output can also be compressed.</span></span>

1. <span data-ttu-id="b94a8-272">To compress the final Hive output, navigate to the Hive **Configs** tab, and then set the `hive.exec.compress.output` parameter to true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-272">To compress the final Hive output, navigate to the Hive **Configs** tab, and then set the `hive.exec.compress.output` parameter to true.</span></span> <span data-ttu-id="b94a8-273">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-273">The default value is false.</span></span>

1. <span data-ttu-id="b94a8-274">To choose the output compression codec, add the `mapred.output.compression.codec` custom property to the Custom hive-site pane, as described in the previous section's step 3.</span><span class="sxs-lookup"><span data-stu-id="b94a8-274">To choose the output compression codec, add the `mapred.output.compression.codec` custom property to the Custom hive-site pane, as described in the previous section's step 3.</span></span>

    ![Hive custom property](./media/hdinsight-changing-configs-via-ambari/hive-custom-property2.png)

### <a name="enable-speculative-execution"></a><span data-ttu-id="b94a8-276">Enable speculative execution</span><span class="sxs-lookup"><span data-stu-id="b94a8-276">Enable speculative execution</span></span>

<span data-ttu-id="b94a8-277">Speculative execution launches a certain number of duplicate tasks in order to detect and blacklist the slow-running task tracker, while improving the overall job execution by optimizing individual task results.</span><span class="sxs-lookup"><span data-stu-id="b94a8-277">Speculative execution launches a certain number of duplicate tasks in order to detect and blacklist the slow-running task tracker, while improving the overall job execution by optimizing individual task results.</span></span>

<span data-ttu-id="b94a8-278">Speculative execution shouldn't be turned on for long-running MapReduce tasks with large amounts of input.</span><span class="sxs-lookup"><span data-stu-id="b94a8-278">Speculative execution shouldn't be turned on for long-running MapReduce tasks with large amounts of input.</span></span>

* <span data-ttu-id="b94a8-279">To enable speculative execution, navigate to the Hive **Configs** tab, and then set the `hive.mapred.reduce.tasks.speculative.execution` parameter to true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-279">To enable speculative execution, navigate to the Hive **Configs** tab, and then set the `hive.mapred.reduce.tasks.speculative.execution` parameter to true.</span></span> <span data-ttu-id="b94a8-280">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-280">The default value is false.</span></span>

    ![Hive mapred reduce tasks speculative execution](./media/hdinsight-changing-configs-via-ambari/hive-mapred-reduce-tasks-speculative-execution.png)

### <a name="tune-dynamic-partitions"></a><span data-ttu-id="b94a8-282">Tune dynamic partitions</span><span class="sxs-lookup"><span data-stu-id="b94a8-282">Tune dynamic partitions</span></span>

<span data-ttu-id="b94a8-283">Hive allows for creating dynamic partitions when inserting records into a table, without predefining each and every partition.</span><span class="sxs-lookup"><span data-stu-id="b94a8-283">Hive allows for creating dynamic partitions when inserting records into a table, without predefining each and every partition.</span></span> <span data-ttu-id="b94a8-284">This is a powerful feature, although it may result in the creation of a large number of partitions and a large number of files for each partition.</span><span class="sxs-lookup"><span data-stu-id="b94a8-284">This is a powerful feature, although it may result in the creation of a large number of partitions and a large number of files for each partition.</span></span>

1. <span data-ttu-id="b94a8-285">For Hive to do dynamic partitions, the `hive.exec.dynamic.partition` parameter value should be true (the  default).</span><span class="sxs-lookup"><span data-stu-id="b94a8-285">For Hive to do dynamic partitions, the `hive.exec.dynamic.partition` parameter value should be true (the  default).</span></span>

1. <span data-ttu-id="b94a8-286">Change the dynamic partition mode to *strict*.</span><span class="sxs-lookup"><span data-stu-id="b94a8-286">Change the dynamic partition mode to *strict*.</span></span> <span data-ttu-id="b94a8-287">In strict mode, at least one partition has to be static.</span><span class="sxs-lookup"><span data-stu-id="b94a8-287">In strict mode, at least one partition has to be static.</span></span> <span data-ttu-id="b94a8-288">This prevents queries without the partition filter in the WHERE clause, that is, *strict* prevents queries that scan all partitions.</span><span class="sxs-lookup"><span data-stu-id="b94a8-288">This prevents queries without the partition filter in the WHERE clause, that is, *strict* prevents queries that scan all partitions.</span></span> <span data-ttu-id="b94a8-289">Navigate to the Hive **Configs** tab, and then set `hive.exec.dynamic.partition.mode` to **strict**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-289">Navigate to the Hive **Configs** tab, and then set `hive.exec.dynamic.partition.mode` to **strict**.</span></span> <span data-ttu-id="b94a8-290">The default value is **nonstrict**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-290">The default value is **nonstrict**.</span></span>
 
1. <span data-ttu-id="b94a8-291">To limit the number of dynamic partitions to be created, modify the `hive.exec.max.dynamic.partitions` parameter.</span><span class="sxs-lookup"><span data-stu-id="b94a8-291">To limit the number of dynamic partitions to be created, modify the `hive.exec.max.dynamic.partitions` parameter.</span></span> <span data-ttu-id="b94a8-292">The default value is 5000.</span><span class="sxs-lookup"><span data-stu-id="b94a8-292">The default value is 5000.</span></span>
 
1. <span data-ttu-id="b94a8-293">To limit the total number of dynamic partitions per node, modify `hive.exec.max.dynamic.partitions.pernode`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-293">To limit the total number of dynamic partitions per node, modify `hive.exec.max.dynamic.partitions.pernode`.</span></span> <span data-ttu-id="b94a8-294">The default value is 2000.</span><span class="sxs-lookup"><span data-stu-id="b94a8-294">The default value is 2000.</span></span>

### <a name="enable-local-mode"></a><span data-ttu-id="b94a8-295">Enable local mode</span><span class="sxs-lookup"><span data-stu-id="b94a8-295">Enable local mode</span></span>

<span data-ttu-id="b94a8-296">Local mode enables Hive to perform all tasks of a job on a single machine, or sometimes in a single process.</span><span class="sxs-lookup"><span data-stu-id="b94a8-296">Local mode enables Hive to perform all tasks of a job on a single machine, or sometimes in a single process.</span></span> <span data-ttu-id="b94a8-297">This improves query performance if the input data is small and the overhead of launching tasks for queries consumes a significant percentage of the overall query execution.</span><span class="sxs-lookup"><span data-stu-id="b94a8-297">This improves query performance if the input data is small and the overhead of launching tasks for queries consumes a significant percentage of the overall query execution.</span></span>

<span data-ttu-id="b94a8-298">To enable local mode, add the `hive.exec.mode.local.auto` parameter to the Custom hive-site panel, as explained in step 3 of the [Enable intermediate compression](#enable-intermediate-compression) section.</span><span class="sxs-lookup"><span data-stu-id="b94a8-298">To enable local mode, add the `hive.exec.mode.local.auto` parameter to the Custom hive-site panel, as explained in step 3 of the [Enable intermediate compression](#enable-intermediate-compression) section.</span></span>

![Hive exec mode local auto](./media/hdinsight-changing-configs-via-ambari/hive-exec-mode-local-auto.png)

### <a name="set-single-mapreduce-multigroup-by"></a><span data-ttu-id="b94a8-300">Set single MapReduce MultiGROUP BY</span><span class="sxs-lookup"><span data-stu-id="b94a8-300">Set single MapReduce MultiGROUP BY</span></span>

<span data-ttu-id="b94a8-301">When this property is set to true, a MultiGROUP BY query with common group-by keys  generates a single MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="b94a8-301">When this property is set to true, a MultiGROUP BY query with common group-by keys  generates a single MapReduce job.</span></span>  

<span data-ttu-id="b94a8-302">To enable this behavior, add the `hive.multigroupby.singlereducer` parameter to the Custom hive-site pane, as explained in step 3 of the [Enable intermediate compression](#enable-intermediate-compression) section.</span><span class="sxs-lookup"><span data-stu-id="b94a8-302">To enable this behavior, add the `hive.multigroupby.singlereducer` parameter to the Custom hive-site pane, as explained in step 3 of the [Enable intermediate compression](#enable-intermediate-compression) section.</span></span>

![Hive set single MapReduce MultiGROUP BY](./media/hdinsight-changing-configs-via-ambari/hive-multigroupby-singlereducer.png)

### <a name="additional-hive-optimizations"></a><span data-ttu-id="b94a8-304">Additional Hive optimizations</span><span class="sxs-lookup"><span data-stu-id="b94a8-304">Additional Hive optimizations</span></span>

<span data-ttu-id="b94a8-305">The following sections describe additional Hive-related optimizations you can set.</span><span class="sxs-lookup"><span data-stu-id="b94a8-305">The following sections describe additional Hive-related optimizations you can set.</span></span>

#### <a name="join-optimizations"></a><span data-ttu-id="b94a8-306">Join optimizations</span><span class="sxs-lookup"><span data-stu-id="b94a8-306">Join optimizations</span></span>

<span data-ttu-id="b94a8-307">The default join type in Hive is a *shuffle join*.</span><span class="sxs-lookup"><span data-stu-id="b94a8-307">The default join type in Hive is a *shuffle join*.</span></span> <span data-ttu-id="b94a8-308">In Hive,  special mappers read the input and emit a join key/value pair to an intermediate file.</span><span class="sxs-lookup"><span data-stu-id="b94a8-308">In Hive,  special mappers read the input and emit a join key/value pair to an intermediate file.</span></span> <span data-ttu-id="b94a8-309">Hadoop sorts and merges these pairs in a shuffle stage.</span><span class="sxs-lookup"><span data-stu-id="b94a8-309">Hadoop sorts and merges these pairs in a shuffle stage.</span></span> <span data-ttu-id="b94a8-310">This shuffle stage is expensive.</span><span class="sxs-lookup"><span data-stu-id="b94a8-310">This shuffle stage is expensive.</span></span> <span data-ttu-id="b94a8-311">Selecting the right join based on your data can significantly improve performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-311">Selecting the right join based on your data can significantly improve performance.</span></span>

| <span data-ttu-id="b94a8-312">Join Type</span><span class="sxs-lookup"><span data-stu-id="b94a8-312">Join Type</span></span> | <span data-ttu-id="b94a8-313">When</span><span class="sxs-lookup"><span data-stu-id="b94a8-313">When</span></span> | <span data-ttu-id="b94a8-314">How</span><span class="sxs-lookup"><span data-stu-id="b94a8-314">How</span></span> | <span data-ttu-id="b94a8-315">Hive settings</span><span class="sxs-lookup"><span data-stu-id="b94a8-315">Hive settings</span></span> | <span data-ttu-id="b94a8-316">Comments</span><span class="sxs-lookup"><span data-stu-id="b94a8-316">Comments</span></span> |
| -- | -- | -- | -- | -- |
| <span data-ttu-id="b94a8-317">Shuffle Join</span><span class="sxs-lookup"><span data-stu-id="b94a8-317">Shuffle Join</span></span> | <ul><li><span data-ttu-id="b94a8-318">Default choice</span><span class="sxs-lookup"><span data-stu-id="b94a8-318">Default choice</span></span></li><li><span data-ttu-id="b94a8-319">Always works</span><span class="sxs-lookup"><span data-stu-id="b94a8-319">Always works</span></span></li></ul> | <ul><li><span data-ttu-id="b94a8-320">Reads from part of one of the tables</span><span class="sxs-lookup"><span data-stu-id="b94a8-320">Reads from part of one of the tables</span></span></li><li><span data-ttu-id="b94a8-321">Buckets and sorts on Join key</span><span class="sxs-lookup"><span data-stu-id="b94a8-321">Buckets and sorts on Join key</span></span></li><li><span data-ttu-id="b94a8-322">Sends one bucket to each reduce</span><span class="sxs-lookup"><span data-stu-id="b94a8-322">Sends one bucket to each reduce</span></span></li><li><span data-ttu-id="b94a8-323">Join is done on the Reduce side</span><span class="sxs-lookup"><span data-stu-id="b94a8-323">Join is done on the Reduce side</span></span></li></ul> | <span data-ttu-id="b94a8-324">No significant Hive setting needed</span><span class="sxs-lookup"><span data-stu-id="b94a8-324">No significant Hive setting needed</span></span> | <span data-ttu-id="b94a8-325">Works every time</span><span class="sxs-lookup"><span data-stu-id="b94a8-325">Works every time</span></span> |
| <span data-ttu-id="b94a8-326">Map Join</span><span class="sxs-lookup"><span data-stu-id="b94a8-326">Map Join</span></span> | <ul><li><span data-ttu-id="b94a8-327">One table can fit in memory</span><span class="sxs-lookup"><span data-stu-id="b94a8-327">One table can fit in memory</span></span></li></ul> | <ul><li><span data-ttu-id="b94a8-328">Reads small table into memory hash table</span><span class="sxs-lookup"><span data-stu-id="b94a8-328">Reads small table into memory hash table</span></span></li><li><span data-ttu-id="b94a8-329">Streams through part of the large file</span><span class="sxs-lookup"><span data-stu-id="b94a8-329">Streams through part of the large file</span></span></li><li><span data-ttu-id="b94a8-330">Joins each record from hash table</span><span class="sxs-lookup"><span data-stu-id="b94a8-330">Joins each record from hash table</span></span></li><li><span data-ttu-id="b94a8-331">Joins are by the mapper alone</span><span class="sxs-lookup"><span data-stu-id="b94a8-331">Joins are by the mapper alone</span></span></li></ul> | `hive.auto.confvert.join=true` | <span data-ttu-id="b94a8-332">Very fast, but limited</span><span class="sxs-lookup"><span data-stu-id="b94a8-332">Very fast, but limited</span></span> |
| <span data-ttu-id="b94a8-333">Sort Merge Bucket</span><span class="sxs-lookup"><span data-stu-id="b94a8-333">Sort Merge Bucket</span></span> | <span data-ttu-id="b94a8-334">If both tables are:</span><span class="sxs-lookup"><span data-stu-id="b94a8-334">If both tables are:</span></span> <ul><li><span data-ttu-id="b94a8-335">Sorted the same</span><span class="sxs-lookup"><span data-stu-id="b94a8-335">Sorted the same</span></span></li><li><span data-ttu-id="b94a8-336">Bucketed the same</span><span class="sxs-lookup"><span data-stu-id="b94a8-336">Bucketed the same</span></span></li><li><span data-ttu-id="b94a8-337">Joining on the sorted/bucketed column</span><span class="sxs-lookup"><span data-stu-id="b94a8-337">Joining on the sorted/bucketed column</span></span></li></ul> | <span data-ttu-id="b94a8-338">Each process:</span><span class="sxs-lookup"><span data-stu-id="b94a8-338">Each process:</span></span> <ul><li><span data-ttu-id="b94a8-339">Reads a bucket from each table</span><span class="sxs-lookup"><span data-stu-id="b94a8-339">Reads a bucket from each table</span></span></li><li><span data-ttu-id="b94a8-340">Processes the row with the lowest value</span><span class="sxs-lookup"><span data-stu-id="b94a8-340">Processes the row with the lowest value</span></span></li></ul> | `hive.auto.convert.sortmerge.join=true` | <span data-ttu-id="b94a8-341">Very efficient</span><span class="sxs-lookup"><span data-stu-id="b94a8-341">Very efficient</span></span> |

#### <a name="execution-engine-optimizations"></a><span data-ttu-id="b94a8-342">Execution engine optimizations</span><span class="sxs-lookup"><span data-stu-id="b94a8-342">Execution engine optimizations</span></span>

<span data-ttu-id="b94a8-343">Additional recommendations for optimizing the Hive execution engine:</span><span class="sxs-lookup"><span data-stu-id="b94a8-343">Additional recommendations for optimizing the Hive execution engine:</span></span>

| <span data-ttu-id="b94a8-344">Setting</span><span class="sxs-lookup"><span data-stu-id="b94a8-344">Setting</span></span> | <span data-ttu-id="b94a8-345">Recommended</span><span class="sxs-lookup"><span data-stu-id="b94a8-345">Recommended</span></span> | <span data-ttu-id="b94a8-346">HDInsight Default</span><span class="sxs-lookup"><span data-stu-id="b94a8-346">HDInsight Default</span></span> |
| -- | -- | -- |
| `hive.mapjoin.hybridgrace.hashtable` | <span data-ttu-id="b94a8-347">True = safer, slower; false = faster</span><span class="sxs-lookup"><span data-stu-id="b94a8-347">True = safer, slower; false = faster</span></span> | <span data-ttu-id="b94a8-348">false</span><span class="sxs-lookup"><span data-stu-id="b94a8-348">false</span></span> |
| `tez.am.resource.memory.mb` | <span data-ttu-id="b94a8-349">4 GB upper bound for most</span><span class="sxs-lookup"><span data-stu-id="b94a8-349">4 GB upper bound for most</span></span> | <span data-ttu-id="b94a8-350">Auto-Tuned</span><span class="sxs-lookup"><span data-stu-id="b94a8-350">Auto-Tuned</span></span> |
| `tez.session.am.dag.submit.timeout.secs` | <span data-ttu-id="b94a8-351">300+</span><span class="sxs-lookup"><span data-stu-id="b94a8-351">300+</span></span> | <span data-ttu-id="b94a8-352">300</span><span class="sxs-lookup"><span data-stu-id="b94a8-352">300</span></span> |
| `tez.am.container.idle.release-timeout-min.millis` | <span data-ttu-id="b94a8-353">20000+</span><span class="sxs-lookup"><span data-stu-id="b94a8-353">20000+</span></span> | <span data-ttu-id="b94a8-354">10000</span><span class="sxs-lookup"><span data-stu-id="b94a8-354">10000</span></span> |
| `tez.am.container.idle.release-timeout-max.millis` | <span data-ttu-id="b94a8-355">40000+</span><span class="sxs-lookup"><span data-stu-id="b94a8-355">40000+</span></span> | <span data-ttu-id="b94a8-356">20000</span><span class="sxs-lookup"><span data-stu-id="b94a8-356">20000</span></span> |

## <a name="pig-optimization"></a><span data-ttu-id="b94a8-357">Pig optimization</span><span class="sxs-lookup"><span data-stu-id="b94a8-357">Pig optimization</span></span>

<span data-ttu-id="b94a8-358">Pig properties can be  modified from the Ambari web UI to tune Pig queries.</span><span class="sxs-lookup"><span data-stu-id="b94a8-358">Pig properties can be  modified from the Ambari web UI to tune Pig queries.</span></span> <span data-ttu-id="b94a8-359">Modifying Pig properties from Ambari directly modifies the Pig properties in the `/etc/pig/2.4.2.0-258.0/pig.properties` file.</span><span class="sxs-lookup"><span data-stu-id="b94a8-359">Modifying Pig properties from Ambari directly modifies the Pig properties in the `/etc/pig/2.4.2.0-258.0/pig.properties` file.</span></span>

1. <span data-ttu-id="b94a8-360">To modify Pig properties, navigate to the Pig **Configs** tab, and then expand the **Advanced pig-properties** pane.</span><span class="sxs-lookup"><span data-stu-id="b94a8-360">To modify Pig properties, navigate to the Pig **Configs** tab, and then expand the **Advanced pig-properties** pane.</span></span>

1. <span data-ttu-id="b94a8-361">Find, uncomment, and change the value of the property you wish to modify.</span><span class="sxs-lookup"><span data-stu-id="b94a8-361">Find, uncomment, and change the value of the property you wish to modify.</span></span>

1. <span data-ttu-id="b94a8-362">Select **Save** on the top right side of the window to save the new value.</span><span class="sxs-lookup"><span data-stu-id="b94a8-362">Select **Save** on the top right side of the window to save the new value.</span></span> <span data-ttu-id="b94a8-363">Some properties may require a service restart.</span><span class="sxs-lookup"><span data-stu-id="b94a8-363">Some properties may require a service restart.</span></span>

    ![Advanced pig-properties](./media/hdinsight-changing-configs-via-ambari/advanced-pig-properties.png)
 
> [!NOTE]
> <span data-ttu-id="b94a8-365">Any session-level settings override property values in the `pig.properties` file.</span><span class="sxs-lookup"><span data-stu-id="b94a8-365">Any session-level settings override property values in the `pig.properties` file.</span></span>

### <a name="tune-execution-engine"></a><span data-ttu-id="b94a8-366">Tune execution engine</span><span class="sxs-lookup"><span data-stu-id="b94a8-366">Tune execution engine</span></span>

<span data-ttu-id="b94a8-367">Two execution engines are available to execute Pig scripts: MapReduce and Tez.</span><span class="sxs-lookup"><span data-stu-id="b94a8-367">Two execution engines are available to execute Pig scripts: MapReduce and Tez.</span></span> <span data-ttu-id="b94a8-368">Tez is an optimized engine and is much faster than MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b94a8-368">Tez is an optimized engine and is much faster than MapReduce.</span></span>

1. <span data-ttu-id="b94a8-369">To modify the execution engine, in the **Advanced pig-properties** pane, find the property `exectype`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-369">To modify the execution engine, in the **Advanced pig-properties** pane, find the property `exectype`.</span></span>

1. <span data-ttu-id="b94a8-370">The default value is **MapReduce**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-370">The default value is **MapReduce**.</span></span> <span data-ttu-id="b94a8-371">Change it to **Tez**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-371">Change it to **Tez**.</span></span>


### <a name="enable-local-mode"></a><span data-ttu-id="b94a8-372">Enable local mode</span><span class="sxs-lookup"><span data-stu-id="b94a8-372">Enable local mode</span></span>

<span data-ttu-id="b94a8-373">Similar to Hive, local mode is used to speed jobs with relatively smaller amounts of data.</span><span class="sxs-lookup"><span data-stu-id="b94a8-373">Similar to Hive, local mode is used to speed jobs with relatively smaller amounts of data.</span></span>

1. <span data-ttu-id="b94a8-374">To enable the local mode, set `pig.auto.local.enabled` to **true**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-374">To enable the local mode, set `pig.auto.local.enabled` to **true**.</span></span> <span data-ttu-id="b94a8-375">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-375">The default value is false.</span></span>

1. <span data-ttu-id="b94a8-376">Jobs with an input data size less than the `pig.auto.local.input.maxbytes` property value are considered to be small jobs.</span><span class="sxs-lookup"><span data-stu-id="b94a8-376">Jobs with an input data size less than the `pig.auto.local.input.maxbytes` property value are considered to be small jobs.</span></span> <span data-ttu-id="b94a8-377">The default value is 1 GB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-377">The default value is 1 GB.</span></span>


### <a name="copy-user-jar-cache"></a><span data-ttu-id="b94a8-378">Copy user jar cache</span><span class="sxs-lookup"><span data-stu-id="b94a8-378">Copy user jar cache</span></span>

<span data-ttu-id="b94a8-379">Pig copies the JAR files required by UDFs to a distributed cache  to make them available for task nodes.</span><span class="sxs-lookup"><span data-stu-id="b94a8-379">Pig copies the JAR files required by UDFs to a distributed cache  to make them available for task nodes.</span></span> <span data-ttu-id="b94a8-380">These jars do not change frequently.</span><span class="sxs-lookup"><span data-stu-id="b94a8-380">These jars do not change frequently.</span></span> <span data-ttu-id="b94a8-381">If enabled, the `pig.user.cache.enabled` setting allows jars to be placed in a cache to reuse them for jobs run by the same user.</span><span class="sxs-lookup"><span data-stu-id="b94a8-381">If enabled, the `pig.user.cache.enabled` setting allows jars to be placed in a cache to reuse them for jobs run by the same user.</span></span> <span data-ttu-id="b94a8-382">This results in a minor increase in job performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-382">This results in a minor increase in job performance.</span></span>

1. <span data-ttu-id="b94a8-383">To enable, set `pig.user.cache.enabled` to true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-383">To enable, set `pig.user.cache.enabled` to true.</span></span> <span data-ttu-id="b94a8-384">The default is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-384">The default is false.</span></span>

1. <span data-ttu-id="b94a8-385">To set the base path of the cached jars, set `pig.user.cache.location` to the base path.</span><span class="sxs-lookup"><span data-stu-id="b94a8-385">To set the base path of the cached jars, set `pig.user.cache.location` to the base path.</span></span> <span data-ttu-id="b94a8-386">The default is `/tmp`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-386">The default is `/tmp`.</span></span>


### <a name="optimize-performance-with-memory-settings"></a><span data-ttu-id="b94a8-387">Optimize performance with memory settings</span><span class="sxs-lookup"><span data-stu-id="b94a8-387">Optimize performance with memory settings</span></span>

<span data-ttu-id="b94a8-388">The following memory settings can help optimize Pig script performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-388">The following memory settings can help optimize Pig script performance.</span></span>

* <span data-ttu-id="b94a8-389">`pig.cachedbag.memusage`: The amount of memory allocated to a bag.</span><span class="sxs-lookup"><span data-stu-id="b94a8-389">`pig.cachedbag.memusage`: The amount of memory allocated to a bag.</span></span> <span data-ttu-id="b94a8-390">A bag is collection of tuples.</span><span class="sxs-lookup"><span data-stu-id="b94a8-390">A bag is collection of tuples.</span></span> <span data-ttu-id="b94a8-391">A tuple is an ordered set of fields, and a field is a piece of data.</span><span class="sxs-lookup"><span data-stu-id="b94a8-391">A tuple is an ordered set of fields, and a field is a piece of data.</span></span> <span data-ttu-id="b94a8-392">If the data in a bag is beyond the allocated memory, it is spilled to disk.</span><span class="sxs-lookup"><span data-stu-id="b94a8-392">If the data in a bag is beyond the allocated memory, it is spilled to disk.</span></span> <span data-ttu-id="b94a8-393">The default value is 0.2, which represents 20 percent of available memory.</span><span class="sxs-lookup"><span data-stu-id="b94a8-393">The default value is 0.2, which represents 20 percent of available memory.</span></span> <span data-ttu-id="b94a8-394">This memory is shared across all bags in an application.</span><span class="sxs-lookup"><span data-stu-id="b94a8-394">This memory is shared across all bags in an application.</span></span>

* <span data-ttu-id="b94a8-395">`pig.spill.size.threshold`: Bags larger than this spill size threshold (in bytes) are  spilled to disk.</span><span class="sxs-lookup"><span data-stu-id="b94a8-395">`pig.spill.size.threshold`: Bags larger than this spill size threshold (in bytes) are  spilled to disk.</span></span> <span data-ttu-id="b94a8-396">The default value is 5 MB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-396">The default value is 5 MB.</span></span>


### <a name="compress-temporary-files"></a><span data-ttu-id="b94a8-397">Compress temporary files</span><span class="sxs-lookup"><span data-stu-id="b94a8-397">Compress temporary files</span></span>

<span data-ttu-id="b94a8-398">Pig generates temporary files during job execution.</span><span class="sxs-lookup"><span data-stu-id="b94a8-398">Pig generates temporary files during job execution.</span></span> <span data-ttu-id="b94a8-399">Compressing the temporary files results in a performance increase when reading or writing files to disk.</span><span class="sxs-lookup"><span data-stu-id="b94a8-399">Compressing the temporary files results in a performance increase when reading or writing files to disk.</span></span> <span data-ttu-id="b94a8-400">The following settings can be used to compress temporary files.</span><span class="sxs-lookup"><span data-stu-id="b94a8-400">The following settings can be used to compress temporary files.</span></span>

* <span data-ttu-id="b94a8-401">`pig.tmpfilecompression`: When true, enables temporary file compression.</span><span class="sxs-lookup"><span data-stu-id="b94a8-401">`pig.tmpfilecompression`: When true, enables temporary file compression.</span></span> <span data-ttu-id="b94a8-402">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-402">The default value is false.</span></span>

* <span data-ttu-id="b94a8-403">`pig.tmpfilecompression.codec`: The compression codec to use for compressing the temporary files.</span><span class="sxs-lookup"><span data-stu-id="b94a8-403">`pig.tmpfilecompression.codec`: The compression codec to use for compressing the temporary files.</span></span> <span data-ttu-id="b94a8-404">The recommended compression codecs are LZO and Snappy for lower CPU utilization.</span><span class="sxs-lookup"><span data-stu-id="b94a8-404">The recommended compression codecs are LZO and Snappy for lower CPU utilization.</span></span>

### <a name="enable-split-combining"></a><span data-ttu-id="b94a8-405">Enable split combining</span><span class="sxs-lookup"><span data-stu-id="b94a8-405">Enable split combining</span></span>

<span data-ttu-id="b94a8-406">When enabled, small files are combined for fewer map tasks.</span><span class="sxs-lookup"><span data-stu-id="b94a8-406">When enabled, small files are combined for fewer map tasks.</span></span> <span data-ttu-id="b94a8-407">This improves the efficiency of jobs with many small files.</span><span class="sxs-lookup"><span data-stu-id="b94a8-407">This improves the efficiency of jobs with many small files.</span></span> <span data-ttu-id="b94a8-408">To enable, set `pig.noSplitCombination` to true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-408">To enable, set `pig.noSplitCombination` to true.</span></span> <span data-ttu-id="b94a8-409">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b94a8-409">The default value is false.</span></span>


### <a name="tune-mappers"></a><span data-ttu-id="b94a8-410">Tune mappers</span><span class="sxs-lookup"><span data-stu-id="b94a8-410">Tune mappers</span></span>

<span data-ttu-id="b94a8-411">The number of mappers is controlled by modifying the property `pig.maxCombinedSplitSize`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-411">The number of mappers is controlled by modifying the property `pig.maxCombinedSplitSize`.</span></span> <span data-ttu-id="b94a8-412">This specifies the size of the data to be processed by a single map task.</span><span class="sxs-lookup"><span data-stu-id="b94a8-412">This specifies the size of the data to be processed by a single map task.</span></span> <span data-ttu-id="b94a8-413">The default value is the filesystem's default block size.</span><span class="sxs-lookup"><span data-stu-id="b94a8-413">The default value is the filesystem's default block size.</span></span> <span data-ttu-id="b94a8-414">Increasing this value results in a decrease of the number of mapper tasks.</span><span class="sxs-lookup"><span data-stu-id="b94a8-414">Increasing this value results in a decrease of the number of mapper tasks.</span></span>


### <a name="tune-reducers"></a><span data-ttu-id="b94a8-415">Tune reducers</span><span class="sxs-lookup"><span data-stu-id="b94a8-415">Tune reducers</span></span>

<span data-ttu-id="b94a8-416">The number of reducers is calculated based on the parameter `pig.exec.reducers.bytes.per.reducer`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-416">The number of reducers is calculated based on the parameter `pig.exec.reducers.bytes.per.reducer`.</span></span> <span data-ttu-id="b94a8-417">The parameter specifies the number of bytes processed per reducer, by default  1 GB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-417">The parameter specifies the number of bytes processed per reducer, by default  1 GB.</span></span> <span data-ttu-id="b94a8-418">To limit the maximum number of reducers, set the `pig.exec.reducers.max` property, by  default  999.</span><span class="sxs-lookup"><span data-stu-id="b94a8-418">To limit the maximum number of reducers, set the `pig.exec.reducers.max` property, by  default  999.</span></span>


## <a name="hbase-optimization-with-the-ambari-web-ui"></a><span data-ttu-id="b94a8-419">HBase optimization with the Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="b94a8-419">HBase optimization with the Ambari web UI</span></span>

<span data-ttu-id="b94a8-420">HBase configuration is modified from the **HBase Configs** tab. The following sections describe  some of the important configuration settings that affect HBase performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-420">HBase configuration is modified from the **HBase Configs** tab. The following sections describe  some of the important configuration settings that affect HBase performance.</span></span>

### <a name="set-hbaseheapsize"></a><span data-ttu-id="b94a8-421">Set HBASE_HEAPSIZE</span><span class="sxs-lookup"><span data-stu-id="b94a8-421">Set HBASE_HEAPSIZE</span></span>

<span data-ttu-id="b94a8-422">The HBase heap size specifies the maximum amount of heap to be used in megabytes by *region* and *master* servers.</span><span class="sxs-lookup"><span data-stu-id="b94a8-422">The HBase heap size specifies the maximum amount of heap to be used in megabytes by *region* and *master* servers.</span></span> <span data-ttu-id="b94a8-423">The default value is 1,000 MB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-423">The default value is 1,000 MB.</span></span> <span data-ttu-id="b94a8-424">This should be tuned for the cluster workload.</span><span class="sxs-lookup"><span data-stu-id="b94a8-424">This should be tuned for the cluster workload.</span></span>

1. <span data-ttu-id="b94a8-425">To modify, navigate to the **Advanced HBase-env** pane in the HBase **Configs** tab, and then find the `HBASE_HEAPSIZE` setting.</span><span class="sxs-lookup"><span data-stu-id="b94a8-425">To modify, navigate to the **Advanced HBase-env** pane in the HBase **Configs** tab, and then find the `HBASE_HEAPSIZE` setting.</span></span>

1. <span data-ttu-id="b94a8-426">Change the default value to 5,000 MB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-426">Change the default value to 5,000 MB.</span></span>

    ![HBASE_HEAPSIZE](./media/hdinsight-changing-configs-via-ambari/hbase-heapsize.png)


### <a name="optimize-read-heavy-workloads"></a><span data-ttu-id="b94a8-428">Optimize read-heavy workloads</span><span class="sxs-lookup"><span data-stu-id="b94a8-428">Optimize read-heavy workloads</span></span>

<span data-ttu-id="b94a8-429">The following configurations are important to improve the performance of read-heavy workloads.</span><span class="sxs-lookup"><span data-stu-id="b94a8-429">The following configurations are important to improve the performance of read-heavy workloads.</span></span>

#### <a name="block-cache-size"></a><span data-ttu-id="b94a8-430">Block cache size</span><span class="sxs-lookup"><span data-stu-id="b94a8-430">Block cache size</span></span>

<span data-ttu-id="b94a8-431">The block cache is the read cache.</span><span class="sxs-lookup"><span data-stu-id="b94a8-431">The block cache is the read cache.</span></span> <span data-ttu-id="b94a8-432">Its size is controlled by the `hfile.block.cache.size` parameter.</span><span class="sxs-lookup"><span data-stu-id="b94a8-432">Its size is controlled by the `hfile.block.cache.size` parameter.</span></span> <span data-ttu-id="b94a8-433">The default value is 0.4, which is 40 percent of the total region server memory.</span><span class="sxs-lookup"><span data-stu-id="b94a8-433">The default value is 0.4, which is 40 percent of the total region server memory.</span></span> <span data-ttu-id="b94a8-434">The larger the block cache size, the faster the random reads will be.</span><span class="sxs-lookup"><span data-stu-id="b94a8-434">The larger the block cache size, the faster the random reads will be.</span></span>

1. <span data-ttu-id="b94a8-435">To modify this parameter, navigate to the **Settings** tab in the HBase **Configs** tab, and then locate **% of RegionServer Allocated to Read Buffers**.</span><span class="sxs-lookup"><span data-stu-id="b94a8-435">To modify this parameter, navigate to the **Settings** tab in the HBase **Configs** tab, and then locate **% of RegionServer Allocated to Read Buffers**.</span></span>

    ![HBase block cache size](./media/hdinsight-changing-configs-via-ambari/hbase-block-cache-size.png)
 
1. <span data-ttu-id="b94a8-437">To change the value, select the **Edit** icon.</span><span class="sxs-lookup"><span data-stu-id="b94a8-437">To change the value, select the **Edit** icon.</span></span>


#### <a name="memstore-size"></a><span data-ttu-id="b94a8-438">Memstore size</span><span class="sxs-lookup"><span data-stu-id="b94a8-438">Memstore size</span></span>

<span data-ttu-id="b94a8-439">All edits are stored in the memory buffer, called a *Memstore*.</span><span class="sxs-lookup"><span data-stu-id="b94a8-439">All edits are stored in the memory buffer, called a *Memstore*.</span></span> <span data-ttu-id="b94a8-440">This increases the total amount of data that can be written to disk in a single operation, and it speeds subsequent access to the recent edits.</span><span class="sxs-lookup"><span data-stu-id="b94a8-440">This increases the total amount of data that can be written to disk in a single operation, and it speeds subsequent access to the recent edits.</span></span> <span data-ttu-id="b94a8-441">The Memstore size is defined by the following two parameters:</span><span class="sxs-lookup"><span data-stu-id="b94a8-441">The Memstore size is defined by the following two parameters:</span></span>

* <span data-ttu-id="b94a8-442">`hbase.regionserver.global.memstore.UpperLimit`: Defines the maximum percentage of the region server that Memstore combined can use.</span><span class="sxs-lookup"><span data-stu-id="b94a8-442">`hbase.regionserver.global.memstore.UpperLimit`: Defines the maximum percentage of the region server that Memstore combined can use.</span></span>

* <span data-ttu-id="b94a8-443">`hbase.regionserver.global.memstore.LowerLimit`: Defines the minimum percentage of the region server that Memstore combined can use.</span><span class="sxs-lookup"><span data-stu-id="b94a8-443">`hbase.regionserver.global.memstore.LowerLimit`: Defines the minimum percentage of the region server that Memstore combined can use.</span></span>

<span data-ttu-id="b94a8-444">To optimize for random reads, you can reduce the Memstore upper and lower limits.</span><span class="sxs-lookup"><span data-stu-id="b94a8-444">To optimize for random reads, you can reduce the Memstore upper and lower limits.</span></span>


#### <a name="number-of-rows-fetched-when-scanning-from-disk"></a><span data-ttu-id="b94a8-445">Number of rows fetched when scanning from disk</span><span class="sxs-lookup"><span data-stu-id="b94a8-445">Number of rows fetched when scanning from disk</span></span>

<span data-ttu-id="b94a8-446">The `hbase.client.scanner.caching` setting defines the number of rows read from disk when the `next` method is called on a scanner.</span><span class="sxs-lookup"><span data-stu-id="b94a8-446">The `hbase.client.scanner.caching` setting defines the number of rows read from disk when the `next` method is called on a scanner.</span></span>  <span data-ttu-id="b94a8-447">The default value is 100.</span><span class="sxs-lookup"><span data-stu-id="b94a8-447">The default value is 100.</span></span> <span data-ttu-id="b94a8-448">The higher the number, the fewer the remote calls made from the client to the region server, resulting in faster scans.</span><span class="sxs-lookup"><span data-stu-id="b94a8-448">The higher the number, the fewer the remote calls made from the client to the region server, resulting in faster scans.</span></span> <span data-ttu-id="b94a8-449">However, this will also increase memory pressure on the client.</span><span class="sxs-lookup"><span data-stu-id="b94a8-449">However, this will also increase memory pressure on the client.</span></span>

![HBase number of rows fetched](./media/hdinsight-changing-configs-via-ambari/hbase-num-rows-fetched.png)

> [!IMPORTANT]
> <span data-ttu-id="b94a8-451">Do not set the value such that the time between invocation of the next method on a scanner is greater than the scanner timeout.</span><span class="sxs-lookup"><span data-stu-id="b94a8-451">Do not set the value such that the time between invocation of the next method on a scanner is greater than the scanner timeout.</span></span> <span data-ttu-id="b94a8-452">The scanner timeout duration is defined by the `hbase.regionserver.lease.period` property.</span><span class="sxs-lookup"><span data-stu-id="b94a8-452">The scanner timeout duration is defined by the `hbase.regionserver.lease.period` property.</span></span>


### <a name="optimize-write-heavy-workloads"></a><span data-ttu-id="b94a8-453">Optimize write-heavy workloads</span><span class="sxs-lookup"><span data-stu-id="b94a8-453">Optimize write-heavy workloads</span></span>

<span data-ttu-id="b94a8-454">The following configurations are important to improve the performance of write-heavy workloads.</span><span class="sxs-lookup"><span data-stu-id="b94a8-454">The following configurations are important to improve the performance of write-heavy workloads.</span></span>


#### <a name="maximum-region-file-size"></a><span data-ttu-id="b94a8-455">Maximum region file size</span><span class="sxs-lookup"><span data-stu-id="b94a8-455">Maximum region file size</span></span>

<span data-ttu-id="b94a8-456">HBase stores  data in an internal file format, called *HFile*.</span><span class="sxs-lookup"><span data-stu-id="b94a8-456">HBase stores  data in an internal file format, called *HFile*.</span></span> <span data-ttu-id="b94a8-457">The property `hbase.hregion.max.filesize` defines the size of a single HFile for a region.</span><span class="sxs-lookup"><span data-stu-id="b94a8-457">The property `hbase.hregion.max.filesize` defines the size of a single HFile for a region.</span></span>  <span data-ttu-id="b94a8-458">A region is split into two regions if the sum of all HFiles in a region is greater than this setting.</span><span class="sxs-lookup"><span data-stu-id="b94a8-458">A region is split into two regions if the sum of all HFiles in a region is greater than this setting.</span></span>
 
![HBase HRegion max filesize](./media/hdinsight-changing-configs-via-ambari/hbase-hregion-max-filesize.png)

<span data-ttu-id="b94a8-460">The larger the region file size, the smaller the number of splits.</span><span class="sxs-lookup"><span data-stu-id="b94a8-460">The larger the region file size, the smaller the number of splits.</span></span> <span data-ttu-id="b94a8-461">You can increase the file size  to determine a value that results in the maximum write performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-461">You can increase the file size  to determine a value that results in the maximum write performance.</span></span>


#### <a name="avoid-update-blocking"></a><span data-ttu-id="b94a8-462">Avoid update blocking</span><span class="sxs-lookup"><span data-stu-id="b94a8-462">Avoid update blocking</span></span>

* <span data-ttu-id="b94a8-463">The property `hbase.hregion.memstore.flush.size` defines the size at which Memstore is flushed to disk.</span><span class="sxs-lookup"><span data-stu-id="b94a8-463">The property `hbase.hregion.memstore.flush.size` defines the size at which Memstore is flushed to disk.</span></span> <span data-ttu-id="b94a8-464">The default size is 128 MB.</span><span class="sxs-lookup"><span data-stu-id="b94a8-464">The default size is 128 MB.</span></span>

* <span data-ttu-id="b94a8-465">The Hbase region block multiplier is defined by `hbase.hregion.memstore.block.multiplier`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-465">The Hbase region block multiplier is defined by `hbase.hregion.memstore.block.multiplier`.</span></span> <span data-ttu-id="b94a8-466">The default value is 4.</span><span class="sxs-lookup"><span data-stu-id="b94a8-466">The default value is 4.</span></span> <span data-ttu-id="b94a8-467">The maximum allowed is 8.</span><span class="sxs-lookup"><span data-stu-id="b94a8-467">The maximum allowed is 8.</span></span>

* <span data-ttu-id="b94a8-468">HBase blocks updates if the Memstore is (`hbase.hregion.memstore.flush.size` \* `hbase.hregion.memstore.block.multiplier`) bytes.</span><span class="sxs-lookup"><span data-stu-id="b94a8-468">HBase blocks updates if the Memstore is (`hbase.hregion.memstore.flush.size` \* `hbase.hregion.memstore.block.multiplier`) bytes.</span></span>

    <span data-ttu-id="b94a8-469">With the default values of flush size and block multiplier, updates are blocked when Memstore is  128 \* 4 = 512 MB in size.</span><span class="sxs-lookup"><span data-stu-id="b94a8-469">With the default values of flush size and block multiplier, updates are blocked when Memstore is  128 \* 4 = 512 MB in size.</span></span> <span data-ttu-id="b94a8-470">To reduce the update blocking count, increase the value of `hbase.hregion.memstore.block.multiplier`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-470">To reduce the update blocking count, increase the value of `hbase.hregion.memstore.block.multiplier`.</span></span>

![HBase Region Block Multiplier](./media/hdinsight-changing-configs-via-ambari/hbase-hregion-memstore-block-multiplier.png)


### <a name="define-memstore-size"></a><span data-ttu-id="b94a8-472">Define Memstore size</span><span class="sxs-lookup"><span data-stu-id="b94a8-472">Define Memstore size</span></span>

<span data-ttu-id="b94a8-473">Memstore size is defined by the `hbase.regionserver.global.memstore.UpperLimit` and `hbase.regionserver.global.memstore.LowerLimit` parameters.</span><span class="sxs-lookup"><span data-stu-id="b94a8-473">Memstore size is defined by the `hbase.regionserver.global.memstore.UpperLimit` and `hbase.regionserver.global.memstore.LowerLimit` parameters.</span></span> <span data-ttu-id="b94a8-474">Setting these values equal to each other reduces pauses during writes (also causing more frequent flushing) and results in increased write performance.</span><span class="sxs-lookup"><span data-stu-id="b94a8-474">Setting these values equal to each other reduces pauses during writes (also causing more frequent flushing) and results in increased write performance.</span></span>


### <a name="set-memstore-local-allocation-buffer"></a><span data-ttu-id="b94a8-475">Set Memstore local allocation buffer</span><span class="sxs-lookup"><span data-stu-id="b94a8-475">Set Memstore local allocation buffer</span></span>

<span data-ttu-id="b94a8-476">Memstore local allocation buffer usage is determined by the property `hbase.hregion.memstore.mslab.enabled`.</span><span class="sxs-lookup"><span data-stu-id="b94a8-476">Memstore local allocation buffer usage is determined by the property `hbase.hregion.memstore.mslab.enabled`.</span></span> <span data-ttu-id="b94a8-477">When enabled (true), this prevents heap fragmentation during heavy write operation.</span><span class="sxs-lookup"><span data-stu-id="b94a8-477">When enabled (true), this prevents heap fragmentation during heavy write operation.</span></span> <span data-ttu-id="b94a8-478">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="b94a8-478">The default value is true.</span></span>
 
![hbase.hregion.memstore.mslab.enabled](./media/hdinsight-changing-configs-via-ambari/hbase-hregion-memstore-mslab-enabled.png)


## <a name="next-steps"></a><span data-ttu-id="b94a8-480">Next steps</span><span class="sxs-lookup"><span data-stu-id="b94a8-480">Next steps</span></span>

* [<span data-ttu-id="b94a8-481">Manage HDInsight clusters with the Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="b94a8-481">Manage HDInsight clusters with the Ambari web UI</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="b94a8-482">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="b94a8-482">Ambari REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)
