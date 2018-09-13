---
title: 'Tutorial: Create a Scala Maven application for Spark in Azure HDInsight using IntelliJ'
description: Create a Spark application written in Scala with Apache Maven as the build system and an existing Maven archetype for Scala provided by IntelliJ IDEA.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,mvc
ms.topic: tutorial
ms.date: 05/07/2018
ms.openlocfilehash: fc1f952128b4cfbb082f4c539a102f40d3b85e8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967544"
---
# <a name="tutorial-create-a-scala-maven-application-for-spark-in-hdinsight-using-intellij"></a><span data-ttu-id="2f127-103">Tutorial: create a Scala Maven application for Spark in HDInsight using IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2f127-103">Tutorial: create a Scala Maven application for Spark in HDInsight using IntelliJ</span></span>

<span data-ttu-id="2f127-104">In this tutorial, you learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2f127-104">In this tutorial, you learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="2f127-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2f127-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="2f127-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f127-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="2f127-107">Use Maven as the build system.</span><span class="sxs-lookup"><span data-stu-id="2f127-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="2f127-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span><span class="sxs-lookup"><span data-stu-id="2f127-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="2f127-109">Write your application in Scala.</span><span class="sxs-lookup"><span data-stu-id="2f127-109">Write your application in Scala.</span></span>
* <span data-ttu-id="2f127-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="2f127-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="2f127-111">Run the application on Spark cluster using Livy.</span><span class="sxs-lookup"><span data-stu-id="2f127-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="2f127-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span><span class="sxs-lookup"><span data-stu-id="2f127-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="2f127-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="2f127-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](apache-spark-intellij-tool-plugin.md).</span></span>
> 

<span data-ttu-id="2f127-114">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="2f127-114">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="2f127-115">Use IntelliJ to develop a Scala Maven application</span><span class="sxs-lookup"><span data-stu-id="2f127-115">Use IntelliJ to develop a Scala Maven application</span></span>

<span data-ttu-id="2f127-116">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="2f127-116">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2f127-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f127-117">Prerequisites</span></span>

* <span data-ttu-id="2f127-118">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f127-118">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2f127-119">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2f127-119">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="2f127-120">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="2f127-120">Oracle Java Development kit.</span></span> <span data-ttu-id="2f127-121">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="2f127-121">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="2f127-122">A Java IDE.</span><span class="sxs-lookup"><span data-stu-id="2f127-122">A Java IDE.</span></span> <span data-ttu-id="2f127-123">This article uses IntelliJ IDEA 18.1.1.</span><span class="sxs-lookup"><span data-stu-id="2f127-123">This article uses IntelliJ IDEA 18.1.1.</span></span> <span data-ttu-id="2f127-124">You can install it from [here](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="2f127-124">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="use-intellij-to-create-application"></a><span data-ttu-id="2f127-125">Use IntelliJ to create application</span><span class="sxs-lookup"><span data-stu-id="2f127-125">Use IntelliJ to create application</span></span>

1. <span data-ttu-id="2f127-126">Start IntelliJ IDEA, and then create a project.</span><span class="sxs-lookup"><span data-stu-id="2f127-126">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="2f127-127">In the **New Project** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="2f127-127">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="2f127-128">a.</span><span class="sxs-lookup"><span data-stu-id="2f127-128">a.</span></span> <span data-ttu-id="2f127-129">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="2f127-129">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="2f127-130">b.</span><span class="sxs-lookup"><span data-stu-id="2f127-130">b.</span></span> <span data-ttu-id="2f127-131">In the **Build tool** list, select either of the following, according to your need:</span><span class="sxs-lookup"><span data-stu-id="2f127-131">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="2f127-132">**Maven**, for Scala project-creation wizard support</span><span class="sxs-lookup"><span data-stu-id="2f127-132">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="2f127-133">**SBT**, for managing the dependencies and building for the Scala project</span><span class="sxs-lookup"><span data-stu-id="2f127-133">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![The New Project dialog box](./media/apache-spark-create-standalone-application/create-hdi-scala-app.png)

1. <span data-ttu-id="2f127-135">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f127-135">Select **Next**.</span></span>

1. <span data-ttu-id="2f127-136">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="2f127-136">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="2f127-137">Select **Install**.</span><span class="sxs-lookup"><span data-stu-id="2f127-137">Select **Install**.</span></span>

   ![Scala Plugin Check](./media/apache-spark-create-standalone-application/Scala-Plugin-check-Reminder.PNG) 

1. <span data-ttu-id="2f127-139">To download the Scala plug-in, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f127-139">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="2f127-140">Follow the instructions to restart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2f127-140">Follow the instructions to restart IntelliJ.</span></span> 

   ![The Scala plugin installation dialog box](./media/apache-spark-create-standalone-application/Choose-Scala-Plugin.PNG)

