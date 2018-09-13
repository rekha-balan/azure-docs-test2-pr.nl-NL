---
title: 'Tutorial: Apache Spark Structured Streaming with Kafka - Azure HDInsight '
description: Learn how to use Apache Spark streaming to get data into or out of Apache Kafka. In this tutorial, you stream data using a Jupyter notebook from Spark on HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: tutorial
ms.date: 05/08/2018
ms.author: jasonh
ms.openlocfilehash: bd79b7f1f458f9ad4b490795a7ded9d8bfb79627
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855854"
---
# <a name="tutorial-use-spark-structured-streaming-with-kafka-on-hdinsight"></a><span data-ttu-id="1f758-104">Tutorial: Use Spark Structured Streaming with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f758-104">Tutorial: Use Spark Structured Streaming with Kafka on HDInsight</span></span>

<span data-ttu-id="1f758-105">This tutorial demonstrates how to use Spark Structured Streaming to read and write data with Apache Kafka on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f758-105">This tutorial demonstrates how to use Spark Structured Streaming to read and write data with Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="1f758-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="1f758-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="1f758-107">It allows you to express streaming computations the same as batch computation on static data.</span><span class="sxs-lookup"><span data-stu-id="1f758-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> 

<span data-ttu-id="1f758-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="1f758-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f758-109">Structured Streaming with Kafka</span><span class="sxs-lookup"><span data-stu-id="1f758-109">Structured Streaming with Kafka</span></span>
> * <span data-ttu-id="1f758-110">Create Kafka and Spark clusters</span><span class="sxs-lookup"><span data-stu-id="1f758-110">Create Kafka and Spark clusters</span></span>
> * <span data-ttu-id="1f758-111">Upload the notebook to Spark</span><span class="sxs-lookup"><span data-stu-id="1f758-111">Upload the notebook to Spark</span></span>
> * <span data-ttu-id="1f758-112">Use the notebook</span><span class="sxs-lookup"><span data-stu-id="1f758-112">Use the notebook</span></span>
> * <span data-ttu-id="1f758-113">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1f758-113">Clean up resources</span></span>

<span data-ttu-id="1f758-114">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span><span class="sxs-lookup"><span data-stu-id="1f758-114">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f758-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f758-115">Prerequisites</span></span>

* <span data-ttu-id="1f758-116">Familiarity with using Jupyter Notebooks with Spark on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f758-116">Familiarity with using Jupyter Notebooks with Spark on HDInsight.</span></span> <span data-ttu-id="1f758-117">For more information, see the [Load data and run queries with Spark on HDInsight](spark/apache-spark-load-data-run-query.md) document.</span><span class="sxs-lookup"><span data-stu-id="1f758-117">For more information, see the [Load data and run queries with Spark on HDInsight](spark/apache-spark-load-data-run-query.md) document.</span></span>

