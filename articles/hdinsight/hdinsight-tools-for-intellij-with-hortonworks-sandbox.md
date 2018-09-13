---
title: Use Azure Toolkit for IntelliJ with the Hortonworks Sandbox | Microsoft Docs
description: Learn how to use HDInsight Tools in Azure Toolkit for IntelliJ with the Hortonworks Sandbox.
keywords: hadoop tools,hive query,intellij,hortonworks sandbox,azure toolkit for intellij
services: HDInsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/07/2017
ms.author: jgao
ms.openlocfilehash: 30f382ae047868b75dff30c6251c5528703f25a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564267"
---
#<a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="fa968-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="fa968-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="fa968-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span><span class="sxs-lookup"><span data-stu-id="fa968-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> <span data-ttu-id="fa968-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span><span class="sxs-lookup"><span data-stu-id="fa968-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="fa968-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fa968-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

##<a name="prerequisites"></a><span data-ttu-id="fa968-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fa968-108">Prerequisites</span></span>

<span data-ttu-id="fa968-109">Before you begin this tutorial, you must have:</span><span class="sxs-lookup"><span data-stu-id="fa968-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="fa968-110">The HDP 2.4 on Hortonworks Sandbox running on your local environment.</span><span class="sxs-lookup"><span data-stu-id="fa968-110">The HDP 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="fa968-111">To cofigure, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa968-111">To cofigure, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> <span data-ttu-id="fa968-112">Please note HDInsight Tools for IntelliJ has been only tested with HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="fa968-112">Please note HDInsight Tools for IntelliJ has been only tested with HDP 2.4.</span></span> <span data-ttu-id="fa968-113">From the [Hortonworks Sandbox download site](http://hortonworks.com/downloads/#sandbox), expand **Hortonworks Sandbox Archive** to get it.</span><span class="sxs-lookup"><span data-stu-id="fa968-113">From the [Hortonworks Sandbox download site](http://hortonworks.com/downloads/#sandbox), expand **Hortonworks Sandbox Archive** to get it.</span></span>
- <span data-ttu-id="fa968-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="fa968-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="fa968-115">JDK is required by the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="fa968-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>
- <span data-ttu-id="fa968-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plugin and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plugin.</span><span class="sxs-lookup"><span data-stu-id="fa968-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plugin and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plugin.</span></span> <span data-ttu-id="fa968-117">HDInsight Tools for IntelliJ are available as a part of the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="fa968-117">HDInsight Tools for IntelliJ are available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="fa968-118">**To install the plugins:**</span><span class="sxs-lookup"><span data-stu-id="fa968-118">**To install the plugins:**</span></span>

  1. <span data-ttu-id="fa968-119">Open IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="fa968-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="fa968-120">From the Welcome screen, click **Configure**, and then click **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="fa968-120">From the Welcome screen, click **Configure**, and then click **Plugins**.</span></span>
  3. <span data-ttu-id="fa968-121">Click **Install JetBrains plugin** from the lower left corner.</span><span class="sxs-lookup"><span data-stu-id="fa968-121">Click **Install JetBrains plugin** from the lower left corner.</span></span>
  4. <span data-ttu-id="fa968-122">Use the search function to search **Scala**, and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="fa968-122">Use the search function to search **Scala**, and then click **Install**.</span></span>
  5. <span data-ttu-id="fa968-123">Click **Restart IntelliJ IDEA** to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="fa968-123">Click **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="fa968-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="fa968-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="fa968-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="fa968-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="fa968-126">Create a Spark Scala application</span><span class="sxs-lookup"><span data-stu-id="fa968-126">Create a Spark Scala application</span></span>

<span data-ttu-id="fa968-127">In this section, you create a sample scala project using IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="fa968-127">In this section, you create a sample scala project using IntelliJ IDEA.</span></span> <span data-ttu-id="fa968-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span><span class="sxs-lookup"><span data-stu-id="fa968-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="fa968-129">Open IntelliJ IDEA from your workstation.</span><span class="sxs-lookup"><span data-stu-id="fa968-129">Open IntelliJ IDEA from your workstation.</span></span>
2. <span data-ttu-id="fa968-130">Click **Create New Project**.</span><span class="sxs-lookup"><span data-stu-id="fa968-130">Click **Create New Project**.</span></span>
3. <span data-ttu-id="fa968-131">Click **HDInsight** from the left pane, click **Spark on HDInsight(Scala)** from the right pane, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fa968-131">Click **HDInsight** from the left pane, click **Spark on HDInsight(Scala)** from the right pane, and then click **Next**.</span></span>

    ![Create IntelliJ Scala project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)
4. <span data-ttu-id="fa968-133">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="fa968-133">Enter the following information:</span></span>

    ![Create IntelliJ Scala project properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    - <span data-ttu-id="fa968-135">**Project name**: Provide a project name.</span><span class="sxs-lookup"><span data-stu-id="fa968-135">**Project name**: Provide a project name.</span></span>
    - <span data-ttu-id="fa968-136">**Project location**: Provide a project location.</span><span class="sxs-lookup"><span data-stu-id="fa968-136">**Project location**: Provide a project location.</span></span>
    - <span data-ttu-id="fa968-137">**Project SDK**: Click **New**, click **JDK**, and then specify the folder of Java JDK version 7 or later.</span><span class="sxs-lookup"><span data-stu-id="fa968-137">**Project SDK**: Click **New**, click **JDK**, and then specify the folder of Java JDK version 7 or later.</span></span>  <span data-ttu-id="fa968-138">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="fa968-138">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>
    - <span data-ttu-id="fa968-139">**Scala SDK**: Click **Select**, select version **2.10.6**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa968-139">**Scala SDK**: Click **Select**, select version **2.10.6**, and then click **OK**.</span></span> <span data-ttu-id="fa968-140">If the version is not listed, click **Download**, select **Scala version**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa968-140">If the version is not listed, click **Download**, select **Scala version**, and then click **OK**.</span></span> <span data-ttu-id="fa968-141">Make sure not to use version 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="fa968-141">Make sure not to use version 2.11.x.</span></span> <span data-ttu-id="fa968-142">This article uses version 2.10.6.</span><span class="sxs-lookup"><span data-stu-id="fa968-142">This article uses version 2.10.6.</span></span>
    - <span data-ttu-id="fa968-143">**Spark SDK**: Download the [SDK](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="fa968-143">**Spark SDK**: Download the [SDK](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span> <span data-ttu-id="fa968-144">You can also ignore this and use the Spark Maven repository instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span><span class="sxs-lookup"><span data-stu-id="fa968-144">You can also ignore this and use the Spark Maven repository instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span></span> <span data-ttu-id="fa968-145">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 - do not use the repository marked as Scala 2.11.)</span><span class="sxs-lookup"><span data-stu-id="fa968-145">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 - do not use the repository marked as Scala 2.11.)</span></span>
5. <span data-ttu-id="fa968-146">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="fa968-146">Click **Finish**.</span></span>
6. <span data-ttu-id="fa968-147">Press **[ALT]+1** to open the Project view if it is not opened.</span><span class="sxs-lookup"><span data-stu-id="fa968-147">Press **[ALT]+1** to open the Project view if it is not opened.</span></span>
7. <span data-ttu-id="fa968-148">From **Project Explorer**, expand the project, and then click **src**.</span><span class="sxs-lookup"><span data-stu-id="fa968-148">From **Project Explorer**, expand the project, and then click **src**.</span></span>
8. <span data-ttu-id="fa968-149">Right-click **src**, point to **New**, and then click **Scala class**.</span><span class="sxs-lookup"><span data-stu-id="fa968-149">Right-click **src**, point to **New**, and then click **Scala class**.</span></span>
9. <span data-ttu-id="fa968-150">Enter a name, select **Object** in **Kind**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa968-150">Enter a name, select **Object** in **Kind**, and then click **OK**.</span></span>

    ![Create new IntelliJ Scala class](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)
10. <span data-ttu-id="fa968-152">In the .scala file, paste the following code:</span><span class="sxs-lookup"><span data-stu-id="fa968-152">In the .scala file, paste the following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

11. <span data-ttu-id="fa968-153">From the **Build** menu, click **Build project**.</span><span class="sxs-lookup"><span data-stu-id="fa968-153">From the **Build** menu, click **Build project**.</span></span> <span data-ttu-id="fa968-154">Make sure the compilation is completed successfully.</span><span class="sxs-lookup"><span data-stu-id="fa968-154">Make sure the compilation is completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="fa968-155">Link to the HortonWorks Sandbox</span><span class="sxs-lookup"><span data-stu-id="fa968-155">Link to the HortonWorks Sandbox</span></span>

<span data-ttu-id="fa968-156">You need to have an existing IntelliJ application before you can link to a Hortonworks Sandbox(emulator).</span><span class="sxs-lookup"><span data-stu-id="fa968-156">You need to have an existing IntelliJ application before you can link to a Hortonworks Sandbox(emulator).</span></span>

<span data-ttu-id="fa968-157">**To link to an emulator**</span><span class="sxs-lookup"><span data-stu-id="fa968-157">**To link to an emulator**</span></span>

1. <span data-ttu-id="fa968-158">Open the project in IntelliJ if it is not opened yet.</span><span class="sxs-lookup"><span data-stu-id="fa968-158">Open the project in IntelliJ if it is not opened yet.</span></span>
2. <span data-ttu-id="fa968-159">From the **View** menu, click **Tools Windows**, and then click **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fa968-159">From the **View** menu, click **Tools Windows**, and then click **Azure Explorer**.</span></span>
3. <span data-ttu-id="fa968-160">Expand **Azure**, right-click **HDInsight**, and then click **Link an Emulator**.</span><span class="sxs-lookup"><span data-stu-id="fa968-160">Expand **Azure**, right-click **HDInsight**, and then click **Link an Emulator**.</span></span>
4. <span data-ttu-id="fa968-161">Enter the password you have configured for the root account of the Hortonworks Sandbox, and the rest of the values simliar to the following screenshot, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa968-161">Enter the password you have configured for the root account of the Hortonworks Sandbox, and the rest of the values simliar to the following screenshot, and then click **OK**.</span></span> 

  ![IntelliJ link an emulator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="fa968-163">Click **Yes** to configure the emulator.</span><span class="sxs-lookup"><span data-stu-id="fa968-163">Click **Yes** to configure the emulator.</span></span>

  <span data-ttu-id="fa968-164">When it is connected successfully, you can see the emulator (Hortonworks Sandbox) listed under the HDInsight node.</span><span class="sxs-lookup"><span data-stu-id="fa968-164">When it is connected successfully, you can see the emulator (Hortonworks Sandbox) listed under the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-sandbox"></a><span data-ttu-id="fa968-165">Submit the Spark Scala application to the Sandbox</span><span class="sxs-lookup"><span data-stu-id="fa968-165">Submit the Spark Scala application to the Sandbox</span></span>

<span data-ttu-id="fa968-166">After you have linked the IntelliJ IDEA to the emulator, you can submit your project.</span><span class="sxs-lookup"><span data-stu-id="fa968-166">After you have linked the IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="fa968-167">**To submit a project to an emulator**</span><span class="sxs-lookup"><span data-stu-id="fa968-167">**To submit a project to an emulator**</span></span>

1. <span data-ttu-id="fa968-168">From the **Project explorer**, right-click the project, and then click **Submit Spark application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fa968-168">From the **Project explorer**, right-click the project, and then click **Submit Spark application to HDInsight**.</span></span>
2. <span data-ttu-id="fa968-169">Specify the following fields:</span><span class="sxs-lookup"><span data-stu-id="fa968-169">Specify the following fields:</span></span>

    - <span data-ttu-id="fa968-170">**Spark cluster (Linux only)**: Select your local Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="fa968-170">**Spark cluster (Linux only)**: Select your local Hortonworks Sandbox.</span></span>
    - <span data-ttu-id="fa968-171">**Main class name**: Choose or enter the main class name.</span><span class="sxs-lookup"><span data-stu-id="fa968-171">**Main class name**: Choose or enter the main class name.</span></span>  <span data-ttu-id="fa968-172">For this tutorial, it is **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="fa968-172">For this tutorial, it is **GroupByTest**.</span></span>
3. <span data-ttu-id="fa968-173">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="fa968-173">Click **Submit**.</span></span> <span data-ttu-id="fa968-174">The job submission logs are shown in the Spark submission tool window.</span><span class="sxs-lookup"><span data-stu-id="fa968-174">The job submission logs are shown in the Spark submission tool window.</span></span>

##<a name="next-steps"></a><span data-ttu-id="fa968-175">Next steps:</span><span class="sxs-lookup"><span data-stu-id="fa968-175">Next steps:</span></span>

- <span data-ttu-id="fa968-176">To learn how to create Spark applications for HDInsight using HDInsight Tools for IntelliJ, see [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="fa968-176">To learn how to create Spark applications for HDInsight using HDInsight Tools for IntelliJ, see [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
- <span data-ttu-id="fa968-177">To watch a video of HDInsight Tools for IntelliJ, see [Introduce HDInsight Tools for IntelliJ for Spark Development](https://mix.office.com/watch/1nqkqjt5xonza).</span><span class="sxs-lookup"><span data-stu-id="fa968-177">To watch a video of HDInsight Tools for IntelliJ, see [Introduce HDInsight Tools for IntelliJ for Spark Development](https://mix.office.com/watch/1nqkqjt5xonza).</span></span>
- <span data-ttu-id="fa968-178">To learn how to debug Spark applications using the toolkit remotely on HDInsight, see [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="fa968-178">To learn how to debug Spark applications using the toolkit remotely on HDInsight, see [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>
- <span data-ttu-id="fa968-179">To learn how to use HDInsight Tools for Eclipse to create Spark application, see [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="fa968-179">To learn how to use HDInsight Tools for Eclipse to create Spark application, see [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>
- <span data-ttu-id="fa968-180">To watch a video of HDInsight Tools for Eclipse, see [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="fa968-180">To watch a video of HDInsight Tools for Eclipse, see [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>



