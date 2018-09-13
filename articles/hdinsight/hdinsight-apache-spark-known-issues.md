---
title: Known issues for Apache Spark cluster in Azure HDInsight | Microsoft Docs
description: Known issues of Apache Spark clusters in Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: nitinme
ms.openlocfilehash: 2ba5f280b38622b6a0c966d76617cd5698420b92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662135"
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="88d6e-103">Known issues for Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="88d6e-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span><span class="sxs-lookup"><span data-stu-id="88d6e-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="88d6e-105">Livy leaks interactive session</span><span class="sxs-lookup"><span data-stu-id="88d6e-105">Livy leaks interactive session</span></span>
<span data-ttu-id="88d6e-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span><span class="sxs-lookup"><span data-stu-id="88d6e-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="88d6e-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span><span class="sxs-lookup"><span data-stu-id="88d6e-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="88d6e-108">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-108">**Mitigation:**</span></span>

<span data-ttu-id="88d6e-109">Use the following procedure to workaround the issue:</span><span class="sxs-lookup"><span data-stu-id="88d6e-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="88d6e-110">Ssh into headnode.</span><span class="sxs-lookup"><span data-stu-id="88d6e-110">Ssh into headnode.</span></span> <span data-ttu-id="88d6e-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="88d6e-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="88d6e-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span><span class="sxs-lookup"><span data-stu-id="88d6e-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="88d6e-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_\*.</span><span class="sxs-lookup"><span data-stu-id="88d6e-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_\*.</span></span> 
3. <span data-ttu-id="88d6e-114">Run the following command to kill those jobs.</span><span class="sxs-lookup"><span data-stu-id="88d6e-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="88d6e-115">New jobs will start running.</span><span class="sxs-lookup"><span data-stu-id="88d6e-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="88d6e-116">Spark History Server not started</span><span class="sxs-lookup"><span data-stu-id="88d6e-116">Spark History Server not started</span></span>
<span data-ttu-id="88d6e-117">Spark History Server is not started automatically after a cluster is created.</span><span class="sxs-lookup"><span data-stu-id="88d6e-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="88d6e-118">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-118">**Mitigation:**</span></span> 

<span data-ttu-id="88d6e-119">Manually start the history server from Ambari.</span><span class="sxs-lookup"><span data-stu-id="88d6e-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="88d6e-120">Permission issue in Spark log directory</span><span class="sxs-lookup"><span data-stu-id="88d6e-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="88d6e-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span><span class="sxs-lookup"><span data-stu-id="88d6e-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="88d6e-122">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-122">**Mitigation:**</span></span>

1. <span data-ttu-id="88d6e-123">Add hdiuser to the Hadoop group.</span><span class="sxs-lookup"><span data-stu-id="88d6e-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="88d6e-124">Provide 777 permissions on /var/log/spark after cluster creation.</span><span class="sxs-lookup"><span data-stu-id="88d6e-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="88d6e-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span><span class="sxs-lookup"><span data-stu-id="88d6e-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="88d6e-126">Run spark-submit as sudo.</span><span class="sxs-lookup"><span data-stu-id="88d6e-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="88d6e-127">Spark-Phoenix connector is not supported</span><span class="sxs-lookup"><span data-stu-id="88d6e-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="88d6e-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="88d6e-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="88d6e-129">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-129">**Mitigation:**</span></span>

<span data-ttu-id="88d6e-130">You must use the Spark-HBase connector instead.</span><span class="sxs-lookup"><span data-stu-id="88d6e-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="88d6e-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="88d6e-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="88d6e-132">Issues related to Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="88d6e-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="88d6e-133">Following are some known issues related to Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="88d6e-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="88d6e-134">Notebooks with non-ASCII characters in filenames</span><span class="sxs-lookup"><span data-stu-id="88d6e-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="88d6e-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span><span class="sxs-lookup"><span data-stu-id="88d6e-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="88d6e-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span><span class="sxs-lookup"><span data-stu-id="88d6e-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="88d6e-137">Error while loading notebooks of larger sizes</span><span class="sxs-lookup"><span data-stu-id="88d6e-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="88d6e-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span><span class="sxs-lookup"><span data-stu-id="88d6e-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="88d6e-139">**Mitigation:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-139">**Mitigation:**</span></span>

