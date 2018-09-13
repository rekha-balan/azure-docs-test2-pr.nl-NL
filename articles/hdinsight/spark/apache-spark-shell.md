---
title: Use an Interactive Spark Shell in Azure HDInsight
description: An interactive Spark Shell provides a read-execute-print process for running Spark commands one at a time and seeing the results.
services: hdinsight
ms.service: hdinsight
author: maxluk
ms.author: maxluk
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/09/2018
ms.openlocfilehash: 5aaf169418962c08f5f45413f53d4c92588a98bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856818"
---
# <a name="run-spark-from-the-spark-shell"></a><span data-ttu-id="4c583-103">Run Spark from the Spark Shell</span><span class="sxs-lookup"><span data-stu-id="4c583-103">Run Spark from the Spark Shell</span></span>

<span data-ttu-id="4c583-104">An interactive Spark Shell provides a REPL (read-execute-print loop) environment for running Spark commands one at a time and seeing the results.</span><span class="sxs-lookup"><span data-stu-id="4c583-104">An interactive Spark Shell provides a REPL (read-execute-print loop) environment for running Spark commands one at a time and seeing the results.</span></span> <span data-ttu-id="4c583-105">This process is useful for development and debugging.</span><span class="sxs-lookup"><span data-stu-id="4c583-105">This process is useful for development and debugging.</span></span> <span data-ttu-id="4c583-106">Spark provides one shell for each of its supported languages: Scala, Python, and R.</span><span class="sxs-lookup"><span data-stu-id="4c583-106">Spark provides one shell for each of its supported languages: Scala, Python, and R.</span></span>

## <a name="get-to-a-spark-shell-with-ssh"></a><span data-ttu-id="4c583-107">Get to a Spark Shell with SSH</span><span class="sxs-lookup"><span data-stu-id="4c583-107">Get to a Spark Shell with SSH</span></span>

<span data-ttu-id="4c583-108">Access a Spark Shell on HDInsight by connecting to the primary head node of the cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="4c583-108">Access a Spark Shell on HDInsight by connecting to the primary head node of the cluster using SSH:</span></span>

     ssh <sshusername>@<clustername>-ssh.azurehdinsight.net

<span data-ttu-id="4c583-109">You can get the complete SSH command for your cluster from the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="4c583-109">You can get the complete SSH command for your cluster from the Azure portal:</span></span>

1. <span data-ttu-id="4c583-110">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c583-110">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c583-111">Navigate to the pane for your HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="4c583-111">Navigate to the pane for your HDInsight Spark cluster.</span></span>
3. <span data-ttu-id="4c583-112">Select Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="4c583-112">Select Secure Shell (SSH).</span></span>

    ![HDInsight pane in Azure portal](./media/apache-spark-shell/hdinsight-spark-blade.png)

4. <span data-ttu-id="4c583-114">Copy the displayed SSH command and run it in your terminal.</span><span class="sxs-lookup"><span data-stu-id="4c583-114">Copy the displayed SSH command and run it in your terminal.</span></span>

    ![HDInsight SSH pane in Azure portal](./media/apache-spark-shell/hdinsight-spark-ssh-blade.png)

<span data-ttu-id="4c583-116">For details on using SSH to connect to HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4c583-116">For details on using SSH to connect to HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="run-a-spark-shell"></a><span data-ttu-id="4c583-117">Run a Spark Shell</span><span class="sxs-lookup"><span data-stu-id="4c583-117">Run a Spark Shell</span></span>

<span data-ttu-id="4c583-118">Spark provides shells for Scala (spark-shell), Python (pyspark), and R (sparkR).</span><span class="sxs-lookup"><span data-stu-id="4c583-118">Spark provides shells for Scala (spark-shell), Python (pyspark), and R (sparkR).</span></span> <span data-ttu-id="4c583-119">In your SSH session at the head node of your HDInsight cluster, enter one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="4c583-119">In your SSH session at the head node of your HDInsight cluster, enter one of the following commands:</span></span>

    ./bin/spark-shell
    ./bin/pyspark
    ./bin/sparkR

<span data-ttu-id="4c583-120">Now you can enter Spark commands in the appropriate language.</span><span class="sxs-lookup"><span data-stu-id="4c583-120">Now you can enter Spark commands in the appropriate language.</span></span>

## <a name="sparksession-and-sparkcontext-instances"></a><span data-ttu-id="4c583-121">SparkSession and SparkContext instances</span><span class="sxs-lookup"><span data-stu-id="4c583-121">SparkSession and SparkContext instances</span></span>

<span data-ttu-id="4c583-122">By default when you run the Spark Shell, instances of SparkSession and SparkContext are automatically instantiated for you.</span><span class="sxs-lookup"><span data-stu-id="4c583-122">By default when you run the Spark Shell, instances of SparkSession and SparkContext are automatically instantiated for you.</span></span>

<span data-ttu-id="4c583-123">To access the SparkSession instance, enter `spark`.</span><span class="sxs-lookup"><span data-stu-id="4c583-123">To access the SparkSession instance, enter `spark`.</span></span> <span data-ttu-id="4c583-124">To access the SparkContext instance, enter `sc`.</span><span class="sxs-lookup"><span data-stu-id="4c583-124">To access the SparkContext instance, enter `sc`.</span></span>

## <a name="important-shell-parameters"></a><span data-ttu-id="4c583-125">Important shell parameters</span><span class="sxs-lookup"><span data-stu-id="4c583-125">Important shell parameters</span></span>

