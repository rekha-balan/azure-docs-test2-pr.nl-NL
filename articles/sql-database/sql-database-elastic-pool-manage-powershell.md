---
title: 'PowerShell: Create & manage an Azure SQL elastic pool | Microsoft Docs'
description: Learn how to use PowerShell to manage an elastic pool.
services: sql-database
documentationcenter: ''
author: srinia
manager: jhubbard
editor: ''
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: multiple databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/22/2016
ms.author: srinia
ms.openlocfilehash: 7ab1d760d26aac7fc185b0e9f5e4a7a47cc2eee5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550198"
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="43bd1-103">Create and manage an elastic pool with PowerShell</span><span class="sxs-lookup"><span data-stu-id="43bd1-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="43bd1-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43bd1-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="43bd1-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="43bd1-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="43bd1-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="43bd1-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="43bd1-107">Create an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-107">Create an elastic pool</span></span>
<span data-ttu-id="43bd1-108">The [New-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt619378\(v=azure.300\).aspx) cmdlet creates an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-108">The [New-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt619378\(v=azure.300\).aspx) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="43bd1-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span><span class="sxs-lookup"><span data-stu-id="43bd1-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="43bd1-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="43bd1-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

    New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="43bd1-111">Create a pooled database in an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="43bd1-112">Use the [New-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619339\(v=azure.300\).aspx) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-112">Use the [New-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619339\(v=azure.300\).aspx) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="43bd1-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="43bd1-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

    New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

