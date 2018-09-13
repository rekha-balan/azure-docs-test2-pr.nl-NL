---
title: Secure a database in SQL Data Warehouse | Microsoft Docs
description: Tips for securing a database in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: kavithaj
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: 8abb40b0c1a5b9cd3f8d1e23124090c00e8cfadb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776106"
---
# <a name="secure-a-database-in-sql-data-warehouse"></a><span data-ttu-id="b329f-103">Secure a database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b329f-103">Secure a database in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [Security Overview](sql-data-warehouse-overview-manage-security.md)
> * [Authentication](sql-data-warehouse-authentication.md)
> * [Encryption (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Encryption (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="b329f-108">This article walks through the basics of securing your Azure SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="b329f-108">This article walks through the basics of securing your Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="b329f-109">In particular, this article gets you started with resources for limiting access, protecting data, and monitoring activities on a database.</span><span class="sxs-lookup"><span data-stu-id="b329f-109">In particular, this article gets you started with resources for limiting access, protecting data, and monitoring activities on a database.</span></span>

## <a name="connection-security"></a><span data-ttu-id="b329f-110">Connection security</span><span class="sxs-lookup"><span data-stu-id="b329f-110">Connection security</span></span>
<span data-ttu-id="b329f-111">Connection Security refers to how you restrict and secure connections to your database using firewall rules and connection encryption.</span><span class="sxs-lookup"><span data-stu-id="b329f-111">Connection Security refers to how you restrict and secure connections to your database using firewall rules and connection encryption.</span></span>

<span data-ttu-id="b329f-112">Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that have not been explicitly whitelisted.</span><span class="sxs-lookup"><span data-stu-id="b329f-112">Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that have not been explicitly whitelisted.</span></span> <span data-ttu-id="b329f-113">To allow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using the Azure portal, REST API, or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b329f-113">To allow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using the Azure portal, REST API, or PowerShell.</span></span> <span data-ttu-id="b329f-114">As a best practice, you should restrict the IP address ranges allowed through your server firewall as much as possible.</span><span class="sxs-lookup"><span data-stu-id="b329f-114">As a best practice, you should restrict the IP address ranges allowed through your server firewall as much as possible.</span></span>  <span data-ttu-id="b329f-115">To access Azure SQL Data Warehouse from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span><span class="sxs-lookup"><span data-stu-id="b329f-115">To access Azure SQL Data Warehouse from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>  

<span data-ttu-id="b329f-116">SQL Data Warehouse uses server-level firewall rules.</span><span class="sxs-lookup"><span data-stu-id="b329f-116">SQL Data Warehouse uses server-level firewall rules.</span></span> <span data-ttu-id="b329f-117">It does not support database-level firewall rules.</span><span class="sxs-lookup"><span data-stu-id="b329f-117">It does not support database-level firewall rules.</span></span> <span data-ttu-id="b329f-118">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="b329f-118">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule].</span></span>

<span data-ttu-id="b329f-119">Connections to your SQL Data Warehouse are encrypted by default.</span><span class="sxs-lookup"><span data-stu-id="b329f-119">Connections to your SQL Data Warehouse are encrypted by default.</span></span>  <span data-ttu-id="b329f-120">Modifying connection settings to disable encryption are ignored.</span><span class="sxs-lookup"><span data-stu-id="b329f-120">Modifying connection settings to disable encryption are ignored.</span></span>

## <a name="authentication"></a><span data-ttu-id="b329f-121">Authentication</span><span class="sxs-lookup"><span data-stu-id="b329f-121">Authentication</span></span>
<span data-ttu-id="b329f-122">Authentication refers to how you prove your identity when connecting to the database.</span><span class="sxs-lookup"><span data-stu-id="b329f-122">Authentication refers to how you prove your identity when connecting to the database.</span></span> <span data-ttu-id="b329f-123">SQL Data Warehouse currently supports SQL Server Authentication with a username and password, and with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b329f-123">SQL Data Warehouse currently supports SQL Server Authentication with a username and password, and with Azure Active Directory.</span></span> 

<span data-ttu-id="b329f-124">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span><span class="sxs-lookup"><span data-stu-id="b329f-124">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="b329f-125">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo" through SQL Server Authentication.</span><span class="sxs-lookup"><span data-stu-id="b329f-125">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo" through SQL Server Authentication.</span></span>

<span data-ttu-id="b329f-126">However, as a best practice, your organization’s users should use a different account to authenticate.</span><span class="sxs-lookup"><span data-stu-id="b329f-126">However, as a best practice, your organization’s users should use a different account to authenticate.</span></span> <span data-ttu-id="b329f-127">This way you can limit the permissions granted to the application and reduce the risks of malicious activity in case your application code is vulnerable to a SQL injection attack.</span><span class="sxs-lookup"><span data-stu-id="b329f-127">This way you can limit the permissions granted to the application and reduce the risks of malicious activity in case your application code is vulnerable to a SQL injection attack.</span></span> 

<span data-ttu-id="b329f-128">To create a SQL Server Authenticated user, connect to the **master** database on your server with your server admin login and create a new server login.</span><span class="sxs-lookup"><span data-stu-id="b329f-128">To create a SQL Server Authenticated user, connect to the **master** database on your server with your server admin login and create a new server login.</span></span>  <span data-ttu-id="b329f-129">Additionally, it is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span><span class="sxs-lookup"><span data-stu-id="b329f-129">Additionally, it is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="b329f-130">Creating a user in master allows a user to log in using tools like SSMS without specifying a database name.</span><span class="sxs-lookup"><span data-stu-id="b329f-130">Creating a user in master allows a user to log in using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="b329f-131">It also allows them to use the object explorer to view all databases on a SQL server.</span><span class="sxs-lookup"><span data-stu-id="b329f-131">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="b329f-132">Then, connect to your **SQL Data Warehouse database** with your server admin login and create a database user based on the server login you created.</span><span class="sxs-lookup"><span data-stu-id="b329f-132">Then, connect to your **SQL Data Warehouse database** with your server admin login and create a database user based on the server login you created.</span></span>

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="b329f-133">To give a user permission to perform additional operations such as creating logins or creating new databases, assign the user to the `Loginmanager` and `dbmanager` roles in the master database.</span><span class="sxs-lookup"><span data-stu-id="b329f-133">To give a user permission to perform additional operations such as creating logins or creating new databases, assign the user to the `Loginmanager` and `dbmanager` roles in the master database.</span></span> <span data-ttu-id="b329f-134">For more information on these additional roles and authenticating to a SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="b329f-134">For more information on these additional roles and authenticating to a SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span></span>  <span data-ttu-id="b329f-135">For more information, see [Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].</span><span class="sxs-lookup"><span data-stu-id="b329f-135">For more information, see [Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].</span></span>

## <a name="authorization"></a><span data-ttu-id="b329f-136">Authorization</span><span class="sxs-lookup"><span data-stu-id="b329f-136">Authorization</span></span>
<span data-ttu-id="b329f-137">Authorization refers to what you can do within an Azure SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="b329f-137">Authorization refers to what you can do within an Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="b329f-138">Authorization privileges are determined by role memberships and permissions.</span><span class="sxs-lookup"><span data-stu-id="b329f-138">Authorization privileges are determined by role memberships and permissions.</span></span> <span data-ttu-id="b329f-139">As a best practice, you should grant users the least privileges necessary.</span><span class="sxs-lookup"><span data-stu-id="b329f-139">As a best practice, you should grant users the least privileges necessary.</span></span> <span data-ttu-id="b329f-140">To manage roles, you can use the following stored procedures:</span><span class="sxs-lookup"><span data-stu-id="b329f-140">To manage roles, you can use the following stored procedures:</span></span>

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

<span data-ttu-id="b329f-141">The server admin account you are connecting with is a member of db_owner, which has authority to do anything within the database.</span><span class="sxs-lookup"><span data-stu-id="b329f-141">The server admin account you are connecting with is a member of db_owner, which has authority to do anything within the database.</span></span> <span data-ttu-id="b329f-142">Save this account for deploying schema upgrades and other management operations.</span><span class="sxs-lookup"><span data-stu-id="b329f-142">Save this account for deploying schema upgrades and other management operations.</span></span> <span data-ttu-id="b329f-143">Use the "ApplicationUser" account with more limited permissions to connect from your application to the database with the least privileges needed by your application.</span><span class="sxs-lookup"><span data-stu-id="b329f-143">Use the "ApplicationUser" account with more limited permissions to connect from your application to the database with the least privileges needed by your application.</span></span>

<span data-ttu-id="b329f-144">There are ways to further limit what a user can do with Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="b329f-144">There are ways to further limit what a user can do with Azure SQL Data Warehouse:</span></span>

* <span data-ttu-id="b329f-145">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, schemas, procedures, and other objects in the database.</span><span class="sxs-lookup"><span data-stu-id="b329f-145">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, schemas, procedures, and other objects in the database.</span></span> <span data-ttu-id="b329f-146">Use granular permissions to have the most control and grant the minimum permissions necessary.</span><span class="sxs-lookup"><span data-stu-id="b329f-146">Use granular permissions to have the most control and grant the minimum permissions necessary.</span></span> 
* <span data-ttu-id="b329f-147">[Database roles][Database roles] other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts.</span><span class="sxs-lookup"><span data-stu-id="b329f-147">[Database roles][Database roles] other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts.</span></span> <span data-ttu-id="b329f-148">The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.</span><span class="sxs-lookup"><span data-stu-id="b329f-148">The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.</span></span>
* <span data-ttu-id="b329f-149">[Stored procedures][Stored procedures] can be used to limit the actions that can be taken on the database.</span><span class="sxs-lookup"><span data-stu-id="b329f-149">[Stored procedures][Stored procedures] can be used to limit the actions that can be taken on the database.</span></span>

<span data-ttu-id="b329f-150">The following example grants read access to a user-defined schema.</span><span class="sxs-lookup"><span data-stu-id="b329f-150">The following example grants read access to a user-defined schema.</span></span>
```sql
--CREATE SCHEMA Test
GRANT SELECT ON SCHEMA::Test to ApplicationUser
```

<span data-ttu-id="b329f-151">Managing databases and logical servers from the Azure portal or using the Azure Resource Manager API is controlled by your portal user account's role assignments.</span><span class="sxs-lookup"><span data-stu-id="b329f-151">Managing databases and logical servers from the Azure portal or using the Azure Resource Manager API is controlled by your portal user account's role assignments.</span></span> <span data-ttu-id="b329f-152">For more information, see [Role-based access control in Azure portal][Role-based access control in Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b329f-152">For more information, see [Role-based access control in Azure portal][Role-based access control in Azure portal].</span></span>

## <a name="encryption"></a><span data-ttu-id="b329f-153">Encryption</span><span class="sxs-lookup"><span data-stu-id="b329f-153">Encryption</span></span>
<span data-ttu-id="b329f-154">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by encrypting and decrypting your data at rest.</span><span class="sxs-lookup"><span data-stu-id="b329f-154">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by encrypting and decrypting your data at rest.</span></span>  <span data-ttu-id="b329f-155">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications.</span><span class="sxs-lookup"><span data-stu-id="b329f-155">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications.</span></span> <span data-ttu-id="b329f-156">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span><span class="sxs-lookup"><span data-stu-id="b329f-156">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> 

<span data-ttu-id="b329f-157">In SQL Database, the database encryption key is protected by a built-in server certificate.</span><span class="sxs-lookup"><span data-stu-id="b329f-157">In SQL Database, the database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="b329f-158">The built-in server certificate is unique for each SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="b329f-158">The built-in server certificate is unique for each SQL Database server.</span></span> <span data-ttu-id="b329f-159">Microsoft automatically rotates these certificates at least every 90 days.</span><span class="sxs-lookup"><span data-stu-id="b329f-159">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="b329f-160">The encryption algorithm used by SQL Data Warehouse is AES-256.</span><span class="sxs-lookup"><span data-stu-id="b329f-160">The encryption algorithm used by SQL Data Warehouse is AES-256.</span></span> <span data-ttu-id="b329f-161">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span><span class="sxs-lookup"><span data-stu-id="b329f-161">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span></span>

<span data-ttu-id="b329f-162">You can encrypt your database using the [Azure portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span><span class="sxs-lookup"><span data-stu-id="b329f-162">You can encrypt your database using the [Azure portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b329f-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="b329f-163">Next steps</span></span>
<span data-ttu-id="b329f-164">For details and examples on connecting to your SQL Data Warehouse with different protocols, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b329f-164">For details and examples on connecting to your SQL Data Warehouse with different protocols, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

<!--Image references-->

<!--Article references-->
[Connect to SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
