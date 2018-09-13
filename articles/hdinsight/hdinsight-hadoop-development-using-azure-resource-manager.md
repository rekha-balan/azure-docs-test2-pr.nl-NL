---
title: Migrate to Azure Resource Manager tools for HDInsight
description: How to migrate to Azure Resource Manager development tools for HDInsight clusters
services: hdinsight
ms.reviewer: jasonh
author: jasonwhowell
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: jasonh
ms.openlocfilehash: 1988593fa7cb0d84baffc4264147d350962bb6bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808332"
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="4056b-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="4056b-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="4056b-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4056b-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="4056b-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager versions of PowerShell, CLI, and .NET SDK going forward.</span><span class="sxs-lookup"><span data-stu-id="4056b-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="4056b-106">This article provides pointers on how to migrate to the new Resource Manager-based approach.</span><span class="sxs-lookup"><span data-stu-id="4056b-106">This article provides pointers on how to migrate to the new Resource Manager-based approach.</span></span> <span data-ttu-id="4056b-107">Wherever applicable, this document highlights the differences between the ASM and Resource Manager approaches for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4056b-107">Wherever applicable, this document highlights the differences between the ASM and Resource Manager approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4056b-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span><span class="sxs-lookup"><span data-stu-id="4056b-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="4056b-109">Migrating Azure CLI to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4056b-109">Migrating Azure CLI to Azure Resource Manager</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4056b-110">Azure CLI 2.0 does not provide support for working with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4056b-110">Azure CLI 2.0 does not provide support for working with HDInsight clusters.</span></span> <span data-ttu-id="4056b-111">You can still use Azure CLI 1.0 with HDInsight, however Azure CLI 1.0 is deprecated.</span><span class="sxs-lookup"><span data-stu-id="4056b-111">You can still use Azure CLI 1.0 with HDInsight, however Azure CLI 1.0 is deprecated.</span></span>

<span data-ttu-id="4056b-112">The following are the basic commands for working with HDInsight through Azure CLI 1.0:</span><span class="sxs-lookup"><span data-stu-id="4056b-112">The following are the basic commands for working with HDInsight through Azure CLI 1.0:</span></span>

* <span data-ttu-id="4056b-113">`azure hdinsight cluster create` - creates a new HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="4056b-113">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="4056b-114">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="4056b-114">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="4056b-115">`azure hdinsight cluster show` - display information about an existing cluster</span><span class="sxs-lookup"><span data-stu-id="4056b-115">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="4056b-116">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4056b-116">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="4056b-117">Use the `-h` switch to inspect the parameters and switches available for each command.</span><span class="sxs-lookup"><span data-stu-id="4056b-117">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="4056b-118">New commands</span><span class="sxs-lookup"><span data-stu-id="4056b-118">New commands</span></span>
<span data-ttu-id="4056b-119">New commands available with Azure Resource Manager are:</span><span class="sxs-lookup"><span data-stu-id="4056b-119">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="4056b-120">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span><span class="sxs-lookup"><span data-stu-id="4056b-120">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="4056b-121">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span><span class="sxs-lookup"><span data-stu-id="4056b-121">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="4056b-122">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span><span class="sxs-lookup"><span data-stu-id="4056b-122">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="4056b-123">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span><span class="sxs-lookup"><span data-stu-id="4056b-123">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="4056b-124">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span><span class="sxs-lookup"><span data-stu-id="4056b-124">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="4056b-125">Deprecated commands</span><span class="sxs-lookup"><span data-stu-id="4056b-125">Deprecated commands</span></span>
<span data-ttu-id="4056b-126">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these commands are not available through the Resource Manager commands.</span><span class="sxs-lookup"><span data-stu-id="4056b-126">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these commands are not available through the Resource Manager commands.</span></span> <span data-ttu-id="4056b-127">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4056b-127">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="4056b-128">For more information on submitting jobs using REST APIs, see the following documents.</span><span class="sxs-lookup"><span data-stu-id="4056b-128">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="4056b-129">Run MapReduce jobs with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="4056b-129">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hadoop/apache-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="4056b-130">Run Hive queries with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="4056b-130">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hadoop/apache-hadoop-use-hive-curl.md)
* [<span data-ttu-id="4056b-131">Run Pig jobs with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="4056b-131">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hadoop/apache-hadoop-use-pig-curl.md)