<span data-ttu-id="4c583-126">The Spark Shell command (`spark-shell`, `pyspark`, or `sparkR`) supports many command-line parameters.</span><span class="sxs-lookup"><span data-stu-id="4c583-126">The Spark Shell command (`spark-shell`, `pyspark`, or `sparkR`) supports many command-line parameters.</span></span> <span data-ttu-id="4c583-127">To see a full list of parameters, start the Spark Shell with the switch `--help`.</span><span class="sxs-lookup"><span data-stu-id="4c583-127">To see a full list of parameters, start the Spark Shell with the switch `--help`.</span></span> <span data-ttu-id="4c583-128">Note that some of these parameters may only apply to `spark-submit`, which the Spark Shell wraps.</span><span class="sxs-lookup"><span data-stu-id="4c583-128">Note that some of these parameters may only apply to `spark-submit`, which the Spark Shell wraps.</span></span>

| <span data-ttu-id="4c583-129">switch</span><span class="sxs-lookup"><span data-stu-id="4c583-129">switch</span></span> | <span data-ttu-id="4c583-130">description</span><span class="sxs-lookup"><span data-stu-id="4c583-130">description</span></span> | <span data-ttu-id="4c583-131">example</span><span class="sxs-lookup"><span data-stu-id="4c583-131">example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c583-132">--master MASTER_URL</span><span class="sxs-lookup"><span data-stu-id="4c583-132">--master MASTER_URL</span></span> | <span data-ttu-id="4c583-133">Specifies the master URL.</span><span class="sxs-lookup"><span data-stu-id="4c583-133">Specifies the master URL.</span></span> <span data-ttu-id="4c583-134">In HDInsight, this value is always `yarn`.</span><span class="sxs-lookup"><span data-stu-id="4c583-134">In HDInsight, this value is always `yarn`.</span></span> | `--master yarn`|
| <span data-ttu-id="4c583-135">--jars JAR_LIST</span><span class="sxs-lookup"><span data-stu-id="4c583-135">--jars JAR_LIST</span></span> | <span data-ttu-id="4c583-136">Comma-separated list of local jars to include on the driver and executor classpaths.</span><span class="sxs-lookup"><span data-stu-id="4c583-136">Comma-separated list of local jars to include on the driver and executor classpaths.</span></span> <span data-ttu-id="4c583-137">In HDInsight, this list is composed of paths to the default filesystem in Azure Storage or Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c583-137">In HDInsight, this list is composed of paths to the default filesystem in Azure Storage or Data Lake Store.</span></span> | `--jars /path/to/examples.jar` |
| <span data-ttu-id="4c583-138">--packages MAVEN_COORDS</span><span class="sxs-lookup"><span data-stu-id="4c583-138">--packages MAVEN_COORDS</span></span> | <span data-ttu-id="4c583-139">Comma-separated list of maven coordinates of jars to include on the driver and executor classpaths.</span><span class="sxs-lookup"><span data-stu-id="4c583-139">Comma-separated list of maven coordinates of jars to include on the driver and executor classpaths.</span></span> <span data-ttu-id="4c583-140">Searches the local maven repo, then maven central, then any additional remote repositories specified with `--repositories`.</span><span class="sxs-lookup"><span data-stu-id="4c583-140">Searches the local maven repo, then maven central, then any additional remote repositories specified with `--repositories`.</span></span> <span data-ttu-id="4c583-141">The format for the coordinates is *groupId*:*artifactId*:*version*.</span><span class="sxs-lookup"><span data-stu-id="4c583-141">The format for the coordinates is *groupId*:*artifactId*:*version*.</span></span> | `--packages "com.microsoft.azure:azure-eventhubs:0.14.0"`|
| <span data-ttu-id="4c583-142">--py-files LIST</span><span class="sxs-lookup"><span data-stu-id="4c583-142">--py-files LIST</span></span> | <span data-ttu-id="4c583-143">For Python only, a comma-separated list of .zip, .egg, or .py files to place on the PYTHONPATH.</span><span class="sxs-lookup"><span data-stu-id="4c583-143">For Python only, a comma-separated list of .zip, .egg, or .py files to place on the PYTHONPATH.</span></span> | `--pyfiles "samples.py"` |

## <a name="next-steps"></a><span data-ttu-id="4c583-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c583-144">Next steps</span></span>

- <span data-ttu-id="4c583-145">See [Introduction to Spark on Azure HDInsight](apache-spark-overview.md) for an overview.</span><span class="sxs-lookup"><span data-stu-id="4c583-145">See [Introduction to Spark on Azure HDInsight](apache-spark-overview.md) for an overview.</span></span>
- <span data-ttu-id="4c583-146">See [Create an Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md) to work with Spark clusters and SparkSQL.</span><span class="sxs-lookup"><span data-stu-id="4c583-146">See [Create an Apache Spark cluster in Azure HDInsight](apache-spark-jupyter-spark-sql.md) to work with Spark clusters and SparkSQL.</span></span>
- <span data-ttu-id="4c583-147">See [What is Spark Structured Streaming?](apache-spark-streaming-overview.md) to write applications that process streaming data with Spark.</span><span class="sxs-lookup"><span data-stu-id="4c583-147">See [What is Spark Structured Streaming?](apache-spark-streaming-overview.md) to write applications that process streaming data with Spark.</span></span>