1. <span data-ttu-id="2f127-142">In the **New Project** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="2f127-142">In the **New Project** window, do the following:</span></span>  

    ![Selecting the Spark SDK](./media/apache-spark-create-standalone-application/hdi-new-project.png)

   <span data-ttu-id="2f127-144">a.</span><span class="sxs-lookup"><span data-stu-id="2f127-144">a.</span></span> <span data-ttu-id="2f127-145">Enter a project name and location.</span><span class="sxs-lookup"><span data-stu-id="2f127-145">Enter a project name and location.</span></span>

   <span data-ttu-id="2f127-146">b.</span><span class="sxs-lookup"><span data-stu-id="2f127-146">b.</span></span> <span data-ttu-id="2f127-147">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span><span class="sxs-lookup"><span data-stu-id="2f127-147">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="2f127-148">c.</span><span class="sxs-lookup"><span data-stu-id="2f127-148">c.</span></span> <span data-ttu-id="2f127-149">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="2f127-149">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="2f127-150">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="2f127-150">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="2f127-151">Otherwise, select **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="2f127-151">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="2f127-152">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="2f127-152">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

1. <span data-ttu-id="2f127-153">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2f127-153">Select **Finish**.</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="2f127-154">Install Scala plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="2f127-154">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="2f127-155">To install the Scala plugin, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f127-155">To install the Scala plugin, use the following steps:</span></span>

1. <span data-ttu-id="2f127-156">Open IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2f127-156">Open IntelliJ IDEA.</span></span>
1. <span data-ttu-id="2f127-157">On the welcome screen, select **Configure** and then select **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="2f127-157">On the welcome screen, select **Configure** and then select **Plugins**.</span></span>
   
    ![Enable scala plugin](./media/apache-spark-create-standalone-application/enable-scala-plugin.png)
1. <span data-ttu-id="2f127-159">Select **Install JetBrains plugin** from the lower left corner.</span><span class="sxs-lookup"><span data-stu-id="2f127-159">Select **Install JetBrains plugin** from the lower left corner.</span></span> 
1. <span data-ttu-id="2f127-160">In the **Browse JetBrains Plugins** dialog box, search for **Scala** and then select **Install**.</span><span class="sxs-lookup"><span data-stu-id="2f127-160">In the **Browse JetBrains Plugins** dialog box, search for **Scala** and then select **Install**.</span></span>
   
    ![Install scala plugin](./media/apache-spark-create-standalone-application/install-scala-plugin.png)
