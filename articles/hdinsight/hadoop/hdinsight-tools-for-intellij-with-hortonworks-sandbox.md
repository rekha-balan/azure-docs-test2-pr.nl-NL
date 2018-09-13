---
title: Use Azure Toolkit for IntelliJ with Hortonworks Sandbox
description: Learn how to use HDInsight Tools in Azure Toolkit for IntelliJ with Hortonworks Sandbox.
keywords: hadoop tools,hive query,intellij,hortonworks sandbox,azure toolkit for intellij
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: 9e87392ad7730571b973dbec809f64487eefa849
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857507"
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="e5080-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="e5080-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="e5080-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications, and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your computer.</span><span class="sxs-lookup"><span data-stu-id="e5080-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications, and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your computer.</span></span> 

<span data-ttu-id="e5080-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java integrated development environment (IDE) for developing computer software.</span><span class="sxs-lookup"><span data-stu-id="e5080-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="e5080-107">After you develop and test your applications on Hortonworks Sandbox, you can move the applications to [Azure HDInsight](apache-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5080-107">After you develop and test your applications on Hortonworks Sandbox, you can move the applications to [Azure HDInsight](apache-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5080-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e5080-108">Prerequisites</span></span>

<span data-ttu-id="e5080-109">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="e5080-109">Before you begin this tutorial, you must have the following items:</span></span>

- <span data-ttu-id="e5080-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local computer.</span><span class="sxs-lookup"><span data-stu-id="e5080-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local computer.</span></span> <span data-ttu-id="e5080-111">To set up HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](apache-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5080-111">To set up HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](apache-hadoop-emulator-get-started.md).</span></span> 
    > [!NOTE]
    > <span data-ttu-id="e5080-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="e5080-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="e5080-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="e5080-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="e5080-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="e5080-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="e5080-115">Azure Toolkit for IntelliJ requires JDK.</span><span class="sxs-lookup"><span data-stu-id="e5080-115">Azure Toolkit for IntelliJ requires JDK.</span></span>

- <span data-ttu-id="e5080-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij) plug-in.</span><span class="sxs-lookup"><span data-stu-id="e5080-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij) plug-in.</span></span> <span data-ttu-id="e5080-117">HDInsight Tools for IntelliJ is available as part of Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e5080-117">HDInsight Tools for IntelliJ is available as part of Azure Toolkit for IntelliJ.</span></span> 

<span data-ttu-id="e5080-118">To install the plug-ins:</span><span class="sxs-lookup"><span data-stu-id="e5080-118">To install the plug-ins:</span></span>

  1. <span data-ttu-id="e5080-119">Open IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e5080-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="e5080-120">On the **Welcome** page, select **Configure**, and then select **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="e5080-120">On the **Welcome** page, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="e5080-121">In the lower-left corner, select **Install JetBrains plugin**.</span><span class="sxs-lookup"><span data-stu-id="e5080-121">In the lower-left corner, select **Install JetBrains plugin**.</span></span>
  4. <span data-ttu-id="e5080-122">Use the search function to search for **Scala**, and then select **Install**.</span><span class="sxs-lookup"><span data-stu-id="e5080-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="e5080-123">To complete the installation, select **Restart IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="e5080-123">To complete the installation, select **Restart IntelliJ IDEA**.</span></span>
  6. <span data-ttu-id="e5080-124">Repeat steps 4 and 5 to install **Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="e5080-124">Repeat steps 4 and 5 to install **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e5080-125">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="e5080-125">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="e5080-126">Create a Spark Scala application</span><span class="sxs-lookup"><span data-stu-id="e5080-126">Create a Spark Scala application</span></span>

