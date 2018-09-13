---
title: Manage databases in Azure SQL Data Warehouse | Microsoft Docs
description: Overview of managing SQL Data Warehouse databases. Includes management tools, DWUs and scale-out performance, troubleshooting query performance, establishing good security policies, and restoring a database from data corruption or from a regional outage.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 044b041df306b4272ba2f284db7da50f4130e3a2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549568"
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="62075-104">Manage databases in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="62075-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="62075-105">SQL Data Warehouse automates many aspects of managing your databases.</span><span class="sxs-lookup"><span data-stu-id="62075-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="62075-106">For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.</span><span class="sxs-lookup"><span data-stu-id="62075-106">For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.</span></span>

<span data-ttu-id="62075-107">You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries.</span><span class="sxs-lookup"><span data-stu-id="62075-107">You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="62075-108">You will also need to perform a few security tasks to manage permissions for users and logins.</span><span class="sxs-lookup"><span data-stu-id="62075-108">You will also need to perform a few security tasks to manage permissions for users and logins.</span></span>

<span data-ttu-id="62075-109">This overview covers these aspects of managing SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62075-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="62075-110">Management tools</span><span class="sxs-lookup"><span data-stu-id="62075-110">Management tools</span></span>
* <span data-ttu-id="62075-111">Scale Compute</span><span class="sxs-lookup"><span data-stu-id="62075-111">Scale Compute</span></span>
* <span data-ttu-id="62075-112">Pause and Resume</span><span class="sxs-lookup"><span data-stu-id="62075-112">Pause and Resume</span></span>
* <span data-ttu-id="62075-113">Performance Best Practices</span><span class="sxs-lookup"><span data-stu-id="62075-113">Performance Best Practices</span></span>
* <span data-ttu-id="62075-114">Query Monitoring</span><span class="sxs-lookup"><span data-stu-id="62075-114">Query Monitoring</span></span>
* <span data-ttu-id="62075-115">Security</span><span class="sxs-lookup"><span data-stu-id="62075-115">Security</span></span>
* <span data-ttu-id="62075-116">Backup and restore</span><span class="sxs-lookup"><span data-stu-id="62075-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="62075-117">Management tools</span><span class="sxs-lookup"><span data-stu-id="62075-117">Management tools</span></span>
<span data-ttu-id="62075-118">You can use a variety of tools to manage databases in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62075-118">You can use a variety of tools to manage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="62075-119">As you manage databases, you will develop tool preferences for each type of task you need to perform.</span><span class="sxs-lookup"><span data-stu-id="62075-119">As you manage databases, you will develop tool preferences for each type of task you need to perform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="62075-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="62075-120">Azure portal</span></span>
<span data-ttu-id="62075-121">The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span><span class="sxs-lookup"><span data-stu-id="62075-121">The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="62075-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.</span><span class="sxs-lookup"><span data-stu-id="62075-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.</span></span>

<span data-ttu-id="62075-123">To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="62075-123">To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="62075-124">SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62075-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="62075-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases.</span><span class="sxs-lookup"><span data-stu-id="62075-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases.</span></span> <span data-ttu-id="62075-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62075-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="62075-127">SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases.</span><span class="sxs-lookup"><span data-stu-id="62075-127">SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="62075-128">To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="62075-128">To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.</span></span>  

<span data-ttu-id="62075-129">To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="62075-129">To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="62075-130">Command-line tools</span><span class="sxs-lookup"><span data-stu-id="62075-130">Command-line tools</span></span>
<span data-ttu-id="62075-131">Command line tools are ideal for automating your workloads.</span><span class="sxs-lookup"><span data-stu-id="62075-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="62075-132">PowerShell and sqlcmd are two great ways to automate your processes.</span><span class="sxs-lookup"><span data-stu-id="62075-132">PowerShell and sqlcmd are two great ways to automate your processes.</span></span>  <span data-ttu-id="62075-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.</span><span class="sxs-lookup"><span data-stu-id="62075-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="62075-134">Dynamic management views</span><span class="sxs-lookup"><span data-stu-id="62075-134">Dynamic management views</span></span>
<span data-ttu-id="62075-135">DMVs are the bread and butter of managing SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62075-135">DMVs are the bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="62075-136">Almost all information that surfaces in the portal relies on DMVs.</span><span class="sxs-lookup"><span data-stu-id="62075-136">Almost all information that surfaces in the portal relies on DMVs.</span></span> <span data-ttu-id="62075-137">To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="62075-137">To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="62075-138">To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="62075-138">To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="62075-139">Scale compute</span><span class="sxs-lookup"><span data-stu-id="62075-139">Scale compute</span></span>
<span data-ttu-id="62075-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span><span class="sxs-lookup"><span data-stu-id="62075-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="62075-141">To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database.</span><span class="sxs-lookup"><span data-stu-id="62075-141">To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database.</span></span> <span data-ttu-id="62075-142">SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.</span><span class="sxs-lookup"><span data-stu-id="62075-142">SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.</span></span>

