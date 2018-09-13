---
title: Use Azure Data Lake Store with Apache Storm on Azure HDInsight
description: Learn how to write data to Azure Data Lake Store from an Apache Storm topology on HDInsight. This document, and the associated example, demonstrate how the HdfsBolt component can be used to write to Data Lake Store.
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/03/2017
ms.author: larryfr
ms.openlocfilehash: 514319dfcb532ab3708352b2467c095d7775b714
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660990"
---
# <a name="use-azure-data-lake-store-with-apache-storm-with-hdinsight-java"></a><span data-ttu-id="f99d2-104">Use Azure Data Lake Store with Apache Storm with HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="f99d2-104">Use Azure Data Lake Store with Apache Storm with HDInsight (Java)</span></span>

<span data-ttu-id="f99d2-105">Azure Data Lake Store is an HDFS compatible cloud storage service that provides high throughput, availability, durability, and reliability for your data.</span><span class="sxs-lookup"><span data-stu-id="f99d2-105">Azure Data Lake Store is an HDFS compatible cloud storage service that provides high throughput, availability, durability, and reliability for your data.</span></span> <span data-ttu-id="f99d2-106">In this document, you learn how to use a Java-based Storm topology to write data to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f99d2-106">In this document, you learn how to use a Java-based Storm topology to write data to Azure Data Lake Store.</span></span> <span data-ttu-id="f99d2-107">The steps in this document using the [HdfsBolt](http://storm.apache.org/releases/1.0.2/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component, which is provided as part of Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="f99d2-107">The steps in this document using the [HdfsBolt](http://storm.apache.org/releases/1.0.2/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component, which is provided as part of Apache Storm.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f99d2-108">The example topology used in this document relies on components that are included with Storm on HDInsight clusters, and may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span><span class="sxs-lookup"><span data-stu-id="f99d2-108">The example topology used in this document relies on components that are included with Storm on HDInsight clusters, and may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="how-to-work-with-azure-data-lake-store"></a><span data-ttu-id="f99d2-109">How to work with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f99d2-109">How to work with Azure Data Lake Store</span></span>

<span data-ttu-id="f99d2-110">Data Lake Store appears to HDInsight as an HDFS compatible file system, so you can use the Storm-HDFS bolt to write to it.</span><span class="sxs-lookup"><span data-stu-id="f99d2-110">Data Lake Store appears to HDInsight as an HDFS compatible file system, so you can use the Storm-HDFS bolt to write to it.</span></span> <span data-ttu-id="f99d2-111">When working with Azure Data Lake from HDInsight, you can use a file scheme of `adl://`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-111">When working with Azure Data Lake from HDInsight, you can use a file scheme of `adl://`.</span></span>

* <span data-ttu-id="f99d2-112">If Data Lake Storage is the primary storage for the cluster, use `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-112">If Data Lake Storage is the primary storage for the cluster, use `adl:///`.</span></span> <span data-ttu-id="f99d2-113">This is the root of the cluster storage in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f99d2-113">This is the root of the cluster storage in Azure Data Lake.</span></span> <span data-ttu-id="f99d2-114">This may translate to a path of /clusters/CLUSTERNAME in your Data Lake Storage account.</span><span class="sxs-lookup"><span data-stu-id="f99d2-114">This may translate to a path of /clusters/CLUSTERNAME in your Data Lake Storage account.</span></span>
* <span data-ttu-id="f99d2-115">If Data Lake Storage is secondary storage for the cluster, use `adl://DATALAKEACCOUNT.azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-115">If Data Lake Storage is secondary storage for the cluster, use `adl://DATALAKEACCOUNT.azuredatalakestore.net/`.</span></span> <span data-ttu-id="f99d2-116">This URI specifies the Data Lake Storage account that data is written to.</span><span class="sxs-lookup"><span data-stu-id="f99d2-116">This URI specifies the Data Lake Storage account that data is written to.</span></span> <span data-ttu-id="f99d2-117">Data is written starting at the root of the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f99d2-117">Data is written starting at the root of the Data Lake Store.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f99d2-118">You can also use this URI format to save data to the Data Lake Store account that contains primary storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-118">You can also use this URI format to save data to the Data Lake Store account that contains primary storage for your cluster.</span></span> <span data-ttu-id="f99d2-119">This allows you to save the data outside of the directory path that contains HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f99d2-119">This allows you to save the data outside of the directory path that contains HDInsight.</span></span>

