---
title: Develop Java-based topologies for Apache Storm | Microsoft Docs
description: Learn how to create Storm topologies in Java by creating a simple word count topology.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/29/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 6a378ac7cd5b6ee1141542f4c581c5c99e565b4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553567"
---
# <a name="use-maven-to-develop-a-java-based-word-count-topology-for-storm-on-hdinsight"></a><span data-ttu-id="a00f1-103">Use Maven to develop a Java-based word count topology for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="a00f1-103">Use Maven to develop a Java-based word count topology for Storm on HDInsight</span></span>

<span data-ttu-id="a00f1-104">Learn how to create a Java-based topology for Apache Storm on HDInsight by using Maven.</span><span class="sxs-lookup"><span data-stu-id="a00f1-104">Learn how to create a Java-based topology for Apache Storm on HDInsight by using Maven.</span></span> <span data-ttu-id="a00f1-105">You create a basic word-count application using Maven and Java, where the topology is defined in Java.</span><span class="sxs-lookup"><span data-stu-id="a00f1-105">You create a basic word-count application using Maven and Java, where the topology is defined in Java.</span></span> <span data-ttu-id="a00f1-106">Then, you learn how to define the topology using the Flux framework.</span><span class="sxs-lookup"><span data-stu-id="a00f1-106">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-107">The Flux framework is available in Storm 0.10.0 or later.</span><span class="sxs-lookup"><span data-stu-id="a00f1-107">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="a00f1-108">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span><span class="sxs-lookup"><span data-stu-id="a00f1-108">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>


<span data-ttu-id="a00f1-109">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a00f1-109">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-110">A completed version of the topologies created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="a00f1-110">A completed version of the topologies created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a00f1-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a00f1-111">Prerequisites</span></span>

