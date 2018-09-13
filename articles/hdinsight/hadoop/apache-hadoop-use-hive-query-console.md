---
title: Use Hadoop Hive on the Query Console in HDInsight - Azure
description: Learn how to use the web-based Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 01/12/2017
ms.author: jasonh
ROBOTS: NOINDEX
ms.openlocfilehash: e080085faa45e0eb330e49edb4450c5a44eb755b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857209"
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="22a67-103">Run Hive queries using the Query Console</span><span class="sxs-lookup"><span data-stu-id="22a67-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="22a67-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span><span class="sxs-lookup"><span data-stu-id="22a67-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22a67-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="22a67-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="22a67-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="22a67-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22a67-107">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="22a67-107">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="22a67-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](apache-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span><span class="sxs-lookup"><span data-stu-id="22a67-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](apache-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <a id="prereq"></a><span data-ttu-id="22a67-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="22a67-109">Prerequisites</span></span>
<span data-ttu-id="22a67-110">To complete the steps in this article, you will need the following.</span><span class="sxs-lookup"><span data-stu-id="22a67-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="22a67-111">A Windows-based HDInsight Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="22a67-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="22a67-112">A modern web browser</span><span class="sxs-lookup"><span data-stu-id="22a67-112">A modern web browser</span></span>

## <a id="run"></a> <span data-ttu-id="22a67-113">Run Hive queries using the Query Console</span><span class="sxs-lookup"><span data-stu-id="22a67-113">Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="22a67-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="22a67-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="22a67-115">If prompted, enter the user name and password that you used when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="22a67-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="22a67-116">From the links at the top of the page, select **Hive Editor**.</span><span class="sxs-lookup"><span data-stu-id="22a67-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="22a67-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="22a67-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![the hive editor](./media/apache-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="22a67-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="22a67-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="22a67-120">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="22a67-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="22a67-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span><span class="sxs-lookup"><span data-stu-id="22a67-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="22a67-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span><span class="sxs-lookup"><span data-stu-id="22a67-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="22a67-123">External tables store only the table definition in Hive; the data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="22a67-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="22a67-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span><span class="sxs-lookup"><span data-stu-id="22a67-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="22a67-125">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="22a67-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="22a67-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="22a67-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="22a67-127">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="22a67-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="22a67-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span><span class="sxs-lookup"><span data-stu-id="22a67-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="22a67-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="22a67-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="22a67-130">This should return a value of **3** because there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="22a67-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="22a67-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="22a67-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="22a67-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span><span class="sxs-lookup"><span data-stu-id="22a67-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="22a67-133">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="22a67-133">Click **Submit**.</span></span> <span data-ttu-id="22a67-134">The **Job Session** at the bottom of the page should display details for the job.</span><span class="sxs-lookup"><span data-stu-id="22a67-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="22a67-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span><span class="sxs-lookup"><span data-stu-id="22a67-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="22a67-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="22a67-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="22a67-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span><span class="sxs-lookup"><span data-stu-id="22a67-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <a id="summary"></a><span data-ttu-id="22a67-138">Summary</span><span class="sxs-lookup"><span data-stu-id="22a67-138">Summary</span></span>
<span data-ttu-id="22a67-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="22a67-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="22a67-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span><span class="sxs-lookup"><span data-stu-id="22a67-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="22a67-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span><span class="sxs-lookup"><span data-stu-id="22a67-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="22a67-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="22a67-142">Next steps</span></span>
<span data-ttu-id="22a67-143">For general information about Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="22a67-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="22a67-144">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="22a67-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="22a67-145">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="22a67-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="22a67-146">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="22a67-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="22a67-147">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="22a67-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="22a67-148">If you are using Tez with Hive, see the following documents for debugging information:</span><span class="sxs-lookup"><span data-stu-id="22a67-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="22a67-149">Use the Tez UI on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="22a67-149">Use the Tez UI on Windows-based HDInsight</span></span>](../hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="22a67-150">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="22a67-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](../hdinsight-debug-ambari-tez-view.md)

[1]:apache-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]:apache-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
