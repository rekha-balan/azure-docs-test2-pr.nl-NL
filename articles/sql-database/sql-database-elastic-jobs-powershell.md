---
title: Create and manage elastic jobs using PowerShell | Microsoft Docs
description: PowerShell used to manage Azure SQL Database pools
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 5a448627f2794b82a93a60bdfb55b70d8a7c64a0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549225"
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="3b877-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span><span class="sxs-lookup"><span data-stu-id="3b877-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="3b877-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span><span class="sxs-lookup"><span data-stu-id="3b877-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="3b877-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3b877-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="3b877-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b877-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3b877-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b877-107">Prerequisites</span></span>
* <span data-ttu-id="3b877-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3b877-108">An Azure subscription.</span></span> <span data-ttu-id="3b877-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b877-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3b877-110">A set of databases created with the Elastic Database tools.</span><span class="sxs-lookup"><span data-stu-id="3b877-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="3b877-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b877-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="3b877-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b877-112">Azure PowerShell.</span></span> <span data-ttu-id="3b877-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="3b877-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="3b877-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="3b877-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="3b877-115">Select your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="3b877-115">Select your Azure subscription</span></span>
<span data-ttu-id="3b877-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="3b877-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="3b877-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span><span class="sxs-lookup"><span data-stu-id="3b877-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="3b877-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span><span class="sxs-lookup"><span data-stu-id="3b877-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="3b877-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="3b877-120">Elastic Database jobs objects</span><span class="sxs-lookup"><span data-stu-id="3b877-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="3b877-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span><span class="sxs-lookup"><span data-stu-id="3b877-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="3b877-122">Object Type</span><span class="sxs-lookup"><span data-stu-id="3b877-122">Object Type</span></span></th>
    <th><span data-ttu-id="3b877-123">Description</span><span class="sxs-lookup"><span data-stu-id="3b877-123">Description</span></span></th>
    <th><span data-ttu-id="3b877-124">Related PowerShell APIs</span><span class="sxs-lookup"><span data-stu-id="3b877-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="3b877-125">Credential</span><span class="sxs-lookup"><span data-stu-id="3b877-125">Credential</span></span></td>
    <td><span data-ttu-id="3b877-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span><span class="sxs-lookup"><span data-stu-id="3b877-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="3b877-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span><span class="sxs-lookup"><span data-stu-id="3b877-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="3b877-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span><span class="sxs-lookup"><span data-stu-id="3b877-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="3b877-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="3b877-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="3b877-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="3b877-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="3b877-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="3b877-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="3b877-132">Script</span><span class="sxs-lookup"><span data-stu-id="3b877-132">Script</span></span></td>
    <td><span data-ttu-id="3b877-133">Transact-SQL script to be used for execution across databases.</span><span class="sxs-lookup"><span data-stu-id="3b877-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="3b877-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span><span class="sxs-lookup"><span data-stu-id="3b877-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="3b877-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="3b877-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="3b877-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="3b877-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="3b877-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="3b877-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="3b877-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="3b877-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="3b877-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="3b877-139">DACPAC</span></span></td>
    <td><span data-ttu-id="3b877-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span><span class="sxs-lookup"><span data-stu-id="3b877-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="3b877-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="3b877-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="3b877-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="3b877-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="3b877-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="3b877-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="3b877-144">Database Target</span><span class="sxs-lookup"><span data-stu-id="3b877-144">Database Target</span></span></td>
    <td><span data-ttu-id="3b877-145">Database and server name pointing to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3b877-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="3b877-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="3b877-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="3b877-148">Shard Map Target</span><span class="sxs-lookup"><span data-stu-id="3b877-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="3b877-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span><span class="sxs-lookup"><span data-stu-id="3b877-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="3b877-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="3b877-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="3b877-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="3b877-153">Custom Collection Target</span><span class="sxs-lookup"><span data-stu-id="3b877-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="3b877-154">Defined group of databases to collectively use for execution.</span><span class="sxs-lookup"><span data-stu-id="3b877-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="3b877-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="3b877-157">Custom Collection Child Target</span><span class="sxs-lookup"><span data-stu-id="3b877-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="3b877-158">Database target that is referenced from a custom collection.</span><span class="sxs-lookup"><span data-stu-id="3b877-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="3b877-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="3b877-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="3b877-161">Job</span><span class="sxs-lookup"><span data-stu-id="3b877-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span><span class="sxs-lookup"><span data-stu-id="3b877-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="3b877-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="3b877-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="3b877-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="3b877-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="3b877-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="3b877-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="3b877-166">Job Execution</span><span class="sxs-lookup"><span data-stu-id="3b877-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span><span class="sxs-lookup"><span data-stu-id="3b877-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="3b877-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="3b877-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="3b877-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="3b877-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="3b877-172">Job Task Execution</span><span class="sxs-lookup"><span data-stu-id="3b877-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-173">Single unit of work to fulfill a job.</span><span class="sxs-lookup"><span data-stu-id="3b877-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="3b877-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span><span class="sxs-lookup"><span data-stu-id="3b877-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="3b877-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="3b877-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="3b877-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="3b877-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="3b877-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="3b877-179">Job Execution Policy</span><span class="sxs-lookup"><span data-stu-id="3b877-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-180">Controls job execution timeouts, retry limits and intervals between retries.</span><span class="sxs-lookup"><span data-stu-id="3b877-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="3b877-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span><span class="sxs-lookup"><span data-stu-id="3b877-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="3b877-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="3b877-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="3b877-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="3b877-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="3b877-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="3b877-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="3b877-185">Schedule</span><span class="sxs-lookup"><span data-stu-id="3b877-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span><span class="sxs-lookup"><span data-stu-id="3b877-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="3b877-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="3b877-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="3b877-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="3b877-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="3b877-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="3b877-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="3b877-190">Job Triggers</span><span class="sxs-lookup"><span data-stu-id="3b877-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="3b877-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span><span class="sxs-lookup"><span data-stu-id="3b877-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="3b877-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="3b877-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="3b877-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="3b877-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="3b877-194">Supported Elastic Database jobs group types</span><span class="sxs-lookup"><span data-stu-id="3b877-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="3b877-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span><span class="sxs-lookup"><span data-stu-id="3b877-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="3b877-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span><span class="sxs-lookup"><span data-stu-id="3b877-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="3b877-197">There are two types of groups that you can create:</span><span class="sxs-lookup"><span data-stu-id="3b877-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="3b877-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span><span class="sxs-lookup"><span data-stu-id="3b877-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="3b877-199">Custom Collection group: A custom defined set of databases.</span><span class="sxs-lookup"><span data-stu-id="3b877-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="3b877-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span><span class="sxs-lookup"><span data-stu-id="3b877-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="3b877-201">To set the Elastic Database jobs connection</span><span class="sxs-lookup"><span data-stu-id="3b877-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="3b877-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span><span class="sxs-lookup"><span data-stu-id="3b877-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="3b877-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="3b877-204">All examples provided within this topic assume that this first step has already been performed.</span><span class="sxs-lookup"><span data-stu-id="3b877-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="3b877-205">Open a connection to the Elastic Database jobs:</span><span class="sxs-lookup"><span data-stu-id="3b877-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="3b877-206">Encrypted credentials within the Elastic Database jobs</span><span class="sxs-lookup"><span data-stu-id="3b877-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="3b877-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span><span class="sxs-lookup"><span data-stu-id="3b877-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="3b877-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span><span class="sxs-lookup"><span data-stu-id="3b877-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="3b877-209">Encryption works through a certificate created as part of the installation script.</span><span class="sxs-lookup"><span data-stu-id="3b877-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="3b877-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span><span class="sxs-lookup"><span data-stu-id="3b877-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="3b877-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span><span class="sxs-lookup"><span data-stu-id="3b877-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="3b877-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span><span class="sxs-lookup"><span data-stu-id="3b877-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="3b877-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span><span class="sxs-lookup"><span data-stu-id="3b877-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="3b877-214">Credentials are designed to be reused across job executions.</span><span class="sxs-lookup"><span data-stu-id="3b877-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="3b877-215">Credentials are passed to target databases when establishing connections.</span><span class="sxs-lookup"><span data-stu-id="3b877-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="3b877-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span><span class="sxs-lookup"><span data-stu-id="3b877-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="3b877-217">The user could subsequently start a job targeting this database to gain the credential's password.</span><span class="sxs-lookup"><span data-stu-id="3b877-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="3b877-218">Security best practices for Elastic Database jobs include:</span><span class="sxs-lookup"><span data-stu-id="3b877-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="3b877-219">Limit usage of the APIs to trusted individuals.</span><span class="sxs-lookup"><span data-stu-id="3b877-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="3b877-220">Credentials should have the least privileges necessary to perform the job task.</span><span class="sxs-lookup"><span data-stu-id="3b877-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="3b877-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span><span class="sxs-lookup"><span data-stu-id="3b877-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="3b877-222">To create an encrypted credential for job execution across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="3b877-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](https://msdn.microsoft.com/library/mt346063.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b877-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](https://msdn.microsoft.com/library/mt346063.aspx).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="3b877-224">To update credentials</span><span class="sxs-lookup"><span data-stu-id="3b877-224">To update credentials</span></span>
