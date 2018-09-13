---
title: Troubleshoot Hive by using Azure HDInsight
description: Get answers to common questions about working with Apache Hive and Azure HDInsight.
keywords: Azure HDInsight, Hive, FAQ, troubleshooting guide, common questions
services: hdinsight
ms.service: hdinsight
author: dharmeshkakadia
ms.author: dharmeshkakadia
ms.topic: conceptual
ms.date: 11/2/2017
ms.openlocfilehash: 832fab6c4f183ddad512c5e6e4309d70938a316b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866847"
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="b2928-104">Troubleshoot Hive by using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2928-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="b2928-105">Learn about the top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="b2928-105">Learn about the top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="b2928-106">How do I export a Hive metastore and import it on another cluster?</span><span class="sxs-lookup"><span data-stu-id="b2928-106">How do I export a Hive metastore and import it on another cluster?</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="b2928-107">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="b2928-107">Resolution steps</span></span>

1. <span data-ttu-id="b2928-108">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span><span class="sxs-lookup"><span data-stu-id="b2928-108">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="b2928-109">For more information, see [Additional reading](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="b2928-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="b2928-110">Run the following command on the HDInsight cluster from which you want to export the metastore:</span><span class="sxs-lookup"><span data-stu-id="b2928-110">Run the following command on the HDInsight cluster from which you want to export the metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="b2928-111">This command generates a file named allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="b2928-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="b2928-112">Copy the file alltables.sql to the new HDInsight cluster, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-112">Copy the file alltables.sql to the new HDInsight cluster, and then run the following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="b2928-113">The code in the resolution steps assumes that data paths on the new cluster are the same as the data paths on the old cluster.</span><span class="sxs-lookup"><span data-stu-id="b2928-113">The code in the resolution steps assumes that data paths on the new cluster are the same as the data paths on the old cluster.</span></span> <span data-ttu-id="b2928-114">If the data paths are different, you can manually edit the generated alltables.sql file to reflect any changes.</span><span class="sxs-lookup"><span data-stu-id="b2928-114">If the data paths are different, you can manually edit the generated alltables.sql file to reflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="b2928-115">Additional reading</span><span class="sxs-lookup"><span data-stu-id="b2928-115">Additional reading</span></span>

- [<span data-ttu-id="b2928-116">Connect to an HDInsight cluster by using SSH</span><span class="sxs-lookup"><span data-stu-id="b2928-116">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="b2928-117">How do I locate Hive logs on a cluster?</span><span class="sxs-lookup"><span data-stu-id="b2928-117">How do I locate Hive logs on a cluster?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="b2928-118">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="b2928-118">Resolution steps</span></span>

1. <span data-ttu-id="b2928-119">Connect to the HDInsight cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="b2928-119">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="b2928-120">For more information, see **Additional reading**.</span><span class="sxs-lookup"><span data-stu-id="b2928-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="b2928-121">To view Hive client logs, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-121">To view Hive client logs, use the following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="b2928-122">To view Hive metastore logs, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-122">To view Hive metastore logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="b2928-123">To view Hiveserver logs, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-123">To view Hiveserver logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="b2928-124">Additional reading</span><span class="sxs-lookup"><span data-stu-id="b2928-124">Additional reading</span></span>

- [<span data-ttu-id="b2928-125">Connect to an HDInsight cluster by using SSH</span><span class="sxs-lookup"><span data-stu-id="b2928-125">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="b2928-126">How do I launch the Hive shell with specific configurations on a cluster?</span><span class="sxs-lookup"><span data-stu-id="b2928-126">How do I launch the Hive shell with specific configurations on a cluster?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="b2928-127">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="b2928-127">Resolution steps</span></span>

1. <span data-ttu-id="b2928-128">Specify a configuration key-value pair when you start the Hive shell.</span><span class="sxs-lookup"><span data-stu-id="b2928-128">Specify a configuration key-value pair when you start the Hive shell.</span></span> <span data-ttu-id="b2928-129">For more information, see [Additional reading](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="b2928-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="b2928-130">To list all effective configurations on Hive shell, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-130">To list all effective configurations on Hive shell, use the following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="b2928-131">For example, use the following command to start Hive shell with debug logging enabled on the console:</span><span class="sxs-lookup"><span data-stu-id="b2928-131">For example, use the following command to start Hive shell with debug logging enabled on the console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="b2928-132">Additional reading</span><span class="sxs-lookup"><span data-stu-id="b2928-132">Additional reading</span></span>

- [<span data-ttu-id="b2928-133">Hive configuration properties</span><span class="sxs-lookup"><span data-stu-id="b2928-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a><span data-ttu-id="b2928-134">How do I analyze Tez DAG data on a cluster-critical path?</span><span class="sxs-lookup"><span data-stu-id="b2928-134">How do I analyze Tez DAG data on a cluster-critical path?</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="b2928-135">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="b2928-135">Resolution steps</span></span>
 
1. <span data-ttu-id="b2928-136">To analyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect to the HDInsight cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="b2928-136">To analyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="b2928-137">For more information, see [Additional reading](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="b2928-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="b2928-138">At a command prompt, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-138">At a command prompt, run the following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="b2928-139">To list other analyzers that can be used to analyze Tez DAG, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-139">To list other analyzers that can be used to analyze Tez DAG, use the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="b2928-140">You must provide an example program as the first argument.</span><span class="sxs-lookup"><span data-stu-id="b2928-140">You must provide an example program as the first argument.</span></span>

  <span data-ttu-id="b2928-141">Valid program names include:</span><span class="sxs-lookup"><span data-stu-id="b2928-141">Valid program names include:</span></span>
    - <span data-ttu-id="b2928-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="b2928-143">**CriticalPath**: Find the critical path of a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-143">**CriticalPath**: Find the critical path of a DAG</span></span>
    - <span data-ttu-id="b2928-144">**LocalityAnalyzer**: Print locality details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="b2928-145">**ShuffleTimeAnalyzer**: Analyze the shuffle time details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-145">**ShuffleTimeAnalyzer**: Analyze the shuffle time details in a DAG</span></span>
    - <span data-ttu-id="b2928-146">**SkewAnalyzer**: Analyze the skew details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-146">**SkewAnalyzer**: Analyze the skew details in a DAG</span></span>
    - <span data-ttu-id="b2928-147">**SlowNodeAnalyzer**: Print node details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="b2928-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="b2928-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="b2928-150">**SpillAnalyzer**: Print spill details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="b2928-151">**TaskConcurrencyAnalyzer**: Print the task concurrency details in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-151">**TaskConcurrencyAnalyzer**: Print the task concurrency details in a DAG</span></span>
    - <span data-ttu-id="b2928-152">**VertexLevelCriticalPathAnalyzer**: Find the critical path at vertex level in a DAG</span><span class="sxs-lookup"><span data-stu-id="b2928-152">**VertexLevelCriticalPathAnalyzer**: Find the critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="b2928-153">Additional reading</span><span class="sxs-lookup"><span data-stu-id="b2928-153">Additional reading</span></span>

- [<span data-ttu-id="b2928-154">Connect to an HDInsight cluster by using SSH</span><span class="sxs-lookup"><span data-stu-id="b2928-154">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="b2928-155">How do I download Tez DAG data from a cluster?</span><span class="sxs-lookup"><span data-stu-id="b2928-155">How do I download Tez DAG data from a cluster?</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="b2928-156">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="b2928-156">Resolution steps</span></span>

<span data-ttu-id="b2928-157">There are two ways to collect the Tez DAG data:</span><span class="sxs-lookup"><span data-stu-id="b2928-157">There are two ways to collect the Tez DAG data:</span></span>

- <span data-ttu-id="b2928-158">From the command line:</span><span class="sxs-lookup"><span data-stu-id="b2928-158">From the command line:</span></span>
 
    <span data-ttu-id="b2928-159">Connect to the HDInsight cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="b2928-159">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="b2928-160">At the command prompt, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b2928-160">At the command prompt, run the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="b2928-161">Use the Ambari Tez view:</span><span class="sxs-lookup"><span data-stu-id="b2928-161">Use the Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="b2928-162">Go to Ambari.</span><span class="sxs-lookup"><span data-stu-id="b2928-162">Go to Ambari.</span></span> 
  2. <span data-ttu-id="b2928-163">Go to Tez view (under the tiles icon in the upper-right corner).</span><span class="sxs-lookup"><span data-stu-id="b2928-163">Go to Tez view (under the tiles icon in the upper-right corner).</span></span> 
  3. <span data-ttu-id="b2928-164">Select the DAG you want to view.</span><span class="sxs-lookup"><span data-stu-id="b2928-164">Select the DAG you want to view.</span></span>
  4. <span data-ttu-id="b2928-165">Select **Download data**.</span><span class="sxs-lookup"><span data-stu-id="b2928-165">Select **Download data**.</span></span>

### <a name="additional-reading-end"></a><span data-ttu-id="b2928-166">Additional reading</span><span class="sxs-lookup"><span data-stu-id="b2928-166">Additional reading</span></span>

[<span data-ttu-id="b2928-167">Connect to an HDInsight cluster by using SSH</span><span class="sxs-lookup"><span data-stu-id="b2928-167">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


### <a name="see-also"></a><span data-ttu-id="b2928-168">See Also</span><span class="sxs-lookup"><span data-stu-id="b2928-168">See Also</span></span>
[<span data-ttu-id="b2928-169">Troubleshoot by Using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2928-169">Troubleshoot by Using Azure HDInsight</span></span>](hdinsight-troubleshoot-guide.md)




