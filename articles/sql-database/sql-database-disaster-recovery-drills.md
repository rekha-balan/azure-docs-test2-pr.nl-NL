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
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="c3273-103">Performing Disaster Recovery Drill</span><span class="sxs-lookup"><span data-stu-id="c3273-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="c3273-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span><span class="sxs-lookup"><span data-stu-id="c3273-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="c3273-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span><span class="sxs-lookup"><span data-stu-id="c3273-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="c3273-106">It is also a requirement by most industry standards as part of business continuity certification.</span><span class="sxs-lookup"><span data-stu-id="c3273-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="c3273-107">Performing a disaster recovery drill consists of:</span><span class="sxs-lookup"><span data-stu-id="c3273-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="c3273-108">Simulating data tier outage</span><span class="sxs-lookup"><span data-stu-id="c3273-108">Simulating data tier outage</span></span>
* <span data-ttu-id="c3273-109">Recovering</span><span class="sxs-lookup"><span data-stu-id="c3273-109">Recovering</span></span>
* <span data-ttu-id="c3273-110">Validate application integrity post recovery</span><span class="sxs-lookup"><span data-stu-id="c3273-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="c3273-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span><span class="sxs-lookup"><span data-stu-id="c3273-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="c3273-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c3273-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="c3273-113">Geo-Restore</span><span class="sxs-lookup"><span data-stu-id="c3273-113">Geo-Restore</span></span>
<span data-ttu-id="c3273-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span><span class="sxs-lookup"><span data-stu-id="c3273-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="c3273-115">Outage simulation</span><span class="sxs-lookup"><span data-stu-id="c3273-115">Outage simulation</span></span>
<span data-ttu-id="c3273-116">To simulate the outage you can delete or rename the source database.</span><span class="sxs-lookup"><span data-stu-id="c3273-116">To simulate the outage you can delete or rename the source database.</span></span> <span data-ttu-id="c3273-117">This will cause application connectivity failure.</span><span class="sxs-lookup"><span data-stu-id="c3273-117">This will cause application connectivity failure.</span></span>

#### <a name="recovery"></a><span data-ttu-id="c3273-118">Recovery</span><span class="sxs-lookup"><span data-stu-id="c3273-118">Recovery</span></span>
* <span data-ttu-id="c3273-119">Perform the Geo-Restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="c3273-119">Perform the Geo-Restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="c3273-120">Change the application configuration to connect to the recovered database(s) and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span><span class="sxs-lookup"><span data-stu-id="c3273-120">Change the application configuration to connect to the recovered database(s) and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="c3273-121">Validation</span><span class="sxs-lookup"><span data-stu-id="c3273-121">Validation</span></span>
* <span data-ttu-id="c3273-122">Complete the drill by verifying the application integrity post recovery (i.e. connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span><span class="sxs-lookup"><span data-stu-id="c3273-122">Complete the drill by verifying the application integrity post recovery (i.e. connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="c3273-123">Geo-Replication</span><span class="sxs-lookup"><span data-stu-id="c3273-123">Geo-Replication</span></span>
<span data-ttu-id="c3273-124">For a database that is protected using Geo-Replication the drill exercise will involve planned failover to the secondary database.</span><span class="sxs-lookup"><span data-stu-id="c3273-124">For a database that is protected using Geo-Replication the drill exercise will involve planned failover to the secondary database.</span></span> <span data-ttu-id="c3273-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span><span class="sxs-lookup"><span data-stu-id="c3273-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="c3273-126">Unlike the unplanned failover, this operation will not result in data loss, so the drill can be performed in the production environment.</span><span class="sxs-lookup"><span data-stu-id="c3273-126">Unlike the unplanned failover, this operation will not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="c3273-127">Outage simulation</span><span class="sxs-lookup"><span data-stu-id="c3273-127">Outage simulation</span></span>
<span data-ttu-id="c3273-128">To simulate the outage you can disable the web application or virtual machine connected to the database.</span><span class="sxs-lookup"><span data-stu-id="c3273-128">To simulate the outage you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="c3273-129">This will result in the connectivity failures for the web clients.</span><span class="sxs-lookup"><span data-stu-id="c3273-129">This will result in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="c3273-130">Recovery</span><span class="sxs-lookup"><span data-stu-id="c3273-130">Recovery</span></span>
* <span data-ttu-id="c3273-131">Make sure the application configuration in the DR region points to the former secondary which will become fully accessible new primary.</span><span class="sxs-lookup"><span data-stu-id="c3273-131">Make sure the application configuration in the DR region points to the former secondary which will become fully accessible new primary.</span></span>
* <span data-ttu-id="c3273-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span><span class="sxs-lookup"><span data-stu-id="c3273-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="c3273-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span><span class="sxs-lookup"><span data-stu-id="c3273-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="c3273-134">Validation</span><span class="sxs-lookup"><span data-stu-id="c3273-134">Validation</span></span>
* <span data-ttu-id="c3273-135">Complete the drill by verifying the application integrity post recovery (i.e. connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span><span class="sxs-lookup"><span data-stu-id="c3273-135">Complete the drill by verifying the application integrity post recovery (i.e. connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3273-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3273-136">Next steps</span></span>
* <span data-ttu-id="c3273-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="c3273-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="c3273-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c3273-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="c3273-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c3273-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="c3273-140">To learn about faster recovery options, see [Active-Geo-Replication](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c3273-140">To learn about faster recovery options, see [Active-Geo-Replication](sql-database-geo-replication-overview.md)</span></span>  
