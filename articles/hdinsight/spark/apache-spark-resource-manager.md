---
title: Manage resources for Apache Spark cluster on Azure HDInsight
description: Learn how to use manage resources for Spark clusters on Azure HDInsight for better performance.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/23/2018
ms.author: jasonh
ms.openlocfilehash: d7395231662d79d284bdf061e651602dea392c28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969435"
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="abda3-103">Manage resources for Apache Spark cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="abda3-103">Manage resources for Apache Spark cluster on Azure HDInsight</span></span> 

<span data-ttu-id="abda3-104">Learn how to access the interfaces like Ambari UI, YARN UI, and the Spark History Server associated with your Spark cluster, and how to tune the cluster configuration for optimal performance.</span><span class="sxs-lookup"><span data-stu-id="abda3-104">Learn how to access the interfaces like Ambari UI, YARN UI, and the Spark History Server associated with your Spark cluster, and how to tune the cluster configuration for optimal performance.</span></span>

<span data-ttu-id="abda3-105">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="abda3-105">**Prerequisites:**</span></span>

* <span data-ttu-id="abda3-106">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abda3-106">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="abda3-107">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="abda3-107">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="open-the-ambari-web-ui"></a><span data-ttu-id="abda3-108">Open the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="abda3-108">Open the Ambari Web UI</span></span>

