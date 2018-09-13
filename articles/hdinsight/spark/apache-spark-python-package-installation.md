---
title: Script action - Install Python packages with Jupyter on Azure HDInsight
description: Step-by-step instructions on how to use script action to configure Jupyter notebooks available with HDInsight Spark clusters to use external python packages.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/09/2018
ms.author: jasonh
ms.openlocfilehash: c8d0b172682654c858a97b4ca2df99ec5079adaa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856416"
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="4ae21-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [Using cell magic](apache-spark-jupyter-notebook-use-external-packages.md)
> * [Using Script Action](apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="4ae21-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4ae21-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> You can also configure a Jupyter notebook by using `%%configure` magic to use external packages. For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

<span data-ttu-id="4ae21-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span><span class="sxs-lookup"><span data-stu-id="4ae21-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="4ae21-110">You can also get a list of available packages from other sources.</span><span class="sxs-lookup"><span data-stu-id="4ae21-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="4ae21-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.org/feedstocks/).</span><span class="sxs-lookup"><span data-stu-id="4ae21-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.org/feedstocks/).</span></span>

<span data-ttu-id="4ae21-112">In this article, you learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Action on your cluster and use it via the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="4ae21-112">In this article, you learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Action on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ae21-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ae21-113">Prerequisites</span></span>
<span data-ttu-id="4ae21-114">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="4ae21-114">You must have the following:</span></span>

* <span data-ttu-id="4ae21-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4ae21-115">An Azure subscription.</span></span> <span data-ttu-id="4ae21-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4ae21-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4ae21-117">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ae21-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4ae21-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4ae21-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation. Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="4ae21-121">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="4ae21-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="4ae21-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="4ae21-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="4ae21-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="4ae21-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="4ae21-124">From the Spark cluster blade, click **Script Actions** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="4ae21-124">From the Spark cluster blade, click **Script Actions** from the left pane.</span></span> <span data-ttu-id="4ae21-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="4ae21-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="4ae21-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="4ae21-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > There are two python installations in the cluster. Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`. Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. <span data-ttu-id="4ae21-130">Open a PySpark Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="4ae21-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="4ae21-131">![Create a new Jupyter notebook](./media/apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="4ae21-131">![Create a new Jupyter notebook](./media/apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="4ae21-132">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="4ae21-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="4ae21-133">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="4ae21-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="4ae21-134">![Provide a name for the notebook](./media/apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="4ae21-134">![Provide a name for the notebook](./media/apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="4ae21-135">You will now `import tensorflow` and run a hello world example.</span><span class="sxs-lookup"><span data-stu-id="4ae21-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="4ae21-136">Code to copy:</span><span class="sxs-lookup"><span data-stu-id="4ae21-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="4ae21-137">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="4ae21-137">The result looks like this:</span></span>
    
    <span data-ttu-id="4ae21-138">![TensorFlow code execution](./media/apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span><span class="sxs-lookup"><span data-stu-id="4ae21-138">![TensorFlow code execution](./media/apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>

## <a name="seealso"></a><span data-ttu-id="4ae21-139">See also</span><span class="sxs-lookup"><span data-stu-id="4ae21-139">See also</span></span>
* [<span data-ttu-id="4ae21-140">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-140">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4ae21-141">Scenarios</span><span class="sxs-lookup"><span data-stu-id="4ae21-141">Scenarios</span></span>
* [<span data-ttu-id="4ae21-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="4ae21-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4ae21-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="4ae21-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4ae21-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="4ae21-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4ae21-145">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-145">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4ae21-146">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="4ae21-146">Create and run applications</span></span>
* [<span data-ttu-id="4ae21-147">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="4ae21-147">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4ae21-148">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="4ae21-148">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4ae21-149">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="4ae21-149">Tools and extensions</span></span>
* [<span data-ttu-id="4ae21-150">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-150">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4ae21-151">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="4ae21-151">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4ae21-152">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="4ae21-152">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4ae21-153">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-153">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4ae21-154">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-154">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4ae21-155">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="4ae21-155">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4ae21-156">Manage resources</span><span class="sxs-lookup"><span data-stu-id="4ae21-156">Manage resources</span></span>
* [<span data-ttu-id="4ae21-157">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-157">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="4ae21-158">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae21-158">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)