<span data-ttu-id="62075-143">To learn more about scaling DWUs, see [Scale performance].</span><span class="sxs-lookup"><span data-stu-id="62075-143">To learn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="62075-144">Pause and resume</span><span class="sxs-lookup"><span data-stu-id="62075-144">Pause and resume</span></span>
<span data-ttu-id="62075-145">To save costs, you can pause and resume compute resources on-demand.</span><span class="sxs-lookup"><span data-stu-id="62075-145">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="62075-146">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span><span class="sxs-lookup"><span data-stu-id="62075-146">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="62075-147">You won't be charged for DWUs while the database is paused.</span><span class="sxs-lookup"><span data-stu-id="62075-147">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="62075-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="62075-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="62075-149">Performance Best Practices</span><span class="sxs-lookup"><span data-stu-id="62075-149">Performance Best Practices</span></span>
<span data-ttu-id="62075-150">When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.</span><span class="sxs-lookup"><span data-stu-id="62075-150">When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.</span></span>  <span data-ttu-id="62075-151">You will find best practices throughout many of our topics.</span><span class="sxs-lookup"><span data-stu-id="62075-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="62075-152">To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="62075-152">To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="62075-153">Query Monitoring</span><span class="sxs-lookup"><span data-stu-id="62075-153">Query Monitoring</span></span>
<span data-ttu-id="62075-154">Sometimes a query is running too long, but you aren't sure of which one is the culprit.</span><span class="sxs-lookup"><span data-stu-id="62075-154">Sometimes a query is running too long, but you aren't sure of which one is the culprit.</span></span> <span data-ttu-id="62075-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.</span><span class="sxs-lookup"><span data-stu-id="62075-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.</span></span>

<span data-ttu-id="62075-156">To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="62075-156">To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="62075-157">Security</span><span class="sxs-lookup"><span data-stu-id="62075-157">Security</span></span>
<span data-ttu-id="62075-158">To maintain a secure system, you must be on the alert and guard against any type of unauthorized access.</span><span class="sxs-lookup"><span data-stu-id="62075-158">To maintain a secure system, you must be on the alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="62075-159">A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect.</span><span class="sxs-lookup"><span data-stu-id="62075-159">A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="62075-160">It needs proper authentication of user credentials.</span><span class="sxs-lookup"><span data-stu-id="62075-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="62075-161">After a user has connected to the database, the user should only have permissions to perform a minimal number of actions.</span><span class="sxs-lookup"><span data-stu-id="62075-161">After a user has connected to the database, the user should only have permissions to perform a minimal number of actions.</span></span> <span data-ttu-id="62075-162">To secure data, you can use encryption.</span><span class="sxs-lookup"><span data-stu-id="62075-162">To secure data, you can use encryption.</span></span> <span data-ttu-id="62075-163">It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.</span><span class="sxs-lookup"><span data-stu-id="62075-163">It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="62075-164">To learn about managing security, head over to the [Security overview][Security overview].</span><span class="sxs-lookup"><span data-stu-id="62075-164">To learn about managing security, head over to the [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="62075-165">Backup and restore</span><span class="sxs-lookup"><span data-stu-id="62075-165">Backup and restore</span></span>
<span data-ttu-id="62075-166">Having reliable backps of your data is an essential part of any production database.</span><span class="sxs-lookup"><span data-stu-id="62075-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="62075-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="62075-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="62075-168">These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span><span class="sxs-lookup"><span data-stu-id="62075-168">These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="62075-169">For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="62075-169">For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="62075-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="62075-170">Next steps</span></span>
<span data-ttu-id="62075-171">Using good database design principles will make it easier to manage your databases in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62075-171">Using good database design principles will make it easier to manage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="62075-172">To learn more, head over to the [Development overview][Development overview].</span><span class="sxs-lookup"><span data-stu-id="62075-172">To learn more, head over to the [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Scale performance]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
