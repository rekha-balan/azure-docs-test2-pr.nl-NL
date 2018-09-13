---
title: Java user-defined function (UDF) with Hive in HDInsight - Azure
description: Learn how to create a Java-based user-defined function (UDF) that works with Hive. This example UDF converts a table of text strings to lowercase.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: b2a4c7ce3ac91ade497ca59a8c2ca4fe642811a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966280"
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="217a9-104">Use a Java UDF with Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="217a9-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="217a9-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span><span class="sxs-lookup"><span data-stu-id="217a9-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="217a9-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span><span class="sxs-lookup"><span data-stu-id="217a9-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="217a9-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="217a9-107">Requirements</span></span>

* <span data-ttu-id="217a9-108">An HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="217a9-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="217a9-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="217a9-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="217a9-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="217a9-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="217a9-111">Most steps in this document work on both Windows- and Linux-based clusters.</span><span class="sxs-lookup"><span data-stu-id="217a9-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="217a9-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span><span class="sxs-lookup"><span data-stu-id="217a9-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="217a9-113">Links are provided to information that can be used with Windows-based clusters.</span><span class="sxs-lookup"><span data-stu-id="217a9-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="217a9-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="217a9-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="217a9-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="217a9-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="217a9-116">A text editor or Java IDE</span><span class="sxs-lookup"><span data-stu-id="217a9-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="217a9-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span><span class="sxs-lookup"><span data-stu-id="217a9-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="217a9-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span><span class="sxs-lookup"><span data-stu-id="217a9-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="217a9-119">Create an example Java UDF</span><span class="sxs-lookup"><span data-stu-id="217a9-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="217a9-120">From a command line, use the following to create a new Maven project:</span><span class="sxs-lookup"><span data-stu-id="217a9-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="217a9-121">If you are using PowerShell, you must put quotes around the parameters.</span><span class="sxs-lookup"><span data-stu-id="217a9-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="217a9-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="217a9-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="217a9-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span><span class="sxs-lookup"><span data-stu-id="217a9-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="217a9-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span><span class="sxs-lookup"><span data-stu-id="217a9-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="217a9-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span><span class="sxs-lookup"><span data-stu-id="217a9-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="217a9-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="217a9-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.6.</span></span> <span data-ttu-id="217a9-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](../hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="217a9-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](../hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="217a9-128">Add a `<build>` section before the `</project>` line at the end of the file.</span><span class="sxs-lookup"><span data-stu-id="217a9-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="217a9-129">This section should contain the following XML:</span><span class="sxs-lookup"><span data-stu-id="217a9-129">This section should contain the following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.6  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    <span data-ttu-id="217a9-130">These entries define how to build the project.</span><span class="sxs-lookup"><span data-stu-id="217a9-130">These entries define how to build the project.</span></span> <span data-ttu-id="217a9-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span><span class="sxs-lookup"><span data-stu-id="217a9-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="217a9-132">Save the file once the changes have been made.</span><span class="sxs-lookup"><span data-stu-id="217a9-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="217a9-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span><span class="sxs-lookup"><span data-stu-id="217a9-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="217a9-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span><span class="sxs-lookup"><span data-stu-id="217a9-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="217a9-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span><span class="sxs-lookup"><span data-stu-id="217a9-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="217a9-136">Build and install the UDF</span><span class="sxs-lookup"><span data-stu-id="217a9-136">Build and install the UDF</span></span>

1. <span data-ttu-id="217a9-137">Use the following command to compile and package the UDF:</span><span class="sxs-lookup"><span data-stu-id="217a9-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="217a9-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span><span class="sxs-lookup"><span data-stu-id="217a9-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="217a9-139">Use the `scp` command to copy the file to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="217a9-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="217a9-140">Replace `myuser` with the SSH user account for your cluster.</span><span class="sxs-lookup"><span data-stu-id="217a9-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="217a9-141">Replace `mycluster` with the cluster name.</span><span class="sxs-lookup"><span data-stu-id="217a9-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="217a9-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span><span class="sxs-lookup"><span data-stu-id="217a9-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="217a9-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span><span class="sxs-lookup"><span data-stu-id="217a9-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="217a9-144">Connect to the cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="217a9-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="217a9-145">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="217a9-145">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="217a9-146">From the SSH session, copy the jar file to HDInsight storage.</span><span class="sxs-lookup"><span data-stu-id="217a9-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="217a9-147">Use the UDF from Hive</span><span class="sxs-lookup"><span data-stu-id="217a9-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="217a9-148">Use the following to start the Beeline client from the SSH session.</span><span class="sxs-lookup"><span data-stu-id="217a9-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

    <span data-ttu-id="217a9-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span><span class="sxs-lookup"><span data-stu-id="217a9-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="217a9-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span><span class="sxs-lookup"><span data-stu-id="217a9-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="217a9-151">This example assumes that Azure Storage is default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="217a9-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="217a9-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="217a9-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="217a9-153">Use the UDF to convert values retrieved from a table to lower case strings.</span><span class="sxs-lookup"><span data-stu-id="217a9-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="217a9-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span><span class="sxs-lookup"><span data-stu-id="217a9-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="217a9-155">The output appears similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="217a9-155">The output appears similar to the following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="217a9-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="217a9-156">Next steps</span></span>

<span data-ttu-id="217a9-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="217a9-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="217a9-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span><span class="sxs-lookup"><span data-stu-id="217a9-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
