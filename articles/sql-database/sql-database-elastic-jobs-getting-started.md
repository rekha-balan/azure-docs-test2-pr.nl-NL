---
title: Getting started with elastic database jobs | Microsoft Docs
description: how to use elastic database jobs
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 396a95665287211eba326964dd8368a87b1172ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564308"
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="0efb6-103">Getting started with Elastic Database jobs</span><span class="sxs-lookup"><span data-stu-id="0efb6-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="0efb6-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span><span class="sxs-lookup"><span data-stu-id="0efb6-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="0efb6-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0efb6-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="0efb6-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0efb6-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="0efb6-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span><span class="sxs-lookup"><span data-stu-id="0efb6-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="0efb6-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span><span class="sxs-lookup"><span data-stu-id="0efb6-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0efb6-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0efb6-109">Prerequisites</span></span>
<span data-ttu-id="0efb6-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0efb6-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="0efb6-111">Create a shard map manager using the sample app</span><span class="sxs-lookup"><span data-stu-id="0efb6-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="0efb6-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span><span class="sxs-lookup"><span data-stu-id="0efb6-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="0efb6-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span><span class="sxs-lookup"><span data-stu-id="0efb6-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="0efb6-114">Build and run the **Getting started with Elastic Database tools** sample application.</span><span class="sxs-lookup"><span data-stu-id="0efb6-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="0efb6-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="0efb6-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="0efb6-116">At the end of Step 7, you will see the following command prompt:</span><span class="sxs-lookup"><span data-stu-id="0efb6-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![command prompt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="0efb6-118">In the command window, type "1" and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0efb6-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="0efb6-119">This creates the shard map manager, and adds two shards to the server.</span><span class="sxs-lookup"><span data-stu-id="0efb6-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="0efb6-120">Then type "3" and press **Enter**; repeat this action four times.</span><span class="sxs-lookup"><span data-stu-id="0efb6-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="0efb6-121">This inserts sample data rows in your shards.</span><span class="sxs-lookup"><span data-stu-id="0efb6-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="0efb6-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span><span class="sxs-lookup"><span data-stu-id="0efb6-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="0efb6-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span><span class="sxs-lookup"><span data-stu-id="0efb6-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="0efb6-125">This will allow us to create and execute a job that add a new table across shards.</span><span class="sxs-lookup"><span data-stu-id="0efb6-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="0efb6-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0efb6-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="0efb6-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span><span class="sxs-lookup"><span data-stu-id="0efb6-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="0efb6-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span><span class="sxs-lookup"><span data-stu-id="0efb6-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="0efb6-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span><span class="sxs-lookup"><span data-stu-id="0efb6-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="0efb6-130">Create a T-SQL Script for execution across databases</span><span class="sxs-lookup"><span data-stu-id="0efb6-130">Create a T-SQL Script for execution across databases</span></span>
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="0efb6-131">Create the job to execute a script across the custom group of databases</span><span class="sxs-lookup"><span data-stu-id="0efb6-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="0efb6-132">Execute the job</span><span class="sxs-lookup"><span data-stu-id="0efb6-132">Execute the job</span></span>
<span data-ttu-id="0efb6-133">The following PowerShell script can be used to execute an existing job:</span><span class="sxs-lookup"><span data-stu-id="0efb6-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="0efb6-134">Update the following variable to reflect the desired job name to have executed:</span><span class="sxs-lookup"><span data-stu-id="0efb6-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="0efb6-135">Retrieve the state of a single job execution</span><span class="sxs-lookup"><span data-stu-id="0efb6-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="0efb6-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span><span class="sxs-lookup"><span data-stu-id="0efb6-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="0efb6-137">View the state across multiple job executions</span><span class="sxs-lookup"><span data-stu-id="0efb6-137">View the state across multiple job executions</span></span>
<span data-ttu-id="0efb6-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span><span class="sxs-lookup"><span data-stu-id="0efb6-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="0efb6-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="0efb6-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="0efb6-140">Retrieve all active top level job executions:</span><span class="sxs-lookup"><span data-stu-id="0efb6-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="0efb6-141">Retrieve all top level job executions, including inactive job executions:</span><span class="sxs-lookup"><span data-stu-id="0efb6-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="0efb6-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span><span class="sxs-lookup"><span data-stu-id="0efb6-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="0efb6-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span><span class="sxs-lookup"><span data-stu-id="0efb6-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="0efb6-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span><span class="sxs-lookup"><span data-stu-id="0efb6-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="0efb6-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span><span class="sxs-lookup"><span data-stu-id="0efb6-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="0efb6-146">Retrieve the list of job task executions within a specific job execution:</span><span class="sxs-lookup"><span data-stu-id="0efb6-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="0efb6-147">Retrieve job task execution details:</span><span class="sxs-lookup"><span data-stu-id="0efb6-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="0efb6-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span><span class="sxs-lookup"><span data-stu-id="0efb6-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="0efb6-149">Retrieve failures within job task executions</span><span class="sxs-lookup"><span data-stu-id="0efb6-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="0efb6-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span><span class="sxs-lookup"><span data-stu-id="0efb6-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="0efb6-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span><span class="sxs-lookup"><span data-stu-id="0efb6-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="0efb6-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span><span class="sxs-lookup"><span data-stu-id="0efb6-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="0efb6-153">Waiting for a job execution to complete</span><span class="sxs-lookup"><span data-stu-id="0efb6-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="0efb6-154">The following PowerShell script can be used to wait for a job task to complete:</span><span class="sxs-lookup"><span data-stu-id="0efb6-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="0efb6-155">Create a custom execution policy</span><span class="sxs-lookup"><span data-stu-id="0efb6-155">Create a custom execution policy</span></span>
<span data-ttu-id="0efb6-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span><span class="sxs-lookup"><span data-stu-id="0efb6-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="0efb6-157">Execution policies currently allow for defining:</span><span class="sxs-lookup"><span data-stu-id="0efb6-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="0efb6-158">Name: Identifier for the execution policy.</span><span class="sxs-lookup"><span data-stu-id="0efb6-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="0efb6-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span><span class="sxs-lookup"><span data-stu-id="0efb6-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="0efb6-160">Initial Retry Interval: Interval to wait before first retry.</span><span class="sxs-lookup"><span data-stu-id="0efb6-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="0efb6-161">Maximum Retry Interval: Cap of retry intervals to use.</span><span class="sxs-lookup"><span data-stu-id="0efb6-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="0efb6-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span><span class="sxs-lookup"><span data-stu-id="0efb6-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="0efb6-163">The following formula is used: (Initial Retry Interval) \* Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span><span class="sxs-lookup"><span data-stu-id="0efb6-163">The following formula is used: (Initial Retry Interval) \* Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="0efb6-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span><span class="sxs-lookup"><span data-stu-id="0efb6-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="0efb6-165">The default execution policy uses the following values:</span><span class="sxs-lookup"><span data-stu-id="0efb6-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="0efb6-166">Name: Default execution policy</span><span class="sxs-lookup"><span data-stu-id="0efb6-166">Name: Default execution policy</span></span>
* <span data-ttu-id="0efb6-167">Job Timeout: 1 week</span><span class="sxs-lookup"><span data-stu-id="0efb6-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="0efb6-168">Initial Retry Interval:  100 milliseconds</span><span class="sxs-lookup"><span data-stu-id="0efb6-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="0efb6-169">Maximum Retry Interval: 30 minutes</span><span class="sxs-lookup"><span data-stu-id="0efb6-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="0efb6-170">Retry Interval Coefficient: 2</span><span class="sxs-lookup"><span data-stu-id="0efb6-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="0efb6-171">Maximum Attempts: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="0efb6-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="0efb6-172">Create the desired execution policy:</span><span class="sxs-lookup"><span data-stu-id="0efb6-172">Create the desired execution policy:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="0efb6-173">Update a custom execution policy</span><span class="sxs-lookup"><span data-stu-id="0efb6-173">Update a custom execution policy</span></span>
<span data-ttu-id="0efb6-174">Update the desired execution policy to update:</span><span class="sxs-lookup"><span data-stu-id="0efb6-174">Update the desired execution policy to update:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a><span data-ttu-id="0efb6-175">Cancel a job</span><span class="sxs-lookup"><span data-stu-id="0efb6-175">Cancel a job</span></span>
<span data-ttu-id="0efb6-176">Elastic Database Jobs supports jobs cancellation requests.</span><span class="sxs-lookup"><span data-stu-id="0efb6-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="0efb6-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span><span class="sxs-lookup"><span data-stu-id="0efb6-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="0efb6-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span><span class="sxs-lookup"><span data-stu-id="0efb6-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="0efb6-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span><span class="sxs-lookup"><span data-stu-id="0efb6-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="0efb6-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span><span class="sxs-lookup"><span data-stu-id="0efb6-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="0efb6-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span><span class="sxs-lookup"><span data-stu-id="0efb6-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="0efb6-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span><span class="sxs-lookup"><span data-stu-id="0efb6-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="0efb6-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="0efb6-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="0efb6-184">Delete a job by name and the job's history</span><span class="sxs-lookup"><span data-stu-id="0efb6-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="0efb6-185">Elastic Database jobs supports asynchronous deletion of jobs.</span><span class="sxs-lookup"><span data-stu-id="0efb6-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="0efb6-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span><span class="sxs-lookup"><span data-stu-id="0efb6-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="0efb6-187">The system will not automatically cancel active job executions.</span><span class="sxs-lookup"><span data-stu-id="0efb6-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="0efb6-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span><span class="sxs-lookup"><span data-stu-id="0efb6-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="0efb6-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span><span class="sxs-lookup"><span data-stu-id="0efb6-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="0efb6-190">Create a custom database target</span><span class="sxs-lookup"><span data-stu-id="0efb6-190">Create a custom database target</span></span>
<span data-ttu-id="0efb6-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span><span class="sxs-lookup"><span data-stu-id="0efb6-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="0efb6-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="0efb6-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="0efb6-193">Set the following variables to reflect the desired database information:</span><span class="sxs-lookup"><span data-stu-id="0efb6-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="0efb6-194">Create a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="0efb6-194">Create a custom database collection target</span></span>
<span data-ttu-id="0efb6-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span><span class="sxs-lookup"><span data-stu-id="0efb6-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="0efb6-196">After a database group is created, databases can be associated to the custom collection target.</span><span class="sxs-lookup"><span data-stu-id="0efb6-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="0efb6-197">Set the following variables to reflect the desired custom collection target configuration:</span><span class="sxs-lookup"><span data-stu-id="0efb6-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="0efb6-198">Add databases to a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="0efb6-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="0efb6-199">Database targets can be associated with custom database collection targets to create a group of databases.</span><span class="sxs-lookup"><span data-stu-id="0efb6-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="0efb6-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span><span class="sxs-lookup"><span data-stu-id="0efb6-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="0efb6-201">Add the desired database to a specific custom collection:</span><span class="sxs-lookup"><span data-stu-id="0efb6-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="0efb6-202">Review the databases within a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="0efb6-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="0efb6-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span><span class="sxs-lookup"><span data-stu-id="0efb6-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="0efb6-204">Create a job to execute a script across a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="0efb6-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="0efb6-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span><span class="sxs-lookup"><span data-stu-id="0efb6-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="0efb6-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span><span class="sxs-lookup"><span data-stu-id="0efb6-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="0efb6-207">Again, it is important that scripts are idempotent to be resilient to retries.</span><span class="sxs-lookup"><span data-stu-id="0efb6-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="0efb6-208">Data collection across databases</span><span class="sxs-lookup"><span data-stu-id="0efb6-208">Data collection across databases</span></span>
<span data-ttu-id="0efb6-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span><span class="sxs-lookup"><span data-stu-id="0efb6-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="0efb6-210">The table can be queried after the fact to see the query’s results from each database.</span><span class="sxs-lookup"><span data-stu-id="0efb6-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="0efb6-211">This provides an asynchronous mechanism to execute a query across many databases.</span><span class="sxs-lookup"><span data-stu-id="0efb6-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="0efb6-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span><span class="sxs-lookup"><span data-stu-id="0efb6-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="0efb6-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span><span class="sxs-lookup"><span data-stu-id="0efb6-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="0efb6-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span><span class="sxs-lookup"><span data-stu-id="0efb6-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="0efb6-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span><span class="sxs-lookup"><span data-stu-id="0efb6-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="0efb6-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span><span class="sxs-lookup"><span data-stu-id="0efb6-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="0efb6-217">Set the following to reflect the desired script, credentials, and execution target:</span><span class="sxs-lookup"><span data-stu-id="0efb6-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="0efb6-218">Create and start a job for data collection scenarios</span><span class="sxs-lookup"><span data-stu-id="0efb6-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="0efb6-219">Create a schedule for job execution using a job trigger</span><span class="sxs-lookup"><span data-stu-id="0efb6-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="0efb6-220">The following PowerShell script can be used to create a reoccurring schedule.</span><span class="sxs-lookup"><span data-stu-id="0efb6-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="0efb6-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span><span class="sxs-lookup"><span data-stu-id="0efb6-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="0efb6-222">Schedules that execute only once can be created by passing -OneTime.</span><span class="sxs-lookup"><span data-stu-id="0efb6-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="0efb6-223">Create a new schedule:</span><span class="sxs-lookup"><span data-stu-id="0efb6-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="0efb6-224">Create a job trigger to have a job executed on a time schedule</span><span class="sxs-lookup"><span data-stu-id="0efb6-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="0efb6-225">A job trigger can be defined to have a job executed according to a time schedule.</span><span class="sxs-lookup"><span data-stu-id="0efb6-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="0efb6-226">The following PowerShell script can be used to create a job trigger.</span><span class="sxs-lookup"><span data-stu-id="0efb6-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="0efb6-227">Set the following variables to correspond to the desired job and schedule:</span><span class="sxs-lookup"><span data-stu-id="0efb6-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="0efb6-228">Remove a scheduled association to stop job from executing on schedule</span><span class="sxs-lookup"><span data-stu-id="0efb6-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="0efb6-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span><span class="sxs-lookup"><span data-stu-id="0efb6-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="0efb6-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0efb6-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="0efb6-231">Import elastic database query results to Excel</span><span class="sxs-lookup"><span data-stu-id="0efb6-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="0efb6-232">You can import the results from of a query to an Excel file.</span><span class="sxs-lookup"><span data-stu-id="0efb6-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="0efb6-233">Launch Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="0efb6-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="0efb6-234">Navigate to the **Data** ribbon.</span><span class="sxs-lookup"><span data-stu-id="0efb6-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="0efb6-235">Click **From Other Sources** and click **From SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0efb6-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel import from other sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="0efb6-237">In the **Data Connection Wizard** type the server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="0efb6-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="0efb6-238">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0efb6-238">Then click **Next**.</span></span>
5. <span data-ttu-id="0efb6-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="0efb6-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="0efb6-240">Select the **Customers** table in the list view and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0efb6-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="0efb6-241">Then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="0efb6-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="0efb6-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0efb6-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="0efb6-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span><span class="sxs-lookup"><span data-stu-id="0efb6-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0efb6-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="0efb6-244">Next steps</span></span>
<span data-ttu-id="0efb6-245">You can now use Excel’s data functions.</span><span class="sxs-lookup"><span data-stu-id="0efb6-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="0efb6-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span><span class="sxs-lookup"><span data-stu-id="0efb6-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="0efb6-247">Make sure that SQL Server is supported as a data source for your tool.</span><span class="sxs-lookup"><span data-stu-id="0efb6-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="0efb6-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span><span class="sxs-lookup"><span data-stu-id="0efb6-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="0efb6-249">Cost</span><span class="sxs-lookup"><span data-stu-id="0efb6-249">Cost</span></span>
<span data-ttu-id="0efb6-250">There is no additional charge for using the Elastic Database query feature.</span><span class="sxs-lookup"><span data-stu-id="0efb6-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="0efb6-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span><span class="sxs-lookup"><span data-stu-id="0efb6-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="0efb6-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0efb6-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/portal.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/tiers.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/details.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->








