---
title: SQL Database Disaster Recovery Drills | Microsoft Docs
description: Learn guidance and best practices for using Azure SQL Database to perform disaster recovery drills that will help keep your mission critical business applications resilient to failures and outages.
services: sql-database
documentationcenter: ''
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 821be267a109bdcb1a1d22107f0ab4c469e6d6aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556303"
---
# <a name="performing-disaster-recovery-drill"></a>Performing Disaster Recovery Drill
It is recommended that validation of application readiness for recovery workflow is performed periodically. Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice. It is also a requirement by most industry standards as part of business continuity certification.

Performing a disaster recovery drill consists of:

* Simulating data tier outage
* Recovering
* Validate application integrity post recovery

Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary. Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.

## <a name="geo-restore"></a>Geo-Restore
To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.

#### <a name="outage-simulation"></a>Outage simulation
To simulate the outage you can delete or rename the source database. This will cause application connectivity failure.

#### <a name="recovery"></a>Recovery
* Perform the Geo-Restore of the database into a different server as described [here](sql-database-disaster-recovery.md).
* Change the application configuration to connect to the recovered database(s) and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.

#### <a name="validation"></a>Validation
* Complete the drill by verifying the application integrity post recovery (i.e. connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).

## <a name="geo-replication"></a>Geo-Replication
For a database that is protected using Geo-Replication the drill exercise will involve planned failover to the secondary database. The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched. Unlike the unplanned failover, this operation will not result in data loss, so the drill can be performed in the production environment.

#### <a name="outage-simulation"></a>Outage simulation
To simulate the outage you can disable the web application or virtual machine connected to the database. This will result in the connectivity failures for the web clients.

#### <a name="recovery"></a>Recovery
* Make sure the application configuration in the DR region points to the former secondary which will become fully accessible new primary.
* Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary
* Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.

#### <a name="validation"></a>Validation
* Complete the drill by verifying the application integrity post recovery (i.e. connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).

## <a name="next-steps"></a>Next steps
* To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)
* To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)
* To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)
* To learn about faster recovery options, see [Active-Geo-Replication](sql-database-geo-replication-overview.md)  
