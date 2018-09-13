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
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Manage databases in Azure SQL Data Warehouse
SQL Data Warehouse automates many aspects of managing your databases. For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.

You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries. You will also need to perform a few security tasks to manage permissions for users and logins.

This overview covers these aspects of managing SQL Data Warehouse.

* Management tools
* Scale Compute
* Pause and Resume
* Performance Best Practices
* Query Monitoring
* Security
* Backup and restore

## <a name="management-tools"></a>Management tools
You can use a variety of tools to manage databases in SQL Data Warehouse. As you manage databases, you will develop tool preferences for each type of task you need to perform.

### <a name="azure-portal"></a>Azure portal
The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources. This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.

To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools in Visual Studio
[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases. If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.

SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases. To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.  

To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Command-line tools
Command line tools are ideal for automating your workloads.  PowerShell and sqlcmd are two great ways to automate your processes.  We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.

### <a name="dynamic-management-views"></a>Dynamic management views
DMVs are the bread and butter of managing SQL Data Warehouse. Almost all information that surfaces in the portal relies on DMVs. To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].

To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Scale compute
In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth. To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database. SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.

To learn more about scaling DWUs, see [Scale performance].

## <a name="pause-and-resume"></a>Pause and resume
To save costs, you can pause and resume compute resources on-demand. For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day. You won't be charged for DWUs while the database is paused.

For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].

## <a name="performance-best-practices"></a>Performance Best Practices
When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.  You will find best practices throughout many of our topics.

To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Query Monitoring
Sometimes a query is running too long, but you aren't sure of which one is the culprit. SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.

To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].

## <a name="security"></a>Security
To maintain a secure system, you must be on the alert and guard against any type of unauthorized access. A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect. It needs proper authentication of user credentials. After a user has connected to the database, the user should only have permissions to perform a minimal number of actions. To secure data, you can use encryption. It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.

To learn about managing security, head over to the [Security overview][Security overview].

## <a name="backup-and-restore"></a>Backup and restore
Having reliable backps of your data is an essential part of any production database. SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals. These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.  For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].

## <a name="next-steps"></a>Next steps
Using good database design principles will make it easier to manage your databases in SQL Data Warehouse. To learn more, head over to the [Development overview][Development overview].

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
