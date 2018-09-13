---
title: Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight | Microsoft Docs
description: Step-by-step instructions on how to use Zeppelin notebooks with Apache Spark clusters on Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: 3c8402a74f9def10586c984d7a2e26b21959f962
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556784"
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="01244-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="01244-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="01244-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="01244-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="01244-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="01244-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="01244-106">By default, Zeppelin notebooks are available only for Spark 1.6.2 on HDInsight cluster version 3.5.</span><span class="sxs-lookup"><span data-stu-id="01244-106">By default, Zeppelin notebooks are available only for Spark 1.6.2 on HDInsight cluster version 3.5.</span></span> <span data-ttu-id="01244-107">If you want to use Zeppelin on other versions of HDInsight Spark clusters, you can install Zeppelin using script action.</span><span class="sxs-lookup"><span data-stu-id="01244-107">If you want to use Zeppelin on other versions of HDInsight Spark clusters, you can install Zeppelin using script action.</span></span> <span data-ttu-id="01244-108">For instructions, see [Install Zeppelin notebooks for Apache Spark cluster on HDInsight Linux](hdinsight-apache-spark-use-zeppelin-notebook.md).</span><span class="sxs-lookup"><span data-stu-id="01244-108">For instructions, see [Install Zeppelin notebooks for Apache Spark cluster on HDInsight Linux](hdinsight-apache-spark-use-zeppelin-notebook.md).</span></span>
> 
>

<span data-ttu-id="01244-109">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="01244-109">**Prerequisites:**</span></span>