<span data-ttu-id="4056b-132">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hadoop/hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hadoop/hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hadoop/hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="4056b-132">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hadoop/hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hadoop/hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hadoop/hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="4056b-133">Examples</span><span class="sxs-lookup"><span data-stu-id="4056b-133">Examples</span></span>
<span data-ttu-id="4056b-134">**Creating a cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-134">**Creating a cluster**</span></span>

* <span data-ttu-id="4056b-135">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="4056b-135">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="4056b-136">New command - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="4056b-136">New command - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="4056b-137">**Deleting a cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-137">**Deleting a cluster**</span></span>

* <span data-ttu-id="4056b-138">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="4056b-138">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="4056b-139">New command - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="4056b-139">New command - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="4056b-140">**List clusters**</span><span class="sxs-lookup"><span data-stu-id="4056b-140">**List clusters**</span></span>

* <span data-ttu-id="4056b-141">Old command (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="4056b-141">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="4056b-142">New command - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="4056b-142">New command - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="4056b-143">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span><span class="sxs-lookup"><span data-stu-id="4056b-143">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="4056b-144">**Show cluster information**</span><span class="sxs-lookup"><span data-stu-id="4056b-144">**Show cluster information**</span></span>

* <span data-ttu-id="4056b-145">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="4056b-145">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="4056b-146">New command - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="4056b-146">New command - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="4056b-147">Migrating Azure PowerShell to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4056b-147">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="4056b-148">The general information about Azure PowerShell in the Azure Resource Manager mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4056b-148">The general information about Azure PowerShell in the Azure Resource Manager mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="4056b-149">The Azure PowerShell Resource Manager cmdlets can be installed side by side with the ASM cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4056b-149">The Azure PowerShell Resource Manager cmdlets can be installed side by side with the ASM cmdlets.</span></span> <span data-ttu-id="4056b-150">The cmdlets from the two modes can be distinguished by their names.</span><span class="sxs-lookup"><span data-stu-id="4056b-150">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="4056b-151">The Resource Manager mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span><span class="sxs-lookup"><span data-stu-id="4056b-151">The Resource Manager mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="4056b-152">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="4056b-152">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="4056b-153">Parameters and switches may have news names, and there are many new parameters available when using Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4056b-153">Parameters and switches may have news names, and there are many new parameters available when using Resource Manager.</span></span>  <span data-ttu-id="4056b-154">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="4056b-154">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="4056b-155">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="4056b-155">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="4056b-156">Connect-AzureRmAccount or [Select-AzureRmProfile](https://docs.microsoft.com/powershell/module/servicemanagement/azurerm.profile/select-azurermprofile?view=azuresmps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="4056b-156">Connect-AzureRmAccount or [Select-AzureRmProfile](https://docs.microsoft.com/powershell/module/servicemanagement/azurerm.profile/select-azurermprofile?view=azuresmps-4.0.0).</span></span> <span data-ttu-id="4056b-157">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="4056b-157">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="4056b-158">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4056b-158">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="4056b-159">Renamed cmdlets</span><span class="sxs-lookup"><span data-stu-id="4056b-159">Renamed cmdlets</span></span>
<span data-ttu-id="4056b-160">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span><span class="sxs-lookup"><span data-stu-id="4056b-160">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="4056b-161">The following table lists the ASM cmdlets and their names in Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="4056b-161">The following table lists the ASM cmdlets and their names in Resource Manager mode:</span></span>

| <span data-ttu-id="4056b-162">ASM cmdlets</span><span class="sxs-lookup"><span data-stu-id="4056b-162">ASM cmdlets</span></span> | <span data-ttu-id="4056b-163">Resource Manager cmdlets</span><span class="sxs-lookup"><span data-stu-id="4056b-163">Resource Manager cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="4056b-164">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="4056b-164">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="4056b-165">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="4056b-165">Add-AzureRmHDInsightConfigValues</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/add-azurermhdinsightconfigvalues?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-166">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="4056b-166">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="4056b-167">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="4056b-167">Add-AzureRmHDInsightMetastore</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/add-azurermhdinsightmetastore?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-168">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="4056b-168">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="4056b-169">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="4056b-169">Add-AzureRmHDInsightScriptAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/add-azurermhdinsightscriptaction?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-170">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="4056b-170">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="4056b-171">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="4056b-171">Add-AzureRmHDInsightStorage</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/add-azurermhdinsightstorage?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-172">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-172">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="4056b-173">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-173">Get-AzureRmHDInsightCluster</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/get-azurermhdinsightcluster?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-174">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-174">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="4056b-175">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-175">Get-AzureRmHDInsightJob</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/get-azurermhdinsightjob?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-176">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="4056b-176">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="4056b-177">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="4056b-177">Get-AzureRmHDInsightJobOutput</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/get-azurermhdinsightjoboutput?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-178">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="4056b-178">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="4056b-179">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="4056b-179">Get-AzureRmHDInsightProperties</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/get-azurermhdinsightproperties?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-180">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-180">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="4056b-181">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-181">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/grant-azurermhdinsighthttpservicesaccess?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-182">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-182">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="4056b-183">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-183">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/grant-azurermhdinsightrdpservicesaccess?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-184">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="4056b-184">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="4056b-185">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="4056b-185">Invoke-AzureRmHDInsightHiveJob</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/invoke-azurermhdinsighthivejob?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-186">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-186">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="4056b-187">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-187">New-AzureRmHDInsightCluster</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsightcluster) |
| <span data-ttu-id="4056b-188">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="4056b-188">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="4056b-189">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="4056b-189">New-AzureRmHDInsightClusterConfig</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsightclusterconfig?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-190">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-190">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="4056b-191">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-191">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsighthivejobdefinition?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-192">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-192">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="4056b-193">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-193">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsightmapreducejobdefinition?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-194">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-194">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="4056b-195">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-195">New-AzureRmHDInsightPigJobDefinition</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsightpigjobdefinition?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-196">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-196">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="4056b-197">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-197">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsightsqoopjobdefinition?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-198">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-198">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="4056b-199">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="4056b-199">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/new-azurermhdinsightstreamingmapreducejobdefinition?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-200">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-200">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="4056b-201">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-201">Remove-AzureRmHDInsightCluster</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/remove-azurermhdinsightcluster?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-202">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-202">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="4056b-203">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-203">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/revoke-azurermhdinsighthttpservicesaccess?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-204">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-204">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="4056b-205">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="4056b-205">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/revoke-azurermhdinsightrdpservicesaccess?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-206">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="4056b-206">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="4056b-207">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="4056b-207">Set-AzureRmHDInsightClusterSize</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/set-azurermhdinsightclustersize?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-208">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="4056b-208">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="4056b-209">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="4056b-209">Set-AzureRmHDInsightDefaultStorage</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/set-azurermhdinsightdefaultstorage?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-210">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-210">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="4056b-211">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-211">Start-AzureRmHDInsightJob</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/start-azurermhdinsightjob?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-212">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-212">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="4056b-213">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-213">Stop-AzureRmHDInsightJob</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/stop-azurermhdinsightjob?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-214">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-214">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="4056b-215">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="4056b-215">Use-AzureRmHDInsightCluster</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/use-azurermhdinsightcluster?view=azurermps-6.6.0) |
| <span data-ttu-id="4056b-216">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-216">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="4056b-217">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="4056b-217">Wait-AzureRmHDInsightJob</span></span>](https://docs.microsoft.com/powershell/module/azurerm.hdinsight/wait-azurermhdinsightjob?view=azurermps-6.6.0) |

### <a name="new-cmdlets"></a><span data-ttu-id="4056b-218">New cmdlets</span><span class="sxs-lookup"><span data-stu-id="4056b-218">New cmdlets</span></span>
<span data-ttu-id="4056b-219">The following are the new cmdlets that are only available in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="4056b-219">The following are the new cmdlets that are only available in Resource Manager mode.</span></span> 

<span data-ttu-id="4056b-220">**Script action-related cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="4056b-220">**Script action-related cmdlets:**</span></span>

* <span data-ttu-id="4056b-221">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span><span class="sxs-lookup"><span data-stu-id="4056b-221">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="4056b-222">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span><span class="sxs-lookup"><span data-stu-id="4056b-222">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="4056b-223">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4056b-223">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="4056b-224">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span><span class="sxs-lookup"><span data-stu-id="4056b-224">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="4056b-225">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4056b-225">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="4056b-226">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4056b-226">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="4056b-227">**Cluster identity-related cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="4056b-227">**Cluster identity-related cmdlets:**</span></span>

* <span data-ttu-id="4056b-228">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span><span class="sxs-lookup"><span data-stu-id="4056b-228">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="4056b-229">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4056b-229">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="4056b-230">Examples</span><span class="sxs-lookup"><span data-stu-id="4056b-230">Examples</span></span>
<span data-ttu-id="4056b-231">**Create cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-231">**Create cluster**</span></span>

<span data-ttu-id="4056b-232">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="4056b-232">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="4056b-233">New command:</span><span class="sxs-lookup"><span data-stu-id="4056b-233">New command:</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="4056b-234">**Delete cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-234">**Delete cluster**</span></span>

<span data-ttu-id="4056b-235">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="4056b-235">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="4056b-236">New command:</span><span class="sxs-lookup"><span data-stu-id="4056b-236">New command:</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="4056b-237">**List cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-237">**List cluster**</span></span>

<span data-ttu-id="4056b-238">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="4056b-238">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="4056b-239">New command:</span><span class="sxs-lookup"><span data-stu-id="4056b-239">New command:</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="4056b-240">**Show cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-240">**Show cluster**</span></span>

<span data-ttu-id="4056b-241">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="4056b-241">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="4056b-242">New command:</span><span class="sxs-lookup"><span data-stu-id="4056b-242">New command:</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="4056b-243">Other samples</span><span class="sxs-lookup"><span data-stu-id="4056b-243">Other samples</span></span>
* [<span data-ttu-id="4056b-244">Create HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="4056b-244">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="4056b-245">Submit Hive jobs</span><span class="sxs-lookup"><span data-stu-id="4056b-245">Submit Hive jobs</span></span>](hadoop/apache-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="4056b-246">Submit Pig jobs</span><span class="sxs-lookup"><span data-stu-id="4056b-246">Submit Pig jobs</span></span>](hadoop/apache-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="4056b-247">Submit Sqoop jobs</span><span class="sxs-lookup"><span data-stu-id="4056b-247">Submit Sqoop jobs</span></span>](hadoop/apache-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-new-hdinsight-net-sdk"></a><span data-ttu-id="4056b-248">Migrating to the new HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-248">Migrating to the new HDInsight .NET SDK</span></span>
<span data-ttu-id="4056b-249">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span><span class="sxs-lookup"><span data-stu-id="4056b-249">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="4056b-250">You are encouraged to use the Azure Resource Management-based [Resource Manager-based HDInsight .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight).</span><span class="sxs-lookup"><span data-stu-id="4056b-250">You are encouraged to use the Azure Resource Management-based [Resource Manager-based HDInsight .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/hdinsight).</span></span> <span data-ttu-id="4056b-251">The following ASM-based HDInsight packages are being deprecated.</span><span class="sxs-lookup"><span data-stu-id="4056b-251">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="4056b-252">This section provides pointers to more information on how to perform certain tasks using the Resource Manager-based SDK.</span><span class="sxs-lookup"><span data-stu-id="4056b-252">This section provides pointers to more information on how to perform certain tasks using the Resource Manager-based SDK.</span></span>

| <span data-ttu-id="4056b-253">How to... using the Resource Manager-based HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-253">How to... using the Resource Manager-based HDInsight SDK</span></span> | <span data-ttu-id="4056b-254">Links</span><span class="sxs-lookup"><span data-stu-id="4056b-254">Links</span></span> |
| --- | --- |
| <span data-ttu-id="4056b-255">Create HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-255">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-256">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="4056b-256">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="4056b-257">Customize a cluster using Script Action with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-257">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="4056b-258">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="4056b-258">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="4056b-259">Authenticate applications interactively using Azure Active Directory with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-259">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="4056b-260">See [Run Hive queries using .NET SDK](hadoop/apache-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4056b-260">See [Run Hive queries using .NET SDK](hadoop/apache-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="4056b-261">The code snippet in this article uses the interactive authentication approach.</span><span class="sxs-lookup"><span data-stu-id="4056b-261">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="4056b-262">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-262">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="4056b-263">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="4056b-263">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="4056b-264">Submit a Hive job using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-264">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="4056b-265">See [Submit Hive jobs](hadoop/apache-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="4056b-265">See [Submit Hive jobs](hadoop/apache-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="4056b-266">Submit a Pig job using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-266">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="4056b-267">See [Submit Pig jobs](hadoop/apache-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="4056b-267">See [Submit Pig jobs](hadoop/apache-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="4056b-268">Submit a Sqoop job using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-268">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="4056b-269">See [Submit Sqoop jobs](hadoop/apache-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="4056b-269">See [Submit Sqoop jobs](hadoop/apache-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="4056b-270">List HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-270">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-271">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="4056b-271">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="4056b-272">Scale HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-272">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-273">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="4056b-273">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="4056b-274">Grant/revoke access to HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-274">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-275">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="4056b-275">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="4056b-276">Update HTTP user credentials for HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-276">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-277">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="4056b-277">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="4056b-278">Find the default storage account for HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-278">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-279">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="4056b-279">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="4056b-280">Delete HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4056b-280">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="4056b-281">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="4056b-281">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="4056b-282">Examples</span><span class="sxs-lookup"><span data-stu-id="4056b-282">Examples</span></span>
<span data-ttu-id="4056b-283">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the Resource Manager-based SDK.</span><span class="sxs-lookup"><span data-stu-id="4056b-283">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the Resource Manager-based SDK.</span></span>

<span data-ttu-id="4056b-284">**Creating a cluster CRUD client**</span><span class="sxs-lookup"><span data-stu-id="4056b-284">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="4056b-285">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="4056b-285">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="4056b-286">New command (Service principal authorization)</span><span class="sxs-lookup"><span data-stu-id="4056b-286">New command (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="4056b-287">New command (User authorization)</span><span class="sxs-lookup"><span data-stu-id="4056b-287">New command (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="4056b-288">**Creating a cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-288">**Creating a cluster**</span></span>

* <span data-ttu-id="4056b-289">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="4056b-289">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="4056b-290">New command</span><span class="sxs-lookup"><span data-stu-id="4056b-290">New command</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="4056b-291">**Enabling HTTP access**</span><span class="sxs-lookup"><span data-stu-id="4056b-291">**Enabling HTTP access**</span></span>

* <span data-ttu-id="4056b-292">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="4056b-292">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="4056b-293">New command</span><span class="sxs-lookup"><span data-stu-id="4056b-293">New command</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="4056b-294">**Deleting a cluster**</span><span class="sxs-lookup"><span data-stu-id="4056b-294">**Deleting a cluster**</span></span>

* <span data-ttu-id="4056b-295">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="4056b-295">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="4056b-296">New command</span><span class="sxs-lookup"><span data-stu-id="4056b-296">New command</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

