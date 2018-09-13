---
title: Use DataFu with Pig on HDInsight
description: DataFu is a collection of libraries for use with Hadoop. Learn how you can use DataFu with Pig on your HDInsight cluster.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/08/2017
ms.author: larryfr
ms.openlocfilehash: ca390e1e93660eb27c08d1fce0574c6e3646a329
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549805"
---
# <a name="use-datafu-with-pig-on-hdinsight"></a><span data-ttu-id="ae0e4-104">Use DataFu with pig on HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae0e4-104">Use DataFu with pig on HDInsight</span></span>

<span data-ttu-id="ae0e4-105">DataFu is a collection of Open Source libraries for use with Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-105">DataFu is a collection of Open Source libraries for use with Hadoop.</span></span> <span data-ttu-id="ae0e4-106">In this document, you learn how to use DataFu on your HDInsight cluster, and how to use DataFu User Defined Functions (UDF) with Pig.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-106">In this document, you learn how to use DataFu on your HDInsight cluster, and how to use DataFu User Defined Functions (UDF) with Pig.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae0e4-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae0e4-107">Prerequisites</span></span>

* <span data-ttu-id="ae0e4-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-108">An Azure subscription.</span></span>

* <span data-ttu-id="ae0e4-109">An Azure HDInsight cluster (Linux or Windows based)</span><span class="sxs-lookup"><span data-stu-id="ae0e4-109">An Azure HDInsight cluster (Linux or Windows based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ae0e4-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae0e4-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="ae0e4-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="ae0e4-112">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span><span class="sxs-lookup"><span data-stu-id="ae0e4-112">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span></span>

## <a name="install-datafu-on-linux-based-hdinsight"></a><span data-ttu-id="ae0e4-113">Install DataFu on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae0e4-113">Install DataFu on Linux-based HDInsight</span></span>

> [!NOTE]
> <span data-ttu-id="ae0e4-114">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-114">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span></span> <span data-ttu-id="ae0e4-115">It is not installed on Linux-based clusters earlier than 3.3.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-115">It is not installed on Linux-based clusters earlier than 3.3.</span></span>
>
> <span data-ttu-id="ae0e4-116">If you are using a Linux-based cluster version 3.3 or higher, or a Windows-based cluster, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-116">If you are using a Linux-based cluster version 3.3 or higher, or a Windows-based cluster, you can skip this section.</span></span>

<span data-ttu-id="ae0e4-117">DataFu can be downloaded and installed from the Maven repository.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-117">DataFu can be downloaded and installed from the Maven repository.</span></span> <span data-ttu-id="ae0e4-118">Use the following steps to add DataFu to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="ae0e4-118">Use the following steps to add DataFu to your HDInsight cluster:</span></span>

1. <span data-ttu-id="ae0e4-119">Connect to your Linux-based HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-119">Connect to your Linux-based HDInsight cluster using SSH.</span></span> <span data-ttu-id="ae0e4-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ae0e4-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ae0e4-121">Use the following command to download the DataFu jar file using the wget utility, or copy and paste the link into your browser to begin the download.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-121">Use the following command to download the DataFu jar file using the wget utility, or copy and paste the link into your browser to begin the download.</span></span>

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. <span data-ttu-id="ae0e4-122">Next, upload the file to default storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-122">Next, upload the file to default storage for your HDInsight cluster.</span></span> <span data-ttu-id="ae0e4-123">This makes the file available to all nodes in the cluster, and the file stays in storage even if you delete and recreate the cluster.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-123">This makes the file available to all nodes in the cluster, and the file stays in storage even if you delete and recreate the cluster.</span></span>

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > <span data-ttu-id="ae0e4-124">The above example stores the jar in `/example/jars` since this directory already exists on the cluster storage.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-124">The above example stores the jar in `/example/jars` since this directory already exists on the cluster storage.</span></span> <span data-ttu-id="ae0e4-125">You can use any location you wish on HDInsight cluster storage.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-125">You can use any location you wish on HDInsight cluster storage.</span></span>

## <a name="use-datafu-with-pig"></a><span data-ttu-id="ae0e4-126">Use DataFu With Pig</span><span class="sxs-lookup"><span data-stu-id="ae0e4-126">Use DataFu With Pig</span></span>

<span data-ttu-id="ae0e4-127">The steps in this section assume that you are familiar with using Pig on HDInsight, and only provide the Pig Latin statements, not the steps on how to use them with the cluster.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-127">The steps in this section assume that you are familiar with using Pig on HDInsight, and only provide the Pig Latin statements, not the steps on how to use them with the cluster.</span></span> <span data-ttu-id="ae0e4-128">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="ae0e4-128">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae0e4-129">When using DataFu from Pig on a Linux-based HDInsight cluster, you must first register the jar file.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-129">When using DataFu from Pig on a Linux-based HDInsight cluster, you must first register the jar file.</span></span>
>
> <span data-ttu-id="ae0e4-130">If your cluster usese Azure Storage, you must use a `wasb://` path.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-130">If your cluster usese Azure Storage, you must use a `wasb://` path.</span></span> <span data-ttu-id="ae0e4-131">For example, `register wasb:///example/jars/datafu-1.2.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-131">For example, `register wasb:///example/jars/datafu-1.2.0.jar`.</span></span>
>
> <span data-ttu-id="ae0e4-132">If your cluster uses Azure Data Lake Store, you must use an `adl://` path.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-132">If your cluster uses Azure Data Lake Store, you must use an `adl://` path.</span></span> <span data-ttu-id="ae0e4-133">For example, `register adl://home/example/jars/datafu-1.2.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-133">For example, `register adl://home/example/jars/datafu-1.2.0.jar`.</span></span>
>
> <span data-ttu-id="ae0e4-134">DataFu is registered by default on Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-134">DataFu is registered by default on Windows-based HDInsight clusters.</span></span>

<span data-ttu-id="ae0e4-135">You often define an alias for DataFu functions.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-135">You often define an alias for DataFu functions.</span></span> <span data-ttu-id="ae0e4-136">For example:</span><span class="sxs-lookup"><span data-stu-id="ae0e4-136">For example:</span></span>

    DEFINE SHA datafu.pig.hash.SHA();

<span data-ttu-id="ae0e4-137">This defines an alias named `SHA` for the SHA hashing function.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-137">This defines an alias named `SHA` for the SHA hashing function.</span></span> <span data-ttu-id="ae0e4-138">You can then use this in a Pig Latin script to generate a hash for the input data.</span><span class="sxs-lookup"><span data-stu-id="ae0e4-138">You can then use this in a Pig Latin script to generate a hash for the input data.</span></span> <span data-ttu-id="ae0e4-139">For example, the following replaces the names in the input data with a hash value:</span><span class="sxs-lookup"><span data-stu-id="ae0e4-139">For example, the following replaces the names in the input data with a hash value:</span></span>

    raw = LOAD '/data/raw/' USING PigStorage(',') AS  
        (name:chararray,
        int1:int,
        int2:int,
        int3:int);
    mask = FOREACH raw GENERATE SHA(name), int1, int2, int3;
    DUMP mask;

<span data-ttu-id="ae0e4-140">If this is used with the following input data:</span><span class="sxs-lookup"><span data-stu-id="ae0e4-140">If this is used with the following input data:</span></span>

    Lana Zemljaric,5,9,1
    Qiong Zhong,9,3,6
    Sandor Harsanyi,0,7,3
    Roko Petkovic,2,6,2
    Tibor Rozsa,8,0,0
    Lea Hrastovsek,6,3,6
    Regina Toth,2,1,2
    Eva Makay,8,9,2
    Shi Liao,4,6,0
    Tjasa Zemljaric,0,2,5

<span data-ttu-id="ae0e4-141">It generates the following output:</span><span class="sxs-lookup"><span data-stu-id="ae0e4-141">It generates the following output:</span></span>

    (c1a743b0f34d349cfc2ce00ef98369bdc3dba1565fec92b4159a9cd5de186347,5,9,1)
    (713d030d621ab69aa3737c8ea37a2c7c724a01cd0657a370e103d8cdecac6f99,9,3,6)
    (7a5f5abdd281f68168199319d98a1a662535f988d1443b3a3c497010937bac89,0,7,3)
    (a94818e93807e12079c4b35f8f3c8c8ef8e8acd1954e7f0476bc1a3a86fc96a9,2,6,2)
    (894ead4f48af91df7e088241218a23157bede7c52115272e417e95c046d48902,8,0,0)
    (6f99f163af3448fda672087db306f363e27a98a9e49c1f274a0860e303f8aec4,6,3,6)
    (a03de92a28be3c6a984c7a153fa9ed81c0413f76a9401955b5f7e04a5dd0ab9f,2,1,2)
    (6ceab977c8fb48d9ad0dc413e6bc646cabd89f22e7ab97a6b0133f3d225c6013,8,9,2)
    (fa9c436469096ff1bd297e182831f460501b826272ae97e921f5f6e3f54747e8,4,6,0)
    (bc22db7c238b86c37af79a62c78f61a304b35143f6087eb99c34040325865654,0,2,5)

## <a name="next-steps"></a><span data-ttu-id="ae0e4-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae0e4-142">Next steps</span></span>

<span data-ttu-id="ae0e4-143">For more information on DataFu or Pig, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="ae0e4-143">For more information on DataFu or Pig, see the following documents:</span></span>

* <span data-ttu-id="ae0e4-144">[Apache DataFu Pig Guide](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span><span class="sxs-lookup"><span data-stu-id="ae0e4-144">[Apache DataFu Pig Guide](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span></span>
* [<span data-ttu-id="ae0e4-145">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae0e4-145">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
