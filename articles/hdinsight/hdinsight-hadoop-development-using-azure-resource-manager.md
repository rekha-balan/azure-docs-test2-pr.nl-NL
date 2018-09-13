---
title: Migrate to Azure Resource Manager tools for HDInsight | Microsoft Docs
description: How to migrate to Azure Resource Manager development tools for HDInsight clusters
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: ''
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 32d7da4ac08db3788490882bc37de3a3f7db9753
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555517"
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="7be71-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="7be71-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="7be71-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7be71-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="7be71-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span><span class="sxs-lookup"><span data-stu-id="7be71-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="7be71-106">This article provides pointers on how to migrate to the new ARM-based approach.</span><span class="sxs-lookup"><span data-stu-id="7be71-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="7be71-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7be71-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7be71-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span><span class="sxs-lookup"><span data-stu-id="7be71-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="7be71-109">Migrating Azure CLI to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7be71-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="7be71-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span><span class="sxs-lookup"><span data-stu-id="7be71-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="7be71-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span><span class="sxs-lookup"><span data-stu-id="7be71-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="7be71-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span><span class="sxs-lookup"><span data-stu-id="7be71-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="7be71-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span><span class="sxs-lookup"><span data-stu-id="7be71-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="7be71-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="7be71-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="7be71-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="7be71-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="7be71-116">`azure hdinsight cluster show` - display information about an existing cluster</span><span class="sxs-lookup"><span data-stu-id="7be71-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="7be71-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7be71-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="7be71-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span><span class="sxs-lookup"><span data-stu-id="7be71-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="7be71-119">New commands</span><span class="sxs-lookup"><span data-stu-id="7be71-119">New commands</span></span>
<span data-ttu-id="7be71-120">New commands available with Azure Resource Manager are:</span><span class="sxs-lookup"><span data-stu-id="7be71-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="7be71-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span><span class="sxs-lookup"><span data-stu-id="7be71-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="7be71-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span><span class="sxs-lookup"><span data-stu-id="7be71-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="7be71-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span><span class="sxs-lookup"><span data-stu-id="7be71-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="7be71-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span><span class="sxs-lookup"><span data-stu-id="7be71-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="7be71-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span><span class="sxs-lookup"><span data-stu-id="7be71-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="7be71-126">Deprecated commands</span><span class="sxs-lookup"><span data-stu-id="7be71-126">Deprecated commands</span></span>
<span data-ttu-id="7be71-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span><span class="sxs-lookup"><span data-stu-id="7be71-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="7be71-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7be71-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="7be71-129">For more information on submitting jobs using REST APIs, see the following documents.</span><span class="sxs-lookup"><span data-stu-id="7be71-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="7be71-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="7be71-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="7be71-131">Run Hive queries with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="7be71-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="7be71-132">Run Pig jobs with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="7be71-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="7be71-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="7be71-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="7be71-134">Examples</span><span class="sxs-lookup"><span data-stu-id="7be71-134">Examples</span></span>
<span data-ttu-id="7be71-135">**Creating a cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-135">**Creating a cluster**</span></span>

* <span data-ttu-id="7be71-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="7be71-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="7be71-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="7be71-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="7be71-138">**Deleting a cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="7be71-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="7be71-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="7be71-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="7be71-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="7be71-141">**List clusters**</span><span class="sxs-lookup"><span data-stu-id="7be71-141">**List clusters**</span></span>

