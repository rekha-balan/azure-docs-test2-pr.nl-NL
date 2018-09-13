---
title: Azure PowerShell Samples for SQL Database | Microsoft Docs
description: Azure PowerShell Samples - Scripts to help you create and manage Azure SQL Database servers, elastic pools, databases, and firewalls.
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: sample
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 03/07/2017
ms.author: janeng
ms.openlocfilehash: b864fd14b6341541302c13222a1650cb21da40af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540904"
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Azure PowerShell samples for Azure SQL Database

The following table includes links to sample Azure PowerShell scripts for Azure SQL Database.

| |  |
|---|---|
|**Create a single database and an elastic pool**||
| [Create a single database and configure a firewall rule](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Creates a single Azure SQL database and configures a server-level firewall rule. |
| [Create elastic pools and move pooled databases](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Creates elastic pools, and moves pooled databases, and changes performance levels.|
|**Configure geo-replication and failover**||
| [Configure and failover a single database using Active Geo-Replication](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Configures Active Geo-Replication for a single Azure SQL database and fails it over to the secondary replica. |
| [Configure and failover a pooled database using Active Geo-Replication](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Configures Active Geo-Replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica. |
|**Scale a single databases and an elastic pool**||
| [Scale a single database](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Monitors the performance metrics of an Azure SQL database, scales it to a higher performance level and creates an alert rule on one of the performance metrics. |
| [Scale an elastic pool](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.  |
| **Auditing and threat detection** |
| [Configure auditing and threat-detection](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Configures auditing and threat detection policies for an Azure SQL database. |
| **Restore, copy, and import a database**||
| [Restore a database](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Restores an Azure SQL database from a geo-redundant backup and restores a deleted Azure SQL database to the latest backup. |
| [Copy a database to new server](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Creates a copy of an existing Azure SQL database in a new Azure SQL server. |
| [Import a database from a bacpac file](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Imports a database to an Azure SQL server from a bacpac file. |
|||