<span data-ttu-id="88d6e-140">If you get this error, it does not mean your data is corrupt or lost.</span><span class="sxs-lookup"><span data-stu-id="88d6e-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="88d6e-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span><span class="sxs-lookup"><span data-stu-id="88d6e-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="88d6e-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="88d6e-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="88d6e-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span><span class="sxs-lookup"><span data-stu-id="88d6e-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="88d6e-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span><span class="sxs-lookup"><span data-stu-id="88d6e-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="88d6e-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span><span class="sxs-lookup"><span data-stu-id="88d6e-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="88d6e-146">To prevent this error from happening in the future, you must follow some best practices:</span><span class="sxs-lookup"><span data-stu-id="88d6e-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="88d6e-147">It is important to keep the notebook size small.</span><span class="sxs-lookup"><span data-stu-id="88d6e-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="88d6e-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span><span class="sxs-lookup"><span data-stu-id="88d6e-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="88d6e-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span><span class="sxs-lookup"><span data-stu-id="88d6e-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="88d6e-150">Also, when you save a notebook, clear all output cells to reduce the size.</span><span class="sxs-lookup"><span data-stu-id="88d6e-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="88d6e-151">Notebook initial startup takes longer than expected</span><span class="sxs-lookup"><span data-stu-id="88d6e-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="88d6e-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span><span class="sxs-lookup"><span data-stu-id="88d6e-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="88d6e-153">**Explanation:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-153">**Explanation:**</span></span>

<span data-ttu-id="88d6e-154">This happens because when the first code cell is run.</span><span class="sxs-lookup"><span data-stu-id="88d6e-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="88d6e-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span><span class="sxs-lookup"><span data-stu-id="88d6e-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="88d6e-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="88d6e-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="88d6e-157">Jupyter notebook timeout in creating the session</span><span class="sxs-lookup"><span data-stu-id="88d6e-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="88d6e-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span><span class="sxs-lookup"><span data-stu-id="88d6e-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="88d6e-159">**Mitigations:**</span><span class="sxs-lookup"><span data-stu-id="88d6e-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="88d6e-160">Free up some resources in your Spark cluster by:</span><span class="sxs-lookup"><span data-stu-id="88d6e-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="88d6e-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span><span class="sxs-lookup"><span data-stu-id="88d6e-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="88d6e-162">Stopping other Spark applications from YARN.</span><span class="sxs-lookup"><span data-stu-id="88d6e-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="88d6e-163">Restart the notebook you were trying to start up.</span><span class="sxs-lookup"><span data-stu-id="88d6e-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="88d6e-164">Enough resources should be available for you to create a session now.</span><span class="sxs-lookup"><span data-stu-id="88d6e-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="88d6e-165">See also</span><span class="sxs-lookup"><span data-stu-id="88d6e-165">See also</span></span>
* [<span data-ttu-id="88d6e-166">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="88d6e-167">Scenarios</span><span class="sxs-lookup"><span data-stu-id="88d6e-167">Scenarios</span></span>
* [<span data-ttu-id="88d6e-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="88d6e-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="88d6e-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="88d6e-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="88d6e-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="88d6e-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="88d6e-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="88d6e-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="88d6e-172">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="88d6e-173">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="88d6e-173">Create and run applications</span></span>
* [<span data-ttu-id="88d6e-174">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="88d6e-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="88d6e-175">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="88d6e-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="88d6e-176">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="88d6e-176">Tools and extensions</span></span>
* [<span data-ttu-id="88d6e-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="88d6e-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="88d6e-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="88d6e-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="88d6e-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="88d6e-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="88d6e-181">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="88d6e-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="88d6e-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="88d6e-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="88d6e-183">Manage resources</span><span class="sxs-lookup"><span data-stu-id="88d6e-183">Manage resources</span></span>
* [<span data-ttu-id="88d6e-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="88d6e-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="88d6e-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