<span data-ttu-id="f99d2-120">The following Java code demonstrates how you can use the Storm-HDFS bolt to write data to a directory named `/stormdata` on a Data Lake Store account named `MYDATALAKE`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-120">The following Java code demonstrates how you can use the Storm-HDFS bolt to write data to a directory named `/stormdata` on a Data Lake Store account named `MYDATALAKE`.</span></span>

```java
// 1. Create sync and rotation policies to control when data is synched
//    (written) to the file system and when to roll over into a new file.
SyncPolicy syncPolicy = new CountSyncPolicy(1000);
FileRotationPolicy rotationPolicy = new FileSizeRotationPolicy(0.5f, Units.KB);
// 2. Set the format. In this case, comma delimited
RecordFormat recordFormat = new DelimitedRecordFormat().withFieldDelimiter(",");
// 3. Set the directory name. In this case, '/stormdata/'
FileNameFormat fileNameFormat = new DefaultFileNameFormat().withPath("/stormdata/");
// 4. Create the bolt using the previously created settings,
//    and also tell it the base URL to your Data Lake Store.
// NOTE! Replace 'MYDATALAKE' below with the name of your data lake store.
HdfsBolt adlsBolt = new HdfsBolt()
    .withFsUrl("adl://MYDATALAKE.azuredatalakestore.net/")
        .withRecordFormat(recordFormat)
        .withFileNameFormat(fileNameFormat)
        .withRotationPolicy(rotationPolicy)
        .withSyncPolicy(syncPolicy);
// 4. Give it a name and wire it up to the bolt it accepts data
//    from. NOTE: The name used here is also used as part of the
//    file name for the files written to Data Lake Store.
builder.setBolt("ADLStoreBolt", adlsBolt, 1)
    .globalGrouping("finalcount");
```

<span data-ttu-id="f99d2-121">The following YAML demonstrates how to use the Storm-HDFS bolt from the Flux framework:</span><span class="sxs-lookup"><span data-stu-id="f99d2-121">The following YAML demonstrates how to use the Storm-HDFS bolt from the Flux framework:</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000
  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.FileSizeRotationPolicy"
    constructorArgs:
      - 5
      - KB

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

  - id: "rotationAction"
    className: "org.apache.storm.hdfs.common.rotation.MoveFileAction"
    configMethods:
      - name: "toDestination"
        args: ["${hdfs.dest.dir}"]

# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
    parallelism: 1
