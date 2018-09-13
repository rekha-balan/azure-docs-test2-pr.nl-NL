---
title: Build a Java HBase application for Windows-based Azure HDInsight | Microsoft Docs
description: Learn how to use Apache Maven to build a Java-based Apache HBase application, then deploy it to a Windows-based Azure HDInsight cluster.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 0570e5eb36a5e7d85faf941e37c5fb5ee9970d80
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662958"
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="6fa97-103">Use Maven to build Java applications that use HBase with Windows-based HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="6fa97-103">Use Maven to build Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="6fa97-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="6fa97-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="6fa97-105">Then use the application with Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="6fa97-105">Then use the application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="6fa97-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span><span class="sxs-lookup"><span data-stu-id="6fa97-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="6fa97-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fa97-108">The steps in this document require an HDInsight cluster that uses Windows.</span><span class="sxs-lookup"><span data-stu-id="6fa97-108">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="6fa97-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="6fa97-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6fa97-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="6fa97-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="requirements"></a><span data-ttu-id="6fa97-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="6fa97-111">Requirements</span></span>
* <span data-ttu-id="6fa97-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span><span class="sxs-lookup"><span data-stu-id="6fa97-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="6fa97-113">Maven</span><span class="sxs-lookup"><span data-stu-id="6fa97-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="6fa97-114">A Windows-based HDInsight cluster with HBase</span><span class="sxs-lookup"><span data-stu-id="6fa97-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="6fa97-115">The steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span><span class="sxs-lookup"><span data-stu-id="6fa97-115">The steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="6fa97-116">The default values provided in examples are for a HDInsight 3.3 cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-116">The default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="6fa97-117">Create the project</span><span class="sxs-lookup"><span data-stu-id="6fa97-117">Create the project</span></span>
1. <span data-ttu-id="6fa97-118">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="6fa97-118">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="6fa97-119">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span><span class="sxs-lookup"><span data-stu-id="6fa97-119">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="6fa97-120">This command creates a directory in the current location, with the name specified by the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span><span class="sxs-lookup"><span data-stu-id="6fa97-120">This command creates a directory in the current location, with the name specified by the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="6fa97-121">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span><span class="sxs-lookup"><span data-stu-id="6fa97-121">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="6fa97-122">**src**: The directory that contains the **main\java\com\microsoft\examples** directory, where you will author the application.</span><span class="sxs-lookup"><span data-stu-id="6fa97-122">**src**: The directory that contains the **main\java\com\microsoft\examples** directory, where you will author the application.</span></span>
3. <span data-ttu-id="6fa97-123">Delete the **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span><span class="sxs-lookup"><span data-stu-id="6fa97-123">Delete the **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="6fa97-124">Update the Project Object Model</span><span class="sxs-lookup"><span data-stu-id="6fa97-124">Update the Project Object Model</span></span>
1. <span data-ttu-id="6fa97-125">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="6fa97-125">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="6fa97-126">This section tells Maven that the project requires **hbase-client** version **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-126">This section tells Maven that the project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="6fa97-127">At compile time, this dependency is downloaded from the default Maven repository.</span><span class="sxs-lookup"><span data-stu-id="6fa97-127">At compile time, this dependency is downloaded from the default Maven repository.</span></span> <span data-ttu-id="6fa97-128">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span><span class="sxs-lookup"><span data-stu-id="6fa97-128">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6fa97-129">The version number must match the version of HBase that is provided with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-129">The version number must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="6fa97-130">Use the following table to find the correct version number.</span><span class="sxs-lookup"><span data-stu-id="6fa97-130">Use the following table to find the correct version number.</span></span>
   >
   >

   | <span data-ttu-id="6fa97-131">HDInsight cluster version</span><span class="sxs-lookup"><span data-stu-id="6fa97-131">HDInsight cluster version</span></span> | <span data-ttu-id="6fa97-132">HBase version to use</span><span class="sxs-lookup"><span data-stu-id="6fa97-132">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="6fa97-133">3.2</span><span class="sxs-lookup"><span data-stu-id="6fa97-133">3.2</span></span> |<span data-ttu-id="6fa97-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="6fa97-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="6fa97-135">3.3</span><span class="sxs-lookup"><span data-stu-id="6fa97-135">3.3</span></span> |<span data-ttu-id="6fa97-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="6fa97-136">1.1.2</span></span> |

    <span data-ttu-id="6fa97-137">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6fa97-137">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="6fa97-138">If you are using an HDInsight 3.3 cluster, you must also add the following to the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="6fa97-138">If you are using an HDInsight 3.3 cluster, you must also add the following to the `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="6fa97-139">This dependency will load the phoenix-core components, which are used by Hbase version 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="6fa97-139">This dependency will load the phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="6fa97-140">Add the following code to the **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-140">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="6fa97-141">This section must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span><span class="sxs-lookup"><span data-stu-id="6fa97-141">This section must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

        <build>
          <sourceDirectory>src</sourceDirectory>
          <resources>
              <resource>
                <directory>${basedir}/conf</directory>
                <filtering>false</filtering>
                <includes>
                  <include>hbase-site.xml</include>
                </includes>
              </resource>
            </resources>
          <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                </configuration>
              </plugin>
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
          </plugins>
        </build>

    <span data-ttu-id="6fa97-142">The `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span><span class="sxs-lookup"><span data-stu-id="6fa97-142">The `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6fa97-143">You can also set configuration values via code.</span><span class="sxs-lookup"><span data-stu-id="6fa97-143">You can also set configuration values via code.</span></span> <span data-ttu-id="6fa97-144">See the comments in the **CreateTable** example that follows for how to do this.</span><span class="sxs-lookup"><span data-stu-id="6fa97-144">See the comments in the **CreateTable** example that follows for how to do this.</span></span>
   >
   >

    <span data-ttu-id="6fa97-145">This `<plugins>` section configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="6fa97-145">This `<plugins>` section configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="6fa97-146">The compiler plug-in is used to compile the topology.</span><span class="sxs-lookup"><span data-stu-id="6fa97-146">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="6fa97-147">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span><span class="sxs-lookup"><span data-stu-id="6fa97-147">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="6fa97-148">The reason this is used is that the duplicate license files cause an error at run time on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-148">The reason this is used is that the duplicate license files cause an error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="6fa97-149">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents this error.</span><span class="sxs-lookup"><span data-stu-id="6fa97-149">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="6fa97-150">The maven-shade-plugin also produces an uber jar (or fat jar) that contains all the dependencies required by the application.</span><span class="sxs-lookup"><span data-stu-id="6fa97-150">The maven-shade-plugin also produces an uber jar (or fat jar) that contains all the dependencies required by the application.</span></span>