* <span data-ttu-id="01244-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="01244-110">An Azure subscription.</span></span> <span data-ttu-id="01244-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="01244-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="01244-112">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01244-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="01244-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="01244-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="01244-114">Launch a Zeppelin notebook</span><span class="sxs-lookup"><span data-stu-id="01244-114">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="01244-115">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span><span class="sxs-lookup"><span data-stu-id="01244-115">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="01244-116">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="01244-116">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01244-117">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="01244-117">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="01244-118">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="01244-118">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="01244-119">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="01244-119">Create a new notebook.</span></span> <span data-ttu-id="01244-120">From the header pane, click **Notebook**, and then click **Create New Note**.</span><span class="sxs-lookup"><span data-stu-id="01244-120">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="01244-121">![Create a new Zeppelin notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.createnewnote.png "Create a new Zeppelin notebook")</span><span class="sxs-lookup"><span data-stu-id="01244-121">![Create a new Zeppelin notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.createnewnote.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="01244-122">Enter a name for the notebook, and then click **Create Note**.</span><span class="sxs-lookup"><span data-stu-id="01244-122">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="01244-123">Also, make sure the notebook header shows a connected status.</span><span class="sxs-lookup"><span data-stu-id="01244-123">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="01244-124">It is denoted by a green dot in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="01244-124">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="01244-125">![Zeppelin notebook status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.newnote.connected.png "Zeppelin notebook status")</span><span class="sxs-lookup"><span data-stu-id="01244-125">![Zeppelin notebook status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.newnote.connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="01244-126">Load sample data into a temporary table.</span><span class="sxs-lookup"><span data-stu-id="01244-126">Load sample data into a temporary table.</span></span> <span data-ttu-id="01244-127">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="01244-127">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="01244-128">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span><span class="sxs-lookup"><span data-stu-id="01244-128">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="01244-129">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span><span class="sxs-lookup"><span data-stu-id="01244-129">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="01244-130">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span><span class="sxs-lookup"><span data-stu-id="01244-130">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="01244-131">The output shows up at the bottom of the same paragraph.</span><span class="sxs-lookup"><span data-stu-id="01244-131">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="01244-132">The screenshot looks like the following:</span><span class="sxs-lookup"><span data-stu-id="01244-132">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="01244-133">![Create a temporary table from raw data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.note.loaddDataintotable.png "Create a temporary table from raw data")</span><span class="sxs-lookup"><span data-stu-id="01244-133">![Create a temporary table from raw data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.note.loaddDataintotable.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="01244-134">You can also provide a title to each paragraph.</span><span class="sxs-lookup"><span data-stu-id="01244-134">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="01244-135">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span><span class="sxs-lookup"><span data-stu-id="01244-135">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="01244-136">You can now run Spark SQL statements on the **hvac** table.</span><span class="sxs-lookup"><span data-stu-id="01244-136">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="01244-137">Paste the following query in a new paragraph.</span><span class="sxs-lookup"><span data-stu-id="01244-137">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="01244-138">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span><span class="sxs-lookup"><span data-stu-id="01244-138">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="01244-139">Press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="01244-139">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="01244-140">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span><span class="sxs-lookup"><span data-stu-id="01244-140">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="01244-141">The following screenshot shows the output.</span><span class="sxs-lookup"><span data-stu-id="01244-141">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="01244-142">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.note.sparksqlquery1.png "Run a Spark SQL statement using the notebook")</span><span class="sxs-lookup"><span data-stu-id="01244-142">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.note.sparksqlquery1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="01244-143">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span><span class="sxs-lookup"><span data-stu-id="01244-143">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="01244-144">Click **Settings** to choose what consitutes the key and values in the output.</span><span class="sxs-lookup"><span data-stu-id="01244-144">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="01244-145">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span><span class="sxs-lookup"><span data-stu-id="01244-145">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="01244-146">You can also run Spark SQL statements using variables in the query.</span><span class="sxs-lookup"><span data-stu-id="01244-146">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="01244-147">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span><span class="sxs-lookup"><span data-stu-id="01244-147">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="01244-148">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span><span class="sxs-lookup"><span data-stu-id="01244-148">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="01244-149">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="01244-149">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="01244-150">The following screenshot shows the output.</span><span class="sxs-lookup"><span data-stu-id="01244-150">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="01244-151">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.note.sparksqlquery2.png "Run a Spark SQL statement using the notebook")</span><span class="sxs-lookup"><span data-stu-id="01244-151">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.note.sparksqlquery2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="01244-152">For subsequent queries, you can select a new value from the drop-down and run the query again.</span><span class="sxs-lookup"><span data-stu-id="01244-152">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="01244-153">Click **Settings** to choose what consitutes the key and values in the output.</span><span class="sxs-lookup"><span data-stu-id="01244-153">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="01244-154">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span><span class="sxs-lookup"><span data-stu-id="01244-154">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="01244-155">Restart the Livy interpreter to exit the application.</span><span class="sxs-lookup"><span data-stu-id="01244-155">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="01244-156">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="01244-156">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="01244-157">![Launch interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="01244-157">![Launch interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="01244-158">Scroll to Livy interpreter settings and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="01244-158">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="01244-159">![Restart the Livy intepreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.zeppelin.restart.interpreter.png "Restart the Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="01244-159">![Restart the Livy intepreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.zeppelin.restart.interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="01244-160">How do I use external packages with the notebook?</span><span class="sxs-lookup"><span data-stu-id="01244-160">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="01244-161">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span><span class="sxs-lookup"><span data-stu-id="01244-161">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="01244-162">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span><span class="sxs-lookup"><span data-stu-id="01244-162">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="01244-163">You can also get a list of available packages from other sources.</span><span class="sxs-lookup"><span data-stu-id="01244-163">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="01244-164">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="01244-164">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="01244-165">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="01244-165">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="01244-166">Open interpreter settings.</span><span class="sxs-lookup"><span data-stu-id="01244-166">Open interpreter settings.</span></span> <span data-ttu-id="01244-167">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="01244-167">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="01244-168">![Launch interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="01244-168">![Launch interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="01244-169">Scroll to Livy interpreter settings and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="01244-169">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="01244-170">![Change interpreter settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span><span class="sxs-lookup"><span data-stu-id="01244-170">![Change interpreter settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="01244-171">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="01244-171">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="01244-172">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="01244-172">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="01244-173">![Change interpreter settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span><span class="sxs-lookup"><span data-stu-id="01244-173">![Change interpreter settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="01244-174">Click **Save** and then restart the Livy interpreter.</span><span class="sxs-lookup"><span data-stu-id="01244-174">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="01244-175">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span><span class="sxs-lookup"><span data-stu-id="01244-175">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="01244-176">a.</span><span class="sxs-lookup"><span data-stu-id="01244-176">a.</span></span> <span data-ttu-id="01244-177">Locate the package in the Maven Repository.</span><span class="sxs-lookup"><span data-stu-id="01244-177">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="01244-178">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="01244-178">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="01244-179">b.</span><span class="sxs-lookup"><span data-stu-id="01244-179">b.</span></span> <span data-ttu-id="01244-180">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span><span class="sxs-lookup"><span data-stu-id="01244-180">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="01244-181">![Use external packages with Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="01244-181">![Use external packages with Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="01244-182">c.</span><span class="sxs-lookup"><span data-stu-id="01244-182">c.</span></span> <span data-ttu-id="01244-183">Concatenate the three values, separated by a colon (**:**).</span><span class="sxs-lookup"><span data-stu-id="01244-183">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="01244-184">Where are the Zeppelin notebooks saved?</span><span class="sxs-lookup"><span data-stu-id="01244-184">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="01244-185">The Zeppelin notebooks are saved to the cluster headnodes.</span><span class="sxs-lookup"><span data-stu-id="01244-185">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="01244-186">So, if you delete the cluster, the notebooks will be deleted as well.</span><span class="sxs-lookup"><span data-stu-id="01244-186">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="01244-187">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span><span class="sxs-lookup"><span data-stu-id="01244-187">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="01244-188">To export a notebook, click the **Export** icon as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="01244-188">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="01244-189">![Download notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span><span class="sxs-lookup"><span data-stu-id="01244-189">![Download notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="01244-190">This saves the notebook as a JSON file in your download location.</span><span class="sxs-lookup"><span data-stu-id="01244-190">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="01244-191">Livy session management</span><span class="sxs-lookup"><span data-stu-id="01244-191">Livy session management</span></span>
<span data-ttu-id="01244-192">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="01244-192">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="01244-193">This session is shared across all Zeppelin notebooks that you subsequently create.</span><span class="sxs-lookup"><span data-stu-id="01244-193">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="01244-194">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="01244-194">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="01244-195">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="01244-195">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="01244-196">Restart the Livy interpreter from the Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="01244-196">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="01244-197">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="01244-197">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="01244-198">![Launch interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="01244-198">![Launch interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="01244-199">Scroll to Livy interpreter settings and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="01244-199">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="01244-200">![Restart the Livy intepreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.zeppelin.restart.interpreter.png "Restart the Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="01244-200">![Restart the Livy intepreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-zeppelin-notebook/hdispark.zeppelin.restart.interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="01244-201">Run a code cell from an existing Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="01244-201">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="01244-202">This creates a new Livy session in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="01244-202">This creates a new Livy session in the HDInsight cluster.</span></span>

## <a name="seealso"></a><span data-ttu-id="01244-203">See also</span><span class="sxs-lookup"><span data-stu-id="01244-203">See also</span></span>
* [<span data-ttu-id="01244-204">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="01244-204">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="01244-205">Scenarios</span><span class="sxs-lookup"><span data-stu-id="01244-205">Scenarios</span></span>
* [<span data-ttu-id="01244-206">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="01244-206">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="01244-207">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="01244-207">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="01244-208">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="01244-208">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="01244-209">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="01244-209">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="01244-210">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="01244-210">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="01244-211">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="01244-211">Create and run applications</span></span>
* [<span data-ttu-id="01244-212">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="01244-212">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="01244-213">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="01244-213">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="01244-214">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="01244-214">Tools and extensions</span></span>
* [<span data-ttu-id="01244-215">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="01244-215">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="01244-216">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="01244-216">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="01244-217">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="01244-217">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="01244-218">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="01244-218">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="01244-219">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="01244-219">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="01244-220">Manage resources</span><span class="sxs-lookup"><span data-stu-id="01244-220">Manage resources</span></span>
* [<span data-ttu-id="01244-221">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="01244-221">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="01244-222">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="01244-222">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md 





















