---
title: Use Apache DataFu with Pig on HDInsight - Azure
description: Apache DataFu Pig is a collection of libraries for use with Pig on Hadoop. Learn how you can use DataFu with Pig on your HDInsight cluster.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/16/2018
ms.author: jasonh
ms.openlocfilehash: 3d276de1910289e1f79d07c111eee1ac33e247ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857278"
---
# <a name="use-apache-datafu-pig-with-pig-on-hdinsight"></a><span data-ttu-id="7c4b5-104">Use Apache DataFu Pig with pig on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c4b5-104">Use Apache DataFu Pig with pig on HDInsight</span></span>

<span data-ttu-id="7c4b5-105">Learn how to use Apache DataFu Pig with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-105">Learn how to use Apache DataFu Pig with HDInsight.</span></span>

<span data-ttu-id="7c4b5-106">DataFu Pig is a collection of Open Source libraries for use with Pig on Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-106">DataFu Pig is a collection of Open Source libraries for use with Pig on Hadoop.</span></span>
<span data-ttu-id="7c4b5-107">For more information on DataFu Pig, see [https://datafu.apache.org/](https://datafu.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="7c4b5-107">For more information on DataFu Pig, see [https://datafu.apache.org/](https://datafu.apache.org/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c4b5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c4b5-108">Prerequisites</span></span>

* <span data-ttu-id="7c4b5-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-109">An Azure subscription.</span></span>

* <span data-ttu-id="7c4b5-110">An Azure HDInsight cluster (Linux or Windows based)</span><span class="sxs-lookup"><span data-stu-id="7c4b5-110">An Azure HDInsight cluster (Linux or Windows based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7c4b5-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7c4b5-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7c4b5-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7c4b5-113">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span><span class="sxs-lookup"><span data-stu-id="7c4b5-113">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span></span>

## <a name="install-datafu-on-linux-based-hdinsight"></a><span data-ttu-id="7c4b5-114">Install DataFu on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c4b5-114">Install DataFu on Linux-based HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c4b5-115">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-115">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span></span> <span data-ttu-id="7c4b5-116">It is not installed on Linux-based clusters earlier than 3.3.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-116">It is not installed on Linux-based clusters earlier than 3.3.</span></span>
>
> <span data-ttu-id="7c4b5-117">If you are using a Windows-based cluster, or a Linux-based cluster higher than version 3.3, skip this section.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-117">If you are using a Windows-based cluster, or a Linux-based cluster higher than version 3.3, skip this section.</span></span>

<span data-ttu-id="7c4b5-118">DataFu can be downloaded and installed from the Maven repository.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-118">DataFu can be downloaded and installed from the Maven repository.</span></span> <span data-ttu-id="7c4b5-119">Use the following steps to find version you need and add it to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="7c4b5-119">Use the following steps to find version you need and add it to your HDInsight cluster:</span></span>

> [!WARNING]
> <span data-ttu-id="7c4b5-120">DataFu versions may have requirements that are not met by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-120">DataFu versions may have requirements that are not met by HDInsight.</span></span> <span data-ttu-id="7c4b5-121">For example, if you use an older version of DataFu, it may require an different version of Pig than what is included in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-121">For example, if you use an older version of DataFu, it may require an different version of Pig than what is included in HDInsight.</span></span>

### <a name="find-a-version"></a><span data-ttu-id="7c4b5-122">Find a version</span><span class="sxs-lookup"><span data-stu-id="7c4b5-122">Find a version</span></span>

1. <span data-ttu-id="7c4b5-123">In your web browser, navigate to https://mvnrepository.com/artifact/org.apache.datafu/datafu-pig and find the version you need.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-123">In your web browser, navigate to https://mvnrepository.com/artifact/org.apache.datafu/datafu-pig and find the version you need.</span></span>

2. <span data-ttu-id="7c4b5-124">Select the linked version number.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-124">Select the linked version number.</span></span>

3. <span data-ttu-id="7c4b5-125">Select __View all__ to view all the files.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-125">Select __View all__ to view all the files.</span></span>

4. <span data-ttu-id="7c4b5-126">In the list of files, find the .jar file.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-126">In the list of files, find the .jar file.</span></span> <span data-ttu-id="7c4b5-127">Usually this file is the largest one listed, as it includes all dependencies.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-127">Usually this file is the largest one listed, as it includes all dependencies.</span></span> <span data-ttu-id="7c4b5-128">Right-click the link and copy the link address.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-128">Right-click the link and copy the link address.</span></span>

### <a name="download-datafu-to-hdinsight"></a><span data-ttu-id="7c4b5-129">Download DataFu to HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c4b5-129">Download DataFu to HDInsight</span></span>

1. <span data-ttu-id="7c4b5-130">Connect to your Linux-based HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-130">Connect to your Linux-based HDInsight cluster using SSH.</span></span> <span data-ttu-id="7c4b5-131">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7c4b5-131">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="7c4b5-132">Use the following command to download the DataFu jar file using the wget utility:</span><span class="sxs-lookup"><span data-stu-id="7c4b5-132">Use the following command to download the DataFu jar file using the wget utility:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7c4b5-133">Replace the link in the command with the URL you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-133">Replace the link in the command with the URL you copied earlier.</span></span>

    ```
    wget http://central.maven.org/maven2/org/apache/datafu/datafu-pig/1.4.0/datafu-pig-1.4.0.jar
    ```

3. <span data-ttu-id="7c4b5-134">Next, upload the file to default storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-134">Next, upload the file to default storage for your HDInsight cluster.</span></span> <span data-ttu-id="7c4b5-135">Placing the file in default storage makes it available to all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-135">Placing the file in default storage makes it available to all nodes in the cluster.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7c4b5-136">Replace the version number in the file name with the version you downloaded.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-136">Replace the version number in the file name with the version you downloaded.</span></span>

    ```
    hdfs dfs -put datafu-pig-1.4.0.jar /example/jars
    ```

    > [!NOTE]
    > <span data-ttu-id="7c4b5-137">The previous command stores the jar in `/example/jars` since this directory already exists on the cluster storage.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-137">The previous command stores the jar in `/example/jars` since this directory already exists on the cluster storage.</span></span> <span data-ttu-id="7c4b5-138">You can use any location you wish on HDInsight cluster storage.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-138">You can use any location you wish on HDInsight cluster storage.</span></span>

## <a name="use-datafu-with-pig"></a><span data-ttu-id="7c4b5-139">Use DataFu With Pig</span><span class="sxs-lookup"><span data-stu-id="7c4b5-139">Use DataFu With Pig</span></span>

<span data-ttu-id="7c4b5-140">The steps in this section assume that you are familiar with using Pig on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-140">The steps in this section assume that you are familiar with using Pig on HDInsight.</span></span> <span data-ttu-id="7c4b5-141">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="7c4b5-141">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c4b5-142">If you manually installed DataFu using the steps in the previous section, you must register it before using it.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-142">If you manually installed DataFu using the steps in the previous section, you must register it before using it.</span></span>
>
> * <span data-ttu-id="7c4b5-143">If your cluster uses Azure Storage, use a `wasb://` path.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-143">If your cluster uses Azure Storage, use a `wasb://` path.</span></span> <span data-ttu-id="7c4b5-144">For example, `register wasb:///example/jars/datafu-pig-1.4.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-144">For example, `register wasb:///example/jars/datafu-pig-1.4.0.jar`.</span></span>
>
> * <span data-ttu-id="7c4b5-145">If your cluster uses Azure Data Lake Store, use an `adl://` path.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-145">If your cluster uses Azure Data Lake Store, use an `adl://` path.</span></span> <span data-ttu-id="7c4b5-146">For example, `register adl://home/example/jars/datafu-pig-1.4.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-146">For example, `register adl://home/example/jars/datafu-pig-1.4.0.jar`.</span></span>

<span data-ttu-id="7c4b5-147">You often define an alias for DataFu functions.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-147">You often define an alias for DataFu functions.</span></span> <span data-ttu-id="7c4b5-148">The following example defines an alias of `SHA`:</span><span class="sxs-lookup"><span data-stu-id="7c4b5-148">The following example defines an alias of `SHA`:</span></span>

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

<span data-ttu-id="7c4b5-149">You can then use this alias in a Pig Latin script to generate a hash for the input data.</span><span class="sxs-lookup"><span data-stu-id="7c4b5-149">You can then use this alias in a Pig Latin script to generate a hash for the input data.</span></span> <span data-ttu-id="7c4b5-150">For example, the following code replaces the location in the input data with a hash value:</span><span class="sxs-lookup"><span data-stu-id="7c4b5-150">For example, the following code replaces the location in the input data with a hash value:</span></span>

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

<span data-ttu-id="7c4b5-151">It generates the following output:</span><span class="sxs-lookup"><span data-stu-id="7c4b5-151">It generates the following output:</span></span>

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a><span data-ttu-id="7c4b5-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c4b5-152">Next steps</span></span>

<span data-ttu-id="7c4b5-153">For more information on DataFu or Pig, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="7c4b5-153">For more information on DataFu or Pig, see the following documents:</span></span>

* <span data-ttu-id="7c4b5-154">[Apache DataFu Pig Getting Started](https://datafu.apache.org/docs/datafu/getting-started.html).</span><span class="sxs-lookup"><span data-stu-id="7c4b5-154">[Apache DataFu Pig Getting Started](https://datafu.apache.org/docs/datafu/getting-started.html).</span></span>
* [<span data-ttu-id="7c4b5-155">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c4b5-155">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