4. <span data-ttu-id="6fa97-151">Save the **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-151">Save the **pom.xml** file.</span></span>
5. <span data-ttu-id="6fa97-152">Create a new directory named **conf** in the **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="6fa97-152">Create a new directory named **conf** in the **hbaseapp** directory.</span></span> <span data-ttu-id="6fa97-153">In the **conf** directory, create a file named **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-153">In the **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="6fa97-154">Use the following as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="6fa97-154">Use the following as the contents of the file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 The Apache Software Foundation
          *
          * Licensed to the Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See the NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  The ASF licenses this file
          * to you under the Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with the License.  You may obtain a copy of the License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed to in writing, software
          * distributed under the License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See the License for the specific language governing permissions and
          * limitations under the License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="6fa97-155">This file will be used to load the HBase configuration for an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-155">This file will be used to load the HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6fa97-156">This is a minimal hbase-site.xml file, and it contains the bare minimum settings for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-156">This is a minimal hbase-site.xml file, and it contains the bare minimum settings for the HDInsight cluster.</span></span>

6. <span data-ttu-id="6fa97-157">Save the **hbase-site.xml** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-157">Save the **hbase-site.xml** file.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="6fa97-158">Create the application</span><span class="sxs-lookup"><span data-stu-id="6fa97-158">Create the application</span></span>
1. <span data-ttu-id="6fa97-159">Go to the **hbaseapp\src\main\java\com\microsoft\examples** directory and rename the app.java file to **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-159">Go to the **hbaseapp\src\main\java\com\microsoft\examples** directory and rename the app.java file to **CreateTable.java**.</span></span>
2. <span data-ttu-id="6fa97-160">Open the **CreateTable.java** file and replace the existing contents with the following code:</span><span class="sxs-lookup"><span data-stu-id="6fa97-160">Open the **CreateTable.java** file and replace the existing contents with the following code:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;
        import org.apache.hadoop.hbase.HTableDescriptor;
        import org.apache.hadoop.hbase.TableName;
        import org.apache.hadoop.hbase.HColumnDescriptor;
        import org.apache.hadoop.hbase.client.HTable;
        import org.apache.hadoop.hbase.client.Put;
        import org.apache.hadoop.hbase.util.Bytes;

        public class CreateTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Example of setting zookeeper values for HDInsight
            // in code instead of an hbase-site.xml file
            //
            // config.set("hbase.zookeeper.quorum",
            //            "zookeepernode0,zookeepernode1,zookeepernode2");
            //config.set("hbase.zookeeper.property.clientPort", "2181");
            //config.set("hbase.cluster.distributed", "true");
            // The following sets the znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

            // create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // create the table...
            HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
            // ... with two column families
            tableDescriptor.addFamily(new HColumnDescriptor("name"));
            tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
            admin.createTable(tableDescriptor);

            // define some people
            String[][] people = {
                { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
                { "2", "Franklin", "Holtz", "franklin@contoso.com" },
                { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
                { "4", "Rae", "Schroeder", "rae@contoso.com" },
                { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
                { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

            HTable table = new HTable(config, "people");

            // Add each person to the table
            //   Use the `name` column family for the name
            //   Use the `contactinfo` column family for the email
            for (int i = 0; i< people.length; i++) {
              Put person = new Put(Bytes.toBytes(people[i][0]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
              person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
              table.put(person);
            }
            // flush commits and close the table
            table.flushCommits();
            table.close();
          }
        }

    <span data-ttu-id="6fa97-161">This is the **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span><span class="sxs-lookup"><span data-stu-id="6fa97-161">This is the **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="6fa97-162">Save the **CreateTable.java** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-162">Save the **CreateTable.java** file.</span></span>
4. <span data-ttu-id="6fa97-163">In the **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-163">In the **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="6fa97-164">Use the following code as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="6fa97-164">Use the following code as the contents of this file:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HTable;
        import org.apache.hadoop.hbase.client.Scan;
        import org.apache.hadoop.hbase.client.ResultScanner;
        import org.apache.hadoop.hbase.client.Result;
        import org.apache.hadoop.hbase.filter.RegexStringComparator;
        import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
        import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
        import org.apache.hadoop.hbase.util.Bytes;
        import org.apache.hadoop.util.GenericOptionsParser;

        public class SearchByEmail {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Use GenericOptionsParser to get only the parameters to the class
            // and not all the parameters passed (when using WebHCat for example)
            String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
            if (otherArgs.length != 1) {
              System.out.println("usage: [regular expression]");
              System.exit(-1);
            }

            // Open the table
            HTable table = new HTable(config, "people");

            // Define the family and qualifiers to be used
            byte[] contactFamily = Bytes.toBytes("contactinfo");
            byte[] emailQualifier = Bytes.toBytes("email");
            byte[] nameFamily = Bytes.toBytes("name");
            byte[] firstNameQualifier = Bytes.toBytes("first");
            byte[] lastNameQualifier = Bytes.toBytes("last");

            // Create a new regex filter
            RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
            // Attach the regex filter to a filter
            //   for the email column
            SingleColumnValueFilter filter = new SingleColumnValueFilter(
              contactFamily,
              emailQualifier,
              CompareOp.EQUAL,
              emailFilter
            );

            // Create a scan and set the filter
            Scan scan = new Scan();
            scan.setFilter(filter);

            // Get the results
            ResultScanner results = table.getScanner(scan);
            // Iterate over results and print  values
            for (Result result : results ) {
              String id = new String(result.getRow());
              byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
              String firstName = new String(firstNameObj);
              byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
              String lastName = new String(lastNameObj);
              System.out.println(firstName + " " + lastName + " - ID: " + id);
              byte[] emailObj = result.getValue(contactFamily, emailQualifier);
              String email = new String(emailObj);
              System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
            }
            results.close();
            table.close();
          }
        }

    <span data-ttu-id="6fa97-165">The **SearchByEmail** class can be used to query for rows by email address.</span><span class="sxs-lookup"><span data-stu-id="6fa97-165">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="6fa97-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span><span class="sxs-lookup"><span data-stu-id="6fa97-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>
5. <span data-ttu-id="6fa97-167">Save the **SearchByEmail.java** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-167">Save the **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="6fa97-168">In the **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-168">In the **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="6fa97-169">Use the following code as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="6fa97-169">Use the following code as the contents of this file:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;

        public class DeleteTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // Disable, and then delete the table
            admin.disableTable("people");
            admin.deleteTable("people");
          }
        }

    <span data-ttu-id="6fa97-170">This class is for cleaning up this example by disabling and dropping the table created by the **CreateTable** class.</span><span class="sxs-lookup"><span data-stu-id="6fa97-170">This class is for cleaning up this example by disabling and dropping the table created by the **CreateTable** class.</span></span>
7. <span data-ttu-id="6fa97-171">Save the **DeleteTable.java** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-171">Save the **DeleteTable.java** file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="6fa97-172">Build and package the application</span><span class="sxs-lookup"><span data-stu-id="6fa97-172">Build and package the application</span></span>
1. <span data-ttu-id="6fa97-173">Open a command prompt and change directories to the **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="6fa97-173">Open a command prompt and change directories to the **hbaseapp** directory.</span></span>
2. <span data-ttu-id="6fa97-174">Use the following command to build a JAR file that contains the application:</span><span class="sxs-lookup"><span data-stu-id="6fa97-174">Use the following command to build a JAR file that contains the application:</span></span>

        mvn clean package

    <span data-ttu-id="6fa97-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span><span class="sxs-lookup"><span data-stu-id="6fa97-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span></span>
3. <span data-ttu-id="6fa97-176">When the command completes, the **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-176">When the command completes, the **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6fa97-177">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all the dependencies required to run the application.</span><span class="sxs-lookup"><span data-stu-id="6fa97-177">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all the dependencies required to run the application.</span></span>

## <a name="upload-the-jar-file-and-start-a-job"></a><span data-ttu-id="6fa97-178">Upload the JAR file and start a job</span><span class="sxs-lookup"><span data-stu-id="6fa97-178">Upload the JAR file and start a job</span></span>
<span data-ttu-id="6fa97-179">There are many ways to upload a file to your HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="6fa97-179">There are many ways to upload a file to your HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="6fa97-180">The following steps use Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fa97-180">The following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="6fa97-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="6fa97-182">Use the following as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="6fa97-182">Use the following as the contents of this file:</span></span>

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
        .EXAMPLE
        Start-HBaseExample -className "com.microsoft.examples.CreateTable"
        -clusterName "MyHDInsightCluster"

        .EXAMPLE
        Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
        -clusterName "MyHDInsightCluster"
        -emailRegex "contoso.com"

        .EXAMPLE
        Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
        -clusterName "MyHDInsightCluster"
        -emailRegex "^r" -showErr
        #>

        function Start-HBaseExample {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
        #The class to run
        [Parameter(Mandatory = $true)]
        [String]$className,

        #The name of the HDInsight cluster
        [Parameter(Mandatory = $true)]
        [String]$clusterName,

        #Only used when using SearchByEmail
        [Parameter(Mandatory = $false)]
        [String]$emailRegex,

        #Use if you want to see stderr output
        [Parameter(Mandatory = $false)]
        [Switch]$showErr
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get the login for the HDInsight cluster
        $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

        # The JAR
        $jarFile = "wasbs:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

        # The job definition
        $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
            -JarFile $jarFile `
            -ClassName $className `
            -Arguments $emailRegex

        # Get the job output
        $job = Start-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobDefinition $jobDefinition `
            -HttpCredential $creds
        Write-Host "Wait for the job to complete ..." -ForegroundColor Green
        Wait-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobId $job.JobId `
            -HttpCredential $creds
        if($showErr)
        {
        Write-Host "STDERR"
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds `
                    -DisplayOutputType StandardError
        }
        Write-Host "Display the standard output ..." -ForegroundColor Green
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds
        }

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
        .EXAMPLE
        Add-HDInsightFile -localPath "C:\temp\data.txt"
        -destinationPath "example/data/data.txt"
        -ClusterName "MyHDInsightCluster"
        .EXAMPLE
        Add-HDInsightFile -localPath "C:\temp\data.txt"
        -destinationPath "example/data/data.txt"
        -ClusterName "MyHDInsightCluster"
        -Container "MyContainer"
        #>

        function Add-HDInsightFile {
            [CmdletBinding(SupportsShouldProcess = $true)]
            param(
                #The path to the local file.
                [Parameter(Mandatory = $true)]
                [String]$localPath,

                #The destination path and file name, relative to the root of the container.
                [Parameter(Mandatory = $true)]
                [String]$destinationPath,

                #The name of the HDInsight cluster
                [Parameter(Mandatory = $true)]
                [String]$clusterName,

                #If specified, overwrites existing files without prompting
                [Parameter(Mandatory = $false)]
                [Switch]$force
            )

            Set-StrictMode -Version 3

            # Is the Azure module installed?
            FindAzure

            # Get authentication for the cluster
            $creds=Get-Credential

            # Does the local path exist?
            if (-not (Test-Path $localPath))
            {
                throw "Source path '$localPath' does not exist."
            }

            # Get the primary storage container
            $storage = GetStorage -clusterName $clusterName

            # Upload file to storage, overwriting existing files if -force was used.
            Set-AzureStorageBlobContent -File $localPath `
                -Blob $destinationPath `
                -force:$force `
                -Container $storage.container `
                -Context $storage.context
        }

        function FindAzure {
            # Is there an active Azure subscription?
            $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
            if(-not($sub))
            {
                throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
            }
        }

        function GetStorage {
            param(
                [Parameter(Mandatory = $true)]
                [String]$clusterName
            )
            $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
            # Does the cluster exist?
            if (!$hdi)
            {
                throw "HDInsight cluster '$clusterName' does not exist."
            }
            # Create a return object for context & container
            $return = @{}
            $storageAccounts = @{}

            # Get storage information
            $resourceGroup = $hdi.ResourceGroup
            $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
            $container=$hdi.DefaultStorageContainer
            $storageAccountKey=(Get-AzureRmStorageAccountKey `
                -Name $storageAccountName `
            -ResourceGroupName $resourceGroup)[0].Value
            # Get the resource group, in case we need that
            $return.resourceGroup = $resourceGroup
            # Get the storage context, as we can't depend
            # on using the default storage context
            $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
            # Get the container, so we know where to
            # find/store blobs
            $return.container = $container
            # Return storage accounts to support finding all accounts for
            # a cluster
            $return.storageAccount = $storageAccountName
            $return.storageAccountKey = $storageAccountKey

            return $return
        }
        # Only export the verb-phrase things
        export-modulemember *-*

    <span data-ttu-id="6fa97-183">This file contains two modules:</span><span class="sxs-lookup"><span data-stu-id="6fa97-183">This file contains two modules:</span></span>

   * <span data-ttu-id="6fa97-184">**Add-HDInsightFile** - used to upload files to HDInsight</span><span class="sxs-lookup"><span data-stu-id="6fa97-184">**Add-HDInsightFile** - used to upload files to HDInsight</span></span>
   * <span data-ttu-id="6fa97-185">**Start-HBaseExample** - used to run the classes created earlier</span><span class="sxs-lookup"><span data-stu-id="6fa97-185">**Start-HBaseExample** - used to run the classes created earlier</span></span>
2. <span data-ttu-id="6fa97-186">Save the **hbase-runner.psm1** file.</span><span class="sxs-lookup"><span data-stu-id="6fa97-186">Save the **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="6fa97-187">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command.</span><span class="sxs-lookup"><span data-stu-id="6fa97-187">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="6fa97-188">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span><span class="sxs-lookup"><span data-stu-id="6fa97-188">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="6fa97-189">This registers the module for this Azure PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="6fa97-189">This registers the module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="6fa97-190">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-190">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="6fa97-191">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-191">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="6fa97-192">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-192">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="6fa97-193">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="6fa97-193">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="6fa97-194">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-194">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="6fa97-195">This command creates a new table named **people** in your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="6fa97-196">This command does not show any output in the console window.</span><span class="sxs-lookup"><span data-stu-id="6fa97-196">This command does not show any output in the console window.</span></span>
6. <span data-ttu-id="6fa97-197">To search for entries in the table, use the following command:</span><span class="sxs-lookup"><span data-stu-id="6fa97-197">To search for entries in the table, use the following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="6fa97-198">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-198">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="6fa97-199">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="6fa97-199">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span></span> <span data-ttu-id="6fa97-200">You should receive the following results:</span><span class="sxs-lookup"><span data-stu-id="6fa97-200">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="6fa97-201">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span><span class="sxs-lookup"><span data-stu-id="6fa97-201">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="6fa97-202">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where the email begins with the letter 'r'.</span><span class="sxs-lookup"><span data-stu-id="6fa97-202">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where the email begins with the letter 'r'.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="6fa97-203">Delete the table</span><span class="sxs-lookup"><span data-stu-id="6fa97-203">Delete the table</span></span>
<span data-ttu-id="6fa97-204">When you are done with the example, use the following command from the Azure PowerShell session to delete the **people** table used in this example:</span><span class="sxs-lookup"><span data-stu-id="6fa97-204">When you are done with the example, use the following command from the Azure PowerShell session to delete the **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="6fa97-205">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6fa97-205">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6fa97-206">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="6fa97-206">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="6fa97-207">No results or unexpected results when using Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="6fa97-207">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="6fa97-208">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span><span class="sxs-lookup"><span data-stu-id="6fa97-208">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>