* <span data-ttu-id="7be71-142">Old command (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="7be71-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="7be71-143">New command (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="7be71-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="7be71-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span><span class="sxs-lookup"><span data-stu-id="7be71-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="7be71-145">**Show cluster information**</span><span class="sxs-lookup"><span data-stu-id="7be71-145">**Show cluster information**</span></span>

* <span data-ttu-id="7be71-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="7be71-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="7be71-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="7be71-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="7be71-148">Migrating Azure PowerShell to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7be71-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="7be71-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7be71-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="7be71-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7be71-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="7be71-151">The cmdlets from the two modes can be distinguished by their names.</span><span class="sxs-lookup"><span data-stu-id="7be71-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="7be71-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span><span class="sxs-lookup"><span data-stu-id="7be71-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="7be71-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="7be71-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="7be71-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span><span class="sxs-lookup"><span data-stu-id="7be71-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="7be71-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="7be71-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="7be71-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="7be71-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="7be71-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="7be71-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="7be71-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="7be71-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="7be71-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7be71-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="7be71-160">Renamed cmdlets</span><span class="sxs-lookup"><span data-stu-id="7be71-160">Renamed cmdlets</span></span>
<span data-ttu-id="7be71-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span><span class="sxs-lookup"><span data-stu-id="7be71-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="7be71-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span><span class="sxs-lookup"><span data-stu-id="7be71-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="7be71-163">ASM cmdlets</span><span class="sxs-lookup"><span data-stu-id="7be71-163">ASM cmdlets</span></span> | <span data-ttu-id="7be71-164">ARM cmdlets</span><span class="sxs-lookup"><span data-stu-id="7be71-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="7be71-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="7be71-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="7be71-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="7be71-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="7be71-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="7be71-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="7be71-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="7be71-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="7be71-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="7be71-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="7be71-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="7be71-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="7be71-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="7be71-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="7be71-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="7be71-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="7be71-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7be71-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="7be71-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="7be71-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="7be71-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="7be71-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="7be71-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="7be71-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="7be71-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="7be71-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="7be71-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="7be71-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="7be71-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="7be71-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="7be71-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="7be71-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="7be71-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="7be71-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="7be71-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="7be71-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="7be71-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7be71-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="7be71-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="7be71-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="7be71-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="7be71-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="7be71-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="7be71-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="7be71-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="7be71-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="7be71-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="7be71-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="7be71-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="7be71-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="7be71-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="7be71-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7be71-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="7be71-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7be71-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="7be71-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="7be71-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="7be71-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="7be71-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7be71-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="7be71-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="7be71-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="7be71-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="7be71-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="7be71-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="7be71-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="7be71-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="7be71-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="7be71-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="7be71-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="7be71-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="7be71-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="7be71-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7be71-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7be71-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="7be71-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="7be71-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7be71-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="7be71-219">New cmdlets</span><span class="sxs-lookup"><span data-stu-id="7be71-219">New cmdlets</span></span>
<span data-ttu-id="7be71-220">The following are the new cmdlets that are only available in the ARM mode.</span><span class="sxs-lookup"><span data-stu-id="7be71-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="7be71-221">**Script action related cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="7be71-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="7be71-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span><span class="sxs-lookup"><span data-stu-id="7be71-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="7be71-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span><span class="sxs-lookup"><span data-stu-id="7be71-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="7be71-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7be71-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="7be71-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span><span class="sxs-lookup"><span data-stu-id="7be71-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="7be71-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7be71-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="7be71-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7be71-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="7be71-228">**Clsuter identity related cmdlets:**</span><span class="sxs-lookup"><span data-stu-id="7be71-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="7be71-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span><span class="sxs-lookup"><span data-stu-id="7be71-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="7be71-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7be71-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="7be71-231">Examples</span><span class="sxs-lookup"><span data-stu-id="7be71-231">Examples</span></span>
<span data-ttu-id="7be71-232">**Create cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-232">**Create cluster**</span></span>

<span data-ttu-id="7be71-233">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="7be71-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="7be71-234">New command (ARM):</span><span class="sxs-lookup"><span data-stu-id="7be71-234">New command (ARM):</span></span>

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


<span data-ttu-id="7be71-235">**Delete cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-235">**Delete cluster**</span></span>

<span data-ttu-id="7be71-236">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="7be71-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="7be71-237">New command (ARM):</span><span class="sxs-lookup"><span data-stu-id="7be71-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="7be71-238">**List cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-238">**List cluster**</span></span>

<span data-ttu-id="7be71-239">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="7be71-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="7be71-240">New command (ARM):</span><span class="sxs-lookup"><span data-stu-id="7be71-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="7be71-241">**Show cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-241">**Show cluster**</span></span>

<span data-ttu-id="7be71-242">Old command (ASM):</span><span class="sxs-lookup"><span data-stu-id="7be71-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="7be71-243">New command (ARM):</span><span class="sxs-lookup"><span data-stu-id="7be71-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="7be71-244">Other samples</span><span class="sxs-lookup"><span data-stu-id="7be71-244">Other samples</span></span>
* [<span data-ttu-id="7be71-245">Create HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="7be71-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="7be71-246">Submit Hive jobs</span><span class="sxs-lookup"><span data-stu-id="7be71-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="7be71-247">Submit Pig jobs</span><span class="sxs-lookup"><span data-stu-id="7be71-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="7be71-248">Submit Sqoop jobs</span><span class="sxs-lookup"><span data-stu-id="7be71-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="7be71-249">Migrating to the ARM-based HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="7be71-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span><span class="sxs-lookup"><span data-stu-id="7be71-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="7be71-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="7be71-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="7be71-252">The following ASM-based HDInsight packages are being deprecated.</span><span class="sxs-lookup"><span data-stu-id="7be71-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="7be71-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span><span class="sxs-lookup"><span data-stu-id="7be71-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="7be71-254">How to... using the ARM-based HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="7be71-255">Links</span><span class="sxs-lookup"><span data-stu-id="7be71-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="7be71-256">Create HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7be71-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7be71-258">Customize a cluster using Script Action with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="7be71-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="7be71-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="7be71-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="7be71-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7be71-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="7be71-262">The code snippet in this article uses the interactive authentication approach.</span><span class="sxs-lookup"><span data-stu-id="7be71-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="7be71-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="7be71-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="7be71-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="7be71-265">Submit a Hive job using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="7be71-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7be71-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7be71-267">Submit a Pig job using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="7be71-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7be71-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7be71-269">Submit a Sqoop job using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="7be71-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7be71-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7be71-271">List HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="7be71-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="7be71-273">Scale HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="7be71-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="7be71-275">Grant/revoke access to HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="7be71-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="7be71-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="7be71-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="7be71-279">Find the default storage account for HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="7be71-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="7be71-281">Delete HDInsight clusters using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7be71-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7be71-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="7be71-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="7be71-283">Examples</span><span class="sxs-lookup"><span data-stu-id="7be71-283">Examples</span></span>
<span data-ttu-id="7be71-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span><span class="sxs-lookup"><span data-stu-id="7be71-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="7be71-285">**Creating a cluster CRUD client**</span><span class="sxs-lookup"><span data-stu-id="7be71-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="7be71-286">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="7be71-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="7be71-287">New command (ARM) (Service principal authorization)</span><span class="sxs-lookup"><span data-stu-id="7be71-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="7be71-288">New command (ARM) (User authorization)</span><span class="sxs-lookup"><span data-stu-id="7be71-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="7be71-289">**Creating a cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-289">**Creating a cluster**</span></span>

* <span data-ttu-id="7be71-290">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="7be71-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="7be71-291">New command (ARM)</span><span class="sxs-lookup"><span data-stu-id="7be71-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="7be71-292">**Enabling HTTP access**</span><span class="sxs-lookup"><span data-stu-id="7be71-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="7be71-293">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="7be71-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="7be71-294">New command (ARM)</span><span class="sxs-lookup"><span data-stu-id="7be71-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="7be71-295">**Deleting a cluster**</span><span class="sxs-lookup"><span data-stu-id="7be71-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="7be71-296">Old command (ASM)</span><span class="sxs-lookup"><span data-stu-id="7be71-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="7be71-297">New command (ARM)</span><span class="sxs-lookup"><span data-stu-id="7be71-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

