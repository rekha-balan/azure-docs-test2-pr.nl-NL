---
title: Use script action to install Zeppelin notebooks for Spark cluster on Azure HDInsight  | Microsoft Docs
description: Step-by-step instructions on how to install and use Zeppelin notebooks with Spark clusters on HDInsight Linux.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: cb276220-fb02-49e2-ac55-434fcb759629
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: f650e8dcee6e8f24680e8ec01ddd0f644c7f01ae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551994"
---
# <a name="install-zeppelin-notebooks-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="84408-103">Install Zeppelin notebooks for Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="84408-103">Install Zeppelin notebooks for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="84408-104">Learn how to install Zeppelin notebooks on Apache Spark clusters and how to use the Zeppelin notebooks to run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="84408-104">Learn how to install Zeppelin notebooks on Apache Spark clusters and how to use the Zeppelin notebooks to run Spark jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84408-105">If you provisioned a Spark 1.6 cluster on HDInsight 3.5, you can access Zeppelin by default using the instructions at [Use Zeppelin notebooks with Apache Spark cluster on HDInsight Linux](hdinsight-apache-spark-zeppelin-notebook.md).</span><span class="sxs-lookup"><span data-stu-id="84408-105">If you provisioned a Spark 1.6 cluster on HDInsight 3.5, you can access Zeppelin by default using the instructions at [Use Zeppelin notebooks with Apache Spark cluster on HDInsight Linux](hdinsight-apache-spark-zeppelin-notebook.md).</span></span> <span data-ttu-id="84408-106">If you want to use Zeppelin on HDInsight cluster versions 3.3 or 3.4, you must follow the instructions in this article to install Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="84408-106">If you want to use Zeppelin on HDInsight cluster versions 3.3 or 3.4, you must follow the instructions in this article to install Zeppelin.</span></span>
>
> <span data-ttu-id="84408-107">Using the scripts in this article to install Zeppelin on Spark 2.0 clusters is not supported.</span><span class="sxs-lookup"><span data-stu-id="84408-107">Using the scripts in this article to install Zeppelin on Spark 2.0 clusters is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84408-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="84408-108">Prerequisites</span></span>

* <span data-ttu-id="84408-109">You must have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="84408-109">You must have an Azure subscription.</span></span> <span data-ttu-id="84408-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="84408-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="84408-111">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84408-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="84408-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="84408-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <a name="install-zeppelin-on-a-spark-cluster"></a><span data-ttu-id="84408-113">Install Zeppelin on a Spark cluster</span><span class="sxs-lookup"><span data-stu-id="84408-113">Install Zeppelin on a Spark cluster</span></span>
<span data-ttu-id="84408-114">You can install Zeppelin on a Spark cluster using script action.</span><span class="sxs-lookup"><span data-stu-id="84408-114">You can install Zeppelin on a Spark cluster using script action.</span></span> <span data-ttu-id="84408-115">Script action uses custom scripts to install components on the cluster that are not available by default.</span><span class="sxs-lookup"><span data-stu-id="84408-115">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="84408-116">You can use the custom script to install Zeppelin from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84408-116">You can use the custom script to install Zeppelin from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="84408-117">You can use the script to install Zeppelin either as part of cluster creation, or after the cluster is up and running.</span><span class="sxs-lookup"><span data-stu-id="84408-117">You can use the script to install Zeppelin either as part of cluster creation, or after the cluster is up and running.</span></span> <span data-ttu-id="84408-118">Links in the sections below provide the instructions on how to do so.</span><span class="sxs-lookup"><span data-stu-id="84408-118">Links in the sections below provide the instructions on how to do so.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="84408-119">Using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="84408-119">Using the Azure Portal</span></span>
<span data-ttu-id="84408-120">For instructions on how to use the Azure Portal to run script action to install Zeppelin, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="84408-120">For instructions on how to use the Azure Portal to run script action to install Zeppelin, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="84408-121">You must make a couple of changes to the instructions in that article.</span><span class="sxs-lookup"><span data-stu-id="84408-121">You must make a couple of changes to the instructions in that article.</span></span>

