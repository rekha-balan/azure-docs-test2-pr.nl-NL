---
title: Manage Hadoop clusters in HDInsight with PowerShell | Microsoft Docs
description: Learn how to perform administrative tasks for the Hadoop clusters in HDInsight using Azure PowerShell.
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: ''
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jgao
ms.openlocfilehash: 87c0f2dc2baec74c91ddb5ea1691a924acaf0deb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555754"
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="846c3-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="846c3-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="846c3-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span><span class="sxs-lookup"><span data-stu-id="846c3-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="846c3-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="846c3-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="846c3-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="846c3-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="846c3-107">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="846c3-107">**Prerequisites**</span></span>

<span data-ttu-id="846c3-108">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="846c3-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="846c3-109">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="846c3-109">**An Azure subscription**.</span></span> <span data-ttu-id="846c3-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="846c3-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="846c3-111">Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="846c3-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="846c3-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span><span class="sxs-lookup"><span data-stu-id="846c3-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="846c3-113">To check the version of the installed PowerShell:</span><span class="sxs-lookup"><span data-stu-id="846c3-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="846c3-114">To uninstall the older version, run Programs and Features in the control panel.</span><span class="sxs-lookup"><span data-stu-id="846c3-114">To uninstall the older version, run Programs and Features in the control panel.</span></span> 

## <a name="create-clusters"></a><span data-ttu-id="846c3-115">Create clusters</span><span class="sxs-lookup"><span data-stu-id="846c3-115">Create clusters</span></span>
<span data-ttu-id="846c3-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="846c3-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="846c3-117">List clusters</span><span class="sxs-lookup"><span data-stu-id="846c3-117">List clusters</span></span>
<span data-ttu-id="846c3-118">Use the following command to list all clusters in the current subscription:</span><span class="sxs-lookup"><span data-stu-id="846c3-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="846c3-119">Show cluster</span><span class="sxs-lookup"><span data-stu-id="846c3-119">Show cluster</span></span>
<span data-ttu-id="846c3-120">Use the following command to show details of a specific cluster in the current subscription:</span><span class="sxs-lookup"><span data-stu-id="846c3-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="846c3-121">Delete clusters</span><span class="sxs-lookup"><span data-stu-id="846c3-121">Delete clusters</span></span>
<span data-ttu-id="846c3-122">Use the following command to delete a cluster:</span><span class="sxs-lookup"><span data-stu-id="846c3-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="846c3-123">You can also delete a cluster by removing the resource group that contains the cluster.</span><span class="sxs-lookup"><span data-stu-id="846c3-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="846c3-124">Please note, this will delete all the resources in the group including the default storage account.</span><span class="sxs-lookup"><span data-stu-id="846c3-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="846c3-125">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="846c3-125">Scale clusters</span></span>
<span data-ttu-id="846c3-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span><span class="sxs-lookup"><span data-stu-id="846c3-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="846c3-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span><span class="sxs-lookup"><span data-stu-id="846c3-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="846c3-128">If you are unsure of the version of your cluster, you can check the Properties page.</span><span class="sxs-lookup"><span data-stu-id="846c3-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="846c3-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="846c3-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="846c3-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span><span class="sxs-lookup"><span data-stu-id="846c3-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="846c3-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="846c3-131">Hadoop</span></span>
  
    <span data-ttu-id="846c3-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span><span class="sxs-lookup"><span data-stu-id="846c3-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="846c3-133">New jobs can also be submitted while the operation is in progress.</span><span class="sxs-lookup"><span data-stu-id="846c3-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="846c3-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span><span class="sxs-lookup"><span data-stu-id="846c3-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="846c3-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span><span class="sxs-lookup"><span data-stu-id="846c3-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="846c3-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="846c3-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="846c3-137">You can, however, resubmit the jobs once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="846c3-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="846c3-138">HBase</span><span class="sxs-lookup"><span data-stu-id="846c3-138">HBase</span></span>
  
    <span data-ttu-id="846c3-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="846c3-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="846c3-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="846c3-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="846c3-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span><span class="sxs-lookup"><span data-stu-id="846c3-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="846c3-142">Storm</span><span class="sxs-lookup"><span data-stu-id="846c3-142">Storm</span></span>
  
    <span data-ttu-id="846c3-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span><span class="sxs-lookup"><span data-stu-id="846c3-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="846c3-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span><span class="sxs-lookup"><span data-stu-id="846c3-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="846c3-145">Rebalancing can be accomplished in two ways:</span><span class="sxs-lookup"><span data-stu-id="846c3-145">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="846c3-146">Storm web UI</span><span class="sxs-lookup"><span data-stu-id="846c3-146">Storm web UI</span></span>
  * <span data-ttu-id="846c3-147">Command-line interface (CLI) tool</span><span class="sxs-lookup"><span data-stu-id="846c3-147">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="846c3-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span><span class="sxs-lookup"><span data-stu-id="846c3-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="846c3-149">The Storm web UI is available on the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="846c3-149">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![HDInsight storm scale rebalance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.storm.rebalance.png)
    
    <span data-ttu-id="846c3-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span><span class="sxs-lookup"><span data-stu-id="846c3-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="846c3-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span><span class="sxs-lookup"><span data-stu-id="846c3-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="846c3-153">Grant/revoke access</span><span class="sxs-lookup"><span data-stu-id="846c3-153">Grant/revoke access</span></span>
