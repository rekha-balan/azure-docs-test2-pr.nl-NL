---
title: Configure Azure SQL Database security for disaster recovery | Microsoft Docs
description: This topic explains security considerations for configuring and managing security after a database restore or a failover to a secondary server in the event of a data center outage or other disaster
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: a1cefadf243f7038605758f1a8dbd52cc787b721
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563551"
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="f3e3e-103">Configure and manage Azure SQL Database security for geo-restore or failover</span><span class="sxs-lookup"><span data-stu-id="f3e3e-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="f3e3e-104">[Active Geo-Replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-104">[Active Geo-Replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="f3e3e-105">Overview of authentication requirements for disaster recovery</span><span class="sxs-lookup"><span data-stu-id="f3e3e-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="f3e3e-106">This topic describes the authentication requirements to configure and control [Active Geo-Replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-106">This topic describes the authentication requirements to configure and control [Active Geo-Replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="f3e3e-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="f3e3e-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="f3e3e-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="f3e3e-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="f3e3e-109">Disaster recovery with contained users</span><span class="sxs-lookup"><span data-stu-id="f3e3e-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="f3e3e-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="f3e3e-111">This has two benefits.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-111">This has two benefits.</span></span> <span data-ttu-id="f3e3e-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="f3e3e-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="f3e3e-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e3e-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="f3e3e-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="f3e3e-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple database may negate the benefits of contained users.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple database may negate the benefits of contained users.</span></span> <span data-ttu-id="f3e3e-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="f3e3e-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="f3e3e-119">How to configure logins and users</span><span class="sxs-lookup"><span data-stu-id="f3e3e-119">How to configure logins and users</span></span>
<span data-ttu-id="f3e3e-120">If you are using logins and users (rather than contained users), you must make take extra steps to insure that the same logins exist in the master database.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-120">If you are using logins and users (rather than contained users), you must make take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="f3e3e-121">The following sections outline the steps involved and additional considerations.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-121">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="f3e3e-122">Set up user access to a secondary or recovered database</span><span class="sxs-lookup"><span data-stu-id="f3e3e-122">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="f3e3e-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="f3e3e-124">The specific permissions for each step are described later in this topic.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-124">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="f3e3e-125">Preparing user access to a Geo-Replication secondary should be performed as part configuring Geo-Replication.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-125">Preparing user access to a Geo-Replication secondary should be performed as part configuring Geo-Replication.</span></span> <span data-ttu-id="f3e3e-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span><span class="sxs-lookup"><span data-stu-id="f3e3e-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="f3e3e-127">If you failover or geo-restore to a server that does not have properly configured logins access to it will be limited to the server admin account.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-127">If you failover or geo-restore to a server that does not have properly configured logins access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="f3e3e-128">Setting up logins on the target server involves three steps outlined below:</span><span class="sxs-lookup"><span data-stu-id="f3e3e-128">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="f3e3e-129">1. Determine logins with access to the primary database:</span><span class="sxs-lookup"><span data-stu-id="f3e3e-129">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="f3e3e-130">The first step of the process is to determine which logins must be duplicated on the target server.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-130">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="f3e3e-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="f3e3e-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="f3e3e-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="f3e3e-134">2. Find the SID for the logins identified in step 1:</span><span class="sxs-lookup"><span data-stu-id="f3e3e-134">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="f3e3e-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="f3e3e-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="f3e3e-137">The following query can be used to see all of the user principals and their SIDs in a database.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-137">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="f3e3e-138">Only a member of the db_owner database role or server admin can run this query.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-138">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="f3e3e-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="f3e3e-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="f3e3e-141">3. Create the logins on the target server:</span><span class="sxs-lookup"><span data-stu-id="f3e3e-141">3. Create the logins on the target server:</span></span>
<span data-ttu-id="f3e3e-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="f3e3e-143">The basic syntax is as follows.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-143">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="f3e3e-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="f3e3e-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="f3e3e-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="f3e3e-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span><span class="sxs-lookup"><span data-stu-id="f3e3e-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f3e3e-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3e3e-147">Next steps</span></span>
* <span data-ttu-id="f3e3e-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="f3e3e-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="f3e3e-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e3e-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="f3e3e-150">For information about using and configuring Active Geo-Replication, see [Active Geo-Replication](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f3e3e-150">For information about using and configuring Active Geo-Replication, see [Active Geo-Replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="f3e3e-151">For informatin about using Geo-Restore, see [Geo-Restore](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="f3e3e-151">For informatin about using Geo-Restore, see [Geo-Restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

