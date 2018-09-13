---
title: Use Azure Toolkit for Eclipse to create Scala applications for Spark | Microsoft Docs
description: Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster, directly from them the Eclipse IDE.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: 1a0f1dc61c9f617e117b5b79a603fd3c2bc9b3d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551281"
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-hdinsight-cluster"></a><span data-ttu-id="17596-103">Use Azure Toolkit for Eclipse to create Spark applications for HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="17596-103">Use Azure Toolkit for Eclipse to create Spark applications for HDInsight cluster</span></span>

<span data-ttu-id="17596-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster, directly from them the Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="17596-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster, directly from them the Eclipse IDE.</span></span> <span data-ttu-id="17596-105">You can use the HDInsight Tools plugin in a few different ways:</span><span class="sxs-lookup"><span data-stu-id="17596-105">You can use the HDInsight Tools plugin in a few different ways:</span></span>

* <span data-ttu-id="17596-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="17596-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="17596-107">To access your Azure HDInsight Spark cluster resources</span><span class="sxs-lookup"><span data-stu-id="17596-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="17596-108">To develop and run a Scala Spark application locally</span><span class="sxs-lookup"><span data-stu-id="17596-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17596-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span><span class="sxs-lookup"><span data-stu-id="17596-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="17596-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="17596-110">Prerequisites</span></span>
* <span data-ttu-id="17596-111">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="17596-111">An Azure subscription.</span></span> <span data-ttu-id="17596-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="17596-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="17596-113">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17596-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="17596-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="17596-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="17596-115">Oracle Java Development kit version 7 and version 8.</span><span class="sxs-lookup"><span data-stu-id="17596-115">Oracle Java Development kit version 7 and version 8.</span></span> 
  
  * <span data-ttu-id="17596-116">**Java SDK 7** is used for compiling Spark projects as the HDInsight clusters support Java version 7.</span><span class="sxs-lookup"><span data-stu-id="17596-116">**Java SDK 7** is used for compiling Spark projects as the HDInsight clusters support Java version 7.</span></span> <span data-ttu-id="17596-117">You can download Java SDK 7 from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html).</span><span class="sxs-lookup"><span data-stu-id="17596-117">You can download Java SDK 7 from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html).</span></span>
  * <span data-ttu-id="17596-118">**Java SDK 8** is used for Eclipse IDE runtime.</span><span class="sxs-lookup"><span data-stu-id="17596-118">**Java SDK 8** is used for Eclipse IDE runtime.</span></span> <span data-ttu-id="17596-119">You can download it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="17596-119">You can download it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="17596-120">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="17596-120">Eclipse IDE.</span></span> <span data-ttu-id="17596-121">This article uses Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="17596-121">This article uses Eclipse Neon.</span></span> <span data-ttu-id="17596-122">You can install it from [here](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="17596-122">You can install it from [here](https://www.eclipse.org/downloads/).</span></span>
* <span data-ttu-id="17596-123">Scala IDE for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="17596-123">Scala IDE for Eclipse.</span></span> 
  
  * <span data-ttu-id="17596-124">**If you have Eclipse IDE installed**, you can add the Scala IDE plugin by going to **Help** -> **Install New SoftWare**, and add [http://download.scala-ide.org/sdk/lithium/e44/scala211/stable/site](http://download.scala-ide.org/sdk/lithium/e44/scala211/stable/site) as source to download Scala Plugin for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="17596-124">**If you have Eclipse IDE installed**, you can add the Scala IDE plugin by going to **Help** -> **Install New SoftWare**, and add [http://download.scala-ide.org/sdk/lithium/e44/scala211/stable/site](http://download.scala-ide.org/sdk/lithium/e44/scala211/stable/site) as source to download Scala Plugin for Eclipse.</span></span> 
  * <span data-ttu-id="17596-125">**If you do not have Eclipse IDE installed**, you can install Scala IDE directly from [here](http://scala-ide.org/download/sdk.html).</span><span class="sxs-lookup"><span data-stu-id="17596-125">**If you do not have Eclipse IDE installed**, you can install Scala IDE directly from [here](http://scala-ide.org/download/sdk.html).</span></span> <span data-ttu-id="17596-126">You can download the .zip file from this link, extract it, navigate to the **/eclipse** folder, and then run **eclipse.exe** file from there.</span><span class="sxs-lookup"><span data-stu-id="17596-126">You can download the .zip file from this link, extract it, navigate to the **/eclipse** folder, and then run **eclipse.exe** file from there.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="17596-127">The steps in this document are based on using Eclipse IDE with Scala plugin installed.</span><span class="sxs-lookup"><span data-stu-id="17596-127">The steps in this document are based on using Eclipse IDE with Scala plugin installed.</span></span>
    > 
    > 
* <span data-ttu-id="17596-128">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="17596-128">Spark SDK.</span></span> <span data-ttu-id="17596-129">You can download it from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="17596-129">You can download it from [here](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>
* <span data-ttu-id="17596-130">Install e(fx)clipse from [https://www.eclipse.org/efxclipse/install.html](https://www.eclipse.org/efxclipse/install.html).</span><span class="sxs-lookup"><span data-stu-id="17596-130">Install e(fx)clipse from [https://www.eclipse.org/efxclipse/install.html](https://www.eclipse.org/efxclipse/install.html).</span></span>

## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="17596-131">Install HDInsight Tools in Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="17596-131">Install HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="17596-132">HDInsight tools for Eclipse is available as part of the Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="17596-132">HDInsight tools for Eclipse is available as part of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="17596-133">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="17596-133">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>

## <a name="log-into-your-azure-subscription"></a><span data-ttu-id="17596-134">Log into your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="17596-134">Log into your Azure subscription</span></span>
1. <span data-ttu-id="17596-135">Launch the Eclipse IDE and open the Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="17596-135">Launch the Eclipse IDE and open the Azure Explorer.</span></span> <span data-ttu-id="17596-136">From the **Window** menu in the IDE, click **Show View** and then click **Other**.</span><span class="sxs-lookup"><span data-stu-id="17596-136">From the **Window** menu in the IDE, click **Show View** and then click **Other**.</span></span> <span data-ttu-id="17596-137">From the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="17596-137">From the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="17596-139">Right-click the **Azure** node in the **Azure Explorer**, and then click **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="17596-139">Right-click the **Azure** node in the **Azure Explorer**, and then click **Manage Subscriptions**.</span></span>
3. <span data-ttu-id="17596-140">In the **Manage Subscriptions** dialog box, click **Sign in** and enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="17596-140">In the **Manage Subscriptions** dialog box, click **Sign in** and enter your Azure credentials.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="17596-142">After you are logged in, the **Manage Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span><span class="sxs-lookup"><span data-stu-id="17596-142">After you are logged in, the **Manage Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="17596-143">Click **Close** in the dialog box.</span><span class="sxs-lookup"><span data-stu-id="17596-143">Click **Close** in the dialog box.</span></span>
5. <span data-ttu-id="17596-144">In the Azure Explorer tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span><span class="sxs-lookup"><span data-stu-id="17596-144">In the Azure Explorer tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="17596-146">You can further expand a cluster name node to see the resources (e.g. storage accounts) associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-146">You can further expand a cluster name node to see the resources (e.g. storage accounts) associated with the cluster.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)

## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="17596-148">Set up a Spark Scala project for an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="17596-148">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>
1. <span data-ttu-id="17596-149">From the Eclipse IDE work space, click **File**, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="17596-149">From the Eclipse IDE work space, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="17596-150">In the **New Project** wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17596-150">In the **New Project** wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="17596-152">In the **New HDInsight Scala Project** dialog box, enter/select values as shown in the image below, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17596-152">In the **New HDInsight Scala Project** dialog box, enter/select values as shown in the image below, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
   
   * <span data-ttu-id="17596-154">Enter a name for the project.</span><span class="sxs-lookup"><span data-stu-id="17596-154">Enter a name for the project.</span></span>
   * <span data-ttu-id="17596-155">In the **JRE** box, make sure **Use an execution environment JRE** is set to **JavaSE-1.7**.</span><span class="sxs-lookup"><span data-stu-id="17596-155">In the **JRE** box, make sure **Use an execution environment JRE** is set to **JavaSE-1.7**.</span></span>
   * <span data-ttu-id="17596-156">Make sure Spark SDK is set to the location where you downloaded the SDK.</span><span class="sxs-lookup"><span data-stu-id="17596-156">Make sure Spark SDK is set to the location where you downloaded the SDK.</span></span> <span data-ttu-id="17596-157">The link to the download location is included in the [Prerequisites](#prerequisites) earlier in this topic.</span><span class="sxs-lookup"><span data-stu-id="17596-157">The link to the download location is included in the [Prerequisites](#prerequisites) earlier in this topic.</span></span> <span data-ttu-id="17596-158">You can also download the SDK from the link included in this dialog box, as shown in the image above.</span><span class="sxs-lookup"><span data-stu-id="17596-158">You can also download the SDK from the link included in this dialog box, as shown in the image above.</span></span>     
4. <span data-ttu-id="17596-159">In the next dialog box, click the **Libraries** tab, and then double-click **JRE System Library [JavaSE-1.7]**.</span><span class="sxs-lookup"><span data-stu-id="17596-159">In the next dialog box, click the **Libraries** tab, and then double-click **JRE System Library [JavaSE-1.7]**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
5. <span data-ttu-id="17596-161">In the **Edit Library** dialog box, make sure **Execution Environment** is set to  **JavaSE-1.7(jdk1.7.0_79)**.</span><span class="sxs-lookup"><span data-stu-id="17596-161">In the **Edit Library** dialog box, make sure **Execution Environment** is set to  **JavaSE-1.7(jdk1.7.0_79)**.</span></span> <span data-ttu-id="17596-162">If this is not available as an option, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="17596-162">If this is not available as an option, follow the steps below.</span></span>
   
   1. <span data-ttu-id="17596-163">Select the **Alternate JRE** option and see if **JavaSE-1.7(jdk1.7.0_79)** is available.</span><span class="sxs-lookup"><span data-stu-id="17596-163">Select the **Alternate JRE** option and see if **JavaSE-1.7(jdk1.7.0_79)** is available.</span></span>
   2. <span data-ttu-id="17596-164">If not, click the **Installed JREs** button.</span><span class="sxs-lookup"><span data-stu-id="17596-164">If not, click the **Installed JREs** button.</span></span>
      
         ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-5.png)
   3. <span data-ttu-id="17596-166">In the **Installed JREs** dialog box, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="17596-166">In the **Installed JREs** dialog box, click **Add**.</span></span>
      
         ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-6.png)    
   4. <span data-ttu-id="17596-168">In the **JRE Type** dialog box, select **Standard VM**, and then click **Next**</span><span class="sxs-lookup"><span data-stu-id="17596-168">In the **JRE Type** dialog box, select **Standard VM**, and then click **Next**</span></span>
      
         ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-7.png)    
   5. <span data-ttu-id="17596-170">In the **JRE Definition** dialog box, click Directory, and then navigate to the location for JDK 7 installation, and select the root folder for **jdk1.7.0_79**.</span><span class="sxs-lookup"><span data-stu-id="17596-170">In the **JRE Definition** dialog box, click Directory, and then navigate to the location for JDK 7 installation, and select the root folder for **jdk1.7.0_79**.</span></span>
      
         ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-8.png)    
   6. <span data-ttu-id="17596-172">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="17596-172">Click **Finish**.</span></span> <span data-ttu-id="17596-173">In the **Installed JREs** dialog box, select the newly added JRE, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="17596-173">In the **Installed JREs** dialog box, select the newly added JRE, and then click **OK**.</span></span>
      
          ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-9.png)
   7. <span data-ttu-id="17596-174">The newly added JRE should be listed for **Execution Environment**.</span><span class="sxs-lookup"><span data-stu-id="17596-174">The newly added JRE should be listed for **Execution Environment**.</span></span> <span data-ttu-id="17596-175">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="17596-175">Click **Finish**.</span></span>
      
            ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-10.png)
6. <span data-ttu-id="17596-176">Back on the **Libraries** tab, double-click **Scala Library Container[2.11.8]**.</span><span class="sxs-lookup"><span data-stu-id="17596-176">Back on the **Libraries** tab, double-click **Scala Library Container[2.11.8]**.</span></span> <span data-ttu-id="17596-177">In the **Edit Library** dialog box, select **Fixed Scala Library container:2.10.6**.</span><span class="sxs-lookup"><span data-stu-id="17596-177">In the **Edit Library** dialog box, select **Fixed Scala Library container:2.10.6**.</span></span> 
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-11.png)
   
    <span data-ttu-id="17596-179">Click **Finish** until you exit the project settings dialog box.</span><span class="sxs-lookup"><span data-stu-id="17596-179">Click **Finish** until you exit the project settings dialog box.</span></span>

