---
title: Use Python components in a Storm topology on HDinsight | Microsoft Docs
description: Learn how you can use Python components with Apache Storm on Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: larryfr
ms.openlocfilehash: 39a8eb9ce6a5363f541f02c33cd46d56fdabcae8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549997"
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="4e732-103">Develop Apache Storm topologies using Python on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e732-103">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="4e732-104">Learn how to use Python components with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e732-104">Learn how to use Python components with Storm on HDInsight.</span></span> <span data-ttu-id="4e732-105">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span><span class="sxs-lookup"><span data-stu-id="4e732-105">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="4e732-106">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span><span class="sxs-lookup"><span data-stu-id="4e732-106">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e732-107">The information in this document was tested using Storm on HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="4e732-107">The information in this document was tested using Storm on HDInsight 3.5.</span></span> <span data-ttu-id="4e732-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="4e732-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4e732-109">For more information, see [HDInsight version 3.3 and 3.4 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="4e732-109">For more information, see [HDInsight version 3.3 and 3.4 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

<span data-ttu-id="4e732-110">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="4e732-110">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e732-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4e732-111">Prerequisites</span></span>

* <span data-ttu-id="4e732-112">Python 2.7 or higher</span><span class="sxs-lookup"><span data-stu-id="4e732-112">Python 2.7 or higher</span></span>

* <span data-ttu-id="4e732-113">Java JDK 1.8 or higher</span><span class="sxs-lookup"><span data-stu-id="4e732-113">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="4e732-114">Maven 3</span><span class="sxs-lookup"><span data-stu-id="4e732-114">Maven 3</span></span>

* <span data-ttu-id="4e732-115">(Optional) A local Storm development environment.</span><span class="sxs-lookup"><span data-stu-id="4e732-115">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="4e732-116">A local Storm environment is only needed if you want to run the topology locally.</span><span class="sxs-lookup"><span data-stu-id="4e732-116">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="4e732-117">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="4e732-117">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="4e732-118">Storm multi-language support</span><span class="sxs-lookup"><span data-stu-id="4e732-118">Storm multi-language support</span></span>

<span data-ttu-id="4e732-119">Storm was designed to work with components written using any programming language.</span><span class="sxs-lookup"><span data-stu-id="4e732-119">Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="4e732-120">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="4e732-120">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="4e732-121">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span><span class="sxs-lookup"><span data-stu-id="4e732-121">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="4e732-122">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="4e732-122">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="4e732-123">Apache Storm is a Java process that runs on the Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="4e732-123">Apache Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="4e732-124">Components written in other languages are executed as subprocesses.</span><span class="sxs-lookup"><span data-stu-id="4e732-124">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="4e732-125">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="4e732-125">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="4e732-126">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span><span class="sxs-lookup"><span data-stu-id="4e732-126">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-and-the-flux-framework"></a><span data-ttu-id="4e732-127">Python and the Flux framework</span><span class="sxs-lookup"><span data-stu-id="4e732-127">Python and the Flux framework</span></span>

<span data-ttu-id="4e732-128">The Flux framework allows you to define Storm topologies separately from the components.</span><span class="sxs-lookup"><span data-stu-id="4e732-128">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="4e732-129">While the components in this example are written using Python, the topology is defined using YAML.</span><span class="sxs-lookup"><span data-stu-id="4e732-129">While the components in this example are written using Python, the topology is defined using YAML.</span></span> <span data-ttu-id="4e732-130">The following text is an example of how a Python component is referenced in the YAML document:</span><span class="sxs-lookup"><span data-stu-id="4e732-130">The following text is an example of how a Python component is referenced in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="4e732-131">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span><span class="sxs-lookup"><span data-stu-id="4e732-131">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="4e732-132">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span><span class="sxs-lookup"><span data-stu-id="4e732-132">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="4e732-133">So this example stores the Python scripts in the `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="4e732-133">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="4e732-134">The `pom.xml` includes this file using the following XML:</span><span class="sxs-lookup"><span data-stu-id="4e732-134">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="4e732-135">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span><span class="sxs-lookup"><span data-stu-id="4e732-135">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="4e732-136">The Flux framework includes this automatically when the project is built, so you don't have to worry about including it.</span><span class="sxs-lookup"><span data-stu-id="4e732-136">The Flux framework includes this automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="4e732-137">Build the project</span><span class="sxs-lookup"><span data-stu-id="4e732-137">Build the project</span></span>

<span data-ttu-id="4e732-138">From the root of the project, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4e732-138">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="4e732-139">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span><span class="sxs-lookup"><span data-stu-id="4e732-139">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="4e732-140">Run the topology locally</span><span class="sxs-lookup"><span data-stu-id="4e732-140">Run the topology locally</span></span>

<span data-ttu-id="4e732-141">To run the topology locally, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4e732-141">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="4e732-142">This command requires a local Storm development environment.</span><span class="sxs-lookup"><span data-stu-id="4e732-142">This command requires a local Storm development environment.</span></span> <span data-ttu-id="4e732-143">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="4e732-143">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="4e732-144">Once the topology starts, it emits information to the local console similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="4e732-144">Once the topology starts, it emits information to the local console similar to the following text:</span></span>

```
24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
^C24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}
```

<span data-ttu-id="4e732-145">Use Ctrl+c to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="4e732-145">Use Ctrl+c to stop the topology.</span></span>

## <a name="run-the-topology-on-hdinsight"></a><span data-ttu-id="4e732-146">Run the topology on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e732-146">Run the topology on HDInsight</span></span>

1. <span data-ttu-id="4e732-147">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="4e732-147">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4e732-148">Replace `sshuser` with the SSH user for your cluster.</span><span class="sxs-lookup"><span data-stu-id="4e732-148">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="4e732-149">Replace `mycluster` with the cluster name.</span><span class="sxs-lookup"><span data-stu-id="4e732-149">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="4e732-150">You may be prompted to enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="4e732-150">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="4e732-151">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4e732-151">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4e732-152">Once the file has been uploaded, connect to the cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="4e732-152">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="4e732-153">From the SSH session, use the following command to start the topology on the cluster:</span><span class="sxs-lookup"><span data-stu-id="4e732-153">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="4e732-154">You can use the Storm UI to view the topology on the cluster.</span><span class="sxs-lookup"><span data-stu-id="4e732-154">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="4e732-155">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="4e732-155">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="4e732-156">Replace `mycluster` with your cluster name.</span><span class="sxs-lookup"><span data-stu-id="4e732-156">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="4e732-157">Once started, a Storm topology runs until stopped.</span><span class="sxs-lookup"><span data-stu-id="4e732-157">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="4e732-158">To stop the topology, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="4e732-158">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="4e732-159">The `storm kill TOPOLOGYNAME` command from the command-line</span><span class="sxs-lookup"><span data-stu-id="4e732-159">The `storm kill TOPOLOGYNAME` command from the command-line</span></span>
> * <span data-ttu-id="4e732-160">The **Kill** button in the Storm UI.</span><span class="sxs-lookup"><span data-stu-id="4e732-160">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4e732-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e732-161">Next steps</span></span>

<span data-ttu-id="4e732-162">See the following documents for other ways to use Python with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4e732-162">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="4e732-163">How to use Python for streaming MapReduce jobs</span><span class="sxs-lookup"><span data-stu-id="4e732-163">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="4e732-164">How to use Python User Defined Functions (UDF) in Pig and Hive</span><span class="sxs-lookup"><span data-stu-id="4e732-164">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
