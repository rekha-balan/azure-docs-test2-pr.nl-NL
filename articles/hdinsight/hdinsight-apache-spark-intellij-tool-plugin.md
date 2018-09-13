---
title: Use Azure Toolkit for IntelliJ to create Scala applications for Spark | Microsoft Docs
description: Use HDInsight Tools in Azure Toolkit for IntelliJ to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 15604aa21a2c57469e85a9ce6d7c0131001dac69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563882"
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-hdinsight-cluster"></a><span data-ttu-id="74cdf-103">Use Azure Toolkit for IntelliJ to create Spark applications for HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="74cdf-103">Use Azure Toolkit for IntelliJ to create Spark applications for HDInsight cluster</span></span>

<span data-ttu-id="74cdf-104">Use HDInsight Tools in Azure Toolkit for IntelliJ to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster, directly from them the IntelliJ IDE.</span><span class="sxs-lookup"><span data-stu-id="74cdf-104">Use HDInsight Tools in Azure Toolkit for IntelliJ to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster, directly from them the IntelliJ IDE.</span></span> <span data-ttu-id="74cdf-105">You can use the HDInsight Tools plugin in a few different ways:</span><span class="sxs-lookup"><span data-stu-id="74cdf-105">You can use the HDInsight Tools plugin in a few different ways:</span></span>

* <span data-ttu-id="74cdf-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="74cdf-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="74cdf-107">To access your Azure HDInsight Spark cluster resources</span><span class="sxs-lookup"><span data-stu-id="74cdf-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="74cdf-108">To develop and run a Scala Spark application locally</span><span class="sxs-lookup"><span data-stu-id="74cdf-108">To develop and run a Scala Spark application locally</span></span>

