---
title: Troubleshoot common connection issues to Azure SQL Database
description: Steps to identify and resolve common connection errors for Azure SQL Database.
services: sql-database
documentationcenter: ''
author: dalechen
manager: cshepard
editor: ''
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: troubleshoot
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: daleche
ms.openlocfilehash: 914084ff790ceb2e11852c5dae757b935f813062
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549770"
---
# <a name="troubleshoot-connection-issues-to-azure-sql-database"></a>Troubleshoot connection issues to Azure SQL Database
When the connection to Azure SQL Database fails, you receive [error messages](sql-database-develop-error-messages.md). This article is a centralized topic that helps you troubleshoot Azure SQL Database connectivity issues. It introduces [the common causes](#cause) of connection issues, recommends [a troubleshooting tool](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) that helps you identity the problem, and provides troubleshooting steps to solve [transient errors](#troubleshoot-transient-errors) and [persistent or non-transient errors](#troubleshoot-the-persistent-errors). Finally, it lists [all the relevant articles for Azure SQL Database connectivity issues](#all-topics-for-azure-sql-database-connection-problems).

If you encounter the connection issues, try the troubleshoot steps that are described in this article.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Cause
Connection problems may be caused by any of the following:

* Failure to apply best practices and design guidelines during the application design process.  See [SQL Database Development Overview](sql-database-develop-overview.md) to get started.
* Azure SQL Database reconfiguration
* Firewall settings
* Connection time-out
* Incorrect login information
* Maximum limit reached on some Azure SQL Database resources

Generally, connection issues to Azure SQL Database can be classified as follows:

* [Transient errors (short-lived or intermittent)](#troubleshoot-transient-errors)
* [Persistent or non-transient errors (errors that regularly recur)](#troubleshoot-the-persistent-errors)

## <a name="try-the-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Try the troubleshooter for Azure SQL Database connectivity issues
If you encounter a specific connection error, try [this tool](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), which will help you quickly identity and resolve your problem.

## <a name="troubleshoot-transient-errors"></a>Troubleshoot transient errors

When an application connects to an Azure SQL database, you receive the following error message:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry the connection later. If the problem persists, contact customer support, and provide them the session tracing ID of <z>"
```

> [!NOTE]
> This error message is typically transient (short-lived).
> 
> 

This error occurs when the Azure database is being moved (or reconfigured) and your application loses its connection to the SQL database. SQL database reconfiguration events occurs because of a planned event (for example, a software upgrade) or an unplanned event (for example, a process crash, or load balancing). Most reconfiguration events are generally short-lived and should be completed in less than 60 seconds at most. However, these events can occasionally take longer to finish, such as when a large transaction causes a long-running recovery.

### <a name="steps-to-resolve-transient-connectivity-issues"></a>Steps to resolve transient connectivity issues

1. Check the [Microsoft Azure Service Dashboard](https://azure.microsoft.com/status) for any known outages that occurred during the time during which the errors were reported by the application.
2. Applications that connect to a cloud service such as Azure SQL Database should expect periodic reconfiguration events and implement retry logic to handle these errors instead of surfacing these as application errors to users. Review the [Transient errors](sql-database-connectivity-issues.md) section and the best practices and design guidelines at [SQL Database Development Overview](sql-database-develop-overview.md) for more information and general retry strategies. Then, see code samples at [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md) for specifics.
3. As a database approaches its resource limits, it can seem to be a transient connectivity issue. See [Troubleshooting Performance Issues](sql-database-troubleshoot-performance.md).
4. If connectivity problems continue, or if the duration for which your application encounters the error exceeds 60 seconds or if you see multiple occurrences of the error in a given day, file an Azure support request by selecting **Get Support** on the [Azure Support](https://azure.microsoft.com/support/options) site.

## <a name="troubleshoot-persistent-errors-non-transient-errors"></a>Troubleshoot persistent errors (non-transient errors)
If the application persistently fails to connect to Azure SQL Database, it usually indicates an issue with one of the following:

* Firewall configuration. The Azure SQL database or client-side firewall is blocking connections to Azure SQL Database.
* Network reconfiguration on the client side: for example, a new IP address or a proxy server.
* User error: for example, mistyped connection parameters, such as the server name in the connection string.

### <a name="steps-to-resolve-persistent-connectivity-issues"></a>Steps to resolve persistent connectivity issues
1. Set up [firewall rules](sql-database-configure-firewall-settings.md) to allow the client IP address. For temporary testing purposes, set up a firewall rule using 0.0.0.0 as the starting IP address range and using 255.255.255.255 as the ending IP address range. This will open the server to all IP addresses. If this resolves your connectivity issue, remove this rule and create a firewall rule for a appropriately limited IP address or address range. 
2. On all firewalls between the client and the Internet, make sure that port 1433 is open for outbound connections. Review [Configure the Windows Firewall to Allow SQL Server Access](https://msdn.microsoft.com/library/cc646023.aspx) and [Hybrid Identity Required Ports and Protocols](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) for additional pointers related to additional ports that you need to open for Azure Active Directory authentication.
3. Verify your connection string and other connection settings. See the Connection String section in the [connectivity issues topic](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Check service health in the dashboard. If you think there’s a regional outage, see [Recover from an outage](sql-database-disaster-recovery.md) for steps to recover to a new region.

## <a name="next-steps"></a>Next steps
* [Troubleshoot Azure SQL Database performance issues](sql-database-troubleshoot-performance.md)
* [Search the documentation on Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [View the latest updates to the Azure SQL Database service](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Additional resources
* [SQL Database Development Overview](sql-database-develop-overview.md)
* [General transient fault-handling guidance](../best-practices-retry-general.md)
* [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)

