---
title: Managing credentials in the elastic database client library | Microsoft Docs
description: How to set the right level of credentials, admin to read-only, for elastic database apps
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 16e8c4ba332cbaba86a13d7b815d0561618cb28b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552720"
---
# <a name="credentials-used-to-access-the-elastic-database-client-library"></a><span data-ttu-id="d2688-103">Credentials used to access the Elastic Database client library</span><span class="sxs-lookup"><span data-stu-id="d2688-103">Credentials used to access the Elastic Database client library</span></span>
<span data-ttu-id="d2688-104">The [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials to access the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="d2688-104">The [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials to access the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="d2688-105">Depending on the need, use the credential with  the lowest level of access possible.</span><span class="sxs-lookup"><span data-stu-id="d2688-105">Depending on the need, use the credential with  the lowest level of access possible.</span></span>

* <span data-ttu-id="d2688-106">**Management credentials**: for creating or manipulating a shard map manager.</span><span class="sxs-lookup"><span data-stu-id="d2688-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="d2688-107">(See the [glossary](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="d2688-107">(See the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="d2688-108">**Access credentials**: to access an existing shard map manager to obtain information about shards.</span><span class="sxs-lookup"><span data-stu-id="d2688-108">**Access credentials**: to access an existing shard map manager to obtain information about shards.</span></span>
* <span data-ttu-id="d2688-109">**Connection credentials**: to connect to shards.</span><span class="sxs-lookup"><span data-stu-id="d2688-109">**Connection credentials**: to connect to shards.</span></span> 

<span data-ttu-id="d2688-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="d2688-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="d2688-111">About management credentials</span><span class="sxs-lookup"><span data-stu-id="d2688-111">About management credentials</span></span>
<span data-ttu-id="d2688-112">Management credentials are used to create a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span><span class="sxs-lookup"><span data-stu-id="d2688-112">Management credentials are used to create a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="d2688-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) The user of the elastic scale client library creates the SQL users and SQL logins and makes sure each is granted the read/write permissions on the global shard map database and all shard databases as well.</span><span class="sxs-lookup"><span data-stu-id="d2688-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) The user of the elastic scale client library creates the SQL users and SQL logins and makes sure each is granted the read/write permissions on the global shard map database and all shard databases as well.</span></span> <span data-ttu-id="d2688-114">These credentials are used to maintain the global shard map and the local shard maps when changes to the shard map are performed.</span><span class="sxs-lookup"><span data-stu-id="d2688-114">These credentials are used to maintain the global shard map and the local shard maps when changes to the shard map are performed.</span></span> <span data-ttu-id="d2688-115">For instance, use the management credentials to create the shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span><span class="sxs-lookup"><span data-stu-id="d2688-115">For instance, use the management credentials to create the shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="d2688-116">The variable **smmAdminConnectionString** is a connection string that contains the management credentials.</span><span class="sxs-lookup"><span data-stu-id="d2688-116">The variable **smmAdminConnectionString** is a connection string that contains the management credentials.</span></span> <span data-ttu-id="d2688-117">The user ID and password provides read/write access to both shard map database and individual shards.</span><span class="sxs-lookup"><span data-stu-id="d2688-117">The user ID and password provides read/write access to both shard map database and individual shards.</span></span> <span data-ttu-id="d2688-118">The management connection string also includes the server name and database name to identify the global shard map database.</span><span class="sxs-lookup"><span data-stu-id="d2688-118">The management connection string also includes the server name and database name to identify the global shard map database.</span></span> <span data-ttu-id="d2688-119">Here is a typical connection string for that purpose:</span><span class="sxs-lookup"><span data-stu-id="d2688-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="d2688-120">Do not use values in the form of "username@server"—instead just use the "username" value.</span><span class="sxs-lookup"><span data-stu-id="d2688-120">Do not use values in the form of "username@server"—instead just use the "username" value.</span></span>  <span data-ttu-id="d2688-121">This is because credentials must work against both the shard map manager database and individual shards, which may be on different servers.</span><span class="sxs-lookup"><span data-stu-id="d2688-121">This is because credentials must work against both the shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="d2688-122">Access credentials</span><span class="sxs-lookup"><span data-stu-id="d2688-122">Access credentials</span></span>
<span data-ttu-id="d2688-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on the global shard map.</span><span class="sxs-lookup"><span data-stu-id="d2688-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on the global shard map.</span></span> <span data-ttu-id="d2688-124">The information retrieved from the global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and to populate the shard map cache on the client.</span><span class="sxs-lookup"><span data-stu-id="d2688-124">The information retrieved from the global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and to populate the shard map cache on the client.</span></span> <span data-ttu-id="d2688-125">The credentials are provided through the same call pattern to **GetSqlShardMapManager** as shown above:</span><span class="sxs-lookup"><span data-stu-id="d2688-125">The credentials are provided through the same call pattern to **GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="d2688-126">Note the use of the **smmReadOnlyConnectionString** to reflect the use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on the global shard map.</span><span class="sxs-lookup"><span data-stu-id="d2688-126">Note the use of the **smmReadOnlyConnectionString** to reflect the use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on the global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="d2688-127">Connection credentials</span><span class="sxs-lookup"><span data-stu-id="d2688-127">Connection credentials</span></span>
<span data-ttu-id="d2688-128">Additional credentials are needed when using the [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method to access a shard associated with a sharding key.</span><span class="sxs-lookup"><span data-stu-id="d2688-128">Additional credentials are needed when using the [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method to access a shard associated with a sharding key.</span></span> <span data-ttu-id="d2688-129">These credentials need to provide permissions for read-only access to the local shard map tables residing on the shard.</span><span class="sxs-lookup"><span data-stu-id="d2688-129">These credentials need to provide permissions for read-only access to the local shard map tables residing on the shard.</span></span> <span data-ttu-id="d2688-130">This is needed to perform connection validation for data-dependent routing on the shard.</span><span class="sxs-lookup"><span data-stu-id="d2688-130">This is needed to perform connection validation for data-dependent routing on the shard.</span></span> <span data-ttu-id="d2688-131">This code snippet allows data access in the context of data dependent routing:</span><span class="sxs-lookup"><span data-stu-id="d2688-131">This code snippet allows data access in the context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="d2688-132">In this example, **smmUserConnectionString** holds the connection string for the user credentials.</span><span class="sxs-lookup"><span data-stu-id="d2688-132">In this example, **smmUserConnectionString** holds the connection string for the user credentials.</span></span> <span data-ttu-id="d2688-133">For Azure SQL DB, here is a typical connection string for user credentials:</span><span class="sxs-lookup"><span data-stu-id="d2688-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="d2688-134">As with the admin credentials, do not values in the form of "username@server".</span><span class="sxs-lookup"><span data-stu-id="d2688-134">As with the admin credentials, do not values in the form of "username@server".</span></span> <span data-ttu-id="d2688-135">Instead, just use "username".</span><span class="sxs-lookup"><span data-stu-id="d2688-135">Instead, just use "username".</span></span>  <span data-ttu-id="d2688-136">Also note that the connection string does not contain a server name and database name.</span><span class="sxs-lookup"><span data-stu-id="d2688-136">Also note that the connection string does not contain a server name and database name.</span></span> <span data-ttu-id="d2688-137">That is because the **OpenConnectionForKey** call will automatically direct the connection to the correct shard based on the key.</span><span class="sxs-lookup"><span data-stu-id="d2688-137">That is because the **OpenConnectionForKey** call will automatically direct the connection to the correct shard based on the key.</span></span> <span data-ttu-id="d2688-138">Hence, the database name and server name are not provided.</span><span class="sxs-lookup"><span data-stu-id="d2688-138">Hence, the database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="d2688-139">See also</span><span class="sxs-lookup"><span data-stu-id="d2688-139">See also</span></span>
[<span data-ttu-id="d2688-140">Managing databases and logins in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d2688-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="d2688-141">Securing your SQL Database</span><span class="sxs-lookup"><span data-stu-id="d2688-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="d2688-142">Getting started with Elastic Database jobs</span><span class="sxs-lookup"><span data-stu-id="d2688-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

