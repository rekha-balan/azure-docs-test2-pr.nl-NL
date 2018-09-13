---
title: Customize HDInsight Clusters using bootstrap - Azure
description: Learn how to customize HDInsight clusters using bootstrap.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/14/2018
ms.author: jasonh
ms.openlocfilehash: f0fe09a6d67d2ad72a1984168b669f34c8d8f3ef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791016"
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="696f2-103">Customize HDInsight clusters using Bootstrap</span><span class="sxs-lookup"><span data-stu-id="696f2-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="696f2-104">Sometimes, you want to configure the configuration files, which include:</span><span class="sxs-lookup"><span data-stu-id="696f2-104">Sometimes, you want to configure the configuration files, which include:</span></span>

* <span data-ttu-id="696f2-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="696f2-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-106">core-site.xml</span></span>
* <span data-ttu-id="696f2-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-107">gateway.xml</span></span>
* <span data-ttu-id="696f2-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-108">hbase-env.xml</span></span>
* <span data-ttu-id="696f2-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-109">hbase-site.xml</span></span>
* <span data-ttu-id="696f2-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-110">hdfs-site.xml</span></span>
* <span data-ttu-id="696f2-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-111">hive-env.xml</span></span>
* <span data-ttu-id="696f2-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-112">hive-site.xml</span></span>
* <span data-ttu-id="696f2-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="696f2-113">mapred-site</span></span>
* <span data-ttu-id="696f2-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-114">oozie-site.xml</span></span>
* <span data-ttu-id="696f2-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-115">oozie-env.xml</span></span>
* <span data-ttu-id="696f2-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-116">storm-site.xml</span></span>
* <span data-ttu-id="696f2-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-117">tez-site.xml</span></span>
* <span data-ttu-id="696f2-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-118">webhcat-site.xml</span></span>
* <span data-ttu-id="696f2-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="696f2-119">yarn-site.xml</span></span>
* <span data-ttu-id="696f2-120">server.properties (kafka-broker configuration)</span><span class="sxs-lookup"><span data-stu-id="696f2-120">server.properties (kafka-broker configuration)</span></span>

<span data-ttu-id="696f2-121">There are three methods to use bootstrap:</span><span class="sxs-lookup"><span data-stu-id="696f2-121">There are three methods to use bootstrap:</span></span>

* <span data-ttu-id="696f2-122">Use Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="696f2-122">Use Azure PowerShell</span></span>
* <span data-ttu-id="696f2-123">Use .NET SDK</span><span class="sxs-lookup"><span data-stu-id="696f2-123">Use .NET SDK</span></span>
* <span data-ttu-id="696f2-124">Use Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="696f2-124">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="696f2-125">For information on installing additional components on HDInsight cluster during the creation time, see:</span><span class="sxs-lookup"><span data-stu-id="696f2-125">For information on installing additional components on HDInsight cluster during the creation time, see:</span></span>

