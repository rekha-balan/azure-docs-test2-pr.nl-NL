---
title: Manage resources for Apache Spark cluster on Azure HDInsight| Microsoft Docs
description: Learn how to use manage resources for Spark clusters on Azure HDInsight for better performance.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: ce4476bb2672bb52d1a4b3d442964281d691663d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661830"
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="17404-103">Manage resources for Apache Spark cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="17404-103">Manage resources for Apache Spark cluster on Azure HDInsight</span></span> 

<span data-ttu-id="17404-104">In this article you will learn how to access the interfaces like Ambari UI, YARN UI, and the Spark History Server associated with your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-104">In this article you will learn how to access the interfaces like Ambari UI, YARN UI, and the Spark History Server associated with your Spark cluster.</span></span> <span data-ttu-id="17404-105">You will also learn about how to tune the cluster configuration for optimal performance.</span><span class="sxs-lookup"><span data-stu-id="17404-105">You will also learn about how to tune the cluster configuration for optimal performance.</span></span>

<span data-ttu-id="17404-106">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="17404-106">**Prerequisites:**</span></span>

<span data-ttu-id="17404-107">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="17404-107">You must have the following:</span></span>

* <span data-ttu-id="17404-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="17404-108">An Azure subscription.</span></span> <span data-ttu-id="17404-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="17404-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="17404-110">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17404-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="17404-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="17404-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-do-i-launch-the-ambari-web-ui"></a><span data-ttu-id="17404-112">How do I launch the Ambari Web UI?</span><span class="sxs-lookup"><span data-stu-id="17404-112">How do I launch the Ambari Web UI?</span></span>
1. <span data-ttu-id="17404-113">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="17404-113">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="17404-114">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="17404-114">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>
2. <span data-ttu-id="17404-115">From the Spark cluster blade, click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="17404-115">From the Spark cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="17404-116">When prompted, enter the admin credentials for the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-116">When prompted, enter the admin credentials for the Spark cluster.</span></span>

    <span data-ttu-id="17404-117">![Launch Ambari](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/hdispark.cluster.launch.dashboard.png "Start Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="17404-117">![Launch Ambari](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/hdispark.cluster.launch.dashboard.png "Start Resource Manager")</span></span>
3. <span data-ttu-id="17404-118">This should launch the Ambari Web UI, as shown below.</span><span class="sxs-lookup"><span data-stu-id="17404-118">This should launch the Ambari Web UI, as shown below.</span></span>

    <span data-ttu-id="17404-119">![Ambari Web UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")</span><span class="sxs-lookup"><span data-stu-id="17404-119">![Ambari Web UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")</span></span>   

## <a name="how-do-i-launch-the-spark-history-server"></a><span data-ttu-id="17404-120">How do I launch the Spark History Server?</span><span class="sxs-lookup"><span data-stu-id="17404-120">How do I launch the Spark History Server?</span></span>
1. <span data-ttu-id="17404-121">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="17404-121">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span>
2. <span data-ttu-id="17404-122">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="17404-122">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**.</span></span> <span data-ttu-id="17404-123">In the **Cluster Dashboard** blade, click **Spark History Server**.</span><span class="sxs-lookup"><span data-stu-id="17404-123">In the **Cluster Dashboard** blade, click **Spark History Server**.</span></span>

    <span data-ttu-id="17404-124">![Spark History Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark History Server")</span><span class="sxs-lookup"><span data-stu-id="17404-124">![Spark History Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark History Server")</span></span>

    <span data-ttu-id="17404-125">When prompted, enter the admin credentials for the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-125">When prompted, enter the admin credentials for the Spark cluster.</span></span>

## <a name="how-do-i-launch-the-yarn-ui"></a><span data-ttu-id="17404-126">How do I launch the Yarn UI?</span><span class="sxs-lookup"><span data-stu-id="17404-126">How do I launch the Yarn UI?</span></span>
<span data-ttu-id="17404-127">You can use the YARN UI to monitor applications that are currently running on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-127">You can use the YARN UI to monitor applications that are currently running on the Spark cluster.</span></span>

1. <span data-ttu-id="17404-128">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span><span class="sxs-lookup"><span data-stu-id="17404-128">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>

    ![Launch YARN UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > <span data-ttu-id="17404-130">Alternatively, you can also launch the YARN UI from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="17404-130">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="17404-131">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="17404-131">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="17404-132">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="17404-132">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>
   >
   >

## <a name="what-is-the-optimum-cluster-configuration-to-run-spark-applications"></a><span data-ttu-id="17404-133">What is the optimum cluster configuration to run Spark applications?</span><span class="sxs-lookup"><span data-stu-id="17404-133">What is the optimum cluster configuration to run Spark applications?</span></span>
<span data-ttu-id="17404-134">The three key parameters that can be used for Spark configuration depending on application requirements are `spark.executor.instances`, `spark.executor.cores`, and `spark.executor.memory`.</span><span class="sxs-lookup"><span data-stu-id="17404-134">The three key parameters that can be used for Spark configuration depending on application requirements are `spark.executor.instances`, `spark.executor.cores`, and `spark.executor.memory`.</span></span> <span data-ttu-id="17404-135">An Executor is a process launched for a Spark application.</span><span class="sxs-lookup"><span data-stu-id="17404-135">An Executor is a process launched for a Spark application.</span></span> <span data-ttu-id="17404-136">It runs on the worker node and is responsible to carry out the tasks for the application.</span><span class="sxs-lookup"><span data-stu-id="17404-136">It runs on the worker node and is responsible to carry out the tasks for the application.</span></span> <span data-ttu-id="17404-137">The default number of executors and the executor sizes for each cluster is calculated based on the number of worker nodes and the worker node size.</span><span class="sxs-lookup"><span data-stu-id="17404-137">The default number of executors and the executor sizes for each cluster is calculated based on the number of worker nodes and the worker node size.</span></span> <span data-ttu-id="17404-138">These are stored in `spark-defaults.conf` on the cluster head nodes.</span><span class="sxs-lookup"><span data-stu-id="17404-138">These are stored in `spark-defaults.conf` on the cluster head nodes.</span></span>

<span data-ttu-id="17404-139">The three configuration parameters can be configured at the cluster level (for all applications that run on the cluster) or can be specified for each individual application as well.</span><span class="sxs-lookup"><span data-stu-id="17404-139">The three configuration parameters can be configured at the cluster level (for all applications that run on the cluster) or can be specified for each individual application as well.</span></span>

### <a name="change-the-parameters-using-ambari-ui"></a><span data-ttu-id="17404-140">Change the parameters using Ambari UI</span><span class="sxs-lookup"><span data-stu-id="17404-140">Change the parameters using Ambari UI</span></span>
1. <span data-ttu-id="17404-141">From the Ambari UI click **Spark**, click **Configs**, and then expand **Custom spark-defaults**.</span><span class="sxs-lookup"><span data-stu-id="17404-141">From the Ambari UI click **Spark**, click **Configs**, and then expand **Custom spark-defaults**.</span></span>

    ![Set parameters using Ambari](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. <span data-ttu-id="17404-143">The default values are good to have 4 Spark applications run concurrently on the cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-143">The default values are good to have 4 Spark applications run concurrently on the cluster.</span></span> <span data-ttu-id="17404-144">You can changes these values from the user interface, as shown below.</span><span class="sxs-lookup"><span data-stu-id="17404-144">You can changes these values from the user interface, as shown below.</span></span>

    ![Set parameters using Ambari](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. <span data-ttu-id="17404-146">Click **Save** to save the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="17404-146">Click **Save** to save the configuration changes.</span></span> <span data-ttu-id="17404-147">At the top of the page, you will be prompted to restart all the affected services.</span><span class="sxs-lookup"><span data-stu-id="17404-147">At the top of the page, you will be prompted to restart all the affected services.</span></span> <span data-ttu-id="17404-148">Click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="17404-148">Click **Restart**.</span></span>

    ![Restart services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-the-parameters-for-an-application-running-in-jupyter-notebook"></a><span data-ttu-id="17404-150">Change the parameters for an application running in Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="17404-150">Change the parameters for an application running in Jupyter notebook</span></span>
<span data-ttu-id="17404-151">For applications running in the Jupyter notebook, you can use the `%%configure` magic to make the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="17404-151">For applications running in the Jupyter notebook, you can use the `%%configure` magic to make the configuration changes.</span></span> <span data-ttu-id="17404-152">Ideally, you must make such changes at the beginning of the application, before you run your first code cell.</span><span class="sxs-lookup"><span data-stu-id="17404-152">Ideally, you must make such changes at the beginning of the application, before you run your first code cell.</span></span> <span data-ttu-id="17404-153">This ensures that the configuration is applied to the Livy session, when it gets created.</span><span class="sxs-lookup"><span data-stu-id="17404-153">This ensures that the configuration is applied to the Livy session, when it gets created.</span></span> <span data-ttu-id="17404-154">If you want to change the configuration at a later stage in the application, you must use the `-f` parameter.</span><span class="sxs-lookup"><span data-stu-id="17404-154">If you want to change the configuration at a later stage in the application, you must use the `-f` parameter.</span></span> <span data-ttu-id="17404-155">However, by doing so all progress in the application will be lost.</span><span class="sxs-lookup"><span data-stu-id="17404-155">However, by doing so all progress in the application will be lost.</span></span>

<span data-ttu-id="17404-156">The snippet below shows how to change the configuration for an application running in Jupyter.</span><span class="sxs-lookup"><span data-stu-id="17404-156">The snippet below shows how to change the configuration for an application running in Jupyter.</span></span>

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, “numExecutors”:10}

<span data-ttu-id="17404-157">Configuration parameters must be passed in as a JSON string and must be on the next line after the magic, as shown in the example column.</span><span class="sxs-lookup"><span data-stu-id="17404-157">Configuration parameters must be passed in as a JSON string and must be on the next line after the magic, as shown in the example column.</span></span>

### <a name="change-the-parameters-for-an-application-submitted-using-spark-submit"></a><span data-ttu-id="17404-158">Change the parameters for an application submitted using spark-submit</span><span class="sxs-lookup"><span data-stu-id="17404-158">Change the parameters for an application submitted using spark-submit</span></span>
<span data-ttu-id="17404-159">Following command is an example of how to change the configuration parameters for a batch application that is submitted using `spark-submit`.</span><span class="sxs-lookup"><span data-stu-id="17404-159">Following command is an example of how to change the configuration parameters for a batch application that is submitted using `spark-submit`.</span></span>

    spark-submit --class <the application class to execute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-the-parameters-for-an-application-submitted-using-curl"></a><span data-ttu-id="17404-160">Change the parameters for an application submitted using cURL</span><span class="sxs-lookup"><span data-stu-id="17404-160">Change the parameters for an application submitted using cURL</span></span>
<span data-ttu-id="17404-161">Following command is an example of how to change the configuration parameters for a batch application that is submitted using using cURL.</span><span class="sxs-lookup"><span data-stu-id="17404-161">Following command is an example of how to change the configuration parameters for a batch application that is submitted using using cURL.</span></span>

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<the application class to execute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a><span data-ttu-id="17404-162">How do I change these parameters on a Spark Thrift Server?</span><span class="sxs-lookup"><span data-stu-id="17404-162">How do I change these parameters on a Spark Thrift Server?</span></span>
<span data-ttu-id="17404-163">Spark Thrift Server provides JDBC/ODBC access to a Spark cluster and is used to service Spark SQL queries.</span><span class="sxs-lookup"><span data-stu-id="17404-163">Spark Thrift Server provides JDBC/ODBC access to a Spark cluster and is used to service Spark SQL queries.</span></span> <span data-ttu-id="17404-164">Tools like Power BI, Tableau etc.</span><span class="sxs-lookup"><span data-stu-id="17404-164">Tools like Power BI, Tableau etc.</span></span> <span data-ttu-id="17404-165">use ODBC protocol to communicate with Spark Thrift Server to execute Spark SQL queries as a Spark Application.</span><span class="sxs-lookup"><span data-stu-id="17404-165">use ODBC protocol to communicate with Spark Thrift Server to execute Spark SQL queries as a Spark Application.</span></span> <span data-ttu-id="17404-166">When a Spark cluster is created, two instances of the Spark Thrift Server are started, one on each head node.</span><span class="sxs-lookup"><span data-stu-id="17404-166">When a Spark cluster is created, two instances of the Spark Thrift Server are started, one on each head node.</span></span> <span data-ttu-id="17404-167">Each Spark Thrift Server is visible as a Spark application in the YARN UI.</span><span class="sxs-lookup"><span data-stu-id="17404-167">Each Spark Thrift Server is visible as a Spark application in the YARN UI.</span></span>

<span data-ttu-id="17404-168">Spark Thrift Server uses Spark dynamic executor allocation and hence the `spark.executor.instances` is not used.</span><span class="sxs-lookup"><span data-stu-id="17404-168">Spark Thrift Server uses Spark dynamic executor allocation and hence the `spark.executor.instances` is not used.</span></span> <span data-ttu-id="17404-169">Instead, Spark Thrift Server uses `spark.dynamicAllocation.minExecutors` and `spark.dynamicAllocation.maxExecutors` to specify the executor count.</span><span class="sxs-lookup"><span data-stu-id="17404-169">Instead, Spark Thrift Server uses `spark.dynamicAllocation.minExecutors` and `spark.dynamicAllocation.maxExecutors` to specify the executor count.</span></span> <span data-ttu-id="17404-170">The configuration parameters `spark.executor.cores` and `spark.executor.memory` is used to modify the executor size.</span><span class="sxs-lookup"><span data-stu-id="17404-170">The configuration parameters `spark.executor.cores` and `spark.executor.memory` is used to modify the executor size.</span></span> <span data-ttu-id="17404-171">You can change these parameters as shown below.</span><span class="sxs-lookup"><span data-stu-id="17404-171">You can change these parameters as shown below.</span></span>

* <span data-ttu-id="17404-172">Expand the **Advanced spark-thrift-sparkconf** category to update the parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, and `spark.executor.memory`.</span><span class="sxs-lookup"><span data-stu-id="17404-172">Expand the **Advanced spark-thrift-sparkconf** category to update the parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, and `spark.executor.memory`.</span></span>

    ![Configure Spark thrift server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* <span data-ttu-id="17404-174">Expand the **Custom spark-thrift-sparkconf** category to update the parameter `spark.executor.cores`.</span><span class="sxs-lookup"><span data-stu-id="17404-174">Expand the **Custom spark-thrift-sparkconf** category to update the parameter `spark.executor.cores`.</span></span>

    ![Configure Spark thrift server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-the-driver-memory-of-the-spark-thrift-server"></a><span data-ttu-id="17404-176">How do I change the driver memory of the Spark Thrift Server?</span><span class="sxs-lookup"><span data-stu-id="17404-176">How do I change the driver memory of the Spark Thrift Server?</span></span>
<span data-ttu-id="17404-177">Spark Thrift Server driver memory is configured to 25% of the head node RAM size, provided the total RAM size of the head node is greater than 14GB.</span><span class="sxs-lookup"><span data-stu-id="17404-177">Spark Thrift Server driver memory is configured to 25% of the head node RAM size, provided the total RAM size of the head node is greater than 14GB.</span></span> <span data-ttu-id="17404-178">You can use the Ambari UI to change the driver memory configuration, as shown below.</span><span class="sxs-lookup"><span data-stu-id="17404-178">You can use the Ambari UI to change the driver memory configuration, as shown below.</span></span>

* <span data-ttu-id="17404-179">From the Ambari UI click **Spark**, click **Configs**, expand **Advanced spark-env**, and then provide the value for **spark_thrift_cmd_opts**.</span><span class="sxs-lookup"><span data-stu-id="17404-179">From the Ambari UI click **Spark**, click **Configs**, expand **Advanced spark-env**, and then provide the value for **spark_thrift_cmd_opts**.</span></span>

    ![Configure Spark thrift server RAM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-the-resources-back"></a><span data-ttu-id="17404-181">I do not use BI with Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-181">I do not use BI with Spark cluster.</span></span> <span data-ttu-id="17404-182">How do I take the resources back?</span><span class="sxs-lookup"><span data-stu-id="17404-182">How do I take the resources back?</span></span>
<span data-ttu-id="17404-183">Since we use Spark dynamic allocation, the only resources that are consumed by thrift server are the resources for the two application masters.</span><span class="sxs-lookup"><span data-stu-id="17404-183">Since we use Spark dynamic allocation, the only resources that are consumed by thrift server are the resources for the two application masters.</span></span> <span data-ttu-id="17404-184">To reclaim these resources you must stop the Thrift Server services running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="17404-184">To reclaim these resources you must stop the Thrift Server services running on the cluster.</span></span>

1. <span data-ttu-id="17404-185">From the Ambari UI, from the left pane, click **Spark**.</span><span class="sxs-lookup"><span data-stu-id="17404-185">From the Ambari UI, from the left pane, click **Spark**.</span></span>
2. <span data-ttu-id="17404-186">In the next page, click **Spark Thrift Servers**.</span><span class="sxs-lookup"><span data-stu-id="17404-186">In the next page, click **Spark Thrift Servers**.</span></span>

    ![Restart thrift server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. <span data-ttu-id="17404-188">You should see the two headnodes on which the Spark Thrift Server is running.</span><span class="sxs-lookup"><span data-stu-id="17404-188">You should see the two headnodes on which the Spark Thrift Server is running.</span></span> <span data-ttu-id="17404-189">Click one of the headnodes.</span><span class="sxs-lookup"><span data-stu-id="17404-189">Click one of the headnodes.</span></span>

    ![Restart thrift server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. <span data-ttu-id="17404-191">The next page lists all the services running on that headnode.</span><span class="sxs-lookup"><span data-stu-id="17404-191">The next page lists all the services running on that headnode.</span></span> <span data-ttu-id="17404-192">From the list click the drop-down button next to Spark Thrift Server, and then click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="17404-192">From the list click the drop-down button next to Spark Thrift Server, and then click **Stop**.</span></span>

    ![Restart thrift server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. <span data-ttu-id="17404-194">Repeat these steps on the other headnode as well.</span><span class="sxs-lookup"><span data-stu-id="17404-194">Repeat these steps on the other headnode as well.</span></span>

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-the-service"></a><span data-ttu-id="17404-195">My Jupyter notebooks are not running as expected.</span><span class="sxs-lookup"><span data-stu-id="17404-195">My Jupyter notebooks are not running as expected.</span></span> <span data-ttu-id="17404-196">How can I restart the service?</span><span class="sxs-lookup"><span data-stu-id="17404-196">How can I restart the service?</span></span>
1. <span data-ttu-id="17404-197">Launch the Ambari Web UI as shown above.</span><span class="sxs-lookup"><span data-stu-id="17404-197">Launch the Ambari Web UI as shown above.</span></span> <span data-ttu-id="17404-198">From the left navigation pane, click **Jupyter**, click **Service Actions**, and then click **Restart All**.</span><span class="sxs-lookup"><span data-stu-id="17404-198">From the left navigation pane, click **Jupyter**, click **Service Actions**, and then click **Restart All**.</span></span> <span data-ttu-id="17404-199">This will start the Jupyter service on all the headnodes.</span><span class="sxs-lookup"><span data-stu-id="17404-199">This will start the Jupyter service on all the headnodes.</span></span>

    <span data-ttu-id="17404-200">![Restart Jupyter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")</span><span class="sxs-lookup"><span data-stu-id="17404-200">![Restart Jupyter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")</span></span>

## <a name="how-do-i-know-if-i-am-running-out-of-resource"></a><span data-ttu-id="17404-201">How do I know if I am running out of resource?</span><span class="sxs-lookup"><span data-stu-id="17404-201">How do I know if I am running out of resource?</span></span>
1. <span data-ttu-id="17404-202">Launch the Yarn UI as shown above.</span><span class="sxs-lookup"><span data-stu-id="17404-202">Launch the Yarn UI as shown above.</span></span> <span data-ttu-id="17404-203">In Cluster Metrics table on top of the screen, check values of **Memory Used** and **Memory Total** columns.</span><span class="sxs-lookup"><span data-stu-id="17404-203">In Cluster Metrics table on top of the screen, check values of **Memory Used** and **Memory Total** columns.</span></span> <span data-ttu-id="17404-204">If the 2 values are very close, there might not be enough resources to start the next application.</span><span class="sxs-lookup"><span data-stu-id="17404-204">If the 2 values are very close, there might not be enough resources to start the next application.</span></span> <span data-ttu-id="17404-205">The same applies to the **VCores Used** and **VCores Total** columns.</span><span class="sxs-lookup"><span data-stu-id="17404-205">The same applies to the **VCores Used** and **VCores Total** columns.</span></span> <span data-ttu-id="17404-206">Also, in the main view, if there is an application stayed in **ACCEPTED** state and not transitioning into **RUNNING** nor **FAILED** state, this could also be an indication that it is not getting enough resources to start.</span><span class="sxs-lookup"><span data-stu-id="17404-206">Also, in the main view, if there is an application stayed in **ACCEPTED** state and not transitioning into **RUNNING** nor **FAILED** state, this could also be an indication that it is not getting enough resources to start.</span></span>

    <span data-ttu-id="17404-207">![Resource Limit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")</span><span class="sxs-lookup"><span data-stu-id="17404-207">![Resource Limit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")</span></span>

## <a name="how-do-i-kill-a-running-application-to-free-up-resource"></a><span data-ttu-id="17404-208">How do I kill a running application to free up resource?</span><span class="sxs-lookup"><span data-stu-id="17404-208">How do I kill a running application to free up resource?</span></span>
1. <span data-ttu-id="17404-209">In the Yarn UI, from the left panel, click **Running**.</span><span class="sxs-lookup"><span data-stu-id="17404-209">In the Yarn UI, from the left panel, click **Running**.</span></span> <span data-ttu-id="17404-210">From the list of running applications, determine the application to be killed and click on the **ID**.</span><span class="sxs-lookup"><span data-stu-id="17404-210">From the list of running applications, determine the application to be killed and click on the **ID**.</span></span>

    <span data-ttu-id="17404-211">![Kill App1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")</span><span class="sxs-lookup"><span data-stu-id="17404-211">![Kill App1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")</span></span>

2. <span data-ttu-id="17404-212">Click **Kill Application** on the top right corner, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="17404-212">Click **Kill Application** on the top right corner, then click **OK**.</span></span>

    <span data-ttu-id="17404-213">![Kill App2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")</span><span class="sxs-lookup"><span data-stu-id="17404-213">![Kill App2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")</span></span>

## <a name="seealso"></a><span data-ttu-id="17404-214">See also</span><span class="sxs-lookup"><span data-stu-id="17404-214">See also</span></span>
* [<span data-ttu-id="17404-215">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="17404-215">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="17404-216">Scenarios</span><span class="sxs-lookup"><span data-stu-id="17404-216">Scenarios</span></span>
* [<span data-ttu-id="17404-217">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="17404-217">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="17404-218">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="17404-218">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="17404-219">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="17404-219">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="17404-220">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="17404-220">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="17404-221">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17404-221">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="17404-222">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="17404-222">Create and run applications</span></span>
* [<span data-ttu-id="17404-223">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="17404-223">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="17404-224">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="17404-224">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="17404-225">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="17404-225">Tools and extensions</span></span>
* [<span data-ttu-id="17404-226">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="17404-226">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="17404-227">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="17404-227">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="17404-228">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17404-228">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="17404-229">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="17404-229">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="17404-230">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="17404-230">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="17404-231">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="17404-231">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="17404-232">Manage resources</span><span class="sxs-lookup"><span data-stu-id="17404-232">Manage resources</span></span>
* [<span data-ttu-id="17404-233">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17404-233">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md


[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md

