```

> [!NOTE]
> <span data-ttu-id="f99d2-122">The examples in this document use the Flux framework.</span><span class="sxs-lookup"><span data-stu-id="f99d2-122">The examples in this document use the Flux framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f99d2-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f99d2-123">Prerequisites</span></span>

* <span data-ttu-id="f99d2-124">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span><span class="sxs-lookup"><span data-stu-id="f99d2-124">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="f99d2-125">HDInsight 3.5 requires Java 8.</span><span class="sxs-lookup"><span data-stu-id="f99d2-125">HDInsight 3.5 requires Java 8.</span></span>

* [<span data-ttu-id="f99d2-126">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="f99d2-126">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="f99d2-127">A Storm on HDInsight cluster version 3.5.</span><span class="sxs-lookup"><span data-stu-id="f99d2-127">A Storm on HDInsight cluster version 3.5.</span></span> <span data-ttu-id="f99d2-128">To create a new Storm on HDInsight cluster, use the steps in the [Use HDInsight with Data Lake Store using Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="f99d2-128">To create a new Storm on HDInsight cluster, use the steps in the [Use HDInsight with Data Lake Store using Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) document.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="f99d2-129">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="f99d2-129">Configure environment variables</span></span>

<span data-ttu-id="f99d2-130">The following environment variables may be set when you install Java and the JDK on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="f99d2-130">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="f99d2-131">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="f99d2-131">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="f99d2-132">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span><span class="sxs-lookup"><span data-stu-id="f99d2-132">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="f99d2-133">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-8-oracle`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-133">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-8-oracle`.</span></span> <span data-ttu-id="f99d2-134">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.8`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-134">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.8`.</span></span>
* <span data-ttu-id="f99d2-135">**PATH** - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="f99d2-135">**PATH** - should contain the following paths:</span></span>
  
  * <span data-ttu-id="f99d2-136">**JAVA\_HOME** (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="f99d2-136">**JAVA\_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="f99d2-137">**JAVA\_HOME\bin** (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="f99d2-137">**JAVA\_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="f99d2-138">The directory where Maven is installed</span><span class="sxs-lookup"><span data-stu-id="f99d2-138">The directory where Maven is installed</span></span>

## <a name="topology-implementation"></a><span data-ttu-id="f99d2-139">Topology implementation</span><span class="sxs-lookup"><span data-stu-id="f99d2-139">Topology implementation</span></span>

<span data-ttu-id="f99d2-140">The example used in this document is written in Java, and uses the following components:</span><span class="sxs-lookup"><span data-stu-id="f99d2-140">The example used in this document is written in Java, and uses the following components:</span></span>

* <span data-ttu-id="f99d2-141">**TickSpout**: Generates the data used by other components in the topology.</span><span class="sxs-lookup"><span data-stu-id="f99d2-141">**TickSpout**: Generates the data used by other components in the topology.</span></span>
* <span data-ttu-id="f99d2-142">**PartialCount**: Counts events generated by TickSpout.</span><span class="sxs-lookup"><span data-stu-id="f99d2-142">**PartialCount**: Counts events generated by TickSpout.</span></span>
* <span data-ttu-id="f99d2-143">**FinalCount**: Aggregates count data from PartialCount.</span><span class="sxs-lookup"><span data-stu-id="f99d2-143">**FinalCount**: Aggregates count data from PartialCount.</span></span>
* <span data-ttu-id="f99d2-144">**ADLStoreBolt**: Writes data to Azure Data Lake Store using the [HdfsBolt](http://storm.apache.org/releases/1.0.2/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component.</span><span class="sxs-lookup"><span data-stu-id="f99d2-144">**ADLStoreBolt**: Writes data to Azure Data Lake Store using the [HdfsBolt](http://storm.apache.org/releases/1.0.2/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component.</span></span>

<span data-ttu-id="f99d2-145">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="f99d2-145">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="f99d2-146">Build and package the topology</span><span class="sxs-lookup"><span data-stu-id="f99d2-146">Build and package the topology</span></span>

1. <span data-ttu-id="f99d2-147">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span><span class="sxs-lookup"><span data-stu-id="f99d2-147">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="f99d2-148">Open the `StormToDataLake\src\main\java\com\microsoft\example\StormToDataLakeStore.java` file in an editor and find the line that contains `.withFsUrl("adl://MYDATALAKE.azuredatalakestore.net/")`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-148">Open the `StormToDataLake\src\main\java\com\microsoft\example\StormToDataLakeStore.java` file in an editor and find the line that contains `.withFsUrl("adl://MYDATALAKE.azuredatalakestore.net/")`.</span></span> <span data-ttu-id="f99d2-149">Change **MYDATALAKE** to the name of the Azure Data Lake Store you used when creating your HDInsight server.</span><span class="sxs-lookup"><span data-stu-id="f99d2-149">Change **MYDATALAKE** to the name of the Azure Data Lake Store you used when creating your HDInsight server.</span></span>

3. <span data-ttu-id="f99d2-150">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project, and run the following commands to build and package the topology.</span><span class="sxs-lookup"><span data-stu-id="f99d2-150">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project, and run the following commands to build and package the topology.</span></span>
   
        mvn compile
        mvn package
   
    <span data-ttu-id="f99d2-151">Once the build and packaging completes, there will be a new directory named `target`, that contains a file named `StormToDataLakeStore-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="f99d2-151">Once the build and packaging completes, there will be a new directory named `target`, that contains a file named `StormToDataLakeStore-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="f99d2-152">This contains the compiled topology.</span><span class="sxs-lookup"><span data-stu-id="f99d2-152">This contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="f99d2-153">Deploy and run the topology</span><span class="sxs-lookup"><span data-stu-id="f99d2-153">Deploy and run the topology</span></span>

1. <span data-ttu-id="f99d2-154">Use the following command to copy the topology to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-154">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="f99d2-155">Replace **USER** with the SSH user name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-155">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="f99d2-156">Replace **CLUSTERNAME** with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-156">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToDataLakeStore-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToDataLakeStore-1.0-SNAPSHOT.jar
   
    <span data-ttu-id="f99d2-157">When prompted, enter the password used when creating the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-157">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="f99d2-158">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span><span class="sxs-lookup"><span data-stu-id="f99d2-158">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f99d2-159">If you are using a Windows client for development, you may not have an `scp` command.</span><span class="sxs-lookup"><span data-stu-id="f99d2-159">If you are using a Windows client for development, you may not have an `scp` command.</span></span> <span data-ttu-id="f99d2-160">If so, you can use `pscp`, which is available from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="f99d2-160">If so, you can use `pscp`, which is available from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

2. <span data-ttu-id="f99d2-161">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="f99d2-161">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="f99d2-162">Replace **USER** with the SSH user name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-162">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="f99d2-163">Replace **CLUSTERNAME** with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-163">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="f99d2-164">When prompted, enter the password used when creating the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="f99d2-164">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="f99d2-165">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span><span class="sxs-lookup"><span data-stu-id="f99d2-165">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="f99d2-166">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f99d2-166">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="f99d2-167">Once connected, use the following command to create a file named `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="f99d2-167">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="f99d2-168">Use the following text as the contents of the `dev.properties` file:</span><span class="sxs-lookup"><span data-stu-id="f99d2-168">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata
        hdfs.url: adl:///
    
    <span data-ttu-id="f99d2-169">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span><span class="sxs-lookup"><span data-stu-id="f99d2-169">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="f99d2-170">The values in this file set the Data Lake store URL and the directory name that data is written to.</span><span class="sxs-lookup"><span data-stu-id="f99d2-170">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="f99d2-171">Use the following command to start the topology:</span><span class="sxs-lookup"><span data-stu-id="f99d2-171">Use the following command to start the topology:</span></span>
   
        storm jar StormToDataLakeStore-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /datalakewriter.yaml --filter dev.properties

    <span data-ttu-id="f99d2-172">This command starts the topology using the Flux framework.</span><span class="sxs-lookup"><span data-stu-id="f99d2-172">This command starts the topology using the Flux framework.</span></span> <span data-ttu-id="f99d2-173">The topology is defined by the `datalakewriter.yaml` file included in the jar.</span><span class="sxs-lookup"><span data-stu-id="f99d2-173">The topology is defined by the `datalakewriter.yaml` file included in the jar.</span></span> <span data-ttu-id="f99d2-174">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span><span class="sxs-lookup"><span data-stu-id="f99d2-174">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="f99d2-175">View output data</span><span class="sxs-lookup"><span data-stu-id="f99d2-175">View output data</span></span>

