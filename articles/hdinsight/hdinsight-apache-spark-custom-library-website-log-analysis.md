---
title: Use Python libraries to analyze website logs in Azure Spark cluster | Microsoft Docs
description: Use custom libraries with an HDInsight Spark cluster to analyze website logs
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: bb64b2a00d389b29a37e4abf0d44974252cbb512
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551672"
---
# <a name="analyze-website-logs-using-a-custom-library-with-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="2d630-103">Analyze website logs using a custom library with Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d630-103">Analyze website logs using a custom library with Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="2d630-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2d630-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="2d630-105">The custom library we use is a Python library called **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="2d630-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="2d630-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2d630-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="2d630-107">The notebook experience lets you run the Python snippets from the notebook itself.</span><span class="sxs-lookup"><span data-stu-id="2d630-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="2d630-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span><span class="sxs-lookup"><span data-stu-id="2d630-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="2d630-109">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="2d630-109">**Prerequisites:**</span></span>

<span data-ttu-id="2d630-110">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-110">You must have the following:</span></span>

* <span data-ttu-id="2d630-111">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2d630-111">An Azure subscription.</span></span> <span data-ttu-id="2d630-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2d630-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="2d630-113">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2d630-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2d630-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2d630-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="2d630-115">Save raw data as an RDD</span><span class="sxs-lookup"><span data-stu-id="2d630-115">Save raw data as an RDD</span></span>
<span data-ttu-id="2d630-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span><span class="sxs-lookup"><span data-stu-id="2d630-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="2d630-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span><span class="sxs-lookup"><span data-stu-id="2d630-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="2d630-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span><span class="sxs-lookup"><span data-stu-id="2d630-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="2d630-119">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span><span class="sxs-lookup"><span data-stu-id="2d630-119">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="2d630-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span><span class="sxs-lookup"><span data-stu-id="2d630-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="2d630-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="2d630-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="2d630-122">If prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="2d630-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2d630-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="2d630-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="2d630-124">Replace **CLUSTERNAME** with the name of your cluster:</span><span class="sxs-lookup"><span data-stu-id="2d630-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="2d630-125">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="2d630-125">Create a new notebook.</span></span> <span data-ttu-id="2d630-126">Click **New**, and then click **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="2d630-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="2d630-127">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span><span class="sxs-lookup"><span data-stu-id="2d630-127">![Create a new Jupyter notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/hdispark.note.jupyter.createnotebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="2d630-128">A new notebook is created and opened with the name Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="2d630-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="2d630-129">Click the notebook name at the top, and enter a friendly name.</span><span class="sxs-lookup"><span data-stu-id="2d630-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="2d630-130">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span><span class="sxs-lookup"><span data-stu-id="2d630-130">![Provide a name for the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/hdispark.note.jupyter.notebook.name.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="2d630-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span><span class="sxs-lookup"><span data-stu-id="2d630-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="2d630-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span><span class="sxs-lookup"><span data-stu-id="2d630-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="2d630-133">You can start by importing the types that are required for this scenario.</span><span class="sxs-lookup"><span data-stu-id="2d630-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="2d630-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="2d630-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="2d630-135">Create an RDD using the sample log data already available on the cluster.</span><span class="sxs-lookup"><span data-stu-id="2d630-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="2d630-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="2d630-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasbs:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="2d630-137">Retrieve a sample log set to verify that the previous step completed successfully.</span><span class="sxs-lookup"><span data-stu-id="2d630-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="2d630-138">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="2d630-139">Analyze log data using a custom Python library</span><span class="sxs-lookup"><span data-stu-id="2d630-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="2d630-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span><span class="sxs-lookup"><span data-stu-id="2d630-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="2d630-141">Parsing such logs could be complicated.</span><span class="sxs-lookup"><span data-stu-id="2d630-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="2d630-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span><span class="sxs-lookup"><span data-stu-id="2d630-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="2d630-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="2d630-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="2d630-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="2d630-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="2d630-145">To use this library, we must distribute it to all the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="2d630-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="2d630-146">Run the following snippet.</span><span class="sxs-lookup"><span data-stu-id="2d630-146">Run the following snippet.</span></span>

        sc.addPyFile('wasbs:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="2d630-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span><span class="sxs-lookup"><span data-stu-id="2d630-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="2d630-148">Use the `LogLine` class to extract only the log lines from the RDD:</span><span class="sxs-lookup"><span data-stu-id="2d630-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="2d630-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span><span class="sxs-lookup"><span data-stu-id="2d630-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="2d630-150">The output should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="2d630-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span><span class="sxs-lookup"><span data-stu-id="2d630-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="2d630-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span><span class="sxs-lookup"><span data-stu-id="2d630-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasbs:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="2d630-153">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="2d630-154">You can also use **Matplotlib** to construct a visualization of the data.</span><span class="sxs-lookup"><span data-stu-id="2d630-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="2d630-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span><span class="sxs-lookup"><span data-stu-id="2d630-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="2d630-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span><span class="sxs-lookup"><span data-stu-id="2d630-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="2d630-157">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-157">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="2d630-158">You can also present this information in the form of plot.</span><span class="sxs-lookup"><span data-stu-id="2d630-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="2d630-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="2d630-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="2d630-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span><span class="sxs-lookup"><span data-stu-id="2d630-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="2d630-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span><span class="sxs-lookup"><span data-stu-id="2d630-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="2d630-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span><span class="sxs-lookup"><span data-stu-id="2d630-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="2d630-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="2d630-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="2d630-164">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-164">You should see an output like the following:</span></span>

   <span data-ttu-id="2d630-165">![SQL query output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/sql.output.png "SQL query output")</span><span class="sxs-lookup"><span data-stu-id="2d630-165">![SQL query output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/sql.output.png "SQL query output")</span></span>

   <span data-ttu-id="2d630-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="2d630-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="2d630-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span><span class="sxs-lookup"><span data-stu-id="2d630-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="2d630-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="2d630-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="2d630-169">This ensures that the code is run locally on the Jupyter server.</span><span class="sxs-lookup"><span data-stu-id="2d630-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="2d630-170">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="2d630-170">You should see an output like the following:</span></span>

   <span data-ttu-id="2d630-171">![Matplotlib output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/hdi-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span><span class="sxs-lookup"><span data-stu-id="2d630-171">![Matplotlib output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-custom-library-website-log-analysis/hdi-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="2d630-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span><span class="sxs-lookup"><span data-stu-id="2d630-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="2d630-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="2d630-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="2d630-174">This will shutdown and close the notebook.</span><span class="sxs-lookup"><span data-stu-id="2d630-174">This will shutdown and close the notebook.</span></span>

## <a name="seealso"></a><span data-ttu-id="2d630-175">See also</span><span class="sxs-lookup"><span data-stu-id="2d630-175">See also</span></span>
* [<span data-ttu-id="2d630-176">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d630-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="2d630-177">Scenarios</span><span class="sxs-lookup"><span data-stu-id="2d630-177">Scenarios</span></span>
* [<span data-ttu-id="2d630-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="2d630-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2d630-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="2d630-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2d630-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="2d630-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2d630-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="2d630-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="2d630-182">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="2d630-182">Create and run applications</span></span>
* [<span data-ttu-id="2d630-183">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="2d630-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2d630-184">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="2d630-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2d630-185">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="2d630-185">Tools and extensions</span></span>
* [<span data-ttu-id="2d630-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="2d630-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2d630-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="2d630-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="2d630-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d630-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="2d630-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d630-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2d630-190">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="2d630-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="2d630-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="2d630-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="2d630-192">Manage resources</span><span class="sxs-lookup"><span data-stu-id="2d630-192">Manage resources</span></span>
* [<span data-ttu-id="2d630-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d630-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2d630-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d630-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)




