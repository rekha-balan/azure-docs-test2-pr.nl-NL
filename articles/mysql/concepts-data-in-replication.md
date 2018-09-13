---
title: Replicate data into Azure Database for MySQL.
description: This article describes data-in replication for Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 08/31/2018
ms.openlocfilehash: 6135e4a0182f3af7db54eab974e4c307402185ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856602"
---
# <a name="replicate-data-into-azure-database-for-mysql"></a><span data-ttu-id="5011f-103">Replicate data into Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="5011f-103">Replicate data into Azure Database for MySQL</span></span>

<span data-ttu-id="5011f-104">Data-in Replication allows you to synchronize data from a MySQL server running on-premises, in virtual machines, or database services hosted by other cloud providers into the Azure Database for MySQL service.</span><span class="sxs-lookup"><span data-stu-id="5011f-104">Data-in Replication allows you to synchronize data from a MySQL server running on-premises, in virtual machines, or database services hosted by other cloud providers into the Azure Database for MySQL service.</span></span> <span data-ttu-id="5011f-105">Data-in Replication is based on the binary log (binlog) file position-based replication native to MySQL.</span><span class="sxs-lookup"><span data-stu-id="5011f-105">Data-in Replication is based on the binary log (binlog) file position-based replication native to MySQL.</span></span> <span data-ttu-id="5011f-106">To learn more about binlog replication, see the [MySQL binlog replication overview](https://dev.mysql.com/doc/refman/5.7/en/binlog-replication-configuration-overview.html).</span><span class="sxs-lookup"><span data-stu-id="5011f-106">To learn more about binlog replication, see the [MySQL binlog replication overview](https://dev.mysql.com/doc/refman/5.7/en/binlog-replication-configuration-overview.html).</span></span> 

## <a name="when-to-use-data-in-replication"></a><span data-ttu-id="5011f-107">When to use Data-in Replication</span><span class="sxs-lookup"><span data-stu-id="5011f-107">When to use Data-in Replication</span></span>
<span data-ttu-id="5011f-108">The main scenarios to consider using Data-in Replication are:</span><span class="sxs-lookup"><span data-stu-id="5011f-108">The main scenarios to consider using Data-in Replication are:</span></span>

- <span data-ttu-id="5011f-109">**Hybrid Data Synchronization:** With Data-in Replication, you can keep data synchronized between your on-premises servers and Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="5011f-109">**Hybrid Data Synchronization:** With Data-in Replication, you can keep data synchronized between your on-premises servers and Azure Database for MySQL.</span></span> <span data-ttu-id="5011f-110">This synchronization is useful for creating hybrid applications.</span><span class="sxs-lookup"><span data-stu-id="5011f-110">This synchronization is useful for creating hybrid applications.</span></span> <span data-ttu-id="5011f-111">This method is appealing when you have an existing local database server, but want to move the data to a region closer to end users.</span><span class="sxs-lookup"><span data-stu-id="5011f-111">This method is appealing when you have an existing local database server, but want to move the data to a region closer to end users.</span></span>
- <span data-ttu-id="5011f-112">**Multi-Cloud Synchronization:** For complex cloud solutions, use Data-in Replication to synchronize data between Azure Database for MySQL and different cloud providers, including virtual machines and database services hosted in those clouds.</span><span class="sxs-lookup"><span data-stu-id="5011f-112">**Multi-Cloud Synchronization:** For complex cloud solutions, use Data-in Replication to synchronize data between Azure Database for MySQL and different cloud providers, including virtual machines and database services hosted in those clouds.</span></span>

## <a name="limitations-and-considerations"></a><span data-ttu-id="5011f-113">Limitations and considerations</span><span class="sxs-lookup"><span data-stu-id="5011f-113">Limitations and considerations</span></span>

### <a name="data-not-replicated"></a><span data-ttu-id="5011f-114">Data not replicated</span><span class="sxs-lookup"><span data-stu-id="5011f-114">Data not replicated</span></span>
<span data-ttu-id="5011f-115">The [*mysql system database*](https://dev.mysql.com/doc/refman/5.7/en/system-database.html) on the master server is not replicated.</span><span class="sxs-lookup"><span data-stu-id="5011f-115">The [*mysql system database*](https://dev.mysql.com/doc/refman/5.7/en/system-database.html) on the master server is not replicated.</span></span> <span data-ttu-id="5011f-116">Changes to accounts and permissions on the master server are not replicated.</span><span class="sxs-lookup"><span data-stu-id="5011f-116">Changes to accounts and permissions on the master server are not replicated.</span></span> <span data-ttu-id="5011f-117">If you create an account on the master server and this account needs to access the replica server, then manually create the same account on the replica server side.</span><span class="sxs-lookup"><span data-stu-id="5011f-117">If you create an account on the master server and this account needs to access the replica server, then manually create the same account on the replica server side.</span></span> <span data-ttu-id="5011f-118">To understand what tables are contained in the system database, see the [MySQL manual](https://dev.mysql.com/doc/refman/5.7/en/system-database.html).</span><span class="sxs-lookup"><span data-stu-id="5011f-118">To understand what tables are contained in the system database, see the [MySQL manual](https://dev.mysql.com/doc/refman/5.7/en/system-database.html).</span></span>

### <a name="requirements"></a><span data-ttu-id="5011f-119">Requirements</span><span class="sxs-lookup"><span data-stu-id="5011f-119">Requirements</span></span>
- <span data-ttu-id="5011f-120">The master server version must be at least MySQL version 5.6.</span><span class="sxs-lookup"><span data-stu-id="5011f-120">The master server version must be at least MySQL version 5.6.</span></span> 
- <span data-ttu-id="5011f-121">The master and replica server versions must be the same.</span><span class="sxs-lookup"><span data-stu-id="5011f-121">The master and replica server versions must be the same.</span></span> <span data-ttu-id="5011f-122">For example, both must be MySQL version 5.6 or both must be MySQL version 5.7.</span><span class="sxs-lookup"><span data-stu-id="5011f-122">For example, both must be MySQL version 5.6 or both must be MySQL version 5.7.</span></span>
- <span data-ttu-id="5011f-123">Each table must have a primary key.</span><span class="sxs-lookup"><span data-stu-id="5011f-123">Each table must have a primary key.</span></span>
- <span data-ttu-id="5011f-124">Master server should use the MySQL InnoDB engine.</span><span class="sxs-lookup"><span data-stu-id="5011f-124">Master server should use the MySQL InnoDB engine.</span></span>
- <span data-ttu-id="5011f-125">User must have permissions to configure binary logging and create new users on the master server.</span><span class="sxs-lookup"><span data-stu-id="5011f-125">User must have permissions to configure binary logging and create new users on the master server.</span></span>

### <a name="other"></a><span data-ttu-id="5011f-126">Other</span><span class="sxs-lookup"><span data-stu-id="5011f-126">Other</span></span>
- <span data-ttu-id="5011f-127">Data-in replication is only supported in General Purpose and Memory Optimized pricing tiers</span><span class="sxs-lookup"><span data-stu-id="5011f-127">Data-in replication is only supported in General Purpose and Memory Optimized pricing tiers</span></span>
- <span data-ttu-id="5011f-128">Global transaction identifiers (GTID) are not supported.</span><span class="sxs-lookup"><span data-stu-id="5011f-128">Global transaction identifiers (GTID) are not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5011f-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="5011f-129">Next steps</span></span>
- <span data-ttu-id="5011f-130">Learn how to [set up data-in replication](howto-data-in-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5011f-130">Learn how to [set up data-in replication](howto-data-in-replication.md)</span></span>
