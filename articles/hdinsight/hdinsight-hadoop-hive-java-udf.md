---
title: Use a Java user-defined function (UDF) with Hive in HDInsight | Microsoft Docs
description: Learn how to create and use a Java user-defined function (UDF) from Hive in HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: larryfr
ms.openlocfilehash: 9691b7ffb9c2bd9dd3f9900a29fb898652d8d7bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554572"
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Use a Java UDF with Hive in HDInsight

Learn how to create a Java-based user-defined function (UDF) that works with Hive.

## <a name="requirements"></a>Requirements

* An HDInsight cluster (Windows or Linux-based)

    > [!IMPORTANT]
    > Linux is the only operating system used on HDInsight version 3.4 or greater. For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).

    Most steps in this document work on both cluster types. However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters. Links are provided to information that can be used with Windows-based clusters.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* A text editor or Java IDE

    > [!IMPORTANT]
    > If you are using a Linux-based HDInsight server, but creating the Python files on a Windows client, you must use an editor that uses LF as a line ending. If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character using utilities on the HDInsight cluster.

## <a name="create-an-example-udf"></a>Create an example UDF

1. From a command line, use the following to create a new Maven project:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > If you are using PowerShell, you must put quotes around the parameters. For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    This command creates a directory named **exampleudf**, which contains the Maven project.

2. Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.

3. Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following:

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

    These entries specify the version of Hadoop and Hive included with HDInsight 3.5. You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.

    Add a `<build>` section before the `</project>` line at the end of the file. This section should contain the following:

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
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

    These entries define how to build the project. Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.

    Save the file once the changes have been made.

4. Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.

5. Replace the contents of the **ExampleUDF.java** file with the following, then save the file.

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

    This code implements a UDF that accepts a string value, and returns a lowercase version of the string.

## <a name="build-and-install-the-udf"></a>Build and install the UDF

1. Use the following command to compile and package the UDF:

    ```bash
    mvn compile package
    ```

    This builds and packages the UDF into **exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar**.

2. Use the `scp` command to copy the file to the HDInsight cluster.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Replace **myuser** with the SSH user account for your cluster. Replace **mycluster** with the cluster name. If you used a password to secure the SSH account, you are prompted to enter the password. If you used a certificate, you may need to use the `-i` parameter to specify the private key file.

3. Connect to the cluster using SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

4. From the SSH session, copy the jar file to HDInsight storage.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a>Use the UDF from Hive

1. Use the following to start the Beeline client from the SSH session.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    This command assumes that you used the default of **admin** for the login account for your cluster.

2. Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.

    ```hiveql
    ADD JAR wasbs:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > This example assumes that Azure Storage is default storage for the cluster. If your cluster uses Data Lake Store instead, change the `wasbs:///` value to `adl:///`.

3. Use the UDF to convert values retrieved from a table to lower case strings.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them. The output appears similar to the following.

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

## <a name="next-steps"></a>Next steps

For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).

For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.