* <span data-ttu-id="1f758-118">Familiarity with the [Scala](https://www.scala-lang.org/) programming language.</span><span class="sxs-lookup"><span data-stu-id="1f758-118">Familiarity with the [Scala](https://www.scala-lang.org/) programming language.</span></span> <span data-ttu-id="1f758-119">The code used in this tutorial is written in Scala.</span><span class="sxs-lookup"><span data-stu-id="1f758-119">The code used in this tutorial is written in Scala.</span></span>

* <span data-ttu-id="1f758-120">Familiarity with creating Kafka topics.</span><span class="sxs-lookup"><span data-stu-id="1f758-120">Familiarity with creating Kafka topics.</span></span> <span data-ttu-id="1f758-121">For more information, see the [Kafka on HDInsight quickstart](kafka/apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="1f758-121">For more information, see the [Kafka on HDInsight quickstart](kafka/apache-kafka-get-started.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f758-122">The steps in this document require an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-122">The steps in this document require an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="1f758-123">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-123">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="1f758-124">For your convenience, this document links to a template that can create all the required Azure resources.</span><span class="sxs-lookup"><span data-stu-id="1f758-124">For your convenience, this document links to a template that can create all the required Azure resources.</span></span> 
>
> <span data-ttu-id="1f758-125">For more information on using HDInsight in a virtual network, see the [Extend HDInsight using a virtual network](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="1f758-125">For more information on using HDInsight in a virtual network, see the [Extend HDInsight using a virtual network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="structured-streaming-with-kafka"></a><span data-ttu-id="1f758-126">Structured Streaming with Kafka</span><span class="sxs-lookup"><span data-stu-id="1f758-126">Structured Streaming with Kafka</span></span>

<span data-ttu-id="1f758-127">Spark Structured Streaming is a stream processing engine built on the Spark SQL engine.</span><span class="sxs-lookup"><span data-stu-id="1f758-127">Spark Structured Streaming is a stream processing engine built on the Spark SQL engine.</span></span> <span data-ttu-id="1f758-128">When using Structured Streaming, you can write streaming queries the same way that you write batch queries.</span><span class="sxs-lookup"><span data-stu-id="1f758-128">When using Structured Streaming, you can write streaming queries the same way that you write batch queries.</span></span>

<span data-ttu-id="1f758-129">The following code snippets demonstrate reading from Kafka and storing to file.</span><span class="sxs-lookup"><span data-stu-id="1f758-129">The following code snippets demonstrate reading from Kafka and storing to file.</span></span> <span data-ttu-id="1f758-130">The first one is a batch operation, while the second one is a streaming operation:</span><span class="sxs-lookup"><span data-stu-id="1f758-130">The first one is a batch operation, while the second one is a streaming operation:</span></span>

```scala
// Read a batch from Kafka
val kafkaDF = spark.read.format("kafka")
                .option("kafka.bootstrap.servers", kafkaBrokers)
                .option("subscribe", kafkaTopic)
                .option("startingOffsets", "earliest")
                .load()
// Select data and write to file
kafkaDF.select(from_json(col("value").cast("string"), schema) as "trip")
                .write
                .format("parquet")
                .option("path","/example/batchtripdata")
                .option("checkpointLocation", "/batchcheckpoint")
                .save()
```

```scala
// Stream from Kafka
val kafkaStreamDF = spark.readStream.format("kafka")
                .option("kafka.bootstrap.servers", kafkaBrokers)
                .option("subscribe", kafkaTopic)
                .option("startingOffsets", "earliest")
                .load()
// Select data from the stream and write to file
kafkaStreamDF.select(from_json(col("value").cast("string"), schema) as "trip")
                .writeStream
                .format("parquet")
                .option("path","/example/streamingtripdata")
                .option("checkpointLocation", "/streamcheckpoint")
                .start.awaitTermination(30000)
```

<span data-ttu-id="1f758-131">In both snippets, data is read from Kafka and written to file.</span><span class="sxs-lookup"><span data-stu-id="1f758-131">In both snippets, data is read from Kafka and written to file.</span></span> <span data-ttu-id="1f758-132">The differences between the examples are:</span><span class="sxs-lookup"><span data-stu-id="1f758-132">The differences between the examples are:</span></span>

| <span data-ttu-id="1f758-133">Batch</span><span class="sxs-lookup"><span data-stu-id="1f758-133">Batch</span></span> | <span data-ttu-id="1f758-134">Streaming</span><span class="sxs-lookup"><span data-stu-id="1f758-134">Streaming</span></span> |
| --- | --- |
| `read` | `readStream` |
| `write` | `writeStream` |
| `save` | `start` |

<span data-ttu-id="1f758-135">The streaming operation also uses `awaitTermination(30000)`, which stops the stream after 30000 ms.</span><span class="sxs-lookup"><span data-stu-id="1f758-135">The streaming operation also uses `awaitTermination(30000)`, which stops the stream after 30000 ms.</span></span> 

<span data-ttu-id="1f758-136">To use Structured Streaming with Kafka, your project must have a dependency on the `org.apache.spark : spark-sql-kafka-0-10_2.11` package.</span><span class="sxs-lookup"><span data-stu-id="1f758-136">To use Structured Streaming with Kafka, your project must have a dependency on the `org.apache.spark : spark-sql-kafka-0-10_2.11` package.</span></span> <span data-ttu-id="1f758-137">The version of this package should match the version of Spark on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f758-137">The version of this package should match the version of Spark on HDInsight.</span></span> <span data-ttu-id="1f758-138">For Spark 2.2.0 (available in HDInsight 3.6), you can find the dependency information for different project types at [https://search.maven.org/#artifactdetails%7Corg.apache.spark%7Cspark-sql-kafka-0-10_2.11%7C2.2.0%7Cjar](https://search.maven.org/#artifactdetails%7Corg.apache.spark%7Cspark-sql-kafka-0-10_2.11%7C2.2.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="1f758-138">For Spark 2.2.0 (available in HDInsight 3.6), you can find the dependency information for different project types at [https://search.maven.org/#artifactdetails%7Corg.apache.spark%7Cspark-sql-kafka-0-10_2.11%7C2.2.0%7Cjar](https://search.maven.org/#artifactdetails%7Corg.apache.spark%7Cspark-sql-kafka-0-10_2.11%7C2.2.0%7Cjar).</span></span>

<span data-ttu-id="1f758-139">For the Jupyter Notebook provided with this tutorial, the following cell loads this package dependency:</span><span class="sxs-lookup"><span data-stu-id="1f758-139">For the Jupyter Notebook provided with this tutorial, the following cell loads this package dependency:</span></span>

```
%%configure -f
{
    "conf": {
        "spark.jars.packages": "org.apache.spark:spark-sql-kafka-0-10_2.11:2.2.0",
        "spark.jars.excludes": "org.scala-lang:scala-reflect,org.apache.spark:spark-tags_2.11"
    }
}
```

## <a name="create-the-clusters"></a><span data-ttu-id="1f758-140">Create the clusters</span><span class="sxs-lookup"><span data-stu-id="1f758-140">Create the clusters</span></span>

<span data-ttu-id="1f758-141">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span><span class="sxs-lookup"><span data-stu-id="1f758-141">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="1f758-142">Anything that uses Kafka must be in the same Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="1f758-142">Anything that uses Kafka must be in the same Azure virtual network.</span></span> <span data-ttu-id="1f758-143">In this tutorial, both the Kafka and Spark clusters are located in the same Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="1f758-143">In this tutorial, both the Kafka and Spark clusters are located in the same Azure virtual network.</span></span> 

<span data-ttu-id="1f758-144">The following diagram shows how communication flows between Spark and Kafka:</span><span class="sxs-lookup"><span data-stu-id="1f758-144">The following diagram shows how communication flows between Spark and Kafka:</span></span>

![Diagram of Spark and Kafka clusters in an Azure virtual network](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="1f758-146">The Kafka service is limited to communication within the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1f758-146">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="1f758-147">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="1f758-147">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="1f758-148">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="1f758-148">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="1f758-149">To create an Azure Virtual Network, and then create the Kafka and Spark clusters within it, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f758-149">To create an Azure Virtual Network, and then create the Kafka and Spark clusters within it, use the following steps:</span></span>

1. <span data-ttu-id="1f758-150">Use the following button to sign in to Azure and open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f758-150">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fhdinsight-spark-kafka-structured-streaming%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="1f758-151">The Azure Resource Manager template is located at **https://raw.githubusercontent.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming/master/azuredeploy.json**.</span><span class="sxs-lookup"><span data-stu-id="1f758-151">The Azure Resource Manager template is located at **https://raw.githubusercontent.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming/master/azuredeploy.json**.</span></span>

    <span data-ttu-id="1f758-152">This template creates the following resources:</span><span class="sxs-lookup"><span data-stu-id="1f758-152">This template creates the following resources:</span></span>

    * <span data-ttu-id="1f758-153">A Kafka on HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-153">A Kafka on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="1f758-154">A Spark 2.2.0 on HDInsight 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-154">A Spark 2.2.0 on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="1f758-155">An Azure Virtual Network, which contains the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="1f758-155">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1f758-156">The structured streaming notebook used in this tutorial requires Spark 2.2.0 on HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="1f758-156">The structured streaming notebook used in this tutorial requires Spark 2.2.0 on HDInsight 3.6.</span></span> <span data-ttu-id="1f758-157">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span><span class="sxs-lookup"><span data-stu-id="1f758-157">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="1f758-158">Use the following information to populate the entries on the **Customized template** section:</span><span class="sxs-lookup"><span data-stu-id="1f758-158">Use the following information to populate the entries on the **Customized template** section:</span></span>

    | <span data-ttu-id="1f758-159">Setting</span><span class="sxs-lookup"><span data-stu-id="1f758-159">Setting</span></span> | <span data-ttu-id="1f758-160">Value</span><span class="sxs-lookup"><span data-stu-id="1f758-160">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1f758-161">Subscription</span><span class="sxs-lookup"><span data-stu-id="1f758-161">Subscription</span></span> | <span data-ttu-id="1f758-162">Your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="1f758-162">Your Azure subscription</span></span> |
    | <span data-ttu-id="1f758-163">Resource group</span><span class="sxs-lookup"><span data-stu-id="1f758-163">Resource group</span></span> | <span data-ttu-id="1f758-164">The resource group that contains the resources.</span><span class="sxs-lookup"><span data-stu-id="1f758-164">The resource group that contains the resources.</span></span> |
    | <span data-ttu-id="1f758-165">Location</span><span class="sxs-lookup"><span data-stu-id="1f758-165">Location</span></span> | <span data-ttu-id="1f758-166">The Azure region that the resources are created in.</span><span class="sxs-lookup"><span data-stu-id="1f758-166">The Azure region that the resources are created in.</span></span> |
    | <span data-ttu-id="1f758-167">Spark Cluster Name</span><span class="sxs-lookup"><span data-stu-id="1f758-167">Spark Cluster Name</span></span> | <span data-ttu-id="1f758-168">The name of the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-168">The name of the Spark cluster.</span></span> <span data-ttu-id="1f758-169">The first six characters must be different than the Kafka cluster name.</span><span class="sxs-lookup"><span data-stu-id="1f758-169">The first six characters must be different than the Kafka cluster name.</span></span> |
    | <span data-ttu-id="1f758-170">Kafka Cluster Name</span><span class="sxs-lookup"><span data-stu-id="1f758-170">Kafka Cluster Name</span></span> | <span data-ttu-id="1f758-171">The name of the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-171">The name of the Kafka cluster.</span></span> <span data-ttu-id="1f758-172">The first six characters must be different than the Spark cluster name.</span><span class="sxs-lookup"><span data-stu-id="1f758-172">The first six characters must be different than the Spark cluster name.</span></span> |
    | <span data-ttu-id="1f758-173">Cluster Login User Name</span><span class="sxs-lookup"><span data-stu-id="1f758-173">Cluster Login User Name</span></span> | <span data-ttu-id="1f758-174">The admin user name for the clusters.</span><span class="sxs-lookup"><span data-stu-id="1f758-174">The admin user name for the clusters.</span></span> |
    | <span data-ttu-id="1f758-175">Cluster Login Password</span><span class="sxs-lookup"><span data-stu-id="1f758-175">Cluster Login Password</span></span> | <span data-ttu-id="1f758-176">The admin user password for the clusters.</span><span class="sxs-lookup"><span data-stu-id="1f758-176">The admin user password for the clusters.</span></span> |
    | <span data-ttu-id="1f758-177">SSH User Name</span><span class="sxs-lookup"><span data-stu-id="1f758-177">SSH User Name</span></span> | <span data-ttu-id="1f758-178">The SSH user to create for the clusters.</span><span class="sxs-lookup"><span data-stu-id="1f758-178">The SSH user to create for the clusters.</span></span> |
    | <span data-ttu-id="1f758-179">SSH Password</span><span class="sxs-lookup"><span data-stu-id="1f758-179">SSH Password</span></span> | <span data-ttu-id="1f758-180">The password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="1f758-180">The password for the SSH user.</span></span> |
   
    ![Screenshot of the customized template](./media/hdinsight-apache-kafka-spark-structured-streaming/spark-kafka-template.png)

3. <span data-ttu-id="1f758-182">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**</span><span class="sxs-lookup"><span data-stu-id="1f758-182">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**</span></span>

4. <span data-ttu-id="1f758-183">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="1f758-183">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f758-184">It can take up to 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="1f758-184">It can take up to 20 minutes to create the clusters.</span></span>

## <a name="upload-the-notebook"></a><span data-ttu-id="1f758-185">Upload the notebook</span><span class="sxs-lookup"><span data-stu-id="1f758-185">Upload the notebook</span></span>

<span data-ttu-id="1f758-186">To upload the notebook from the project to your Spark on HDInsight cluster, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="1f758-186">To upload the notebook from the project to your Spark on HDInsight cluster, use the following steps:</span></span>

1. <span data-ttu-id="1f758-187">Download the project from [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="1f758-187">Download the project from [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

1. <span data-ttu-id="1f758-188">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-188">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="1f758-189">In the following URL, replace `CLUSTERNAME` with the name of your __Spark__ cluster:</span><span class="sxs-lookup"><span data-stu-id="1f758-189">In the following URL, replace `CLUSTERNAME` with the name of your __Spark__ cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="1f758-190">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-190">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="1f758-191">From the upper right side of the page, use the __Upload__ button to upload the __spark-structured-streaming-kafka.ipynb__ file to the cluster.</span><span class="sxs-lookup"><span data-stu-id="1f758-191">From the upper right side of the page, use the __Upload__ button to upload the __spark-structured-streaming-kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="1f758-192">Select __Open__ to start the upload.</span><span class="sxs-lookup"><span data-stu-id="1f758-192">Select __Open__ to start the upload.</span></span>

    ![Use the upload button to select and upload a notebook](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Select the KafkaStreaming.ipynb file](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="1f758-195">Find the __spark-structured-streaming-kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span><span class="sxs-lookup"><span data-stu-id="1f758-195">Find the __spark-structured-streaming-kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![To upload the notebook, use the upload button for the KafkaStreaming.ipynb entry](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)


## <a name="use-the-notebook"></a><span data-ttu-id="1f758-197">Use the notebook</span><span class="sxs-lookup"><span data-stu-id="1f758-197">Use the notebook</span></span>

<span data-ttu-id="1f758-198">Once the files have been uploaded, select the __spark-structured-streaming-kafka.ipynb__ entry to open the notebook.</span><span class="sxs-lookup"><span data-stu-id="1f758-198">Once the files have been uploaded, select the __spark-structured-streaming-kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="1f758-199">To learn how to use Spark structured streaming with Kafka on HDInsight, follow the instructions in the notebook.</span><span class="sxs-lookup"><span data-stu-id="1f758-199">To learn how to use Spark structured streaming with Kafka on HDInsight, follow the instructions in the notebook.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="1f758-200">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1f758-200">Clean up resources</span></span>

<span data-ttu-id="1f758-201">To clean up the resources created by this tutorial, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="1f758-201">To clean up the resources created by this tutorial, you can delete the resource group.</span></span> <span data-ttu-id="1f758-202">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span><span class="sxs-lookup"><span data-stu-id="1f758-202">Deleting the resource group also deletes the associated HDInsight cluster, and any other resources associated with the resource group.</span></span>

<span data-ttu-id="1f758-203">To remove the resource group using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="1f758-203">To remove the resource group using the Azure portal:</span></span>

1. <span data-ttu-id="1f758-204">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span><span class="sxs-lookup"><span data-stu-id="1f758-204">In the Azure portal, expand the menu on the left side to open the menu of services, and then choose __Resource Groups__ to display the list of your resource groups.</span></span>
2. <span data-ttu-id="1f758-205">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span><span class="sxs-lookup"><span data-stu-id="1f758-205">Locate the resource group to delete, and then right-click the __More__ button (...) on the right side of the listing.</span></span>
3. <span data-ttu-id="1f758-206">Select __Delete resource group__, and then confirm.</span><span class="sxs-lookup"><span data-stu-id="1f758-206">Select __Delete resource group__, and then confirm.</span></span>

> [!WARNING]
> <span data-ttu-id="1f758-207">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="1f758-207">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="1f758-208">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span><span class="sxs-lookup"><span data-stu-id="1f758-208">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span>
> 
> <span data-ttu-id="1f758-209">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="1f758-209">Deleting a Kafka on HDInsight cluster deletes any data stored in Kafka.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f758-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f758-210">Next steps</span></span>

<span data-ttu-id="1f758-211">In this tutorial, you learned how to use Spark Structured Streaming to write and read data from Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f758-211">In this tutorial, you learned how to use Spark Structured Streaming to write and read data from Kafka on HDInsight.</span></span> <span data-ttu-id="1f758-212">Use the following link to learn how to use Storm with Kafka.</span><span class="sxs-lookup"><span data-stu-id="1f758-212">Use the following link to learn how to use Storm with Kafka.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1f758-213">Use Apache Storm with Kafka</span><span class="sxs-lookup"><span data-stu-id="1f758-213">Use Apache Storm with Kafka</span></span>](hdinsight-apache-storm-with-kafka.md)
