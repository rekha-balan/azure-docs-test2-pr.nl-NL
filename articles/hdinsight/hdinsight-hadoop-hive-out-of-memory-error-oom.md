---
title: Out of memory error (OOM) - Hive settings | Microsoft Docs
description: Fix an out of memory error (OOM) from a Hive query in Hadoop in HDInsight. The customer scenario is a query across many large tables.
keywords: out of memory error, OOM, Hive settings
services: hdinsight
documentationcenter: ''
author: rashimg
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/22/2017
ms.author: rashimg;jgao
ms.openlocfilehash: 2008848db0513e431e22c06b7dac3c786ae984d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671628"
---
# <a name="fix-an-out-of-memory-oom-error-with-hive-memory-settings-in-hadoop-in-azure-hdinsight"></a><span data-ttu-id="e4460-105">Fix an Out of Memory (OOM) error with Hive memory settings in Hadoop in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4460-105">Fix an Out of Memory (OOM) error with Hive memory settings in Hadoop in Azure HDInsight</span></span>
<span data-ttu-id="e4460-106">One of the common problems our customers face is getting an Out of Memory (OOM) error when using Hive.</span><span class="sxs-lookup"><span data-stu-id="e4460-106">One of the common problems our customers face is getting an Out of Memory (OOM) error when using Hive.</span></span> <span data-ttu-id="e4460-107">This article describes a customer scenario and the Hive settings we recommended to fix the issue.</span><span class="sxs-lookup"><span data-stu-id="e4460-107">This article describes a customer scenario and the Hive settings we recommended to fix the issue.</span></span>

## <a name="scenario-hive-query-across-large-tables"></a><span data-ttu-id="e4460-108">Scenario: Hive query across large tables</span><span class="sxs-lookup"><span data-stu-id="e4460-108">Scenario: Hive query across large tables</span></span>
<span data-ttu-id="e4460-109">A customer ran the query below using Hive.</span><span class="sxs-lookup"><span data-stu-id="e4460-109">A customer ran the query below using Hive.</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="e4460-110">Some nuances of this query:</span><span class="sxs-lookup"><span data-stu-id="e4460-110">Some nuances of this query:</span></span>

* <span data-ttu-id="e4460-111">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span><span class="sxs-lookup"><span data-stu-id="e4460-111">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="e4460-112">Other tables are not that big but do have a large number of columns.</span><span class="sxs-lookup"><span data-stu-id="e4460-112">Other tables are not that big but do have a large number of columns.</span></span>
* <span data-ttu-id="e4460-113">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span><span class="sxs-lookup"><span data-stu-id="e4460-113">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="e4460-114">When the customer ran the query using Hive on MapReduce on a 24 node A3 cluster, the query ran in about 26 minutes.</span><span class="sxs-lookup"><span data-stu-id="e4460-114">When the customer ran the query using Hive on MapReduce on a 24 node A3 cluster, the query ran in about 26 minutes.</span></span> <span data-ttu-id="e4460-115">The customer noticed the following warning messages when the query was run using Hive on MapReduce:</span><span class="sxs-lookup"><span data-stu-id="e4460-115">The customer noticed the following warning messages when the query was run using Hive on MapReduce:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="e4460-116">Because the query finished executing in about 26 minutes, the customer ignored these warnings and instead started to focus on how to improve the this query’s performance further.</span><span class="sxs-lookup"><span data-stu-id="e4460-116">Because the query finished executing in about 26 minutes, the customer ignored these warnings and instead started to focus on how to improve the this query’s performance further.</span></span>

<span data-ttu-id="e4460-117">The customer consulted [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md), and decided to use Tez execution engine.</span><span class="sxs-lookup"><span data-stu-id="e4460-117">The customer consulted [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md), and decided to use Tez execution engine.</span></span> <span data-ttu-id="e4460-118">Once the same query was run with the Tez setting enabled the query ran for 15 minutes, and then threw the following error:</span><span class="sxs-lookup"><span data-stu-id="e4460-118">Once the same query was run with the Tez setting enabled the query ran for 15 minutes, and then threw the following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="e4460-119">The customer then decided to use a bigger VM (i.e. D12) thinking a bigger VM would have more heap space.</span><span class="sxs-lookup"><span data-stu-id="e4460-119">The customer then decided to use a bigger VM (i.e. D12) thinking a bigger VM would have more heap space.</span></span> <span data-ttu-id="e4460-120">Even then, the customer continued to see the error.</span><span class="sxs-lookup"><span data-stu-id="e4460-120">Even then, the customer continued to see the error.</span></span> <span data-ttu-id="e4460-121">The customer reached out to the HDInsight team for help in debugging this issue.</span><span class="sxs-lookup"><span data-stu-id="e4460-121">The customer reached out to the HDInsight team for help in debugging this issue.</span></span>

