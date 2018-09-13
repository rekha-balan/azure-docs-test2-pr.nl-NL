---
title: Manage groups of Azure SQL databases | Microsoft Docs
description: Walk through creation and management of an elastic job.
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fe44bd6d97875f7e94446912de0ab55332360f41
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550064"
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="92f59-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span><span class="sxs-lookup"><span data-stu-id="92f59-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="92f59-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span><span class="sxs-lookup"><span data-stu-id="92f59-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="92f59-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="92f59-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="92f59-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="92f59-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="92f59-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="92f59-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="92f59-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92f59-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="92f59-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="92f59-109">Prerequisites</span></span>
* <span data-ttu-id="92f59-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="92f59-110">An Azure subscription.</span></span> <span data-ttu-id="92f59-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92f59-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="92f59-112">An elastic pool.</span><span class="sxs-lookup"><span data-stu-id="92f59-112">An elastic pool.</span></span> <span data-ttu-id="92f59-113">See [About elastic pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="92f59-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="92f59-114">Installation of elastic database job service components.</span><span class="sxs-lookup"><span data-stu-id="92f59-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="92f59-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="92f59-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="92f59-116">Creating jobs</span><span class="sxs-lookup"><span data-stu-id="92f59-116">Creating jobs</span></span>
1. <span data-ttu-id="92f59-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span><span class="sxs-lookup"><span data-stu-id="92f59-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="92f59-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span><span class="sxs-lookup"><span data-stu-id="92f59-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![Name the job, type or paste in code, and click Run][1]
3. <span data-ttu-id="92f59-120">In the **Create Job** blade, type a name for the job.</span><span class="sxs-lookup"><span data-stu-id="92f59-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="92f59-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span><span class="sxs-lookup"><span data-stu-id="92f59-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="92f59-122">Paste or type in the T-SQL script.</span><span class="sxs-lookup"><span data-stu-id="92f59-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="92f59-123">Click **Save** and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="92f59-123">Click **Save** and then click **Run**.</span></span>
   
    ![Create jobs and run][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="92f59-125">Run idempotent jobs</span><span class="sxs-lookup"><span data-stu-id="92f59-125">Run idempotent jobs</span></span>
<span data-ttu-id="92f59-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span><span class="sxs-lookup"><span data-stu-id="92f59-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="92f59-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span><span class="sxs-lookup"><span data-stu-id="92f59-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="92f59-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span><span class="sxs-lookup"><span data-stu-id="92f59-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="92f59-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span><span class="sxs-lookup"><span data-stu-id="92f59-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="92f59-130">An example is shown here:</span><span class="sxs-lookup"><span data-stu-id="92f59-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="92f59-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span><span class="sxs-lookup"><span data-stu-id="92f59-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="92f59-132">This script then updates the table created previously.</span><span class="sxs-lookup"><span data-stu-id="92f59-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="92f59-133">Checking job status</span><span class="sxs-lookup"><span data-stu-id="92f59-133">Checking job status</span></span>
<span data-ttu-id="92f59-134">After a job has begun, you can check on its progress.</span><span class="sxs-lookup"><span data-stu-id="92f59-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="92f59-135">From the elastic pool page, click **Manage jobs**.</span><span class="sxs-lookup"><span data-stu-id="92f59-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Click "Manage jobs"][2]
2. <span data-ttu-id="92f59-137">Click on the name (a) of a job.</span><span class="sxs-lookup"><span data-stu-id="92f59-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="92f59-138">The **STATUS** can be "Completed" or "Failed."</span><span class="sxs-lookup"><span data-stu-id="92f59-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="92f59-139">The job's details appear (b) with its date and time of creation and running.</span><span class="sxs-lookup"><span data-stu-id="92f59-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="92f59-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span><span class="sxs-lookup"><span data-stu-id="92f59-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Checking a finished job][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="92f59-142">Checking failed jobs</span><span class="sxs-lookup"><span data-stu-id="92f59-142">Checking failed jobs</span></span>
<span data-ttu-id="92f59-143">If a job fails, a log of its execution can found.</span><span class="sxs-lookup"><span data-stu-id="92f59-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="92f59-144">Click the name of the failed job to see its details.</span><span class="sxs-lookup"><span data-stu-id="92f59-144">Click the name of the failed job to see its details.</span></span>

![Check a failed job][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-jobs-create-and-manage/screen-2.png







