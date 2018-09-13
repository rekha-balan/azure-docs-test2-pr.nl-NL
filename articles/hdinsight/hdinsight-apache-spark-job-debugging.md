---
title: Debug jobs running on Apache Spark cluster in Azure HDInsight | Microsoft Docs
description: Use YARN UI, Spark UI, and Spark History server to track and debug jobs running on a Spark cluster in Azure HDInsight
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 51d4b40f278e8d991cb976c51a930e7ae5741b7c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549594"
---
# <a name="track-and-debug-jobs-running-on-apache-spark-cluster-in-hdinsight"></a><span data-ttu-id="6b0bb-103">Track and debug jobs running on Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b0bb-103">Track and debug jobs running on Apache Spark cluster in HDInsight</span></span>

<span data-ttu-id="6b0bb-104">In this article you will learn how to track and debug Spark jobs using the YARN UI, Spark UI, and the Spark History Server.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-104">In this article you will learn how to track and debug Spark jobs using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="6b0bb-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="6b0bb-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b0bb-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6b0bb-107">Prerequisites</span></span>
<span data-ttu-id="6b0bb-108">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="6b0bb-108">You must have the following:</span></span>

* <span data-ttu-id="6b0bb-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-109">An Azure subscription.</span></span> <span data-ttu-id="6b0bb-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6b0bb-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6b0bb-111">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="6b0bb-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6b0bb-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="6b0bb-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="6b0bb-114">For instructions on how to run this notebook, follow the link.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="6b0bb-115">Track an application in the YARN UI</span><span class="sxs-lookup"><span data-stu-id="6b0bb-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="6b0bb-116">Launch the YARN UI.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-116">Launch the YARN UI.</span></span> <span data-ttu-id="6b0bb-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Launch YARN UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="6b0bb-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="6b0bb-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="6b0bb-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="6b0bb-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span><span class="sxs-lookup"><span data-stu-id="6b0bb-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="6b0bb-123">Click the application ID against the application name to get more information about the job.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="6b0bb-124">This launches the application view.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-124">This launches the application view.</span></span>
   
    ![Find Spark application ID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="6b0bb-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="6b0bb-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="6b0bb-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="6b0bb-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Download container logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="6b0bb-130">Track an application in the Spark UI</span><span class="sxs-lookup"><span data-stu-id="6b0bb-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="6b0bb-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="6b0bb-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="6b0bb-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![View Spark jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="6b0bb-135">Click the **Executors** tab to see processing and storage information for each executor.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="6b0bb-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![View Spark executors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="6b0bb-138">Click the **Stages** tab to see the stages associated with the application.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![View Spark stages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="6b0bb-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![View Spark stages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="6b0bb-142">From the stage details page, you can launch DAG Visualization.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="6b0bb-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![View Spark stages DAG visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="6b0bb-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="6b0bb-146">Each blue box in the graph represents a Spark operation invoked from the application.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="6b0bb-147">From the stage details page, you can also launch the application timeline view.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="6b0bb-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![View Spark stages event timeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="6b0bb-150">This displays the Spark events in the form of a timeline.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="6b0bb-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="6b0bb-152">The image above captures the timeline view for a given stage.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="6b0bb-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="6b0bb-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="6b0bb-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="6b0bb-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span><span class="sxs-lookup"><span data-stu-id="6b0bb-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="6b0bb-157">Scala version</span><span class="sxs-lookup"><span data-stu-id="6b0bb-157">Scala version</span></span>
     * <span data-ttu-id="6b0bb-158">Event log directory associated with the cluster</span><span class="sxs-lookup"><span data-stu-id="6b0bb-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="6b0bb-159">Number of executor cores for the application</span><span class="sxs-lookup"><span data-stu-id="6b0bb-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="6b0bb-160">Etc.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="6b0bb-161">Find information about completed jobs using the Spark History Server</span><span class="sxs-lookup"><span data-stu-id="6b0bb-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="6b0bb-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="6b0bb-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Launch Spark History Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="6b0bb-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="6b0bb-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="6b0bb-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="6b0bb-168">You will see all the completed applications listed.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="6b0bb-169">Click an application ID to drill down into an application for more info.</span><span class="sxs-lookup"><span data-stu-id="6b0bb-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Launch Spark History Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="seealso"></a><span data-ttu-id="6b0bb-171">See also</span><span class="sxs-lookup"><span data-stu-id="6b0bb-171">See also</span></span>
* [<span data-ttu-id="6b0bb-172">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b0bb-172">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="6b0bb-173">Scenarios</span><span class="sxs-lookup"><span data-stu-id="6b0bb-173">Scenarios</span></span>
* [<span data-ttu-id="6b0bb-174">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="6b0bb-174">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="6b0bb-175">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="6b0bb-175">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6b0bb-176">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="6b0bb-176">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="6b0bb-177">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="6b0bb-177">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6b0bb-178">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b0bb-178">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="6b0bb-179">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="6b0bb-179">Create and run applications</span></span>
* [<span data-ttu-id="6b0bb-180">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="6b0bb-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6b0bb-181">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="6b0bb-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="6b0bb-182">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="6b0bb-182">Tools and extensions</span></span>
* [<span data-ttu-id="6b0bb-183">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="6b0bb-183">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6b0bb-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="6b0bb-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="6b0bb-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b0bb-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="6b0bb-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b0bb-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6b0bb-187">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="6b0bb-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="6b0bb-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="6b0bb-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="6b0bb-189">Manage resources</span><span class="sxs-lookup"><span data-stu-id="6b0bb-189">Manage resources</span></span>
* [<span data-ttu-id="6b0bb-190">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b0bb-190">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)












