---
title: Secure a database in SQL Data Warehouse | Microsoft Docs
description: Tips for securing a database in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: ''
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 6ea45c40bc428282faf24b4a08f8b0d345adb3fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662418"
---
# <a name="secure-a-database-in-sql-data-warehouse"></a><span data-ttu-id="92c69-103">Secure a database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="92c69-103">Secure a database in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [Security Overview](sql-data-warehouse-overview-manage-security.md)
> * [Authentication](sql-data-warehouse-authentication.md)
> * [Encryption (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Encryption (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="92c69-108">This article walks through the basics of securing your Azure SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="92c69-108">This article walks through the basics of securing your Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="92c69-109">In particular, this article will get you started with resources for limiting access, protecting data, and monitoring activities on a database.</span><span class="sxs-lookup"><span data-stu-id="92c69-109">In particular, this article will get you started with resources for limiting access, protecting data, and monitoring activities on a database.</span></span>

## <a name="connection-security"></a><span data-ttu-id="92c69-110">Connection security</span><span class="sxs-lookup"><span data-stu-id="92c69-110">Connection security</span></span>
<span data-ttu-id="92c69-111">Connection Security refers to how you restrict and secure connections to your database using firewall rules and connection encryption.</span><span class="sxs-lookup"><span data-stu-id="92c69-111">Connection Security refers to how you restrict and secure connections to your database using firewall rules and connection encryption.</span></span>

<span data-ttu-id="92c69-112">Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that have not been explicitly whitelisted.</span><span class="sxs-lookup"><span data-stu-id="92c69-112">Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that have not been explicitly whitelisted.</span></span> <span data-ttu-id="92c69-113">To allow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using the Azure Portal, REST API, or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92c69-113">To allow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using the Azure Portal, REST API, or PowerShell.</span></span> <span data-ttu-id="92c69-114">As a best practice, you should restrict the IP address ranges allowed through your server firewall as much as possible.</span><span class="sxs-lookup"><span data-stu-id="92c69-114">As a best practice, you should restrict the IP address ranges allowed through your server firewall as much as possible.</span></span>  <span data-ttu-id="92c69-115">To access Azure SQL Data Warehouse from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span><span class="sxs-lookup"><span data-stu-id="92c69-115">To access Azure SQL Data Warehouse from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>  <span data-ttu-id="92c69-116">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="92c69-116">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="92c69-117">Connections to your SQL Data Warehouse are encrypted by default.</span><span class="sxs-lookup"><span data-stu-id="92c69-117">Connections to your SQL Data Warehouse are encrypted by default.</span></span>  <span data-ttu-id="92c69-118">Modifying connection settings to disable encryption are ignored.</span><span class="sxs-lookup"><span data-stu-id="92c69-118">Modifying connection settings to disable encryption are ignored.</span></span>

## <a name="authentication"></a><span data-ttu-id="92c69-119">Authentication</span><span class="sxs-lookup"><span data-stu-id="92c69-119">Authentication</span></span>
<span data-ttu-id="92c69-120">Authentication refers to how you prove your identity when connecting to the database.</span><span class="sxs-lookup"><span data-stu-id="92c69-120">Authentication refers to how you prove your identity when connecting to the database.</span></span> <span data-ttu-id="92c69-121">SQL Data Warehouse currently supports SQL Server Authentication with a username and password as well as a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92c69-121">SQL Data Warehouse currently supports SQL Server Authentication with a username and password as well as a Azure Active Directory.</span></span> 

<span data-ttu-id="92c69-122">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span><span class="sxs-lookup"><span data-stu-id="92c69-122">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="92c69-123">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo" through SQL Server Authentication.</span><span class="sxs-lookup"><span data-stu-id="92c69-123">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo" through SQL Server Authentication.</span></span>

<span data-ttu-id="92c69-124">However, as a best practice, your organization’s users should use a different account to authenticate.</span><span class="sxs-lookup"><span data-stu-id="92c69-124">However, as a best practice, your organization’s users should use a different account to authenticate.</span></span> <span data-ttu-id="92c69-125">This way you can limit the permissions granted to the application and reduce the risks of malicious activity in case your application code is vulnerable to a SQL injection attack.</span><span class="sxs-lookup"><span data-stu-id="92c69-125">This way you can limit the permissions granted to the application and reduce the risks of malicious activity in case your application code is vulnerable to a SQL injection attack.</span></span> 

<span data-ttu-id="92c69-126">To create a SQL Server Authenticated user, connect to the **master** database on your server with your server admin login and create a new server login.</span><span class="sxs-lookup"><span data-stu-id="92c69-126">To create a SQL Server Authenticated user, connect to the **master** database on your server with your server admin login and create a new server login.</span></span>  <span data-ttu-id="92c69-127">Additionally, it is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span><span class="sxs-lookup"><span data-stu-id="92c69-127">Additionally, it is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="92c69-128">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span><span class="sxs-lookup"><span data-stu-id="92c69-128">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="92c69-129">It also allows them to use the object explorer to view all databases on a SQL server.</span><span class="sxs-lookup"><span data-stu-id="92c69-129">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="92c69-130">Then, connect to your **SQL Data Warehouse database** with your server admin login and create a database user based on the server login you just created.</span><span class="sxs-lookup"><span data-stu-id="92c69-130">Then, connect to your **SQL Data Warehouse database** with your server admin login and create a database user based on the server login you just created.</span></span>

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="92c69-131">If a user will be doing additional operations such as creating logins or creating new databases, they will also need to be assigned to the `Loginmanager` and `dbmanager` roles in the master database.</span><span class="sxs-lookup"><span data-stu-id="92c69-131">If a user will be doing additional operations such as creating logins or creating new databases, they will also need to be assigned to the `Loginmanager` and `dbmanager` roles in the master database.</span></span> <span data-ttu-id="92c69-132">For more information on these additonal roles and authenticating to a SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="92c69-132">For more information on these additonal roles and authenticating to a SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span></span>  <span data-ttu-id="92c69-133">For more details on Azure AD for SQL Data Warehouse, see [Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].</span><span class="sxs-lookup"><span data-stu-id="92c69-133">For more details on Azure AD for SQL Data Warehouse, see [Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].</span></span>

## <a name="authorization"></a><span data-ttu-id="92c69-134">Authorization</span><span class="sxs-lookup"><span data-stu-id="92c69-134">Authorization</span></span>
<span data-ttu-id="92c69-135">Authorization refers to what you can do within an Azure SQL Data Warehouse database, and this is controlled by your user account's role memberships and permissions.</span><span class="sxs-lookup"><span data-stu-id="92c69-135">Authorization refers to what you can do within an Azure SQL Data Warehouse database, and this is controlled by your user account's role memberships and permissions.</span></span> <span data-ttu-id="92c69-136">As a best practice, you should grant users the least privileges necessary.</span><span class="sxs-lookup"><span data-stu-id="92c69-136">As a best practice, you should grant users the least privileges necessary.</span></span> <span data-ttu-id="92c69-137">Azure SQL Data Warehouse makes this easy to manage with roles in T-SQL:</span><span class="sxs-lookup"><span data-stu-id="92c69-137">Azure SQL Data Warehouse makes this easy to manage with roles in T-SQL:</span></span>

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

<span data-ttu-id="92c69-138">The server admin account you are connecting with is a member of db_owner, which has authority to do anything within the database.</span><span class="sxs-lookup"><span data-stu-id="92c69-138">The server admin account you are connecting with is a member of db_owner, which has authority to do anything within the database.</span></span> <span data-ttu-id="92c69-139">Save this account for deploying schema upgrades and other management operations.</span><span class="sxs-lookup"><span data-stu-id="92c69-139">Save this account for deploying schema upgrades and other management operations.</span></span> <span data-ttu-id="92c69-140">Use the "ApplicationUser" account with more limited permissions to connect from your application to the database with the least privileges needed by your application.</span><span class="sxs-lookup"><span data-stu-id="92c69-140">Use the "ApplicationUser" account with more limited permissions to connect from your application to the database with the least privileges needed by your application.</span></span>

<span data-ttu-id="92c69-141">There are ways to further limit what a user can do with Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="92c69-141">There are ways to further limit what a user can do with Azure SQL Database:</span></span>

* <span data-ttu-id="92c69-142">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, procedures, and other objects in the database.</span><span class="sxs-lookup"><span data-stu-id="92c69-142">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, procedures, and other objects in the database.</span></span> <span data-ttu-id="92c69-143">Use granular permissions to have the most control and grant the minimum permissions necessary.</span><span class="sxs-lookup"><span data-stu-id="92c69-143">Use granular permissions to have the most control and grant the minimum permissions necessary.</span></span> <span data-ttu-id="92c69-144">The granular permission system is somewhat complicated and will require some study to use effectively.</span><span class="sxs-lookup"><span data-stu-id="92c69-144">The granular permission system is somewhat complicated and will require some study to use effectively.</span></span>
* <span data-ttu-id="92c69-145">[Database roles][Database roles] other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts.</span><span class="sxs-lookup"><span data-stu-id="92c69-145">[Database roles][Database roles] other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts.</span></span> <span data-ttu-id="92c69-146">The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.</span><span class="sxs-lookup"><span data-stu-id="92c69-146">The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.</span></span>
* <span data-ttu-id="92c69-147">[Stored procedures][Stored procedures] can be used to limit the actions that can be taken on the database.</span><span class="sxs-lookup"><span data-stu-id="92c69-147">[Stored procedures][Stored procedures] can be used to limit the actions that can be taken on the database.</span></span>

<span data-ttu-id="92c69-148">Managing databases and logical servers from the Azure Classic Portal or using the Azure Resource Manager API is controlled by your portal user account's role assignments.</span><span class="sxs-lookup"><span data-stu-id="92c69-148">Managing databases and logical servers from the Azure Classic Portal or using the Azure Resource Manager API is controlled by your portal user account's role assignments.</span></span> <span data-ttu-id="92c69-149">For more information on this topic, see [Role-based access control in Azure Portal][Role-based access control in Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="92c69-149">For more information on this topic, see [Role-based access control in Azure Portal][Role-based access control in Azure Portal].</span></span>

## <a name="encryption"></a><span data-ttu-id="92c69-150">Encryption</span><span class="sxs-lookup"><span data-stu-id="92c69-150">Encryption</span></span>
<span data-ttu-id="92c69-151">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of your data at rest.</span><span class="sxs-lookup"><span data-stu-id="92c69-151">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of your data at rest.</span></span>  <span data-ttu-id="92c69-152">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications.</span><span class="sxs-lookup"><span data-stu-id="92c69-152">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications.</span></span> <span data-ttu-id="92c69-153">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span><span class="sxs-lookup"><span data-stu-id="92c69-153">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="92c69-154">In SQL Database the database encryption key is protected by a built-in server certificate.</span><span class="sxs-lookup"><span data-stu-id="92c69-154">In SQL Database the database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="92c69-155">The built-in server certificate is unique for each SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="92c69-155">The built-in server certificate is unique for each SQL Database server.</span></span> <span data-ttu-id="92c69-156">Microsoft automatically rotates these certificates at least every 90 days.</span><span class="sxs-lookup"><span data-stu-id="92c69-156">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="92c69-157">The encryption algorithm used by SQL Data Warehouse is AES-256.</span><span class="sxs-lookup"><span data-stu-id="92c69-157">The encryption algorithm used by SQL Data Warehouse is AES-256.</span></span> <span data-ttu-id="92c69-158">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span><span class="sxs-lookup"><span data-stu-id="92c69-158">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span></span>

<span data-ttu-id="92c69-159">You can encrypt your database using the [Azure Portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span><span class="sxs-lookup"><span data-stu-id="92c69-159">You can encrypt your database using the [Azure Portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span></span>

## <a name="next-steps"></a><span data-ttu-id="92c69-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="92c69-160">Next steps</span></span>
<span data-ttu-id="92c69-161">For details and examples on connecting to your SQL Data Warehouse with different protocols, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="92c69-161">For details and examples on connecting to your SQL Data Warehouse with different protocols, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

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
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