* [<span data-ttu-id="696f2-126">Customize HDInsight clusters using Script Action (Linux)</span><span class="sxs-lookup"><span data-stu-id="696f2-126">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="696f2-127">Use Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="696f2-127">Use Azure PowerShell</span></span>
<span data-ttu-id="696f2-128">The following PowerShell code customizes a Hive configuration:</span><span class="sxs-lookup"><span data-stu-id="696f2-128">The following PowerShell code customizes a Hive configuration:</span></span>

```powershell
# hive-site.xml configuration
$hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

$config = New-AzureRmHDInsightClusterConfig `
    | Set-AzureRmHDInsightDefaultStorage `
        -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -StorageAccountKey $defaultStorageAccountKey `
    | Add-AzureRmHDInsightConfigValues `
        -HiveSite $hiveConfigValues 

New-AzureRmHDInsightCluster `
    -ResourceGroupName $existingResourceGroupName `
    -ClusterName $clusterName `
    -Location $location `
    -ClusterSizeInNodes $clusterSizeInNodes `
    -ClusterType Hadoop `
    -OSType Linux `
    -Version "3.6" `
    -HttpCredential $httpCredential `
    -Config $config 
```

<span data-ttu-id="696f2-129">A complete working PowerShell script can be found in [Appendix](#appendix-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="696f2-129">A complete working PowerShell script can be found in [Appendix](#appendix-powershell-sample).</span></span>

<span data-ttu-id="696f2-130">**To verify the change:**</span><span class="sxs-lookup"><span data-stu-id="696f2-130">**To verify the change:**</span></span>

1. <span data-ttu-id="696f2-131">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="696f2-131">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="696f2-132">From the left menu, click **HDInsight clusters**.</span><span class="sxs-lookup"><span data-stu-id="696f2-132">From the left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="696f2-133">If you don't see it, click **All services** first.</span><span class="sxs-lookup"><span data-stu-id="696f2-133">If you don't see it, click **All services** first.</span></span>
3. <span data-ttu-id="696f2-134">Click the cluster you just created using the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="696f2-134">Click the cluster you just created using the PowerShell script.</span></span>
4. <span data-ttu-id="696f2-135">Click **Dashboard** from the top of the blade to open the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="696f2-135">Click **Dashboard** from the top of the blade to open the Ambari UI.</span></span>
5. <span data-ttu-id="696f2-136">Click **Hive** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="696f2-136">Click **Hive** from the left menu.</span></span>
6. <span data-ttu-id="696f2-137">Click **HiveServer2** from **Summary**.</span><span class="sxs-lookup"><span data-stu-id="696f2-137">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="696f2-138">Click the **Configs** tab.</span><span class="sxs-lookup"><span data-stu-id="696f2-138">Click the **Configs** tab.</span></span>
8. <span data-ttu-id="696f2-139">Click **Hive** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="696f2-139">Click **Hive** from the left menu.</span></span>
9. <span data-ttu-id="696f2-140">Click the **Advanced** tab.</span><span class="sxs-lookup"><span data-stu-id="696f2-140">Click the **Advanced** tab.</span></span>
10. <span data-ttu-id="696f2-141">Scroll down and then expand **Advanced hive-site**.</span><span class="sxs-lookup"><span data-stu-id="696f2-141">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="696f2-142">Look for **hive.metastore.client.socket.timeout** in the section.</span><span class="sxs-lookup"><span data-stu-id="696f2-142">Look for **hive.metastore.client.socket.timeout** in the section.</span></span>

<span data-ttu-id="696f2-143">Some more samples on customizing other configuration files:</span><span class="sxs-lookup"><span data-stu-id="696f2-143">Some more samples on customizing other configuration files:</span></span>

```xml
# hdfs-site.xml configuration
$HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

# core-site.xml configuration
$CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

# mapred-site.xml configuration
$MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

# oozie-site.xml configuration
$OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120
```
<span data-ttu-id="696f2-144">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="696f2-144">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="696f2-145">Use .NET SDK</span><span class="sxs-lookup"><span data-stu-id="696f2-145">Use .NET SDK</span></span>
<span data-ttu-id="696f2-146">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="696f2-146">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="696f2-147">Use Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="696f2-147">Use Resource Manager template</span></span>
<span data-ttu-id="696f2-148">You can use bootstrap in Resource Manager template:</span><span class="sxs-lookup"><span data-stu-id="696f2-148">You can use bootstrap in Resource Manager template:</span></span>

```json
"configurations": {
    �
    "hive-site": {
        "hive.metastore.client.connect.retry.delay": "5",
        "hive.execution.engine": "mr",
        "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
    }
}
```

![HDInsight Hadoop customizes cluster bootstrap Azure Resource Manager template](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="696f2-150">See also</span><span class="sxs-lookup"><span data-stu-id="696f2-150">See also</span></span>
* <span data-ttu-id="696f2-151">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span><span class="sxs-lookup"><span data-stu-id="696f2-151">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="696f2-152">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="696f2-152">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="696f2-153">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="696f2-153">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="696f2-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="696f2-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="696f2-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="696f2-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"

## <a name="appendix-powershell-sample"></a><span data-ttu-id="696f2-157">Appendix: PowerShell sample</span><span class="sxs-lookup"><span data-stu-id="696f2-157">Appendix: PowerShell sample</span></span>
<span data-ttu-id="696f2-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span><span class="sxs-lookup"><span data-stu-id="696f2-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

```powershell
####################################
# Set these variables
####################################
#region - used for creating Azure service names
$nameToken = "<ENTER AN ALIAS>" 
#endregion

#region - cluster user accounts
$httpUserName = "admin"  #HDInsight cluster username
$httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

$sshUserName = "sshuser" #HDInsight ssh user name
$sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
#endregion

####################################
# Service names and varialbes
####################################
#region - service names
$namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

$resourceGroupName = $namePrefix + "rg"
$hdinsightClusterName = $namePrefix + "hdi"
$defaultStorageAccountName = $namePrefix + "store"
$defaultBlobContainerName = $hdinsightClusterName

$location = "East US 2"
#endregion

# Treat all errors as terminating
$ErrorActionPreference = "Stop"

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Connect-AzureRmAccount}
#endregion

#region - Create an HDInsight cluster
####################################
# Create dependent components
####################################
Write-Host "Creating a resource group ..." -ForegroundColor Green
New-AzureRmResourceGroup `
    -Name  $resourceGroupName `
    -Location $location

Write-Host "Creating the default storage account and default blob container ..."  -ForegroundColor Green
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $defaultStorageAccountName `
    -Location $location `
    -Type Standard_GRS

$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
$defaultStorageContext = New-AzureStorageContext `
                                -StorageAccountName $defaultStorageAccountName `
                                -StorageAccountKey $defaultStorageAccountKey
New-AzureStorageContainer `
    -Name $defaultBlobContainerName `
    -Context $defaultStorageContext #use the cluster name as the container name

####################################
# Create a configuration object
####################################
$hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

$config = New-AzureRmHDInsightClusterConfig `
    | Set-AzureRmHDInsightDefaultStorage `
        -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -StorageAccountKey $defaultStorageAccountKey `
    | Add-AzureRmHDInsightConfigValues `
        -HiveSite $hiveConfigValues 

####################################
# Create an HDInsight cluster
####################################
$httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

$sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
$sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

New-AzureRmHDInsightCluster `
    -ResourceGroupName $resourceGroupName `
    -ClusterName $hdinsightClusterName `
    -Location $location `
    -ClusterSizeInNodes 1 `
    -ClusterType Hadoop `
    -OSType Linux `
    -Version "3.6" `
    -HttpCredential $httpCredential `
    -SshCredential $sshCredential `
    -Config $config

####################################
# Verify the cluster
####################################
Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

#endregion
```