<span data-ttu-id="abda3-109">Apache Ambari is used to monitor the cluster and make configuration changes.</span><span class="sxs-lookup"><span data-stu-id="abda3-109">Apache Ambari is used to monitor the cluster and make configuration changes.</span></span> <span data-ttu-id="abda3-110">For more information, see [Manage Hadoop clusters in HDInsight by using the Azure portal](../hdinsight-administer-use-portal-linux.md#open-the-ambari-web-ui)</span><span class="sxs-lookup"><span data-stu-id="abda3-110">For more information, see [Manage Hadoop clusters in HDInsight by using the Azure portal](../hdinsight-administer-use-portal-linux.md#open-the-ambari-web-ui)</span></span>

## <a name="open-the-spark-history-server"></a><span data-ttu-id="abda3-111">Open the Spark History Server</span><span class="sxs-lookup"><span data-stu-id="abda3-111">Open the Spark History Server</span></span>

<span data-ttu-id="abda3-112">Spark History Server is the web UI for completed and running Spark applications.</span><span class="sxs-lookup"><span data-stu-id="abda3-112">Spark History Server is the web UI for completed and running Spark applications.</span></span> <span data-ttu-id="abda3-113">It is an extension of Spark's Web UI.</span><span class="sxs-lookup"><span data-stu-id="abda3-113">It is an extension of Spark's Web UI.</span></span>

<span data-ttu-id="abda3-114">**To open the Spark History Server Web UI**</span><span class="sxs-lookup"><span data-stu-id="abda3-114">**To open the Spark History Server Web UI**</span></span>

1. <span data-ttu-id="abda3-115">From the [Azure portal](https://portal.azure.com/), open the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="abda3-115">From the [Azure portal](https://portal.azure.com/), open the Spark cluster.</span></span> <span data-ttu-id="abda3-116">For more information, see [List and show clusters](../hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="abda3-116">For more information, see [List and show clusters](../hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
2. <span data-ttu-id="abda3-117">From **Quick Links**, click **Cluster Dashboard**, and then click **Spark History Server**</span><span class="sxs-lookup"><span data-stu-id="abda3-117">From **Quick Links**, click **Cluster Dashboard**, and then click **Spark History Server**</span></span>

    <span data-ttu-id="abda3-118">![Spark History Server](./media/apache-spark-resource-manager/launch-history-server.png "Spark History Server")</span><span class="sxs-lookup"><span data-stu-id="abda3-118">![Spark History Server](./media/apache-spark-resource-manager/launch-history-server.png "Spark History Server")</span></span>

    <span data-ttu-id="abda3-119">When prompted, enter the admin credentials for the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="abda3-119">When prompted, enter the admin credentials for the Spark cluster.</span></span> <span data-ttu-id="abda3-120">You can also open the Spark History Server by browsing to the following URL:</span><span class="sxs-lookup"><span data-stu-id="abda3-120">You can also open the Spark History Server by browsing to the following URL:</span></span>

    ```
    https://<ClusterName>.azurehdinsight.net/sparkhistory
    ```

    <span data-ttu-id="abda3-121">Replace <ClusterName> with your Spark cluster name.</span><span class="sxs-lookup"><span data-stu-id="abda3-121">Replace <ClusterName> with your Spark cluster name.</span></span>

<span data-ttu-id="abda3-122">The Spark History Server web UI looks like:</span><span class="sxs-lookup"><span data-stu-id="abda3-122">The Spark History Server web UI looks like:</span></span>

![HDInsight Spark History Server](./media/apache-spark-resource-manager/hdinsight-spark-history-server.png)

## <a name="open-the-yarn-ui"></a><span data-ttu-id="abda3-124">Open the Yarn UI</span><span class="sxs-lookup"><span data-stu-id="abda3-124">Open the Yarn UI</span></span>
<span data-ttu-id="abda3-125">You can use the YARN UI to monitor applications that are currently running on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="abda3-125">You can use the YARN UI to monitor applications that are currently running on the Spark cluster.</span></span>

1. <span data-ttu-id="abda3-126">From the [Azure portal](https://portal.azure.com/), open the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="abda3-126">From the [Azure portal](https://portal.azure.com/), open the Spark cluster.</span></span> <span data-ttu-id="abda3-127">For more information, see [List and show clusters](../hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="abda3-127">For more information, see [List and show clusters](../hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
2. <span data-ttu-id="abda3-128">From **Quick Links**, click **Cluster Dashboard**, and then click **YARN**.</span><span class="sxs-lookup"><span data-stu-id="abda3-128">From **Quick Links**, click **Cluster Dashboard**, and then click **YARN**.</span></span>

    ![Launch YARN UI](./media/apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > <span data-ttu-id="abda3-130">Alternatively, you can also launch the YARN UI from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="abda3-130">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="abda3-131">To launch the Ambari UI, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="abda3-131">To launch the Ambari UI, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="abda3-132">From the Ambari UI, click **YARN**, click **Quick Links**, click the active Resource Manager, and then click **Resource Manager UI**.</span><span class="sxs-lookup"><span data-stu-id="abda3-132">From the Ambari UI, click **YARN**, click **Quick Links**, click the active Resource Manager, and then click **Resource Manager UI**.</span></span>
   >
   >

## <a name="optimize-clusters-for-spark-applications"></a><span data-ttu-id="abda3-133">Optimize clusters for Spark applications</span><span class="sxs-lookup"><span data-stu-id="abda3-133">Optimize clusters for Spark applications</span></span>
<span data-ttu-id="abda3-134">The three key parameters that can be used for Spark configuration depending on application requirements are `spark.executor.instances`, `spark.executor.cores`, and `spark.executor.memory`.</span><span class="sxs-lookup"><span data-stu-id="abda3-134">The three key parameters that can be used for Spark configuration depending on application requirements are `spark.executor.instances`, `spark.executor.cores`, and `spark.executor.memory`.</span></span> <span data-ttu-id="abda3-135">An Executor is a process launched for a Spark application.</span><span class="sxs-lookup"><span data-stu-id="abda3-135">An Executor is a process launched for a Spark application.</span></span> <span data-ttu-id="abda3-136">It runs on the worker node and is responsible to carry out the tasks for the application.</span><span class="sxs-lookup"><span data-stu-id="abda3-136">It runs on the worker node and is responsible to carry out the tasks for the application.</span></span> <span data-ttu-id="abda3-137">The default number of executors and the executor sizes for each cluster is calculated based on the number of worker nodes and the worker node size.</span><span class="sxs-lookup"><span data-stu-id="abda3-137">The default number of executors and the executor sizes for each cluster is calculated based on the number of worker nodes and the worker node size.</span></span> <span data-ttu-id="abda3-138">This information is stored in `spark-defaults.conf` on the cluster head nodes.</span><span class="sxs-lookup"><span data-stu-id="abda3-138">This information is stored in `spark-defaults.conf` on the cluster head nodes.</span></span>

<span data-ttu-id="abda3-139">The three configuration parameters can be configured at the cluster level (for all applications that run on the cluster) or can be specified for each individual application as well.</span><span class="sxs-lookup"><span data-stu-id="abda3-139">The three configuration parameters can be configured at the cluster level (for all applications that run on the cluster) or can be specified for each individual application as well.</span></span>

### <a name="change-the-parameters-using-ambari-ui"></a><span data-ttu-id="abda3-140">Change the parameters using Ambari UI</span><span class="sxs-lookup"><span data-stu-id="abda3-140">Change the parameters using Ambari UI</span></span>
1. <span data-ttu-id="abda3-141">From the Ambari UI click **Spark**, click **Configs**, and then expand **Custom spark-defaults**.</span><span class="sxs-lookup"><span data-stu-id="abda3-141">From the Ambari UI click **Spark**, click **Configs**, and then expand **Custom spark-defaults**.</span></span>

    ![Set parameters using Ambari](./media/apache-spark-resource-manager/set-parameters-using-ambari.png)
2. <span data-ttu-id="abda3-143">The default values are good to have four Spark applications run concurrently on the cluster.</span><span class="sxs-lookup"><span data-stu-id="abda3-143">The default values are good to have four Spark applications run concurrently on the cluster.</span></span> <span data-ttu-id="abda3-144">You can change these values from the user interface, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="abda3-144">You can change these values from the user interface, as shown in the following screenshot:</span></span>

    ![Set parameters using Ambari](./media/apache-spark-resource-manager/set-executor-parameters.png)
3. <span data-ttu-id="abda3-146">Click **Save** to save the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="abda3-146">Click **Save** to save the configuration changes.</span></span> <span data-ttu-id="abda3-147">At the top of the page, you are prompted to restart all the affected services.</span><span class="sxs-lookup"><span data-stu-id="abda3-147">At the top of the page, you are prompted to restart all the affected services.</span></span> <span data-ttu-id="abda3-148">Click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="abda3-148">Click **Restart**.</span></span>

    ![Restart services](./media/apache-spark-resource-manager/restart-services.png)

### <a name="change-the-parameters-for-an-application-running-in-jupyter-notebook"></a><span data-ttu-id="abda3-150">Change the parameters for an application running in Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="abda3-150">Change the parameters for an application running in Jupyter notebook</span></span>
<span data-ttu-id="abda3-151">For applications running in the Jupyter notebook, you can use the `%%configure` magic to make the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="abda3-151">For applications running in the Jupyter notebook, you can use the `%%configure` magic to make the configuration changes.</span></span> <span data-ttu-id="abda3-152">Ideally, you must make such changes at the beginning of the application, before you run your first code cell.</span><span class="sxs-lookup"><span data-stu-id="abda3-152">Ideally, you must make such changes at the beginning of the application, before you run your first code cell.</span></span> <span data-ttu-id="abda3-153">Doing this ensures that the configuration is applied to the Livy session, when it gets created.</span><span class="sxs-lookup"><span data-stu-id="abda3-153">Doing this ensures that the configuration is applied to the Livy session, when it gets created.</span></span> <span data-ttu-id="abda3-154">If you want to change the configuration at a later stage in the application, you must use the `-f` parameter.</span><span class="sxs-lookup"><span data-stu-id="abda3-154">If you want to change the configuration at a later stage in the application, you must use the `-f` parameter.</span></span> <span data-ttu-id="abda3-155">However, by doing so all progress in the application is lost.</span><span class="sxs-lookup"><span data-stu-id="abda3-155">However, by doing so all progress in the application is lost.</span></span>

<span data-ttu-id="abda3-156">The following snippet shows how to change the configuration for an application running in Jupyter.</span><span class="sxs-lookup"><span data-stu-id="abda3-156">The following snippet shows how to change the configuration for an application running in Jupyter.</span></span>

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

<span data-ttu-id="abda3-157">Configuration parameters must be passed in as a JSON string and must be on the next line after the magic, as shown in the example column.</span><span class="sxs-lookup"><span data-stu-id="abda3-157">Configuration parameters must be passed in as a JSON string and must be on the next line after the magic, as shown in the example column.</span></span>

### <a name="change-the-parameters-for-an-application-submitted-using-spark-submit"></a><span data-ttu-id="abda3-158">Change the parameters for an application submitted using spark-submit</span><span class="sxs-lookup"><span data-stu-id="abda3-158">Change the parameters for an application submitted using spark-submit</span></span>
<span data-ttu-id="abda3-159">Following command is an example of how to change the configuration parameters for a batch application that is submitted using `spark-submit`.</span><span class="sxs-lookup"><span data-stu-id="abda3-159">Following command is an example of how to change the configuration parameters for a batch application that is submitted using `spark-submit`.</span></span>

    spark-submit --class <the application class to execute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-the-parameters-for-an-application-submitted-using-curl"></a><span data-ttu-id="abda3-160">Change the parameters for an application submitted using cURL</span><span class="sxs-lookup"><span data-stu-id="abda3-160">Change the parameters for an application submitted using cURL</span></span>
<span data-ttu-id="abda3-161">The following command is an example of how to change the configuration parameters for a batch application that is submitted using cURL.</span><span class="sxs-lookup"><span data-stu-id="abda3-161">The following command is an example of how to change the configuration parameters for a batch application that is submitted using cURL.</span></span>

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<the application class to execute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="change-these-parameters-on-a-spark-thrift-server"></a><span data-ttu-id="abda3-162">Change these parameters on a Spark Thrift Server</span><span class="sxs-lookup"><span data-stu-id="abda3-162">Change these parameters on a Spark Thrift Server</span></span>
<span data-ttu-id="abda3-163">Spark Thrift Server provides JDBC/ODBC access to a Spark cluster and is used to service Spark SQL queries.</span><span class="sxs-lookup"><span data-stu-id="abda3-163">Spark Thrift Server provides JDBC/ODBC access to a Spark cluster and is used to service Spark SQL queries.</span></span> <span data-ttu-id="abda3-164">Tools like Power BI, Tableau etc.</span><span class="sxs-lookup"><span data-stu-id="abda3-164">Tools like Power BI, Tableau etc.</span></span> <span data-ttu-id="abda3-165">use ODBC protocol to communicate with Spark Thrift Server to execute Spark SQL queries as a Spark Application.</span><span class="sxs-lookup"><span data-stu-id="abda3-165">use ODBC protocol to communicate with Spark Thrift Server to execute Spark SQL queries as a Spark Application.</span></span> <span data-ttu-id="abda3-166">When a Spark cluster is created, two instances of the Spark Thrift Server are started, one on each head node.</span><span class="sxs-lookup"><span data-stu-id="abda3-166">When a Spark cluster is created, two instances of the Spark Thrift Server are started, one on each head node.</span></span> <span data-ttu-id="abda3-167">Each Spark Thrift Server is visible as a Spark application in the YARN UI.</span><span class="sxs-lookup"><span data-stu-id="abda3-167">Each Spark Thrift Server is visible as a Spark application in the YARN UI.</span></span>

<span data-ttu-id="abda3-168">Spark Thrift Server uses Spark dynamic executor allocation and hence the `spark.executor.instances` is not used.</span><span class="sxs-lookup"><span data-stu-id="abda3-168">Spark Thrift Server uses Spark dynamic executor allocation and hence the `spark.executor.instances` is not used.</span></span> <span data-ttu-id="abda3-169">Instead, Spark Thrift Server uses `spark.dynamicAllocation.minExecutors` and `spark.dynamicAllocation.maxExecutors` to specify the executor count.</span><span class="sxs-lookup"><span data-stu-id="abda3-169">Instead, Spark Thrift Server uses `spark.dynamicAllocation.minExecutors` and `spark.dynamicAllocation.maxExecutors` to specify the executor count.</span></span> <span data-ttu-id="abda3-170">The configuration parameters `spark.executor.cores` and `spark.executor.memory` is used to modify the executor size.</span><span class="sxs-lookup"><span data-stu-id="abda3-170">The configuration parameters `spark.executor.cores` and `spark.executor.memory` is used to modify the executor size.</span></span> <span data-ttu-id="abda3-171">You can change these parameters as shown in the following steps:</span><span class="sxs-lookup"><span data-stu-id="abda3-171">You can change these parameters as shown in the following steps:</span></span>

* <span data-ttu-id="abda3-172">Expand the **Advanced spark-thrift-sparkconf** category to update the parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, and `spark.executor.memory`.</span><span class="sxs-lookup"><span data-stu-id="abda3-172">Expand the **Advanced spark-thrift-sparkconf** category to update the parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, and `spark.executor.memory`.</span></span>

    ![Configure Spark thrift server](./media/apache-spark-resource-manager/spark-thrift-server-1.png)    
* <span data-ttu-id="abda3-174">Expand the **Custom spark-thrift-sparkconf** category to update the parameter `spark.executor.cores`.</span><span class="sxs-lookup"><span data-stu-id="abda3-174">Expand the **Custom spark-thrift-sparkconf** category to update the parameter `spark.executor.cores`.</span></span>

    ![Configure Spark thrift server](./media/apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="change-the-driver-memory-of-the-spark-thrift-server"></a><span data-ttu-id="abda3-176">Change the driver memory of the Spark Thrift Server</span><span class="sxs-lookup"><span data-stu-id="abda3-176">Change the driver memory of the Spark Thrift Server</span></span>
<span data-ttu-id="abda3-177">Spark Thrift Server driver memory is configured to 25% of the head node RAM size, provided the total RAM size of the head node is greater than 14 GB.</span><span class="sxs-lookup"><span data-stu-id="abda3-177">Spark Thrift Server driver memory is configured to 25% of the head node RAM size, provided the total RAM size of the head node is greater than 14 GB.</span></span> <span data-ttu-id="abda3-178">You can use the Ambari UI to change the driver memory configuration, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="abda3-178">You can use the Ambari UI to change the driver memory configuration, as shown in the following screenshot:</span></span>

* <span data-ttu-id="abda3-179">From the Ambari UI click **Spark**, click **Configs**, expand **Advanced spark-env**, and then provide the value for **spark_thrift_cmd_opts**.</span><span class="sxs-lookup"><span data-stu-id="abda3-179">From the Ambari UI click **Spark**, click **Configs**, expand **Advanced spark-env**, and then provide the value for **spark_thrift_cmd_opts**.</span></span>

    ![Configure Spark thrift server RAM](./media/apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="reclaim-spark-cluster-resources"></a><span data-ttu-id="abda3-181">Reclaim Spark cluster resources</span><span class="sxs-lookup"><span data-stu-id="abda3-181">Reclaim Spark cluster resources</span></span>
<span data-ttu-id="abda3-182">Because of Spark dynamic allocation, the only resources that are consumed by thrift server are the resources for the two application masters.</span><span class="sxs-lookup"><span data-stu-id="abda3-182">Because of Spark dynamic allocation, the only resources that are consumed by thrift server are the resources for the two application masters.</span></span> <span data-ttu-id="abda3-183">To reclaim these resources, you must stop the Thrift Server services running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="abda3-183">To reclaim these resources, you must stop the Thrift Server services running on the cluster.</span></span>

1. <span data-ttu-id="abda3-184">From the Ambari UI, from the left pane, click **Spark**.</span><span class="sxs-lookup"><span data-stu-id="abda3-184">From the Ambari UI, from the left pane, click **Spark**.</span></span>
2. <span data-ttu-id="abda3-185">In the next page, click **Spark Thrift Servers**.</span><span class="sxs-lookup"><span data-stu-id="abda3-185">In the next page, click **Spark Thrift Servers**.</span></span>

    ![Restart thrift server](./media/apache-spark-resource-manager/restart-thrift-server-1.png)
3. <span data-ttu-id="abda3-187">You should see the two headnodes on which the Spark Thrift Server is running.</span><span class="sxs-lookup"><span data-stu-id="abda3-187">You should see the two headnodes on which the Spark Thrift Server is running.</span></span> <span data-ttu-id="abda3-188">Click one of the headnodes.</span><span class="sxs-lookup"><span data-stu-id="abda3-188">Click one of the headnodes.</span></span>

    ![Restart thrift server](./media/apache-spark-resource-manager/restart-thrift-server-2.png)
4. <span data-ttu-id="abda3-190">The next page lists all the services running on that headnode.</span><span class="sxs-lookup"><span data-stu-id="abda3-190">The next page lists all the services running on that headnode.</span></span> <span data-ttu-id="abda3-191">From the list click the drop-down button next to Spark Thrift Server, and then click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="abda3-191">From the list click the drop-down button next to Spark Thrift Server, and then click **Stop**.</span></span>

    ![Restart thrift server](./media/apache-spark-resource-manager/restart-thrift-server-3.png)
5. <span data-ttu-id="abda3-193">Repeat these steps on the other headnode as well.</span><span class="sxs-lookup"><span data-stu-id="abda3-193">Repeat these steps on the other headnode as well.</span></span>

## <a name="restart-the-jupyter-service"></a><span data-ttu-id="abda3-194">Restart the Jupyter service</span><span class="sxs-lookup"><span data-stu-id="abda3-194">Restart the Jupyter service</span></span>
<span data-ttu-id="abda3-195">Launch the Ambari Web UI as shown in the beginning of the article.</span><span class="sxs-lookup"><span data-stu-id="abda3-195">Launch the Ambari Web UI as shown in the beginning of the article.</span></span> <span data-ttu-id="abda3-196">From the left navigation pane, click **Jupyter**, click **Service Actions**, and then click **Restart All**.</span><span class="sxs-lookup"><span data-stu-id="abda3-196">From the left navigation pane, click **Jupyter**, click **Service Actions**, and then click **Restart All**.</span></span> <span data-ttu-id="abda3-197">This starts the Jupyter service on all the headnodes.</span><span class="sxs-lookup"><span data-stu-id="abda3-197">This starts the Jupyter service on all the headnodes.</span></span>

<span data-ttu-id="abda3-198">![Restart Jupyter](./media/apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")</span><span class="sxs-lookup"><span data-stu-id="abda3-198">![Restart Jupyter](./media/apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")</span></span>

## <a name="monitor-resources"></a><span data-ttu-id="abda3-199">Monitor resources</span><span class="sxs-lookup"><span data-stu-id="abda3-199">Monitor resources</span></span>
<span data-ttu-id="abda3-200">Launch the Yarn UI as shown in the beginning of the article.</span><span class="sxs-lookup"><span data-stu-id="abda3-200">Launch the Yarn UI as shown in the beginning of the article.</span></span> <span data-ttu-id="abda3-201">In Cluster Metrics table on top of the screen, check values of **Memory Used** and **Memory Total** columns.</span><span class="sxs-lookup"><span data-stu-id="abda3-201">In Cluster Metrics table on top of the screen, check values of **Memory Used** and **Memory Total** columns.</span></span> <span data-ttu-id="abda3-202">If the two values are close, there might not be enough resources to start the next application.</span><span class="sxs-lookup"><span data-stu-id="abda3-202">If the two values are close, there might not be enough resources to start the next application.</span></span> <span data-ttu-id="abda3-203">The same applies to the **VCores Used** and **VCores Total** columns.</span><span class="sxs-lookup"><span data-stu-id="abda3-203">The same applies to the **VCores Used** and **VCores Total** columns.</span></span> <span data-ttu-id="abda3-204">Also, in the main view, if there is an application stayed in **ACCEPTED** state and not transitioning into **RUNNING** nor **FAILED** state, this could also be an indication that it is not getting enough resources to start.</span><span class="sxs-lookup"><span data-stu-id="abda3-204">Also, in the main view, if there is an application stayed in **ACCEPTED** state and not transitioning into **RUNNING** nor **FAILED** state, this could also be an indication that it is not getting enough resources to start.</span></span>

<span data-ttu-id="abda3-205">![Resource Limit](./media/apache-spark-resource-manager/resource-limit.png "Resource Limit")</span><span class="sxs-lookup"><span data-stu-id="abda3-205">![Resource Limit](./media/apache-spark-resource-manager/resource-limit.png "Resource Limit")</span></span>

## <a name="kill-running-applications"></a><span data-ttu-id="abda3-206">Kill running applications</span><span class="sxs-lookup"><span data-stu-id="abda3-206">Kill running applications</span></span>
1. <span data-ttu-id="abda3-207">In the Yarn UI, from the left panel, click **Running**.</span><span class="sxs-lookup"><span data-stu-id="abda3-207">In the Yarn UI, from the left panel, click **Running**.</span></span> <span data-ttu-id="abda3-208">From the list of running applications, determine the application to be killed and click on the **ID**.</span><span class="sxs-lookup"><span data-stu-id="abda3-208">From the list of running applications, determine the application to be killed and click on the **ID**.</span></span>

    <span data-ttu-id="abda3-209">![Kill App1](./media/apache-spark-resource-manager/kill-app1.png "Kill App1")</span><span class="sxs-lookup"><span data-stu-id="abda3-209">![Kill App1](./media/apache-spark-resource-manager/kill-app1.png "Kill App1")</span></span>

2. <span data-ttu-id="abda3-210">Click **Kill Application** on the top right corner, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="abda3-210">Click **Kill Application** on the top right corner, then click **OK**.</span></span>

    <span data-ttu-id="abda3-211">![Kill App2](./media/apache-spark-resource-manager/kill-app2.png "Kill App2")</span><span class="sxs-lookup"><span data-stu-id="abda3-211">![Kill App2](./media/apache-spark-resource-manager/kill-app2.png "Kill App2")</span></span>

## <a name="see-also"></a><span data-ttu-id="abda3-212">See also</span><span class="sxs-lookup"><span data-stu-id="abda3-212">See also</span></span>
* [<span data-ttu-id="abda3-213">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="abda3-213">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a><span data-ttu-id="abda3-214">For data analysts</span><span class="sxs-lookup"><span data-stu-id="abda3-214">For data analysts</span></span>

* [<span data-ttu-id="abda3-215">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="abda3-215">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="abda3-216">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="abda3-216">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="abda3-217">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="abda3-217">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="abda3-218">Application Insight telemetry data analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="abda3-218">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](apache-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="abda3-219">Use Caffe on Azure HDInsight Spark for distributed deep learning</span><span class="sxs-lookup"><span data-stu-id="abda3-219">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](apache-spark-deep-learning-caffe.md)

### <a name="for-spark-developers"></a><span data-ttu-id="abda3-220">For Spark developers</span><span class="sxs-lookup"><span data-stu-id="abda3-220">For Spark developers</span></span>

* [<span data-ttu-id="abda3-221">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="abda3-221">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="abda3-222">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="abda3-222">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="abda3-223">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="abda3-223">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="abda3-224">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="abda3-224">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="abda3-225">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="abda3-225">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="abda3-226">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="abda3-226">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="abda3-227">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="abda3-227">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="abda3-228">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="abda3-228">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)
