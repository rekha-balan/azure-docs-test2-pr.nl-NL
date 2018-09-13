---
title: Microsoft Cognitive Toolkit with Azure HDInsight Spark for deep learning
description: Learn how a trained Microsoft Cognitive Toolkit deep learning model can be applied to a dataset using the Spark Python API in an Azure HDInsight Spark cluster.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/28/2017
ms.author: jasonh
ms.openlocfilehash: cc36c68f4867b9b450703c881a13a65f17ebad4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870705"
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="5847a-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5847a-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="5847a-104">In this article, you do the following steps.</span><span class="sxs-lookup"><span data-stu-id="5847a-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="5847a-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="5847a-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="5847a-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="5847a-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5847a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5847a-107">Prerequisites</span></span>

* <span data-ttu-id="5847a-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="5847a-108">**An Azure subscription**.</span></span> <span data-ttu-id="5847a-109">Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5847a-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5847a-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="5847a-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="5847a-111">**Azure HDInsight Spark cluster**.</span><span class="sxs-lookup"><span data-stu-id="5847a-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="5847a-112">For this article, create a Spark 2.0 cluster.</span><span class="sxs-lookup"><span data-stu-id="5847a-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="5847a-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5847a-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="5847a-114">How does this solution flow?</span><span class="sxs-lookup"><span data-stu-id="5847a-114">How does this solution flow?</span></span>

<span data-ttu-id="5847a-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5847a-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="5847a-116">In this article, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="5847a-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="5847a-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span><span class="sxs-lookup"><span data-stu-id="5847a-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="5847a-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="5847a-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="5847a-119">The following remaining steps are covered in the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="5847a-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="5847a-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span><span class="sxs-lookup"><span data-stu-id="5847a-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="5847a-121">Load modules and define presets</span><span class="sxs-lookup"><span data-stu-id="5847a-121">Load modules and define presets</span></span>
   - <span data-ttu-id="5847a-122">Download the dataset locally on the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5847a-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="5847a-123">Convert the dataset into an RDD</span><span class="sxs-lookup"><span data-stu-id="5847a-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="5847a-124">Score the images using a trained Cognitive Toolkit model</span><span class="sxs-lookup"><span data-stu-id="5847a-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="5847a-125">Download the trained Cognitive Toolkit model to the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5847a-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="5847a-126">Define functions to be used by worker nodes</span><span class="sxs-lookup"><span data-stu-id="5847a-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="5847a-127">Score the images on worker nodes</span><span class="sxs-lookup"><span data-stu-id="5847a-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="5847a-128">Evaluate model accuracy</span><span class="sxs-lookup"><span data-stu-id="5847a-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="5847a-129">Install Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="5847a-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="5847a-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span><span class="sxs-lookup"><span data-stu-id="5847a-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="5847a-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span><span class="sxs-lookup"><span data-stu-id="5847a-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="5847a-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5847a-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="5847a-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span><span class="sxs-lookup"><span data-stu-id="5847a-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="5847a-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="5847a-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="5847a-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](../hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5847a-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](../hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="5847a-136">Using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5847a-136">Using the Azure Portal</span></span>

<span data-ttu-id="5847a-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](../hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="5847a-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](../hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="5847a-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="5847a-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="5847a-139">Provide a value for the script action name.</span><span class="sxs-lookup"><span data-stu-id="5847a-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="5847a-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="5847a-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="5847a-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span><span class="sxs-lookup"><span data-stu-id="5847a-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="5847a-142">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5847a-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="5847a-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5847a-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="5847a-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="5847a-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="5847a-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="5847a-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="5847a-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="5847a-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="5847a-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="5847a-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="5847a-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span><span class="sxs-lookup"><span data-stu-id="5847a-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="5847a-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="5847a-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="5847a-150">Replace \<clustername> with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5847a-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="5847a-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="5847a-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="5847a-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span><span class="sxs-lookup"><span data-stu-id="5847a-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="5847a-153">Click **Upload** again.</span><span class="sxs-lookup"><span data-stu-id="5847a-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="5847a-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5847a-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="5847a-155">See also</span><span class="sxs-lookup"><span data-stu-id="5847a-155">See also</span></span>
* [<span data-ttu-id="5847a-156">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-156">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="5847a-157">Scenarios</span><span class="sxs-lookup"><span data-stu-id="5847a-157">Scenarios</span></span>
* [<span data-ttu-id="5847a-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="5847a-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5847a-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="5847a-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5847a-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="5847a-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5847a-161">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-161">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="5847a-162">Application Insight telemetry data analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-162">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](apache-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5847a-163">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="5847a-163">Create and run applications</span></span>
* [<span data-ttu-id="5847a-164">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="5847a-164">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5847a-165">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="5847a-165">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5847a-166">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="5847a-166">Tools and extensions</span></span>
* [<span data-ttu-id="5847a-167">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="5847a-167">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5847a-168">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="5847a-168">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5847a-169">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-169">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5847a-170">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-170">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5847a-171">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="5847a-171">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5847a-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5847a-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5847a-173">Manage resources</span><span class="sxs-lookup"><span data-stu-id="5847a-173">Manage resources</span></span>
* [<span data-ttu-id="5847a-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="5847a-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5847a-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../../storage/common/storage-create-storage-account.md
