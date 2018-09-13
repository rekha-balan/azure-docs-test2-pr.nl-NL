---
title: 'Quickstart: Create an Spark cluster in HDInsight using Azure PowerShell'
description: This quickstart shows how to use Azure PowerShell to create an Apache Spark cluster in Azure HDInsight, and run a simple Spark SQL query.
services: azure-hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: quickstart
ms.date: 05/07/2018
ms.author: jasonh
ms.custom: mvc
ms.openlocfilehash: 2e179396ed8ec98f1d8ee61d5173f2f43b31d6f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857066"
---
# <a name="quickstart-create-a-spark-cluster-in-hdinsight-using-powershell"></a><span data-ttu-id="e1b4f-103">Quickstart: Create a Spark cluster in HDInsight using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1b4f-103">Quickstart: Create a Spark cluster in HDInsight using PowerShell</span></span>
<span data-ttu-id="e1b4f-104">Learn how to create Apache Spark cluster in Azure HDInsight, and how to run Spark SQL queries against Hive tables.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-104">Learn how to create Apache Spark cluster in Azure HDInsight, and how to run Spark SQL queries against Hive tables.</span></span> <span data-ttu-id="e1b4f-105">Apache Spark enables fast data analytics and cluster computing using in-memory processing.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-105">Apache Spark enables fast data analytics and cluster computing using in-memory processing.</span></span> <span data-ttu-id="e1b4f-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1b4f-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](apache-spark-overview.md).</span></span>

