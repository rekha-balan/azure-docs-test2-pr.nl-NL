---
title: Develop Java MapReduce programs for Linux-based HDInsight | Microsoft Docs
description: Learn how to develop Java MapReduce programs and deploy them to Linux-based HDInsight.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: ''
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/17/2017
ms.author: larryfr
ms.openlocfilehash: a8623991dda4192d700d35ef3970d416e315c5c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549264"
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight-linux"></a><span data-ttu-id="2fd09-103">Develop Java MapReduce programs for Hadoop on HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="2fd09-103">Develop Java MapReduce programs for Hadoop on HDInsight Linux</span></span>

<span data-ttu-id="2fd09-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then deploy and run it on a Linux-based Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd09-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then deploy and run it on a Linux-based Hadoop on HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fd09-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2fd09-105">Prerequisites</span></span>

* <span data-ttu-id="2fd09-106">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)...</span><span class="sxs-lookup"><span data-stu-id="2fd09-106">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)...</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2fd09-107">HDInsight versions 3.4 and earlier use Java 7.</span><span class="sxs-lookup"><span data-stu-id="2fd09-107">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="2fd09-108">HDInsight 3.5 uses Java 8.</span><span class="sxs-lookup"><span data-stu-id="2fd09-108">HDInsight 3.5 uses Java 8.</span></span>