* <span data-ttu-id="84408-122">You must use the script to install Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="84408-122">You must use the script to install Zeppelin.</span></span> <span data-ttu-id="84408-123">The custom script to install Zeppelin on a Spark cluster on HDInsight is available from the following links:</span><span class="sxs-lookup"><span data-stu-id="84408-123">The custom script to install Zeppelin on a Spark cluster on HDInsight is available from the following links:</span></span>

  * <span data-ttu-id="84408-124">For Spark 1.6.0 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark160-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="84408-124">For Spark 1.6.0 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark160-v01.sh`</span></span>
  * <span data-ttu-id="84408-125">For Spark 1.5.2 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="84408-125">For Spark 1.5.2 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh`</span></span>
* <span data-ttu-id="84408-126">You must run the script action only on the headnode.</span><span class="sxs-lookup"><span data-stu-id="84408-126">You must run the script action only on the headnode.</span></span>
* <span data-ttu-id="84408-127">The script does not need any parameters.</span><span class="sxs-lookup"><span data-stu-id="84408-127">The script does not need any parameters.</span></span>

### <a name="using-hdinsight-net-sdk"></a><span data-ttu-id="84408-128">Using HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="84408-128">Using HDInsight .NET SDK</span></span>
<span data-ttu-id="84408-129">For instructions on how to use HDInsight .NET SDK to run script action to install Zeppelin, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="84408-129">For instructions on how to use HDInsight .NET SDK to run script action to install Zeppelin, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="84408-130">You must make a couple of changes to the instructions in that article.</span><span class="sxs-lookup"><span data-stu-id="84408-130">You must make a couple of changes to the instructions in that article.</span></span>

* <span data-ttu-id="84408-131">You must use the script to install Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="84408-131">You must use the script to install Zeppelin.</span></span> <span data-ttu-id="84408-132">The custom script to install Zeppelin on a Spark cluster on HDInsight is available from the following links:</span><span class="sxs-lookup"><span data-stu-id="84408-132">The custom script to install Zeppelin on a Spark cluster on HDInsight is available from the following links:</span></span>

  * <span data-ttu-id="84408-133">For Spark 1.6.0 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark160-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="84408-133">For Spark 1.6.0 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark160-v01.sh`</span></span>
  * <span data-ttu-id="84408-134">For Spark 1.5.2 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="84408-134">For Spark 1.5.2 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh`</span></span>
* <span data-ttu-id="84408-135">The script does not need any parameters.</span><span class="sxs-lookup"><span data-stu-id="84408-135">The script does not need any parameters.</span></span>
* <span data-ttu-id="84408-136">Set the cluster type you are creating to Spark.</span><span class="sxs-lookup"><span data-stu-id="84408-136">Set the cluster type you are creating to Spark.</span></span>

### <a name="using-azure-powershell"></a><span data-ttu-id="84408-137">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="84408-137">Using Azure PowerShell</span></span>
<span data-ttu-id="84408-138">Use the following PowerShell snippet to create a Spark cluster on HDInsight Linux with Zeppelin installed.</span><span class="sxs-lookup"><span data-stu-id="84408-138">Use the following PowerShell snippet to create a Spark cluster on HDInsight Linux with Zeppelin installed.</span></span> <span data-ttu-id="84408-139">Depending on which version of Spark cluster you have, you must update the PowerShell snippet below to include the link to the corresponding custom script.</span><span class="sxs-lookup"><span data-stu-id="84408-139">Depending on which version of Spark cluster you have, you must update the PowerShell snippet below to include the link to the corresponding custom script.</span></span>

