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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Create and manage an elastic pool with PowerShell
This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.  You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md). You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Create an elastic pool
The [New-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt619378\(v=azure.300\).aspx) cmdlet creates an elastic pool. The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS). See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

    New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Create a pooled database in an elastic pool
Use the [New-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619339\(v=azure.300\).aspx) cmdlet and set the **ElasticPoolName** parameter to the target pool. To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

    New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

### <a name="complete-script"></a>Complete script
This script creates an Azure resource group and a server. When prompted, supply an administrator username and password for the new server (not your Azure credentials).

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Create an elastic pool and add multiple pooled databases
Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time. To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).   

## <a name="move-a-database-into-an-elastic-pool"></a>Move a database into an elastic pool
You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](https://msdn.microsoft.com/library/azure/mt619433\(v=azure.300\).aspx).

    Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

## <a name="change-performance-settings-of-an-elastic-pool"></a>Change performance settings of an elastic pool
When performance suffers, you can change the settings of the pool to accommodate growth. Use the [Set-AzureRmSqlElasticPool](https://msdn.microsoft.com/library/azure/mt603511\(v=azure.300\).aspx) cmdlet. Set the -Dtu parameter to the eDTUs per pool. See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.  

    Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50

## <a name="get-the-status-of-pool-operations"></a>Get the status of pool operations
Creating an elastic pool can take time. To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](https://msdn.microsoft.com/library/azure/mt603812\(v=azure.300\).aspx) cmdlet.

    Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Get the status of moving a database into and out of an elastic pool
Moving a database can take time. Track a move status using the [Get-AzureRmSqlDatabaseActivity](https://msdn.microsoft.com/library/azure/mt603687\(v=azure.300\).aspx) cmdlet.

    Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Get resource usage data for an elastic pool
Metrics that can be retrieved as a percentage of the resource pool limit:   

| Metric name | Description |
|:--- |:--- |
| cpu\_percent |Average compute utilization in percentage of the limit of the pool. |
| physical\_data\_read\_percent |Average I/O utilization in percentage based on the limit of the pool. |
| log\_write\_percent |Average write resource utilization in percentage of the limit of the pool. |
| DTU\_consumption\_percent |Average eDTU utilization in percentage of eDTU limit for the pool |
| storage\_percent |Average storage utilization in percentage of the storage limit of the pool. |
| workers\_percent |Maximum concurrent workers (requests) in percentage based on the limit of the pool. |
| sessions\_percent |Maximum concurrent sessions in percentage based on the limit of the pool. |
| eDTU_limit |Current max elastic pool DTU setting for this elastic pool during this interval. |
| storage\_limit |Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval. |
| eDTU\_used |Average eDTUs used by the pool in this interval. |
| storage\_used |Average storage used by the pool in this interval in bytes |

**Metrics granularity/retention periods:**

* Data is returned at 5-minute granularity.  
* Data retention is 35 days.  

This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity). But this command can be called multiple times with different start/end time intervals to retrieve more data

To retrieve the metrics:

    $metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")  

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Get resource usage data for a database in an elastic pool
These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool. For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.

To retrieve the metrics:

    $metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")

## <a name="add-an-alert-to-an-elastic-pool-resource"></a>Add an alert to an elastic pool resource
You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up. Use the Add-AzureRmMetricAlertRule cmdlet.

> [!IMPORTANT]
> Resource utilization monitoring for elastic pools has a lag of at least 20 minutes. Setting alerts of less than 30 minutes for elastic pools is not currently supported. Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered. Make sure that any alerts you define for elastic pools use a period (WindowSize) of 30 minutes or more.
>
>

This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.

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

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a>Add alerts to all databases in an elastic pool
You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.

> [!IMPORTANT]
> Resource utilization monitoring for elastic pools has a lag of at least 20 minutes. Setting alerts of less than 30 minutes for elastic pools is not currently supported. Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered. Make sure that any alerts you define for elastic pools use a period (WindowSize) of 30 minutes or more.
>
>

This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Collect and monitor resource usage data across multiple pools in a subscription
When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately. Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage. A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.

To use this sample implementation, follow these steps.

1. Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Modify the scripts for your environment. Specify one or more servers on which elastic pools are hosted.
3. Specify a telemetry database where the collected metrics are to be stored.
4. Customize the script to specify the duration of the scripts' execution.

At a high level, the scripts do the following:

* Enumerates all servers in a given Azure subscription (or a specified list of servers).
* Runs a background job for each server. The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server. It then loads the collected data into the specified telemetry database.
* Enumerates a list of databases in each pool to collect the database resource usage data. It then loads the collected data into the telemetry database.

The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it. The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window. For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.” Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Example: retrieve resource consumption metrics for an elastic pool and its databases
This example retrieves the consumption metrics for a given elastic pool and all its databases. Collected data is formatted and written to a .csv formatted file. The file can be browsed with Excel.

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

## <a name="latency-of-elastic-pool-operations"></a>Latency of elastic pool operations
* Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.
* Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool. Changes average 90 minutes or less per 100 GB. For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.

For reference documentation about these PowerShell cmdlets, see:

* [Get-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt603582\(v=azure.300\).aspx)
* [Start-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt619403\(v=azure.300\).aspx)
* [Stop-AzureRMSqlServerUpgrade](https://msdn.microsoft.com/library/azure/mt603589\(v=azure.300\).aspx)

The Stop- cmdlet means cancel, not pause. There is no way to resume an upgrade, other than starting again from the beginning. The Stop- cmdlet cleans up and releases all appropriate resources.

## <a name="next-steps"></a>Next steps
* [Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.
* See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.
