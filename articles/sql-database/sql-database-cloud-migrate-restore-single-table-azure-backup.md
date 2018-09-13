---
title: Restore a single table from Azure SQL Database backup | Microsoft Docs
description: Learn how to restore a single table from Azure SQL Database backup.
services: sql-database
documentationcenter: ''
author: dalechen
manager: cshepard
editor: ''
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: restore
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/20/2017
ms.author: daleche
ms.openlocfilehash: c10861efcdfafad127d00a072b65eb0e6b3ab805
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550194"
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="28ea0-103">How to restore a single table from an Azure SQL Database backup</span><span class="sxs-lookup"><span data-stu-id="28ea0-103">How to restore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="28ea0-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span><span class="sxs-lookup"><span data-stu-id="28ea0-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span></span> <span data-ttu-id="28ea0-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="28ea0-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a><span data-ttu-id="28ea0-106">Preparation steps: Rename the table and restore a copy of the database</span><span class="sxs-lookup"><span data-stu-id="28ea0-106">Preparation steps: Rename the table and restore a copy of the database</span></span>
1. <span data-ttu-id="28ea0-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span><span class="sxs-lookup"><span data-stu-id="28ea0-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span></span> <span data-ttu-id="28ea0-108">Use Microsoft SQL Management Studio to rename the table.</span><span class="sxs-lookup"><span data-stu-id="28ea0-108">Use Microsoft SQL Management Studio to rename the table.</span></span> <span data-ttu-id="28ea0-109">For example, rename the table as &lt;table name&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="28ea0-109">For example, rename the table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="28ea0-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span><span class="sxs-lookup"><span data-stu-id="28ea0-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span></span> <span data-ttu-id="28ea0-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span><span class="sxs-lookup"><span data-stu-id="28ea0-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="28ea0-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span><span class="sxs-lookup"><span data-stu-id="28ea0-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="28ea0-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="28ea0-114">This step doesn't overwrite the existing database name on the server.</span><span class="sxs-lookup"><span data-stu-id="28ea0-114">This step doesn't overwrite the existing database name on the server.</span></span> <span data-ttu-id="28ea0-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span><span class="sxs-lookup"><span data-stu-id="28ea0-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span></span>
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a><span data-ttu-id="28ea0-116">Copying the table from the restored database by using the SQL Database Migration tool</span><span class="sxs-lookup"><span data-stu-id="28ea0-116">Copying the table from the restored database by using the SQL Database Migration tool</span></span>

1. <span data-ttu-id="28ea0-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="28ea0-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="28ea0-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database Migration wizard - Select Process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="28ea0-120">In the **Connect to Server** dialog box, apply the following settings:</span><span class="sxs-lookup"><span data-stu-id="28ea0-120">In the **Connect to Server** dialog box, apply the following settings:</span></span>

   * <span data-ttu-id="28ea0-121">Server name: **Your SQL server**</span><span class="sxs-lookup"><span data-stu-id="28ea0-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="28ea0-122">Authentication: **SQL Server Authentication**</span><span class="sxs-lookup"><span data-stu-id="28ea0-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="28ea0-123">Login: **Your login**</span><span class="sxs-lookup"><span data-stu-id="28ea0-123">Login: **Your login**</span></span>
   * <span data-ttu-id="28ea0-124">Password: **Your password**</span><span class="sxs-lookup"><span data-stu-id="28ea0-124">Password: **Your password**</span></span>
   * <span data-ttu-id="28ea0-125">Database: **Master DB (List all databases)**</span><span class="sxs-lookup"><span data-stu-id="28ea0-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="28ea0-126">By default the wizard saves your login information.</span><span class="sxs-lookup"><span data-stu-id="28ea0-126">By default the wizard saves your login information.</span></span> <span data-ttu-id="28ea0-127">If you don't want it to, select **Forget Login Information**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database Migration wizard - Select Source - step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="28ea0-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database Migration wizard - Select Source - step 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="28ea0-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span><span class="sxs-lookup"><span data-stu-id="28ea0-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span></span>
   <span data-ttu-id="28ea0-132">![SQL Database Migration wizard - Choose Objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="28ea0-132">![SQL Database Migration wizard - Choose Objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="28ea0-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span><span class="sxs-lookup"><span data-stu-id="28ea0-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span></span> <span data-ttu-id="28ea0-134">You also have the option to save the TSQL Script for later use.</span><span class="sxs-lookup"><span data-stu-id="28ea0-134">You also have the option to save the TSQL Script for later use.</span></span>
   <span data-ttu-id="28ea0-135">![SQL Database Migration wizard - Script Wizard Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="28ea0-135">![SQL Database Migration wizard - Script Wizard Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="28ea0-136">On the **Results Summary** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-136">On the **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="28ea0-137">![SQL Database Migration wizard - Results Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="28ea0-137">![SQL Database Migration wizard - Results Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="28ea0-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span><span class="sxs-lookup"><span data-stu-id="28ea0-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span></span>
   
   * <span data-ttu-id="28ea0-139">**Server Name**: Target server instance</span><span class="sxs-lookup"><span data-stu-id="28ea0-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="28ea0-140">**Authentication**: **SQL Server authentication**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="28ea0-141">Enter your login credentials.</span><span class="sxs-lookup"><span data-stu-id="28ea0-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="28ea0-142">**Database**: **Master DB (List all databases)**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="28ea0-143">This option lists all the databases on the target server.</span><span class="sxs-lookup"><span data-stu-id="28ea0-143">This option lists all the databases on the target server.</span></span>
     
     ![SQL Database Migration wizard - Setup Target Server Connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="28ea0-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28ea0-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span></span> <span data-ttu-id="28ea0-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span><span class="sxs-lookup"><span data-stu-id="28ea0-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="28ea0-147">Verification step</span><span class="sxs-lookup"><span data-stu-id="28ea0-147">Verification step</span></span>

- <span data-ttu-id="28ea0-148">Query and test the newly copied table to make sure that the data is intact.</span><span class="sxs-lookup"><span data-stu-id="28ea0-148">Query and test the newly copied table to make sure that the data is intact.</span></span> <span data-ttu-id="28ea0-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span><span class="sxs-lookup"><span data-stu-id="28ea0-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="28ea0-150">(for example, &lt;table name&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="28ea0-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="28ea0-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="28ea0-151">Next steps</span></span>
[<span data-ttu-id="28ea0-152">SQL Database automatic backups</span><span class="sxs-lookup"><span data-stu-id="28ea0-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)