<span data-ttu-id="74cdf-109">You can also follow a video [here](https://mix.office.com/watch/1nqkqjt5xonza) to get you started.</span><span class="sxs-lookup"><span data-stu-id="74cdf-109">You can also follow a video [here](https://mix.office.com/watch/1nqkqjt5xonza) to get you started.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74cdf-110">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span><span class="sxs-lookup"><span data-stu-id="74cdf-110">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="74cdf-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74cdf-111">Prerequisites</span></span>
* <span data-ttu-id="74cdf-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="74cdf-112">An Azure subscription.</span></span> <span data-ttu-id="74cdf-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="74cdf-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="74cdf-114">An Apache Spark cluster on HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="74cdf-114">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="74cdf-115">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="74cdf-115">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="74cdf-116">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="74cdf-116">Oracle Java Development kit.</span></span> <span data-ttu-id="74cdf-117">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="74cdf-117">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="74cdf-118">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="74cdf-118">IntelliJ IDEA.</span></span> <span data-ttu-id="74cdf-119">This article uses version 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="74cdf-119">This article uses version 15.0.1.</span></span> <span data-ttu-id="74cdf-120">You can install it from [here](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="74cdf-120">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-hdinsight-tools-in-azure-toolkit-for-intellij"></a><span data-ttu-id="74cdf-121">Install HDInsight Tools in Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="74cdf-121">Install HDInsight Tools in Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="74cdf-122">HDInsight tools for IntelliJ is available as part of the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74cdf-122">HDInsight tools for IntelliJ is available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="74cdf-123">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="74cdf-123">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="log-into-your-azure-subscription"></a><span data-ttu-id="74cdf-124">Log into your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="74cdf-124">Log into your Azure subscription</span></span>
1. <span data-ttu-id="74cdf-125">Launch the IntelliJ IDE and open the Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="74cdf-125">Launch the IntelliJ IDE and open the Azure Explorer.</span></span> <span data-ttu-id="74cdf-126">From the **View** menu in the IDE, click **Tool Windows** and then click **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-126">From the **View** menu in the IDE, click **Tool Windows** and then click **Azure Explorer**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)
2. <span data-ttu-id="74cdf-128">Right-click the **Azure** node in the **Azure Explorer**, and then click **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-128">Right-click the **Azure** node in the **Azure Explorer**, and then click **Manage Subscriptions**.</span></span>
3. <span data-ttu-id="74cdf-129">In the **Manage Subscriptions** dialog box, click **Sign in** and enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="74cdf-129">In the **Manage Subscriptions** dialog box, click **Sign in** and enter your Azure credentials.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="74cdf-131">After you are logged in, the **Manage Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span><span class="sxs-lookup"><span data-stu-id="74cdf-131">After you are logged in, the **Manage Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="74cdf-132">Click **Close** in the dialog box.</span><span class="sxs-lookup"><span data-stu-id="74cdf-132">Click **Close** in the dialog box.</span></span>
5. <span data-ttu-id="74cdf-133">In the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span><span class="sxs-lookup"><span data-stu-id="74cdf-133">In the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="74cdf-135">You can further expand a cluster name node to see the resources (e.g. storage accounts) associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-135">You can further expand a cluster name node to see the resources (e.g. storage accounts) associated with the cluster.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="74cdf-137">Run a Spark Scala application on an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="74cdf-137">Run a Spark Scala application on an HDInsight Spark cluster</span></span>
1. <span data-ttu-id="74cdf-138">Launch IntelliJ IDEA and create a new project.</span><span class="sxs-lookup"><span data-stu-id="74cdf-138">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="74cdf-139">In the new project dialog box, make the following choices, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-139">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)
   
   * <span data-ttu-id="74cdf-141">From the left pane, select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-141">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="74cdf-142">From the right pane, select **Spark on HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-142">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="74cdf-143">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-143">Click **Next**.</span></span>
2. <span data-ttu-id="74cdf-144">In the next window, provide the project details.</span><span class="sxs-lookup"><span data-stu-id="74cdf-144">In the next window, provide the project details.</span></span>
   
   * <span data-ttu-id="74cdf-145">Provide a project name and project location.</span><span class="sxs-lookup"><span data-stu-id="74cdf-145">Provide a project name and project location.</span></span>
   * <span data-ttu-id="74cdf-146">For **Project SDK**, Java 1.7 or above for Spark 1.6 cluster and Java 1.8 for Spark 2.0 cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-146">For **Project SDK**, Java 1.7 or above for Spark 1.6 cluster and Java 1.8 for Spark 2.0 cluster.</span></span>
   * <span data-ttu-id="74cdf-147">For **Scala SDK**, click **Create**, click **Download**, and then select the version of Scala to use.</span><span class="sxs-lookup"><span data-stu-id="74cdf-147">For **Scala SDK**, click **Create**, click **Download**, and then select the version of Scala to use.</span></span>
   * * <span data-ttu-id="74cdf-148">Choose **JDK 1.8 and Scala 2.11.x** if you're willing to submit job to Spark 2.0 cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-148">Choose **JDK 1.8 and Scala 2.11.x** if you're willing to submit job to Spark 2.0 cluster.</span></span>
   * * <span data-ttu-id="74cdf-149">Choose **JDK 1.7 or above and Scala 2.10.x** if you're willing to submit job to Spark 1.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-149">Choose **JDK 1.7 or above and Scala 2.10.x** if you're willing to submit job to Spark 1.6 cluster.</span></span>

        ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/show-scala2.11.x-select.png)
   * <span data-ttu-id="74cdf-150">For **Spark SDK**, download and use the SDK from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409)(spark-assembly-2.0.0-hadoop2.7.0-SNAPSHOT.jar is for Spark 2.0 cluster and spark-assembly-x.jar is for Spark 1.6 cluster).</span><span class="sxs-lookup"><span data-stu-id="74cdf-150">For **Spark SDK**, download and use the SDK from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409)(spark-assembly-2.0.0-hadoop2.7.0-SNAPSHOT.jar is for Spark 2.0 cluster and spark-assembly-x.jar is for Spark 1.6 cluster).</span></span> <span data-ttu-id="74cdf-151">You can also ignore this and use the [Spark Maven repository](http://mvnrepository.com/search?q=spark) instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span><span class="sxs-lookup"><span data-stu-id="74cdf-151">You can also ignore this and use the [Spark Maven repository](http://mvnrepository.com/search?q=spark) instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span></span> <span data-ttu-id="74cdf-152">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 for Spark 1.6 cluster and marked as Scala 2.11 for Spark 2.0 cluster.)</span><span class="sxs-lookup"><span data-stu-id="74cdf-152">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 for Spark 1.6 cluster and marked as Scala 2.11 for Spark 2.0 cluster.)</span></span>
     
       ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-scala-project-details.png)
   * <span data-ttu-id="74cdf-154">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-154">Click **Finish**.</span></span>