* <span data-ttu-id="84408-140">For Spark 1.6.0 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark160-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="84408-140">For Spark 1.6.0 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark160-v01.sh`</span></span>
* <span data-ttu-id="84408-141">For Spark 1.5.2 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh`</span><span class="sxs-lookup"><span data-stu-id="84408-141">For Spark 1.5.2 clusters - `https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh`</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    Login-AzureRMAccount

    # PROVIDE VALUES FOR THE VARIABLES
    $clusterAdminUsername="admin"
    $clusterAdminPassword="<<password>>"
    $clusterSshUsername="adminssh"
    $clusterSshPassword="<<password>>"
    $clusterName="<<clustername>>"
    $clusterContainerName=$clusterName
    $resourceGroupName="<<resourceGroupName>>"
    $location="<<region>>"
    $storage1Name="<<storagename>>"
    $storage1Key="<<storagekey>>"
    $subscriptionId="<<subscriptionId>>"

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $passwordAsSecureString=ConvertTo-SecureString $clusterAdminPassword -AsPlainText -Force
    $clusterCredential=New-Object System.Management.Automation.PSCredential ($clusterAdminUsername, $passwordAsSecureString)
    $passwordAsSecureString=ConvertTo-SecureString $clusterSshPassword -AsPlainText -Force
    $clusterSshCredential=New-Object System.Management.Automation.PSCredential ($clusterSshUsername, $passwordAsSecureString)

    $azureHDInsightConfigs= New-AzureRmHDInsightClusterConfig -ClusterType Spark
    $azureHDInsightConfigs.DefaultStorageAccountKey = $storage1Key
    $azureHDInsightConfigs.DefaultStorageAccountName = "$storage1Name.blob.core.windows.net"

    Add-AzureRMHDInsightScriptAction -Config $azureHDInsightConfigs -Name "Install Zeppelin" -NodeType HeadNode -Parameters "void" -Uri "https://hdiconfigactions.blob.core.windows.net/linuxincubatorzeppelinv01/install-zeppelin-spark151-v01.sh"

    New-AzureRMHDInsightCluster -Config $azureHDInsightConfigs -OSType Linux -HeadNodeSize "Standard_D12" -WorkerNodeSize "Standard_D12" -ClusterSizeInNodes 2 -Location $location -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $clusterCredential -DefaultStorageContainer $clusterContainerName -SshCredential $clusterSshCredential -Version "3.3"

## <a name="access-the-zeppelin-notebook"></a><span data-ttu-id="84408-142">Access the Zeppelin notebook</span><span class="sxs-lookup"><span data-stu-id="84408-142">Access the Zeppelin notebook</span></span>

<span data-ttu-id="84408-143">Once you have successfully installed Zeppelin using script action, you can use the following steps to access Zeppelin notebook on the Spark cluster by following the steps below.</span><span class="sxs-lookup"><span data-stu-id="84408-143">Once you have successfully installed Zeppelin using script action, you can use the following steps to access Zeppelin notebook on the Spark cluster by following the steps below.</span></span> <span data-ttu-id="84408-144">In this section, you will see how to run %sql and %hive statements.</span><span class="sxs-lookup"><span data-stu-id="84408-144">In this section, you will see how to run %sql and %hive statements.</span></span>

1. <span data-ttu-id="84408-145">From the web browser, open the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="84408-145">From the web browser, open the following endpoint:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/zeppelin

   
2. <span data-ttu-id="84408-146">Create a new notebook.</span><span class="sxs-lookup"><span data-stu-id="84408-146">Create a new notebook.</span></span> <span data-ttu-id="84408-147">From the header pane, click **Notebook**, and then click **Create New Note**.</span><span class="sxs-lookup"><span data-stu-id="84408-147">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>

    <span data-ttu-id="84408-148">![Create a new Zeppelin notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.createnewnote.png "Create a new Zeppelin notebook")</span><span class="sxs-lookup"><span data-stu-id="84408-148">![Create a new Zeppelin notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.createnewnote.png "Create a new Zeppelin notebook")</span></span>

    <span data-ttu-id="84408-149">On the same page, under the **Notebook** heading, you should see a new notebook with the name starting with **Note XXXXXXXXX**.</span><span class="sxs-lookup"><span data-stu-id="84408-149">On the same page, under the **Notebook** heading, you should see a new notebook with the name starting with **Note XXXXXXXXX**.</span></span> <span data-ttu-id="84408-150">Click the new notebook.</span><span class="sxs-lookup"><span data-stu-id="84408-150">Click the new notebook.</span></span>
