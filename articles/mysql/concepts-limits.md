---
title: Limitations in Azure Database for MySQL
description: This article describes limitations in Azure Database for MySQL, such as number of connection and storage engine options.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 06/30/2018
ms.openlocfilehash: 1fd5905b8ea3f87fe6cfc2a830b73b8120a717dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871588"
---
# <a name="limitations-in-azure-database-for-mysql"></a><span data-ttu-id="cca4f-103">Limitations in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="cca4f-103">Limitations in Azure Database for MySQL</span></span>
<span data-ttu-id="cca4f-104">The following sections describe capacity, storage engine support, privilege support, data manipulation statement support, and functional limits in the database service.</span><span class="sxs-lookup"><span data-stu-id="cca4f-104">The following sections describe capacity, storage engine support, privilege support, data manipulation statement support, and functional limits in the database service.</span></span> <span data-ttu-id="cca4f-105">Also see [general limitations](https://dev.mysql.com/doc/mysql-reslimits-excerpt/5.6/en/limits.html) applicable to the MySQL database engine.</span><span class="sxs-lookup"><span data-stu-id="cca4f-105">Also see [general limitations](https://dev.mysql.com/doc/mysql-reslimits-excerpt/5.6/en/limits.html) applicable to the MySQL database engine.</span></span>

## <a name="maximum-connections"></a><span data-ttu-id="cca4f-106">Maximum connections</span><span class="sxs-lookup"><span data-stu-id="cca4f-106">Maximum connections</span></span>
<span data-ttu-id="cca4f-107">The maximum number of connections per pricing tier and vCores are as follows:</span><span class="sxs-lookup"><span data-stu-id="cca4f-107">The maximum number of connections per pricing tier and vCores are as follows:</span></span> 

|<span data-ttu-id="cca4f-108">**Pricing Tier**</span><span class="sxs-lookup"><span data-stu-id="cca4f-108">**Pricing Tier**</span></span>|<span data-ttu-id="cca4f-109">**vCore(s)**</span><span class="sxs-lookup"><span data-stu-id="cca4f-109">**vCore(s)**</span></span>| <span data-ttu-id="cca4f-110">**Max Connections**</span><span class="sxs-lookup"><span data-stu-id="cca4f-110">**Max Connections**</span></span>|
|---|---|---|
|<span data-ttu-id="cca4f-111">Basic</span><span class="sxs-lookup"><span data-stu-id="cca4f-111">Basic</span></span>| <span data-ttu-id="cca4f-112">1</span><span class="sxs-lookup"><span data-stu-id="cca4f-112">1</span></span>| <span data-ttu-id="cca4f-113">50</span><span class="sxs-lookup"><span data-stu-id="cca4f-113">50</span></span>|
|<span data-ttu-id="cca4f-114">Basic</span><span class="sxs-lookup"><span data-stu-id="cca4f-114">Basic</span></span>| <span data-ttu-id="cca4f-115">2</span><span class="sxs-lookup"><span data-stu-id="cca4f-115">2</span></span>| <span data-ttu-id="cca4f-116">100</span><span class="sxs-lookup"><span data-stu-id="cca4f-116">100</span></span>|
|<span data-ttu-id="cca4f-117">General Purpose</span><span class="sxs-lookup"><span data-stu-id="cca4f-117">General Purpose</span></span>| <span data-ttu-id="cca4f-118">2</span><span class="sxs-lookup"><span data-stu-id="cca4f-118">2</span></span>| <span data-ttu-id="cca4f-119">300</span><span class="sxs-lookup"><span data-stu-id="cca4f-119">300</span></span>|
|<span data-ttu-id="cca4f-120">General Purpose</span><span class="sxs-lookup"><span data-stu-id="cca4f-120">General Purpose</span></span>| <span data-ttu-id="cca4f-121">4</span><span class="sxs-lookup"><span data-stu-id="cca4f-121">4</span></span>| <span data-ttu-id="cca4f-122">625</span><span class="sxs-lookup"><span data-stu-id="cca4f-122">625</span></span>|
|<span data-ttu-id="cca4f-123">General Purpose</span><span class="sxs-lookup"><span data-stu-id="cca4f-123">General Purpose</span></span>| <span data-ttu-id="cca4f-124">8</span><span class="sxs-lookup"><span data-stu-id="cca4f-124">8</span></span>| <span data-ttu-id="cca4f-125">1250</span><span class="sxs-lookup"><span data-stu-id="cca4f-125">1250</span></span>|
|<span data-ttu-id="cca4f-126">General Purpose</span><span class="sxs-lookup"><span data-stu-id="cca4f-126">General Purpose</span></span>| <span data-ttu-id="cca4f-127">16</span><span class="sxs-lookup"><span data-stu-id="cca4f-127">16</span></span>| <span data-ttu-id="cca4f-128">2500</span><span class="sxs-lookup"><span data-stu-id="cca4f-128">2500</span></span>|
|<span data-ttu-id="cca4f-129">General Purpose</span><span class="sxs-lookup"><span data-stu-id="cca4f-129">General Purpose</span></span>| <span data-ttu-id="cca4f-130">32</span><span class="sxs-lookup"><span data-stu-id="cca4f-130">32</span></span>| <span data-ttu-id="cca4f-131">5000</span><span class="sxs-lookup"><span data-stu-id="cca4f-131">5000</span></span>|
|<span data-ttu-id="cca4f-132">Memory Optimized</span><span class="sxs-lookup"><span data-stu-id="cca4f-132">Memory Optimized</span></span>| <span data-ttu-id="cca4f-133">2</span><span class="sxs-lookup"><span data-stu-id="cca4f-133">2</span></span>| <span data-ttu-id="cca4f-134">600</span><span class="sxs-lookup"><span data-stu-id="cca4f-134">600</span></span>|
|<span data-ttu-id="cca4f-135">Memory Optimized</span><span class="sxs-lookup"><span data-stu-id="cca4f-135">Memory Optimized</span></span>| <span data-ttu-id="cca4f-136">4</span><span class="sxs-lookup"><span data-stu-id="cca4f-136">4</span></span>| <span data-ttu-id="cca4f-137">1250</span><span class="sxs-lookup"><span data-stu-id="cca4f-137">1250</span></span>|
|<span data-ttu-id="cca4f-138">Memory Optimized</span><span class="sxs-lookup"><span data-stu-id="cca4f-138">Memory Optimized</span></span>| <span data-ttu-id="cca4f-139">8</span><span class="sxs-lookup"><span data-stu-id="cca4f-139">8</span></span>| <span data-ttu-id="cca4f-140">2500</span><span class="sxs-lookup"><span data-stu-id="cca4f-140">2500</span></span>|
|<span data-ttu-id="cca4f-141">Memory Optimized</span><span class="sxs-lookup"><span data-stu-id="cca4f-141">Memory Optimized</span></span>| <span data-ttu-id="cca4f-142">16</span><span class="sxs-lookup"><span data-stu-id="cca4f-142">16</span></span>| <span data-ttu-id="cca4f-143">5000</span><span class="sxs-lookup"><span data-stu-id="cca4f-143">5000</span></span>|

<span data-ttu-id="cca4f-144">When connections exceed the limit, you may receive the following error:</span><span class="sxs-lookup"><span data-stu-id="cca4f-144">When connections exceed the limit, you may receive the following error:</span></span>
> <span data-ttu-id="cca4f-145">ERROR 1040 (08004): Too many connections</span><span class="sxs-lookup"><span data-stu-id="cca4f-145">ERROR 1040 (08004): Too many connections</span></span>

## <a name="storage-engine-support"></a><span data-ttu-id="cca4f-146">Storage engine support</span><span class="sxs-lookup"><span data-stu-id="cca4f-146">Storage engine support</span></span>

### <a name="supported"></a><span data-ttu-id="cca4f-147">Supported</span><span class="sxs-lookup"><span data-stu-id="cca4f-147">Supported</span></span>
- [<span data-ttu-id="cca4f-148">InnoDB</span><span class="sxs-lookup"><span data-stu-id="cca4f-148">InnoDB</span></span>](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html)
- [<span data-ttu-id="cca4f-149">MEMORY</span><span class="sxs-lookup"><span data-stu-id="cca4f-149">MEMORY</span></span>](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html)

### <a name="unsupported"></a><span data-ttu-id="cca4f-150">Unsupported</span><span class="sxs-lookup"><span data-stu-id="cca4f-150">Unsupported</span></span>
- [<span data-ttu-id="cca4f-151">MyISAM</span><span class="sxs-lookup"><span data-stu-id="cca4f-151">MyISAM</span></span>](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html)
- [<span data-ttu-id="cca4f-152">BLACKHOLE</span><span class="sxs-lookup"><span data-stu-id="cca4f-152">BLACKHOLE</span></span>](https://dev.mysql.com/doc/refman/5.7/en/blackhole-storage-engine.html)
- [<span data-ttu-id="cca4f-153">ARCHIVE</span><span class="sxs-lookup"><span data-stu-id="cca4f-153">ARCHIVE</span></span>](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html)
- [<span data-ttu-id="cca4f-154">FEDERATED</span><span class="sxs-lookup"><span data-stu-id="cca4f-154">FEDERATED</span></span>](https://dev.mysql.com/doc/refman/5.7/en/federated-storage-engine.html)

## <a name="privilege-support"></a><span data-ttu-id="cca4f-155">Privilege support</span><span class="sxs-lookup"><span data-stu-id="cca4f-155">Privilege support</span></span>

### <a name="unsupported"></a><span data-ttu-id="cca4f-156">Unsupported</span><span class="sxs-lookup"><span data-stu-id="cca4f-156">Unsupported</span></span>
- <span data-ttu-id="cca4f-157">DBA role: Many server parameters and settings can inadvertently degrade server performance or negate ACID properties of the DBMS.</span><span class="sxs-lookup"><span data-stu-id="cca4f-157">DBA role: Many server parameters and settings can inadvertently degrade server performance or negate ACID properties of the DBMS.</span></span> <span data-ttu-id="cca4f-158">As such, to maintain the service integrity and SLA at a product level, this service does not expose the DBA role.</span><span class="sxs-lookup"><span data-stu-id="cca4f-158">As such, to maintain the service integrity and SLA at a product level, this service does not expose the DBA role.</span></span> <span data-ttu-id="cca4f-159">The default user account, which is constructed when a new database instance is created, allows that user to perform most of DDL and DML statements in the managed database instance.</span><span class="sxs-lookup"><span data-stu-id="cca4f-159">The default user account, which is constructed when a new database instance is created, allows that user to perform most of DDL and DML statements in the managed database instance.</span></span> 
- <span data-ttu-id="cca4f-160">SUPER privilege: Similarly [SUPER privilege](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_super) is also restricted.</span><span class="sxs-lookup"><span data-stu-id="cca4f-160">SUPER privilege: Similarly [SUPER privilege](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_super) is also restricted.</span></span>

## <a name="data-manipulation-statement-support"></a><span data-ttu-id="cca4f-161">Data manipulation statement support</span><span class="sxs-lookup"><span data-stu-id="cca4f-161">Data manipulation statement support</span></span>

### <a name="supported"></a><span data-ttu-id="cca4f-162">Supported</span><span class="sxs-lookup"><span data-stu-id="cca4f-162">Supported</span></span>
- <span data-ttu-id="cca4f-163">`LOAD DATA INFILE` is supported, but the `[LOCAL]` parameter must be specified and directed to a UNC path (Azure storage mounted through SMB).</span><span class="sxs-lookup"><span data-stu-id="cca4f-163">`LOAD DATA INFILE` is supported, but the `[LOCAL]` parameter must be specified and directed to a UNC path (Azure storage mounted through SMB).</span></span>

### <a name="unsupported"></a><span data-ttu-id="cca4f-164">Unsupported</span><span class="sxs-lookup"><span data-stu-id="cca4f-164">Unsupported</span></span>
- `SELECT ... INTO OUTFILE`

## <a name="functional-limitations"></a><span data-ttu-id="cca4f-165">Functional limitations</span><span class="sxs-lookup"><span data-stu-id="cca4f-165">Functional limitations</span></span>

### <a name="scale-operations"></a><span data-ttu-id="cca4f-166">Scale operations</span><span class="sxs-lookup"><span data-stu-id="cca4f-166">Scale operations</span></span>
- <span data-ttu-id="cca4f-167">Dynamic scaling to and from the Basic pricing tiers is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="cca4f-167">Dynamic scaling to and from the Basic pricing tiers is currently not supported.</span></span>
- <span data-ttu-id="cca4f-168">Decreasing server storage size is not supported.</span><span class="sxs-lookup"><span data-stu-id="cca4f-168">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="cca4f-169">Server version upgrades</span><span class="sxs-lookup"><span data-stu-id="cca4f-169">Server version upgrades</span></span>
- <span data-ttu-id="cca4f-170">Automated migration between major database engine versions is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="cca4f-170">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="cca4f-171">Point-in-time-restore</span><span class="sxs-lookup"><span data-stu-id="cca4f-171">Point-in-time-restore</span></span>
- <span data-ttu-id="cca4f-172">When using the PITR feature, the new server is created with the same configurations as the server it is based on.</span><span class="sxs-lookup"><span data-stu-id="cca4f-172">When using the PITR feature, the new server is created with the same configurations as the server it is based on.</span></span>
- <span data-ttu-id="cca4f-173">Restoring a deleted server is not supported.</span><span class="sxs-lookup"><span data-stu-id="cca4f-173">Restoring a deleted server is not supported.</span></span>

### <a name="vnet-service-endpoints"></a><span data-ttu-id="cca4f-174">VNet service endpoints</span><span class="sxs-lookup"><span data-stu-id="cca4f-174">VNet service endpoints</span></span>
- <span data-ttu-id="cca4f-175">Support for VNet service endpoints is only for General Purpose and Memory Optimized servers.</span><span class="sxs-lookup"><span data-stu-id="cca4f-175">Support for VNet service endpoints is only for General Purpose and Memory Optimized servers.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="cca4f-176">Subscription management</span><span class="sxs-lookup"><span data-stu-id="cca4f-176">Subscription management</span></span>
- <span data-ttu-id="cca4f-177">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="cca4f-177">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

## <a name="current-known-issues"></a><span data-ttu-id="cca4f-178">Current known issues</span><span class="sxs-lookup"><span data-stu-id="cca4f-178">Current known issues</span></span>
- <span data-ttu-id="cca4f-179">MySQL server instance displays the wrong server version after connection is established.</span><span class="sxs-lookup"><span data-stu-id="cca4f-179">MySQL server instance displays the wrong server version after connection is established.</span></span> <span data-ttu-id="cca4f-180">To get the correct server instance engine version, use the `select version();` command.</span><span class="sxs-lookup"><span data-stu-id="cca4f-180">To get the correct server instance engine version, use the `select version();` command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cca4f-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="cca4f-181">Next steps</span></span>
- [<span data-ttu-id="cca4f-182">What’s available in each service tier</span><span class="sxs-lookup"><span data-stu-id="cca4f-182">What’s available in each service tier</span></span>](concepts-pricing-tiers.md)
- [<span data-ttu-id="cca4f-183">Supported MySQL database versions</span><span class="sxs-lookup"><span data-stu-id="cca4f-183">Supported MySQL database versions</span></span>](concepts-supported-versions.md)