3. <span data-ttu-id="74cdf-155">The Spark project will automatically create an artifact for you.</span><span class="sxs-lookup"><span data-stu-id="74cdf-155">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="74cdf-156">To see the artifact, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="74cdf-156">To see the artifact, follow these steps.</span></span>
   
   1. <span data-ttu-id="74cdf-157">From the **File** menu, click **Project Structure**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-157">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="74cdf-158">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span><span class="sxs-lookup"><span data-stu-id="74cdf-158">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
      <span data-ttu-id="74cdf-160">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span><span class="sxs-lookup"><span data-stu-id="74cdf-160">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>
4. <span data-ttu-id="74cdf-161">In the **Project Structure** dialog box, click **Project**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-161">In the **Project Structure** dialog box, click **Project**.</span></span> <span data-ttu-id="74cdf-162">If the **Project SDK** is set to 1.8, make sure the **Project language level** is set to **7 - Diamonds, ARM, multi-catch, etc**(It's optional for Spark 2.0 cluster).</span><span class="sxs-lookup"><span data-stu-id="74cdf-162">If the **Project SDK** is set to 1.8, make sure the **Project language level** is set to **7 - Diamonds, ARM, multi-catch, etc**(It's optional for Spark 2.0 cluster).</span></span>
   
    ![Set project language level](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/set-project-language-level.png)
5. <span data-ttu-id="74cdf-164">Add your application source code.</span><span class="sxs-lookup"><span data-stu-id="74cdf-164">Add your application source code.</span></span>
   
   1. <span data-ttu-id="74cdf-165">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-165">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>
      
       ![Add source code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)
   2. <span data-ttu-id="74cdf-167">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-167">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>
      
       ![Add source code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)
   3. <span data-ttu-id="74cdf-169">In the **MyClusterApp.scala** file, paste the following code.</span><span class="sxs-lookup"><span data-stu-id="74cdf-169">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="74cdf-170">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-170">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

            import org.apache.spark.SparkConf
            import org.apache.spark.SparkContext

            object MyClusterApp{
              def main (arg: Array[String]): Unit = {
                val conf = new SparkConf().setAppName("MyClusterApp")
                val sc = new SparkContext(conf)

                val rdd = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

                //find the rows which have only one digit in the 7th column in the CSV
                val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

                rdd1.saveAsTextFile("wasbs:///HVACOut")
              }

            }

