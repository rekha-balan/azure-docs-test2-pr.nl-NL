---
title: Data dependent routing with Azure SQL Database | Microsoft Docs
description: How to use the ShardMapManager class in .NET apps for data-dependent routing, a feature of sharded databases in  Azure SQL Database
services: sql-database
manager: craigg
author: stevestein
ms.service: sql-database
ms.custom: scale out apps
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: sstein
ms.openlocfilehash: 715b6e55b053b3f999f3bd938c14d72a8e20ad1a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780798"
---
# <a name="data-dependent-routing"></a>Data dependent routing
**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database. This is a fundamental pattern when working with sharded databases. The request context may also be used to route the request, especially if the sharding key is not part of the query. Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request. For the Azure SQL Database Elastic tools, this routing is accomplished with the **ShardMapManager** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)) class.

The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment. Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request. The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request. 

For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-the-client-library"></a>Download the client library
To download:
* The Java version of the library, see [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Celastic-db-tools).
* The .NET version of the library, see [NuGet](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Using a ShardMapManager in a data dependent routing application
Applications should instantiate the **ShardMapManager** during initialization, using the factory call **GetSQLShardMapManager** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.getsqlshardmapmanager), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)). In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized. This example shows the GetSqlShardMapManager and GetRangeShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.getrangeshardmap), [.NET](https://msdn.microsoft.com/library/azure/dn824173.aspx)) methods.

```Java
ShardMapManager smm = ShardMapManagerFactory.getSqlShardMapManager(connectionString, ShardMapManagerLoadPolicy.Lazy);
RangeShardMap<int> rangeShardMap = smm.getRangeShardMap(Configuration.getRangeShardMapName(), ShardKeyType.Int32);
```

```csharp
ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, ShardMapManagerLoadPolicy.Lazy);
RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 
```

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a>Use lowest privilege credentials possible for getting the shard map
If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database. These credentials are typically different from credentials used to open connections to the shard map manager. See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-the-openconnectionforkey-method"></a>Call the OpenConnectionForKey method
The **ShardMap.OpenConnectionForKey method** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapper._list_shard_mapper.openconnectionforkey), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)) returns a connection ready for issuing commands to the appropriate database based on the value of the **key** parameter. Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database. 

```Java
// Syntax: 
public Connection openConnectionForKey(Object key, String connectionString, ConnectionOptions options)
```

```csharp
// Syntax: 
public SqlConnection OpenConnectionForKey<TKey>(TKey key, string connectionString, ConnectionOptions options)
```
* The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request. 
* The **connectionString** is used to pass only the user credentials for the desired connection. No database name or server name is included in this *connectionString* since the method determines the database and server using the **ShardMap**. 
* The **connectionOptions** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapper._connection_options), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)) should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations. This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application. 

If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager queries the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection. 

Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online. In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped. That reduces database traffic. The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.  

This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.  

```Java 
int customerId = 12345; 
int productId = 4321; 
// Looks up the key in the shard map and opens a connection to the shard
try (Connection conn = shardMap.openConnectionForKey(customerId, Configuration.getCredentialsConnectionString())) {
    // Create a simple command that will insert or update the customer information
    PreparedStatement ps = conn.prepareStatement("UPDATE Sales.Customer SET PersonID = ? WHERE CustomerID = ?");

    ps.setInt(1, productId);
    ps.setInt(2, customerId);
    ps.executeUpdate();
} catch (SQLException e) {
    e.printStackTrace();
}
```

```csharp
int customerId = 12345; 
int newPersonId = 4321; 

// Connect to the shard for that customer ID. No need to call a SqlConnection 
// constructor followed by the Open method.
using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
{ 
    // Execute a simple command. 
    SqlCommand cmd = conn.CreateCommand(); 
    cmd.CommandText = @"UPDATE Sales.Customer 
                        SET PersonID = @newPersonID WHERE CustomerID = @customerID"; 

    cmd.Parameters.AddWithValue("@customerID", customerId);cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
    cmd.ExecuteNonQuery(); 
}  
```

The **OpenConnectionForKey** method returns a new already-open connection to the correct database. Connections utilized in this way still take full advantage of connection pooling. 

The **OpenConnectionForKeyAsync method** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapper._list_shard_mapper.openconnectionforkeyasync), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)) is also available if your application makes use asynchronous programming.

## <a name="integrating-with-transient-fault-handling"></a>Integrating with transient fault handling
A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error. Transient fault handling for cloud applications is discussed at Transient Fault Handling ([Java](/java/api/com.microsoft.azure.elasticdb.core.commons.transientfaulthandling), [.NET](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx)). 

Transient fault handling can coexist naturally with the Data Dependent Routing pattern. The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection. The preceding example could be rewritten as follows. 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Example - data dependent routing with transient fault handling
```Java 
int customerId = 12345; 
int productId = 4321; 
try {
    SqlDatabaseUtils.getSqlRetryPolicy().executeAction(() -> {
        // Looks up the key in the shard map and opens a connection to the shard
        try (Connection conn = shardMap.openConnectionForKey(customerId, Configuration.getCredentialsConnectionString())) {
            // Create a simple command that will insert or update the customer information
            PreparedStatement ps = conn.prepareStatement("UPDATE Sales.Customer SET PersonID = ? WHERE CustomerID = ?");

            ps.setInt(1, productId);
            ps.setInt(2, customerId);
            ps.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    });
} catch (Exception e) {
    throw new StoreException(e.getMessage(), e);
}
```

```csharp
int customerId = 12345; 
int newPersonId = 4321; 

Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; 
{
    // Connect to the shard for a customer ID. 
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command 
        SqlCommand cmd = conn.CreateCommand(); 

        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 

        Console.WriteLine("Update completed"); 
    } 
}); 
```

Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application. 

## <a name="transactional-consistency"></a>Transactional consistency
Transactional properties are guaranteed for all operations local to a shard. For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection. At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.

## <a name="next-steps"></a>Next steps
To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