### <a name="complete-script"></a><span data-ttu-id="43bd1-114">Complete script</span><span class="sxs-lookup"><span data-stu-id="43bd1-114">Complete script</span></span>
<span data-ttu-id="43bd1-115">This script creates an Azure resource group and a server.</span><span class="sxs-lookup"><span data-stu-id="43bd1-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="43bd1-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span><span class="sxs-lookup"><span data-stu-id="43bd1-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

    $subscriptionId = '<your Azure subscription id>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $serverName = '<server name>'
    $poolName = '<pool name>'
    $databaseName = '<database name>'

    Login-AzureRmAccount
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
    New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

    New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

    New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="43bd1-117">Create an elastic pool and add multiple pooled databases</span><span class="sxs-lookup"><span data-stu-id="43bd1-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="43bd1-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span><span class="sxs-lookup"><span data-stu-id="43bd1-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="43bd1-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="43bd1-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>   

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="43bd1-120">Move a database into an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="43bd1-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619433\(v=azure.300\).aspx).</span><span class="sxs-lookup"><span data-stu-id="43bd1-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619433\(v=azure.300\).aspx).</span></span>

    Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="43bd1-122">Change performance settings of an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="43bd1-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span><span class="sxs-lookup"><span data-stu-id="43bd1-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="43bd1-124">Use the [Set-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt603511\(v=azure.300\).aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="43bd1-124">Use the [Set-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt603511\(v=azure.300\).aspx) cmdlet.</span></span> <span data-ttu-id="43bd1-125">Set the -Dtu parameter to the eDTUs per pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="43bd1-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span><span class="sxs-lookup"><span data-stu-id="43bd1-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>  

    Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="43bd1-127">Get the status of pool operations</span><span class="sxs-lookup"><span data-stu-id="43bd1-127">Get the status of pool operations</span></span>
<span data-ttu-id="43bd1-128">Creating an elastic pool can take time.</span><span class="sxs-lookup"><span data-stu-id="43bd1-128">Creating an elastic pool can take time.</span></span> <span data-ttu-id="43bd1-129">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](https://msdn.microsoft.com/library/azure/mt603812\(v=azure.300\).aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="43bd1-129">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](https://msdn.microsoft.com/library/azure/mt603812\(v=azure.300\).aspx) cmdlet.</span></span>

    Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="43bd1-130">Get the status of moving a database into and out of an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-130">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="43bd1-131">Moving a database can take time.</span><span class="sxs-lookup"><span data-stu-id="43bd1-131">Moving a database can take time.</span></span> <span data-ttu-id="43bd1-132">Track a move status using the [Get-AzureRmSqlDatabaseActivity](https://msdn.microsoft.com/library/azure/mt603687\(v=azure.300\).aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="43bd1-132">Track a move status using the [Get-AzureRmSqlDatabaseActivity](https://msdn.microsoft.com/library/azure/mt603687\(v=azure.300\).aspx) cmdlet.</span></span>

    Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="43bd1-133">Get resource usage data for an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-133">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="43bd1-134">Metrics that can be retrieved as a percentage of the resource pool limit:</span><span class="sxs-lookup"><span data-stu-id="43bd1-134">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>   

| <span data-ttu-id="43bd1-135">Metric name</span><span class="sxs-lookup"><span data-stu-id="43bd1-135">Metric name</span></span> | <span data-ttu-id="43bd1-136">Description</span><span class="sxs-lookup"><span data-stu-id="43bd1-136">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="43bd1-137">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-137">cpu\_percent</span></span> |<span data-ttu-id="43bd1-138">Average compute utilization in percentage of the limit of the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-138">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="43bd1-139">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-139">physical\_data\_read\_percent</span></span> |<span data-ttu-id="43bd1-140">Average I/O utilization in percentage based on the limit of the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-140">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="43bd1-141">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-141">log\_write\_percent</span></span> |<span data-ttu-id="43bd1-142">Average write resource utilization in percentage of the limit of the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-142">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="43bd1-143">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-143">DTU\_consumption\_percent</span></span> |<span data-ttu-id="43bd1-144">Average eDTU utilization in percentage of eDTU limit for the pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-144">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="43bd1-145">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-145">storage\_percent</span></span> |<span data-ttu-id="43bd1-146">Average storage utilization in percentage of the storage limit of the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-146">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="43bd1-147">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-147">workers\_percent</span></span> |<span data-ttu-id="43bd1-148">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-148">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="43bd1-149">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="43bd1-149">sessions\_percent</span></span> |<span data-ttu-id="43bd1-150">Maximum concurrent sessions in percentage based on the limit of the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-150">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="43bd1-151">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="43bd1-151">eDTU_limit</span></span> |<span data-ttu-id="43bd1-152">Current max elastic pool DTU setting for this elastic pool during this interval.</span><span class="sxs-lookup"><span data-stu-id="43bd1-152">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="43bd1-153">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="43bd1-153">storage\_limit</span></span> |<span data-ttu-id="43bd1-154">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span><span class="sxs-lookup"><span data-stu-id="43bd1-154">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="43bd1-155">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="43bd1-155">eDTU\_used</span></span> |<span data-ttu-id="43bd1-156">Average eDTUs used by the pool in this interval.</span><span class="sxs-lookup"><span data-stu-id="43bd1-156">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="43bd1-157">storage\_used</span><span class="sxs-lookup"><span data-stu-id="43bd1-157">storage\_used</span></span> |<span data-ttu-id="43bd1-158">Average storage used by the pool in this interval in bytes</span><span class="sxs-lookup"><span data-stu-id="43bd1-158">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="43bd1-159">**Metrics granularity/retention periods:**</span><span class="sxs-lookup"><span data-stu-id="43bd1-159">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="43bd1-160">Data is returned at 5-minute granularity.</span><span class="sxs-lookup"><span data-stu-id="43bd1-160">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="43bd1-161">Data retention is 35 days.</span><span class="sxs-lookup"><span data-stu-id="43bd1-161">Data retention is 35 days.</span></span>  

<span data-ttu-id="43bd1-162">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span><span class="sxs-lookup"><span data-stu-id="43bd1-162">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="43bd1-163">But this command can be called multiple times with different start/end time intervals to retrieve more data</span><span class="sxs-lookup"><span data-stu-id="43bd1-163">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="43bd1-164">To retrieve the metrics:</span><span class="sxs-lookup"><span data-stu-id="43bd1-164">To retrieve the metrics:</span></span>

    $metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")  

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="43bd1-165">Get resource usage data for a database in an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-165">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="43bd1-166">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-166">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="43bd1-167">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-167">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="43bd1-168">To retrieve the metrics:</span><span class="sxs-lookup"><span data-stu-id="43bd1-168">To retrieve the metrics:</span></span>

    $metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="43bd1-169">Add an alert to an elastic pool resource</span><span class="sxs-lookup"><span data-stu-id="43bd1-169">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="43bd1-170">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span><span class="sxs-lookup"><span data-stu-id="43bd1-170">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="43bd1-171">Use the Add-AzureRmMetricAlertRule cmdlet.</span><span class="sxs-lookup"><span data-stu-id="43bd1-171">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43bd1-172">Resource utilization monitoring for elastic pools has a lag of at least 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="43bd1-172">Resource utilization monitoring for elastic pools has a lag of at least 20 minutes.</span></span> <span data-ttu-id="43bd1-173">Setting alerts of less than 30 minutes for elastic pools is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="43bd1-173">Setting alerts of less than 30 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="43bd1-174">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered.</span><span class="sxs-lookup"><span data-stu-id="43bd1-174">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered.</span></span> <span data-ttu-id="43bd1-175">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 30 minutes or more.</span><span class="sxs-lookup"><span data-stu-id="43bd1-175">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 30 minutes or more.</span></span>
>
>

<span data-ttu-id="43bd1-176">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span><span class="sxs-lookup"><span data-stu-id="43bd1-176">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

    # Set up your resource ID configurations
    $subscriptionId = '<Azure subscription id>'      # Azure subscription ID
    $location =  '<location'                         # Azure region
    $resourceGroupName = '<resource group name>'     # Resource Group
    $serverName = '<server name>'                    # server name
    $poolName = '<elastic pool name>'                # pool name

    #$Target Resource ID
    $ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

    # Create an email action
    $actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

    # create a unique rule name
    $alertName = $poolName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="43bd1-177">Add alerts to all databases in an elastic pool</span><span class="sxs-lookup"><span data-stu-id="43bd1-177">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="43bd1-178">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span><span class="sxs-lookup"><span data-stu-id="43bd1-178">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43bd1-179">Resource utilization monitoring for elastic pools has a lag of at least 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="43bd1-179">Resource utilization monitoring for elastic pools has a lag of at least 20 minutes.</span></span> <span data-ttu-id="43bd1-180">Setting alerts of less than 30 minutes for elastic pools is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="43bd1-180">Setting alerts of less than 30 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="43bd1-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered.</span><span class="sxs-lookup"><span data-stu-id="43bd1-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered.</span></span> <span data-ttu-id="43bd1-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 30 minutes or more.</span><span class="sxs-lookup"><span data-stu-id="43bd1-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 30 minutes or more.</span></span>
>
>

<span data-ttu-id="43bd1-183">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span><span class="sxs-lookup"><span data-stu-id="43bd1-183">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

    # Set up your resource ID configurations
    $subscriptionId = '<Azure subscription id>'      # Azure subscription ID
    $location = '<location'                          # Azure region
    $resourceGroupName = '<resource group name>'     # Resource Group
    $serverName = '<server name>'                    # server name
    $poolName = '<elastic pool name>'                # pool name

    # Get the list of databases in this pool.
    $dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

    # Create an email action
    $actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

    # Get resource usage metrics for a database in an elastic pool for the specified time interval.
    foreach ($db in $dbList)
    {
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
    }

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="43bd1-184">Collect and monitor resource usage data across multiple pools in a subscription</span><span class="sxs-lookup"><span data-stu-id="43bd1-184">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="43bd1-185">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span><span class="sxs-lookup"><span data-stu-id="43bd1-185">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="43bd1-186">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span><span class="sxs-lookup"><span data-stu-id="43bd1-186">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="43bd1-187">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span><span class="sxs-lookup"><span data-stu-id="43bd1-187">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="43bd1-188">To use this sample implementation, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="43bd1-188">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="43bd1-189">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="43bd1-189">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="43bd1-190">Modify the scripts for your environment.</span><span class="sxs-lookup"><span data-stu-id="43bd1-190">Modify the scripts for your environment.</span></span> <span data-ttu-id="43bd1-191">Specify one or more servers on which elastic pools are hosted.</span><span class="sxs-lookup"><span data-stu-id="43bd1-191">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="43bd1-192">Specify a telemetry database where the collected metrics are to be stored.</span><span class="sxs-lookup"><span data-stu-id="43bd1-192">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="43bd1-193">Customize the script to specify the duration of the scripts' execution.</span><span class="sxs-lookup"><span data-stu-id="43bd1-193">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="43bd1-194">At a high level, the scripts do the following:</span><span class="sxs-lookup"><span data-stu-id="43bd1-194">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="43bd1-195">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span><span class="sxs-lookup"><span data-stu-id="43bd1-195">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="43bd1-196">Runs a background job for each server.</span><span class="sxs-lookup"><span data-stu-id="43bd1-196">Runs a background job for each server.</span></span> <span data-ttu-id="43bd1-197">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span><span class="sxs-lookup"><span data-stu-id="43bd1-197">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="43bd1-198">It then loads the collected data into the specified telemetry database.</span><span class="sxs-lookup"><span data-stu-id="43bd1-198">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="43bd1-199">Enumerates a list of databases in each pool to collect the database resource usage data.</span><span class="sxs-lookup"><span data-stu-id="43bd1-199">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="43bd1-200">It then loads the collected data into the telemetry database.</span><span class="sxs-lookup"><span data-stu-id="43bd1-200">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="43bd1-201">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span><span class="sxs-lookup"><span data-stu-id="43bd1-201">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="43bd1-202">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span><span class="sxs-lookup"><span data-stu-id="43bd1-202">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="43bd1-203">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span><span class="sxs-lookup"><span data-stu-id="43bd1-203">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="43bd1-204">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span><span class="sxs-lookup"><span data-stu-id="43bd1-204">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="43bd1-205">Example: retrieve resource consumption metrics for an elastic pool and its databases</span><span class="sxs-lookup"><span data-stu-id="43bd1-205">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="43bd1-206">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span><span class="sxs-lookup"><span data-stu-id="43bd1-206">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="43bd1-207">Collected data is formatted and written to a .csv formatted file.</span><span class="sxs-lookup"><span data-stu-id="43bd1-207">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="43bd1-208">The file can be browsed with Excel.</span><span class="sxs-lookup"><span data-stu-id="43bd1-208">The file can be browsed with Excel.</span></span>

    $subscriptionId = '<Azure subscription id>'          # Azure subscription ID
    $resourceGroupName = '<resource group name>'             # Resource Group
    $serverName = <server name>                              # server name
    $poolName = <elastic pool name>                          # pool name

    # Login to Azure account and select the subscription.
    Login-AzureRmAccount
    Set-AzureRmContext -SubscriptionId $subscriptionId

    # Get resource usage metrics for an elastic pool for the specified time interval.
    $startTime = '4/27/2016 00:00:00'  # start time in UTC
    $endTime = '4/27/2016 01:00:00'    # end time in UTC

    # Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
    $poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
    $poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

    # Get the list of databases in this pool.
    $dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

    # Get resource usage metrics for a database in an elastic pool for the specified time interval.
    $dbMetrics = @()
    foreach ($db in $dbList)
    {
        $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
        $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
    }

    #Optionally you can format the metrics and output as .csv file using the following script block.
    $command = {
    param($metricList, $outputFile)

    # Format metrics into a table.
    $table = @()
    foreach($metric in $metricList) {
      foreach($metricValue in $metric.MetricValues) {
        $sx = New-Object PSObject -Property @{
            Timestamp = $metricValue.Timestamp.ToString()
            MetricName = $metric.Name;
            Average = $metricValue.Average;
            ResourceID = $metric.ResourceId
          }
          $table = $table += $sx
      }
    }

    # Output the metrics into a .csv file.
    write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
    }

    # Format and output pool metrics
    Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

    # Format and output database metrics
    Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="43bd1-209">Latency of elastic pool operations</span><span class="sxs-lookup"><span data-stu-id="43bd1-209">Latency of elastic pool operations</span></span>
* <span data-ttu-id="43bd1-210">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span><span class="sxs-lookup"><span data-stu-id="43bd1-210">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="43bd1-211">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-211">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="43bd1-212">Changes average 90 minutes or less per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="43bd1-212">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="43bd1-213">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span><span class="sxs-lookup"><span data-stu-id="43bd1-213">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

<span data-ttu-id="43bd1-214">For reference documentation about these PowerShell cmdlets, see:</span><span class="sxs-lookup"><span data-stu-id="43bd1-214">For reference documentation about these PowerShell cmdlets, see:</span></span>

* <span data-ttu-id="43bd1-215">[Get-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt603582\(v=azure.300\).aspx)</span><span class="sxs-lookup"><span data-stu-id="43bd1-215">[Get-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt603582\(v=azure.300\).aspx)</span></span>
* <span data-ttu-id="43bd1-216">[Start-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt619403\(v=azure.300\).aspx)</span><span class="sxs-lookup"><span data-stu-id="43bd1-216">[Start-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt619403\(v=azure.300\).aspx)</span></span>
* <span data-ttu-id="43bd1-217">[Stop-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt603589\(v=azure.300\).aspx)</span><span class="sxs-lookup"><span data-stu-id="43bd1-217">[Stop-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt603589\(v=azure.300\).aspx)</span></span>

<span data-ttu-id="43bd1-218">The Stop- cmdlet means cancel, not pause.</span><span class="sxs-lookup"><span data-stu-id="43bd1-218">The Stop- cmdlet means cancel, not pause.</span></span> <span data-ttu-id="43bd1-219">There is no way to resume an upgrade, other than starting again from the beginning.</span><span class="sxs-lookup"><span data-stu-id="43bd1-219">There is no way to resume an upgrade, other than starting again from the beginning.</span></span> <span data-ttu-id="43bd1-220">The Stop- cmdlet cleans up and releases all appropriate resources.</span><span class="sxs-lookup"><span data-stu-id="43bd1-220">The Stop- cmdlet cleans up and releases all appropriate resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43bd1-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="43bd1-221">Next steps</span></span>
* <span data-ttu-id="43bd1-222">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="43bd1-222">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="43bd1-223">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span><span class="sxs-lookup"><span data-stu-id="43bd1-223">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
