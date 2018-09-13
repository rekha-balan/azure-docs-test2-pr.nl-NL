---
title: Data dependent routing with Azure SQL Database | Microsoft Docs
description: How to use the ShardMapManager class in .NET apps for data-dependent routing, a feature of sharded databases in  Azure SQL Database
services: sql-database
documentationcenter: ''
manager: jhubbard
author: torsteng
editor: ''
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: ff9f3ee4e44f7d0b51a6724304b0ec0f967f7d88
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556735"
---
# <a name="data-dependent-routing"></a><span data-ttu-id="8123c-103">Data dependent routing</span><span class="sxs-lookup"><span data-stu-id="8123c-103">Data dependent routing</span></span>
<span data-ttu-id="8123c-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span><span class="sxs-lookup"><span data-stu-id="8123c-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="8123c-105">This is a fundamental pattern when working with sharded databases.</span><span class="sxs-lookup"><span data-stu-id="8123c-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="8123c-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span><span class="sxs-lookup"><span data-stu-id="8123c-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="8123c-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span><span class="sxs-lookup"><span data-stu-id="8123c-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="8123c-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span><span class="sxs-lookup"><span data-stu-id="8123c-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="8123c-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span><span class="sxs-lookup"><span data-stu-id="8123c-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="8123c-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span><span class="sxs-lookup"><span data-stu-id="8123c-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="8123c-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span><span class="sxs-lookup"><span data-stu-id="8123c-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="8123c-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="8123c-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="8123c-113">Download the client library</span><span class="sxs-lookup"><span data-stu-id="8123c-113">Download the client library</span></span>
<span data-ttu-id="8123c-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="8123c-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="8123c-115">Using a ShardMapManager in a data dependent routing application</span><span class="sxs-lookup"><span data-stu-id="8123c-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="8123c-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="8123c-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="8123c-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span><span class="sxs-lookup"><span data-stu-id="8123c-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="8123c-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span><span class="sxs-lookup"><span data-stu-id="8123c-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="8123c-119">Use lowest privilege credentials possible for getting the shard map</span><span class="sxs-lookup"><span data-stu-id="8123c-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="8123c-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span><span class="sxs-lookup"><span data-stu-id="8123c-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="8123c-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span><span class="sxs-lookup"><span data-stu-id="8123c-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="8123c-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="8123c-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="8123c-123">Call the OpenConnectionForKey method</span><span class="sxs-lookup"><span data-stu-id="8123c-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="8123c-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span><span class="sxs-lookup"><span data-stu-id="8123c-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="8123c-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span><span class="sxs-lookup"><span data-stu-id="8123c-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="8123c-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span><span class="sxs-lookup"><span data-stu-id="8123c-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="8123c-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span><span class="sxs-lookup"><span data-stu-id="8123c-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="8123c-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="8123c-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="8123c-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span><span class="sxs-lookup"><span data-stu-id="8123c-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="8123c-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span><span class="sxs-lookup"><span data-stu-id="8123c-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="8123c-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span><span class="sxs-lookup"><span data-stu-id="8123c-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="8123c-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span><span class="sxs-lookup"><span data-stu-id="8123c-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="8123c-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span><span class="sxs-lookup"><span data-stu-id="8123c-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="8123c-134">That reduces database traffic.</span><span class="sxs-lookup"><span data-stu-id="8123c-134">That reduces database traffic.</span></span> <span data-ttu-id="8123c-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span><span class="sxs-lookup"><span data-stu-id="8123c-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="8123c-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="8123c-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="8123c-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span><span class="sxs-lookup"><span data-stu-id="8123c-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="8123c-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span><span class="sxs-lookup"><span data-stu-id="8123c-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="8123c-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="8123c-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="8123c-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="8123c-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="8123c-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span><span class="sxs-lookup"><span data-stu-id="8123c-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="8123c-142">Integrating with transient fault handling</span><span class="sxs-lookup"><span data-stu-id="8123c-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="8123c-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span><span class="sxs-lookup"><span data-stu-id="8123c-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="8123c-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="8123c-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="8123c-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span><span class="sxs-lookup"><span data-stu-id="8123c-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="8123c-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span><span class="sxs-lookup"><span data-stu-id="8123c-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="8123c-147">The example above could be rewritten as follows (note highlighted change).</span><span class="sxs-lookup"><span data-stu-id="8123c-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="8123c-148">Example - data dependent routing with transient fault handling</span><span class="sxs-lookup"><span data-stu-id="8123c-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="8123c-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span><span class="sxs-lookup"><span data-stu-id="8123c-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="8123c-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="8123c-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="8123c-151">Use version 6.0 or later.</span><span class="sxs-lookup"><span data-stu-id="8123c-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="8123c-152">Transactional consistency</span><span class="sxs-lookup"><span data-stu-id="8123c-152">Transactional consistency</span></span>
<span data-ttu-id="8123c-153">Transactional properties are guaranteed for all operations local to a shard.</span><span class="sxs-lookup"><span data-stu-id="8123c-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="8123c-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span><span class="sxs-lookup"><span data-stu-id="8123c-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="8123c-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span><span class="sxs-lookup"><span data-stu-id="8123c-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8123c-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="8123c-156">Next steps</span></span>
<span data-ttu-id="8123c-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="8123c-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