* [<span data-ttu-id="a00f1-112">Java Developer Kit (JDK) version 7</span><span class="sxs-lookup"><span data-stu-id="a00f1-112">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="a00f1-113">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span><span class="sxs-lookup"><span data-stu-id="a00f1-113">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="a00f1-114">A text editor or IDE.</span><span class="sxs-lookup"><span data-stu-id="a00f1-114">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="a00f1-115">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="a00f1-115">Configure environment variables</span></span>

<span data-ttu-id="a00f1-116">The following environment variables may be set when you install Java and the JDK.</span><span class="sxs-lookup"><span data-stu-id="a00f1-116">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="a00f1-117">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="a00f1-117">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="a00f1-118">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span><span class="sxs-lookup"><span data-stu-id="a00f1-118">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="a00f1-119">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-119">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="a00f1-120">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="a00f1-120">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="a00f1-121">**PATH** - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="a00f1-121">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="a00f1-122">**JAVA_HOME** (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="a00f1-122">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="a00f1-123">**JAVA_HOME\bin** (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="a00f1-123">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="a00f1-124">The directory where Maven is installed</span><span class="sxs-lookup"><span data-stu-id="a00f1-124">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="a00f1-125">Create a Maven project</span><span class="sxs-lookup"><span data-stu-id="a00f1-125">Create a Maven project</span></span>

<span data-ttu-id="a00f1-126">From the command line, use the following command to create a Maven project named **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="a00f1-126">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

    mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false

> [!NOTE]
> <span data-ttu-id="a00f1-127">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span><span class="sxs-lookup"><span data-stu-id="a00f1-127">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="a00f1-128">This command creates a  directory named `WordCount` at the current location, which contains a basic Maven project.</span><span class="sxs-lookup"><span data-stu-id="a00f1-128">This command creates a  directory named `WordCount` at the current location, which contains a basic Maven project.</span></span>

<span data-ttu-id="a00f1-129">The `WordCount` directory contains the following items:</span><span class="sxs-lookup"><span data-stu-id="a00f1-129">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="a00f1-130">`pom.xml`: Contains settings for the Maven project.</span><span class="sxs-lookup"><span data-stu-id="a00f1-130">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="a00f1-131">`src\main\java\com\microsoft\example`: Contains your application code.</span><span class="sxs-lookup"><span data-stu-id="a00f1-131">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="a00f1-132">`src\test\java\com\microsoft\example`: Contains tests for your application.</span><span class="sxs-lookup"><span data-stu-id="a00f1-132">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-example-code"></a><span data-ttu-id="a00f1-133">Remove the example code</span><span class="sxs-lookup"><span data-stu-id="a00f1-133">Remove the example code</span></span>

<span data-ttu-id="a00f1-134">Delete the generated test and the application files:</span><span class="sxs-lookup"><span data-stu-id="a00f1-134">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="a00f1-135">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="a00f1-135">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="a00f1-136">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="a00f1-136">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-repositories"></a><span data-ttu-id="a00f1-137">Add repositories</span><span class="sxs-lookup"><span data-stu-id="a00f1-137">Add repositories</span></span>

<span data-ttu-id="a00f1-138">Since HDInsight is based on the Hortonworks Data Platform (HDP) we recommend using the Hortonworks repository to download dependencies for your HDInsight projects.</span><span class="sxs-lookup"><span data-stu-id="a00f1-138">Since HDInsight is based on the Hortonworks Data Platform (HDP) we recommend using the Hortonworks repository to download dependencies for your HDInsight projects.</span></span> <span data-ttu-id="a00f1-139">In the __pom.xml__ file, add the following after the `<url>http://maven.apache.org</url>` line:</span><span class="sxs-lookup"><span data-stu-id="a00f1-139">In the __pom.xml__ file, add the following after the `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="a00f1-140">Add properties</span><span class="sxs-lookup"><span data-stu-id="a00f1-140">Add properties</span></span>

<span data-ttu-id="a00f1-141">Maven allows you to define project-level values called properties.</span><span class="sxs-lookup"><span data-stu-id="a00f1-141">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="a00f1-142">In the __pom.xml__, add the following text after the `</repositories>` line:</span><span class="sxs-lookup"><span data-stu-id="a00f1-142">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="a00f1-143">You can now use this value in other sections of the `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-143">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="a00f1-144">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span><span class="sxs-lookup"><span data-stu-id="a00f1-144">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="a00f1-145">Add dependencies</span><span class="sxs-lookup"><span data-stu-id="a00f1-145">Add dependencies</span></span>

<span data-ttu-id="a00f1-146">You must add a dependency for Storm components.</span><span class="sxs-lookup"><span data-stu-id="a00f1-146">You must add a dependency for Storm components.</span></span> <span data-ttu-id="a00f1-147">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="a00f1-147">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="a00f1-148">At compile time, Maven uses this information to look up **storm-core** in the Maven repository.</span><span class="sxs-lookup"><span data-stu-id="a00f1-148">At compile time, Maven uses this information to look up **storm-core** in the Maven repository.</span></span> <span data-ttu-id="a00f1-149">It first looks in the repository on your local computer.</span><span class="sxs-lookup"><span data-stu-id="a00f1-149">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="a00f1-150">If the files aren't there, Maven downloads them from the public Maven repository and store them in the local repository.</span><span class="sxs-lookup"><span data-stu-id="a00f1-150">If the files aren't there, Maven downloads them from the public Maven repository and store them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-151">Notice the `<scope>provided</scope>` line in this section.</span><span class="sxs-lookup"><span data-stu-id="a00f1-151">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="a00f1-152">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span><span class="sxs-lookup"><span data-stu-id="a00f1-152">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="a00f1-153">Build configuration</span><span class="sxs-lookup"><span data-stu-id="a00f1-153">Build configuration</span></span>

<span data-ttu-id="a00f1-154">Maven plug-ins allow you to customize the build stages of the project, such as how the project is compiled or how to package it into a JAR file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-154">Maven plug-ins allow you to customize the build stages of the project, such as how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="a00f1-155">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span><span class="sxs-lookup"><span data-stu-id="a00f1-155">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="a00f1-156">This section is used to add plug-ins, resources, and other build configuration options.</span><span class="sxs-lookup"><span data-stu-id="a00f1-156">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="a00f1-157">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="a00f1-157">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="a00f1-158">Add plug-ins</span><span class="sxs-lookup"><span data-stu-id="a00f1-158">Add plug-ins</span></span>

<span data-ttu-id="a00f1-159">For Storm topologies, the [Exec Maven Plugin](http://mojo.codehaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span><span class="sxs-lookup"><span data-stu-id="a00f1-159">For Storm topologies, the [Exec Maven Plugin](http://mojo.codehaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="a00f1-160">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span><span class="sxs-lookup"><span data-stu-id="a00f1-160">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
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
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="a00f1-161">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span><span class="sxs-lookup"><span data-stu-id="a00f1-161">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="a00f1-162">The changes the Java version that Maven uses for the source and target for your application.</span><span class="sxs-lookup"><span data-stu-id="a00f1-162">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="a00f1-163">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span><span class="sxs-lookup"><span data-stu-id="a00f1-163">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="a00f1-164">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span><span class="sxs-lookup"><span data-stu-id="a00f1-164">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="a00f1-165">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span><span class="sxs-lookup"><span data-stu-id="a00f1-165">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="a00f1-166">This example specifies 1.8, so the target HDInsight version is 3.5.</span><span class="sxs-lookup"><span data-stu-id="a00f1-166">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="a00f1-167">Configure resources</span><span class="sxs-lookup"><span data-stu-id="a00f1-167">Configure resources</span></span>

<span data-ttu-id="a00f1-168">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-168">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="a00f1-169">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-169">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="a00f1-170">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-170">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="a00f1-171">This file is used to configure what information is logged by the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-171">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="a00f1-172">Create the topology</span><span class="sxs-lookup"><span data-stu-id="a00f1-172">Create the topology</span></span>

<span data-ttu-id="a00f1-173">A Java-based Storm topology consists of three components that you must author (or reference) as a dependency.</span><span class="sxs-lookup"><span data-stu-id="a00f1-173">A Java-based Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="a00f1-174">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-174">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="a00f1-175">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span><span class="sxs-lookup"><span data-stu-id="a00f1-175">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="a00f1-176">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-176">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="a00f1-177">Create the spout</span><span class="sxs-lookup"><span data-stu-id="a00f1-177">Create the spout</span></span>

<span data-ttu-id="a00f1-178">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span><span class="sxs-lookup"><span data-stu-id="a00f1-178">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="a00f1-179">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="a00f1-179">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-180">For an example of a spout that reads from an external data source, see one of the following examples:</span><span class="sxs-lookup"><span data-stu-id="a00f1-180">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
> 
> * <span data-ttu-id="a00f1-181">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span><span class="sxs-lookup"><span data-stu-id="a00f1-181">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="a00f1-182">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span><span class="sxs-lookup"><span data-stu-id="a00f1-182">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="a00f1-183">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following text as the contents:</span><span class="sxs-lookup"><span data-stu-id="a00f1-183">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following text as the contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

<span data-ttu-id="a00f1-184">Take a moment to read through the code comments to understand how this spout works.</span><span class="sxs-lookup"><span data-stu-id="a00f1-184">Take a moment to read through the code comments to understand how this spout works.</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-185">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-185">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="a00f1-186">Create the bolts</span><span class="sxs-lookup"><span data-stu-id="a00f1-186">Create the bolts</span></span>

<span data-ttu-id="a00f1-187">Bolts handle the data processing.</span><span class="sxs-lookup"><span data-stu-id="a00f1-187">Bolts handle the data processing.</span></span> <span data-ttu-id="a00f1-188">This topology uses two bolts:</span><span class="sxs-lookup"><span data-stu-id="a00f1-188">This topology uses two bolts:</span></span>

* <span data-ttu-id="a00f1-189">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span><span class="sxs-lookup"><span data-stu-id="a00f1-189">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="a00f1-190">**WordCount**: Counts how many times each word has occurred.</span><span class="sxs-lookup"><span data-stu-id="a00f1-190">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-191">Bolts can do literally anything, for example, computation, persistence, or talking to external components.</span><span class="sxs-lookup"><span data-stu-id="a00f1-191">Bolts can do literally anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="a00f1-192">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="a00f1-192">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="a00f1-193">Use the following text as the contents for the files:</span><span class="sxs-lookup"><span data-stu-id="a00f1-193">Use the following text as the contents for the files:</span></span>

<span data-ttu-id="a00f1-194">**SplitSentence**</span><span class="sxs-lookup"><span data-stu-id="a00f1-194">**SplitSentence**</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

<span data-ttu-id="a00f1-195">**WordCount**</span><span class="sxs-lookup"><span data-stu-id="a00f1-195">**WordCount**</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

<span data-ttu-id="a00f1-196">Take a moment to read through the code comments to understand how each bolt works.</span><span class="sxs-lookup"><span data-stu-id="a00f1-196">Take a moment to read through the code comments to understand how each bolt works.</span></span>

### <a name="define-the-topology"></a><span data-ttu-id="a00f1-197">Define the topology</span><span class="sxs-lookup"><span data-stu-id="a00f1-197">Define the topology</span></span>

<span data-ttu-id="a00f1-198">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span><span class="sxs-lookup"><span data-stu-id="a00f1-198">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="a00f1-199">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span><span class="sxs-lookup"><span data-stu-id="a00f1-199">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="a00f1-200">The following image is a basic diagram of the graph of components for this topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-200">The following image is a basic diagram of the graph of components for this topology.</span></span>

![diagram showing the spouts and bolts arrangement](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="a00f1-202">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="a00f1-202">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="a00f1-203">Use the following text as text the contents for the file:</span><span class="sxs-lookup"><span data-stu-id="a00f1-203">Use the following text as text the contents for the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

<span data-ttu-id="a00f1-204">Take a moment to read through the code comments to understand how the topology is defined and then submitted to the cluster.</span><span class="sxs-lookup"><span data-stu-id="a00f1-204">Take a moment to read through the code comments to understand how the topology is defined and then submitted to the cluster.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="a00f1-205">Configure logging</span><span class="sxs-lookup"><span data-stu-id="a00f1-205">Configure logging</span></span>

<span data-ttu-id="a00f1-206">Storm uses Apache Log4j to log information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="a00f1-207">If you do not configure logging, the topology emits diagnostic information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="a00f1-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span><span class="sxs-lookup"><span data-stu-id="a00f1-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="a00f1-209">Use the following text as the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-209">Use the following text as the contents of the file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="a00f1-210">This configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-210">This configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="a00f1-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="a00f1-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="a00f1-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="a00f1-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="a00f1-214">Storm version 0.10.0 and higher use Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="a00f1-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="a00f1-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span><span class="sxs-lookup"><span data-stu-id="a00f1-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="a00f1-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="a00f1-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="a00f1-217">Test the topology locally</span><span class="sxs-lookup"><span data-stu-id="a00f1-217">Test the topology locally</span></span>

<span data-ttu-id="a00f1-218">After you save the files, use the following command to test the topology locally.</span><span class="sxs-lookup"><span data-stu-id="a00f1-218">After you save the files, use the following command to test the topology locally.</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology

<span data-ttu-id="a00f1-219">As it runs, the topology displays startup information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="a00f1-220">The following text is an example of the word count output:</span><span class="sxs-lookup"><span data-stu-id="a00f1-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="a00f1-221">By looking at the logging emitted by the WordCount bolt, you can see that 'and' has been emitted 113 times.</span><span class="sxs-lookup"><span data-stu-id="a00f1-221">By looking at the logging emitted by the WordCount bolt, you can see that 'and' has been emitted 113 times.</span></span> <span data-ttu-id="a00f1-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span><span class="sxs-lookup"><span data-stu-id="a00f1-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="a00f1-223">There is a 5-second interval between emission of words and counts.</span><span class="sxs-lookup"><span data-stu-id="a00f1-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="a00f1-224">The **WordCount** component is configured to only emit information when a tick tuple arrives, and it requests that such tuples are only delivered every five seconds by default.</span><span class="sxs-lookup"><span data-stu-id="a00f1-224">The **WordCount** component is configured to only emit information when a tick tuple arrives, and it requests that such tuples are only delivered every five seconds by default.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="a00f1-225">Convert the topology to Flux</span><span class="sxs-lookup"><span data-stu-id="a00f1-225">Convert the topology to Flux</span></span>

<span data-ttu-id="a00f1-226">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span><span class="sxs-lookup"><span data-stu-id="a00f1-226">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="a00f1-227">Your components (bolts and spouts) are still defined in Java, but the topology is defined using a YAML file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-227">Your components (bolts and spouts) are still defined in Java, but the topology is defined using a YAML file.</span></span>

<span data-ttu-id="a00f1-228">The YAML file defines the components to use for the topology, how data flows between them, and what values to use when initializing the components.</span><span class="sxs-lookup"><span data-stu-id="a00f1-228">The YAML file defines the components to use for the topology, how data flows between them, and what values to use when initializing the components.</span></span> <span data-ttu-id="a00f1-229">You can include a YAML file as part of the jar file or you can use an external YAML file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-229">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

> [!WARNING]
> <span data-ttu-id="a00f1-230">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span><span class="sxs-lookup"><span data-stu-id="a00f1-230">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="a00f1-231">Move the `WordCountTopology.java` file out of the project.</span><span class="sxs-lookup"><span data-stu-id="a00f1-231">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="a00f1-232">Previously, this file defined the topology, but isn't needed with Flux.</span><span class="sxs-lookup"><span data-stu-id="a00f1-232">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="a00f1-233">In the `resources` directory, create a file named `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-233">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="a00f1-234">Use the following text as the contents of this file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-234">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="a00f1-235">Make the following changes to the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="a00f1-235">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="a00f1-236">Add the following new dependency in the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="a00f1-236">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="a00f1-237">Add the following plugin to the `<plugins>` section.</span><span class="sxs-lookup"><span data-stu-id="a00f1-237">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="a00f1-238">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span><span class="sxs-lookup"><span data-stu-id="a00f1-238">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer to it as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * <span data-ttu-id="a00f1-239">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-239">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="a00f1-240">This setting allows Flux to handle running the topology locally in development.</span><span class="sxs-lookup"><span data-stu-id="a00f1-240">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="a00f1-241">In the `<resources>` section, add the following to the `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-241">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="a00f1-242">This includes the YAML file that defines the topology as part of the project.</span><span class="sxs-lookup"><span data-stu-id="a00f1-242">This includes the YAML file that defines the topology as part of the project.</span></span>
     
        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="a00f1-243">Test the flux topology locally</span><span class="sxs-lookup"><span data-stu-id="a00f1-243">Test the flux topology locally</span></span>

1. <span data-ttu-id="a00f1-244">Use the following to compile and execute the Flux topology using Maven:</span><span class="sxs-lookup"><span data-stu-id="a00f1-244">Use the following to compile and execute the Flux topology using Maven:</span></span>
   
        mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
   
    <span data-ttu-id="a00f1-245">If you are using PowerShell, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a00f1-245">If you are using PowerShell, use the following command:</span></span>
   
        mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"

    > [!WARNING]
    > <span data-ttu-id="a00f1-246">This command fails if your topology uses Storm 1.0.1 bits.</span><span class="sxs-lookup"><span data-stu-id="a00f1-246">This command fails if your topology uses Storm 1.0.1 bits.</span></span> <span data-ttu-id="a00f1-247">This is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="a00f1-247">This is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="a00f1-248">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-248">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>
   
    <span data-ttu-id="a00f1-249">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span><span class="sxs-lookup"><span data-stu-id="a00f1-249">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>
   
        mvn compile package
        storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
   
    <span data-ttu-id="a00f1-250">The `--local` parameter runs the topology in local mode on your development environment.</span><span class="sxs-lookup"><span data-stu-id="a00f1-250">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="a00f1-251">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-251">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>
   
    <span data-ttu-id="a00f1-252">As it runs, the topology displays startup information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-252">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="a00f1-253">The following text is an example of the output:</span><span class="sxs-lookup"><span data-stu-id="a00f1-253">The following text is an example of the output:</span></span>
   
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
   
    <span data-ttu-id="a00f1-254">There is a 10-second delay between batches of logged information.</span><span class="sxs-lookup"><span data-stu-id="a00f1-254">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="a00f1-255">Make a copy of the `topology.yaml` file from the project.</span><span class="sxs-lookup"><span data-stu-id="a00f1-255">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="a00f1-256">Name the new file `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-256">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="a00f1-257">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span><span class="sxs-lookup"><span data-stu-id="a00f1-257">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="a00f1-258">This changes the interval between emitting batches of word counts from 10 seconds to 5.</span><span class="sxs-lookup"><span data-stu-id="a00f1-258">This changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>
   
        - id: "counter-bolt"
        className: "com.microsoft.example.WordCount"
        constructorArgs:
        - 5
        parallelism: 1

3. <span data-ttu-id="a00f1-259">To run the topology, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a00f1-259">To run the topology, use the following command:</span></span>
   
        mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
   
    <span data-ttu-id="a00f1-260">Or, if you have Storm on your development environment:</span><span class="sxs-lookup"><span data-stu-id="a00f1-260">Or, if you have Storm on your development environment:</span></span>
   
        storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
   
    <span data-ttu-id="a00f1-261">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="a00f1-261">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="a00f1-262">This command uses the newtopology.yaml as the topology definition.</span><span class="sxs-lookup"><span data-stu-id="a00f1-262">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="a00f1-263">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span><span class="sxs-lookup"><span data-stu-id="a00f1-263">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>
   
    <span data-ttu-id="a00f1-264">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="a00f1-264">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="a00f1-265">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span><span class="sxs-lookup"><span data-stu-id="a00f1-265">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="a00f1-266">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="a00f1-266">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="a00f1-267">Trident</span><span class="sxs-lookup"><span data-stu-id="a00f1-267">Trident</span></span>

<span data-ttu-id="a00f1-268">Trident is a high-level abstraction that is provided by Storm.</span><span class="sxs-lookup"><span data-stu-id="a00f1-268">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="a00f1-269">It supports stateful processing.</span><span class="sxs-lookup"><span data-stu-id="a00f1-269">It supports stateful processing.</span></span> <span data-ttu-id="a00f1-270">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span><span class="sxs-lookup"><span data-stu-id="a00f1-270">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="a00f1-271">This is difficult to achieve in a Java topology, which guarantee's that messages are processed at least once.</span><span class="sxs-lookup"><span data-stu-id="a00f1-271">This is difficult to achieve in a Java topology, which guarantee's that messages are processed at least once.</span></span> <span data-ttu-id="a00f1-272">There are also other differences, such as built-in components that can be used instead of creating bolts.</span><span class="sxs-lookup"><span data-stu-id="a00f1-272">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="a00f1-273">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span><span class="sxs-lookup"><span data-stu-id="a00f1-273">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="a00f1-274">Trident applications can be created by using Maven projects.</span><span class="sxs-lookup"><span data-stu-id="a00f1-274">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="a00f1-275">You use the same basic steps as presented earlier in this article—only the code is different.</span><span class="sxs-lookup"><span data-stu-id="a00f1-275">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="a00f1-276">Trident also cannot (currently) be used with the Flux framework.</span><span class="sxs-lookup"><span data-stu-id="a00f1-276">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="a00f1-277">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="a00f1-277">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="a00f1-278">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="a00f1-278">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a00f1-279">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a00f1-279">Next Steps</span></span>

<span data-ttu-id="a00f1-280">You have learned how to create a Storm topology by using Java.</span><span class="sxs-lookup"><span data-stu-id="a00f1-280">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="a00f1-281">Now learn how to:</span><span class="sxs-lookup"><span data-stu-id="a00f1-281">Now learn how to:</span></span>

* [<span data-ttu-id="a00f1-282">Deploy and manage Apache Storm topologies on HDInsight</span><span class="sxs-lookup"><span data-stu-id="a00f1-282">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="a00f1-283">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a00f1-283">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="a00f1-284">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a00f1-284">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>