3. <span data-ttu-id="84408-151">On the web page for the new notebook, click the heading, and change the name of the notebook if you want to.</span><span class="sxs-lookup"><span data-stu-id="84408-151">On the web page for the new notebook, click the heading, and change the name of the notebook if you want to.</span></span> <span data-ttu-id="84408-152">Press ENTER to save the name change.</span><span class="sxs-lookup"><span data-stu-id="84408-152">Press ENTER to save the name change.</span></span> <span data-ttu-id="84408-153">Also, make sure the notebook header shows a **Connected** status in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="84408-153">Also, make sure the notebook header shows a **Connected** status in the top-right corner.</span></span>

    <span data-ttu-id="84408-154">![Zeppelin notebook status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.newnote.connected.png "Zeppelin notebook status")</span><span class="sxs-lookup"><span data-stu-id="84408-154">![Zeppelin notebook status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.newnote.connected.png "Zeppelin notebook status")</span></span>

### <a name="run-sql-statements"></a><span data-ttu-id="84408-155">Run SQL statements</span><span class="sxs-lookup"><span data-stu-id="84408-155">Run SQL statements</span></span>
1. <span data-ttu-id="84408-156">Load sample data into a temporary table.</span><span class="sxs-lookup"><span data-stu-id="84408-156">Load sample data into a temporary table.</span></span> <span data-ttu-id="84408-157">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="84408-157">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="84408-158">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span><span class="sxs-lookup"><span data-stu-id="84408-158">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>

        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)

        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0),
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()

        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")

    <span data-ttu-id="84408-159">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span><span class="sxs-lookup"><span data-stu-id="84408-159">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="84408-160">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span><span class="sxs-lookup"><span data-stu-id="84408-160">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="84408-161">The output shows up at the bottom of the same paragraph.</span><span class="sxs-lookup"><span data-stu-id="84408-161">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="84408-162">The screenshot looks like the following:</span><span class="sxs-lookup"><span data-stu-id="84408-162">The screenshot looks like the following:</span></span>

    <span data-ttu-id="84408-163">![Create a temporary table from raw data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.note.loaddDataintotable.png "Create a temporary table from raw data")</span><span class="sxs-lookup"><span data-stu-id="84408-163">![Create a temporary table from raw data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.note.loaddDataintotable.png "Create a temporary table from raw data")</span></span>

    <span data-ttu-id="84408-164">You can also provide a title to each paragraph.</span><span class="sxs-lookup"><span data-stu-id="84408-164">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="84408-165">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span><span class="sxs-lookup"><span data-stu-id="84408-165">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
2. <span data-ttu-id="84408-166">You can now run Spark SQL statements on the **hvac** table.</span><span class="sxs-lookup"><span data-stu-id="84408-166">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="84408-167">Paste the following query in a new paragraph.</span><span class="sxs-lookup"><span data-stu-id="84408-167">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="84408-168">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span><span class="sxs-lookup"><span data-stu-id="84408-168">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="84408-169">Press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="84408-169">Press **SHIFT + ENTER**.</span></span>

        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date
        from hvac
        where date = "6/1/13"

    <span data-ttu-id="84408-170">The **%sql** statement at the beginning tells the notebook to use the Spark  SQL interpreter.</span><span class="sxs-lookup"><span data-stu-id="84408-170">The **%sql** statement at the beginning tells the notebook to use the Spark  SQL interpreter.</span></span> <span data-ttu-id="84408-171">You can look at the defined interpreters from the **Interpreter** tab in the notebook header.</span><span class="sxs-lookup"><span data-stu-id="84408-171">You can look at the defined interpreters from the **Interpreter** tab in the notebook header.</span></span>

    <span data-ttu-id="84408-172">The following screenshot shows the output.</span><span class="sxs-lookup"><span data-stu-id="84408-172">The following screenshot shows the output.</span></span>

    <span data-ttu-id="84408-173">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.note.sparksqlquery1.png "Run a Spark SQL statement using the notebook")</span><span class="sxs-lookup"><span data-stu-id="84408-173">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.note.sparksqlquery1.png "Run a Spark SQL statement using the notebook")</span></span>

     <span data-ttu-id="84408-174">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span><span class="sxs-lookup"><span data-stu-id="84408-174">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="84408-175">Click **Settings** to choose what consitutes the key and values in the output.</span><span class="sxs-lookup"><span data-stu-id="84408-175">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="84408-176">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span><span class="sxs-lookup"><span data-stu-id="84408-176">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
