---
title: Get started with ML Services on HDInsight - Azure
description: Learn how to create an Apache Spark on HDInsight cluster that includes ML Services and submit an R script on the cluster.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/27/2018
ms.openlocfilehash: 7b3d2d47db733d1290bccca0e44958098451324e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867954"
---
# <a name="get-started-with-ml-services-on-azure-hdinsight"></a><span data-ttu-id="6dd6f-103">Get started with ML Services on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dd6f-103">Get started with ML Services on Azure HDInsight</span></span>

<span data-ttu-id="6dd6f-104">Azure HDInsight enables you to create an ML Services cluster.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-104">Azure HDInsight enables you to create an ML Services cluster.</span></span> <span data-ttu-id="6dd6f-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="6dd6f-106">In this article, you learn how to create an ML Service cluster on HDInsight and how to run an R script that demonstrates using Spark for distributed R computations.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-106">In this article, you learn how to create an ML Service cluster on HDInsight and how to run an R script that demonstrates using Spark for distributed R computations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dd6f-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6dd6f-107">Prerequisites</span></span>

* <span data-ttu-id="6dd6f-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="6dd6f-109">For more information, see [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-109">For more information, see [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6dd6f-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="6dd6f-111">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-111">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="6dd6f-112">Create the cluster using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6dd6f-112">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="6dd6f-113">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6dd6f-114">Click **Create a resource** > **Data + Analytics** > **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-114">Click **Create a resource** > **Data + Analytics** > **HDInsight**.</span></span>

3. <span data-ttu-id="6dd6f-115">From **Basics**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-115">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="6dd6f-116">**Cluster Name**: The name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-116">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="6dd6f-117">**Subscription**: Select the subscription to use.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-117">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="6dd6f-118">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-118">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="6dd6f-119">You use these credentials to access services such as the Ambari Web UI or REST API.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-119">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="6dd6f-120">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-120">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="6dd6f-121">By default the password is the same as the cluster login password.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-121">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="6dd6f-122">**Resource Group**: The resource group to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-122">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="6dd6f-123">**Location**: The Azure region to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-123">**Location**: The Azure region to create the cluster in.</span></span>

        ![Cluster basic details](./media/r-server-get-started/clustername.png)

4. <span data-ttu-id="6dd6f-125">Select **Cluster type**, and then set the following values in the **Cluster configuration** section:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-125">Select **Cluster type**, and then set the following values in the **Cluster configuration** section:</span></span>

    * <span data-ttu-id="6dd6f-126">**Cluster Type**: ML Services</span><span class="sxs-lookup"><span data-stu-id="6dd6f-126">**Cluster Type**: ML Services</span></span>

    * <span data-ttu-id="6dd6f-127">**Operating system**: Linux</span><span class="sxs-lookup"><span data-stu-id="6dd6f-127">**Operating system**: Linux</span></span>

    * <span data-ttu-id="6dd6f-128">**Version**: ML Server 9.3 (HDI 3.6).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-128">**Version**: ML Server 9.3 (HDI 3.6).</span></span> <span data-ttu-id="6dd6f-129">Release notes for ML Server 9.3 are available on [docs.microsoft.com](https://docs.microsoft.com/machine-learning-server/whats-new-in-machine-learning-server).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-129">Release notes for ML Server 9.3 are available on [docs.microsoft.com](https://docs.microsoft.com/machine-learning-server/whats-new-in-machine-learning-server).</span></span>

    * <span data-ttu-id="6dd6f-130">**R Studio community edition for ML Server**: This browser-based IDE is installed by default on the edge node.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-130">**R Studio community edition for ML Server**: This browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="6dd6f-131">Clear the check box if you prefer to not have it installed.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-131">Clear the check box if you prefer to not have it installed.</span></span> <span data-ttu-id="6dd6f-132">If you choose to have it installed, the URL for accessing the RStudio Server login is available on the portal application blade for your cluster once it’s been created.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-132">If you choose to have it installed, the URL for accessing the RStudio Server login is available on the portal application blade for your cluster once it’s been created.</span></span>

        ![Cluster basic details](./media/r-server-get-started/clustertypeconfig.png)

4. <span data-ttu-id="6dd6f-134">After selecting the cluster type, use the __Select__ button to set the cluster type.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-134">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="6dd6f-135">Next, use the __Next__ button to finish basic configuration.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-135">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="6dd6f-136">From the **Storage** section, select or create a Storage account.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-136">From the **Storage** section, select or create a Storage account.</span></span> <span data-ttu-id="6dd6f-137">For the steps in this document, leave the other fields in this section at the default values.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-137">For the steps in this document, leave the other fields in this section at the default values.</span></span> <span data-ttu-id="6dd6f-138">Use the __Next__ button to save storage configuration.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-138">Use the __Next__ button to save storage configuration.</span></span>

    ![Set the storage account settings for HDInsight](./media/r-server-get-started/cluster-storage.png)

6. <span data-ttu-id="6dd6f-140">From the **Summary** section, review the configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-140">From the **Summary** section, review the configuration for the cluster.</span></span> <span data-ttu-id="6dd6f-141">Use the __Edit__ links to change any settings that are incorrect.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-141">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="6dd6f-142">Finally, use the __Create__ button to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-142">Finally, use the __Create__ button to create the cluster.</span></span>

    ![Set the storage account settings for HDInsight](./media/r-server-get-started/clustersummary.png)

    > [!NOTE]
    > <span data-ttu-id="6dd6f-144">It can take up to 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-144">It can take up to 20 minutes to create the cluster.</span></span>

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="6dd6f-145">Connect to RStudio Server</span><span class="sxs-lookup"><span data-stu-id="6dd6f-145">Connect to RStudio Server</span></span>

<span data-ttu-id="6dd6f-146">If you chose to install RStudio Server Community Edition as part of your HDInsight cluster, then you can access the RStudio login using one of the following two methods:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-146">If you chose to install RStudio Server Community Edition as part of your HDInsight cluster, then you can access the RStudio login using one of the following two methods:</span></span>

* <span data-ttu-id="6dd6f-147">**Option 1** - Go to the following URL (where **CLUSTERNAME** is the name of the ML Services cluster you created):</span><span class="sxs-lookup"><span data-stu-id="6dd6f-147">**Option 1** - Go to the following URL (where **CLUSTERNAME** is the name of the ML Services cluster you created):</span></span>

        https://CLUSTERNAME.azurehdinsight.net/rstudio/

* <span data-ttu-id="6dd6f-148">**Option 2** - Open the ML Services cluster in the Azure portal, under **Quick links** click **ML Services Dashboards**.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-148">**Option 2** - Open the ML Services cluster in the Azure portal, under **Quick links** click **ML Services Dashboards**.</span></span>

     ![Set the storage account settings for HDInsight](./media/r-server-get-started/dashboard-quick-links.png)

    <span data-ttu-id="6dd6f-150">From **Cluster Dashboards**, click **R Studio Server**.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-150">From **Cluster Dashboards**, click **R Studio Server**.</span></span>

    ![Set the storage account settings for HDInsight](./media/r-server-get-started/r-studio-server-dashboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="6dd6f-152">Regardless of the method used, the first time you log in you need to authenticate twice.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-152">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="6dd6f-153">For the first authentication prompt, provide the *cluster Admin userid* and *password*.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-153">For the first authentication prompt, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="6dd6f-154">For the second authentication prompt, provide the *SSH userid* and *password*.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-154">For the second authentication prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="6dd6f-155">Subsequent log ins only require the SSH credentials.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-155">Subsequent log ins only require the SSH credentials.</span></span>

<span data-ttu-id="6dd6f-156">Once you are connected, your screen should resemble the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-156">Once you are connected, your screen should resemble the following screenshot:</span></span>

![Connect to RStudio](./media/r-server-get-started/connect-to-r-studio.png)

## <a name="run-a-sample-job"></a><span data-ttu-id="6dd6f-158">Run a sample job</span><span class="sxs-lookup"><span data-stu-id="6dd6f-158">Run a sample job</span></span>

<span data-ttu-id="6dd6f-159">You can submit a job using ScaleR functions.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-159">You can submit a job using ScaleR functions.</span></span> <span data-ttu-id="6dd6f-160">Here is an example of the commands used to run a job:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-160">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
    remoteDir <- "https://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-cluster-edge-node"></a><span data-ttu-id="6dd6f-161">Connect to the cluster edge node</span><span class="sxs-lookup"><span data-stu-id="6dd6f-161">Connect to the cluster edge node</span></span>

<span data-ttu-id="6dd6f-162">In this section, you learn how to connect to the edge node of an ML Services HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-162">In this section, you learn how to connect to the edge node of an ML Services HDInsight cluster using SSH.</span></span> <span data-ttu-id="6dd6f-163">For familiarity on using SSH, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-163">For familiarity on using SSH, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="6dd6f-164">The SSH command to connect to the ML Services cluster edge node is:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-164">The SSH command to connect to the ML Services cluster edge node is:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

<span data-ttu-id="6dd6f-165">To find the SSH command for your cluster, from the Azure portal click the cluster name, click **SSH + Cluster login**, and then for **Hostname**, select the edge node.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-165">To find the SSH command for your cluster, from the Azure portal click the cluster name, click **SSH + Cluster login**, and then for **Hostname**, select the edge node.</span></span> <span data-ttu-id="6dd6f-166">This displays the SSH Endpoint information for the edge node.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-166">This displays the SSH Endpoint information for the edge node.</span></span>

![Image of the SSH Endpoint for the edge node](./media/r-server-get-started/sshendpoint.png)

<span data-ttu-id="6dd6f-168">If you used a password to secure your SSH user account, you are prompted to enter it.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-168">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="6dd6f-169">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-169">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="6dd6f-170">For example:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-170">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6dd6f-171">Once connected, you get at a prompt similar to the following:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-171">Once connected, you get at a prompt similar to the following:</span></span>

    sshuser@ed00-myrclu:~$

<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="6dd6f-172">Use the R console</span><span class="sxs-lookup"><span data-stu-id="6dd6f-172">Use the R console</span></span>

1. <span data-ttu-id="6dd6f-173">From the SSH session, use the following command to start the R console:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-173">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="6dd6f-174">You should see an output with the version of ML Server, in addition to other information.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-174">You should see an output with the version of ML Server, in addition to other information.</span></span>
    
3. <span data-ttu-id="6dd6f-175">From the `>` prompt, you can enter R code.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-175">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="6dd6f-176">ML Services on HDInsight includes packages that allow you to easily interact with Hadoop and run distributed computations.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-176">ML Services on HDInsight includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="6dd6f-177">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-177">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

        rxHadoopListFiles("/")

4. <span data-ttu-id="6dd6f-178">You can also use the WASB style addressing.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-178">You can also use the WASB style addressing.</span></span>

        rxHadoopListFiles("wasb:///")

5. <span data-ttu-id="6dd6f-179">To quit the R console, use the following command:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-179">To quit the R console, use the following command:</span></span>

        quit()

## <a name="automated-cluster-creation"></a><span data-ttu-id="6dd6f-180">Automated cluster creation</span><span class="sxs-lookup"><span data-stu-id="6dd6f-180">Automated cluster creation</span></span>

<span data-ttu-id="6dd6f-181">You can automate the creation of ML Services cluster for HDInsight by using the SDK and the PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-181">You can automate the creation of ML Services cluster for HDInsight by using the SDK and the PowerShell.</span></span>

<!---* To create an ML Server cluster using an Azure Resource Management template, see [Deploy an R Server for HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).--->
* <span data-ttu-id="6dd6f-182">To create an ML Services cluster using the .NET SDK, see [Create Linux-based clusters in HDInsight using the .NET SDK.](../hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="6dd6f-182">To create an ML Services cluster using the .NET SDK, see [Create Linux-based clusters in HDInsight using the .NET SDK.](../hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="6dd6f-183">To create an ML Services cluster using powershell, see the article on [Create HDInsight clusters using Azure PowerShell](../hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-183">To create an ML Services cluster using powershell, see the article on [Create HDInsight clusters using Azure PowerShell](../hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="6dd6f-184">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="6dd6f-184">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="6dd6f-185">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="6dd6f-185">Troubleshoot</span></span>

<span data-ttu-id="6dd6f-186">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="6dd6f-186">If you run into issues with creating HDInsight clusters, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dd6f-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="6dd6f-187">Next steps</span></span>

<span data-ttu-id="6dd6f-188">In this article you learned how to create a new ML Services cluster in Azure HDInsight and the basics of using the R console from an SSH session.</span><span class="sxs-lookup"><span data-stu-id="6dd6f-188">In this article you learned how to create a new ML Services cluster in Azure HDInsight and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="6dd6f-189">The following articles explain other ways of managing and working with ML Services on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6dd6f-189">The following articles explain other ways of managing and working with ML Services on HDInsight:</span></span>

* [<span data-ttu-id="6dd6f-190">Submit jobs from R Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6dd6f-190">Submit jobs from R Tools for Visual Studio</span></span>](r-server-submit-jobs-r-tools-vs.md)
* [<span data-ttu-id="6dd6f-191">Manage ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dd6f-191">Manage ML Services cluster on HDInsight</span></span>](r-server-hdinsight-manage.md)
* [<span data-ttu-id="6dd6f-192">Operationalize ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dd6f-192">Operationalize ML Services cluster on HDInsight</span></span>](r-server-operationalize.md)
* [<span data-ttu-id="6dd6f-193">Compute context options for ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dd6f-193">Compute context options for ML Services cluster on HDInsight</span></span>](r-server-compute-contexts.md)
* [<span data-ttu-id="6dd6f-194">Azure Storage options for ML Services cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dd6f-194">Azure Storage options for ML Services cluster on HDInsight</span></span>](r-server-storage.md)