<span data-ttu-id="3b877-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](https://msdn.microsoft.com/library/mt346062.aspx) and set the **CredentialName** parameter.</span><span class="sxs-lookup"><span data-stu-id="3b877-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](https://msdn.microsoft.com/library/mt346062.aspx) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="3b877-226">To define an Elastic Database shard map target</span><span class="sxs-lookup"><span data-stu-id="3b877-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="3b877-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span><span class="sxs-lookup"><span data-stu-id="3b877-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="3b877-228">This example requires a sharded application created using the Elastic Database client library.</span><span class="sxs-lookup"><span data-stu-id="3b877-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="3b877-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b877-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="3b877-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span><span class="sxs-lookup"><span data-stu-id="3b877-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="3b877-231">Create a T-SQL Script for execution across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="3b877-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span><span class="sxs-lookup"><span data-stu-id="3b877-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="3b877-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span><span class="sxs-lookup"><span data-stu-id="3b877-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="3b877-234">Use the [**New-AzureSqlJobContent cmdlet**](https://msdn.microsoft.com/library/mt346085.aspx) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span><span class="sxs-lookup"><span data-stu-id="3b877-234">Use the [**New-AzureSqlJobContent cmdlet**](https://msdn.microsoft.com/library/mt346085.aspx) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="3b877-235">Create a new script from a file</span><span class="sxs-lookup"><span data-stu-id="3b877-235">Create a new script from a file</span></span>
<span data-ttu-id="3b877-236">If the T-SQL script is defined within a file, use this to import the script:</span><span class="sxs-lookup"><span data-stu-id="3b877-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="3b877-237">To update a T-SQL script for execution across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="3b877-238">This PowerShell script updates the T-SQL command text for an existing script.</span><span class="sxs-lookup"><span data-stu-id="3b877-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="3b877-239">Set the following variables to reflect the desired script definition to be set:</span><span class="sxs-lookup"><span data-stu-id="3b877-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="3b877-240">To update the definition to an existing script</span><span class="sxs-lookup"><span data-stu-id="3b877-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="3b877-241">To create a job to execute a script across a shard map</span><span class="sxs-lookup"><span data-stu-id="3b877-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="3b877-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span><span class="sxs-lookup"><span data-stu-id="3b877-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="3b877-243">Set the following variables to reflect the desired script and target:</span><span class="sxs-lookup"><span data-stu-id="3b877-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="3b877-244">To execute a job</span><span class="sxs-lookup"><span data-stu-id="3b877-244">To execute a job</span></span>
<span data-ttu-id="3b877-245">This PowerShell script executes an existing job:</span><span class="sxs-lookup"><span data-stu-id="3b877-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="3b877-246">Update the following variable to reflect the desired job name to have executed:</span><span class="sxs-lookup"><span data-stu-id="3b877-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="3b877-247">To retrieve the state of a single job execution</span><span class="sxs-lookup"><span data-stu-id="3b877-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="3b877-248">Use the [**Get-AzureSqlJobExecution cmdlet**](https://msdn.microsoft.com/library/mt346058.aspx) and set the **JobExecutionId** parameter to view the state of job execution.</span><span class="sxs-lookup"><span data-stu-id="3b877-248">Use the [**Get-AzureSqlJobExecution cmdlet**](https://msdn.microsoft.com/library/mt346058.aspx) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="3b877-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span><span class="sxs-lookup"><span data-stu-id="3b877-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="3b877-250">To view the state across multiple job executions</span><span class="sxs-lookup"><span data-stu-id="3b877-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="3b877-251">The [**Get-AzureSqlJobExecution cmdlet**](https://msdn.microsoft.com/library/mt346058.aspx) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span><span class="sxs-lookup"><span data-stu-id="3b877-251">The [**Get-AzureSqlJobExecution cmdlet**](https://msdn.microsoft.com/library/mt346058.aspx) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="3b877-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="3b877-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="3b877-253">Retrieve all active top level job executions:</span><span class="sxs-lookup"><span data-stu-id="3b877-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="3b877-254">Retrieve all top level job executions, including inactive job executions:</span><span class="sxs-lookup"><span data-stu-id="3b877-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="3b877-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span><span class="sxs-lookup"><span data-stu-id="3b877-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="3b877-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span><span class="sxs-lookup"><span data-stu-id="3b877-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="3b877-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span><span class="sxs-lookup"><span data-stu-id="3b877-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="3b877-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span><span class="sxs-lookup"><span data-stu-id="3b877-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="3b877-259">Retrieve the list of job task executions within a specific job execution:</span><span class="sxs-lookup"><span data-stu-id="3b877-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="3b877-260">Retrieve job task execution details:</span><span class="sxs-lookup"><span data-stu-id="3b877-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="3b877-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span><span class="sxs-lookup"><span data-stu-id="3b877-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="3b877-262">To retrieve failures within job task executions</span><span class="sxs-lookup"><span data-stu-id="3b877-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="3b877-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span><span class="sxs-lookup"><span data-stu-id="3b877-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="3b877-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span><span class="sxs-lookup"><span data-stu-id="3b877-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="3b877-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span><span class="sxs-lookup"><span data-stu-id="3b877-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="3b877-266">To wait for a job execution to complete</span><span class="sxs-lookup"><span data-stu-id="3b877-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="3b877-267">The following PowerShell script can be used to wait for a job task to complete:</span><span class="sxs-lookup"><span data-stu-id="3b877-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="3b877-268">Create a custom execution policy</span><span class="sxs-lookup"><span data-stu-id="3b877-268">Create a custom execution policy</span></span>
<span data-ttu-id="3b877-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="3b877-270">Execution policies currently allow for defining:</span><span class="sxs-lookup"><span data-stu-id="3b877-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="3b877-271">Name: Identifier for the execution policy.</span><span class="sxs-lookup"><span data-stu-id="3b877-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="3b877-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="3b877-273">Initial Retry Interval: Interval to wait before first retry.</span><span class="sxs-lookup"><span data-stu-id="3b877-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="3b877-274">Maximum Retry Interval: Cap of retry intervals to use.</span><span class="sxs-lookup"><span data-stu-id="3b877-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="3b877-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span><span class="sxs-lookup"><span data-stu-id="3b877-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="3b877-276">The following formula is used: (Initial Retry Interval) \* Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span><span class="sxs-lookup"><span data-stu-id="3b877-276">The following formula is used: (Initial Retry Interval) \* Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="3b877-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span><span class="sxs-lookup"><span data-stu-id="3b877-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="3b877-278">The default execution policy uses the following values:</span><span class="sxs-lookup"><span data-stu-id="3b877-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="3b877-279">Name: Default execution policy</span><span class="sxs-lookup"><span data-stu-id="3b877-279">Name: Default execution policy</span></span>
* <span data-ttu-id="3b877-280">Job Timeout: 1 week</span><span class="sxs-lookup"><span data-stu-id="3b877-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="3b877-281">Initial Retry Interval:  100 milliseconds</span><span class="sxs-lookup"><span data-stu-id="3b877-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="3b877-282">Maximum Retry Interval: 30 minutes</span><span class="sxs-lookup"><span data-stu-id="3b877-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="3b877-283">Retry Interval Coefficient: 2</span><span class="sxs-lookup"><span data-stu-id="3b877-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="3b877-284">Maximum Attempts: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="3b877-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="3b877-285">Create the desired execution policy:</span><span class="sxs-lookup"><span data-stu-id="3b877-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="3b877-286">Update a custom execution policy</span><span class="sxs-lookup"><span data-stu-id="3b877-286">Update a custom execution policy</span></span>
<span data-ttu-id="3b877-287">Update the desired execution policy to update:</span><span class="sxs-lookup"><span data-stu-id="3b877-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="3b877-288">Cancel a job</span><span class="sxs-lookup"><span data-stu-id="3b877-288">Cancel a job</span></span>
<span data-ttu-id="3b877-289">Elastic Database Jobs supports cancellation requests of jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="3b877-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span><span class="sxs-lookup"><span data-stu-id="3b877-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="3b877-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span><span class="sxs-lookup"><span data-stu-id="3b877-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="3b877-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span><span class="sxs-lookup"><span data-stu-id="3b877-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="3b877-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span><span class="sxs-lookup"><span data-stu-id="3b877-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="3b877-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span><span class="sxs-lookup"><span data-stu-id="3b877-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="3b877-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="3b877-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](https://msdn.microsoft.com/library/mt346053.aspx) and set the **JobExecutionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="3b877-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](https://msdn.microsoft.com/library/mt346053.aspx) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="3b877-297">To delete a job and job history asynchronously</span><span class="sxs-lookup"><span data-stu-id="3b877-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="3b877-298">Elastic Database jobs supports asynchronous deletion of jobs.</span><span class="sxs-lookup"><span data-stu-id="3b877-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="3b877-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span><span class="sxs-lookup"><span data-stu-id="3b877-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="3b877-300">The system will not automatically cancel active job executions.</span><span class="sxs-lookup"><span data-stu-id="3b877-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="3b877-301">Invoke [**Stop-AzureSqlJobExecution**](https://msdn.microsoft.com/library/mt346053.aspx) to cancel active job executions.</span><span class="sxs-lookup"><span data-stu-id="3b877-301">Invoke [**Stop-AzureSqlJobExecution**](https://msdn.microsoft.com/library/mt346053.aspx) to cancel active job executions.</span></span>

<span data-ttu-id="3b877-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](https://msdn.microsoft.com/library/mt346083.aspx) and set the **JobName** parameter.</span><span class="sxs-lookup"><span data-stu-id="3b877-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](https://msdn.microsoft.com/library/mt346083.aspx) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="3b877-303">To create a custom database target</span><span class="sxs-lookup"><span data-stu-id="3b877-303">To create a custom database target</span></span>
<span data-ttu-id="3b877-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span><span class="sxs-lookup"><span data-stu-id="3b877-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="3b877-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="3b877-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="3b877-306">Set the following variables to reflect the desired database information:</span><span class="sxs-lookup"><span data-stu-id="3b877-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="3b877-307">To create a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="3b877-307">To create a custom database collection target</span></span>
<span data-ttu-id="3b877-308">Use the [**New-AzureSqlJobTarget**](https://msdn.microsoft.com/library/mt346077.aspx) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span><span class="sxs-lookup"><span data-stu-id="3b877-308">Use the [**New-AzureSqlJobTarget**](https://msdn.microsoft.com/library/mt346077.aspx) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="3b877-309">After creating a database group, databases can be associated with the custom collection target.</span><span class="sxs-lookup"><span data-stu-id="3b877-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="3b877-310">Set the following variables to reflect the desired custom collection target configuration:</span><span class="sxs-lookup"><span data-stu-id="3b877-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="3b877-311">To add databases to a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="3b877-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="3b877-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](https://msdn.microsoft.comlibrary/mt346064.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b877-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](https://msdn.microsoft.comlibrary/mt346064.aspx) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="3b877-313">Review the databases within a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="3b877-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="3b877-314">Use the [**Get-AzureSqlJobTarget**](https://msdn.microsoft.com/library/mt346077.aspx) cmdlet to retrieve the child databases within a custom database collection target.</span><span class="sxs-lookup"><span data-stu-id="3b877-314">Use the [**Get-AzureSqlJobTarget**](https://msdn.microsoft.com/library/mt346077.aspx) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="3b877-315">Create a job to execute a script across a custom database collection target</span><span class="sxs-lookup"><span data-stu-id="3b877-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="3b877-316">Use the [**New-AzureSqlJob**](https://msdn.microsoft.com/library/mt346078.aspx) cmdlet to create a job against a group of databases defined by a custom database collection target.</span><span class="sxs-lookup"><span data-stu-id="3b877-316">Use the [**New-AzureSqlJob**](https://msdn.microsoft.com/library/mt346078.aspx) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="3b877-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span><span class="sxs-lookup"><span data-stu-id="3b877-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="3b877-318">Again, it is important that scripts are idempotent to be resilient to retries.</span><span class="sxs-lookup"><span data-stu-id="3b877-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="3b877-319">Data collection across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-319">Data collection across databases</span></span>
<span data-ttu-id="3b877-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span><span class="sxs-lookup"><span data-stu-id="3b877-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="3b877-321">The table can be queried after the fact to see the query’s results from each database.</span><span class="sxs-lookup"><span data-stu-id="3b877-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="3b877-322">This provides an asynchronous method to execute a query across many databases.</span><span class="sxs-lookup"><span data-stu-id="3b877-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="3b877-323">Failed attempts are handled automatically via retries.</span><span class="sxs-lookup"><span data-stu-id="3b877-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="3b877-324">The specified destination table will be automatically created if it does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="3b877-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="3b877-325">The new table matches the schema of the returned result set.</span><span class="sxs-lookup"><span data-stu-id="3b877-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="3b877-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span><span class="sxs-lookup"><span data-stu-id="3b877-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="3b877-327">The following PowerShell script executes a script and collects its results into a specified table.</span><span class="sxs-lookup"><span data-stu-id="3b877-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="3b877-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span><span class="sxs-lookup"><span data-stu-id="3b877-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="3b877-329">This script uses the [**Get-AzureSqlJobTarget**](https://msdn.microsoft.com/library/mt346077.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b877-329">This script uses the [**Get-AzureSqlJobTarget**](https://msdn.microsoft.com/library/mt346077.aspx) cmdlet.</span></span> <span data-ttu-id="3b877-330">Set the parameters for script, credentials, and execution target:</span><span class="sxs-lookup"><span data-stu-id="3b877-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="3b877-331">To create and start a job for data collection scenarios</span><span class="sxs-lookup"><span data-stu-id="3b877-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="3b877-332">This script uses the [**Start-AzureSqlJobExecution**](https://msdn.microsoft.com/library/mt346055.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b877-332">This script uses the [**Start-AzureSqlJobExecution**](https://msdn.microsoft.com/library/mt346055.aspx) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="3b877-333">To schedule a job execution trigger</span><span class="sxs-lookup"><span data-stu-id="3b877-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="3b877-334">The following PowerShell script can be used to create a recurring schedule.</span><span class="sxs-lookup"><span data-stu-id="3b877-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="3b877-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](https://msdn.microsoft.com/library/mt346068.aspx) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span><span class="sxs-lookup"><span data-stu-id="3b877-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](https://msdn.microsoft.com/library/mt346068.aspx) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="3b877-336">Schedules that execute only once can be created by passing -OneTime.</span><span class="sxs-lookup"><span data-stu-id="3b877-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="3b877-337">Create a new schedule:</span><span class="sxs-lookup"><span data-stu-id="3b877-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="3b877-338">To trigger a job executed on a time schedule</span><span class="sxs-lookup"><span data-stu-id="3b877-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="3b877-339">A job trigger can be defined to have a job executed according to a time schedule.</span><span class="sxs-lookup"><span data-stu-id="3b877-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="3b877-340">The following PowerShell script can be used to create a job trigger.</span><span class="sxs-lookup"><span data-stu-id="3b877-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="3b877-341">Use [New-AzureSqlJobTrigger](https://msdn.microsoft.com/library/mt346069.aspx) and set the following variables to correspond to the desired job and schedule:</span><span class="sxs-lookup"><span data-stu-id="3b877-341">Use [New-AzureSqlJobTrigger](https://msdn.microsoft.com/library/mt346069.aspx) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="3b877-342">To remove a scheduled association to stop job from executing on schedule</span><span class="sxs-lookup"><span data-stu-id="3b877-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="3b877-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span><span class="sxs-lookup"><span data-stu-id="3b877-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="3b877-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](https://msdn.microsoft.com/library/mt346070.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b877-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](https://msdn.microsoft.com/library/mt346070.aspx).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="3b877-345">Retrieve job triggers bound to a time schedule</span><span class="sxs-lookup"><span data-stu-id="3b877-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="3b877-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span><span class="sxs-lookup"><span data-stu-id="3b877-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="3b877-347">To retrieve job triggers bound to a job</span><span class="sxs-lookup"><span data-stu-id="3b877-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="3b877-348">Use [Get-AzureSqlJobTrigger](https://msdn.microsoft.com/library/mt346067.aspx) to obtain and display schedules containing a registered job.</span><span class="sxs-lookup"><span data-stu-id="3b877-348">Use [Get-AzureSqlJobTrigger](https://msdn.microsoft.com/library/mt346067.aspx) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="3b877-349">To create a data-tier application (DACPAC) for execution across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="3b877-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b877-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="3b877-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](https://msdn.microsoft.com/library/mt346085.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b877-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](https://msdn.microsoft.com/library/mt346085.aspx).</span></span> <span data-ttu-id="3b877-352">The DACPAC must be accessible to the service.</span><span class="sxs-lookup"><span data-stu-id="3b877-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="3b877-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span><span class="sxs-lookup"><span data-stu-id="3b877-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="3b877-354">To update a data-tier application (DACPAC) for execution across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="3b877-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span><span class="sxs-lookup"><span data-stu-id="3b877-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="3b877-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](https://msdn.microsoft.com/library/mt346074.aspx) to update the DACPAC URI on an existing registered DACPAC:</span><span class="sxs-lookup"><span data-stu-id="3b877-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](https://msdn.microsoft.com/library/mt346074.aspx) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="3b877-357">To create a job to apply a data-tier application (DACPAC) across databases</span><span class="sxs-lookup"><span data-stu-id="3b877-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="3b877-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span><span class="sxs-lookup"><span data-stu-id="3b877-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="3b877-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span><span class="sxs-lookup"><span data-stu-id="3b877-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->


