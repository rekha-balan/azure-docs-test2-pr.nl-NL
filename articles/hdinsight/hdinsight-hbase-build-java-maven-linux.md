---
title: Build a Java HBase application for Azure HDInsight | Microsoft Docs
description: Learn how to use Apache Maven to build a Java-based Apache HBase application, then deploy it to Linux-based HDInsight in the Azure cloud.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: ''
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: larryfr
ms.openlocfilehash: ce83fe64c4922b0e420f447e5b9db04c824412a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661635"
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-linux-based-hdinsight-hadoop"></a><span data-ttu-id="0dd31-103">Use Maven to build Java applications that use HBase with Linux-based HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="0dd31-103">Use Maven to build Java applications that use HBase with Linux-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="0dd31-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="0dd31-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="0dd31-105">Then use the application with a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-105">Then use the application with a Linux-based HDInsight cluster.</span></span>

<span data-ttu-id="0dd31-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span><span class="sxs-lookup"><span data-stu-id="0dd31-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="0dd31-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on a Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dd31-108">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="0dd31-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="0dd31-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="0dd31-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0dd31-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="0dd31-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="requirements"></a><span data-ttu-id="0dd31-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="0dd31-111">Requirements</span></span>

* <span data-ttu-id="0dd31-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span><span class="sxs-lookup"><span data-stu-id="0dd31-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0dd31-113">HDInsight 3.5 requires Java 8.</span><span class="sxs-lookup"><span data-stu-id="0dd31-113">HDInsight 3.5 requires Java 8.</span></span> <span data-ttu-id="0dd31-114">Earlier versions of HDInsight require Java 7.</span><span class="sxs-lookup"><span data-stu-id="0dd31-114">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="0dd31-115">Maven</span><span class="sxs-lookup"><span data-stu-id="0dd31-115">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="0dd31-116">A Linux-based Azure HDInsight cluster with HBase</span><span class="sxs-lookup"><span data-stu-id="0dd31-116">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="0dd31-117">The steps in this document have been tested with HDInsight cluster versions 3.2, 3.3, 3.4 and 3.5.</span><span class="sxs-lookup"><span data-stu-id="0dd31-117">The steps in this document have been tested with HDInsight cluster versions 3.2, 3.3, 3.4 and 3.5.</span></span> <span data-ttu-id="0dd31-118">The default values provided in examples are for a HDInsight 3.5 cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-118">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

* <span data-ttu-id="0dd31-119">**Familiarity with SSH and SCP** or **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-119">**Familiarity with SSH and SCP** or **Azure PowerShell**.</span></span> <span data-ttu-id="0dd31-120">This document provides steps for using both SSH/SCP and Azure PowerShell when running this example.</span><span class="sxs-lookup"><span data-stu-id="0dd31-120">This document provides steps for using both SSH/SCP and Azure PowerShell when running this example.</span></span>

    <span data-ttu-id="0dd31-121">For information on installing Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="0dd31-121">For information on installing Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

    <span data-ttu-id="0dd31-122">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0dd31-122">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="0dd31-123">Create the project</span><span class="sxs-lookup"><span data-stu-id="0dd31-123">Create the project</span></span>

