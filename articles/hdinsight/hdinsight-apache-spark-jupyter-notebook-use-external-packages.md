---
title: Use custom Maven packages with Jupyter notebooks in Spark on Azure | Microsoft Docs
description: Step-by-step instructions on how to configure Jupyter notebooks available with HDInsight Spark clusters to use external Spark packages.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 0dbe32816d67f8977804f4744f0df7ccba59a737
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550727"
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="df613-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [Using cell magic](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Using Script Action](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="df613-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span><span class="sxs-lookup"><span data-stu-id="df613-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="df613-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span><span class="sxs-lookup"><span data-stu-id="df613-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="df613-108">You can also get a list of available packages from other sources.</span><span class="sxs-lookup"><span data-stu-id="df613-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="df613-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="df613-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="df613-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="df613-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="df613-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="df613-111">Prerequisites</span></span>
<span data-ttu-id="df613-112">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="df613-112">You must have the following:</span></span>

* <span data-ttu-id="df613-113">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="df613-113">An Azure subscription.</span></span> <span data-ttu-id="df613-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="df613-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="df613-115">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df613-115">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="df613-116">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="df613-116">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="df613-117">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="df613-117">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="df613-118">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="df613-118">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="df613-119">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="df613-119">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="df613-120">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="df613-120">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="df613-121">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="df613-121">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser. Replace **CLUSTERNAME** with the name of your cluster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="df613-124">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="df613-124">Create a new notebook.</span></span> <span data-ttu-id="df613-125">Click **New**, and then click **Spark**.</span><span class="sxs-lookup"><span data-stu-id="df613-125">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="df613-126">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="df613-126">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="df613-127">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="df613-127">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="df613-128">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="df613-128">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="df613-129">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="df613-129">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="df613-130">You will use the `%%configure` magic to configure the notebook to use an external package.</span><span class="sxs-lookup"><span data-stu-id="df613-130">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="df613-131">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span><span class="sxs-lookup"><span data-stu-id="df613-131">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="df613-132">This ensures that the kernel is configured to use the package before the session starts.</span><span class="sxs-lookup"><span data-stu-id="df613-132">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    >If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.

    | <span data-ttu-id="df613-134">HDInsight version</span><span class="sxs-lookup"><span data-stu-id="df613-134">HDInsight version</span></span> | <span data-ttu-id="df613-135">Command</span><span class="sxs-lookup"><span data-stu-id="df613-135">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="df613-136">For HDInsight 3.3 and HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="df613-136">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="df613-137">For HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="df613-137">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="df613-138">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span><span class="sxs-lookup"><span data-stu-id="df613-138">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="df613-139">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span><span class="sxs-lookup"><span data-stu-id="df613-139">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="df613-140">Here's how you construct the coordinates for a package.</span><span class="sxs-lookup"><span data-stu-id="df613-140">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="df613-141">a.</span><span class="sxs-lookup"><span data-stu-id="df613-141">a.</span></span> <span data-ttu-id="df613-142">Locate the package in the Maven Repository.</span><span class="sxs-lookup"><span data-stu-id="df613-142">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="df613-143">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="df613-143">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="df613-144">b.</span><span class="sxs-lookup"><span data-stu-id="df613-144">b.</span></span> <span data-ttu-id="df613-145">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span><span class="sxs-lookup"><span data-stu-id="df613-145">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="df613-146">Make sure that the values you gather match your cluster.</span><span class="sxs-lookup"><span data-stu-id="df613-146">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="df613-147">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span><span class="sxs-lookup"><span data-stu-id="df613-147">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="df613-148">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span><span class="sxs-lookup"><span data-stu-id="df613-148">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="df613-149">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="df613-149">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="df613-150">![Use external packages with Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="df613-150">![Use external packages with Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="df613-151">c.</span><span class="sxs-lookup"><span data-stu-id="df613-151">c.</span></span> <span data-ttu-id="df613-152">Concatenate the three values, separated by a colon (**:**).</span><span class="sxs-lookup"><span data-stu-id="df613-152">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="df613-153">Run the code cell with the `%%configure` magic.</span><span class="sxs-lookup"><span data-stu-id="df613-153">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="df613-154">This will configure the underlying Livy session to use the package you provided.</span><span class="sxs-lookup"><span data-stu-id="df613-154">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="df613-155">In the subsequent cells in the notebook, you can now use the package, as shown below.</span><span class="sxs-lookup"><span data-stu-id="df613-155">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="df613-156">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="df613-156">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a><span data-ttu-id="df613-157">See also</span><span class="sxs-lookup"><span data-stu-id="df613-157">See also</span></span>
* [<span data-ttu-id="df613-158">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-158">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="df613-159">Scenarios</span><span class="sxs-lookup"><span data-stu-id="df613-159">Scenarios</span></span>
* [<span data-ttu-id="df613-160">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="df613-160">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="df613-161">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="df613-161">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="df613-162">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="df613-162">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="df613-163">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="df613-163">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="df613-164">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-164">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="df613-165">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="df613-165">Create and run applications</span></span>
* [<span data-ttu-id="df613-166">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="df613-166">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="df613-167">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="df613-167">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="df613-168">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="df613-168">Tools and extensions</span></span>

* [<span data-ttu-id="df613-169">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="df613-169">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="df613-170">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="df613-170">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="df613-171">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="df613-171">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="df613-172">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-172">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="df613-173">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-173">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="df613-174">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="df613-174">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="df613-175">Manage resources</span><span class="sxs-lookup"><span data-stu-id="df613-175">Manage resources</span></span>
* [<span data-ttu-id="df613-176">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-176">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="df613-177">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="df613-177">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)




