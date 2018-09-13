---
title: Debug Apache Spark jobs running on Azure HDInsight
description: Use YARN UI, Spark UI, and Spark History server to track and debug jobs running on a Spark cluster in Azure HDInsight
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 12/20/2017
ms.author: jasonh
ms.openlocfilehash: 6b62c1ff4649ac72f5c4d04cd7507e7db0166b6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868380"
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="7dc54-103">Debug Apache Spark jobs running on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dc54-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="7dc54-104">In this article, you learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span><span class="sxs-lookup"><span data-stu-id="7dc54-104">In this article, you learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="7dc54-105">You start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-105">You start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="7dc54-106">You can use the following steps to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-106">You can use the following steps to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dc54-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7dc54-107">Prerequisites</span></span>
<span data-ttu-id="7dc54-108">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="7dc54-108">You must have the following:</span></span>

* <span data-ttu-id="7dc54-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7dc54-109">An Azure subscription.</span></span> <span data-ttu-id="7dc54-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7dc54-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7dc54-111">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dc54-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7dc54-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7dc54-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="7dc54-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="7dc54-114">For instructions on how to run this notebook, follow the link.</span><span class="sxs-lookup"><span data-stu-id="7dc54-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="7dc54-115">Track an application in the YARN UI</span><span class="sxs-lookup"><span data-stu-id="7dc54-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="7dc54-116">Launch the YARN UI.</span><span class="sxs-lookup"><span data-stu-id="7dc54-116">Launch the YARN UI.</span></span> <span data-ttu-id="7dc54-117">Click **Cluster Dashboard**, and then click **YARN**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-117">Click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Launch YARN UI](./media/apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="7dc54-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="7dc54-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="7dc54-120">To launch the Ambari UI, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-120">To launch the Ambari UI, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="7dc54-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active Resource Manager, and then click **Resource Manager UI**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active Resource Manager, and then click **Resource Manager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="7dc54-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span><span class="sxs-lookup"><span data-stu-id="7dc54-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="7dc54-123">Click the application ID against the application name to get more information about the job.</span><span class="sxs-lookup"><span data-stu-id="7dc54-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="7dc54-124">This launches the application view.</span><span class="sxs-lookup"><span data-stu-id="7dc54-124">This launches the application view.</span></span>
   
    ![Find Spark application ID](./media/apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="7dc54-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span><span class="sxs-lookup"><span data-stu-id="7dc54-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="7dc54-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="7dc54-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="7dc54-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span><span class="sxs-lookup"><span data-stu-id="7dc54-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Download container logs](./media/apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="7dc54-130">Track an application in the Spark UI</span><span class="sxs-lookup"><span data-stu-id="7dc54-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="7dc54-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span><span class="sxs-lookup"><span data-stu-id="7dc54-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="7dc54-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span><span class="sxs-lookup"><span data-stu-id="7dc54-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="7dc54-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="7dc54-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![View Spark jobs](./media/apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="7dc54-135">Click the **Executors** tab to see processing and storage information for each executor.</span><span class="sxs-lookup"><span data-stu-id="7dc54-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="7dc54-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span><span class="sxs-lookup"><span data-stu-id="7dc54-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![View Spark executors](./media/apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="7dc54-138">Click the **Stages** tab to see the stages associated with the application.</span><span class="sxs-lookup"><span data-stu-id="7dc54-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![View Spark stages](./media/apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="7dc54-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span><span class="sxs-lookup"><span data-stu-id="7dc54-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![View Spark stages](./media/apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="7dc54-142">From the stage details page, you can launch DAG Visualization.</span><span class="sxs-lookup"><span data-stu-id="7dc54-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="7dc54-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span><span class="sxs-lookup"><span data-stu-id="7dc54-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![View Spark stages DAG visualization](./media/apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="7dc54-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span><span class="sxs-lookup"><span data-stu-id="7dc54-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="7dc54-146">Each blue box in the graph represents a Spark operation invoked from the application.</span><span class="sxs-lookup"><span data-stu-id="7dc54-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="7dc54-147">From the stage details page, you can also launch the application timeline view.</span><span class="sxs-lookup"><span data-stu-id="7dc54-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="7dc54-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span><span class="sxs-lookup"><span data-stu-id="7dc54-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![View Spark stages event timeline](./media/apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="7dc54-150">This displays the Spark events in the form of a timeline.</span><span class="sxs-lookup"><span data-stu-id="7dc54-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="7dc54-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span><span class="sxs-lookup"><span data-stu-id="7dc54-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="7dc54-152">The image above captures the timeline view for a given stage.</span><span class="sxs-lookup"><span data-stu-id="7dc54-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7dc54-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span><span class="sxs-lookup"><span data-stu-id="7dc54-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="7dc54-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span><span class="sxs-lookup"><span data-stu-id="7dc54-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="7dc54-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span><span class="sxs-lookup"><span data-stu-id="7dc54-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="7dc54-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span><span class="sxs-lookup"><span data-stu-id="7dc54-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="7dc54-157">Scala version</span><span class="sxs-lookup"><span data-stu-id="7dc54-157">Scala version</span></span>
     * <span data-ttu-id="7dc54-158">Event log directory associated with the cluster</span><span class="sxs-lookup"><span data-stu-id="7dc54-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="7dc54-159">Number of executor cores for the application</span><span class="sxs-lookup"><span data-stu-id="7dc54-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="7dc54-160">Etc.</span><span class="sxs-lookup"><span data-stu-id="7dc54-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="7dc54-161">Find information about completed jobs using the Spark History Server</span><span class="sxs-lookup"><span data-stu-id="7dc54-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="7dc54-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span><span class="sxs-lookup"><span data-stu-id="7dc54-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="7dc54-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Launch Spark History Server](./media/apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="7dc54-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="7dc54-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="7dc54-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="7dc54-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span><span class="sxs-lookup"><span data-stu-id="7dc54-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="7dc54-168">You see all the completed applications listed.</span><span class="sxs-lookup"><span data-stu-id="7dc54-168">You see all the completed applications listed.</span></span> <span data-ttu-id="7dc54-169">Click an application ID to drill down into an application for more info.</span><span class="sxs-lookup"><span data-stu-id="7dc54-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Launch Spark History Server](./media/apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="7dc54-171">See also</span><span class="sxs-lookup"><span data-stu-id="7dc54-171">See also</span></span>
*  [<span data-ttu-id="7dc54-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dc54-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
*  [<span data-ttu-id="7dc54-173">Debug Spark Jobs using extended Spark History Server</span><span class="sxs-lookup"><span data-stu-id="7dc54-173">Debug Spark Jobs using extended Spark History Server</span></span>](apache-azure-spark-history-server.md)

### <a name="for-data-analysts"></a><span data-ttu-id="7dc54-174">For data analysts</span><span class="sxs-lookup"><span data-stu-id="7dc54-174">For data analysts</span></span>

* [<span data-ttu-id="7dc54-175">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="7dc54-175">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7dc54-176">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="7dc54-176">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7dc54-177">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dc54-177">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="7dc54-178">Application Insight telemetry data analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dc54-178">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](apache-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="7dc54-179">Use Caffe on Azure HDInsight Spark for distributed deep learning</span><span class="sxs-lookup"><span data-stu-id="7dc54-179">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](apache-spark-deep-learning-caffe.md)

### <a name="for-spark-developers"></a><span data-ttu-id="7dc54-180">For Spark developers</span><span class="sxs-lookup"><span data-stu-id="7dc54-180">For Spark developers</span></span>

* [<span data-ttu-id="7dc54-181">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="7dc54-181">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7dc54-182">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="7dc54-182">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="7dc54-183">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="7dc54-183">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7dc54-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="7dc54-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7dc54-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dc54-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7dc54-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dc54-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7dc54-187">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="7dc54-187">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7dc54-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="7dc54-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)


