---
title: Get started with Apache Spark cluster in Azure HDInsight | Microsoft Docs
description: Step-by-step instructions on how to quickly create an Apache Spark cluster in HDInsight and then use Spark SQL from Jupyter notebooks to run interactive queries.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/13/2017
ms.author: nitinme
ms.openlocfilehash: 7f35f63ffb275fb8d20785f1ceaeb6e7cbe29df9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563889"
---
# <a name="get-started-create-apache-spark-cluster-in-azure-hdinsight-and-run-interactive-queries-using-spark-sql"></a><span data-ttu-id="b2689-103">Get started: Create Apache Spark cluster in Azure HDInsight and run interactive queries using Spark SQL</span><span class="sxs-lookup"><span data-stu-id="b2689-103">Get started: Create Apache Spark cluster in Azure HDInsight and run interactive queries using Spark SQL</span></span>

<span data-ttu-id="b2689-104">Learn how to create an [Apache Spark](hdinsight-apache-spark-overview.md) cluster in HDInsight and then use [Jupyter](https://jupyter.org) notebook to run Spark SQL interactive queries on the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-104">Learn how to create an [Apache Spark](hdinsight-apache-spark-overview.md) cluster in HDInsight and then use [Jupyter](https://jupyter.org) notebook to run Spark SQL interactive queries on the Spark cluster.</span></span>

   <span data-ttu-id="b2689-105">![Get started using Apache Spark in HDInsight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.getstartedflow.png "Get started using Apache Spark in HDInsight tutorial. Steps illustrated: create a storage account; create a cluster; run Spark SQL statements")</span><span class="sxs-lookup"><span data-stu-id="b2689-105">![Get started using Apache Spark in HDInsight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.getstartedflow.png "Get started using Apache Spark in HDInsight tutorial. Steps illustrated: create a storage account; create a cluster; run Spark SQL statements")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2689-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b2689-106">Prerequisites</span></span>
* <span data-ttu-id="b2689-107">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="b2689-107">**An Azure subscription**.</span></span> <span data-ttu-id="b2689-108">Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b2689-108">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b2689-109">See [Create your free Azure account today](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b2689-109">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-a-spark-cluster"></a><span data-ttu-id="b2689-110">Create a Spark cluster</span><span class="sxs-lookup"><span data-stu-id="b2689-110">Create a Spark cluster</span></span>
<span data-ttu-id="b2689-111">In this section, you create a Spark cluster in HDInsight using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="b2689-111">In this section, you create a Spark cluster in HDInsight using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="b2689-112">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b2689-112">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="b2689-113">Click the following image to open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2689-113">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="b2689-114">Enter the following values:</span><span class="sxs-lookup"><span data-stu-id="b2689-114">Enter the following values:</span></span>

    <span data-ttu-id="b2689-115">![Create Spark cluster in HDInsight using an Azure Resource Manager template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span><span class="sxs-lookup"><span data-stu-id="b2689-115">![Create Spark cluster in HDInsight using an Azure Resource Manager template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="b2689-116">**Subscription**: Select your Azure subscription for this cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-116">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="b2689-117">**Resource group**: Create a resource group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="b2689-117">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="b2689-118">Resource group is used to manage Azure resources for your projects.</span><span class="sxs-lookup"><span data-stu-id="b2689-118">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="b2689-119">**Location**: Select a location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="b2689-119">**Location**: Select a location for the resource group.</span></span>  <span data-ttu-id="b2689-120">This location is also used for the default cluster storage and the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-120">This location is also used for the default cluster storage and the HDInsight cluster.</span></span>
    * <span data-ttu-id="b2689-121">**ClusterName**: Enter a name for the Hadoop cluster that you create.</span><span class="sxs-lookup"><span data-stu-id="b2689-121">**ClusterName**: Enter a name for the Hadoop cluster that you create.</span></span>
    * <span data-ttu-id="b2689-122">**Spark version**: Select the Spark version that you want to install on the cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-122">**Spark version**: Select the Spark version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="b2689-123">**Cluster login name and password**: The default login name is admin.</span><span class="sxs-lookup"><span data-stu-id="b2689-123">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="b2689-124">**SSH user name and password**.</span><span class="sxs-lookup"><span data-stu-id="b2689-124">**SSH user name and password**.</span></span>

   <span data-ttu-id="b2689-125">Write down these values.</span><span class="sxs-lookup"><span data-stu-id="b2689-125">Write down these values.</span></span>  <span data-ttu-id="b2689-126">You need them later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b2689-126">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="b2689-127">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="b2689-127">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="b2689-128">You can see a new tile titled Submitting deployment for Template deployment.</span><span class="sxs-lookup"><span data-stu-id="b2689-128">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="b2689-129">It takes about 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-129">It takes about 20 minutes to create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b2689-130">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b2689-130">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="b2689-131">You can also create a Spark cluster that uses [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) as additional storage, in addition to Azure Storage Blobs as the default storage.</span><span class="sxs-lookup"><span data-stu-id="b2689-131">You can also create a Spark cluster that uses [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) as additional storage, in addition to Azure Storage Blobs as the default storage.</span></span> <span data-ttu-id="b2689-132">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2689-132">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-spark-sql-query"></a><span data-ttu-id="b2689-133">Run a Spark SQL query</span><span class="sxs-lookup"><span data-stu-id="b2689-133">Run a Spark SQL query</span></span>

<span data-ttu-id="b2689-134">In this section, you use Jupyter notebook to run Spark SQL queries against the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-134">In this section, you use Jupyter notebook to run Spark SQL queries against the Spark cluster.</span></span> <span data-ttu-id="b2689-135">HDInsight Spark clusters provide three kernels that you can use with the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="b2689-135">HDInsight Spark clusters provide three kernels that you can use with the Jupyter notebook.</span></span> <span data-ttu-id="b2689-136">These are:</span><span class="sxs-lookup"><span data-stu-id="b2689-136">These are:</span></span>

* <span data-ttu-id="b2689-137">**PySpark** (for applications written in Python)</span><span class="sxs-lookup"><span data-stu-id="b2689-137">**PySpark** (for applications written in Python)</span></span>
* <span data-ttu-id="b2689-138">**PySpark3** (for applications written in Python3)</span><span class="sxs-lookup"><span data-stu-id="b2689-138">**PySpark3** (for applications written in Python3)</span></span>
* <span data-ttu-id="b2689-139">**Spark** (for applications written in Scala)</span><span class="sxs-lookup"><span data-stu-id="b2689-139">**Spark** (for applications written in Scala)</span></span>

<span data-ttu-id="b2689-140">In this article, you use the **PySpark** kernel.</span><span class="sxs-lookup"><span data-stu-id="b2689-140">In this article, you use the **PySpark** kernel.</span></span> <span data-ttu-id="b2689-141">For more information about the kernels, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b2689-141">For more information about the kernels, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span> <span data-ttu-id="b2689-142">Some of the key benefits of using the PySpark kernel are:</span><span class="sxs-lookup"><span data-stu-id="b2689-142">Some of the key benefits of using the PySpark kernel are:</span></span>

* <span data-ttu-id="b2689-143">The contexts for Spark and Hive are set automatically.</span><span class="sxs-lookup"><span data-stu-id="b2689-143">The contexts for Spark and Hive are set automatically.</span></span>
* <span data-ttu-id="b2689-144">Use cell magics, such as `%%sql`, to directly run SQL or Hive queries, without any preceding code snippets.</span><span class="sxs-lookup"><span data-stu-id="b2689-144">Use cell magics, such as `%%sql`, to directly run SQL or Hive queries, without any preceding code snippets.</span></span>
* <span data-ttu-id="b2689-145">The output for the SQL or Hive queries is automatically visualized.</span><span class="sxs-lookup"><span data-stu-id="b2689-145">The output for the SQL or Hive queries is automatically visualized.</span></span>

### <a name="create-jupyter-notebook-with-pyspark-kernel"></a><span data-ttu-id="b2689-146">Create Jupyter notebook with PySpark kernel</span><span class="sxs-lookup"><span data-stu-id="b2689-146">Create Jupyter notebook with PySpark kernel</span></span>

1. <span data-ttu-id="b2689-147">Open the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b2689-147">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="b2689-148">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span><span class="sxs-lookup"><span data-stu-id="b2689-148">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="b2689-149">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span><span class="sxs-lookup"><span data-stu-id="b2689-149">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="b2689-150">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="b2689-150">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="b2689-151">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b2689-151">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="b2689-152">![HDInsight cluster dashboards](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-azure-portal-cluster-dashboards.png "HDInsight cluster dashboards")</span><span class="sxs-lookup"><span data-stu-id="b2689-152">![HDInsight cluster dashboards](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-azure-portal-cluster-dashboards.png "HDInsight cluster dashboards")</span></span>

   > [!NOTE]
   > <span data-ttu-id="b2689-153">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="b2689-153">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="b2689-154">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="b2689-154">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="b2689-155">Create a notebook.</span><span class="sxs-lookup"><span data-stu-id="b2689-155">Create a notebook.</span></span> <span data-ttu-id="b2689-156">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b2689-156">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="b2689-157">![Create a Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.note.jupyter.createnotebook.png "Create a Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="b2689-157">![Create a Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.note.jupyter.createnotebook.png "Create a Jupyter notebook")</span></span>

   <span data-ttu-id="b2689-158">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="b2689-158">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="b2689-159">Click the notebook name at the top, and enter a friendly name if you want.</span><span class="sxs-lookup"><span data-stu-id="b2689-159">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="b2689-160">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="b2689-160">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="b2689-161">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to execute the code.</span><span class="sxs-lookup"><span data-stu-id="b2689-161">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to execute the code.</span></span> <span data-ttu-id="b2689-162">The code imports the types required for this scenario:</span><span class="sxs-lookup"><span data-stu-id="b2689-162">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="b2689-163">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="b2689-163">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="b2689-164">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="b2689-164">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="b2689-165">![Status of a Jupyter notebook job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.jupyter.job.status.png "Status of a Jupyter notebook job")</span><span class="sxs-lookup"><span data-stu-id="b2689-165">![Status of a Jupyter notebook job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/hdispark.jupyter.job.status.png "Status of a Jupyter notebook job")</span></span>

    <span data-ttu-id="b2689-166">Every time you run a job in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span><span class="sxs-lookup"><span data-stu-id="b2689-166">Every time you run a job in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="b2689-167">You also see a solid circle next to the **PySpark** text in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="b2689-167">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="b2689-168">After the job is completed, it changes to a hollow circle.</span><span class="sxs-lookup"><span data-stu-id="b2689-168">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="b2689-169">Register a sample data set as a temporary table (**hvac**) by running the following code.</span><span class="sxs-lookup"><span data-stu-id="b2689-169">Register a sample data set as a temporary table (**hvac**) by running the following code.</span></span>

        # Load the data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create the schema
        hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

        # Parse the data in hvacText
        hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

        # Create a data frame
        hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

        # Register the data fram as a table to run queries against
        hvacdf.registerTempTable("hvac")

    <span data-ttu-id="b2689-170">Spark clusters in HDInsight come with a sample data file, **hvac.csv**, under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="b2689-170">Spark clusters in HDInsight come with a sample data file, **hvac.csv**, under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

7. <span data-ttu-id="b2689-171">To query the data run the following code.</span><span class="sxs-lookup"><span data-stu-id="b2689-171">To query the data run the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="b2689-172">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span><span class="sxs-lookup"><span data-stu-id="b2689-172">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="b2689-173">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="b2689-173">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="b2689-174">The following tabular output is displayed by default.</span><span class="sxs-lookup"><span data-stu-id="b2689-174">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="b2689-175">![Table output of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/tabular.output.png "Table output of query result")</span><span class="sxs-lookup"><span data-stu-id="b2689-175">![Table output of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/tabular.output.png "Table output of query result")</span></span>

    <span data-ttu-id="b2689-176">You can also see the results in other visualizations as well.</span><span class="sxs-lookup"><span data-stu-id="b2689-176">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="b2689-177">For example, an area graph for the same output would look like the following.</span><span class="sxs-lookup"><span data-stu-id="b2689-177">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="b2689-178">![Area graph of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/area.output.png "Area graph of query result")</span><span class="sxs-lookup"><span data-stu-id="b2689-178">![Area graph of query result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-jupyter-spark-sql/area.output.png "Area graph of query result")</span></span>

9. <span data-ttu-id="b2689-179">Shut down the notebook to release the cluster resources after you have finished running the application.</span><span class="sxs-lookup"><span data-stu-id="b2689-179">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="b2689-180">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="b2689-180">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="b2689-181">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="b2689-181">Troubleshoot</span></span>

<span data-ttu-id="b2689-182">Here are some common issues that you might run into while working with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="b2689-182">Here are some common issues that you might run into while working with HDInsight clusters.</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="b2689-183">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="b2689-183">Access control requirements</span></span>
[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="delete-the-cluster"></a><span data-ttu-id="b2689-184">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="b2689-184">Delete the cluster</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="see-also"></a><span data-ttu-id="b2689-185">See also</span><span class="sxs-lookup"><span data-stu-id="b2689-185">See also</span></span>
* [<span data-ttu-id="b2689-186">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b2689-187">Scenarios</span><span class="sxs-lookup"><span data-stu-id="b2689-187">Scenarios</span></span>
* [<span data-ttu-id="b2689-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="b2689-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b2689-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="b2689-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b2689-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="b2689-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b2689-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="b2689-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b2689-192">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="b2689-193">Application Insight telemetry data analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-193">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b2689-194">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="b2689-194">Create and run applications</span></span>
* [<span data-ttu-id="b2689-195">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="b2689-195">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b2689-196">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="b2689-196">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b2689-197">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="b2689-197">Tools and extensions</span></span>
* [<span data-ttu-id="b2689-198">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="b2689-198">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b2689-199">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="b2689-199">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b2689-200">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-200">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="b2689-201">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-201">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b2689-202">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="b2689-202">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b2689-203">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="b2689-203">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b2689-204">Manage resources</span><span class="sxs-lookup"><span data-stu-id="b2689-204">Manage resources</span></span>
* [<span data-ttu-id="b2689-205">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-205">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b2689-206">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2689-206">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md









