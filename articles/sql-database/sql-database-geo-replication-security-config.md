---
title: Configure Azure SQL Database security for disaster recovery | Microsoft Docs
description: Learn the security considerations for configuring and managing security after a database restore or a failover to a secondary server.
services: sql-database
author: anosov1960
manager: craigg
ms.service: sql-database
ms.custom: business continuity
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: sashan
ms.openlocfilehash: 0796e5900bc67d93e51a0ce377ef5d1144346e2c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784659"
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="0f358-103">Configure and manage Azure SQL Database security for geo-restore or failover</span><span class="sxs-lookup"><span data-stu-id="0f358-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

<span data-ttu-id="0f358-104">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span><span class="sxs-lookup"><span data-stu-id="0f358-104">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="0f358-105">It also describes how to enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="0f358-105">It also describes how to enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="0f358-106">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="0f358-106">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0f358-107">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span><span class="sxs-lookup"><span data-stu-id="0f358-107">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="0f358-108">Disaster recovery with contained users</span><span class="sxs-lookup"><span data-stu-id="0f358-108">Disaster recovery with contained users</span></span>
<span data-ttu-id="0f358-109">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span><span class="sxs-lookup"><span data-stu-id="0f358-109">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="0f358-110">This has two benefits.</span><span class="sxs-lookup"><span data-stu-id="0f358-110">This has two benefits.</span></span> <span data-ttu-id="0f358-111">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span><span class="sxs-lookup"><span data-stu-id="0f358-111">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="0f358-112">There are also potential scalability and performance benefits from this configuration from a login perspective.</span><span class="sxs-lookup"><span data-stu-id="0f358-112">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="0f358-113">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f358-113">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="0f358-114">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span><span class="sxs-lookup"><span data-stu-id="0f358-114">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="0f358-115">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span><span class="sxs-lookup"><span data-stu-id="0f358-115">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span></span> <span data-ttu-id="0f358-116">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span><span class="sxs-lookup"><span data-stu-id="0f358-116">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="0f358-117">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span><span class="sxs-lookup"><span data-stu-id="0f358-117">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="0f358-118">How to configure logins and users</span><span class="sxs-lookup"><span data-stu-id="0f358-118">How to configure logins and users</span></span>
<span data-ttu-id="0f358-119">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span><span class="sxs-lookup"><span data-stu-id="0f358-119">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="0f358-120">The following sections outline the steps involved and additional considerations.</span><span class="sxs-lookup"><span data-stu-id="0f358-120">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="0f358-121">Set up user access to a secondary or recovered database</span><span class="sxs-lookup"><span data-stu-id="0f358-121">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="0f358-122">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span><span class="sxs-lookup"><span data-stu-id="0f358-122">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="0f358-123">The specific permissions for each step are described later in this topic.</span><span class="sxs-lookup"><span data-stu-id="0f358-123">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="0f358-124">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span><span class="sxs-lookup"><span data-stu-id="0f358-124">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="0f358-125">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span><span class="sxs-lookup"><span data-stu-id="0f358-125">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="0f358-126">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span><span class="sxs-lookup"><span data-stu-id="0f358-126">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="0f358-127">Setting up logins on the target server involves three steps outlined below:</span><span class="sxs-lookup"><span data-stu-id="0f358-127">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="0f358-128">1. Determine logins with access to the primary database:</span><span class="sxs-lookup"><span data-stu-id="0f358-128">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="0f358-129">The first step of the process is to determine which logins must be duplicated on the target server.</span><span class="sxs-lookup"><span data-stu-id="0f358-129">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="0f358-130">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span><span class="sxs-lookup"><span data-stu-id="0f358-130">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="0f358-131">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="0f358-131">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="0f358-132">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span><span class="sxs-lookup"><span data-stu-id="0f358-132">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="0f358-133">2. Find the SID for the logins identified in step 1:</span><span class="sxs-lookup"><span data-stu-id="0f358-133">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="0f358-134">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span><span class="sxs-lookup"><span data-stu-id="0f358-134">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="0f358-135">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span><span class="sxs-lookup"><span data-stu-id="0f358-135">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="0f358-136">The following query can be used to see all of the user principals and their SIDs in a database.</span><span class="sxs-lookup"><span data-stu-id="0f358-136">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="0f358-137">Only a member of the db_owner database role or server admin can run this query.</span><span class="sxs-lookup"><span data-stu-id="0f358-137">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="0f358-138">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span><span class="sxs-lookup"><span data-stu-id="0f358-138">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="0f358-139">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="0f358-139">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="0f358-140">3. Create the logins on the target server:</span><span class="sxs-lookup"><span data-stu-id="0f358-140">3. Create the logins on the target server:</span></span>
<span data-ttu-id="0f358-141">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span><span class="sxs-lookup"><span data-stu-id="0f358-141">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="0f358-142">The basic syntax is as follows.</span><span class="sxs-lookup"><span data-stu-id="0f358-142">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="0f358-143">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span><span class="sxs-lookup"><span data-stu-id="0f358-143">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="0f358-144">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="0f358-144">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="0f358-145">DISABLE doesn’t change the password, so you can always enable it if needed.</span><span class="sxs-lookup"><span data-stu-id="0f358-145">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0f358-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f358-146">Next steps</span></span>
* <span data-ttu-id="0f358-147">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="0f358-147">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="0f358-148">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f358-148">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="0f358-149">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0f358-149">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="0f358-150">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="0f358-150">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

