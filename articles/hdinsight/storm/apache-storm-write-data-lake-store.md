---
title: Apache Storm write to Storage/Data Lake Store - Azure HDInsight
description: Learn how to use the Apache Storm to write to the HDFS-compatible storage for HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/27/2018
ms.openlocfilehash: 670d465f1481592862f5e653a508460c19be07d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966525"
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="5a040-103">Write to HDFS from Apache Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a040-103">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="5a040-104">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a040-104">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="5a040-105">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-compatible storage.</span><span class="sxs-lookup"><span data-stu-id="5a040-105">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-compatible storage.</span></span> <span data-ttu-id="5a040-106">Storm provides an [HdfsBolt](http://storm.apache.org/releases/current/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span><span class="sxs-lookup"><span data-stu-id="5a040-106">Storm provides an [HdfsBolt](http://storm.apache.org/releases/current/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="5a040-107">This document provides information on writing to either type of storage from the HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="5a040-107">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5a040-108">The example topology used in this document relies on components that are included with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a040-108">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="5a040-109">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span><span class="sxs-lookup"><span data-stu-id="5a040-109">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="5a040-110">Get the code</span><span class="sxs-lookup"><span data-stu-id="5a040-110">Get the code</span></span>

<span data-ttu-id="5a040-111">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="5a040-111">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="5a040-112">To compile this project, you need the following configuration for your development environment:</span><span class="sxs-lookup"><span data-stu-id="5a040-112">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="5a040-113">[Java JDK 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) or higher.</span><span class="sxs-lookup"><span data-stu-id="5a040-113">[Java JDK 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) or higher.</span></span> <span data-ttu-id="5a040-114">HDInsight 3.5 or higher require Java 8.</span><span class="sxs-lookup"><span data-stu-id="5a040-114">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="5a040-115">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="5a040-115">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="5a040-116">The following environment variables may be set when you install Java and the JDK on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="5a040-116">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="5a040-117">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="5a040-117">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="5a040-118">`JAVA_HOME` - should point to the directory where the JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="5a040-118">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="5a040-119">`PATH` - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="5a040-119">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="5a040-120">`JAVA_HOME` (or the equivalent path).</span><span class="sxs-lookup"><span data-stu-id="5a040-120">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="5a040-121">`JAVA_HOME\bin` (or the equivalent path).</span><span class="sxs-lookup"><span data-stu-id="5a040-121">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="5a040-122">The directory where Maven is installed.</span><span class="sxs-lookup"><span data-stu-id="5a040-122">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="5a040-123">How to use the HdfsBolt with HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a040-123">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a040-124">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span><span class="sxs-lookup"><span data-stu-id="5a040-124">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="5a040-125">For more information, see the [Configure the cluster](#configure) section.</span><span class="sxs-lookup"><span data-stu-id="5a040-125">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="5a040-126">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span><span class="sxs-lookup"><span data-stu-id="5a040-126">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="5a040-127">With HDInsight, use one of the following schemes:</span><span class="sxs-lookup"><span data-stu-id="5a040-127">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="5a040-128">`wasb://`: Used with an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="5a040-128">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="5a040-129">`adl://`: Used with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5a040-129">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="5a040-130">The following table provides examples of using the file scheme for different scenarios:</span><span class="sxs-lookup"><span data-stu-id="5a040-130">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="5a040-131">Scheme</span><span class="sxs-lookup"><span data-stu-id="5a040-131">Scheme</span></span> | <span data-ttu-id="5a040-132">Notes</span><span class="sxs-lookup"><span data-stu-id="5a040-132">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="5a040-133">The default storage account is a blob container in an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="5a040-133">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="5a040-134">The default storage account is a directory in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5a040-134">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="5a040-135">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span><span class="sxs-lookup"><span data-stu-id="5a040-135">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="5a040-136">For example, the `/clusters/myclustername/` directory.</span><span class="sxs-lookup"><span data-stu-id="5a040-136">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="5a040-137">A non-default (additional) Azure storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-137">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="5a040-138">The root of the Data Lake Store used by the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-138">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="5a040-139">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span><span class="sxs-lookup"><span data-stu-id="5a040-139">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="5a040-140">For more information, see the [HdfsBolt](http://storm.apache.org/releases/current/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span><span class="sxs-lookup"><span data-stu-id="5a040-140">For more information, see the [HdfsBolt](http://storm.apache.org/releases/current/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="5a040-141">Example configuration</span><span class="sxs-lookup"><span data-stu-id="5a040-141">Example configuration</span></span>

<span data-ttu-id="5a040-142">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span><span class="sxs-lookup"><span data-stu-id="5a040-142">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="5a040-143">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.2/flux.html) framework for Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="5a040-143">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.2/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  # Rotate files when they hit 5 MB
  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.FileSizeRotationPolicy"
    constructorArgs:
      - 5
      - "MB"

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

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


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
```

<span data-ttu-id="5a040-144">This YAML defines the following items:</span><span class="sxs-lookup"><span data-stu-id="5a040-144">This YAML defines the following items:</span></span>

* <span data-ttu-id="5a040-145">`syncPolicy`: Defines when files are synched/flushed to the file system.</span><span class="sxs-lookup"><span data-stu-id="5a040-145">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="5a040-146">In this example, every 1000 tuples.</span><span class="sxs-lookup"><span data-stu-id="5a040-146">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="5a040-147">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span><span class="sxs-lookup"><span data-stu-id="5a040-147">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="5a040-148">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span><span class="sxs-lookup"><span data-stu-id="5a040-148">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="5a040-149">`recordFormat`: Defines the internal format of the files written.</span><span class="sxs-lookup"><span data-stu-id="5a040-149">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="5a040-150">In this example, fields are delimited by the `|` character.</span><span class="sxs-lookup"><span data-stu-id="5a040-150">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="5a040-151">`rotationPolicy`: Defines when to rotate files.</span><span class="sxs-lookup"><span data-stu-id="5a040-151">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="5a040-152">In this example, no rotation is performed.</span><span class="sxs-lookup"><span data-stu-id="5a040-152">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="5a040-153">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span><span class="sxs-lookup"><span data-stu-id="5a040-153">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="5a040-154">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.2/flux.html](https://storm.apache.org/releases/1.1.2/flux.html).</span><span class="sxs-lookup"><span data-stu-id="5a040-154">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.2/flux.html](https://storm.apache.org/releases/1.1.2/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="5a040-155">Configure the cluster</span><span class="sxs-lookup"><span data-stu-id="5a040-155">Configure the cluster</span></span>

<span data-ttu-id="5a040-156">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span><span class="sxs-lookup"><span data-stu-id="5a040-156">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="5a040-157">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span><span class="sxs-lookup"><span data-stu-id="5a040-157">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

* <span data-ttu-id="5a040-158">Script URI: `https://hdiconfigactions.blob.core.windows.net/linuxstormextlibv01/stormextlib.sh`</span><span class="sxs-lookup"><span data-stu-id="5a040-158">Script URI: `https://hdiconfigactions.blob.core.windows.net/linuxstormextlibv01/stormextlib.sh`</span></span>
* <span data-ttu-id="5a040-159">Nodes to apply to: Nimbus, Supervisor</span><span class="sxs-lookup"><span data-stu-id="5a040-159">Nodes to apply to: Nimbus, Supervisor</span></span>
* <span data-ttu-id="5a040-160">Parameters: None</span><span class="sxs-lookup"><span data-stu-id="5a040-160">Parameters: None</span></span>

<span data-ttu-id="5a040-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./../hdinsight-hadoop-customize-cluster-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="5a040-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./../hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="5a040-162">Build and package the topology</span><span class="sxs-lookup"><span data-stu-id="5a040-162">Build and package the topology</span></span>

1. <span data-ttu-id="5a040-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span><span class="sxs-lookup"><span data-stu-id="5a040-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="5a040-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span><span class="sxs-lookup"><span data-stu-id="5a040-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="5a040-165">To build and package the topology, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5a040-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="5a040-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="5a040-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="5a040-167">This file contains the compiled topology.</span><span class="sxs-lookup"><span data-stu-id="5a040-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="5a040-168">Deploy and run the topology</span><span class="sxs-lookup"><span data-stu-id="5a040-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="5a040-169">Use the following command to copy the topology to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="5a040-170">Replace **USER** with the SSH user name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="5a040-171">Replace **CLUSTERNAME** with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs-1.0-SNAPSHOT.jar
   
    <span data-ttu-id="5a040-172">When prompted, enter the password used when creating the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="5a040-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span><span class="sxs-lookup"><span data-stu-id="5a040-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a040-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5a040-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5a040-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="5a040-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="5a040-176">Replace **USER** with the SSH user name you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="5a040-177">Replace **CLUSTERNAME** with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5a040-178">When prompted, enter the password used when creating the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="5a040-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span><span class="sxs-lookup"><span data-stu-id="5a040-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="5a040-180">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5a040-180">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="5a040-181">Once connected, use the following command to create a file named `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="5a040-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="5a040-182">Use the following text as the contents of the `dev.properties` file:</span><span class="sxs-lookup"><span data-stu-id="5a040-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="5a040-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span><span class="sxs-lookup"><span data-stu-id="5a040-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="5a040-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span><span class="sxs-lookup"><span data-stu-id="5a040-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="5a040-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span><span class="sxs-lookup"><span data-stu-id="5a040-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="5a040-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span><span class="sxs-lookup"><span data-stu-id="5a040-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="5a040-187">Use the following command to start the topology:</span><span class="sxs-lookup"><span data-stu-id="5a040-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="5a040-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a040-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="5a040-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span><span class="sxs-lookup"><span data-stu-id="5a040-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="5a040-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span><span class="sxs-lookup"><span data-stu-id="5a040-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="5a040-191">View output data</span><span class="sxs-lookup"><span data-stu-id="5a040-191">View output data</span></span>

<span data-ttu-id="5a040-192">To view the data, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5a040-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="5a040-193">A list of the files created by this topology is displayed.</span><span class="sxs-lookup"><span data-stu-id="5a040-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="5a040-194">The following list is an example of the data retuned by the previous commands:</span><span class="sxs-lookup"><span data-stu-id="5a040-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       488000 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       444000 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       502000 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       582000 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       464000 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt

## <a name="stop-the-topology"></a><span data-ttu-id="5a040-195">Stop the topology</span><span class="sxs-lookup"><span data-stu-id="5a040-195">Stop the topology</span></span>

<span data-ttu-id="5a040-196">Storm topologies run until stopped, or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="5a040-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="5a040-197">To stop the topology, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5a040-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="5a040-198">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="5a040-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="5a040-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a040-199">Next steps</span></span>

<span data-ttu-id="5a040-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](apache-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5a040-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](apache-storm-example-topology.md).</span></span>

