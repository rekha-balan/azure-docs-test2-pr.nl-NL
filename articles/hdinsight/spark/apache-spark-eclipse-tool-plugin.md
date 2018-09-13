---
title: 'Azure Toolkit for Eclipse: Create Scala applications for HDInsight Spark '
description: Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an HDInsight Spark cluster, directly from the Eclipse IDE.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/30/2017
ms.author: jasonh
ms.openlocfilehash: 836bdccbf3f8887a47da38b47b414722c878be04
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857933"
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="323c8-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="323c8-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="323c8-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span></span> <span data-ttu-id="323c8-105">You can use the HDInsight Tools plug-in in a few different ways:</span><span class="sxs-lookup"><span data-stu-id="323c8-105">You can use the HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="323c8-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="323c8-107">To access your Azure HDInsight Spark cluster resources</span><span class="sxs-lookup"><span data-stu-id="323c8-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="323c8-108">To develop and run a Scala Spark application locally</span><span class="sxs-lookup"><span data-stu-id="323c8-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="323c8-109">You can use this tool to create and submit applications only for an HDInsight Spark cluster on Linux.</span><span class="sxs-lookup"><span data-stu-id="323c8-109">You can use this tool to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="323c8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="323c8-110">Prerequisites</span></span>

* <span data-ttu-id="323c8-111">Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="323c8-111">Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="323c8-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="323c8-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="323c8-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span><span class="sxs-lookup"><span data-stu-id="323c8-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span></span> <span data-ttu-id="323c8-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="323c8-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="323c8-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="323c8-115">Eclipse IDE.</span></span> <span data-ttu-id="323c8-116">This article uses Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="323c8-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="323c8-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="323c8-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span></span>



## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-the-scala-plug-in"></a><span data-ttu-id="323c8-118">Install HDInsight Tools in Azure Toolkit for Eclipse and the Scala plug-in</span><span class="sxs-lookup"><span data-stu-id="323c8-118">Install HDInsight Tools in Azure Toolkit for Eclipse and the Scala plug-in</span></span>

### <a name="install-azure-toolkit-for-eclipse"></a><span data-ttu-id="323c8-119">Install Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="323c8-119">Install Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="323c8-120">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="323c8-120">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="323c8-121">For installation instructions, see [Installing Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="323c8-121">For installation instructions, see [Installing Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-installation).</span></span>

### <a name="install-the-scala-plug-in"></a><span data-ttu-id="323c8-122">Install the Scala plug-in</span><span class="sxs-lookup"><span data-stu-id="323c8-122">Install the Scala plug-in</span></span>
<span data-ttu-id="323c8-123">When you open Eclipse, HDInsight Tool automatically detects whether you installed the Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="323c8-123">When you open Eclipse, HDInsight Tool automatically detects whether you installed the Scala plug-in.</span></span> <span data-ttu-id="323c8-124">Select **OK** to continue, and then follow the instructions to install the plug-in from the Eclipse Marketplace.</span><span class="sxs-lookup"><span data-stu-id="323c8-124">Select **OK** to continue, and then follow the instructions to install the plug-in from the Eclipse Marketplace.</span></span>

![Automatic installation of the Scala plug-in](./media/apache-spark-eclipse-tool-plugin/auto-install-scala.png)

