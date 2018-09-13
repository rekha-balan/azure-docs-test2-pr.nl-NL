---
title: Create Scala Maven application to run on Azure Spark clusters | Microsoft Docs
description: Learn how to create a standalone Spark application using Maven to run on HDInsight Spark clusters.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 7ca8325c415e8be50597d0606631f2db5a39dd37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540965"
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="6c86b-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="6c86b-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="6c86b-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="6c86b-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="6c86b-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="6c86b-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c86b-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="6c86b-107">Use Maven as the build system.</span><span class="sxs-lookup"><span data-stu-id="6c86b-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="6c86b-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span><span class="sxs-lookup"><span data-stu-id="6c86b-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="6c86b-109">Write your application in Scala.</span><span class="sxs-lookup"><span data-stu-id="6c86b-109">Write your application in Scala.</span></span>
* <span data-ttu-id="6c86b-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="6c86b-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="6c86b-111">Run the application on Spark cluster using Livy.</span><span class="sxs-lookup"><span data-stu-id="6c86b-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="6c86b-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span><span class="sxs-lookup"><span data-stu-id="6c86b-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="6c86b-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="6c86b-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6c86b-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c86b-114">Prerequisites</span></span>

* <span data-ttu-id="6c86b-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6c86b-115">An Azure subscription.</span></span> <span data-ttu-id="6c86b-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6c86b-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6c86b-117">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6c86b-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="6c86b-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6c86b-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="6c86b-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="6c86b-119">Oracle Java Development kit.</span></span> <span data-ttu-id="6c86b-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="6c86b-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="6c86b-121">A Java IDE.</span><span class="sxs-lookup"><span data-stu-id="6c86b-121">A Java IDE.</span></span> <span data-ttu-id="6c86b-122">This article uses IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="6c86b-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="6c86b-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="6c86b-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="6c86b-124">Install Scala plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="6c86b-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="6c86b-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span><span class="sxs-lookup"><span data-stu-id="6c86b-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="6c86b-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Enable scala plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="6c86b-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span><span class="sxs-lookup"><span data-stu-id="6c86b-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="6c86b-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Install scala plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="6c86b-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span><span class="sxs-lookup"><span data-stu-id="6c86b-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="6c86b-132">Create a standalone Scala project</span><span class="sxs-lookup"><span data-stu-id="6c86b-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="6c86b-133">Launch IntelliJ IDEA and create a new project.</span><span class="sxs-lookup"><span data-stu-id="6c86b-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="6c86b-134">In the new project dialog box, make the following choices, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Create Maven project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="6c86b-136">Select **Maven** as the project type.</span><span class="sxs-lookup"><span data-stu-id="6c86b-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="6c86b-137">Specify a **Project SDK**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="6c86b-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="6c86b-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="6c86b-139">Select the **Create from archetype** option.</span><span class="sxs-lookup"><span data-stu-id="6c86b-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="6c86b-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="6c86b-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span><span class="sxs-lookup"><span data-stu-id="6c86b-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="6c86b-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="6c86b-143">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-143">Click **Next**.</span></span>
3. <span data-ttu-id="6c86b-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="6c86b-145">In the last dialog box, specify a project name and location and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="6c86b-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="6c86b-147">You do not need this for the application.</span><span class="sxs-lookup"><span data-stu-id="6c86b-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="6c86b-148">If required, rename the default source and test files.</span><span class="sxs-lookup"><span data-stu-id="6c86b-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="6c86b-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="6c86b-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![Rename files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="6c86b-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span><span class="sxs-lookup"><span data-stu-id="6c86b-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="6c86b-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span><span class="sxs-lookup"><span data-stu-id="6c86b-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configure Maven for automatic downloads](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="6c86b-155">From the **File** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="6c86b-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="6c86b-157">Select the option to **Import Maven projects automatically**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="6c86b-158">Click **Apply**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="6c86b-159">Update the Scala source file to include your application code.</span><span class="sxs-lookup"><span data-stu-id="6c86b-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="6c86b-160">Open and replace the existing sample code with the following code and save the changes.</span><span class="sxs-lookup"><span data-stu-id="6c86b-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="6c86b-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="6c86b-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasbs:///HVACout")
          }
        }
