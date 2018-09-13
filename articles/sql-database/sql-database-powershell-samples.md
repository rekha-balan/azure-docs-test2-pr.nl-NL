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
# <a name="azure-powershell-samples-for-azure-sql-database"></a><span data-ttu-id="cb56e-103">Azure PowerShell samples for Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cb56e-103">Azure PowerShell samples for Azure SQL Database</span></span>

<span data-ttu-id="cb56e-104">The following table includes links to sample Azure PowerShell scripts for Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cb56e-104">The following table includes links to sample Azure PowerShell scripts for Azure SQL Database.</span></span>

| |  |
|---|---|
|<span data-ttu-id="cb56e-105">**Create a single database and an elastic pool**</span><span class="sxs-lookup"><span data-stu-id="cb56e-105">**Create a single database and an elastic pool**</span></span>||
| [<span data-ttu-id="cb56e-106">Create a single database and configure a firewall rule</span><span class="sxs-lookup"><span data-stu-id="cb56e-106">Create a single database and configure a firewall rule</span></span>](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="cb56e-107">Creates a single Azure SQL database and configures a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="cb56e-107">Creates a single Azure SQL database and configures a server-level firewall rule.</span></span> |
| [<span data-ttu-id="cb56e-108">Create elastic pools and move pooled databases</span><span class="sxs-lookup"><span data-stu-id="cb56e-108">Create elastic pools and move pooled databases</span></span>](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="cb56e-109">Creates elastic pools, and moves pooled databases, and changes performance levels.</span><span class="sxs-lookup"><span data-stu-id="cb56e-109">Creates elastic pools, and moves pooled databases, and changes performance levels.</span></span>|
|<span data-ttu-id="cb56e-110">**Configure geo-replication and failover**</span><span class="sxs-lookup"><span data-stu-id="cb56e-110">**Configure geo-replication and failover**</span></span>||
| [<span data-ttu-id="cb56e-111">Configure and failover a single database using Active Geo-Replication</span><span class="sxs-lookup"><span data-stu-id="cb56e-111">Configure and failover a single database using Active Geo-Replication</span></span>](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="cb56e-112">Configures Active Geo-Replication for a single Azure SQL database and fails it over to the secondary replica.</span><span class="sxs-lookup"><span data-stu-id="cb56e-112">Configures Active Geo-Replication for a single Azure SQL database and fails it over to the secondary replica.</span></span> |
| [<span data-ttu-id="cb56e-113">Configure and failover a pooled database using Active Geo-Replication</span><span class="sxs-lookup"><span data-stu-id="cb56e-113">Configure and failover a pooled database using Active Geo-Replication</span></span>](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="cb56e-114">Configures Active Geo-Replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica.</span><span class="sxs-lookup"><span data-stu-id="cb56e-114">Configures Active Geo-Replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica.</span></span> |
|<span data-ttu-id="cb56e-115">**Scale a single databases and an elastic pool**</span><span class="sxs-lookup"><span data-stu-id="cb56e-115">**Scale a single databases and an elastic pool**</span></span>||
| [<span data-ttu-id="cb56e-116">Scale a single database</span><span class="sxs-lookup"><span data-stu-id="cb56e-116">Scale a single database</span></span>](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="cb56e-117">Monitors the performance metrics of an Azure SQL database, scales it to a higher performance level and creates an alert rule on one of the performance metrics.</span><span class="sxs-lookup"><span data-stu-id="cb56e-117">Monitors the performance metrics of an Azure SQL database, scales it to a higher performance level and creates an alert rule on one of the performance metrics.</span></span> |
| [<span data-ttu-id="cb56e-118">Scale an elastic pool</span><span class="sxs-lookup"><span data-stu-id="cb56e-118">Scale an elastic pool</span></span>](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="cb56e-119">Monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span><span class="sxs-lookup"><span data-stu-id="cb56e-119">Monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span>  |
| <span data-ttu-id="cb56e-120">**Auditing and threat detection**</span><span class="sxs-lookup"><span data-stu-id="cb56e-120">**Auditing and threat detection**</span></span> |
| [<span data-ttu-id="cb56e-121">Configure auditing and threat-detection</span><span class="sxs-lookup"><span data-stu-id="cb56e-121">Configure auditing and threat-detection</span></span>](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="cb56e-122">Configures auditing and threat detection policies for an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="cb56e-122">Configures auditing and threat detection policies for an Azure SQL database.</span></span> |
| <span data-ttu-id="cb56e-123">**Restore, copy, and import a database**</span><span class="sxs-lookup"><span data-stu-id="cb56e-123">**Restore, copy, and import a database**</span></span>||
| [<span data-ttu-id="cb56e-124">Restore a database</span><span class="sxs-lookup"><span data-stu-id="cb56e-124">Restore a database</span></span>](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="cb56e-125">Restores an Azure SQL database from a geo-redundant backup and restores a deleted Azure SQL database to the latest backup.</span><span class="sxs-lookup"><span data-stu-id="cb56e-125">Restores an Azure SQL database from a geo-redundant backup and restores a deleted Azure SQL database to the latest backup.</span></span> |
| [<span data-ttu-id="cb56e-126">Copy a database to new server</span><span class="sxs-lookup"><span data-stu-id="cb56e-126">Copy a database to new server</span></span>](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="cb56e-127">Creates a copy of an existing Azure SQL database in a new Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="cb56e-127">Creates a copy of an existing Azure SQL database in a new Azure SQL server.</span></span> |
| [<span data-ttu-id="cb56e-128">Import a database from a bacpac file</span><span class="sxs-lookup"><span data-stu-id="cb56e-128">Import a database from a bacpac file</span></span>](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="cb56e-129">Imports a database to an Azure SQL server from a bacpac file.</span><span class="sxs-lookup"><span data-stu-id="cb56e-129">Imports a database to an Azure SQL server from a bacpac file.</span></span> |
|||