<span data-ttu-id="e1b4f-107">In this quickstart, you use Azure PowerShell to create an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-107">In this quickstart, you use Azure PowerShell to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="e1b4f-108">The cluster uses Azure Storage Blobs as the cluster storage.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-108">The cluster uses Azure Storage Blobs as the cluster storage.</span></span> <span data-ttu-id="e1b4f-109">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e1b4f-109">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1b4f-110">Billing for HDInsight clusters is prorated per minute, whether you are using them or not.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-110">Billing for HDInsight clusters is prorated per minute, whether you are using them or not.</span></span> <span data-ttu-id="e1b4f-111">Be sure to delete your cluster after you have finished using it.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-111">Be sure to delete your cluster after you have finished using it.</span></span> <span data-ttu-id="e1b4f-112">For more information, see the [Clean up resources](#clean-up-resources) section of this article.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-112">For more information, see the [Clean up resources](#clean-up-resources) section of this article.</span></span>

<span data-ttu-id="e1b4f-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="create-an-hdinsight-spark-cluster"></a><span data-ttu-id="e1b4f-114">Create an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="e1b4f-114">Create an HDInsight Spark cluster</span></span>

<span data-ttu-id="e1b4f-115">Creating an HDInsight cluster includes creating the following Azure objects and resources:</span><span class="sxs-lookup"><span data-stu-id="e1b4f-115">Creating an HDInsight cluster includes creating the following Azure objects and resources:</span></span>

- <span data-ttu-id="e1b4f-116">An Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-116">An Azure resource group.</span></span> <span data-ttu-id="e1b4f-117">An Azure resource group is a container for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-117">An Azure resource group is a container for Azure resources.</span></span> 
- <span data-ttu-id="e1b4f-118">An Azure storage account or an Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-118">An Azure storage account or an Azure Data Lake Store.</span></span>  <span data-ttu-id="e1b4f-119">Each HDInsight cluster requires a dependent data storage.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-119">Each HDInsight cluster requires a dependent data storage.</span></span> <span data-ttu-id="e1b4f-120">In this quickstart, you create a storage account.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-120">In this quickstart, you create a storage account.</span></span>
- <span data-ttu-id="e1b4f-121">An HDInsight cluster of different cluster types.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-121">An HDInsight cluster of different cluster types.</span></span>  <span data-ttu-id="e1b4f-122">In this quickstart, you create a Spark 2.3 cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-122">In this quickstart, you create a Spark 2.3 cluster.</span></span>

<span data-ttu-id="e1b4f-123">You use a PowerShell script to create the resources.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-123">You use a PowerShell script to create the resources.</span></span>  <span data-ttu-id="e1b4f-124">When you run the script, you are prompted to enter the following values:</span><span class="sxs-lookup"><span data-stu-id="e1b4f-124">When you run the script, you are prompted to enter the following values:</span></span>

|<span data-ttu-id="e1b4f-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="e1b4f-125">Parameter</span></span>|<span data-ttu-id="e1b4f-126">Value</span><span class="sxs-lookup"><span data-stu-id="e1b4f-126">Value</span></span>|
|------|------|
|<span data-ttu-id="e1b4f-127">Azure resource group name</span><span class="sxs-lookup"><span data-stu-id="e1b4f-127">Azure resource group name</span></span> | <span data-ttu-id="e1b4f-128">Provide a unique name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-128">Provide a unique name for the resource group.</span></span>|
|<span data-ttu-id="e1b4f-129">Location</span><span class="sxs-lookup"><span data-stu-id="e1b4f-129">Location</span></span>| <span data-ttu-id="e1b4f-130">Specify the Azure region, for example 'Central US'.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-130">Specify the Azure region, for example 'Central US'.</span></span> |
|<span data-ttu-id="e1b4f-131">Default storage account name</span><span class="sxs-lookup"><span data-stu-id="e1b4f-131">Default storage account name</span></span> | <span data-ttu-id="e1b4f-132">Provide a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-132">Provide a unique name for the storage account.</span></span> |
|<span data-ttu-id="e1b4f-133">Cluster name</span><span class="sxs-lookup"><span data-stu-id="e1b4f-133">Cluster name</span></span> | <span data-ttu-id="e1b4f-134">Provide a unique name for the HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-134">Provide a unique name for the HDInsight Spark cluster.</span></span>|
|<span data-ttu-id="e1b4f-135">Cluster login credentials</span><span class="sxs-lookup"><span data-stu-id="e1b4f-135">Cluster login credentials</span></span> | <span data-ttu-id="e1b4f-136">You use this account to connect to the cluster dashboard later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-136">You use this account to connect to the cluster dashboard later in the quickstart.</span></span>|
|<span data-ttu-id="e1b4f-137">SSH user credentials</span><span class="sxs-lookup"><span data-stu-id="e1b4f-137">SSH user credentials</span></span> | <span data-ttu-id="e1b4f-138">The SSH clients can be used to create a remote command-line session with the HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-138">The SSH clients can be used to create a remote command-line session with the HDInsight clusters.</span></span>|



1. <span data-ttu-id="e1b4f-139">Click **Try It** in the upper right corner for the following code block to open [Azure Cloud Shell](../../cloud-shell/overview.md), and the follow the instructions to connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-139">Click **Try It** in the upper right corner for the following code block to open [Azure Cloud Shell](../../cloud-shell/overview.md), and the follow the instructions to connect to Azure.</span></span>
2. <span data-ttu-id="e1b4f-140">Copy and paste the following PowerShell script in the cloud shell.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-140">Copy and paste the following PowerShell script in the cloud shell.</span></span> 

    ```azurepowershell-interactive
    ### Create a Spark 2.3 cluster in Azure HDInsight
        
    # Create the resource group
    $resourceGroupName = Read-Host -Prompt "Enter the resource group name"
    $location = Read-Host -Prompt "Enter the Azure region to create resources in, such as 'Central US'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    
    $defaultStorageAccountName = Read-Host -Prompt "Enter the default storage account name"
    
    # Create an Azure storae account and container
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Type Standard_LRS `
        -Location $location
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    
    # Create a Spark 2.3 cluster
    $clusterName = Read-Host -Prompt "Enter the name of the HDInsight cluster"
    # Cluster login is used to secure HTTPS services hosted on the cluster
    $httpCredential = Get-Credential -Message "Enter Cluster login credentials" -UserName "admin"
    # SSH user is used to remotely connect to the cluster using SSH clients
    $sshCredentials = Get-Credential -Message "Enter SSH user credentials"
    
    # Default cluster size (# of worker nodes), version, type, and OS
    $clusterSizeInNodes = "1"
    $clusterVersion = "3.6"
    $clusterType = "Spark"
    $clusterOS = "Linux"
    
    # Set the storage container name to the cluster name
    $defaultBlobContainerName = $clusterName
    
    # Create a blob container. This holds the default data store for the cluster.
    New-AzureStorageContainer `
        -Name $clusterName -Context $defaultStorageContext 
    
    $sparkConfig = New-Object "System.Collections.Generic.Dictionary``2[System.String,System.String]"
    $sparkConfig.Add("spark", "2.3")
    
    # Create the HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType $clusterType `
        -OSType $clusterOS `
        -Version $clusterVersion `
        -ComponentVersion $sparkConfig `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $clusterName `
        -SshCredential $sshCredentials 
    
    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    ```
<span data-ttu-id="e1b4f-141">It takes about 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-141">It takes about 20 minutes to create the cluster.</span></span> <span data-ttu-id="e1b4f-142">The cluster must be created before you can proceed to the next session.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-142">The cluster must be created before you can proceed to the next session.</span></span>

<span data-ttu-id="e1b4f-143">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-143">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="e1b4f-144">For more information, see [Access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="e1b4f-144">For more information, see [Access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="create-a-jupyter-notebook"></a><span data-ttu-id="e1b4f-145">Create a Jupyter notebook</span><span class="sxs-lookup"><span data-stu-id="e1b4f-145">Create a Jupyter notebook</span></span>

<span data-ttu-id="e1b4f-146">Jupyter Notebook is an interactive notebook environment that supports various programming languages.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-146">Jupyter Notebook is an interactive notebook environment that supports various programming languages.</span></span> <span data-ttu-id="e1b4f-147">The notebook allows you to interact with your data, combine code with markdown text and perform simple visualizations.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-147">The notebook allows you to interact with your data, combine code with markdown text and perform simple visualizations.</span></span> 

1. <span data-ttu-id="e1b4f-148">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1b4f-148">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1b4f-149">Select **HDInsight clusters**, and then select the cluster you created.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-149">Select **HDInsight clusters**, and then select the cluster you created.</span></span>

    ![open HDInsight cluster in the Azure portal](./media/apache-spark-jupyter-spark-sql/azure-portal-open-hdinsight-cluster.png)

3. <span data-ttu-id="e1b4f-151">From the portal, select **Cluster dashboards**, and then select **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-151">From the portal, select **Cluster dashboards**, and then select **Jupyter Notebook**.</span></span> <span data-ttu-id="e1b4f-152">If prompted, enter the cluster login credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-152">If prompted, enter the cluster login credentials for the cluster.</span></span>

   <span data-ttu-id="e1b4f-153">![Open Jupyter Notebook to run interactive Spark SQL query](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter Notebook to run interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="e1b4f-153">![Open Jupyter Notebook to run interactive Spark SQL query](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter Notebook to run interactive Spark SQL query")</span></span>

4. <span data-ttu-id="e1b4f-154">Select **New** > **PySpark** to create a notebook.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-154">Select **New** > **PySpark** to create a notebook.</span></span> 

   <span data-ttu-id="e1b4f-155">![Create a Jupyter Notebook to run interactive Spark SQL query](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-spark-sql-query.png "Create a Jupyter Notebook to run interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="e1b4f-155">![Create a Jupyter Notebook to run interactive Spark SQL query](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-spark-sql-query.png "Create a Jupyter Notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="e1b4f-156">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="e1b4f-156">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>


## <a name="run-spark-sql-statements"></a><span data-ttu-id="e1b4f-157">Run Spark SQL statements</span><span class="sxs-lookup"><span data-stu-id="e1b4f-157">Run Spark SQL statements</span></span>

<span data-ttu-id="e1b4f-158">SQL (Structured Query Language) is the most common and widely used language for querying and defining data.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-158">SQL (Structured Query Language) is the most common and widely used language for querying and defining data.</span></span> <span data-ttu-id="e1b4f-159">Spark SQL functions as an extension to Apache Spark for processing structured data, using the familiar SQL syntax.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-159">Spark SQL functions as an extension to Apache Spark for processing structured data, using the familiar SQL syntax.</span></span>

1. <span data-ttu-id="e1b4f-160">Verify the kernel is ready.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-160">Verify the kernel is ready.</span></span> <span data-ttu-id="e1b4f-161">The kernel is ready when you see a hollow circle next to the kernel name in the notebook.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-161">The kernel is ready when you see a hollow circle next to the kernel name in the notebook.</span></span> <span data-ttu-id="e1b4f-162">Solid circle denotes that the kernel is busy.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-162">Solid circle denotes that the kernel is busy.</span></span>

    <span data-ttu-id="e1b4f-163">![Hive query in HDInsight Spark](./media/apache-spark-jupyter-spark-sql/jupyter-spark-kernel-status.png "Hive query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b4f-163">![Hive query in HDInsight Spark](./media/apache-spark-jupyter-spark-sql/jupyter-spark-kernel-status.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="e1b4f-164">When you start the notebook for the first time, the kernel performs some tasks in the background.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-164">When you start the notebook for the first time, the kernel performs some tasks in the background.</span></span> <span data-ttu-id="e1b4f-165">Wait for the kernel to be ready.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-165">Wait for the kernel to be ready.</span></span> 
2. <span data-ttu-id="e1b4f-166">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-166">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="e1b4f-167">The command lists the Hive tables on the cluster:</span><span class="sxs-lookup"><span data-stu-id="e1b4f-167">The command lists the Hive tables on the cluster:</span></span>

    ```PySpark
    %%sql
    SHOW TABLES
    ```
    <span data-ttu-id="e1b4f-168">When you use a Jupyter Notebook with your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-168">When you use a Jupyter Notebook with your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="e1b4f-169">`%%sql` tells Jupyter Notebook to use the preset `sqlContext` to run the Hive query.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-169">`%%sql` tells Jupyter Notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="e1b4f-170">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that comes with all HDInsight clusters by default.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-170">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that comes with all HDInsight clusters by default.</span></span> <span data-ttu-id="e1b4f-171">It takes about 30 seconds to get the results.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-171">It takes about 30 seconds to get the results.</span></span> <span data-ttu-id="e1b4f-172">The output looks like:</span><span class="sxs-lookup"><span data-stu-id="e1b4f-172">The output looks like:</span></span> 

    <span data-ttu-id="e1b4f-173">![Hive query in HDInsight Spark](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b4f-173">![Hive query in HDInsight Spark](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="e1b4f-174">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-174">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="e1b4f-175">You also see a solid circle next to the **PySpark** text in the top-right corner.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-175">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span>
    
2. <span data-ttu-id="e1b4f-176">Run another query to see the data in `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-176">Run another query to see the data in `hivesampletable`.</span></span>

    ```PySpark
    %%sql
    SELECT * FROM hivesampletable LIMIT 10
    ```
    
    <span data-ttu-id="e1b4f-177">The screen shall refresh to show the query output.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-177">The screen shall refresh to show the query output.</span></span>

    <span data-ttu-id="e1b4f-178">![Hive query output in HDInsight Spark](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b4f-178">![Hive query output in HDInsight Spark](./media/apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

2. <span data-ttu-id="e1b4f-179">From the **File** menu on the notebook, select **Close and Halt**.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-179">From the **File** menu on the notebook, select **Close and Halt**.</span></span> <span data-ttu-id="e1b4f-180">Shutting down the notebook releases the cluster resources.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-180">Shutting down the notebook releases the cluster resources.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e1b4f-181">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e1b4f-181">Clean up resources</span></span>
<span data-ttu-id="e1b4f-182">HDInsight saves your data in Azure Storage or Azure Data Lake Store, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-182">HDInsight saves your data in Azure Storage or Azure Data Lake Store, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="e1b4f-183">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-183">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="e1b4f-184">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-184">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="e1b4f-185">If you plan to work on the tutorial listed in [Next steps](#next-steps) immediately, you might want to keep the cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-185">If you plan to work on the tutorial listed in [Next steps](#next-steps) immediately, you might want to keep the cluster.</span></span>

<span data-ttu-id="e1b4f-186">Switch back to the Azure portal, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-186">Switch back to the Azure portal, and select **Delete**.</span></span>

<span data-ttu-id="e1b4f-187">![Delete an HDInsight cluster](./media/apache-spark-jupyter-spark-sql/hdinsight-azure-portal-delete-cluster.png "Delete HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="e1b4f-187">![Delete an HDInsight cluster](./media/apache-spark-jupyter-spark-sql/hdinsight-azure-portal-delete-cluster.png "Delete HDInsight cluster")</span></span>

<span data-ttu-id="e1b4f-188">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-188">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span></span> <span data-ttu-id="e1b4f-189">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-189">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1b4f-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1b4f-190">Next steps</span></span> 

<span data-ttu-id="e1b4f-191">In this quickstart, you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-191">In this quickstart, you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="e1b4f-192">Advance to the next tutorial to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span><span class="sxs-lookup"><span data-stu-id="e1b4f-192">Advance to the next tutorial to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="e1b4f-193">Run interactive queries on Spark</span><span class="sxs-lookup"><span data-stu-id="e1b4f-193">Run interactive queries on Spark</span></span>](./apache-spark-load-data-run-query.md)