<span data-ttu-id="323c8-126">User can either [sign in to Azure subscription](#Sign-in-to-your-Azure-subscription), or [link a HDInsight cluster](#Link-a-cluster) using Ambari username/password or domain joined credential to start.</span><span class="sxs-lookup"><span data-stu-id="323c8-126">User can either [sign in to Azure subscription](#Sign-in-to-your-Azure-subscription), or [link a HDInsight cluster](#Link-a-cluster) using Ambari username/password or domain joined credential to start.</span></span> 

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="323c8-127">Sign in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="323c8-127">Sign in to your Azure subscription</span></span>
1. <span data-ttu-id="323c8-128">Start the Eclipse IDE and open Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="323c8-128">Start the Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="323c8-129">On the **Window** menu, select **Show View**, and then select **Other**.</span><span class="sxs-lookup"><span data-stu-id="323c8-129">On the **Window** menu, select **Show View**, and then select **Other**.</span></span> <span data-ttu-id="323c8-130">In the dialog box that opens, expand **Azure**, select **Azure Explorer**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="323c8-130">In the dialog box that opens, expand **Azure**, select **Azure Explorer**, and then select **OK**.</span></span>

   ![Show View dialog box](./media/apache-spark-eclipse-tool-plugin/view-explorer-1.png)
1. <span data-ttu-id="323c8-132">Right-click the **Azure** node, and then select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="323c8-132">Right-click the **Azure** node, and then select **Sign in**.</span></span>
1. <span data-ttu-id="323c8-133">In the **Azure Sign In** dialog box, choose the authentication method, select **Sign in**, and enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="323c8-133">In the **Azure Sign In** dialog box, choose the authentication method, select **Sign in**, and enter your Azure credentials.</span></span>
   
   ![Azure Sign In dialog box](./media/apache-spark-eclipse-tool-plugin/view-explorer-2.png)
1. <span data-ttu-id="323c8-135">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span><span class="sxs-lookup"><span data-stu-id="323c8-135">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="323c8-136">Click **Select** to close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="323c8-136">Click **Select** to close the dialog box.</span></span>

   ![Select Subscriptions dialog box](./media/apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
1. <span data-ttu-id="323c8-138">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span><span class="sxs-lookup"><span data-stu-id="323c8-138">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
   ![HDInsight Spark clusters in Azure Explorer](./media/apache-spark-eclipse-tool-plugin/view-explorer-3.png)
1. <span data-ttu-id="323c8-140">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-140">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span></span>
   
   ![Expanding a cluster name to see resources](./media/apache-spark-eclipse-tool-plugin/view-explorer-4.png)

## <a name="link-a-cluster"></a><span data-ttu-id="323c8-142">Link a cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-142">Link a cluster</span></span>
<span data-ttu-id="323c8-143">You can link a normal cluster by using the Ambari managed username.</span><span class="sxs-lookup"><span data-stu-id="323c8-143">You can link a normal cluster by using the Ambari managed username.</span></span> <span data-ttu-id="323c8-144">Similarly, for a domain-joined HDInsight cluster, you can link by using the domain and username, such as user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="323c8-144">Similarly, for a domain-joined HDInsight cluster, you can link by using the domain and username, such as user1@contoso.com.</span></span>

1. <span data-ttu-id="323c8-145">Select **Link a cluster** from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="323c8-145">Select **Link a cluster** from **Azure Explorer**.</span></span>

   ![link cluster context menu](./media/apache-spark-intellij-tool-plugin/link-a-cluster-context-menu.png)

1. <span data-ttu-id="323c8-147">Enter **Cluster Name**, **User Name** and **Password**, then click OK button to link cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-147">Enter **Cluster Name**, **User Name** and **Password**, then click OK button to link cluster.</span></span> <span data-ttu-id="323c8-148">Optionally, enter Storage Account, Storage Key and then select Storage Container for storage explorer to work in the left tree view</span><span class="sxs-lookup"><span data-stu-id="323c8-148">Optionally, enter Storage Account, Storage Key and then select Storage Container for storage explorer to work in the left tree view</span></span>
   
   ![link cluster dialog](./media/apache-spark-eclipse-tool-plugin/link-cluster-dialog.png)
   
   > [!NOTE]
   > <span data-ttu-id="323c8-150">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-150">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span></span>
   > <span data-ttu-id="323c8-151">![storage explorer in Eclipse](./media/apache-spark-eclipse-tool-plugin/storage-explorer-in-Eclipse.png)</span><span class="sxs-lookup"><span data-stu-id="323c8-151">![storage explorer in Eclipse](./media/apache-spark-eclipse-tool-plugin/storage-explorer-in-Eclipse.png)</span></span>

1. <span data-ttu-id="323c8-152">You can see a Linked cluster in **HDInsight** node after clicking OK button, if the input information are right.</span><span class="sxs-lookup"><span data-stu-id="323c8-152">You can see a Linked cluster in **HDInsight** node after clicking OK button, if the input information are right.</span></span> <span data-ttu-id="323c8-153">Now you can submit an application to this linked cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-153">Now you can submit an application to this linked cluster.</span></span>

   ![linked cluster](./media/apache-spark-intellij-tool-plugin/linked-cluster.png)

1. <span data-ttu-id="323c8-155">You also can unlink a cluster from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="323c8-155">You also can unlink a cluster from **Azure Explorer**.</span></span>
   
   ![unlinked cluster](./media/apache-spark-intellij-tool-plugin/unlink.png)


## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="323c8-157">Set up a Spark Scala project for an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-157">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="323c8-158">In the Eclipse IDE workspace, select **File**, select **New**, and then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="323c8-158">In the Eclipse IDE workspace, select **File**, select **New**, and then select **Project**.</span></span> 
1. <span data-ttu-id="323c8-159">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="323c8-159">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then select **Next**.</span></span>

   ![Selecting the Spark on HDInsight (Scala) project](./media/apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
1. <span data-ttu-id="323c8-161">The Scala project creation wizard automatically detects whether you installed the Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="323c8-161">The Scala project creation wizard automatically detects whether you installed the Scala plug-in.</span></span> <span data-ttu-id="323c8-162">Select **OK** to continue downloading the Scala plug-in, and then follow the instructions to restart Eclipse.</span><span class="sxs-lookup"><span data-stu-id="323c8-162">Select **OK** to continue downloading the Scala plug-in, and then follow the instructions to restart Eclipse.</span></span>

   ![Scala check](./media/apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
1. <span data-ttu-id="323c8-164">In the **New HDInsight Scala Project** dialog box, provide the following values, and then select **Next**:</span><span class="sxs-lookup"><span data-stu-id="323c8-164">In the **New HDInsight Scala Project** dialog box, provide the following values, and then select **Next**:</span></span>
   * <span data-ttu-id="323c8-165">Enter a name for the project.</span><span class="sxs-lookup"><span data-stu-id="323c8-165">Enter a name for the project.</span></span>
   * <span data-ttu-id="323c8-166">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span><span class="sxs-lookup"><span data-stu-id="323c8-166">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="323c8-167">In the **Spark Library** area, you can choose **Use Maven to configure Spark SDK** option.</span><span class="sxs-lookup"><span data-stu-id="323c8-167">In the **Spark Library** area, you can choose **Use Maven to configure Spark SDK** option.</span></span>  <span data-ttu-id="323c8-168">Our tool integrates the proper version for Spark SDK and Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="323c8-168">Our tool integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="323c8-169">You can also choose **Add Spark SDK manually** option, download and add Spark SDK by manually.</span><span class="sxs-lookup"><span data-stu-id="323c8-169">You can also choose **Add Spark SDK manually** option, download and add Spark SDK by manually.</span></span>

   ![New HDInsight Scala Project dialog box](./media/apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
1. <span data-ttu-id="323c8-171">In the next dialog box, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="323c8-171">In the next dialog box, select **Finish**.</span></span> 
   
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="323c8-172">Create a Scala application for an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-172">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="323c8-173">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then select **Other**.</span><span class="sxs-lookup"><span data-stu-id="323c8-173">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then select **Other**.</span></span>
1. <span data-ttu-id="323c8-174">In the **Select a wizard** dialog box, expand **Scala Wizards**, select **Scala Object**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="323c8-174">In the **Select a wizard** dialog box, expand **Scala Wizards**, select **Scala Object**, and then select **Next**.</span></span>
   
   ![Select a wizard dialog box](./media/apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
1. <span data-ttu-id="323c8-176">In the **Create New File** dialog box, enter a name for the object, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="323c8-176">In the **Create New File** dialog box, enter a name for the object, and then select **Finish**.</span></span>
   
   ![Create New File dialog box](./media/apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
1. <span data-ttu-id="323c8-178">Paste the following code in the text editor:</span><span class="sxs-lookup"><span data-stu-id="323c8-178">Paste the following code in the text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
1. <span data-ttu-id="323c8-179">Run the application on an HDInsight Spark cluster:</span><span class="sxs-lookup"><span data-stu-id="323c8-179">Run the application on an HDInsight Spark cluster:</span></span>
   
   <span data-ttu-id="323c8-180">a.</span><span class="sxs-lookup"><span data-stu-id="323c8-180">a.</span></span> <span data-ttu-id="323c8-181">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="323c8-181">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   <span data-ttu-id="323c8-182">b.</span><span class="sxs-lookup"><span data-stu-id="323c8-182">b.</span></span> <span data-ttu-id="323c8-183">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**:</span><span class="sxs-lookup"><span data-stu-id="323c8-183">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**:</span></span>
      
      * <span data-ttu-id="323c8-184">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span><span class="sxs-lookup"><span data-stu-id="323c8-184">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="323c8-185">Select an artifact from the Eclipse project, or select one from a hard drive.</span><span class="sxs-lookup"><span data-stu-id="323c8-185">Select an artifact from the Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="323c8-186">The default value depends on the item that you right-click from Package Explorer.</span><span class="sxs-lookup"><span data-stu-id="323c8-186">The default value depends on the item that you right-click from Package Explorer.</span></span>
      * <span data-ttu-id="323c8-187">In the **Main class name** drop-down list, the submission wizard displays all object names from your project.</span><span class="sxs-lookup"><span data-stu-id="323c8-187">In the **Main class name** drop-down list, the submission wizard displays all object names from your project.</span></span> <span data-ttu-id="323c8-188">Select or enter one that you want to run.</span><span class="sxs-lookup"><span data-stu-id="323c8-188">Select or enter one that you want to run.</span></span> <span data-ttu-id="323c8-189">If you selected an artifact from a hard drive, you must enter the main class name manually.</span><span class="sxs-lookup"><span data-stu-id="323c8-189">If you selected an artifact from a hard drive, you must enter the main class name manually.</span></span> 
      * <span data-ttu-id="323c8-190">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span><span class="sxs-lookup"><span data-stu-id="323c8-190">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
        
      ![Spark Submission dialog box](./media/apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
1. <span data-ttu-id="323c8-192">The **Spark Submission** tab should start displaying the progress.</span><span class="sxs-lookup"><span data-stu-id="323c8-192">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="323c8-193">You can stop the application by selecting the red button in the **Spark Submission** window.</span><span class="sxs-lookup"><span data-stu-id="323c8-193">You can stop the application by selecting the red button in the **Spark Submission** window.</span></span> <span data-ttu-id="323c8-194">You can also view the logs for this specific application run by selecting the globe icon (denoted by the blue box in the image).</span><span class="sxs-lookup"><span data-stu-id="323c8-194">You can also view the logs for this specific application run by selecting the globe icon (denoted by the blue box in the image).</span></span>
      
   ![Spark Submission window](./media/apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)


## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="323c8-196">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="323c8-196">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="323c8-197">You can perform various operations by using HDInsight Tools, including accessing the job output.</span><span class="sxs-lookup"><span data-stu-id="323c8-197">You can perform various operations by using HDInsight Tools, including accessing the job output.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="323c8-198">Access the job view</span><span class="sxs-lookup"><span data-stu-id="323c8-198">Access the job view</span></span>
1. <span data-ttu-id="323c8-199">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="323c8-199">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span> 

   ![Job view node](./media/apache-spark-eclipse-tool-plugin/job-view-node.png)

1. <span data-ttu-id="323c8-201">Select the **Jobs** node.</span><span class="sxs-lookup"><span data-stu-id="323c8-201">Select the **Jobs** node.</span></span> <span data-ttu-id="323c8-202">If Java version is lower than **1.8**, HDInsight Tools automatically reminder you install the **E(fx)clipse** plug-in.</span><span class="sxs-lookup"><span data-stu-id="323c8-202">If Java version is lower than **1.8**, HDInsight Tools automatically reminder you install the **E(fx)clipse** plug-in.</span></span> <span data-ttu-id="323c8-203">Select **OK** to continue, and then follow the wizard to install it from the Eclipse Marketplace and restart Eclipse.</span><span class="sxs-lookup"><span data-stu-id="323c8-203">Select **OK** to continue, and then follow the wizard to install it from the Eclipse Marketplace and restart Eclipse.</span></span> 

   ![Install E(fx)clipse](./media/apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

1. <span data-ttu-id="323c8-205">Open the Job View from the **Jobs** node.</span><span class="sxs-lookup"><span data-stu-id="323c8-205">Open the Job View from the **Jobs** node.</span></span> <span data-ttu-id="323c8-206">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-206">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="323c8-207">Select the name of the application for which you want to see more details.</span><span class="sxs-lookup"><span data-stu-id="323c8-207">Select the name of the application for which you want to see more details.</span></span>

   ![Application details](./media/apache-spark-eclipse-tool-plugin/view-job-logs.png)

   <span data-ttu-id="323c8-209">You can then take any of these actions:</span><span class="sxs-lookup"><span data-stu-id="323c8-209">You can then take any of these actions:</span></span>

   * <span data-ttu-id="323c8-210">Hover on the job graph.</span><span class="sxs-lookup"><span data-stu-id="323c8-210">Hover on the job graph.</span></span> <span data-ttu-id="323c8-211">It displays basic info about the running job.</span><span class="sxs-lookup"><span data-stu-id="323c8-211">It displays basic info about the running job.</span></span> <span data-ttu-id="323c8-212">Select the job graph, and you can see the stages and info that every job generates.</span><span class="sxs-lookup"><span data-stu-id="323c8-212">Select the job graph, and you can see the stages and info that every job generates.</span></span>

     ![Job stage details](./media/apache-spark-eclipse-tool-plugin/Job-graph-stage-info.png)

   * <span data-ttu-id="323c8-214">Select the **Log** tab to view frequently used logs, including **Driver Stderr**, **Driver Stdout**, and **Directory Info**.</span><span class="sxs-lookup"><span data-stu-id="323c8-214">Select the **Log** tab to view frequently used logs, including **Driver Stderr**, **Driver Stdout**, and **Directory Info**.</span></span>

     ![Log details](./media/apache-spark-eclipse-tool-plugin/Job-log-info.png)

   * <span data-ttu-id="323c8-216">Open the Spark history UI and the YARN UI (at the application level) by selecting the hyperlinks at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="323c8-216">Open the Spark history UI and the YARN UI (at the application level) by selecting the hyperlinks at the top of the window.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="323c8-217">Access the storage container for the cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-217">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="323c8-218">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span><span class="sxs-lookup"><span data-stu-id="323c8-218">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
1. <span data-ttu-id="323c8-219">Expand the cluster name to see the storage account and the default storage container for the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-219">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
   ![Storage account and default storage container](./media/apache-spark-eclipse-tool-plugin/view-explorer-5.png)
1. <span data-ttu-id="323c8-221">Select the storage container name associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-221">Select the storage container name associated with the cluster.</span></span> <span data-ttu-id="323c8-222">In the right pane, double-click the **HVACOut** folder.</span><span class="sxs-lookup"><span data-stu-id="323c8-222">In the right pane, double-click the **HVACOut** folder.</span></span> <span data-ttu-id="323c8-223">Open one of the **part-** files to see the output of the application.</span><span class="sxs-lookup"><span data-stu-id="323c8-223">Open one of the **part-** files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="323c8-224">Access the Spark history server</span><span class="sxs-lookup"><span data-stu-id="323c8-224">Access the Spark history server</span></span>
1. <span data-ttu-id="323c8-225">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span><span class="sxs-lookup"><span data-stu-id="323c8-225">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="323c8-226">When you're prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-226">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="323c8-227">You specified these while provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-227">You specified these while provisioning the cluster.</span></span>
1. <span data-ttu-id="323c8-228">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span><span class="sxs-lookup"><span data-stu-id="323c8-228">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="323c8-229">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="323c8-229">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="323c8-230">So, your Spark application name was **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="323c8-230">So, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="323c8-231">Start the Ambari portal</span><span class="sxs-lookup"><span data-stu-id="323c8-231">Start the Ambari portal</span></span>
1. <span data-ttu-id="323c8-232">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="323c8-232">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
1. <span data-ttu-id="323c8-233">When you're prompted, enter the admin credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-233">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="323c8-234">You specified these while provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-234">You specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="323c8-235">Manage Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="323c8-235">Manage Azure subscriptions</span></span>
<span data-ttu-id="323c8-236">By default, HDInsight Tool in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="323c8-236">By default, HDInsight Tool in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="323c8-237">If necessary, you can specify the subscriptions for which you want to access the cluster.</span><span class="sxs-lookup"><span data-stu-id="323c8-237">If necessary, you can specify the subscriptions for which you want to access the cluster.</span></span> 

1. <span data-ttu-id="323c8-238">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="323c8-238">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 
1. <span data-ttu-id="323c8-239">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="323c8-239">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="323c8-240">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="323c8-240">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="323c8-241">Run a Spark Scala application locally</span><span class="sxs-lookup"><span data-stu-id="323c8-241">Run a Spark Scala application locally</span></span>
<span data-ttu-id="323c8-242">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span><span class="sxs-lookup"><span data-stu-id="323c8-242">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="323c8-243">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span><span class="sxs-lookup"><span data-stu-id="323c8-243">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="323c8-244">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="323c8-244">Prerequisite</span></span>
<span data-ttu-id="323c8-245">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="323c8-245">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="323c8-246">This exception occurs because **WinUtils.exe** is missing in Windows.</span><span class="sxs-lookup"><span data-stu-id="323c8-246">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="323c8-247">To resolve this error, you need [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**, and then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="323c8-247">To resolve this error, you need [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**, and then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="323c8-248">Run a local Spark Scala application</span><span class="sxs-lookup"><span data-stu-id="323c8-248">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="323c8-249">Start Eclipse and create a project.</span><span class="sxs-lookup"><span data-stu-id="323c8-249">Start Eclipse and create a project.</span></span> <span data-ttu-id="323c8-250">In the **New Project** dialog box, make the following choices, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="323c8-250">In the **New Project** dialog box, make the following choices, and then select **Next**.</span></span>
   
   * <span data-ttu-id="323c8-251">In the left pane, select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="323c8-251">In the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="323c8-252">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="323c8-252">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

   ![New Project dialog box](./media/apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
   
1. <span data-ttu-id="323c8-254">To provide the project details, follow steps 3 through 6 from the earlier section [Setup a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster).</span><span class="sxs-lookup"><span data-stu-id="323c8-254">To provide the project details, follow steps 3 through 6 from the earlier section [Setup a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster).</span></span>

1. <span data-ttu-id="323c8-255">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="323c8-255">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
   ![Location of LogQuery](./media/apache-spark-eclipse-tool-plugin/local-app.png)
   
1. <span data-ttu-id="323c8-257">Right-click the **LogQuery** application, point to **Run As**, and then select **1 Scala Application**.</span><span class="sxs-lookup"><span data-stu-id="323c8-257">Right-click the **LogQuery** application, point to **Run As**, and then select **1 Scala Application**.</span></span> <span data-ttu-id="323c8-258">Output like this appears on the **Console** tab:</span><span class="sxs-lookup"><span data-stu-id="323c8-258">Output like this appears on the **Console** tab:</span></span>
   
   ![Spark application local run result](./media/apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="known-problems"></a><span data-ttu-id="323c8-260">Known problems</span><span class="sxs-lookup"><span data-stu-id="323c8-260">Known problems</span></span>
<span data-ttu-id="323c8-261">When link a cluster, I would suggest you to provide credential of storage.</span><span class="sxs-lookup"><span data-stu-id="323c8-261">When link a cluster, I would suggest you to provide credential of storage.</span></span>

![Interactive sign-in](./media/apache-spark-eclipse-tool-plugin/link-cluster-with-storage-credential-eclipse.png)

<span data-ttu-id="323c8-263">There are two modes to submit the jobs.</span><span class="sxs-lookup"><span data-stu-id="323c8-263">There are two modes to submit the jobs.</span></span> <span data-ttu-id="323c8-264">If storage credential is provided, batch mode will be used to submit the job.</span><span class="sxs-lookup"><span data-stu-id="323c8-264">If storage credential is provided, batch mode will be used to submit the job.</span></span> <span data-ttu-id="323c8-265">Otherwise, interactive mode will be used.</span><span class="sxs-lookup"><span data-stu-id="323c8-265">Otherwise, interactive mode will be used.</span></span> <span data-ttu-id="323c8-266">If the cluster is busy, you might get the error below.</span><span class="sxs-lookup"><span data-stu-id="323c8-266">If the cluster is busy, you might get the error below.</span></span>

![eclipse get error when cluster busy](./media/apache-spark-eclipse-tool-plugin/eclipse-interactive-cluster-busy-upload.png)

![eclipse get error when cluster busy](./media/apache-spark-eclipse-tool-plugin/eclipse-interactive-cluster-busy-submit.png)

## <a name="feedback"></a><span data-ttu-id="323c8-269">Feedback</span><span class="sxs-lookup"><span data-stu-id="323c8-269">Feedback</span></span>
<span data-ttu-id="323c8-270">If you have any feedback, or if you encounter any other problems when using this tool, send us an email at hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="323c8-270">If you have any feedback, or if you encounter any other problems when using this tool, send us an email at hdivstool@microsoft.com.</span></span>

## <a name="seealso"></a><span data-ttu-id="323c8-271">See also</span><span class="sxs-lookup"><span data-stu-id="323c8-271">See also</span></span>
* [<span data-ttu-id="323c8-272">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="323c8-272">Overview: Apache Spark on Azure HDInsight</span></span>](apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="323c8-273">Scenarios</span><span class="sxs-lookup"><span data-stu-id="323c8-273">Scenarios</span></span>
* [<span data-ttu-id="323c8-274">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="323c8-274">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](apache-spark-use-bi-tools.md)
* [<span data-ttu-id="323c8-275">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="323c8-275">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="323c8-276">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="323c8-276">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="323c8-277">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="323c8-277">Website log analysis using Spark in HDInsight</span></span>](apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="323c8-278">Creating and running applications</span><span class="sxs-lookup"><span data-stu-id="323c8-278">Creating and running applications</span></span>
* [<span data-ttu-id="323c8-279">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="323c8-279">Create a standalone application using Scala</span></span>](apache-spark-create-standalone-application.md)
* [<span data-ttu-id="323c8-280">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="323c8-280">Run jobs remotely on a Spark cluster using Livy</span></span>](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="323c8-281">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="323c8-281">Tools and extensions</span></span>
* [<span data-ttu-id="323c8-282">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="323c8-282">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="323c8-283">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span><span class="sxs-lookup"><span data-stu-id="323c8-283">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](../hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="323c8-284">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span><span class="sxs-lookup"><span data-stu-id="323c8-284">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](../hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="323c8-285">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="323c8-285">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](../hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="323c8-286">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="323c8-286">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="323c8-287">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="323c8-287">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="323c8-288">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="323c8-288">Use external packages with Jupyter notebooks</span></span>](apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="323c8-289">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="323c8-289">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="323c8-290">Managing resources</span><span class="sxs-lookup"><span data-stu-id="323c8-290">Managing resources</span></span>
* [<span data-ttu-id="323c8-291">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="323c8-291">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="323c8-292">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="323c8-292">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)

