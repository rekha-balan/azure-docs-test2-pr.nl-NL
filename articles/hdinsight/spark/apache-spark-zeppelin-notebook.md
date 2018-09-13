---
title: Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight
description: Step-by-step instructions on how to use Zeppelin notebooks with Apache Spark clusters on Azure HDInsight.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/21/2018
ms.openlocfilehash: 9b076709ee24c61b2699672d28bd61204c88a744
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865285"
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="40f94-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="40f94-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="40f94-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="40f94-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="40f94-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="40f94-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="40f94-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="40f94-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="40f94-107">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="40f94-107">**Prerequisites:**</span></span>

* <span data-ttu-id="40f94-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="40f94-108">An Azure subscription.</span></span> <span data-ttu-id="40f94-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="40f94-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="40f94-110">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40f94-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="40f94-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="40f94-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="40f94-112">Launch a Zeppelin notebook</span><span class="sxs-lookup"><span data-stu-id="40f94-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="40f94-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span><span class="sxs-lookup"><span data-stu-id="40f94-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="40f94-114">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="40f94-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40f94-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="40f94-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="40f94-116">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="40f94-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
1. <span data-ttu-id="40f94-117">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="40f94-117">Create a new notebook.</span></span> <span data-ttu-id="40f94-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span><span class="sxs-lookup"><span data-stu-id="40f94-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="40f94-119">![Create a new Zeppelin notebook](./media/apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span><span class="sxs-lookup"><span data-stu-id="40f94-119">![Create a new Zeppelin notebook](./media/apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="40f94-120">Enter a name for the notebook, and then click **Create Note**.</span><span class="sxs-lookup"><span data-stu-id="40f94-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
1. <span data-ttu-id="40f94-121">Also, make sure the notebook header shows a connected status.</span><span class="sxs-lookup"><span data-stu-id="40f94-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="40f94-122">It is denoted by a green dot in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="40f94-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="40f94-123">![Zeppelin notebook status](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span><span class="sxs-lookup"><span data-stu-id="40f94-123">![Zeppelin notebook status](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
1. <span data-ttu-id="40f94-124">Load sample data into a temporary table.</span><span class="sxs-lookup"><span data-stu-id="40f94-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="40f94-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="40f94-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="40f94-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span><span class="sxs-lookup"><span data-stu-id="40f94-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
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
   
    <span data-ttu-id="40f94-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span><span class="sxs-lookup"><span data-stu-id="40f94-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="40f94-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span><span class="sxs-lookup"><span data-stu-id="40f94-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="40f94-129">The output shows up at the bottom of the same paragraph.</span><span class="sxs-lookup"><span data-stu-id="40f94-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="40f94-130">The screenshot looks like the following:</span><span class="sxs-lookup"><span data-stu-id="40f94-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="40f94-131">![Create a temporary table from raw data](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span><span class="sxs-lookup"><span data-stu-id="40f94-131">![Create a temporary table from raw data](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="40f94-132">You can also provide a title to each paragraph.</span><span class="sxs-lookup"><span data-stu-id="40f94-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="40f94-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span><span class="sxs-lookup"><span data-stu-id="40f94-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
1. <span data-ttu-id="40f94-134">You can now run Spark SQL statements on the **hvac** table.</span><span class="sxs-lookup"><span data-stu-id="40f94-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="40f94-135">Paste the following query in a new paragraph.</span><span class="sxs-lookup"><span data-stu-id="40f94-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="40f94-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span><span class="sxs-lookup"><span data-stu-id="40f94-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="40f94-137">Press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="40f94-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="40f94-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span><span class="sxs-lookup"><span data-stu-id="40f94-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="40f94-139">The following screenshot shows the output.</span><span class="sxs-lookup"><span data-stu-id="40f94-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="40f94-140">![Run a Spark SQL statement using the notebook](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span><span class="sxs-lookup"><span data-stu-id="40f94-140">![Run a Spark SQL statement using the notebook](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="40f94-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span><span class="sxs-lookup"><span data-stu-id="40f94-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="40f94-142">Click **Settings** to choose what consitutes the key and values in the output.</span><span class="sxs-lookup"><span data-stu-id="40f94-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="40f94-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span><span class="sxs-lookup"><span data-stu-id="40f94-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
1. <span data-ttu-id="40f94-144">You can also run Spark SQL statements using variables in the query.</span><span class="sxs-lookup"><span data-stu-id="40f94-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="40f94-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span><span class="sxs-lookup"><span data-stu-id="40f94-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="40f94-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span><span class="sxs-lookup"><span data-stu-id="40f94-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="40f94-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="40f94-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="40f94-148">The following screenshot shows the output.</span><span class="sxs-lookup"><span data-stu-id="40f94-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="40f94-149">![Run a Spark SQL statement using the notebook](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span><span class="sxs-lookup"><span data-stu-id="40f94-149">![Run a Spark SQL statement using the notebook](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="40f94-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span><span class="sxs-lookup"><span data-stu-id="40f94-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="40f94-151">Click **Settings** to choose what consitutes the key and values in the output.</span><span class="sxs-lookup"><span data-stu-id="40f94-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="40f94-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span><span class="sxs-lookup"><span data-stu-id="40f94-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
1. <span data-ttu-id="40f94-153">Restart the Livy interpreter to exit the application.</span><span class="sxs-lookup"><span data-stu-id="40f94-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="40f94-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="40f94-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="40f94-155">![Launch interpreter](./media/apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="40f94-155">![Launch interpreter](./media/apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
1. <span data-ttu-id="40f94-156">Scroll to Livy interpreter settings and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="40f94-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="40f94-157">![Restart the Livy intepreter](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="40f94-157">![Restart the Livy intepreter](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="40f94-158">How do I use external packages with the notebook?</span><span class="sxs-lookup"><span data-stu-id="40f94-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="40f94-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span><span class="sxs-lookup"><span data-stu-id="40f94-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="40f94-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span><span class="sxs-lookup"><span data-stu-id="40f94-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="40f94-161">You can also get a list of available packages from other sources.</span><span class="sxs-lookup"><span data-stu-id="40f94-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="40f94-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="40f94-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="40f94-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="40f94-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="40f94-164">Open interpreter settings.</span><span class="sxs-lookup"><span data-stu-id="40f94-164">Open interpreter settings.</span></span> <span data-ttu-id="40f94-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="40f94-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="40f94-166">![Launch interpreter](./media/apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="40f94-166">![Launch interpreter](./media/apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
1. <span data-ttu-id="40f94-167">Scroll to Livy interpreter settings and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="40f94-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="40f94-168">![Change interpreter settings](./media/apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span><span class="sxs-lookup"><span data-stu-id="40f94-168">![Change interpreter settings](./media/apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
1. <span data-ttu-id="40f94-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="40f94-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="40f94-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="40f94-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="40f94-171">![Change interpreter settings](./media/apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span><span class="sxs-lookup"><span data-stu-id="40f94-171">![Change interpreter settings](./media/apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="40f94-172">Click **Save** and then restart the Livy interpreter.</span><span class="sxs-lookup"><span data-stu-id="40f94-172">Click **Save** and then restart the Livy interpreter.</span></span>
1. <span data-ttu-id="40f94-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span><span class="sxs-lookup"><span data-stu-id="40f94-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="40f94-174">a.</span><span class="sxs-lookup"><span data-stu-id="40f94-174">a.</span></span> <span data-ttu-id="40f94-175">Locate the package in the Maven Repository.</span><span class="sxs-lookup"><span data-stu-id="40f94-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="40f94-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="40f94-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="40f94-177">b.</span><span class="sxs-lookup"><span data-stu-id="40f94-177">b.</span></span> <span data-ttu-id="40f94-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span><span class="sxs-lookup"><span data-stu-id="40f94-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="40f94-179">![Use external packages with Jupyter notebook](./media/apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="40f94-179">![Use external packages with Jupyter notebook](./media/apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="40f94-180">c.</span><span class="sxs-lookup"><span data-stu-id="40f94-180">c.</span></span> <span data-ttu-id="40f94-181">Concatenate the three values, separated by a colon (**:**).</span><span class="sxs-lookup"><span data-stu-id="40f94-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="40f94-182">Where are the Zeppelin notebooks saved?</span><span class="sxs-lookup"><span data-stu-id="40f94-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="40f94-183">The Zeppelin notebooks are saved to the cluster headnodes.</span><span class="sxs-lookup"><span data-stu-id="40f94-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="40f94-184">So, if you delete the cluster, the notebooks will be deleted as well.</span><span class="sxs-lookup"><span data-stu-id="40f94-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="40f94-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span><span class="sxs-lookup"><span data-stu-id="40f94-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="40f94-186">To export a notebook, click the **Export** icon as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="40f94-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="40f94-187">![Download notebook](./media/apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span><span class="sxs-lookup"><span data-stu-id="40f94-187">![Download notebook](./media/apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="40f94-188">This saves the notebook as a JSON file in your download location.</span><span class="sxs-lookup"><span data-stu-id="40f94-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="40f94-189">Livy session management</span><span class="sxs-lookup"><span data-stu-id="40f94-189">Livy session management</span></span>
<span data-ttu-id="40f94-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="40f94-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="40f94-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span><span class="sxs-lookup"><span data-stu-id="40f94-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="40f94-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="40f94-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="40f94-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="40f94-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="40f94-194">Restart the Livy interpreter from the Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="40f94-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="40f94-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="40f94-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="40f94-196">![Launch interpreter](./media/apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="40f94-196">![Launch interpreter](./media/apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
1. <span data-ttu-id="40f94-197">Scroll to Livy interpreter settings and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="40f94-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="40f94-198">![Restart the Livy intepreter](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="40f94-198">![Restart the Livy intepreter](./media/apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
1. <span data-ttu-id="40f94-199">Run a code cell from an existing Zeppelin notebook.</span><span class="sxs-lookup"><span data-stu-id="40f94-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="40f94-200">This creates a new Livy session in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="40f94-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <a name="seealso"></a><span data-ttu-id="40f94-201">See also</span><span class="sxs-lookup"><span data-stu-id="40f94-201">See also</span></span>
* [<span data-ttu-id="40f94-202">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="40f94-202">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="40f94-203">Scenarios</span><span class="sxs-lookup"><span data-stu-id="40f94-203">Scenarios</span></span>
* [<span data-ttu-id="40f94-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="40f94-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="40f94-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="40f94-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="40f94-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="40f94-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="40f94-207">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="40f94-207">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="40f94-208">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="40f94-208">Create and run applications</span></span>
* [<span data-ttu-id="40f94-209">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="40f94-209">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="40f94-210">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="40f94-210">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="40f94-211">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="40f94-211">Tools and extensions</span></span>
* [<span data-ttu-id="40f94-212">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="40f94-212">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="40f94-213">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="40f94-213">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="40f94-214">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="40f94-214">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="40f94-215">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="40f94-215">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="40f94-216">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="40f94-216">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="40f94-217">Manage resources</span><span class="sxs-lookup"><span data-stu-id="40f94-217">Manage resources</span></span>
* [<span data-ttu-id="40f94-218">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="40f94-218">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="40f94-219">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="40f94-219">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../../storage/common/storage-create-storage-account.md 







