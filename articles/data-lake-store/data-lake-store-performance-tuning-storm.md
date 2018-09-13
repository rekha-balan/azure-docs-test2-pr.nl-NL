---
title: Azure Data Lake Store Storm performance tuning guidelines | Microsoft Docs
description: Azure Data Lake Store Storm performance tuning guidelines
services: data-lake-store
documentationcenter: ''
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 1dfa93643f45a96ded3fd022aa8b1c71d487acb4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669458"
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Performance tuning guidance for Storm on HDInsight and Azure Data Lake Store

Understand the factors that should be considered when you tune the performance of an Azure Storm topology. For example, it's important to understand the characteristics of the work done by the spouts and the bolts (whether the work is I/O or memory intensive). This article covers a range of performance tuning guidelines, including troubleshooting common issues.

## <a name="prerequisites"></a>Prerequisites

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **An Azure Data Lake Store account**. For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **An Azure HDInsight cluster** with access to a Data Lake Store account. See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Make sure you enable Remote Desktop for the cluster.
* **Running a Storm cluster on Data Lake Store**. For more information, see [Storm on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Performance tuning guidelines on Data Lake Store**.  For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-the-parallelism-of-the-topology"></a>Tune the parallelism of the topology

You might be able to improve performance by increasing the concurrency of the I/O to and from Data Lake Store. A Storm topology has a set of configurations that determine the parallelism:
* Number of worker processes (the workers are evenly distributed across the VMs).
* Number of spout executor instances.
* Number of bolt executor instances.
* Number of spout tasks.
* Number of bolt tasks.

For example, on a cluster with 4 VMs and 4 worker processes, 32 spout executors and 32 spout tasks, and 256 bolt executors and 512 bolt tasks, consider the following:

Each supervisor, which is a worker node, has a single worker Java virtual machine (JVM) process. This JVM process manages 4 spout threads and 64 bolt threads. Within each thread, tasks are run sequentially. With the preceding configuration, each spout thread has 1 task, and each bolt thread has 2 tasks.

In Storm, here are the various components involved, and how they affect the level of parallelism you have:
* The head node (called Nimbus in Storm) is used to submit and manage jobs. These nodes have no impact on the degree of parallelism.
* The supervisor nodes. In HDInsight, this corresponds to a worker node Azure VM.
* The worker tasks are Storm processes running in the VMs. Each worker task corresponds to a JVM instance. Storm distributes the number of worker processes you specify to the worker nodes as evenly as possible.
* Spout and bolt executor instances. Each executor instance corresponds to a thread running within the workers (JVMs).
* Storm tasks. These are logical tasks that each of these threads run. This does not change the level of parallelism, so you should evaluate if you need multiple tasks per executor or not.

### <a name="get-the-best-performance-from-data-lake-store"></a>Get the best performance from Data Lake Store

When working with Data Lake Store, you get the best performance if you do the following:
* Coalesce your small appends into larger sizes (ideally 4 MB).
* Do as many concurrent requests as you can. Because each bolt thread is doing blocking reads, you want to have somewhere in the range of 8-12 threads per core. This keeps the NIC and the CPU well utilized. A larger VM enables more concurrent requests.  

### <a name="example-topology"></a>Example topology

Let’s assume you have an 8 worker node cluster with a D13v2 Azure VM. This VM has 8 cores, so among the 8 worker nodes, you have 64 total cores.

Let’s say we do 8 bolt threads per core. Given 64 cores, that means we want 512 total bolt executor instances (that is, threads). In this case, let’s say we start with one JVM per VM, and mainly use the thread concurrency within the JVM to achieve concurrency. That means we need 8 worker tasks (one per Azure VM), and 512 bolt executors. Given this configuration, Storm tries to distribute the workers evenly across worker nodes (also known as supervisor nodes), giving each worker node 1 JVM. Now within the supervisors, Storm tries to distribute the executors evenly between supervisors, giving each supervisor (that is, JVM) 8 threads each.

## <a name="tune-additional-parameters"></a>Tune additional parameters
After you have the basic topology, you can consider whether you want to tweak any of the parameters:
* **Number of JVMs per worker node.** If you have a large data structure (for example, a lookup table) that you host in memory, each JVM requires a separate copy. Alternatively, you can use the data structure across many threads if you have fewer JVMs. For the bolt’s I/O, the number of JVMs does not make as much of a difference as the number of threads added across those JVMs. For simplicity, it's a good idea to have one JVM per worker. Depending on what your bolt is doing or what application processing you require, though, you may need to change this number.
* **Number of spout executors.** Because the preceding example uses bolts for writing to Data Lake Store, the number of spouts is not directly relevant to the bolt performance. However, depending on the amount of processing or I/O happening in the spout, it's a good idea to tune the spouts for best performance. Ensure that you have enough spouts to be able to keep the bolts busy. The output rates of the spouts should match the throughput of the bolts. The actual configuration depends on the spout.
* **Number of tasks.** Each bolt runs as a single thread. Additional tasks per bolt don't provide any additional concurrency. The only time they are of benefit is if your process of acknowledging the tuple takes a large proportion of your bolt execution time. It's a good idea to group many tuples into a larger append before you send an acknowledgement from the bolt. So, in most cases, multiple tasks provide no additional benefit.
* **Local or shuffle grouping.** When this setting is enabled, tuples are sent to bolts within the same worker process. This reduces inter-process communication and network calls. This is recommended for most topologies.

This basic scenario is a good starting point. Test with your own data to tweak the preceding parameters to achieve optimal performance.

## <a name="tune-the-spout"></a>Tune the spout

You can modify the following settings to tune the spout.

- **Tuple timeout: topology.message.timeout.secs**. This setting determines the amount of time a message takes to complete, and receive acknowledgement, before it is considered failed.

- **Max memory per worker process: worker.childopts**. This setting lets you specify additional command-line parameters to the Java workers. The most commonly used setting here is XmX, which determines the maximum memory allocated to a JVM’s heap.

- **Max spout pending: topology.max.spout.pending**. This setting determines the number of tuples that can in be flight (not yet acknowledged at all nodes in the topology) per spout thread at any time.

 A good calculation to do is to estimate the size of each of your tuples. Then figure out how much memory one spout thread has. The total memory allocated to a thread, divided by this value, should give you the upper bound for the max spout pending parameter.

## <a name="tune-the-bolt"></a>Tune the bolt
When you're writing to Data Lake Store, set a size sync policy (buffer on the client side) to 4 MB. A flushing or hsync() is then performed only when the buffer size is the at this value. The Data Lake Store driver on the worker VM automatically does this buffering, unless you explicitly perform an hsync().

The default Data Lake Store Storm bolt has a size sync policy parameter (fileBufferSize) that can be used to tune this parameter.

In I/O-intensive topologies, it's a good idea to have each bolt thread write to its own file, and to set a file rotation policy (fileRotationSize). When the file reaches a certain size, the stream is automatically flushed and a new file is written to. The recommended file size for rotation is 1 GB.

### <a name="handle-tuple-data"></a>Handle tuple data

In Storm, a spout holds on to a tuple until it is explicitly acknowledged by the bolt. If a tuple has been read by the bolt but has not been acknowledged yet, the spout might not have persisted into Data Lake Store back end. After a tuple is acknowledged, the spout can be guaranteed persistence by the bolt, and can then delete the source data from whatever source it is reading from.  

For best performance on Data Lake Store, have the bolt buffer 4 MB of tuple data. Then write to the Data Lake Store back end as one 4-MB write. After the data has been successfully written to the store (by calling hflush()), the bolt can acknowledge the data back to the spout. This is what the example bolt supplied here does. It is also acceptable to hold a larger number of tuples before the hflush() call is made and the tuples acknowledged. However, this increases the number of tuples in flight that the spout needs to hold, and therefore increases the amount of memory required per JVM.

> [!NOTE]
Applications might have a requirement to acknowledge tuples more frequently (at data sizes less than 4 MB) for other non-performance reasons. However, that might affect the I/O throughput to the storage back end. Carefully weigh this tradeoff against the bolt’s I/O performance.

If the incoming rate of tuples is not high, so the 4-MB buffer takes a long time to fill, consider mitigating this by:
* Reducing the number of bolts, so there are fewer buffers to fill.
* Having a time-based or count-based policy, where an hflush() is triggered every x flushes or every y milliseconds, and the tuples accumulated so far are acknowledged back.

Note that the throughput in this case is lower, but with a slow rate of events, maximum throughput is not the biggest objective anyway. These mitigations help you reduce the total time that it takes for a tuple to flow through to the store. This might matter if you want a real-time pipeline even with a low event rate. Also note that if your incoming tuple rate is low, you should adjust the topology.message.timeout_secs parameter, so the tuples don’t time out while they are getting buffered or processed.

## <a name="monitor-your-topology-in-storm"></a>Monitor your topology in Storm  
While your topology is running, you can monitor it in the Storm user interface. Here are the main parameters to look at:

* **Total process execution latency.** This is the average time one tuple takes to be emitted by the spout, processed by the bolt, and acknowledged.

* **Total bolt process latency.** This is the average time spent by the tuple at the bolt until it receives an acknowledgement.

* **Total bolt execute latency.** This is the average time spent by the bolt in the execute method.

* **Number of failures.** This refers to the number of tuples that failed to be fully processed before they timed out.

* **Capacity.** This is a measure of how busy your system is. If this number is 1, your bolts are working as fast as they can. If it is less than 1, increase the parallelism. If it is greater than 1, reduce the parallelism.

## <a name="troubleshoot-common-problems"></a>Troubleshoot common problems
Here are a few common troubleshooting scenarios.
* **Many tuples are timing out.** Look at each node in the topology to determine where the bottleneck is. The most common reason for this is that the bolts are not able to keep up with the spouts. This leads to tuples clogging the internal buffers while waiting to be processed. Consider increasing the timeout value or decreasing the max spout pending.

* **There is a high total process execution latency, but a low bolt process latency.** In this case, it is possible that the tuples are not being acknowledged fast enough. Check that there are a sufficient number of acknowledgers. Another possibility is that they are waiting in the queue for too long before the bolts start processing them. Decrease the max spout pending.

* **There is a high bolt execute latency.** This means that the execute() method of your bolt is taking too long. Optimize the code, or look at write sizes and flush behavior.

### <a name="data-lake-store-throttling"></a>Data Lake Store throttling
If you hit the limits of bandwidth provided by Data Lake Store, you might see task failures. Check task logs for throttling errors. You can decrease the parallelism by increasing container size.    

To check if you are getting throttled, enable the debug logging on the client side:

1. In **Ambari** > **Storm** > **Config** > **Advanced storm-worker-log4j**, change **&lt;root level="info"&gt;** to **&lt;root level=”debug”&gt;**. Restart all the nodes/service for the configuration to take effect.
2. Monitor the Storm topology logs on worker nodes (under /var/log/storm/worker-artifacts/&lt;TopologyName&gt;/&lt;port&gt;/worker.log) for Data Lake Store throttling exceptions.

## <a name="next-steps"></a>Next steps
Additional performance tuning for Storm can be referenced in [this blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

For an additional example to run, see [this one on GitHub](https://github.com/hdinsight/storm-performance-automation).