<span data-ttu-id="f99d2-176">To view the data, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f99d2-176">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="f99d2-177">This displays a list of files that were created by the topology.</span><span class="sxs-lookup"><span data-stu-id="f99d2-177">This displays a list of files that were created by the topology.</span></span>

<span data-ttu-id="f99d2-178">If Data Lake Store is not the default storage for the cluster, use the following command to view the data:</span><span class="sxs-lookup"><span data-stu-id="f99d2-178">If Data Lake Store is not the default storage for the cluster, use the following command to view the data:</span></span>

    hdfs dfs -ls adl://MYDATALAKE.azuredatalakestore.net/stormdata/

<span data-ttu-id="f99d2-179">In the previous command, replace __MYDATALAKE__ with the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f99d2-179">In the previous command, replace __MYDATALAKE__ with the Data Lake Store account.</span></span>

<span data-ttu-id="f99d2-180">The following list is an example of the data retuned by the previous commands:</span><span class="sxs-lookup"><span data-stu-id="f99d2-180">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 larryfr larryfr       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="f99d2-181">Stop the topology</span><span class="sxs-lookup"><span data-stu-id="f99d2-181">Stop the topology</span></span>

<span data-ttu-id="f99d2-182">Storm topologies will run until stopped, or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="f99d2-182">Storm topologies will run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="f99d2-183">To stop the topologies, use the following information.</span><span class="sxs-lookup"><span data-stu-id="f99d2-183">To stop the topologies, use the following information.</span></span>

<span data-ttu-id="f99d2-184">**For Linux-based HDInsight**:</span><span class="sxs-lookup"><span data-stu-id="f99d2-184">**For Linux-based HDInsight**:</span></span>

<span data-ttu-id="f99d2-185">From an SSH session to the cluster, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f99d2-185">From an SSH session to the cluster, use the following command:</span></span>

    storm kill datalakewriter

## <a name="delete-your-cluster"></a><span data-ttu-id="f99d2-186">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="f99d2-186">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="f99d2-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="f99d2-187">Next steps</span></span>

<span data-ttu-id="f99d2-188">Now that you have learned how to use Storm to write to Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f99d2-188">Now that you have learned how to use Storm to write to Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

