---
title: Microsoft Cognitive Toolkit with Azure HDInsight Spark for deep learning | Microsoft Docs
description: Learn how a trained Microsoft Cognitive Toolkit deep learning model can be applied to a dataset using the Spark Python API in an Azure HDInsight Spark cluster.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: nitinme
ms.openlocfilehash: 92e62bf530038a983fd1d92327843b9dcffb6af5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669666"
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="98ae9-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="98ae9-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="98ae9-104">In this article, you do the following steps.</span><span class="sxs-lookup"><span data-stu-id="98ae9-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="98ae9-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="98ae9-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="98ae9-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="98ae9-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98ae9-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="98ae9-107">Prerequisites</span></span>

* <span data-ttu-id="98ae9-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="98ae9-108">**An Azure subscription**.</span></span> <span data-ttu-id="98ae9-109">Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="98ae9-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="98ae9-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="98ae9-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="98ae9-111">**Azure HDInsight Spark cluster**.</span><span class="sxs-lookup"><span data-stu-id="98ae9-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="98ae9-112">For this article, create a Spark 2.0 cluster.</span><span class="sxs-lookup"><span data-stu-id="98ae9-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="98ae9-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="98ae9-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="98ae9-114">How does this solution flow?</span><span class="sxs-lookup"><span data-stu-id="98ae9-114">How does this solution flow?</span></span>

<span data-ttu-id="98ae9-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="98ae9-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="98ae9-116">In this article, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="98ae9-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="98ae9-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span><span class="sxs-lookup"><span data-stu-id="98ae9-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="98ae9-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="98ae9-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="98ae9-119">The following remaining steps are covered in the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="98ae9-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="98ae9-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span><span class="sxs-lookup"><span data-stu-id="98ae9-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="98ae9-121">Load modules and define presets</span><span class="sxs-lookup"><span data-stu-id="98ae9-121">Load modules and define presets</span></span>
   - <span data-ttu-id="98ae9-122">Download the dataset locally on the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="98ae9-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="98ae9-123">Convert the dataset into an RDD</span><span class="sxs-lookup"><span data-stu-id="98ae9-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="98ae9-124">Score the images using a trained Cognitive Toolkit model</span><span class="sxs-lookup"><span data-stu-id="98ae9-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="98ae9-125">Download the trained Cognitive Toolkit model to the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="98ae9-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="98ae9-126">Define functions to be used by worker nodes</span><span class="sxs-lookup"><span data-stu-id="98ae9-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="98ae9-127">Score the images on worker nodes</span><span class="sxs-lookup"><span data-stu-id="98ae9-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="98ae9-128">Evaluate model accuracy</span><span class="sxs-lookup"><span data-stu-id="98ae9-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="98ae9-129">Install Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="98ae9-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="98ae9-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span><span class="sxs-lookup"><span data-stu-id="98ae9-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="98ae9-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span><span class="sxs-lookup"><span data-stu-id="98ae9-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="98ae9-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98ae9-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="98ae9-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span><span class="sxs-lookup"><span data-stu-id="98ae9-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="98ae9-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="98ae9-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="98ae9-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="98ae9-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="98ae9-136">Using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="98ae9-136">Using the Azure Portal</span></span>

<span data-ttu-id="98ae9-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="98ae9-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="98ae9-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span><span class="sxs-lookup"><span data-stu-id="98ae9-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="98ae9-139">Provide a value for the script action name.</span><span class="sxs-lookup"><span data-stu-id="98ae9-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="98ae9-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="98ae9-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="98ae9-141">Make sure you run the script only on the headnode.</span><span class="sxs-lookup"><span data-stu-id="98ae9-141">Make sure you run the script only on the headnode.</span></span> <span data-ttu-id="98ae9-142">Clear the checkboxes for Worker node and Zookeeper node.</span><span class="sxs-lookup"><span data-stu-id="98ae9-142">Clear the checkboxes for Worker node and Zookeeper node.</span></span>

* <span data-ttu-id="98ae9-143">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="98ae9-143">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="98ae9-144">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="98ae9-144">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="98ae9-145">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="98ae9-145">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="98ae9-146">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="98ae9-146">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="98ae9-147">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="98ae9-147">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="98ae9-148">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="98ae9-148">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="98ae9-149">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span><span class="sxs-lookup"><span data-stu-id="98ae9-149">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="98ae9-150">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="98ae9-150">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="98ae9-151">Replace \<clustername> with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="98ae9-151">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="98ae9-152">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="98ae9-152">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="98ae9-153">![Upload Jupyter notebook to Azure HDInsight Spark cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-microsoft-cognitive-toolkit.md/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span><span class="sxs-lookup"><span data-stu-id="98ae9-153">![Upload Jupyter notebook to Azure HDInsight Spark cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-microsoft-cognitive-toolkit.md/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="98ae9-154">Click **Upload** again.</span><span class="sxs-lookup"><span data-stu-id="98ae9-154">Click **Upload** again.</span></span>

5. <span data-ttu-id="98ae9-155">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span><span class="sxs-lookup"><span data-stu-id="98ae9-155">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="98ae9-156">See also</span><span class="sxs-lookup"><span data-stu-id="98ae9-156">See also</span></span>
* [<span data-ttu-id="98ae9-157">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-157">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="98ae9-158">Scenarios</span><span class="sxs-lookup"><span data-stu-id="98ae9-158">Scenarios</span></span>
* [<span data-ttu-id="98ae9-159">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="98ae9-159">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="98ae9-160">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="98ae9-160">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="98ae9-161">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="98ae9-161">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="98ae9-162">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="98ae9-162">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="98ae9-163">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-163">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="98ae9-164">Application Insight telemetry data analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-164">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="98ae9-165">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="98ae9-165">Create and run applications</span></span>
* [<span data-ttu-id="98ae9-166">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="98ae9-166">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="98ae9-167">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="98ae9-167">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="98ae9-168">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="98ae9-168">Tools and extensions</span></span>
* [<span data-ttu-id="98ae9-169">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="98ae9-169">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="98ae9-170">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="98ae9-170">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="98ae9-171">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-171">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="98ae9-172">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-172">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="98ae9-173">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="98ae9-173">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="98ae9-174">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="98ae9-174">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="98ae9-175">Manage resources</span><span class="sxs-lookup"><span data-stu-id="98ae9-175">Manage resources</span></span>
* [<span data-ttu-id="98ae9-176">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-176">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="98ae9-177">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="98ae9-177">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md

