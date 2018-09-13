---
title: Use custom Maven packages with Jupyter in Spark on Azure HDInsight
description: Step-by-step instructions on how to configure Jupyter notebooks available with HDInsight Spark clusters to use custom Maven packages.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/09/2018
ms.author: jasonh
ms.openlocfilehash: c6ef336e694bffec00ff239733fd7f07ba5fb09e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867078"
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="f0fd6-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [Using cell magic](apache-spark-jupyter-notebook-use-external-packages.md)
> * [Using Script Action](apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="f0fd6-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="f0fd6-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="f0fd6-108">You can also get a list of available packages from other sources.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="f0fd6-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="f0fd6-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="f0fd6-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0fd6-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f0fd6-111">Prerequisites</span></span>
<span data-ttu-id="f0fd6-112">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="f0fd6-112">You must have the following:</span></span>

* <span data-ttu-id="f0fd6-113">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f0fd6-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f0fd6-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="f0fd6-115">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="f0fd6-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="f0fd6-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="f0fd6-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="f0fd6-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

1. <span data-ttu-id="f0fd6-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="f0fd6-119">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser. Replace **CLUSTERNAME** with the name of your cluster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

1. <span data-ttu-id="f0fd6-122">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-122">Create a new notebook.</span></span> <span data-ttu-id="f0fd6-123">Click **New**, and then click **Spark**.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="f0fd6-124">![Create a new Jupyter notebook](./media/apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="f0fd6-124">![Create a new Jupyter notebook](./media/apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

1. <span data-ttu-id="f0fd6-125">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="f0fd6-126">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="f0fd6-127">![Provide a name for the notebook](./media/apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="f0fd6-127">![Provide a name for the notebook](./media/apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

1. <span data-ttu-id="f0fd6-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="f0fd6-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="f0fd6-130">This ensures that the kernel is configured to use the package before the session starts.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    >If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.

    | <span data-ttu-id="f0fd6-132">HDInsight version</span><span class="sxs-lookup"><span data-stu-id="f0fd6-132">HDInsight version</span></span> | <span data-ttu-id="f0fd6-133">Command</span><span class="sxs-lookup"><span data-stu-id="f0fd6-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="f0fd6-134">For HDInsight 3.3 and HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="f0fd6-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="f0fd6-135">For HDInsight 3.5 and HDInsight 3.6</span><span class="sxs-lookup"><span data-stu-id="f0fd6-135">For HDInsight 3.5 and HDInsight 3.6</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

1. <span data-ttu-id="f0fd6-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="f0fd6-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="f0fd6-138">Here's how you construct the coordinates for a package.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="f0fd6-139">a.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-139">a.</span></span> <span data-ttu-id="f0fd6-140">Locate the package in the Maven Repository.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="f0fd6-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="f0fd6-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="f0fd6-142">b.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-142">b.</span></span> <span data-ttu-id="f0fd6-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="f0fd6-144">Make sure that the values you gather match your cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="f0fd6-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="f0fd6-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="f0fd6-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="f0fd6-148">![Use external packages with Jupyter notebook](./media/apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="f0fd6-148">![Use external packages with Jupyter notebook](./media/apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="f0fd6-149">c.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-149">c.</span></span> <span data-ttu-id="f0fd6-150">Concatenate the three values, separated by a colon (**:**).</span><span class="sxs-lookup"><span data-stu-id="f0fd6-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

1. <span data-ttu-id="f0fd6-151">Run the code cell with the `%%configure` magic.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="f0fd6-152">This will configure the underlying Livy session to use the package you provided.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="f0fd6-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

    <span data-ttu-id="f0fd6-154">For HDInsight 3.6, you should use the following snippet.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-154">For HDInsight 3.6, you should use the following snippet.</span></span>

        val df = spark.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

1. <span data-ttu-id="f0fd6-155">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f0fd6-155">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a><span data-ttu-id="f0fd6-156">See also</span><span class="sxs-lookup"><span data-stu-id="f0fd6-156">See also</span></span>
* [<span data-ttu-id="f0fd6-157">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-157">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f0fd6-158">Scenarios</span><span class="sxs-lookup"><span data-stu-id="f0fd6-158">Scenarios</span></span>
* [<span data-ttu-id="f0fd6-159">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="f0fd6-159">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f0fd6-160">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="f0fd6-160">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f0fd6-161">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="f0fd6-161">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f0fd6-162">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-162">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f0fd6-163">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="f0fd6-163">Create and run applications</span></span>
* [<span data-ttu-id="f0fd6-164">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="f0fd6-164">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f0fd6-165">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="f0fd6-165">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f0fd6-166">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="f0fd6-166">Tools and extensions</span></span>

* [<span data-ttu-id="f0fd6-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="f0fd6-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](apache-spark-python-package-installation.md)
* [<span data-ttu-id="f0fd6-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="f0fd6-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f0fd6-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="f0fd6-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f0fd6-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f0fd6-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f0fd6-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="f0fd6-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f0fd6-173">Manage resources</span><span class="sxs-lookup"><span data-stu-id="f0fd6-173">Manage resources</span></span>
* [<span data-ttu-id="f0fd6-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="f0fd6-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0fd6-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)