<span data-ttu-id="846c3-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span><span class="sxs-lookup"><span data-stu-id="846c3-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="846c3-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="846c3-155">ODBC</span></span>
* <span data-ttu-id="846c3-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="846c3-156">JDBC</span></span>
* <span data-ttu-id="846c3-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="846c3-157">Ambari</span></span>
* <span data-ttu-id="846c3-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="846c3-158">Oozie</span></span>
* <span data-ttu-id="846c3-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="846c3-159">Templeton</span></span>

<span data-ttu-id="846c3-160">By default, these services are granted for access.</span><span class="sxs-lookup"><span data-stu-id="846c3-160">By default, these services are granted for access.</span></span> <span data-ttu-id="846c3-161">You can revoke/grant the access.</span><span class="sxs-lookup"><span data-stu-id="846c3-161">You can revoke/grant the access.</span></span> <span data-ttu-id="846c3-162">To revoke:</span><span class="sxs-lookup"><span data-stu-id="846c3-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="846c3-163">To grant:</span><span class="sxs-lookup"><span data-stu-id="846c3-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="846c3-164">By granting/revoking the access, you will reset the cluster user name and password.</span><span class="sxs-lookup"><span data-stu-id="846c3-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="846c3-165">This can also be done via the Portal.</span><span class="sxs-lookup"><span data-stu-id="846c3-165">This can also be done via the Portal.</span></span> <span data-ttu-id="846c3-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="846c3-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="846c3-167">Update HTTP user credentials</span><span class="sxs-lookup"><span data-stu-id="846c3-167">Update HTTP user credentials</span></span>
<span data-ttu-id="846c3-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span><span class="sxs-lookup"><span data-stu-id="846c3-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="846c3-169">And then grant the access with new HTTP user credentials.</span><span class="sxs-lookup"><span data-stu-id="846c3-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="846c3-170">Find the default storage account</span><span class="sxs-lookup"><span data-stu-id="846c3-170">Find the default storage account</span></span>
<span data-ttu-id="846c3-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span><span class="sxs-lookup"><span data-stu-id="846c3-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey 

## <a name="find-the-resource-group"></a><span data-ttu-id="846c3-172">Find the resource group</span><span class="sxs-lookup"><span data-stu-id="846c3-172">Find the resource group</span></span>
<span data-ttu-id="846c3-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="846c3-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="846c3-174">To find the resource group:</span><span class="sxs-lookup"><span data-stu-id="846c3-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="846c3-175">Submit jobs</span><span class="sxs-lookup"><span data-stu-id="846c3-175">Submit jobs</span></span>
<span data-ttu-id="846c3-176">**To submit MapReduce jobs**</span><span class="sxs-lookup"><span data-stu-id="846c3-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="846c3-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="846c3-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="846c3-178">**To submit Hive jobs**</span><span class="sxs-lookup"><span data-stu-id="846c3-178">**To submit Hive jobs**</span></span> 

<span data-ttu-id="846c3-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="846c3-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="846c3-180">**To submit Pig jobs**</span><span class="sxs-lookup"><span data-stu-id="846c3-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="846c3-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="846c3-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="846c3-182">**To submit Sqoop jobs**</span><span class="sxs-lookup"><span data-stu-id="846c3-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="846c3-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="846c3-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="846c3-184">**To submit Oozie jobs**</span><span class="sxs-lookup"><span data-stu-id="846c3-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="846c3-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="846c3-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="846c3-186">Upload data to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="846c3-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="846c3-187">See [Upload data to HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="846c3-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="846c3-188">See Also</span><span class="sxs-lookup"><span data-stu-id="846c3-188">See Also</span></span>
* <span data-ttu-id="846c3-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="846c3-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="846c3-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="846c3-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="846c3-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="846c3-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="846c3-192">[Create HDInsight clusters][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="846c3-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="846c3-193">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="846c3-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="846c3-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="846c3-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="846c3-195">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="846c3-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-provision-custom-options]: hdinsight-provision-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-administer-use-powershell/HDI.PS.Provision.png


