---
title: 'Azure Toolkit for IntelliJ: Create Spark applications for an HDInsight cluster '
description: Use the Azure Toolkit for IntelliJ to develop Spark applications written in Scala, and submit them to an HDInsight Spark cluster.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/25/2017
ms.author: maxluk
ms.openlocfilehash: ed0118584d51f08d64a88dc1e7e6e2ba5f95cb0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870986"
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="5dfb9-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="5dfb9-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="5dfb9-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="5dfb9-105">You can use the plug-in in a few ways:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="5dfb9-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="5dfb9-107">Access your Azure HDInsight Spark cluster resources.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="5dfb9-108">Develop and run a Scala Spark application locally.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="5dfb9-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dfb9-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="5dfb9-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5dfb9-111">Prerequisites</span></span>

- <span data-ttu-id="5dfb9-112">An Apache Spark cluster on HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="5dfb9-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="5dfb9-114">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="5dfb9-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="5dfb9-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-116">IntelliJ IDEA.</span></span> <span data-ttu-id="5dfb9-117">This article uses version 2017.1.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-117">This article uses version 2017.1.</span></span> <span data-ttu-id="5dfb9-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="5dfb9-119">Install Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5dfb9-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="5dfb9-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).</span></span>

## <a name="get-started"></a><span data-ttu-id="5dfb9-121">Get Started</span><span class="sxs-lookup"><span data-stu-id="5dfb9-121">Get Started</span></span>
<span data-ttu-id="5dfb9-122">User can either [sign in to Azure subscription](#sign-in-to-your-azure-subscription), or [link a HDInsight cluster](#link-a-cluster) using Ambari username/password or domain joined credential to start.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-122">User can either [sign in to Azure subscription](#sign-in-to-your-azure-subscription), or [link a HDInsight cluster](#link-a-cluster) using Ambari username/password or domain joined credential to start.</span></span>


## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="5dfb9-123">Sign in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5dfb9-123">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="5dfb9-124">Start the IntelliJ IDE, and open Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-124">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="5dfb9-125">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-125">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![The Azure Explorer link](./media/apache-spark-intellij-tool-plugin/show-azure-explorer.png)

1. <span data-ttu-id="5dfb9-127">Right-click the **Azure** node, and then select **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-127">Right-click the **Azure** node, and then select **Sign In**.</span></span>

1. <span data-ttu-id="5dfb9-128">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-128">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![The Azure Sign In dialog box](./media/apache-spark-intellij-tool-plugin/view-explorer-2.png)

1. <span data-ttu-id="5dfb9-130">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-130">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="5dfb9-131">Select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-131">Select the **Select** button.</span></span>

    ![The Select Subscriptions dialog box](./media/apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

1. <span data-ttu-id="5dfb9-133">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-133">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![HDInsight Spark clusters in Azure Explorer](./media/apache-spark-intellij-tool-plugin/view-explorer-3.png)

1. <span data-ttu-id="5dfb9-135">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-135">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![An expanded cluster-name node](./media/apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="link-a-cluster"></a><span data-ttu-id="5dfb9-137">Link a cluster</span><span class="sxs-lookup"><span data-stu-id="5dfb9-137">Link a cluster</span></span>
<span data-ttu-id="5dfb9-138">You can link a normal HDInsight cluster by using the Ambari managed username.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-138">You can link a normal HDInsight cluster by using the Ambari managed username.</span></span> <span data-ttu-id="5dfb9-139">Similarly, for a domain-joined HDInsight cluster, you can link by using the domain and username, such as user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-139">Similarly, for a domain-joined HDInsight cluster, you can link by using the domain and username, such as user1@contoso.com.</span></span>

1. <span data-ttu-id="5dfb9-140">Select **Link a cluster** from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-140">Select **Link a cluster** from **Azure Explorer**.</span></span>

   ![link cluster context menu](./media/apache-spark-intellij-tool-plugin/link-a-cluster-context-menu.png)


1. <span data-ttu-id="5dfb9-142">Enter **Cluster Name**, **User Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-142">Enter **Cluster Name**, **User Name** and **Password**.</span></span> <span data-ttu-id="5dfb9-143">You need to check the username and password if got the authentication failure.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-143">You need to check the username and password if got the authentication failure.</span></span> <span data-ttu-id="5dfb9-144">Optionally, add Storage Account, Storage Key, then select a container from Storage Container.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-144">Optionally, add Storage Account, Storage Key, then select a container from Storage Container.</span></span> <span data-ttu-id="5dfb9-145">Storage information is for storage explorer in the left tree</span><span class="sxs-lookup"><span data-stu-id="5dfb9-145">Storage information is for storage explorer in the left tree</span></span>
   
   ![link cluster dialog](./media/apache-spark-intellij-tool-plugin/link-a-cluster-dialog.png)

   > [!NOTE]
   > <span data-ttu-id="5dfb9-147">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-147">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span></span>
   > <span data-ttu-id="5dfb9-148">![storage explorer in IntelliJ](./media/apache-spark-intellij-tool-plugin/storage-explorer-in-IntelliJ.png)</span><span class="sxs-lookup"><span data-stu-id="5dfb9-148">![storage explorer in IntelliJ](./media/apache-spark-intellij-tool-plugin/storage-explorer-in-IntelliJ.png)</span></span>

   
1. <span data-ttu-id="5dfb9-149">You can see a Linked cluster in **HDInsight** node if the input information is right.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-149">You can see a Linked cluster in **HDInsight** node if the input information is right.</span></span> <span data-ttu-id="5dfb9-150">Now you can submit an application to this linked cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-150">Now you can submit an application to this linked cluster.</span></span>

   ![linked cluster](./media/apache-spark-intellij-tool-plugin/linked-cluster.png)

1. <span data-ttu-id="5dfb9-152">You also can unlink a cluster from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-152">You also can unlink a cluster from **Azure Explorer**.</span></span>
   
   ![unlinked cluster](./media/apache-spark-intellij-tool-plugin/unlink.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="5dfb9-154">Run a Spark Scala application on an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5dfb9-154">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="5dfb9-155">Start IntelliJ IDEA, and then create a project.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-155">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="5dfb9-156">In the **New Project** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-156">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="5dfb9-157">a.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-157">a.</span></span> <span data-ttu-id="5dfb9-158">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-158">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="5dfb9-159">b.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-159">b.</span></span> <span data-ttu-id="5dfb9-160">In the **Build tool** list, select either of the following, according to your need:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-160">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="5dfb9-161">**Maven**, for Scala project-creation wizard support</span><span class="sxs-lookup"><span data-stu-id="5dfb9-161">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="5dfb9-162">**SBT**, for managing the dependencies and building for the Scala project</span><span class="sxs-lookup"><span data-stu-id="5dfb9-162">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![The New Project dialog box](./media/apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

1. <span data-ttu-id="5dfb9-164">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-164">Select **Next**.</span></span>

1. <span data-ttu-id="5dfb9-165">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-165">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="5dfb9-166">Select **Install**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-166">Select **Install**.</span></span>

   ![Scala Plugin Check](./media/apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

1. <span data-ttu-id="5dfb9-168">To download the Scala plug-in, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-168">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="5dfb9-169">Follow the instructions to restart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-169">Follow the instructions to restart IntelliJ.</span></span> 

   ![The Scala plugin installation dialog box](./media/apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

1. <span data-ttu-id="5dfb9-171">In the **New Project** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-171">In the **New Project** window, do the following:</span></span>  

    ![Selecting the Spark SDK](./media/apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="5dfb9-173">a.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-173">a.</span></span> <span data-ttu-id="5dfb9-174">Enter a project name and location.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-174">Enter a project name and location.</span></span>

   <span data-ttu-id="5dfb9-175">b.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-175">b.</span></span> <span data-ttu-id="5dfb9-176">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-176">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="5dfb9-177">c.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-177">c.</span></span> <span data-ttu-id="5dfb9-178">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-178">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="5dfb9-179">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-179">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="5dfb9-180">Otherwise, select **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-180">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="5dfb9-181">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-181">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

1. <span data-ttu-id="5dfb9-182">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-182">Select **Finish**.</span></span>

1. <span data-ttu-id="5dfb9-183">The Spark project automatically creates an artifact for you.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-183">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="5dfb9-184">To view the artifact, do the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-184">To view the artifact, do the following:</span></span>

   <span data-ttu-id="5dfb9-185">a.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-185">a.</span></span> <span data-ttu-id="5dfb9-186">On the **File** menu, select **Project Structure**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-186">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="5dfb9-187">b.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-187">b.</span></span> <span data-ttu-id="5dfb9-188">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-188">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="5dfb9-189">You can also create your own artifact by selecting the plus sign (**+**).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-189">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![Artifact info in the dialog box](./media/apache-spark-intellij-tool-plugin/default-artifact.png)
      
1. <span data-ttu-id="5dfb9-191">Add your application source code by doing the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-191">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="5dfb9-192">a.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-192">a.</span></span> <span data-ttu-id="5dfb9-193">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-193">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Commands for creating a Scala class from Project Explorer](./media/apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="5dfb9-195">b.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-195">b.</span></span> <span data-ttu-id="5dfb9-196">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-196">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Create New Scala Class dialog box](./media/apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="5dfb9-198">c.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-198">c.</span></span> <span data-ttu-id="5dfb9-199">In the **MyClusterApp.scala** file, paste the following code.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-199">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="5dfb9-200">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-200">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

1. <span data-ttu-id="5dfb9-201">Run the application on an HDInsight Spark cluster by doing the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-201">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="5dfb9-202">a.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-202">a.</span></span> <span data-ttu-id="5dfb9-203">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-203">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![The Submit Spark Application to HDInsight command](./media/apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="5dfb9-205">b.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-205">b.</span></span> <span data-ttu-id="5dfb9-206">You are prompted to enter your Azure subscription credentials.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-206">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="5dfb9-207">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-207">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="5dfb9-208">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-208">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="5dfb9-209">Select an artifact from the IntelliJ project, or select one from the hard drive.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-209">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="5dfb9-210">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-210">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![The Select Main Class dialog box](./media/apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="5dfb9-212">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-212">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="5dfb9-213">After you provide all the information, the dialog box should resemble the following image.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-213">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![The Spark Submission dialog box](./media/apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="5dfb9-215">c.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-215">c.</span></span> <span data-ttu-id="5dfb9-216">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-216">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="5dfb9-217">You can also stop the application by selecting the red button in the **Spark Submission** window.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-217">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
     ![The Spark Submission window](./media/apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="5dfb9-219">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-219">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="debug-spark-applications-locally-or-remotely-on-an-hdinsight-cluster"></a><span data-ttu-id="5dfb9-220">Debug Spark applications locally or remotely on an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="5dfb9-220">Debug Spark applications locally or remotely on an HDInsight cluster</span></span> 
<span data-ttu-id="5dfb9-221">We also recommend another way of submitting the Spark application to the cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-221">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="5dfb9-222">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-222">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="5dfb9-223">For more information, see [Debug Spark applications locally or remotely on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="5dfb9-223">For more information, see [Debug Spark applications locally or remotely on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>



## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="5dfb9-224">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5dfb9-224">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="5dfb9-225">You can perform various operations by using Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-225">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="5dfb9-226">Access the job view</span><span class="sxs-lookup"><span data-stu-id="5dfb9-226">Access the job view</span></span>
1. <span data-ttu-id="5dfb9-227">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-227">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Job view node](./media/apache-spark-intellij-tool-plugin/job-view-node.png)

1. <span data-ttu-id="5dfb9-229">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-229">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="5dfb9-230">Select the name of the application for which you want to see more details.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-230">Select the name of the application for which you want to see more details.</span></span>

    ![Application details](./media/apache-spark-intellij-tool-plugin/view-job-logs.png)
    ><span data-ttu-id="5dfb9-232">Note</span><span class="sxs-lookup"><span data-stu-id="5dfb9-232">Note</span></span>
    >

1. <span data-ttu-id="5dfb9-233">To display basic running job information, hover over the job graph.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-233">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="5dfb9-234">To view the stages graph and information that every job generates, select a node on the job graph.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-234">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Job stage details](./media/apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

1. <span data-ttu-id="5dfb9-236">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-236">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Log details](./media/apache-spark-intellij-tool-plugin/Job-log-info.png)

1. <span data-ttu-id="5dfb9-238">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-238">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="5dfb9-239">Access the Spark history server</span><span class="sxs-lookup"><span data-stu-id="5dfb9-239">Access the Spark history server</span></span>
1. <span data-ttu-id="5dfb9-240">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-240">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

1. <span data-ttu-id="5dfb9-241">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-241">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

1. <span data-ttu-id="5dfb9-242">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-242">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="5dfb9-243">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-243">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="5dfb9-244">Therefore, your Spark application name is **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-244">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="5dfb9-245">Start the Ambari portal</span><span class="sxs-lookup"><span data-stu-id="5dfb9-245">Start the Ambari portal</span></span>
1. <span data-ttu-id="5dfb9-246">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-246">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

1. <span data-ttu-id="5dfb9-247">When you're prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-247">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="5dfb9-248">You specified these credentials during the cluster setup process.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-248">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="5dfb9-249">Manage Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="5dfb9-249">Manage Azure subscriptions</span></span>
<span data-ttu-id="5dfb9-250">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-250">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="5dfb9-251">If necessary, you can specify the subscriptions that you want to access.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-251">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="5dfb9-252">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-252">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

1. <span data-ttu-id="5dfb9-253">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-253">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="5dfb9-254">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-254">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="5dfb9-255">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5dfb9-255">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="5dfb9-256">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-256">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="5dfb9-257">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-257">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="5dfb9-258">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-258">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

1. <span data-ttu-id="5dfb9-259">At the root level is a **module** element like the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-259">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="5dfb9-260">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-260">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

1. <span data-ttu-id="5dfb9-261">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-261">Save the changes.</span></span> <span data-ttu-id="5dfb9-262">Your application should now be compatible with Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-262">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="5dfb9-263">You can test it by right-clicking the project name in Project Explorer.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-263">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="5dfb9-264">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-264">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5dfb9-265">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="5dfb9-265">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="5dfb9-266">Error in local run: *Please use a larger heap size*</span><span class="sxs-lookup"><span data-stu-id="5dfb9-266">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="5dfb9-267">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-267">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="5dfb9-268">These errors happen because the heap size is not large enough for Spark to run.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-268">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="5dfb9-269">Spark requires at least 471 MB.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-269">Spark requires at least 471 MB.</span></span> <span data-ttu-id="5dfb9-270">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-270">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="5dfb9-271">You can also change the JVM settings in IntelliJ by adding the following options:</span><span class="sxs-lookup"><span data-stu-id="5dfb9-271">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Adding options to the "VM options" box in IntelliJ](./media/apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="5dfb9-273">FAQ</span><span class="sxs-lookup"><span data-stu-id="5dfb9-273">FAQ</span></span>
<span data-ttu-id="5dfb9-274">When link a cluster, I would suggest you to provide credential of storage.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-274">When link a cluster, I would suggest you to provide credential of storage.</span></span>

![Link cluster, provide storage credential](./media/apache-spark-intellij-tool-plugin/link-cluster-with-storage-credential-intellij.png)

<span data-ttu-id="5dfb9-276">There are two modes to submit the jobs.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-276">There are two modes to submit the jobs.</span></span> <span data-ttu-id="5dfb9-277">If storage credential is provided, batch mode will be used to submit the job.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-277">If storage credential is provided, batch mode will be used to submit the job.</span></span> <span data-ttu-id="5dfb9-278">Otherwise, interactive mode will be used.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-278">Otherwise, interactive mode will be used.</span></span> <span data-ttu-id="5dfb9-279">If the cluster is busy, you might get the error below.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-279">If the cluster is busy, you might get the error below.</span></span>

![Intellij get error when cluster busy](./media/apache-spark-intellij-tool-plugin/intellij-interactive-cluster-busy-upload.png)

![Intellij get error when cluster busy](./media/apache-spark-intellij-tool-plugin/intellij-interactive-cluster-busy-submit.png)

## <a name="feedback-and-known-issues"></a><span data-ttu-id="5dfb9-282">Feedback and known issues</span><span class="sxs-lookup"><span data-stu-id="5dfb9-282">Feedback and known issues</span></span>
<span data-ttu-id="5dfb9-283">Currently, viewing Spark outputs directly is not supported.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-283">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="5dfb9-284">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5dfb9-284">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <a name="seealso"></a><span data-ttu-id="5dfb9-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="5dfb9-285">Next steps</span></span>
* [<span data-ttu-id="5dfb9-286">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dfb9-286">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="5dfb9-287">Demo</span><span class="sxs-lookup"><span data-stu-id="5dfb9-287">Demo</span></span>
* <span data-ttu-id="5dfb9-288">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5dfb9-288">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="5dfb9-289">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5dfb9-289">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="5dfb9-290">Scenarios</span><span class="sxs-lookup"><span data-stu-id="5dfb9-290">Scenarios</span></span>
* [<span data-ttu-id="5dfb9-291">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="5dfb9-291">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5dfb9-292">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="5dfb9-292">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5dfb9-293">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="5dfb9-293">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5dfb9-294">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dfb9-294">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="5dfb9-295">Creating and running applications</span><span class="sxs-lookup"><span data-stu-id="5dfb9-295">Creating and running applications</span></span>
* [<span data-ttu-id="5dfb9-296">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="5dfb9-296">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5dfb9-297">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="5dfb9-297">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5dfb9-298">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="5dfb9-298">Tools and extensions</span></span>
* [<span data-ttu-id="5dfb9-299">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span><span class="sxs-lookup"><span data-stu-id="5dfb9-299">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5dfb9-300">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span><span class="sxs-lookup"><span data-stu-id="5dfb9-300">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="5dfb9-301">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="5dfb9-301">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](../hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="5dfb9-302">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span><span class="sxs-lookup"><span data-stu-id="5dfb9-302">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="5dfb9-303">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dfb9-303">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5dfb9-304">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dfb9-304">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5dfb9-305">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="5dfb9-305">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5dfb9-306">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5dfb9-306">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="5dfb9-307">Managing resources</span><span class="sxs-lookup"><span data-stu-id="5dfb9-307">Managing resources</span></span>
* [<span data-ttu-id="5dfb9-308">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dfb9-308">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="5dfb9-309">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dfb9-309">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)