## <a name="create-a-scala-application-for-hdinsight-spark-cluster"></a><span data-ttu-id="17596-180">Create a Scala application for HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="17596-180">Create a Scala application for HDInsight Spark cluster</span></span>
1. <span data-ttu-id="17596-181">In the already open Eclipse IDE, from the **Package Explorer**, expand the project you created earlier, right-click **src**, point to **New**, and then click **Other**.</span><span class="sxs-lookup"><span data-stu-id="17596-181">In the already open Eclipse IDE, from the **Package Explorer**, expand the project you created earlier, right-click **src**, point to **New**, and then click **Other**.</span></span>
2. <span data-ttu-id="17596-182">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17596-182">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="17596-184">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="17596-184">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="17596-186">Paste the following code in the text editor.</span><span class="sxs-lookup"><span data-stu-id="17596-186">Paste the following code in the text editor.</span></span>
   
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
5. <span data-ttu-id="17596-187">Run the application on an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-187">Run the application on an HDInsight Spark cluster.</span></span>
   
   1. <span data-ttu-id="17596-188">From the **Package Explorer**, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="17596-188">From the **Package Explorer**, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   2. <span data-ttu-id="17596-189">In the **Spark Submission** dialog box, provide the following values.</span><span class="sxs-lookup"><span data-stu-id="17596-189">In the **Spark Submission** dialog box, provide the following values.</span></span>
      
      * <span data-ttu-id="17596-190">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span><span class="sxs-lookup"><span data-stu-id="17596-190">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="17596-191">You need to either select an Artifact from the Eclipse project, or select one from hard disk.</span><span class="sxs-lookup"><span data-stu-id="17596-191">You need to either select an Artifact from the Eclipse project, or select one from hard disk.</span></span>
      * <span data-ttu-id="17596-192">Against the **Main class name** text box, enter the name of the object you specified in the code (see image below).</span><span class="sxs-lookup"><span data-stu-id="17596-192">Against the **Main class name** text box, enter the name of the object you specified in the code (see image below).</span></span>
        
          ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
      * <span data-ttu-id="17596-194">Because the application code in this example does not require any command line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span><span class="sxs-lookup"><span data-stu-id="17596-194">Because the application code in this example does not require any command line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
      * <span data-ttu-id="17596-195">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="17596-195">Click **Submit**.</span></span>
   3. <span data-ttu-id="17596-196">The **Spark Submission** tab should start displaying the progress.</span><span class="sxs-lookup"><span data-stu-id="17596-196">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="17596-197">You can stop the application by clicking the red button in the "Spark Submission" window.</span><span class="sxs-lookup"><span data-stu-id="17596-197">You can stop the application by clicking the red button in the "Spark Submission" window.</span></span> <span data-ttu-id="17596-198">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span><span class="sxs-lookup"><span data-stu-id="17596-198">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span></span>
      
       ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)
      
      <span data-ttu-id="17596-200">In the next section, you learn how to access the job output using the HDInsight Tools in Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="17596-200">In the next section, you learn how to access the job output using the HDInsight Tools in Azure Toolkit for Eclipse.</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-using-the-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="17596-201">Access and manage HDInsight Spark clusters using the HDInsight Tools in Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="17596-201">Access and manage HDInsight Spark clusters using the HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="17596-202">You can perform a variety of operations using the HDInsight tools.</span><span class="sxs-lookup"><span data-stu-id="17596-202">You can perform a variety of operations using the HDInsight tools.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="17596-203">Access the storage container for the cluster</span><span class="sxs-lookup"><span data-stu-id="17596-203">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="17596-204">From the Azure Explorer, expand **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span><span class="sxs-lookup"><span data-stu-id="17596-204">From the Azure Explorer, expand **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="17596-205">Expand the cluster name to see the storage account and the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-205">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="17596-207">Click the storage container name associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-207">Click the storage container name associated with the cluster.</span></span> <span data-ttu-id="17596-208">In the right-pane, you should see a folder called **HVACOut**.</span><span class="sxs-lookup"><span data-stu-id="17596-208">In the right-pane, you should see a folder called **HVACOut**.</span></span> <span data-ttu-id="17596-209">Double-click to open the folder and you will see **part-**\* files.</span><span class="sxs-lookup"><span data-stu-id="17596-209">Double-click to open the folder and you will see **part-**\* files.</span></span> <span data-ttu-id="17596-210">Open one of those files to see the output of the application.</span><span class="sxs-lookup"><span data-stu-id="17596-210">Open one of those files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="17596-211">Access the Spark History Server</span><span class="sxs-lookup"><span data-stu-id="17596-211">Access the Spark History Server</span></span>