1. <span data-ttu-id="0dd31-124">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code/hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="0dd31-124">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code/hdinsight`.</span></span>

2. <span data-ttu-id="0dd31-125">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span><span class="sxs-lookup"><span data-stu-id="0dd31-125">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="0dd31-126">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span><span class="sxs-lookup"><span data-stu-id="0dd31-126">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="0dd31-127">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span><span class="sxs-lookup"><span data-stu-id="0dd31-127">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="0dd31-128">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span><span class="sxs-lookup"><span data-stu-id="0dd31-128">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="0dd31-129">Delete the **src/test/java/com/microsoft/examples/apptest.java** file because it is not be used in this example.</span><span class="sxs-lookup"><span data-stu-id="0dd31-129">Delete the **src/test/java/com/microsoft/examples/apptest.java** file because it is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="0dd31-130">Update the Project Object Model</span><span class="sxs-lookup"><span data-stu-id="0dd31-130">Update the Project Object Model</span></span>

1. <span data-ttu-id="0dd31-131">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="0dd31-131">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
   ```

    <span data-ttu-id="0dd31-132">This section indicates that the project needs **hbase-client** version **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-132">This section indicates that the project needs **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="0dd31-133">At compile time, this dependency is downloaded from the default Maven repository.</span><span class="sxs-lookup"><span data-stu-id="0dd31-133">At compile time, this dependency is downloaded from the default Maven repository.</span></span> <span data-ttu-id="0dd31-134">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span><span class="sxs-lookup"><span data-stu-id="0dd31-134">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0dd31-135">The version number must match the version of HBase that is provided with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-135">The version number must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="0dd31-136">Use the following table to find the correct version number.</span><span class="sxs-lookup"><span data-stu-id="0dd31-136">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="0dd31-137">HDInsight cluster version</span><span class="sxs-lookup"><span data-stu-id="0dd31-137">HDInsight cluster version</span></span> | <span data-ttu-id="0dd31-138">HBase version to use</span><span class="sxs-lookup"><span data-stu-id="0dd31-138">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="0dd31-139">3.2</span><span class="sxs-lookup"><span data-stu-id="0dd31-139">3.2</span></span> |<span data-ttu-id="0dd31-140">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="0dd31-140">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="0dd31-141">3.3, 3.4 and 3.5</span><span class="sxs-lookup"><span data-stu-id="0dd31-141">3.3, 3.4 and 3.5</span></span> |<span data-ttu-id="0dd31-142">1.1.2</span><span class="sxs-lookup"><span data-stu-id="0dd31-142">1.1.2</span></span> |

    <span data-ttu-id="0dd31-143">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0dd31-143">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