1. <span data-ttu-id="2f127-162">After the plugin installs successfully, you must restart the IDE.</span><span class="sxs-lookup"><span data-stu-id="2f127-162">After the plugin installs successfully, you must restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="2f127-163">Create a standalone Scala project</span><span class="sxs-lookup"><span data-stu-id="2f127-163">Create a standalone Scala project</span></span>
1. <span data-ttu-id="2f127-164">Open IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="2f127-164">Open IntelliJ IDEA.</span></span>
1. <span data-ttu-id="2f127-165">From the **File** menu, select **New > Project** to create a new project.</span><span class="sxs-lookup"><span data-stu-id="2f127-165">From the **File** menu, select **New > Project** to create a new project.</span></span>
1. <span data-ttu-id="2f127-166">In the new project dialog box, make the following choices:</span><span class="sxs-lookup"><span data-stu-id="2f127-166">In the new project dialog box, make the following choices:</span></span>
   
    ![Create Maven project](./media/apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="2f127-168">Select **Maven** as the project type.</span><span class="sxs-lookup"><span data-stu-id="2f127-168">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="2f127-169">Specify a **Project SDK**.</span><span class="sxs-lookup"><span data-stu-id="2f127-169">Specify a **Project SDK**.</span></span> <span data-ttu-id="2f127-170">Select **New** and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="2f127-170">Select **New** and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="2f127-171">Select the **Create from archetype** option.</span><span class="sxs-lookup"><span data-stu-id="2f127-171">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="2f127-172">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span><span class="sxs-lookup"><span data-stu-id="2f127-172">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="2f127-173">This archetype creates the right directory structure and download the required default dependencies to write Scala program.</span><span class="sxs-lookup"><span data-stu-id="2f127-173">This archetype creates the right directory structure and download the required default dependencies to write Scala program.</span></span>
1. <span data-ttu-id="2f127-174">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f127-174">Select **Next**.</span></span>
1. <span data-ttu-id="2f127-175">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span><span class="sxs-lookup"><span data-stu-id="2f127-175">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="2f127-176">The following values are used in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="2f127-176">The following values are used in this tutorial:</span></span>

    - <span data-ttu-id="2f127-177">GroupId: com.microsoft.spark.example</span><span class="sxs-lookup"><span data-stu-id="2f127-177">GroupId: com.microsoft.spark.example</span></span>
    - <span data-ttu-id="2f127-178">ArtifactId: SparkSimpleApp</span><span class="sxs-lookup"><span data-stu-id="2f127-178">ArtifactId: SparkSimpleApp</span></span>
1. <span data-ttu-id="2f127-179">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f127-179">Select **Next**.</span></span>
1. <span data-ttu-id="2f127-180">Verify the settings and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f127-180">Verify the settings and then select **Next**.</span></span>
1. <span data-ttu-id="2f127-181">Verify the project name and location, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2f127-181">Verify the project name and location, and then select **Finish**.</span></span>
1. <span data-ttu-id="2f127-182">In the left pane, select **src > test > scala > com > microsoft > spark > example**, right-click **MySpec**, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2f127-182">In the left pane, select **src > test > scala > com > microsoft > spark > example**, right-click **MySpec**, and then select **Delete**.</span></span> <span data-ttu-id="2f127-183">You do not need this file for the application.</span><span class="sxs-lookup"><span data-stu-id="2f127-183">You do not need this file for the application.</span></span>
  
1. <span data-ttu-id="2f127-184">In the subsequent steps, you update the pom.xml to define the dependencies for the Spark Scala application.</span><span class="sxs-lookup"><span data-stu-id="2f127-184">In the subsequent steps, you update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="2f127-185">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span><span class="sxs-lookup"><span data-stu-id="2f127-185">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configure Maven for automatic downloads](./media/apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="2f127-187">From the **File** menu, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="2f127-187">From the **File** menu, select **Settings**.</span></span>
   1. <span data-ttu-id="2f127-188">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span><span class="sxs-lookup"><span data-stu-id="2f127-188">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   1. <span data-ttu-id="2f127-189">Select the option to **Import Maven projects automatically**.</span><span class="sxs-lookup"><span data-stu-id="2f127-189">Select the option to **Import Maven projects automatically**.</span></span>
   1. <span data-ttu-id="2f127-190">Select **Apply**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f127-190">Select **Apply**, and then select **OK**.</span></span>
1. <span data-ttu-id="2f127-191">In the left pane, select **src > main > scala > com.microsoft.spark.example**, and then double-click **App** to open App.scala.</span><span class="sxs-lookup"><span data-stu-id="2f127-191">In the left pane, select **src > main > scala > com.microsoft.spark.example**, and then double-click **App** to open App.scala.</span></span>

1. <span data-ttu-id="2f127-192">Replace the existing sample code with the following code and save the changes.</span><span class="sxs-lookup"><span data-stu-id="2f127-192">Replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="2f127-193">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="2f127-193">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

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
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
1. <span data-ttu-id="2f127-194">In the left pane, double-click **pom.xml**.</span><span class="sxs-lookup"><span data-stu-id="2f127-194">In the left pane, double-click **pom.xml**.</span></span>
   
   1. <span data-ttu-id="2f127-195">Within `<project>\<properties>` add the following segments:</span><span class="sxs-lookup"><span data-stu-id="2f127-195">Within `<project>\<properties>` add the following segments:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   1. <span data-ttu-id="2f127-196">Within `<project>\<dependencies>` add the following segments:</span><span class="sxs-lookup"><span data-stu-id="2f127-196">Within `<project>\<dependencies>` add the following segments:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="2f127-197">Save changes to pom.xml.</span><span class="sxs-lookup"><span data-stu-id="2f127-197">Save changes to pom.xml.</span></span>
1. <span data-ttu-id="2f127-198">Create the .jar file.</span><span class="sxs-lookup"><span data-stu-id="2f127-198">Create the .jar file.</span></span> <span data-ttu-id="2f127-199">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span><span class="sxs-lookup"><span data-stu-id="2f127-199">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="2f127-200">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="2f127-200">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="2f127-201">From the **File** menu, select **Project Structure**.</span><span class="sxs-lookup"><span data-stu-id="2f127-201">From the **File** menu, select **Project Structure**.</span></span>
    1. <span data-ttu-id="2f127-202">In the **Project Structure** dialog box, select **Artifacts** and then select the plus symbol.</span><span class="sxs-lookup"><span data-stu-id="2f127-202">In the **Project Structure** dialog box, select **Artifacts** and then select the plus symbol.</span></span> <span data-ttu-id="2f127-203">From the pop-up dialog box, select **JAR**, and then select **From modules with dependencies**.</span><span class="sxs-lookup"><span data-stu-id="2f127-203">From the pop-up dialog box, select **JAR**, and then select **From modules with dependencies**.</span></span>
       
        ![Create JAR](./media/apache-spark-create-standalone-application/create-jar-1.png)
    1. <span data-ttu-id="2f127-205">In the **Create JAR from Modules** dialog box, select the ellipsis (![ellipsis](./media/apache-spark-create-standalone-application/ellipsis.png)) against the **Main Class**.</span><span class="sxs-lookup"><span data-stu-id="2f127-205">In the **Create JAR from Modules** dialog box, select the ellipsis (![ellipsis](./media/apache-spark-create-standalone-application/ellipsis.png)) against the **Main Class**.</span></span>
    1. <span data-ttu-id="2f127-206">In the **Select Main Class** dialog box, select the class that appears by default and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f127-206">In the **Select Main Class** dialog box, select the class that appears by default and then select **OK**.</span></span>
       
        ![Create JAR](./media/apache-spark-create-standalone-application/create-jar-2.png)
    1. <span data-ttu-id="2f127-208">In the **Create JAR from Modules** dialog box, make sure the **extract to the target JAR** option is selected, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f127-208">In the **Create JAR from Modules** dialog box, make sure the **extract to the target JAR** option is selected, and then select **OK**.</span></span>  <span data-ttu-id="2f127-209">This setting creates a single JAR with all dependencies.</span><span class="sxs-lookup"><span data-stu-id="2f127-209">This setting creates a single JAR with all dependencies.</span></span>
       
        ![Create JAR](./media/apache-spark-create-standalone-application/create-jar-3.png)
    1. <span data-ttu-id="2f127-211">The output layout tab lists all the jars that are included as part of the Maven project.</span><span class="sxs-lookup"><span data-stu-id="2f127-211">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="2f127-212">You can select and delete the ones on which the Scala application has no direct dependency.</span><span class="sxs-lookup"><span data-stu-id="2f127-212">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="2f127-213">For the application, you are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span><span class="sxs-lookup"><span data-stu-id="2f127-213">For the application, you are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="2f127-214">Select the jars to delete and then select the **Delete** icon.</span><span class="sxs-lookup"><span data-stu-id="2f127-214">Select the jars to delete and then select the **Delete** icon.</span></span>
       
        ![Create JAR](./media/apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="2f127-216">Make sure the **Include in project build** box is selected, which ensures that the jar is created every time the project is built or updated.</span><span class="sxs-lookup"><span data-stu-id="2f127-216">Make sure the **Include in project build** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="2f127-217">select **Apply** and then **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f127-217">select **Apply** and then **OK**.</span></span>
    1. <span data-ttu-id="2f127-218">From the **Build** menu, select **Build Artifacts** to create the jar.</span><span class="sxs-lookup"><span data-stu-id="2f127-218">From the **Build** menu, select **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="2f127-219">The output jar is created under **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="2f127-219">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Create JAR](./media/apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="2f127-221">Run the application on the Spark cluster</span><span class="sxs-lookup"><span data-stu-id="2f127-221">Run the application on the Spark cluster</span></span>
<span data-ttu-id="2f127-222">To run the application on the cluster, you can use the following approaches:</span><span class="sxs-lookup"><span data-stu-id="2f127-222">To run the application on the cluster, you can use the following approaches:</span></span>

* <span data-ttu-id="2f127-223">**Copy the application jar to the Azure storage blob** associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="2f127-223">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="2f127-224">You can use [**AzCopy**](../../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span><span class="sxs-lookup"><span data-stu-id="2f127-224">You can use [**AzCopy**](../../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="2f127-225">There are many other clients as well that you can use to upload data.</span><span class="sxs-lookup"><span data-stu-id="2f127-225">There are many other clients as well that you can use to upload data.</span></span> <span data-ttu-id="2f127-226">You can find more about them at [Upload data for Hadoop jobs in HDInsight](../hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="2f127-226">You can find more about them at [Upload data for Hadoop jobs in HDInsight](../hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="2f127-227">**Use Livy to submit an application job remotely** to the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="2f127-227">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="2f127-228">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="2f127-228">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="2f127-229">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="2f127-229">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="2f127-230">Next step</span><span class="sxs-lookup"><span data-stu-id="2f127-230">Next step</span></span>

<span data-ttu-id="2f127-231">In this article, you learned how to create a Spark scala application.</span><span class="sxs-lookup"><span data-stu-id="2f127-231">In this article, you learned how to create a Spark scala application.</span></span> <span data-ttu-id="2f127-232">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span><span class="sxs-lookup"><span data-stu-id="2f127-232">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="2f127-233">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="2f127-233">Run jobs remotely on a Spark cluster using Livy</span></span>](./apache-spark-livy-rest-interface.md)

