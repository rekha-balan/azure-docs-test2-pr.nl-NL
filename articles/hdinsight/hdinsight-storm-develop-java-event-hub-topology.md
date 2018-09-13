---
title: Process events from Event Hubs with Storm on HDInsight using Java | Microsoft Docs
description: Learn how to process Event Hubs data with a Java Storm topology created with Maven.
services: hdinsight,notification hubs
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: larryfr
ms.openlocfilehash: 299b47090ec7247e0c5bed645311a35b0c203319
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549100"
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="51c14-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="51c14-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="51c14-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51c14-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="51c14-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="51c14-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="51c14-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span><span class="sxs-lookup"><span data-stu-id="51c14-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="51c14-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span><span class="sxs-lookup"><span data-stu-id="51c14-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="51c14-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span><span class="sxs-lookup"><span data-stu-id="51c14-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51c14-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="51c14-109">Prerequisites</span></span>

* <span data-ttu-id="51c14-110">An Apache Storm on HDInsight cluster version 3.5.</span><span class="sxs-lookup"><span data-stu-id="51c14-110">An Apache Storm on HDInsight cluster version 3.5.</span></span> <span data-ttu-id="51c14-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="51c14-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="51c14-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="51c14-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="51c14-113">For more information, see [HDInsight 3.3 and 3.4 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="51c14-113">For more information, see [HDInsight 3.3 and 3.4 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="51c14-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="51c14-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="51c14-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="51c14-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="51c14-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span><span class="sxs-lookup"><span data-stu-id="51c14-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="51c14-117">A text editor or integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="51c14-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="51c14-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span><span class="sxs-lookup"><span data-stu-id="51c14-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="51c14-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span><span class="sxs-lookup"><span data-stu-id="51c14-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="51c14-120">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="51c14-120">An SSH client.</span></span> <span data-ttu-id="51c14-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="51c14-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="51c14-122">An SCP client.</span><span class="sxs-lookup"><span data-stu-id="51c14-122">An SCP client.</span></span> <span data-ttu-id="51c14-123">The `scp` command is provided with all Linux, Unix, and OS X systems (including Bash on Windows 10.) For Windows systems that do not have the `scp` command, we recommend PSCP.</span><span class="sxs-lookup"><span data-stu-id="51c14-123">The `scp` command is provided with all Linux, Unix, and OS X systems (including Bash on Windows 10.) For Windows systems that do not have the `scp` command, we recommend PSCP.</span></span> <span data-ttu-id="51c14-124">PSCP is available from the [PuTTY download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="51c14-124">PSCP is available from the [PuTTY download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="51c14-125">Understanding the example</span><span class="sxs-lookup"><span data-stu-id="51c14-125">Understanding the example</span></span>

<span data-ttu-id="51c14-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span><span class="sxs-lookup"><span data-stu-id="51c14-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="51c14-127">**com.microsoft.example.EventHubWriter** writes random data to an Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="51c14-127">**com.microsoft.example.EventHubWriter** writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="51c14-128">The data is generated by a spout, and is a random device ID and device value.</span><span class="sxs-lookup"><span data-stu-id="51c14-128">The data is generated by a spout, and is a random device ID and device value.</span></span> <span data-ttu-id="51c14-129">So it's simulating some hardware that emits a string ID and a numeric value.</span><span class="sxs-lookup"><span data-stu-id="51c14-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="51c14-130">**com.microsoft.example.EventHubReader** reads data from Event Hub and stores it to the clusters default storage in the /devicedata directory.</span><span class="sxs-lookup"><span data-stu-id="51c14-130">**com.microsoft.example.EventHubReader** reads data from Event Hub and stores it to the clusters default storage in the /devicedata directory.</span></span>

<span data-ttu-id="51c14-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span><span class="sxs-lookup"><span data-stu-id="51c14-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="51c14-132">The JSON format is as follows:</span><span class="sxs-lookup"><span data-stu-id="51c14-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="51c14-133">Project configuration</span><span class="sxs-lookup"><span data-stu-id="51c14-133">Project configuration</span></span>

<span data-ttu-id="51c14-134">The `POM.xml` file contains configuration information for this Maven project.</span><span class="sxs-lookup"><span data-stu-id="51c14-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="51c14-135">The interesting pieces are:</span><span class="sxs-lookup"><span data-stu-id="51c14-135">The interesting pieces are:</span></span>

#### <a name="hortonworks-repository"></a><span data-ttu-id="51c14-136">Hortonworks repository</span><span class="sxs-lookup"><span data-stu-id="51c14-136">Hortonworks repository</span></span>

<span data-ttu-id="51c14-137">HDInsight is based on the Hortonworks Data Platform.</span><span class="sxs-lookup"><span data-stu-id="51c14-137">HDInsight is based on the Hortonworks Data Platform.</span></span> <span data-ttu-id="51c14-138">To make sure that your project is compatible with the version of Storm and Hadoop used with HDInsight 3.5, the following section configures the project to use bits from Hortonworks:</span><span class="sxs-lookup"><span data-stu-id="51c14-138">To make sure that your project is compatible with the version of Storm and Hadoop used with HDInsight 3.5, the following section configures the project to use bits from Hortonworks:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="51c14-139">The EventHubs Storm Spout dependency</span><span class="sxs-lookup"><span data-stu-id="51c14-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>1.0.2</version>
</dependency>
```

<span data-ttu-id="51c14-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span><span class="sxs-lookup"><span data-stu-id="51c14-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

> [!NOTE]
> <span data-ttu-id="51c14-141">This package is installed later in this document.</span><span class="sxs-lookup"><span data-stu-id="51c14-141">This package is installed later in this document.</span></span>

#### <a name="the-hdfsbolt-and-wasb-components"></a><span data-ttu-id="51c14-142">The HdfsBolt and WASB components</span><span class="sxs-lookup"><span data-stu-id="51c14-142">The HdfsBolt and WASB components</span></span>

<span data-ttu-id="51c14-143">The HdfsBolt is normally used to store data to the Hadoop Distributed File System HDFS.</span><span class="sxs-lookup"><span data-stu-id="51c14-143">The HdfsBolt is normally used to store data to the Hadoop Distributed File System HDFS.</span></span> <span data-ttu-id="51c14-144">However HDInsight clusters use Azure Storage (WASB) as the default data store, so we have to load several components that allow HdfsBolt to understand the WASB file system.</span><span class="sxs-lookup"><span data-stu-id="51c14-144">However HDInsight clusters use Azure Storage (WASB) as the default data store, so we have to load several components that allow HdfsBolt to understand the WASB file system.</span></span>

```xml
<!--HdfsBolt stuff -->
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-hdfs</artifactId>
    <!-- exclude these storm-hdfs dependencies since they are on the server -->
    <exclusions>
        <exclusion>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-hdfs</artifactId>
        </exclusion>
    </exclusions>
    <version>${storm.version}</version>
</dependency>
<dependency>
    <groupId>org.apache.hadoop</groupId>
    <artifactId>hadoop-common</artifactId>
    <version>${hadoop.version}</version>
    <exclusions>
    <exclusion>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
    </exclusion>
    </exclusions>
</dependency>
```

> [!NOTE]
> <span data-ttu-id="51c14-145">When working with an earlier version of HDInsight, such as version 3.2, you must manually register these components.</span><span class="sxs-lookup"><span data-stu-id="51c14-145">When working with an earlier version of HDInsight, such as version 3.2, you must manually register these components.</span></span> <span data-ttu-id="51c14-146">For an example, see the [Storm v0.9.3](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub/tree/Storm_v0.9.3) branch of the example repository.</span><span class="sxs-lookup"><span data-stu-id="51c14-146">For an example, see the [Storm v0.9.3](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub/tree/Storm_v0.9.3) branch of the example repository.</span></span>

#### <a name="the-maven-compiler-plugin"></a><span data-ttu-id="51c14-147">The maven-compiler-plugin</span><span class="sxs-lookup"><span data-stu-id="51c14-147">The maven-compiler-plugin</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>2.3.2</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="51c14-148">This configures the project to generate output for Java 8, which is used by HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="51c14-148">This configures the project to generate output for Java 8, which is used by HDInsight 3.5.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="51c14-149">The maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="51c14-149">The maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <!-- Keep us from getting errors when trying to use WASB from the storm-hdfs bolt -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

<span data-ttu-id="51c14-150">This configures the solution to package the output into an uber jar.</span><span class="sxs-lookup"><span data-stu-id="51c14-150">This configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="51c14-151">The jar contains both the project code and required dependencies.</span><span class="sxs-lookup"><span data-stu-id="51c14-151">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="51c14-152">It is also used to:</span><span class="sxs-lookup"><span data-stu-id="51c14-152">It is also used to:</span></span>

* <span data-ttu-id="51c14-153">Rename license files for the dependencies.</span><span class="sxs-lookup"><span data-stu-id="51c14-153">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="51c14-154">Exclude security/signatures.</span><span class="sxs-lookup"><span data-stu-id="51c14-154">Exclude security/signatures.</span></span>
* <span data-ttu-id="51c14-155">Ensure that multiple implementations of the same interface are merged into one entry.</span><span class="sxs-lookup"><span data-stu-id="51c14-155">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="51c14-156">These configuration settings prevent errors at runtime.</span><span class="sxs-lookup"><span data-stu-id="51c14-156">These configuration settings prevent errors at runtime.</span></span>

#### <a name="the-exec-maven-plugin"></a><span data-ttu-id="51c14-157">The exec-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="51c14-157">The exec-maven-plugin</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.2.1</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    </configuration>
</plugin>
```

<span data-ttu-id="51c14-158">This configuration makes it easier to run the topology locally on your development environment.</span><span class="sxs-lookup"><span data-stu-id="51c14-158">This configuration makes it easier to run the topology locally on your development environment.</span></span> <span data-ttu-id="51c14-159">You can run the topology locally using the following syntax:</span><span class="sxs-lookup"><span data-stu-id="51c14-159">You can run the topology locally using the following syntax:</span></span>

    mvn compile exec:java -Dstorm.topology=<CLASSNAME>

<span data-ttu-id="51c14-160">For example, `mvn compile exec:java -Dstorm.topology=com.microsoft.example.EventHubWriter`.</span><span class="sxs-lookup"><span data-stu-id="51c14-160">For example, `mvn compile exec:java -Dstorm.topology=com.microsoft.example.EventHubWriter`.</span></span>

#### <a name="the-resources-section"></a><span data-ttu-id="51c14-161">The resources section</span><span class="sxs-lookup"><span data-stu-id="51c14-161">The resources section</span></span>

```xml
<resources>
    <resource>
    <directory>${basedir}/conf</directory>
    <filtering>false</filtering>
    <includes>
        <include>EventHubs.properties</include>
    </includes>
    </resource>
</resources>
```

<span data-ttu-id="51c14-162">This configuration defines non-Java resources that are included in the project.</span><span class="sxs-lookup"><span data-stu-id="51c14-162">This configuration defines non-Java resources that are included in the project.</span></span> <span data-ttu-id="51c14-163">For example, the **EventHubs.properties** file contains information used to connect to an Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="51c14-163">For example, the **EventHubs.properties** file contains information used to connect to an Azure Event Hub.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="51c14-164">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="51c14-164">Configure environment variables</span></span>

<span data-ttu-id="51c14-165">The following environment variables may be set when you install Java and the JDK on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="51c14-165">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="51c14-166">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="51c14-166">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="51c14-167">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span><span class="sxs-lookup"><span data-stu-id="51c14-167">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="51c14-168">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="51c14-168">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="51c14-169">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="51c14-169">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="51c14-170">**PATH** - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="51c14-170">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="51c14-171">**JAVA_HOME** (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="51c14-171">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="51c14-172">**JAVA_HOME\bin** (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="51c14-172">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="51c14-173">The directory where Maven is installed</span><span class="sxs-lookup"><span data-stu-id="51c14-173">The directory where Maven is installed</span></span>

## <a name="download-and-register-the-eventhub-components"></a><span data-ttu-id="51c14-174">Download and register the EventHub components</span><span class="sxs-lookup"><span data-stu-id="51c14-174">Download and register the EventHub components</span></span>

1. <span data-ttu-id="51c14-175">Download the `storm-eventhubs-1.0.2-jar-with-dependencies.jar` from [https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar](https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar).</span><span class="sxs-lookup"><span data-stu-id="51c14-175">Download the `storm-eventhubs-1.0.2-jar-with-dependencies.jar` from [https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar](https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar).</span></span> <span data-ttu-id="51c14-176">This file contains a spout and bolt component for reading and writing from EventHubs.</span><span class="sxs-lookup"><span data-stu-id="51c14-176">This file contains a spout and bolt component for reading and writing from EventHubs.</span></span>

2. <span data-ttu-id="51c14-177">Use the following command to register the components in your local maven repository:</span><span class="sxs-lookup"><span data-stu-id="51c14-177">Use the following command to register the components in your local maven repository:</span></span>

        mvn install:install-file -Dfile=storm-eventhubs-1.0.2-jar-with-dependencies.jar -DgroupId=com.microsoft -DartifactId=eventhubs -Dversion=1.0.2 -Dpackaging=jar

    <span data-ttu-id="51c14-178">Modify the `-Dfile=` parameter to point to the downloaded file location.</span><span class="sxs-lookup"><span data-stu-id="51c14-178">Modify the `-Dfile=` parameter to point to the downloaded file location.</span></span>

    <span data-ttu-id="51c14-179">This command installs the file in the local Maven repository, where it can be found at compile time by Maven.</span><span class="sxs-lookup"><span data-stu-id="51c14-179">This command installs the file in the local Maven repository, where it can be found at compile time by Maven.</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="51c14-180">Configure Event Hub</span><span class="sxs-lookup"><span data-stu-id="51c14-180">Configure Event Hub</span></span>

<span data-ttu-id="51c14-181">Event Hubs is the data source for this example.</span><span class="sxs-lookup"><span data-stu-id="51c14-181">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="51c14-182">Use the following steps to create a Event Hub.</span><span class="sxs-lookup"><span data-stu-id="51c14-182">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="51c14-183">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="51c14-183">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="51c14-184">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span><span class="sxs-lookup"><span data-stu-id="51c14-184">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="51c14-185">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="51c14-185">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="51c14-186">Finally, click the **Arrow** to continue.</span><span class="sxs-lookup"><span data-stu-id="51c14-186">Finally, click the **Arrow** to continue.</span></span>

    ![wizard page 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="51c14-188">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span><span class="sxs-lookup"><span data-stu-id="51c14-188">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="51c14-189">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span><span class="sxs-lookup"><span data-stu-id="51c14-189">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="51c14-190">For this example, use a partition count of 10 and a message retention of 1.</span><span class="sxs-lookup"><span data-stu-id="51c14-190">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="51c14-191">Note the partition count because you need this value later.</span><span class="sxs-lookup"><span data-stu-id="51c14-191">Note the partition count because you need this value later.</span></span>

    ![wizard page 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="51c14-193">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="51c14-193">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="51c14-194">Select **Configure**, then create two new access policies by using the following information:</span><span class="sxs-lookup"><span data-stu-id="51c14-194">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="51c14-195">Name</span><span class="sxs-lookup"><span data-stu-id="51c14-195">Name</span></span></th><th><span data-ttu-id="51c14-196">Permissions</span><span class="sxs-lookup"><span data-stu-id="51c14-196">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="51c14-197">Writer</span><span class="sxs-lookup"><span data-stu-id="51c14-197">Writer</span></span></td><td><span data-ttu-id="51c14-198">Send</span><span class="sxs-lookup"><span data-stu-id="51c14-198">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="51c14-199">Reader</span><span class="sxs-lookup"><span data-stu-id="51c14-199">Reader</span></span></td><td><span data-ttu-id="51c14-200">Listen</span><span class="sxs-lookup"><span data-stu-id="51c14-200">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="51c14-201">After You create the permissions, select the **Save** icon at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="51c14-201">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="51c14-202">These shared access policies are used to read and write to Event Hub.</span><span class="sxs-lookup"><span data-stu-id="51c14-202">These shared access policies are used to read and write to Event Hub.</span></span>

    ![policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="51c14-204">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span><span class="sxs-lookup"><span data-stu-id="51c14-204">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="51c14-205">Save these keys.</span><span class="sxs-lookup"><span data-stu-id="51c14-205">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="51c14-206">Download and build the project</span><span class="sxs-lookup"><span data-stu-id="51c14-206">Download and build the project</span></span>

1. <span data-ttu-id="51c14-207">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="51c14-207">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="51c14-208">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span><span class="sxs-lookup"><span data-stu-id="51c14-208">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="51c14-209">Use the following to build and package the project:</span><span class="sxs-lookup"><span data-stu-id="51c14-209">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="51c14-210">This command downloads required dependencies, builds, and then packages the project.</span><span class="sxs-lookup"><span data-stu-id="51c14-210">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="51c14-211">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="51c14-211">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="51c14-212">Deploy the topologies</span><span class="sxs-lookup"><span data-stu-id="51c14-212">Deploy the topologies</span></span>

<span data-ttu-id="51c14-213">The jar created by this project contains two topologies; **com.microsoft.example.EventHubWriter** and **com.microsoft.example.EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="51c14-213">The jar created by this project contains two topologies; **com.microsoft.example.EventHubWriter** and **com.microsoft.example.EventHubReader**.</span></span> <span data-ttu-id="51c14-214">The EventHubWriter topology should be started first, as it writes events in to Event Hub that are then read by the EventHubReader.</span><span class="sxs-lookup"><span data-stu-id="51c14-214">The EventHubWriter topology should be started first, as it writes events in to Event Hub that are then read by the EventHubReader.</span></span>

1. <span data-ttu-id="51c14-215">Use SCP to copy the jar package to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="51c14-215">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="51c14-216">Replace USERNAME with the SSH user for your cluster.</span><span class="sxs-lookup"><span data-stu-id="51c14-216">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="51c14-217">Replace CLUSTERNAME with the name of your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="51c14-217">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="51c14-218">If you used a password for your SSH account, you are prompted to enter the password.</span><span class="sxs-lookup"><span data-stu-id="51c14-218">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="51c14-219">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span><span class="sxs-lookup"><span data-stu-id="51c14-219">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="51c14-220">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`.</span><span class="sxs-lookup"><span data-stu-id="51c14-220">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`.</span></span>

    <span data-ttu-id="51c14-221">This command copies the file to the home directory of your SSH user on the cluster.</span><span class="sxs-lookup"><span data-stu-id="51c14-221">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="51c14-222">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="51c14-222">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="51c14-223">Replace **USERNAME** the name of your SSH login.</span><span class="sxs-lookup"><span data-stu-id="51c14-223">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="51c14-224">Replace **CLUSTERNAME** with your HDInsight cluster name:</span><span class="sxs-lookup"><span data-stu-id="51c14-224">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="51c14-225">If you used a password for your SSH account, you are prompted to enter the password.</span><span class="sxs-lookup"><span data-stu-id="51c14-225">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="51c14-226">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span><span class="sxs-lookup"><span data-stu-id="51c14-226">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="51c14-227">The following example loads the private key from `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="51c14-227">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="51c14-228">Use the following command to start the topologies:</span><span class="sxs-lookup"><span data-stu-id="51c14-228">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar com.microsoft.example.EventHubWriter writer
        storm jar EventHubExample-1.0-SNAPSHOT.jar com.microsoft.example.EventHubReader reader

    <span data-ttu-id="51c14-229">These commands start the topologies using the friendly names of "reader" and "writer".</span><span class="sxs-lookup"><span data-stu-id="51c14-229">These commands start the topologies using the friendly names of "reader" and "writer".</span></span>

4. <span data-ttu-id="51c14-230">Wait a minute for the topologies to generate data.</span><span class="sxs-lookup"><span data-stu-id="51c14-230">Wait a minute for the topologies to generate data.</span></span> <span data-ttu-id="51c14-231">Use the following command to verify that data is written to HDInsight storage:</span><span class="sxs-lookup"><span data-stu-id="51c14-231">Use the following command to verify that data is written to HDInsight storage:</span></span>

        hdfs dfs fs -ls /devicedata

    <span data-ttu-id="51c14-232">This command returns a list of files similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="51c14-232">This command returns a list of files similar to the following text:</span></span>

        -rw-r--r--   1 storm supergroup      10283 2015-08-11 19:35 /devicedata/wasbbolt-14-0-1439321744110.txt
        -rw-r--r--   1 storm supergroup      10277 2015-08-11 19:35 /devicedata/wasbbolt-14-1-1439321748237.txt
        -rw-r--r--   1 storm supergroup      10280 2015-08-11 19:36 /devicedata/wasbbolt-14-10-1439321760398.txt
        -rw-r--r--   1 storm supergroup      10267 2015-08-11 19:36 /devicedata/wasbbolt-14-11-1439321761090.txt
        -rw-r--r--   1 storm supergroup      10259 2015-08-11 19:36 /devicedata/wasbbolt-14-12-1439321762679.txt

   > [!NOTE]
   > <span data-ttu-id="51c14-233">Some files may show a size of 0, as they have been created by the EventHubReader, but data has not been stored to them yet.</span><span class="sxs-lookup"><span data-stu-id="51c14-233">Some files may show a size of 0, as they have been created by the EventHubReader, but data has not been stored to them yet.</span></span>

    <span data-ttu-id="51c14-234">You can view the contents of these files by using the following command:</span><span class="sxs-lookup"><span data-stu-id="51c14-234">You can view the contents of these files by using the following command:</span></span>

        hdfs dfs -text /devicedata/*.txt

    <span data-ttu-id="51c14-235">This returns data similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="51c14-235">This returns data similar to the following text:</span></span>

        3409e622-c85d-4d64-8622-af45e30bf774,848981614
        c3305f7e-6948-4cce-89b0-d9fbc2330c36,-1638780537
        788b9796-e2ab-49c4-91e3-bc5b6af1f07e,-1662107246
        6403df8a-6495-402f-bca0-3244be67f225,275738503
        d7c7f96c-581a-45b1-b66c-e32de6d47fce,543829859
        9a692795-e6aa-4946-98c1-2de381b37593,1857409996
        3c8d199b-0003-4a79-8d03-24e13bde7086,-1271260574

    <span data-ttu-id="51c14-236">The first column contains the device ID value and the second column is the device value.</span><span class="sxs-lookup"><span data-stu-id="51c14-236">The first column contains the device ID value and the second column is the device value.</span></span>

5. <span data-ttu-id="51c14-237">Use the following commands to stop the topologies:</span><span class="sxs-lookup"><span data-stu-id="51c14-237">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="51c14-238">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="51c14-238">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshooting"></a><span data-ttu-id="51c14-239">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="51c14-239">Troubleshooting</span></span>

<span data-ttu-id="51c14-240">If you do not see files in the /devicedata directory, use the Storm UI to look for any errors returned by the topologies.</span><span class="sxs-lookup"><span data-stu-id="51c14-240">If you do not see files in the /devicedata directory, use the Storm UI to look for any errors returned by the topologies.</span></span>

<span data-ttu-id="51c14-241">For more information on using the Storm UI, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="51c14-241">For more information on using the Storm UI, see the following topics:</span></span>

* <span data-ttu-id="51c14-242">If you are using a **Linux-based** Storm on HDInsight cluster, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="51c14-242">If you are using a **Linux-based** Storm on HDInsight cluster, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

* <span data-ttu-id="51c14-243">If you are using a **Windows-based** Storm on HDInsight cluster, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="51c14-243">If you are using a **Windows-based** Storm on HDInsight cluster, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="51c14-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="51c14-244">Next steps</span></span>

* [<span data-ttu-id="51c14-245">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="51c14-245">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)