3. <span data-ttu-id="84408-177">You can also run Spark SQL statements using variables in the query.</span><span class="sxs-lookup"><span data-stu-id="84408-177">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="84408-178">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span><span class="sxs-lookup"><span data-stu-id="84408-178">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="84408-179">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span><span class="sxs-lookup"><span data-stu-id="84408-179">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>

        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff
        from hvac
        where targettemp > "${Temp = 65,65|75|85}"

    <span data-ttu-id="84408-180">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="84408-180">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="84408-181">The following screenshot shows the output.</span><span class="sxs-lookup"><span data-stu-id="84408-181">The following screenshot shows the output.</span></span>

    <span data-ttu-id="84408-182">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.note.sparksqlquery2.png "Run a Spark SQL statement using the notebook")</span><span class="sxs-lookup"><span data-stu-id="84408-182">![Run a Spark SQL statement using the notebook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.note.sparksqlquery2.png "Run a Spark SQL statement using the notebook")</span></span>

    <span data-ttu-id="84408-183">For subsequent queries, you can select a new value from the drop-down and run the query again.</span><span class="sxs-lookup"><span data-stu-id="84408-183">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="84408-184">Click **Settings** to choose what consitutes the key and values in the output.</span><span class="sxs-lookup"><span data-stu-id="84408-184">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="84408-185">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span><span class="sxs-lookup"><span data-stu-id="84408-185">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
