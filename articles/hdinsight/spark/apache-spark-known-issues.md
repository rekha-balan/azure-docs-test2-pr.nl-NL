---
title: Troubleshoot issues with Apache Spark cluster in Azure HDInsight
description: Learn about issues related to Apache Spark clusters in Azure HDInsight and how to work around those.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: jasonh
ms.openlocfilehash: 92baa28393100abe3d7694920e5ee327966db927
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868985"
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="c2878-103">Known issues for Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="c2878-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span><span class="sxs-lookup"><span data-stu-id="c2878-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="c2878-105">Livy leaks interactive session</span><span class="sxs-lookup"><span data-stu-id="c2878-105">Livy leaks interactive session</span></span>
<span data-ttu-id="c2878-106">When Livy restarts (from Ambari or because of headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session is leaked.</span><span class="sxs-lookup"><span data-stu-id="c2878-106">When Livy restarts (from Ambari or because of headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session is leaked.</span></span> <span data-ttu-id="c2878-107">As a result, new jobs can be stuck in the Accepted state.</span><span class="sxs-lookup"><span data-stu-id="c2878-107">As a result, new jobs can be stuck in the Accepted state.</span></span>

<span data-ttu-id="c2878-108">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="c2878-108">**Mitigation:**</span></span>

<span data-ttu-id="c2878-109">Use the following procedure to work around the issue:</span><span class="sxs-lookup"><span data-stu-id="c2878-109">Use the following procedure to work around the issue:</span></span>

1. <span data-ttu-id="c2878-110">Ssh into headnode.</span><span class="sxs-lookup"><span data-stu-id="c2878-110">Ssh into headnode.</span></span> <span data-ttu-id="c2878-111">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c2878-111">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c2878-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span><span class="sxs-lookup"><span data-stu-id="c2878-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="c2878-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified.</span><span class="sxs-lookup"><span data-stu-id="c2878-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified.</span></span> <span data-ttu-id="c2878-114">For the Livy session started by Jupyter notebook, the job name starts with remotesparkmagics_\*.</span><span class="sxs-lookup"><span data-stu-id="c2878-114">For the Livy session started by Jupyter notebook, the job name starts with remotesparkmagics_\*.</span></span> 
3. <span data-ttu-id="c2878-115">Run the following command to kill those jobs.</span><span class="sxs-lookup"><span data-stu-id="c2878-115">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="c2878-116">New jobs start running.</span><span class="sxs-lookup"><span data-stu-id="c2878-116">New jobs start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="c2878-117">Spark History Server not started</span><span class="sxs-lookup"><span data-stu-id="c2878-117">Spark History Server not started</span></span>
<span data-ttu-id="c2878-118">Spark History Server is not started automatically after a cluster is created.</span><span class="sxs-lookup"><span data-stu-id="c2878-118">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="c2878-119">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="c2878-119">**Mitigation:**</span></span> 

<span data-ttu-id="c2878-120">Manually start the history server from Ambari.</span><span class="sxs-lookup"><span data-stu-id="c2878-120">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="c2878-121">Permission issue in Spark log directory</span><span class="sxs-lookup"><span data-stu-id="c2878-121">Permission issue in Spark log directory</span></span>
<span data-ttu-id="c2878-122">hdiuser gets the following error when submitting a job using spark-submit:</span><span class="sxs-lookup"><span data-stu-id="c2878-122">hdiuser gets the following error when submitting a job using spark-submit:</span></span>

```
java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied)
```
<span data-ttu-id="c2878-123">And no driver log is written.</span><span class="sxs-lookup"><span data-stu-id="c2878-123">And no driver log is written.</span></span> 

<span data-ttu-id="c2878-124">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="c2878-124">**Mitigation:**</span></span>

1. <span data-ttu-id="c2878-125">Add hdiuser to the Hadoop group.</span><span class="sxs-lookup"><span data-stu-id="c2878-125">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="c2878-126">Provide 777 permissions on /var/log/spark after cluster creation.</span><span class="sxs-lookup"><span data-stu-id="c2878-126">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="c2878-127">Update the spark log location using Ambari to be a directory with 777 permissions.</span><span class="sxs-lookup"><span data-stu-id="c2878-127">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="c2878-128">Run spark-submit as sudo.</span><span class="sxs-lookup"><span data-stu-id="c2878-128">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="c2878-129">Spark-Phoenix connector is not supported</span><span class="sxs-lookup"><span data-stu-id="c2878-129">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="c2878-130">HDInsight Spark clusters do not support the Spark-Phoenix connector.</span><span class="sxs-lookup"><span data-stu-id="c2878-130">HDInsight Spark clusters do not support the Spark-Phoenix connector.</span></span>

<span data-ttu-id="c2878-131">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="c2878-131">**Mitigation:**</span></span>

<span data-ttu-id="c2878-132">You must use the Spark-HBase connector instead.</span><span class="sxs-lookup"><span data-stu-id="c2878-132">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="c2878-133">For the instructions, see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="c2878-133">For the instructions, see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="c2878-134">Issues related to Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="c2878-134">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="c2878-135">Following are some known issues related to Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="c2878-135">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="c2878-136">Notebooks with non-ASCII characters in filenames</span><span class="sxs-lookup"><span data-stu-id="c2878-136">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="c2878-137">Do not use non-ASCII characters in Jupyter notebook filenames.</span><span class="sxs-lookup"><span data-stu-id="c2878-137">Do not use non-ASCII characters in Jupyter notebook filenames.</span></span> <span data-ttu-id="c2878-138">If you try to upload a file through the Jupyter UI, which has a non-ASCII filename, it fails without any error message.</span><span class="sxs-lookup"><span data-stu-id="c2878-138">If you try to upload a file through the Jupyter UI, which has a non-ASCII filename, it fails without any error message.</span></span> <span data-ttu-id="c2878-139">Jupyter does not let you upload the file, but it does not throw a visible error either.</span><span class="sxs-lookup"><span data-stu-id="c2878-139">Jupyter does not let you upload the file, but it does not throw a visible error either.</span></span>

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="c2878-140">Error while loading notebooks of larger sizes</span><span class="sxs-lookup"><span data-stu-id="c2878-140">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="c2878-141">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span><span class="sxs-lookup"><span data-stu-id="c2878-141">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="c2878-142">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="c2878-142">**Mitigation:**</span></span>

<span data-ttu-id="c2878-143">If you get this error, it does not mean your data is corrupt or lost.</span><span class="sxs-lookup"><span data-stu-id="c2878-143">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="c2878-144">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span><span class="sxs-lookup"><span data-stu-id="c2878-144">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="c2878-145">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c2878-145">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="c2878-146">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span><span class="sxs-lookup"><span data-stu-id="c2878-146">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="c2878-147">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span><span class="sxs-lookup"><span data-stu-id="c2878-147">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="c2878-148">From there, you can clear the output of your notebook and resave it to minimize the notebook’s size.</span><span class="sxs-lookup"><span data-stu-id="c2878-148">From there, you can clear the output of your notebook and resave it to minimize the notebook’s size.</span></span>

<span data-ttu-id="c2878-149">To prevent this error from happening in the future, you must follow some best practices:</span><span class="sxs-lookup"><span data-stu-id="c2878-149">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="c2878-150">It is important to keep the notebook size small.</span><span class="sxs-lookup"><span data-stu-id="c2878-150">It is important to keep the notebook size small.</span></span> <span data-ttu-id="c2878-151">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span><span class="sxs-lookup"><span data-stu-id="c2878-151">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="c2878-152">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too large.</span><span class="sxs-lookup"><span data-stu-id="c2878-152">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too large.</span></span>
* <span data-ttu-id="c2878-153">Also, when you save a notebook, clear all output cells to reduce the size.</span><span class="sxs-lookup"><span data-stu-id="c2878-153">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="c2878-154">Notebook initial startup takes longer than expected</span><span class="sxs-lookup"><span data-stu-id="c2878-154">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="c2878-155">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span><span class="sxs-lookup"><span data-stu-id="c2878-155">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="c2878-156">**Explanation:**</span><span class="sxs-lookup"><span data-stu-id="c2878-156">**Explanation:**</span></span>

<span data-ttu-id="c2878-157">This happens because when the first code cell is run.</span><span class="sxs-lookup"><span data-stu-id="c2878-157">This happens because when the first code cell is run.</span></span> <span data-ttu-id="c2878-158">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span><span class="sxs-lookup"><span data-stu-id="c2878-158">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="c2878-159">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="c2878-159">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="c2878-160">Jupyter notebook timeout in creating the session</span><span class="sxs-lookup"><span data-stu-id="c2878-160">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="c2878-161">When Spark cluster is out of resources, the Spark and PySpark kernels in the Jupyter notebook will time out trying to create the session.</span><span class="sxs-lookup"><span data-stu-id="c2878-161">When Spark cluster is out of resources, the Spark and PySpark kernels in the Jupyter notebook will time out trying to create the session.</span></span> 

<span data-ttu-id="c2878-162">**Mitigations:**</span><span class="sxs-lookup"><span data-stu-id="c2878-162">**Mitigations:**</span></span> 

1. <span data-ttu-id="c2878-163">Free up some resources in your Spark cluster by:</span><span class="sxs-lookup"><span data-stu-id="c2878-163">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="c2878-164">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span><span class="sxs-lookup"><span data-stu-id="c2878-164">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="c2878-165">Stopping other Spark applications from YARN.</span><span class="sxs-lookup"><span data-stu-id="c2878-165">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="c2878-166">Restart the notebook you were trying to start up.</span><span class="sxs-lookup"><span data-stu-id="c2878-166">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="c2878-167">Enough resources should be available for you to create a session now.</span><span class="sxs-lookup"><span data-stu-id="c2878-167">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2878-168">See also</span><span class="sxs-lookup"><span data-stu-id="c2878-168">See also</span></span>
* [<span data-ttu-id="c2878-169">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-169">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c2878-170">Scenarios</span><span class="sxs-lookup"><span data-stu-id="c2878-170">Scenarios</span></span>
* [<span data-ttu-id="c2878-171">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="c2878-171">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c2878-172">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="c2878-172">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c2878-173">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="c2878-173">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c2878-174">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-174">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c2878-175">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="c2878-175">Create and run applications</span></span>
* [<span data-ttu-id="c2878-176">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="c2878-176">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c2878-177">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="c2878-177">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c2878-178">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="c2878-178">Tools and extensions</span></span>
* [<span data-ttu-id="c2878-179">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="c2878-179">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c2878-180">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="c2878-180">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c2878-181">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-181">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c2878-182">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-182">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c2878-183">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="c2878-183">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c2878-184">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="c2878-184">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c2878-185">Manage resources</span><span class="sxs-lookup"><span data-stu-id="c2878-185">Manage resources</span></span>
* [<span data-ttu-id="c2878-186">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-186">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="c2878-187">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2878-187">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)