9. <span data-ttu-id="6c86b-162">Update the pom.xml.</span><span class="sxs-lookup"><span data-stu-id="6c86b-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="6c86b-163">Within `<project>\<properties>` add the following:</span><span class="sxs-lookup"><span data-stu-id="6c86b-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="6c86b-164">Within `<project>\<dependencies>` add the following:</span><span class="sxs-lookup"><span data-stu-id="6c86b-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="6c86b-165">Save changes to pom.xml.</span><span class="sxs-lookup"><span data-stu-id="6c86b-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="6c86b-166">Create the .jar file.</span><span class="sxs-lookup"><span data-stu-id="6c86b-166">Create the .jar file.</span></span> <span data-ttu-id="6c86b-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span><span class="sxs-lookup"><span data-stu-id="6c86b-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="6c86b-168">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="6c86b-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="6c86b-169">From the **File** menu, click **Project Structure**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="6c86b-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span><span class="sxs-lookup"><span data-stu-id="6c86b-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="6c86b-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="6c86b-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="6c86b-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="6c86b-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="6c86b-177">This creates a single JAR with all dependencies.</span><span class="sxs-lookup"><span data-stu-id="6c86b-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="6c86b-179">The output layout tab lists all the jars that are included as part of the Maven project.</span><span class="sxs-lookup"><span data-stu-id="6c86b-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="6c86b-180">You can select and delete the ones on which the Scala application has no direct dependency.</span><span class="sxs-lookup"><span data-stu-id="6c86b-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="6c86b-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span><span class="sxs-lookup"><span data-stu-id="6c86b-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="6c86b-182">Select the jars to delete and then click the **Delete** icon.</span><span class="sxs-lookup"><span data-stu-id="6c86b-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="6c86b-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span><span class="sxs-lookup"><span data-stu-id="6c86b-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="6c86b-185">Click **Apply** and then **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="6c86b-186">From the menu bar, click **Build**, and then click **Make Project**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="6c86b-187">You can also click **Build Artifacts** to create the jar.</span><span class="sxs-lookup"><span data-stu-id="6c86b-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="6c86b-188">The output jar is created under **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="6c86b-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="6c86b-190">Run the application on the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="6c86b-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="6c86b-191">To run the application on the cluster, you must do the following:</span><span class="sxs-lookup"><span data-stu-id="6c86b-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="6c86b-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="6c86b-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="6c86b-193">You can use [**AzCopy**](../storage/storage-use-azcopy.md), a command line utility, to do so.</span><span class="sxs-lookup"><span data-stu-id="6c86b-193">You can use [**AzCopy**](../storage/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="6c86b-194">There are a lot of other clients as well that you can use to upload data.</span><span class="sxs-lookup"><span data-stu-id="6c86b-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="6c86b-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="6c86b-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="6c86b-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="6c86b-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="6c86b-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="6c86b-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="6c86b-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="6c86b-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="seealso"></a><span data-ttu-id="6c86b-199">See also</span><span class="sxs-lookup"><span data-stu-id="6c86b-199">See also</span></span>
* [<span data-ttu-id="6c86b-200">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-200">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="6c86b-201">Scenarios</span><span class="sxs-lookup"><span data-stu-id="6c86b-201">Scenarios</span></span>
* [<span data-ttu-id="6c86b-202">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="6c86b-202">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="6c86b-203">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="6c86b-203">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="6c86b-204">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="6c86b-204">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="6c86b-205">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="6c86b-205">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="6c86b-206">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-206">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="6c86b-207">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="6c86b-207">Create and run applications</span></span>
* [<span data-ttu-id="6c86b-208">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="6c86b-208">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="6c86b-209">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="6c86b-209">Tools and extensions</span></span>
* [<span data-ttu-id="6c86b-210">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="6c86b-210">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6c86b-211">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="6c86b-211">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="6c86b-212">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-212">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="6c86b-213">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-213">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="6c86b-214">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="6c86b-214">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="6c86b-215">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="6c86b-215">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="6c86b-216">Manage resources</span><span class="sxs-lookup"><span data-stu-id="6c86b-216">Manage resources</span></span>
* [<span data-ttu-id="6c86b-217">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-217">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="6c86b-218">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c86b-218">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)