2. <span data-ttu-id="0dd31-144">If you are using an HDInsight 3.3, 3.4 or 3.5 cluster, you must also add the following to the `<dependencies>` section:</span><span class="sxs-lookup"><span data-stu-id="0dd31-144">If you are using an HDInsight 3.3, 3.4 or 3.5 cluster, you must also add the following to the `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="0dd31-145">This section loads the phoenix-core components, which are needed with Hbase version 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="0dd31-145">This section loads the phoenix-core components, which are needed with Hbase version 1.1.x.</span></span>

3. <span data-ttu-id="0dd31-146">Add the following code to the **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-146">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="0dd31-147">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span><span class="sxs-lookup"><span data-stu-id="0dd31-147">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
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
                <source>1.8</source>
                <target>1.8</target>
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
   ```

    <span data-ttu-id="0dd31-148">This section configures a resource (**conf/hbase-site.xml**) that contains configuration information for HBase.</span><span class="sxs-lookup"><span data-stu-id="0dd31-148">This section configures a resource (**conf/hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0dd31-149">You can also set configuration values via code.</span><span class="sxs-lookup"><span data-stu-id="0dd31-149">You can also set configuration values via code.</span></span> <span data-ttu-id="0dd31-150">See the comments in the **CreateTable** example.</span><span class="sxs-lookup"><span data-stu-id="0dd31-150">See the comments in the **CreateTable** example.</span></span>

    <span data-ttu-id="0dd31-151">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="0dd31-151">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="0dd31-152">The compiler plug-in is used to compile the topology.</span><span class="sxs-lookup"><span data-stu-id="0dd31-152">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="0dd31-153">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span><span class="sxs-lookup"><span data-stu-id="0dd31-153">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="0dd31-154">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-154">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="0dd31-155">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span><span class="sxs-lookup"><span data-stu-id="0dd31-155">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="0dd31-156">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span><span class="sxs-lookup"><span data-stu-id="0dd31-156">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="0dd31-157">Save the **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-157">Save the **pom.xml** file.</span></span>

5. <span data-ttu-id="0dd31-158">Create a directory named **conf** in the **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="0dd31-158">Create a directory named **conf** in the **hbaseapp** directory.</span></span> <span data-ttu-id="0dd31-159">This directory is used to hold configuration information for connecting to HBase.</span><span class="sxs-lookup"><span data-stu-id="0dd31-159">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="0dd31-160">Use the following command to copy the HBase configuration from the HDInsight server to the **conf** directory.</span><span class="sxs-lookup"><span data-stu-id="0dd31-160">Use the following command to copy the HBase configuration from the HDInsight server to the **conf** directory.</span></span> <span data-ttu-id="0dd31-161">Replace **USERNAME** with the name of your SSH login.</span><span class="sxs-lookup"><span data-stu-id="0dd31-161">Replace **USERNAME** with the name of your SSH login.</span></span> <span data-ttu-id="0dd31-162">Replace **CLUSTERNAME** with your HDInsight cluster name:</span><span class="sxs-lookup"><span data-stu-id="0dd31-162">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml

   > [!NOTE]
   > <span data-ttu-id="0dd31-163">If you used a password for your SSH account, you are prompted to enter the password.</span><span class="sxs-lookup"><span data-stu-id="0dd31-163">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="0dd31-164">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-164">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="0dd31-165">The following example loads the private key from `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="0dd31-165">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
   >
   > `scp -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml`


## <a name="create-the-application"></a><span data-ttu-id="0dd31-166">Create the application</span><span class="sxs-lookup"><span data-stu-id="0dd31-166">Create the application</span></span>

1. <span data-ttu-id="0dd31-167">Go to the **hbaseapp/src/main/java/com/microsoft/examples** directory and rename the app.java file to **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-167">Go to the **hbaseapp/src/main/java/com/microsoft/examples** directory and rename the app.java file to **CreateTable.java**.</span></span>

2. <span data-ttu-id="0dd31-168">Open the **CreateTable.java** file and replace the existing contents with the following text:</span><span class="sxs-lookup"><span data-stu-id="0dd31-168">Open the **CreateTable.java** file and replace the existing contents with the following text:</span></span>

   ```java
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
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

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
   ```

    <span data-ttu-id="0dd31-169">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span><span class="sxs-lookup"><span data-stu-id="0dd31-169">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="0dd31-170">Save the **CreateTable.java** file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-170">Save the **CreateTable.java** file.</span></span>

4. <span data-ttu-id="0dd31-171">In the **hbaseapp/src/main/java/com/microsoft/examples** directory, create a file named **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-171">In the **hbaseapp/src/main/java/com/microsoft/examples** directory, create a file named **SearchByEmail.java**.</span></span> <span data-ttu-id="0dd31-172">Use the following text as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="0dd31-172">Use the following text as the contents of this file:</span></span>

   ```java
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

        // Create a regex filter
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
   ```

    <span data-ttu-id="0dd31-173">The **SearchByEmail** class can be used to query for rows by email address.</span><span class="sxs-lookup"><span data-stu-id="0dd31-173">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="0dd31-174">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span><span class="sxs-lookup"><span data-stu-id="0dd31-174">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="0dd31-175">Save the **SearchByEmail.java** file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-175">Save the **SearchByEmail.java** file.</span></span>

6. <span data-ttu-id="0dd31-176">In the **hbaseapp/src/main/hava/com/microsoft/examples** directory, create a file named **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-176">In the **hbaseapp/src/main/hava/com/microsoft/examples** directory, create a file named **DeleteTable.java**.</span></span> <span data-ttu-id="0dd31-177">Use the following text as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="0dd31-177">Use the following text as the contents of this file:</span></span>

   ```java
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
   ```

    <span data-ttu-id="0dd31-178">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the **CreateTable** class.</span><span class="sxs-lookup"><span data-stu-id="0dd31-178">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the **CreateTable** class.</span></span>

7. <span data-ttu-id="0dd31-179">Save the **DeleteTable.java** file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-179">Save the **DeleteTable.java** file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="0dd31-180">Build and package the application</span><span class="sxs-lookup"><span data-stu-id="0dd31-180">Build and package the application</span></span>

1. <span data-ttu-id="0dd31-181">From the **hbaseapp** directory, use the following command to build a JAR file that contains the application:</span><span class="sxs-lookup"><span data-stu-id="0dd31-181">From the **hbaseapp** directory, use the following command to build a JAR file that contains the application:</span></span>

        mvn clean package

    <span data-ttu-id="0dd31-182">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span><span class="sxs-lookup"><span data-stu-id="0dd31-182">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span></span>

2. <span data-ttu-id="0dd31-183">When the command completes, the **hbaseapp/target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-183">When the command completes, the **hbaseapp/target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0dd31-184">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar.</span><span class="sxs-lookup"><span data-stu-id="0dd31-184">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar.</span></span> <span data-ttu-id="0dd31-185">It contains all the dependencies required to run the application.</span><span class="sxs-lookup"><span data-stu-id="0dd31-185">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="0dd31-186">Upload the JAR and run jobs (SSH)</span><span class="sxs-lookup"><span data-stu-id="0dd31-186">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="0dd31-187">The following steps use `scp` to copy the JAR to the primary head node of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-187">The following steps use `scp` to copy the JAR to the primary head node of your HDInsight cluster.</span></span> <span data-ttu-id="0dd31-188">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span><span class="sxs-lookup"><span data-stu-id="0dd31-188">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="0dd31-189">Use the following to upload the jar to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-189">Use the following to upload the jar to the HDInsight cluster.</span></span> <span data-ttu-id="0dd31-190">Replace **USERNAME** with the name of your SSH login.</span><span class="sxs-lookup"><span data-stu-id="0dd31-190">Replace **USERNAME** with the name of your SSH login.</span></span> <span data-ttu-id="0dd31-191">Replace **CLUSTERNAME** with your HDInsight cluster name:</span><span class="sxs-lookup"><span data-stu-id="0dd31-191">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar

    <span data-ttu-id="0dd31-192">This command uploads the file to the home directory for your SSH user account.</span><span class="sxs-lookup"><span data-stu-id="0dd31-192">This command uploads the file to the home directory for your SSH user account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0dd31-193">If you used a password for your SSH account, you are prompted to enter the password.</span><span class="sxs-lookup"><span data-stu-id="0dd31-193">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="0dd31-194">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-194">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="0dd31-195">The following example loads the private key from `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="0dd31-195">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
   >
   > `scp -i ~/.ssh/id_rsa ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar`

2. <span data-ttu-id="0dd31-196">Use SSH to connect to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-196">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="0dd31-197">Replace **USERNAME** the name of your SSH login.</span><span class="sxs-lookup"><span data-stu-id="0dd31-197">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="0dd31-198">Replace **CLUSTERNAME** with your HDInsight cluster name:</span><span class="sxs-lookup"><span data-stu-id="0dd31-198">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

   > [!NOTE]
   > <span data-ttu-id="0dd31-199">If you used a password for your SSH account, you are prompted to enter the password.</span><span class="sxs-lookup"><span data-stu-id="0dd31-199">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="0dd31-200">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-200">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="0dd31-201">The following example loads the private key from `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="0dd31-201">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
   >
   > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="0dd31-202">Once connected, use the following to create an HBase table using the Java application:</span><span class="sxs-lookup"><span data-stu-id="0dd31-202">Once connected, use the following to create an HBase table using the Java application:</span></span>

        hadoop jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable

    <span data-ttu-id="0dd31-203">This command creates a new HBase table named **people**, and populates it with data.</span><span class="sxs-lookup"><span data-stu-id="0dd31-203">This command creates a new HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="0dd31-204">Next, use the following to search for email addresses stored in the table:</span><span class="sxs-lookup"><span data-stu-id="0dd31-204">Next, use the following to search for email addresses stored in the table:</span></span>

        hadoop jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com

    <span data-ttu-id="0dd31-205">You should receive the following results:</span><span class="sxs-lookup"><span data-stu-id="0dd31-205">You should receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="0dd31-206">Upload the JAR and run jobs (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0dd31-206">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="0dd31-207">The following steps use Azure PowerShell to upload the JAR to the default storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-207">The following steps use Azure PowerShell to upload the JAR to the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="0dd31-208">HDInsight cmdlets are then used to run the examples remotely.</span><span class="sxs-lookup"><span data-stu-id="0dd31-208">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="0dd31-209">After installing and configuring Azure PowerShell, create a file named **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-209">After installing and configuring Azure PowerShell, create a file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="0dd31-210">Use the following text as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="0dd31-210">Use the following text as the contents of this file:</span></span>

   ```powershell
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
   ```

    <span data-ttu-id="0dd31-211">This file contains two modules:</span><span class="sxs-lookup"><span data-stu-id="0dd31-211">This file contains two modules:</span></span>

   * <span data-ttu-id="0dd31-212">**Add-HDInsightFile** - used to upload files to HDInsight</span><span class="sxs-lookup"><span data-stu-id="0dd31-212">**Add-HDInsightFile** - used to upload files to HDInsight</span></span>
   * <span data-ttu-id="0dd31-213">**Start-HBaseExample** - used to run the classes created earlier</span><span class="sxs-lookup"><span data-stu-id="0dd31-213">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="0dd31-214">Save the **hbase-runner.psm1** file.</span><span class="sxs-lookup"><span data-stu-id="0dd31-214">Save the **hbase-runner.psm1** file.</span></span>

3. <span data-ttu-id="0dd31-215">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="0dd31-215">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command:</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="0dd31-216">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span><span class="sxs-lookup"><span data-stu-id="0dd31-216">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="0dd31-217">This command registers the module with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0dd31-217">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="0dd31-218">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-218">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="0dd31-219">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-219">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="0dd31-220">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-220">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span></span>

5. <span data-ttu-id="0dd31-221">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="0dd31-221">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="0dd31-222">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-222">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="0dd31-223">This command creates a new table named **people** in your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-223">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="0dd31-224">This command does not show any output in the console window.</span><span class="sxs-lookup"><span data-stu-id="0dd31-224">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="0dd31-225">To search for entries in the table, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0dd31-225">To search for entries in the table, use the following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="0dd31-226">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0dd31-226">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="0dd31-227">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0dd31-227">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span></span> <span data-ttu-id="0dd31-228">You should receive the following results:</span><span class="sxs-lookup"><span data-stu-id="0dd31-228">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="0dd31-229">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span><span class="sxs-lookup"><span data-stu-id="0dd31-229">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="0dd31-230">You can also use regular expressions as the search term.</span><span class="sxs-lookup"><span data-stu-id="0dd31-230">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="0dd31-231">For example, **^r** returns email addresses that begin with the letter 'r'.</span><span class="sxs-lookup"><span data-stu-id="0dd31-231">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="0dd31-232">No results or unexpected results when using Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="0dd31-232">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="0dd31-233">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span><span class="sxs-lookup"><span data-stu-id="0dd31-233">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="0dd31-234">Delete the table</span><span class="sxs-lookup"><span data-stu-id="0dd31-234">Delete the table</span></span>

<span data-ttu-id="0dd31-235">When you are done with the example, use the following to delete the **people** table used in this example:</span><span class="sxs-lookup"><span data-stu-id="0dd31-235">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="0dd31-236">__From an `ssh` session__:</span><span class="sxs-lookup"><span data-stu-id="0dd31-236">__From an `ssh` session__:</span></span>

`hadoop jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="0dd31-237">__From Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="0dd31-237">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`