1. <span data-ttu-id="74cdf-171">Run the application on an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-171">Run the application on an HDInsight Spark cluster.</span></span>
   
   1. <span data-ttu-id="74cdf-172">From the **Project Explorer**, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-172">From the **Project Explorer**, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
       ![Submit Spark application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)
   2. <span data-ttu-id="74cdf-174">You will be prompted to enter your Azure subscription credentials.</span><span class="sxs-lookup"><span data-stu-id="74cdf-174">You will be prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="74cdf-175">In the **Spark Submission** dialog box, provide the following values.</span><span class="sxs-lookup"><span data-stu-id="74cdf-175">In the **Spark Submission** dialog box, provide the following values.</span></span>
      
      * <span data-ttu-id="74cdf-176">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span><span class="sxs-lookup"><span data-stu-id="74cdf-176">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="74cdf-177">You need either select an Artifact from the IntelliJ project, or select one from hard disk.</span><span class="sxs-lookup"><span data-stu-id="74cdf-177">You need either select an Artifact from the IntelliJ project, or select one from hard disk.</span></span>
      * <span data-ttu-id="74cdf-178">Against the **Main class name** text box, click the ellipsis (![ellipsis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/ellipsis.png) ), select the main class in your application source code, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-178">Against the **Main class name** text box, click the ellipsis (![ellipsis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/ellipsis.png) ), select the main class in your application source code, and then click **OK**.</span></span>
        
          ![Submit Spark application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)
      * <span data-ttu-id="74cdf-180">Because the application code in this example does not require any command line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span><span class="sxs-lookup"><span data-stu-id="74cdf-180">Because the application code in this example does not require any command line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
      * <span data-ttu-id="74cdf-181">After providing all the inputs, the dialog box should resemble the following.</span><span class="sxs-lookup"><span data-stu-id="74cdf-181">After providing all the inputs, the dialog box should resemble the following.</span></span>
        
          ![Submit Spark application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)
      * <span data-ttu-id="74cdf-183">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-183">Click **Submit**.</span></span>
   3. <span data-ttu-id="74cdf-184">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span><span class="sxs-lookup"><span data-stu-id="74cdf-184">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="74cdf-185">You can also stop the application by clicking the red button in the "Spark Submission" window.</span><span class="sxs-lookup"><span data-stu-id="74cdf-185">You can also stop the application by clicking the red button in the "Spark Submission" window.</span></span>
      
       ![Spark Application Result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="74cdf-187">In the next section, you learn how to access the job output using the HDInsight Tools in Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74cdf-187">In the next section, you learn how to access the job output using the HDInsight Tools in Azure Toolkit for IntelliJ.</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-using-the-hdinsight-tools-in-azure-toolkit-for-intellij"></a><span data-ttu-id="74cdf-188">Access and manage HDInsight Spark clusters using the HDInsight Tools in Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="74cdf-188">Access and manage HDInsight Spark clusters using the HDInsight Tools in Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="74cdf-189">You can perform a variety of operations using the HDInsight tools that are part of Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74cdf-189">You can perform a variety of operations using the HDInsight tools that are part of Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view-directly-from-the-hdinsight-tools"></a><span data-ttu-id="74cdf-190">Access the job view directly from the HDInsight tools</span><span class="sxs-lookup"><span data-stu-id="74cdf-190">Access the job view directly from the HDInsight tools</span></span>
1. <span data-ttu-id="74cdf-191">From the **Azure Explorer**, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-191">From the **Azure Explorer**, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span></span>
2. <span data-ttu-id="74cdf-192">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-192">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="74cdf-193">Click the application name for which you want to see more details.</span><span class="sxs-lookup"><span data-stu-id="74cdf-193">Click the application name for which you want to see more details.</span></span>
   
    ![Access job view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
3. <span data-ttu-id="74cdf-195">The boxes for **Error Message**, **Job Output**, **Livy Job Logs**, and **Spark Driver Logs** are populated based on the application you select.</span><span class="sxs-lookup"><span data-stu-id="74cdf-195">The boxes for **Error Message**, **Job Output**, **Livy Job Logs**, and **Spark Driver Logs** are populated based on the application you select.</span></span>
4. <span data-ttu-id="74cdf-196">You can also open the **Spark History UI** and the **YARN UI** (at the application level) by clicking the respective buttons at the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="74cdf-196">You can also open the **Spark History UI** and the **YARN UI** (at the application level) by clicking the respective buttons at the top of the screen.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="74cdf-197">Access the Spark History Server</span><span class="sxs-lookup"><span data-stu-id="74cdf-197">Access the Spark History Server</span></span>
1. <span data-ttu-id="74cdf-198">From the **Azure Explorer**, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-198">From the **Azure Explorer**, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="74cdf-199">When prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-199">When prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="74cdf-200">You must have specified these while provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-200">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="74cdf-201">In the Spark History Server dashboard, you can look for the application you just finished running by using the application name.</span><span class="sxs-lookup"><span data-stu-id="74cdf-201">In the Spark History Server dashboard, you can look for the application you just finished running by using the application name.</span></span> <span data-ttu-id="74cdf-202">In the code above, you set the application name using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="74cdf-202">In the code above, you set the application name using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="74cdf-203">Hence, your Spark application name was **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-203">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="launch-the-ambari-portal"></a><span data-ttu-id="74cdf-204">Launch the Ambari portal</span><span class="sxs-lookup"><span data-stu-id="74cdf-204">Launch the Ambari portal</span></span>
<span data-ttu-id="74cdf-205">From the **Azure Explorer**, expand **HDInsight**, right-click your Spark cluster name and then select **Open Cluster Management Portal (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-205">From the **Azure Explorer**, expand **HDInsight**, right-click your Spark cluster name and then select **Open Cluster Management Portal (Ambari)**.</span></span> <span data-ttu-id="74cdf-206">When prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-206">When prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="74cdf-207">You must have specified these while provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-207">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="74cdf-208">Manage Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="74cdf-208">Manage Azure subscriptions</span></span>
<span data-ttu-id="74cdf-209">By default, the HDInsight tools lists the Spark clusters from all your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="74cdf-209">By default, the HDInsight tools lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="74cdf-210">If required, you can specify the subscriptions for which you want to access the cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-210">If required, you can specify the subscriptions for which you want to access the cluster.</span></span> <span data-ttu-id="74cdf-211">From the **Azure Explorer**, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-211">From the **Azure Explorer**, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> <span data-ttu-id="74cdf-212">From the dialog box, clear the check boxes against the subscription that you do not want to access and then click **Close**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-212">From the dialog box, clear the check boxes against the subscription that you do not want to access and then click **Close**.</span></span> <span data-ttu-id="74cdf-213">You can also click **Sign Out** if you want to log off from your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="74cdf-213">You can also click **Sign Out** if you want to log off from your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="74cdf-214">Run a Spark Scala application locally</span><span class="sxs-lookup"><span data-stu-id="74cdf-214">Run a Spark Scala application locally</span></span>
<span data-ttu-id="74cdf-215">You can use the HDInsight Tools in Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span><span class="sxs-lookup"><span data-stu-id="74cdf-215">You can use the HDInsight Tools in Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="74cdf-216">Typically, such applications do not need access to cluster resources such as storage container and can be run and tested locally.</span><span class="sxs-lookup"><span data-stu-id="74cdf-216">Typically, such applications do not need access to cluster resources such as storage container and can be run and tested locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="74cdf-217">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="74cdf-217">Prerequisite</span></span>
<span data-ttu-id="74cdf-218">While running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span><span class="sxs-lookup"><span data-stu-id="74cdf-218">While running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="74cdf-219">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-219">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="74cdf-220">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-220">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="74cdf-221">Run a local Spark Scala application</span><span class="sxs-lookup"><span data-stu-id="74cdf-221">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="74cdf-222">Launch IntelliJ IDEA and create a new project.</span><span class="sxs-lookup"><span data-stu-id="74cdf-222">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="74cdf-223">In the new project dialog box, make the following choices, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-223">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)
   
   * <span data-ttu-id="74cdf-225">From the left pane, select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-225">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="74cdf-226">From the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-226">From the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>
   * <span data-ttu-id="74cdf-227">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-227">Click **Next**.</span></span>
2. <span data-ttu-id="74cdf-228">In the next window, provide the project details.</span><span class="sxs-lookup"><span data-stu-id="74cdf-228">In the next window, provide the project details.</span></span>
   
   * <span data-ttu-id="74cdf-229">Provide a project name and project location.</span><span class="sxs-lookup"><span data-stu-id="74cdf-229">Provide a project name and project location.</span></span>
   * <span data-ttu-id="74cdf-230">For **Project SDK**, make sure you provide a Java version greater than 7.</span><span class="sxs-lookup"><span data-stu-id="74cdf-230">For **Project SDK**, make sure you provide a Java version greater than 7.</span></span>
   * <span data-ttu-id="74cdf-231">For **Scala SDK**, click **Create**, click **Download**, and then select the version of Scala to use.**Scala 2.11.x for Spark 2.0 and Scala 2.10.x for Spark 1.6**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-231">For **Scala SDK**, click **Create**, click **Download**, and then select the version of Scala to use.**Scala 2.11.x for Spark 2.0 and Scala 2.10.x for Spark 1.6**.</span></span>
     
       ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-scala-version.png)
   * <span data-ttu-id="74cdf-233">For **Spark SDK**, download and use the SDK from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="74cdf-233">For **Spark SDK**, download and use the SDK from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span> <span data-ttu-id="74cdf-234">You can also ignore this and use the [Spark Maven repository](http://mvnrepository.com/search?q=spark) instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span><span class="sxs-lookup"><span data-stu-id="74cdf-234">You can also ignore this and use the [Spark Maven repository](http://mvnrepository.com/search?q=spark) instead, however please make sure you have the right maven repository installed to develop your Spark applications.</span></span> <span data-ttu-id="74cdf-235">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 for Spark 1.6 cluster and marked as Scala 2.11 for Spark 2.0 cluster.)</span><span class="sxs-lookup"><span data-stu-id="74cdf-235">(For example, you need to make sure you have the Spark Streaming part installed if you are using Spark Streaming; Also please make sure you are using the repository marked as Scala 2.10 for Spark 1.6 cluster and marked as Scala 2.11 for Spark 2.0 cluster.)</span></span>
     
       ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-create-project.png)
   * <span data-ttu-id="74cdf-237">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-237">Click **Finish**.</span></span>
3. <span data-ttu-id="74cdf-238">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="74cdf-238">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Local Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)
4. <span data-ttu-id="74cdf-240">Right click on the **LogQuery** application, and then click **"Run 'LogQuery'"**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-240">Right click on the **LogQuery** application, and then click **"Run 'LogQuery'"**.</span></span> <span data-ttu-id="74cdf-241">You will see an output like this in the **Run** tab at the bottom.</span><span class="sxs-lookup"><span data-stu-id="74cdf-241">You will see an output like this in the **Run** tab at the bottom.</span></span>
   
   ![Spark Application local run result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-the-hdinsight-tools-in-azure-toolkit-for-intellij"></a><span data-ttu-id="74cdf-243">Convert existing IntelliJ IDEA applications to use the HDInsight Tools in Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="74cdf-243">Convert existing IntelliJ IDEA applications to use the HDInsight Tools in Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="74cdf-244">You can also convert your existing Spark Scala applications created in IntelliJ IDEA to be compatible with the HDInsight Tools in Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74cdf-244">You can also convert your existing Spark Scala applications created in IntelliJ IDEA to be compatible with the HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="74cdf-245">This will enable you to use the tool to submit the applications to an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="74cdf-245">This will enable you to use the tool to submit the applications to an HDInsight Spark cluster.</span></span> <span data-ttu-id="74cdf-246">You can do so by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="74cdf-246">You can do so by performing the following steps:</span></span>

1. <span data-ttu-id="74cdf-247">For an existing Spark Scala appliction created using IntelliJ IDEA, open the associated .iml file.</span><span class="sxs-lookup"><span data-stu-id="74cdf-247">For an existing Spark Scala appliction created using IntelliJ IDEA, open the associated .iml file.</span></span>
2. <span data-ttu-id="74cdf-248">At the root level, you will see a **module** element like this:</span><span class="sxs-lookup"><span data-stu-id="74cdf-248">At the root level, you will see a **module** element like this:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">
3. <span data-ttu-id="74cdf-249">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span><span class="sxs-lookup"><span data-stu-id="74cdf-249">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">
4. <span data-ttu-id="74cdf-250">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="74cdf-250">Save the changes.</span></span> <span data-ttu-id="74cdf-251">Your application should now be compatible with the HDInsight Tools in Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74cdf-251">Your application should now be compatible with the HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="74cdf-252">You can test this by right-clicking on the project name in the Project Explorer.</span><span class="sxs-lookup"><span data-stu-id="74cdf-252">You can test this by right-clicking on the project name in the Project Explorer.</span></span> <span data-ttu-id="74cdf-253">The pop-up menu should now have the option to **Submit Spark Application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="74cdf-253">The pop-up menu should now have the option to **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="74cdf-254">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="74cdf-254">Troubleshooting</span></span>
### <a name="please-use-a-larger-heap-size-error-in-local-run"></a><span data-ttu-id="74cdf-255">"Please use a larger heap size" error in local run</span><span class="sxs-lookup"><span data-stu-id="74cdf-255">"Please use a larger heap size" error in local run</span></span>
<span data-ttu-id="74cdf-256">In Spark 1.6, If you are using a 32-bit Java SDK during local run, you may encounter the following errors:</span><span class="sxs-lookup"><span data-stu-id="74cdf-256">In Spark 1.6, If you are using a 32-bit Java SDK during local run, you may encounter the following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="74cdf-257">This is because the heap size is not large enough for Spark to run, since Spark requires at least 471MB (you can get more details from [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081) if you want).</span><span class="sxs-lookup"><span data-stu-id="74cdf-257">This is because the heap size is not large enough for Spark to run, since Spark requires at least 471MB (you can get more details from [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081) if you want).</span></span> <span data-ttu-id="74cdf-258">One simple solution is to use a 64-bit Java SDK.</span><span class="sxs-lookup"><span data-stu-id="74cdf-258">One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="74cdf-259">You can also change the JVM settings in IntelliJ by adding the following options:</span><span class="sxs-lookup"><span data-stu-id="74cdf-259">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Spark Application local run result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="feedback--known-issues"></a><span data-ttu-id="74cdf-261">Feedback & Known issues</span><span class="sxs-lookup"><span data-stu-id="74cdf-261">Feedback & Known issues</span></span>
<span data-ttu-id="74cdf-262">Currently viewing Spark outputs directly is not supported and we are working on that.</span><span class="sxs-lookup"><span data-stu-id="74cdf-262">Currently viewing Spark outputs directly is not supported and we are working on that.</span></span>

<span data-ttu-id="74cdf-263">If you have any suggestions or feedbacks, or if you encounter any problems when using this tool, feel free to drop us an email at hdivstool at microsoft dot com.</span><span class="sxs-lookup"><span data-stu-id="74cdf-263">If you have any suggestions or feedbacks, or if you encounter any problems when using this tool, feel free to drop us an email at hdivstool at microsoft dot com.</span></span>

## <a name="seealso"></a><span data-ttu-id="74cdf-264">See also</span><span class="sxs-lookup"><span data-stu-id="74cdf-264">See also</span></span>
* [<span data-ttu-id="74cdf-265">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="74cdf-265">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="74cdf-266">Scenarios</span><span class="sxs-lookup"><span data-stu-id="74cdf-266">Scenarios</span></span>
* [<span data-ttu-id="74cdf-267">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="74cdf-267">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="74cdf-268">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="74cdf-268">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="74cdf-269">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="74cdf-269">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="74cdf-270">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="74cdf-270">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="74cdf-271">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="74cdf-271">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="74cdf-272">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="74cdf-272">Create and run applications</span></span>
* [<span data-ttu-id="74cdf-273">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="74cdf-273">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="74cdf-274">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="74cdf-274">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="74cdf-275">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="74cdf-275">Tools and extensions</span></span>
* [<span data-ttu-id="74cdf-276">Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="74cdf-276">Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="74cdf-277">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span><span class="sxs-lookup"><span data-stu-id="74cdf-277">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="74cdf-278">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="74cdf-278">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="74cdf-279">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="74cdf-279">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="74cdf-280">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="74cdf-280">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="74cdf-281">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="74cdf-281">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="74cdf-282">Manage resources</span><span class="sxs-lookup"><span data-stu-id="74cdf-282">Manage resources</span></span>
* [<span data-ttu-id="74cdf-283">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="74cdf-283">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="74cdf-284">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="74cdf-284">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
























