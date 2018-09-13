---
title: Apache Storm with Python comopnents - Azure HDInsight
description: Learn how to create an Apache Storm topology that uses Python components.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
keywords: apache storm python
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 04/30/2018
ms.author: jasonh
ms.openlocfilehash: 753c870f5d99d7bf887944b0d180645dc019b2b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871592"
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="9d5d2-104">Develop Apache Storm topologies using Python on HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d5d2-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="9d5d2-105">Learn how to create an Apache Storm topology that uses Python components.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="9d5d2-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="9d5d2-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d5d2-108">The information in this document was tested using Storm on HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="9d5d2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9d5d2-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="9d5d2-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d5d2-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d5d2-112">Prerequisites</span></span>

* <span data-ttu-id="9d5d2-113">Python 2.7 or higher</span><span class="sxs-lookup"><span data-stu-id="9d5d2-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="9d5d2-114">Java JDK 1.8 or higher</span><span class="sxs-lookup"><span data-stu-id="9d5d2-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="9d5d2-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="9d5d2-115">Maven 3</span></span>

* <span data-ttu-id="9d5d2-116">(Optional) A local Storm development environment.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="9d5d2-117">A local Storm environment is only needed if you want to run the topology locally.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="9d5d2-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.1.2/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.1.2/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="9d5d2-119">Storm multi-language support</span><span class="sxs-lookup"><span data-stu-id="9d5d2-119">Storm multi-language support</span></span>

<span data-ttu-id="9d5d2-120">Apache Storm was designed to work with components written using any programming language.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="9d5d2-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="9d5d2-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="9d5d2-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="9d5d2-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="9d5d2-125">Components written in other languages are executed as subprocesses.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="9d5d2-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="9d5d2-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="9d5d2-128">Python with the Flux framework</span><span class="sxs-lookup"><span data-stu-id="9d5d2-128">Python with the Flux framework</span></span>

<span data-ttu-id="9d5d2-129">The Flux framework allows you to define Storm topologies separately from the components.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="9d5d2-130">The Flux framework uses YAML to define the Storm topology.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="9d5d2-131">The following text is an example of how to reference a Python component in the YAML document:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

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

<span data-ttu-id="9d5d2-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="9d5d2-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="9d5d2-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="9d5d2-135">The `pom.xml` includes this file using the following XML:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="9d5d2-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="9d5d2-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="9d5d2-138">Build the project</span><span class="sxs-lookup"><span data-stu-id="9d5d2-138">Build the project</span></span>

<span data-ttu-id="9d5d2-139">From the root of the project, use the following command:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="9d5d2-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="9d5d2-141">Run the topology locally</span><span class="sxs-lookup"><span data-stu-id="9d5d2-141">Run the topology locally</span></span>

<span data-ttu-id="9d5d2-142">To run the topology locally, use the following command:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="9d5d2-143">This command requires a local Storm development environment.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="9d5d2-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="9d5d2-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="9d5d2-145">Once the topology starts, it emits information to the local console similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="9d5d2-146">To stop the topology, use __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="9d5d2-147">Run the Storm topology on HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d5d2-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="9d5d2-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="9d5d2-149">Replace `sshuser` with the SSH user for your cluster.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="9d5d2-150">Replace `mycluster` with the cluster name.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="9d5d2-151">You may be prompted to enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="9d5d2-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9d5d2-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9d5d2-153">Once the file has been uploaded, connect to the cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="9d5d2-154">From the SSH session, use the following command to start the topology on the cluster:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="9d5d2-155">You can use the Storm UI to view the topology on the cluster.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="9d5d2-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="9d5d2-157">Replace `mycluster` with your cluster name.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="9d5d2-158">Once started, a Storm topology runs until stopped.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="9d5d2-159">To stop the topology, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="9d5d2-160">The `storm kill TOPOLOGYNAME` command from the command line</span><span class="sxs-lookup"><span data-stu-id="9d5d2-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="9d5d2-161">The **Kill** button in the Storm UI.</span><span class="sxs-lookup"><span data-stu-id="9d5d2-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d5d2-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d5d2-162">Next steps</span></span>

<span data-ttu-id="9d5d2-163">See the following documents for other ways to use Python with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9d5d2-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="9d5d2-164">How to use Python for streaming MapReduce jobs</span><span class="sxs-lookup"><span data-stu-id="9d5d2-164">How to use Python for streaming MapReduce jobs</span></span>](../hadoop/apache-hadoop-streaming-python.md)
* [<span data-ttu-id="9d5d2-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span><span class="sxs-lookup"><span data-stu-id="9d5d2-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](../hadoop/python-udf-hdinsight.md)