<span data-ttu-id="e5080-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e5080-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="e5080-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span><span class="sxs-lookup"><span data-stu-id="e5080-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="e5080-129">Open IntelliJ IDEA on your computer.</span><span class="sxs-lookup"><span data-stu-id="e5080-129">Open IntelliJ IDEA on your computer.</span></span> <span data-ttu-id="e5080-130">In the **New Project** dialog box, complete these steps:</span><span class="sxs-lookup"><span data-stu-id="e5080-130">In the **New Project** dialog box, complete these steps:</span></span>

   1. <span data-ttu-id="e5080-131">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="e5080-131">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>
   2. <span data-ttu-id="e5080-132">In the **Build tool** list, select one of the following, based on your scenario:</span><span class="sxs-lookup"><span data-stu-id="e5080-132">In the **Build tool** list, select one of the following, based on your scenario:</span></span>

    * <span data-ttu-id="e5080-133">**Maven**: For Scala project-creation wizard support.</span><span class="sxs-lookup"><span data-stu-id="e5080-133">**Maven**: For Scala project-creation wizard support.</span></span>
    * <span data-ttu-id="e5080-134">**SBT**: For managing dependencies and building for the Scala project.</span><span class="sxs-lookup"><span data-stu-id="e5080-134">**SBT**: For managing dependencies and building for the Scala project.</span></span>

   ![The New Project dialog box](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="e5080-136">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="e5080-136">Select **Next**.</span></span>
3. <span data-ttu-id="e5080-137">In the next **New Project** dialog box, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="e5080-137">In the next **New Project** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="e5080-138">In the **Project name** box, enter a project name.</span><span class="sxs-lookup"><span data-stu-id="e5080-138">In the **Project name** box, enter a project name.</span></span>
    2. <span data-ttu-id="e5080-139">In the **Project location** box, enter a project location.</span><span class="sxs-lookup"><span data-stu-id="e5080-139">In the **Project location** box, enter a project location.</span></span>
    3. <span data-ttu-id="e5080-140">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder for Java JDK version 1.7 or later.</span><span class="sxs-lookup"><span data-stu-id="e5080-140">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder for Java JDK version 1.7 or later.</span></span> <span data-ttu-id="e5080-141">Select **Java 1.8** for the Spark 2.x cluster.</span><span class="sxs-lookup"><span data-stu-id="e5080-141">Select **Java 1.8** for the Spark 2.x cluster.</span></span> <span data-ttu-id="e5080-142">Select **Java 1.7** for the Spark 1.x cluster.</span><span class="sxs-lookup"><span data-stu-id="e5080-142">Select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="e5080-143">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="e5080-143">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>
    4. <span data-ttu-id="e5080-144">In the **Spark version** drop-down list, the Scala project creation wizard integrates the correct version for the Spark SDK and Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="e5080-144">In the **Spark version** drop-down list, the Scala project creation wizard integrates the correct version for the Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e5080-145">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="e5080-145">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="e5080-146">Otherwise, select **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="e5080-146">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="e5080-147">This example uses Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="e5080-147">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="e5080-148">Ensure that you are using the repository marked **Scala 2.10.x**.</span><span class="sxs-lookup"><span data-stu-id="e5080-148">Ensure that you are using the repository marked **Scala 2.10.x**.</span></span> <span data-ttu-id="e5080-149">Do not use the repository marked Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="e5080-149">Do not use the repository marked Scala 2.11.x.</span></span>
    
    ![Create IntelliJ Scala project properties](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)


4. <span data-ttu-id="e5080-151">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e5080-151">Select **Finish**.</span></span>
5. <span data-ttu-id="e5080-152">If the **Project** view is not already open, press **Alt+1** to open it.</span><span class="sxs-lookup"><span data-stu-id="e5080-152">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>
6. <span data-ttu-id="e5080-153">In **Project Explorer**, expand the project, and then select **src**.</span><span class="sxs-lookup"><span data-stu-id="e5080-153">In **Project Explorer**, expand the project, and then select **src**.</span></span>
7. <span data-ttu-id="e5080-154">Right-click **src**, point to **New**, and then select **Scala class**.</span><span class="sxs-lookup"><span data-stu-id="e5080-154">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>
8. <span data-ttu-id="e5080-155">In the **Name** box, enter a name.</span><span class="sxs-lookup"><span data-stu-id="e5080-155">In the **Name** box, enter a name.</span></span> <span data-ttu-id="e5080-156">In the **Kind** box, select **Object**.</span><span class="sxs-lookup"><span data-stu-id="e5080-156">In the **Kind** box, select **Object**.</span></span> <span data-ttu-id="e5080-157">Then, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5080-157">Then, select **OK**.</span></span>

    ![The Create New Scala Class dialog box](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="e5080-159">In the .scala file, paste the following code:</span><span class="sxs-lookup"><span data-stu-id="e5080-159">In the .scala file, paste the following code:</span></span>

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
                // Enforce that everything has been calculated and in cache.
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="e5080-160">On the **Build** menu, select **Build project**.</span><span class="sxs-lookup"><span data-stu-id="e5080-160">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="e5080-161">Ensure that the compilation finishes successfully.</span><span class="sxs-lookup"><span data-stu-id="e5080-161">Ensure that the compilation finishes successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="e5080-162">Link to the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="e5080-162">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="e5080-163">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span><span class="sxs-lookup"><span data-stu-id="e5080-163">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="e5080-164">To link to an emulator:</span><span class="sxs-lookup"><span data-stu-id="e5080-164">To link to an emulator:</span></span>

1. <span data-ttu-id="e5080-165">Open the project in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e5080-165">Open the project in IntelliJ.</span></span>
2. <span data-ttu-id="e5080-166">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e5080-166">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>
3. <span data-ttu-id="e5080-167">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span><span class="sxs-lookup"><span data-stu-id="e5080-167">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>
4. <span data-ttu-id="e5080-168">In the **Link A New Emulator** dialog box, enter the password that you've set for the root account of the Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e5080-168">In the **Link A New Emulator** dialog box, enter the password that you've set for the root account of the Hortonworks Sandbox.</span></span> <span data-ttu-id="e5080-169">Next, enter values similar to those used in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="e5080-169">Next, enter values similar to those used in the following screenshot.</span></span> <span data-ttu-id="e5080-170">Then, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5080-170">Then, select **OK**.</span></span> 

   ![The Link a New Emulator dialog box](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="e5080-172">To configure the emulator, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="e5080-172">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="e5080-173">When the emulator is successfully connected, the emulator (Hortonworks Sandbox) is listed on the HDInsight node.</span><span class="sxs-lookup"><span data-stu-id="e5080-173">When the emulator is successfully connected, the emulator (Hortonworks Sandbox) is listed on the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="e5080-174">Submit the Spark Scala application to the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="e5080-174">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="e5080-175">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span><span class="sxs-lookup"><span data-stu-id="e5080-175">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="e5080-176">To submit a project to an emulator:</span><span class="sxs-lookup"><span data-stu-id="e5080-176">To submit a project to an emulator:</span></span>

1. <span data-ttu-id="e5080-177">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e5080-177">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>
2. <span data-ttu-id="e5080-178">Complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="e5080-178">Complete the following steps:</span></span>

    1. <span data-ttu-id="e5080-179">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e5080-179">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>
    2. <span data-ttu-id="e5080-180">In the **Main class name** box, select or enter the main class name.</span><span class="sxs-lookup"><span data-stu-id="e5080-180">In the **Main class name** box, select or enter the main class name.</span></span> <span data-ttu-id="e5080-181">For this tutorial, the name is **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="e5080-181">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="e5080-182">Select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="e5080-182">Select **Submit**.</span></span> <span data-ttu-id="e5080-183">The job submission logs are shown in the Spark submission tool window.</span><span class="sxs-lookup"><span data-stu-id="e5080-183">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5080-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5080-184">Next steps</span></span>

- <span data-ttu-id="e5080-185">Learn how to [use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for an HDInsight Spark Linux cluster](../spark/apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="e5080-185">Learn how to [use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for an HDInsight Spark Linux cluster](../spark/apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="e5080-186">For a video about HDInsight Tools for IntelliJ, see [Introduce HDInsight Tools for IntelliJ for Spark development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="e5080-186">For a video about HDInsight Tools for IntelliJ, see [Introduce HDInsight Tools for IntelliJ for Spark development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="e5080-187">Learn how to [remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](../spark/apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="e5080-187">Learn how to [remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](../spark/apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="e5080-188">Learn how to [use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight Spark Linux cluster](../spark/apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="e5080-188">Learn how to [use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight Spark Linux cluster](../spark/apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="e5080-189">Learn how to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](../spark/apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="e5080-189">Learn how to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](../spark/apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="e5080-190">For a video about HDInsight Tools for Eclipse, see [Use HDInsight Tools for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="e5080-190">For a video about HDInsight Tools for Eclipse, see [Use HDInsight Tools for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