4. <span data-ttu-id="84408-186">Restart the Spark SQL interpreter to exit the application.</span><span class="sxs-lookup"><span data-stu-id="84408-186">Restart the Spark SQL interpreter to exit the application.</span></span> <span data-ttu-id="84408-187">Click the **Interpreter** tab at the top, and for the Spark interpreter, click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="84408-187">Click the **Interpreter** tab at the top, and for the Spark interpreter, click **Restart**.</span></span>

    <span data-ttu-id="84408-188">![Restart the Zeppelin intepreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.zeppelin.restart.interpreter.png "Restart the Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="84408-188">![Restart the Zeppelin intepreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/hdispark.zeppelin.restart.interpreter.png "Restart the Zeppelin intepreter")</span></span>

### <a name="run-hive-statements"></a><span data-ttu-id="84408-189">Run hive statements</span><span class="sxs-lookup"><span data-stu-id="84408-189">Run hive statements</span></span>
1. <span data-ttu-id="84408-190">From the Zeppelin notebook, click the **Interpreter** button.</span><span class="sxs-lookup"><span data-stu-id="84408-190">From the Zeppelin notebook, click the **Interpreter** button.</span></span>

    <span data-ttu-id="84408-191">![Update Hive interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-1.png "Update Hive interpreter")</span><span class="sxs-lookup"><span data-stu-id="84408-191">![Update Hive interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-1.png "Update Hive interpreter")</span></span>
2. <span data-ttu-id="84408-192">For the **hive** interpreter, click **edit**.</span><span class="sxs-lookup"><span data-stu-id="84408-192">For the **hive** interpreter, click **edit**.</span></span>

    <span data-ttu-id="84408-193">![Update Hive interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-2.png "Update Hive interpreter")</span><span class="sxs-lookup"><span data-stu-id="84408-193">![Update Hive interpreter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-2.png "Update Hive interpreter")</span></span>

    <span data-ttu-id="84408-194">Update the following properties.</span><span class="sxs-lookup"><span data-stu-id="84408-194">Update the following properties.</span></span>

   * <span data-ttu-id="84408-195">Set **default.password** to the password you specified for the admin user while creating the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="84408-195">Set **default.password** to the password you specified for the admin user while creating the HDInsight Spark cluster.</span></span>
   * <span data-ttu-id="84408-196">Set **default.url** to `jdbc:hive2://<spark_cluster_name>.azurehdinsight.net:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2`.</span><span class="sxs-lookup"><span data-stu-id="84408-196">Set **default.url** to `jdbc:hive2://<spark_cluster_name>.azurehdinsight.net:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2`.</span></span> <span data-ttu-id="84408-197">Replace **\<spark_cluster_name>** with the name of your Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="84408-197">Replace **\<spark_cluster_name>** with the name of your Spark cluster.</span></span>
   * <span data-ttu-id="84408-198">Set **default.user** to the name of the admin user you specified while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="84408-198">Set **default.user** to the name of the admin user you specified while creating the cluster.</span></span> <span data-ttu-id="84408-199">For example, *admin*.</span><span class="sxs-lookup"><span data-stu-id="84408-199">For example, *admin*.</span></span>
3. <span data-ttu-id="84408-200">Click **Save** and when prompted to restart the hive interpreter, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="84408-200">Click **Save** and when prompted to restart the hive interpreter, click **OK**.</span></span>
4. <span data-ttu-id="84408-201">Create a new notebook and run the following statement to list all the hive tables on the cluster.</span><span class="sxs-lookup"><span data-stu-id="84408-201">Create a new notebook and run the following statement to list all the hive tables on the cluster.</span></span>

        %hive
        SHOW TABLES

    <span data-ttu-id="84408-202">By default, an HDInsight cluster has a sample table called **hivesampletable** so you should see the following output.</span><span class="sxs-lookup"><span data-stu-id="84408-202">By default, an HDInsight cluster has a sample table called **hivesampletable** so you should see the following output.</span></span>

    <span data-ttu-id="84408-203">![Hive output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-3.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="84408-203">![Hive output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-3.png "Hive output")</span></span>
5. <span data-ttu-id="84408-204">Run the following statement to list the records in the table.</span><span class="sxs-lookup"><span data-stu-id="84408-204">Run the following statement to list the records in the table.</span></span>

        %hive
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="84408-205">You should an output like the following.</span><span class="sxs-lookup"><span data-stu-id="84408-205">You should an output like the following.</span></span>

    <span data-ttu-id="84408-206">![Hive output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-4.png "Hive output")</span><span class="sxs-lookup"><span data-stu-id="84408-206">![Hive output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-use-zeppelin-notebook/zeppelin-update-hive-interpreter-4.png "Hive output")</span></span>

## <a name="seealso"></a><span data-ttu-id="84408-207">See also</span><span class="sxs-lookup"><span data-stu-id="84408-207">See also</span></span>
* [<span data-ttu-id="84408-208">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="84408-208">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="84408-209">Scenarios</span><span class="sxs-lookup"><span data-stu-id="84408-209">Scenarios</span></span>
* [<span data-ttu-id="84408-210">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="84408-210">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="84408-211">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="84408-211">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="84408-212">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="84408-212">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="84408-213">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="84408-213">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="84408-214">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="84408-214">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="84408-215">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="84408-215">Create and run applications</span></span>
* [<span data-ttu-id="84408-216">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="84408-216">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="84408-217">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="84408-217">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="84408-218">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="84408-218">Tools and extensions</span></span>
* [<span data-ttu-id="84408-219">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="84408-219">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="84408-220">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="84408-220">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="84408-221">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="84408-221">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="84408-222">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="84408-222">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="84408-223">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="84408-223">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="84408-224">Manage resources</span><span class="sxs-lookup"><span data-stu-id="84408-224">Manage resources</span></span>
* [<span data-ttu-id="84408-225">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="84408-225">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="84408-226">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="84408-226">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md