## <a name="debug-the-out-of-memory-oom-error"></a><span data-ttu-id="e4460-122">Debug the Out of Memory (OOM) error</span><span class="sxs-lookup"><span data-stu-id="e4460-122">Debug the Out of Memory (OOM) error</span></span>
<span data-ttu-id="e4460-123">Our support and engineering teams together found one of the issues causing the Out of Memory (OOM) error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306).</span><span class="sxs-lookup"><span data-stu-id="e4460-123">Our support and engineering teams together found one of the issues causing the Out of Memory (OOM) error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306).</span></span> <span data-ttu-id="e4460-124">From the description in the JIRA:</span><span class="sxs-lookup"><span data-stu-id="e4460-124">From the description in the JIRA:</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="e4460-125">We confirmed that **hive.auto.convert.join.noconditionaltask** was indeed set to **true** by looking under hive-site.xml file:</span><span class="sxs-lookup"><span data-stu-id="e4460-125">We confirmed that **hive.auto.convert.join.noconditionaltask** was indeed set to **true** by looking under hive-site.xml file:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="e4460-126">Based on the warning and the JIRA, our hypothesis was Map Join was the cause of the Java Heap Space OOM error.</span><span class="sxs-lookup"><span data-stu-id="e4460-126">Based on the warning and the JIRA, our hypothesis was Map Join was the cause of the Java Heap Space OOM error.</span></span> <span data-ttu-id="e4460-127">So we dug deeper into this issue.</span><span class="sxs-lookup"><span data-stu-id="e4460-127">So we dug deeper into this issue.</span></span>

<span data-ttu-id="e4460-128">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span><span class="sxs-lookup"><span data-stu-id="e4460-128">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="e4460-129">See the image below describing the Tez container memory.</span><span class="sxs-lookup"><span data-stu-id="e4460-129">See the image below describing the Tez container memory.</span></span>

![Tez container memory diagram: Hive out of memory error  OOM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="e4460-131">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="e4460-131">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="e4460-132">From our experience, the OOM exception does not mean the container size is too small.</span><span class="sxs-lookup"><span data-stu-id="e4460-132">From our experience, the OOM exception does not mean the container size is too small.</span></span> <span data-ttu-id="e4460-133">It means the Java heap size (hive.tez.java.opts) is too small.</span><span class="sxs-lookup"><span data-stu-id="e4460-133">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="e4460-134">So whenever you see OOM, you can try to increase **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="e4460-134">So whenever you see OOM, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="e4460-135">If needed you might have to increase **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="e4460-135">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="e4460-136">The **java.opts** setting should be around 80% of **container.size**.</span><span class="sxs-lookup"><span data-stu-id="e4460-136">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="e4460-137">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="e4460-137">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="e4460-138">Since a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts.</span><span class="sxs-lookup"><span data-stu-id="e4460-138">Since a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts.</span></span> <span data-ttu-id="e4460-139">This was done on the Hive console using the setting below:</span><span class="sxs-lookup"><span data-stu-id="e4460-139">This was done on the Hive console using the setting below:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="e4460-140">Based on these settings, the query successfully ran in under ten minutes.</span><span class="sxs-lookup"><span data-stu-id="e4460-140">Based on these settings, the query successfully ran in under ten minutes.</span></span>

## <a name="conclusion-oom-errors-and-container-size"></a><span data-ttu-id="e4460-141">Conclusion: OOM errors and container size</span><span class="sxs-lookup"><span data-stu-id="e4460-141">Conclusion: OOM errors and container size</span></span>
<span data-ttu-id="e4460-142">Getting an OOM error doesn't necessarily mean the container size is too small.</span><span class="sxs-lookup"><span data-stu-id="e4460-142">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="e4460-143">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span><span class="sxs-lookup"><span data-stu-id="e4460-143">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span>