* [<span data-ttu-id="2fd09-109">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="2fd09-109">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="2fd09-110">**An Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="2fd09-110">**An Azure subscription**</span></span>

* <span data-ttu-id="2fd09-111">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="2fd09-111">**Azure CLI**</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="configure-environment-variables"></a><span data-ttu-id="2fd09-112">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="2fd09-112">Configure environment variables</span></span>
<span data-ttu-id="2fd09-113">The following environment variables may be set when you install Java and the JDK.</span><span class="sxs-lookup"><span data-stu-id="2fd09-113">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="2fd09-114">However, you should check that they exist and that they contain the correct values for your system.</span><span class="sxs-lookup"><span data-stu-id="2fd09-114">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="2fd09-115">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span><span class="sxs-lookup"><span data-stu-id="2fd09-115">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="2fd09-116">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="2fd09-116">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="2fd09-117">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="2fd09-117">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="2fd09-118">`PATH` - should contain the following paths:</span><span class="sxs-lookup"><span data-stu-id="2fd09-118">`PATH` - should contain the following paths:</span></span>
  
  * <span data-ttu-id="2fd09-119">`JAVA_HOME` (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="2fd09-119">`JAVA_HOME` (or the equivalent path)</span></span>

  * <span data-ttu-id="2fd09-120">`JAVA_HOME\bin` (or the equivalent path)</span><span class="sxs-lookup"><span data-stu-id="2fd09-120">`JAVA_HOME\bin` (or the equivalent path)</span></span>

  * <span data-ttu-id="2fd09-121">The directory where Maven is installed</span><span class="sxs-lookup"><span data-stu-id="2fd09-121">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="2fd09-122">Create a Maven project</span><span class="sxs-lookup"><span data-stu-id="2fd09-122">Create a Maven project</span></span>

1. <span data-ttu-id="2fd09-123">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span><span class="sxs-lookup"><span data-stu-id="2fd09-123">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span></span>

2. <span data-ttu-id="2fd09-124">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span><span class="sxs-lookup"><span data-stu-id="2fd09-124">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

   ```
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    <span data-ttu-id="2fd09-125">This command creates a directory with the name specified by the **artifactID** parameter (**wordcountjava** in this example.) This directory contains the following items:</span><span class="sxs-lookup"><span data-stu-id="2fd09-125">This command creates a directory with the name specified by the **artifactID** parameter (**wordcountjava** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="2fd09-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span><span class="sxs-lookup"><span data-stu-id="2fd09-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span></span>

   * <span data-ttu-id="2fd09-127">`src` - The directory that contains the application.</span><span class="sxs-lookup"><span data-stu-id="2fd09-127">`src` - The directory that contains the application.</span></span>

3. <span data-ttu-id="2fd09-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file, as it is not used in this example.</span><span class="sxs-lookup"><span data-stu-id="2fd09-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file, as it is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="2fd09-129">Add dependencies</span><span class="sxs-lookup"><span data-stu-id="2fd09-129">Add dependencies</span></span>

1. <span data-ttu-id="2fd09-130">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="2fd09-130">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span></span>
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.5.1</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.5.1</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.5.1</version>
        <scope>provided</scope>
    </dependency>
   ```

    <span data-ttu-id="2fd09-131">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="2fd09-131">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="2fd09-132">At compile time, these dependencies are downloaded from the default Maven repository.</span><span class="sxs-lookup"><span data-stu-id="2fd09-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="2fd09-133">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span><span class="sxs-lookup"><span data-stu-id="2fd09-133">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span></span>
   
    <span data-ttu-id="2fd09-134">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span><span class="sxs-lookup"><span data-stu-id="2fd09-134">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span></span>

2. <span data-ttu-id="2fd09-135">Add the following to the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="2fd09-135">Add the following to the `pom.xml` file.</span></span> <span data-ttu-id="2fd09-136">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span><span class="sxs-lookup"><span data-stu-id="2fd09-136">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
            <source>1.7</source>
            <target>1.7</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="2fd09-137">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span><span class="sxs-lookup"><span data-stu-id="2fd09-137">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span></span> <span data-ttu-id="2fd09-138">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span><span class="sxs-lookup"><span data-stu-id="2fd09-138">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="2fd09-139">The second plugin configures the target Java version.</span><span class="sxs-lookup"><span data-stu-id="2fd09-139">The second plugin configures the target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2fd09-140">HDInsight 3.4 and earlier use Java 7.</span><span class="sxs-lookup"><span data-stu-id="2fd09-140">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="2fd09-141">HDInsight 3.5 uses Java 8.</span><span class="sxs-lookup"><span data-stu-id="2fd09-141">HDInsight 3.5 uses Java 8.</span></span>

3. <span data-ttu-id="2fd09-142">Save the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="2fd09-142">Save the `pom.xml` file.</span></span>

## <a name="create-the-mapreduce-application"></a><span data-ttu-id="2fd09-143">Create the MapReduce application</span><span class="sxs-lookup"><span data-stu-id="2fd09-143">Create the MapReduce application</span></span>

1. <span data-ttu-id="2fd09-144">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="2fd09-144">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span></span>

2. <span data-ttu-id="2fd09-145">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span><span class="sxs-lookup"><span data-stu-id="2fd09-145">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span></span>
   
   ```java
   package org.apache.hadoop.examples;

   import java.io.IOException;
   import java.util.StringTokenizer;
   import org.apache.hadoop.conf.Configuration;
   import org.apache.hadoop.fs.Path;
   import org.apache.hadoop.io.IntWritable;
   import org.apache.hadoop.io.Text;
   import org.apache.hadoop.mapreduce.Job;
   import org.apache.hadoop.mapreduce.Mapper;
   import org.apache.hadoop.mapreduce.Reducer;
   import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
   import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
   import org.apache.hadoop.util.GenericOptionsParser;

   public class WordCount {

       public static class TokenizerMapper
           extends Mapper<Object, Text, Text, IntWritable>{

       private final static IntWritable one = new IntWritable(1);
       private Text word = new Text();

       public void map(Object key, Text value, Context context
                       ) throws IOException, InterruptedException {
           StringTokenizer itr = new StringTokenizer(value.toString());
           while (itr.hasMoreTokens()) {
           word.set(itr.nextToken());
           context.write(word, one);
           }
       }
   }

   public static class IntSumReducer
           extends Reducer<Text,IntWritable,Text,IntWritable> {
       private IntWritable result = new IntWritable();

       public void reduce(Text key, Iterable<IntWritable> values,
                           Context context
                           ) throws IOException, InterruptedException {
           int sum = 0;
           for (IntWritable val : values) {
           sum += val.get();
           }
          result.set(sum);
          context.write(key, result);
       }
   }

   public static void main(String[] args) throws Exception {
       Configuration conf = new Configuration();
       String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
       if (otherArgs.length != 2) {
           System.err.println("Usage: wordcount <in> <out>");
           System.exit(2);
       }
       Job job = new Job(conf, "word count");
       job.setJarByClass(WordCount.class);
       job.setMapperClass(TokenizerMapper.class);
       job.setCombinerClass(IntSumReducer.class);
       job.setReducerClass(IntSumReducer.class);
       job.setOutputKeyClass(Text.class);
       job.setOutputValueClass(IntWritable.class);
       FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
       FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
       System.exit(job.waitForCompletion(true) ? 0 : 1);
       }
   }
   ```
   
    <span data-ttu-id="2fd09-146">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="2fd09-146">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span></span> <span data-ttu-id="2fd09-147">You use these names when you submit the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="2fd09-147">You use these names when you submit the MapReduce job.</span></span>

3. <span data-ttu-id="2fd09-148">Save the file.</span><span class="sxs-lookup"><span data-stu-id="2fd09-148">Save the file.</span></span>

## <a name="build-the-application"></a><span data-ttu-id="2fd09-149">Build the application</span><span class="sxs-lookup"><span data-stu-id="2fd09-149">Build the application</span></span>

1. <span data-ttu-id="2fd09-150">Change to the `wordcountjava` directory, if you are not already there.</span><span class="sxs-lookup"><span data-stu-id="2fd09-150">Change to the `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="2fd09-151">Use the following command to build a JAR file containing the application:</span><span class="sxs-lookup"><span data-stu-id="2fd09-151">Use the following command to build a JAR file containing the application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="2fd09-152">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span><span class="sxs-lookup"><span data-stu-id="2fd09-152">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span></span>

3. <span data-ttu-id="2fd09-153">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="2fd09-153">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2fd09-154">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span><span class="sxs-lookup"><span data-stu-id="2fd09-154">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span></span>

## <a id="upload"></a><span data-ttu-id="2fd09-155">Upload the jar</span><span class="sxs-lookup"><span data-stu-id="2fd09-155">Upload the jar</span></span>

<span data-ttu-id="2fd09-156">Use the following command to upload the jar file to the HDInsight headnode:</span><span class="sxs-lookup"><span data-stu-id="2fd09-156">Use the following command to upload the jar file to the HDInsight headnode:</span></span>

   ```bash
   scp wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

<span data-ttu-id="2fd09-157">This command copies the files from the local system to the head node.</span><span class="sxs-lookup"><span data-stu-id="2fd09-157">This command copies the files from the local system to the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd09-158">If you used a password to secure your SSH account, you are prompted for the password.</span><span class="sxs-lookup"><span data-stu-id="2fd09-158">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="2fd09-159">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span><span class="sxs-lookup"><span data-stu-id="2fd09-159">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="2fd09-160">For example, `scp -i /path/to/private/key wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="2fd09-160">For example, `scp -i /path/to/private/key wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>


## <a name="run"></a><span data-ttu-id="2fd09-161">Run the MapReduce job</span><span class="sxs-lookup"><span data-stu-id="2fd09-161">Run the MapReduce job</span></span>

1. <span data-ttu-id="2fd09-162">Connect to HDInsight using SSH.</span><span class="sxs-lookup"><span data-stu-id="2fd09-162">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="2fd09-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2fd09-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2fd09-164">From the SSH session, use the following command to run the MapReduce application:</span><span class="sxs-lookup"><span data-stu-id="2fd09-164">From the SSH session, use the following command to run the MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="2fd09-165">This command starts the WordCount MapReduce application.</span><span class="sxs-lookup"><span data-stu-id="2fd09-165">This command starts the WordCount MapReduce application.</span></span> <span data-ttu-id="2fd09-166">The input file is **/example/data/gutenberg/davinci.txt**, and the output is stored in **/example/data/wordcountout**.</span><span class="sxs-lookup"><span data-stu-id="2fd09-166">The input file is **/example/data/gutenberg/davinci.txt**, and the output is stored in **/example/data/wordcountout**.</span></span> <span data-ttu-id="2fd09-167">Both the input file and output are stored to the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="2fd09-167">Both the input file and output are stored to the default storage for the cluster.</span></span>

3. <span data-ttu-id="2fd09-168">Once the job completes, use the following command to view the results:</span><span class="sxs-lookup"><span data-stu-id="2fd09-168">Once the job completes, use the following command to view the results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="2fd09-169">You should receive a list of words and counts, with values similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="2fd09-169">You should receive a list of words and counts, with values similar to the following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a><span data-ttu-id="2fd09-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fd09-170">Next steps</span></span>

<span data-ttu-id="2fd09-171">In this document, you have learned how to develop a Java MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="2fd09-171">In this document, you have learned how to develop a Java MapReduce job.</span></span> <span data-ttu-id="2fd09-172">See the following documents for other ways to work with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fd09-172">See the following documents for other ways to work with HDInsight.</span></span>

* <span data-ttu-id="2fd09-173">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2fd09-173">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2fd09-174">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2fd09-174">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="2fd09-175">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="2fd09-175">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="2fd09-176">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="2fd09-176">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