1. <span data-ttu-id="17596-212">From the **Azure Explorer**, right-click your Spark cluster name and then select **Open Spark History UI**.</span><span class="sxs-lookup"><span data-stu-id="17596-212">From the **Azure Explorer**, right-click your Spark cluster name and then select **Open Spark History UI**.</span></span> <span data-ttu-id="17596-213">When prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-213">When prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="17596-214">You must have specified these while provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-214">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="17596-215">In the Spark History Server dashboard, you can look for the application you just finished running by using the application name.</span><span class="sxs-lookup"><span data-stu-id="17596-215">In the Spark History Server dashboard, you can look for the application you just finished running by using the application name.</span></span> <span data-ttu-id="17596-216">In the code above, you set the application name using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="17596-216">In the code above, you set the application name using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="17596-217">Hence, your Spark application name was **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="17596-217">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="launch-the-ambari-portal"></a><span data-ttu-id="17596-218">Launch the Ambari portal</span><span class="sxs-lookup"><span data-stu-id="17596-218">Launch the Ambari portal</span></span>
<span data-ttu-id="17596-219">From the **Azure Explorer**, right-click your Spark cluster name and then select **Open Cluster Management Portal (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="17596-219">From the **Azure Explorer**, right-click your Spark cluster name and then select **Open Cluster Management Portal (Ambari)**.</span></span> <span data-ttu-id="17596-220">When prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-220">When prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="17596-221">You must have specified these while provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-221">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="17596-222">Manage Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="17596-222">Manage Azure subscriptions</span></span>
<span data-ttu-id="17596-223">By default, the HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="17596-223">By default, the HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="17596-224">If required, you can specify the subscriptions for which you want to access the cluster.</span><span class="sxs-lookup"><span data-stu-id="17596-224">If required, you can specify the subscriptions for which you want to access the cluster.</span></span> <span data-ttu-id="17596-225">From the **Azure Explorer**, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="17596-225">From the **Azure Explorer**, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> <span data-ttu-id="17596-226">From the dialog box, clear the check boxes against the subscription that you do not want to access and then click **Close**.</span><span class="sxs-lookup"><span data-stu-id="17596-226">From the dialog box, clear the check boxes against the subscription that you do not want to access and then click **Close**.</span></span> <span data-ttu-id="17596-227">You can also click **Sign Out** if you want to log off from your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="17596-227">You can also click **Sign Out** if you want to log off from your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="17596-228">Run a Spark Scala application locally</span><span class="sxs-lookup"><span data-stu-id="17596-228">Run a Spark Scala application locally</span></span>
<span data-ttu-id="17596-229">You can use the HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span><span class="sxs-lookup"><span data-stu-id="17596-229">You can use the HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="17596-230">Typically, such applications do not need access to cluster resources such as storage container and can be run and tested locally.</span><span class="sxs-lookup"><span data-stu-id="17596-230">Typically, such applications do not need access to cluster resources such as storage container and can be run and tested locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="17596-231">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="17596-231">Prerequisite</span></span>
<span data-ttu-id="17596-232">While running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing **WinUtils.exe** on Windows OS.</span><span class="sxs-lookup"><span data-stu-id="17596-232">While running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing **WinUtils.exe** on Windows OS.</span></span> <span data-ttu-id="17596-233">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="17596-233">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="17596-234">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="17596-234">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="17596-235">Run a local Spark Scala application</span><span class="sxs-lookup"><span data-stu-id="17596-235">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="17596-236">Launch Eclipse and create a new project.</span><span class="sxs-lookup"><span data-stu-id="17596-236">Launch Eclipse and create a new project.</span></span> <span data-ttu-id="17596-237">In the new project dialog box, make the following choices, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17596-237">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Create Spark Scala application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
   
   * <span data-ttu-id="17596-239">From the left pane, select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="17596-239">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="17596-240">From the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="17596-240">From the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>
   * <span data-ttu-id="17596-241">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17596-241">Click **Next**.</span></span>
2. <span data-ttu-id="17596-242">To provide the project details, follow steps 3 through 6 as shown in the earlier section [Set up a Spark Scala application project for an HDInsight Spark cluster](#set-up-a-spark-scala-application-project-for-an-hdinsight-spark cluster).</span><span class="sxs-lookup"><span data-stu-id="17596-242">To provide the project details, follow steps 3 through 6 as shown in the earlier section [Set up a Spark Scala application project for an HDInsight Spark cluster](#set-up-a-spark-scala-application-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="17596-243">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="17596-243">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Spark Application local run result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="17596-245">Right click on the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span><span class="sxs-lookup"><span data-stu-id="17596-245">Right click on the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="17596-246">You will see an output like this in the **Console** tab at the bottom.</span><span class="sxs-lookup"><span data-stu-id="17596-246">You will see an output like this in the **Console** tab at the bottom.</span></span>
   
   ![Spark Application local run result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="feedback--known-issues"></a><span data-ttu-id="17596-248">Feedback & Known issues</span><span class="sxs-lookup"><span data-stu-id="17596-248">Feedback & Known issues</span></span>
<span data-ttu-id="17596-249">Currently viewing Spark outputs directly is not supported and we are working on that.</span><span class="sxs-lookup"><span data-stu-id="17596-249">Currently viewing Spark outputs directly is not supported and we are working on that.</span></span>

<span data-ttu-id="17596-250">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to drop us an email at hdivstool at microsoft dot com.</span><span class="sxs-lookup"><span data-stu-id="17596-250">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to drop us an email at hdivstool at microsoft dot com.</span></span>

## <a name="seealso"></a><span data-ttu-id="17596-251">See also</span><span class="sxs-lookup"><span data-stu-id="17596-251">See also</span></span>
* [<span data-ttu-id="17596-252">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="17596-252">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="17596-253">Scenarios</span><span class="sxs-lookup"><span data-stu-id="17596-253">Scenarios</span></span>
* [<span data-ttu-id="17596-254">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="17596-254">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="17596-255">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="17596-255">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="17596-256">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="17596-256">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="17596-257">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="17596-257">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="17596-258">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17596-258">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="17596-259">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="17596-259">Create and run applications</span></span>
* [<span data-ttu-id="17596-260">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="17596-260">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="17596-261">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="17596-261">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="17596-262">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="17596-262">Tools and extensions</span></span>
* [<span data-ttu-id="17596-263">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="17596-263">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="17596-264">Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="17596-264">Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="17596-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17596-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="17596-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="17596-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="17596-267">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="17596-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="17596-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="17596-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="17596-269">Manage resources</span><span class="sxs-lookup"><span data-stu-id="17596-269">Manage resources</span></span>
* [<span data-ttu-id="17596-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="17596-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="17596-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="17596-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)























