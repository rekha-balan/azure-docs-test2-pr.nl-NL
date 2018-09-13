---
title: Azure Data Lake Store Spark Performance Tuning Guidelines | Microsoft Docs
description: Azure Data Lake Store Spark Performance Tuning Guidelines
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
ms.openlocfilehash: 2109744fb7ffdfafb7a86bbea355e119718af099
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549276"
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Performance tuning guidance for Spark on HDInsight and Azure Data Lake Store

When tuning performance on Spark, you need to consider the number of apps that will be running on your cluster.  By default, you can run 4 apps concurrently on your HDI cluster (Note: the default setting is subject to change).  You may decide to use fewer apps so you can override the default settings and use more of the cluster for those apps.  

## <a name="prerequisites"></a>Prerequisites

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **An Azure Data Lake Store account**. For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Azure HDInsight cluster** with access to a Data Lake Store account. See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Make sure you enable Remote Desktop for the cluster.
* **Running Spark cluster on Azure Data Lake Store**.  For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Performance tuning guidelines on ADLS**.  For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>Parameters

When running Spark jobs, here are the most important settings that can be tuned to increase performance on ADLS:

* **Num-executors** - The number of concurrent tasks that can be executed.

* **Executor-memory** - The amount of memory allocated to each executor.

* **Executor-cores** - The number of cores allocated to each executor.                     

**Num-executors** Num-executors will set the maximum number of tasks that can run in parallel.  The actual number of tasks that can run in parallel is bounded by the memory and CPU resources available in your cluster.

**Executor-memory** This is the amount of memory that is being allocated to each executor.  The memory needed for each executor is dependent on the job.  For complex operations, the memory needs to be higher.  For simple operations like read and write, memory requirements will be lower.  The amount of memory for each executor can be viewed in Ambari.  In Ambari, navigate to Spark and view the Configs tab.  

**Executor-cores** This sets the amount of cores used per executor, which determines the number of parallel threads that can be run per executor.  For example, if executor-cores = 2, then each executor can run 2 parallel tasks in the executor.  The executor-cores needed will be dependent on the job.  I/O heavy jobs do not require a large amount of memory per task so each executor can handle more parallel tasks.

By default, two virtual YARN cores are defined for each physical core when running Spark on HDInsight.  This number provides a good balance of concurrecy and amount of context switching from multiple threads.  

## <a name="guidance"></a>Guidance

While running Spark analytic workloads to work with data in Data Lake Store, we recommend that you use the most recent HDInsight version to get the best performance with Data Lake Store. When your job is more I/O intensive, then certain parameters can be configured to improve performance.  Azure Data Lake Store is a highly scalable storage platform that can handle high throughput.  If the job mainly consists of read or writes, then increasing concurrency for I/O to and from Azure Data Lake Store could increase performance.

There are a few general ways to increase concurrency for I/O intensive jobs.

**Step 1: Determine how many apps are running on your cluster** – You should know how many apps are running on the cluster including the current one.  The default values for each Spark setting assumes that there are 4 apps running concurrently.  Therefore, you will only have 25% of the cluster available for each app.  To get better performance, you can override the defaults by changing the number of executors.  

**Step 2: Set executor-memory** – the first thing to set is the executor-memory.  The memory will be dependent on the job that you are going to run.  You can increase concurrency by allocating less memory per executor.  If you see out of memory exceptions when you run your job, then you should increase the value for this parameter.  One alternative is to get more memory by using a cluster that has higher amounts of memory or increasing the size of your cluster.  More memory will enable more executors to be used, which means more concurrency.

**Step 3: Set executor-cores** – For I/O intensive workloads that do not have complex operations, it’s good to start with a high number of executor-cores to increase the number of parallel tasks per executor.  Setting executor-cores to 4 is a good start.   

    executor-cores = 4
Increasing the number of executor-cores will give you more parallelism so you can experiment with different executor-cores.  For jobs that have more complex operations, you should reduce the number of cores per executor.  If executor-cores is set higher than 4, then garbage collection may become inefficient and degrade performance.

**Step 4: Determine amount of YARN memory in cluster** – This information is available in Ambari.  Navigate to YARN and view the Configs tab.  The YARN memory is displayed in this window.  
Note: while you are in the window, you can also see the default YARN container size.  The YARN container size is the same as memory per executor paramter.

    Total YARN memory = nodes * YARN memory per node
**Step 5: Calculate num-executors**

**Calculate memory constraint** - The num-executors parameter is constrained either by memory or by CPU.  The memory constraint is determined by the amount of available YARN memory for your application.  You should take total YARN memory and divide that by executor-memory.  The constraint needs to be de-scaled for the number of apps so we divide by the number of apps.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Calculate CPU constraint** - The CPU constraint is calculated as the total virtual cores divided by the number of cores per executor.  There are 2 virtual cores for each physical core.  Similar to the memory constraint, we have divide by the number of apps.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Set num-executors** – The num-executors parameter is determined by taking the minimum of the memory constraint and the CPU constraint. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Setting a higher number of num-executors does not necessarily increase performance.  You should consider that adding more executors will add extra overhead for each additional executor, which can potentially degrade performance.  Num-executors is bounded by the cluster resources.    

## <a name="example-calculation"></a>Example Calculation

Let’s say you currently have a cluster composed of 8 D4v2 nodes that is running 2 apps including the one you are going to run.  

**Step 1: Determine how many apps are running on your cluster** – you know that you have 2 apps on your cluster, including the one you are going to run.  

**Step 2: Set executor-memory** – for this example, we determine that 6GB of executor-memory will be sufficient for I/O intensive job.  

    executor-memory = 6GB
**Step 3: Set executor-cores** – Since this is an I/O intensive job, we can set the number of cores for each executor to 4.  Setting cores per executor to larger than 4 may cause garbage collection problems.  

    executor-cores = 4
**Step 4: Determine amount of YARN memory in cluster** – We navigate to Ambari to find out that each D4v2 has 25GB of YARN memory.  Since there are 8 nodes, the available YARN memory is multiplied by 8.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Step 5: Calculate num-executors** – The num-executors parameter is determined by taking the minimum of the memory constraint and the CPU constraint divided by the # of apps running on Spark.    

**Calculate memory constraint** – The memory constraint is calculated as the total YARN memory divided by the memory per executor.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Calculate CPU constraint** - The CPU constraint is calculated as the total yarn cores divided by the number of cores per executor.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Set num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    
