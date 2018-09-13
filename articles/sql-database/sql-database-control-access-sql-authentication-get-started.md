---
title: 'SQL auth: Azure SQL Database firewalls, authentication, access | Microsoft Docs'
description: In this getting-started tutorial, you learn how to use SQL Server Management Studio and Transact-SQL to work with server-level and database-level firewall rules, SQL authentication, logins, users, and roles to grant access and control to Azure SQL Database servers and databases.
keywords: ''
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: 67797b09-f5c3-4ec2-8494-fe18883edf7f
ms.service: sql-database
ms.custom: security-access
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: carlrab
ms.openlocfilehash: ca0f3d6adfa4741c209706c55ac029f3766824ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552526"
---
# <a name="sql-server-authentication-access-and-database-level-firewall-rules"></a><span data-ttu-id="d5687-103">SQL Server authentication, access, and database-level firewall rules</span><span class="sxs-lookup"><span data-stu-id="d5687-103">SQL Server authentication, access, and database-level firewall rules</span></span>

<span data-ttu-id="d5687-104">In this tutorial, you learn how to use SQL Server Management Studio to work with SQL Server authentication, logins, users, and database roles that grant access and permissions to Azure SQL Database servers and databases.</span><span class="sxs-lookup"><span data-stu-id="d5687-104">In this tutorial, you learn how to use SQL Server Management Studio to work with SQL Server authentication, logins, users, and database roles that grant access and permissions to Azure SQL Database servers and databases.</span></span> <span data-ttu-id="d5687-105">After you complete this tutorial, you will know how to:</span><span class="sxs-lookup"><span data-stu-id="d5687-105">After you complete this tutorial, you will know how to:</span></span>

- <span data-ttu-id="d5687-106">Create logins and users based on SQL Server authentication</span><span class="sxs-lookup"><span data-stu-id="d5687-106">Create logins and users based on SQL Server authentication</span></span>
- <span data-ttu-id="d5687-107">Add users to roles and grant permissions to roles</span><span class="sxs-lookup"><span data-stu-id="d5687-107">Add users to roles and grant permissions to roles</span></span>
- <span data-ttu-id="d5687-108">Use T-SQL to create a database-level and a server-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="d5687-108">Use T-SQL to create a database-level and a server-level firewall rule</span></span> 
- <span data-ttu-id="d5687-109">Connect as a user to a specific database using SSMS</span><span class="sxs-lookup"><span data-stu-id="d5687-109">Connect as a user to a specific database using SSMS</span></span>
- <span data-ttu-id="d5687-110">View user permissions in the master database and in user databases</span><span class="sxs-lookup"><span data-stu-id="d5687-110">View user permissions in the master database and in user databases</span></span>

<span data-ttu-id="d5687-111">**Time estimate**: This tutorial takes approximately 45 minutes to complete (assuming you have already met the prerequisites).</span><span class="sxs-lookup"><span data-stu-id="d5687-111">**Time estimate**: This tutorial takes approximately 45 minutes to complete (assuming you have already met the prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="d5687-112">This tutorial helps you to learn the content of these topics: [SQL Database access and control](sql-database-control-access.md), [Logins, users, and database roles](sql-database-manage-logins.md), [Principals](https://msdn.microsoft.com/library/ms181127.aspx), [Database roles](https://msdn.microsoft.com/library/ms189121.aspx), and [SQL Database firewall rules](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-112">This tutorial helps you to learn the content of these topics: [SQL Database access and control](sql-database-control-access.md), [Logins, users, and database roles](sql-database-manage-logins.md), [Principals](https://msdn.microsoft.com/library/ms181127.aspx), [Database roles](https://msdn.microsoft.com/library/ms189121.aspx), and [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span> <span data-ttu-id="d5687-113">For a tutorial about Azure Active Directory authentication, see [Getting started with Azure AD Authentication](sql-database-control-access-aad-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-113">For a tutorial about Azure Active Directory authentication, see [Getting started with Azure AD Authentication](sql-database-control-access-aad-authentication-get-started.md).</span></span>
>  

## <a name="prerequisites"></a><span data-ttu-id="d5687-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d5687-114">Prerequisites</span></span>

* <span data-ttu-id="d5687-115">**An Azure account**.</span><span class="sxs-lookup"><span data-stu-id="d5687-115">**An Azure account**.</span></span> <span data-ttu-id="d5687-116">You need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="d5687-116">You need an Azure account.</span></span> <span data-ttu-id="d5687-117">You can [open a free Azure account](https://azure.microsoft.com/free/) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/).</span><span class="sxs-lookup"><span data-stu-id="d5687-117">You can [open a free Azure account](https://azure.microsoft.com/free/) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/).</span></span> 

* <span data-ttu-id="d5687-118">**Azure create permissions**.</span><span class="sxs-lookup"><span data-stu-id="d5687-118">**Azure create permissions**.</span></span> <span data-ttu-id="d5687-119">You must be able to connect to the Azure portal using an account that is a member of either the subscription owner or contributor role.</span><span class="sxs-lookup"><span data-stu-id="d5687-119">You must be able to connect to the Azure portal using an account that is a member of either the subscription owner or contributor role.</span></span> <span data-ttu-id="d5687-120">For more information on role-based access control (RBAC), see [Getting started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-120">For more information on role-based access control (RBAC), see [Getting started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

* <span data-ttu-id="d5687-121">**SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="d5687-121">**SQL Server Management Studio**.</span></span> <span data-ttu-id="d5687-122">You can download and install the latest version of SQL Server Management Studio (SSMS) at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5687-122">You can download and install the latest version of SQL Server Management Studio (SSMS) at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> <span data-ttu-id="d5687-123">Always use the latest version of SSMS when connecting to Azure SQL Database as new capabilities are continually being released.</span><span class="sxs-lookup"><span data-stu-id="d5687-123">Always use the latest version of SSMS when connecting to Azure SQL Database as new capabilities are continually being released.</span></span>

* <span data-ttu-id="d5687-124">**Base server and databases** To install and configure a server and the two databases used in this tutorial, click the **Deploy to Azure** button.</span><span class="sxs-lookup"><span data-stu-id="d5687-124">**Base server and databases** To install and configure a server and the two databases used in this tutorial, click the **Deploy to Azure** button.</span></span> <span data-ttu-id="d5687-125">Clicking the button opens the **Deploy from a template** blade; create a new resource group, and provide the **Admin Login Password** for the new server that will be created:</span><span class="sxs-lookup"><span data-stu-id="d5687-125">Clicking the button opens the **Deploy from a template** blade; create a new resource group, and provide the **Admin Login Password** for the new server that will be created:</span></span>

   <span data-ttu-id="d5687-126">[![download](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fsqldbtutorial.blob.core.windows.net%2Ftemplates%2Fsqldbgetstarted.json)</span><span class="sxs-lookup"><span data-stu-id="d5687-126">[![download](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fsqldbtutorial.blob.core.windows.net%2Ftemplates%2Fsqldbgetstarted.json)</span></span>


## <a name="sign-in-to-the-azure-portal-using-your-azure-account"></a><span data-ttu-id="d5687-127">Sign in to the Azure portal using your Azure account</span><span class="sxs-lookup"><span data-stu-id="d5687-127">Sign in to the Azure portal using your Azure account</span></span>
<span data-ttu-id="d5687-128">The steps in this procedure show you how to connect to the Azure portal using your Azure account](https://account.windowsazure.com/Home/Index).</span><span class="sxs-lookup"><span data-stu-id="d5687-128">The steps in this procedure show you how to connect to the Azure portal using your Azure account](https://account.windowsazure.com/Home/Index).</span></span>

1. <span data-ttu-id="d5687-129">Open your browser of choice and connect to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d5687-129">Open your browser of choice and connect to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d5687-130">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d5687-130">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
3. <span data-ttu-id="d5687-131">On the **Sign in** page, provide the credentials for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d5687-131">On the **Sign in** page, provide the credentials for your subscription.</span></span>

## <a name="view-logical-server-security-information-in-the-azure-portal"></a><span data-ttu-id="d5687-132">View logical server security information in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d5687-132">View logical server security information in the Azure portal</span></span>

<span data-ttu-id="d5687-133">The steps in this procedure show you how to view information about the security configuration for your logical server in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d5687-133">The steps in this procedure show you how to view information about the security configuration for your logical server in the Azure portal.</span></span>

1. <span data-ttu-id="d5687-134">Open the **SQL Server** blade for your server and view the information in the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="d5687-134">Open the **SQL Server** blade for your server and view the information in the **Overview** page.</span></span>

   ![Server admin account in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/sql_admin_portal.png)

2. <span data-ttu-id="d5687-136">Make note of the name for server admin on your logical server.</span><span class="sxs-lookup"><span data-stu-id="d5687-136">Make note of the name for server admin on your logical server.</span></span> 

3. <span data-ttu-id="d5687-137">If you do not remember the password, click **Reset password** to set a new password.</span><span class="sxs-lookup"><span data-stu-id="d5687-137">If you do not remember the password, click **Reset password** to set a new password.</span></span>

4. <span data-ttu-id="d5687-138">If you need to get the connection information for this server, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d5687-138">If you need to get the connection information for this server, click **Properties**.</span></span>

## <a name="view-server-admin-permissions-using-ssms"></a><span data-ttu-id="d5687-139">View server admin permissions using SSMS</span><span class="sxs-lookup"><span data-stu-id="d5687-139">View server admin permissions using SSMS</span></span>

<span data-ttu-id="d5687-140">The steps in this procedure show you how to view information about the server admin account and its permissions in the master database and in user databases.</span><span class="sxs-lookup"><span data-stu-id="d5687-140">The steps in this procedure show you how to view information about the server admin account and its permissions in the master database and in user databases.</span></span>

1. <span data-ttu-id="d5687-141">Open SQL Server Management Studio and connect to your server as the server admin using SQL Server Authentication and the Server admin account.</span><span class="sxs-lookup"><span data-stu-id="d5687-141">Open SQL Server Management Studio and connect to your server as the server admin using SQL Server Authentication and the Server admin account.</span></span>

   ![connect to server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/connect-to-server.png)

2. <span data-ttu-id="d5687-143">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d5687-143">Click **Connect**.</span></span>

   ![connected to server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/connected-to-server.png)

3. <span data-ttu-id="d5687-145">In Object Explorer, expand **Security**, and then expand **Logins** to view the existing logins for your server - the only login on a new server is the login for server admin account.</span><span class="sxs-lookup"><span data-stu-id="d5687-145">In Object Explorer, expand **Security**, and then expand **Logins** to view the existing logins for your server - the only login on a new server is the login for server admin account.</span></span>

   ![Server admin login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/server_admin_login.png)

4. <span data-ttu-id="d5687-147">In Object Explorer, expand **Databases**, expand **System databases**, expand **master**, expand **Security**, and then expand **Users** to view the user account that was created for the server admin login in this database.</span><span class="sxs-lookup"><span data-stu-id="d5687-147">In Object Explorer, expand **Databases**, expand **System databases**, expand **master**, expand **Security**, and then expand **Users** to view the user account that was created for the server admin login in this database.</span></span>

   ![master database user account for server admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/master_database_user_account_for_server_admin.png)

   > [!NOTE]
   > <span data-ttu-id="d5687-149">For information about the other user accounts that appear in the Users node, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5687-149">For information about the other user accounts that appear in the Users node, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
   >

5. <span data-ttu-id="d5687-150">In Object Explorer, right-click **master** and then click **New Query** to open a query window connected to the master database.</span><span class="sxs-lookup"><span data-stu-id="d5687-150">In Object Explorer, right-click **master** and then click **New Query** to open a query window connected to the master database.</span></span>
6. <span data-ttu-id="d5687-151">In the query window, execute the following query to return information about the user executing the query.</span><span class="sxs-lookup"><span data-stu-id="d5687-151">In the query window, execute the following query to return information about the user executing the query.</span></span> 

   ```
   SELECT USER;
   ```

   ![select user query in the master database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/select_user_query_in_master_database.png)

7. <span data-ttu-id="d5687-153">In the query window, execute the following query to return information about the permissions of the sqladmin user in the **master** database.</span><span class="sxs-lookup"><span data-stu-id="d5687-153">In the query window, execute the following query to return information about the permissions of the sqladmin user in the **master** database.</span></span> 

   ```
   SELECT prm.permission_name
      , prm.class_desc
      , prm.state_desc
      , p2.name as 'Database role'
      , p3.name as 'Additional database role' 
   FROM sys.database_principals p
   JOIN sys.database_permissions prm
      ON p.principal_id = prm.grantee_principal_id
      LEFT JOIN sys.database_principals p2
      ON prm.major_id = p2.principal_id
      LEFT JOIN sys.database_role_members r
      ON p.principal_id = r.member_principal_id
      LEFT JOIN sys.database_principals p3
      ON r.role_principal_id = p3.principal_id
   WHERE p.name = 'sqladmin';
   ```

   ![server admin permissions in the master database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/server_admin_permissions_in_master_database.png)

   >[!NOTE]
   > <span data-ttu-id="d5687-155">The server admin has permissions to connect to the master database, create logins and users, select information from the sys.sql_logins table, and add users to the dbmanager and dbcreator database roles.</span><span class="sxs-lookup"><span data-stu-id="d5687-155">The server admin has permissions to connect to the master database, create logins and users, select information from the sys.sql_logins table, and add users to the dbmanager and dbcreator database roles.</span></span> <span data-ttu-id="d5687-156">These permissions are in addition to permissions granted to the public role from which all users inherit permissions (such as permissions to select information from certain tables).</span><span class="sxs-lookup"><span data-stu-id="d5687-156">These permissions are in addition to permissions granted to the public role from which all users inherit permissions (such as permissions to select information from certain tables).</span></span> <span data-ttu-id="d5687-157">See [Permissions](https://msdn.microsoft.com/library/ms191291.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="d5687-157">See [Permissions](https://msdn.microsoft.com/library/ms191291.aspx) for more information.</span></span>
   >

8. <span data-ttu-id="d5687-158">In Object Explorer, expand **blankdb**, expand **Security**, and then expand **Users** to view the user account that was created for the server admin login in this database (and in each user database).</span><span class="sxs-lookup"><span data-stu-id="d5687-158">In Object Explorer, expand **blankdb**, expand **Security**, and then expand **Users** to view the user account that was created for the server admin login in this database (and in each user database).</span></span>

   ![user accounts in blankdb](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/user_accounts_in_blankdb.png)

9. <span data-ttu-id="d5687-160">In Object Explorer, right-click **blankdb** and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="d5687-160">In Object Explorer, right-click **blankdb** and then click **New Query**.</span></span>

10. <span data-ttu-id="d5687-161">In the query window, execute the following query to return information about the user executing the query.</span><span class="sxs-lookup"><span data-stu-id="d5687-161">In the query window, execute the following query to return information about the user executing the query.</span></span>

   ```
   SELECT USER;
   ```

   ![select user query in the blankdb database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/select_user_query_in_blankdb_database.png)

11. <span data-ttu-id="d5687-163">In the query window, execute the following query to return information about the permissions of the dbo user.</span><span class="sxs-lookup"><span data-stu-id="d5687-163">In the query window, execute the following query to return information about the permissions of the dbo user.</span></span> 

   ```
   SELECT prm.permission_name
      , prm.class_desc
      , prm.state_desc
      , p2.name as 'Database role'
      , p3.name as 'Additional database role' 
   FROM sys.database_principals AS p
   JOIN sys.database_permissions AS prm
      ON p.principal_id = prm.grantee_principal_id
      LEFT JOIN sys.database_principals AS p2
      ON prm.major_id = p2.principal_id
      LEFT JOIN sys.database_role_members r
      ON p.principal_id = r.member_principal_id
      LEFT JOIN sys.database_principals AS p3
      ON r.role_principal_id = p3.principal_id
   WHERE p.name = 'dbo';
   ```

   ![server admin permissions in the blankdb database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/server_admin_permissions_in_blankdb_database.png)

   > [!NOTE]
   > <span data-ttu-id="d5687-165">The dbo user is a member of the public role and also a member of the db_owner fixed database role.</span><span class="sxs-lookup"><span data-stu-id="d5687-165">The dbo user is a member of the public role and also a member of the db_owner fixed database role.</span></span> <span data-ttu-id="d5687-166">See [Database-Level Roles](https://msdn.microsoft.com/library/ms189121.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="d5687-166">See [Database-Level Roles](https://msdn.microsoft.com/library/ms189121.aspx) for more information.</span></span>
   >

## <a name="create-a-new-user-with-select-permissions"></a><span data-ttu-id="d5687-167">Create a new user with SELECT permissions</span><span class="sxs-lookup"><span data-stu-id="d5687-167">Create a new user with SELECT permissions</span></span>

<span data-ttu-id="d5687-168">The steps in this procedure show you how to create a database-level user, test the default permissions of a new user(through the public role), grant a user **SELECT** permissions, and view these modified permissions.</span><span class="sxs-lookup"><span data-stu-id="d5687-168">The steps in this procedure show you how to create a database-level user, test the default permissions of a new user(through the public role), grant a user **SELECT** permissions, and view these modified permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="d5687-169">Database-level users are also called [contained users](https://msdn.microsoft.com/library/ff929188.aspx) and increase the portability of your database.</span><span class="sxs-lookup"><span data-stu-id="d5687-169">Database-level users are also called [contained users](https://msdn.microsoft.com/library/ff929188.aspx) and increase the portability of your database.</span></span> <span data-ttu-id="d5687-170">For information about the benefits of portability, see [Configure and manage Azure SQL Database security for geo-restore or failover to a secondary server](sql-database-geo-replication-security-config.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-170">For information about the benefits of portability, see [Configure and manage Azure SQL Database security for geo-restore or failover to a secondary server](sql-database-geo-replication-security-config.md).</span></span>
>

1. <span data-ttu-id="d5687-171">In Object Explorer, right-click **sqldbtutorialdb** and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="d5687-171">In Object Explorer, right-click **sqldbtutorialdb** and then click **New Query**.</span></span>
2. <span data-ttu-id="d5687-172">Execute the following statement in this query window to create a user called **user1** in the sqldbtutorialdb database.</span><span class="sxs-lookup"><span data-stu-id="d5687-172">Execute the following statement in this query window to create a user called **user1** in the sqldbtutorialdb database.</span></span>

   ```
   CREATE USER user1
   WITH PASSWORD = 'p@ssw0rd';
   ```
   ![new user user1 sqldbtutorialdb](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/new_user_user1_aw.png)

3. <span data-ttu-id="d5687-174">In the query window, execute the following query to return information about the permissions of user1.</span><span class="sxs-lookup"><span data-stu-id="d5687-174">In the query window, execute the following query to return information about the permissions of user1.</span></span>

   ```
   SELECT prm.permission_name
      , prm.class_desc
      , prm.state_desc
      , p2.name as 'Database role'
      , p3.name as 'Additional database role' 
   FROM sys.database_principals AS p
   JOIN sys.database_permissions AS prm
      ON p.principal_id = prm.grantee_principal_id
      LEFT JOIN sys.database_principals AS p2
      ON prm.major_id = p2.principal_id
      LEFT JOIN sys.database_role_members r
      ON p.principal_id = r.member_principal_id
      LEFT JOIN sys.database_principals AS p3
      ON r.role_principal_id = p3.principal_id
   WHERE p.name = 'user1';
   ```

   ![new user permissions in a user database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/new_user_permissions_in_user_database.png)

   > [!NOTE]
   > <span data-ttu-id="d5687-176">A new user in a database only has the permissions inherited from the public role.</span><span class="sxs-lookup"><span data-stu-id="d5687-176">A new user in a database only has the permissions inherited from the public role.</span></span>
   >

4. <span data-ttu-id="d5687-177">Execute the following queries using the **EXECUTE AS USER** statement to attempt to query the SalesLT.ProductCategory table in the sqldbtutorialdb database as **user1** with only the permissions inherited from the public role.</span><span class="sxs-lookup"><span data-stu-id="d5687-177">Execute the following queries using the **EXECUTE AS USER** statement to attempt to query the SalesLT.ProductCategory table in the sqldbtutorialdb database as **user1** with only the permissions inherited from the public role.</span></span>

   ```
   EXECUTE AS USER = 'user1';  
   SELECT * FROM [SalesLT].[ProductCategory];
   REVERT;
   ```

   ![no select permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/no_select_permissions.png)

   > [!NOTE]
   > <span data-ttu-id="d5687-179">By default, the public role does not grant **SELECT** permissions on user objects.</span><span class="sxs-lookup"><span data-stu-id="d5687-179">By default, the public role does not grant **SELECT** permissions on user objects.</span></span>
   >

5. <span data-ttu-id="d5687-180">Execute the following statement to grant **SELECT** permissions on the SalesLT.ProductCategory table to **user1**.</span><span class="sxs-lookup"><span data-stu-id="d5687-180">Execute the following statement to grant **SELECT** permissions on the SalesLT.ProductCategory table to **user1**.</span></span>

   ```
   GRANT SELECT ON OBJECT::[SalesLT].[ProductCategory] to user1;
   ```

   ![grant select permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/grant_select_permissions.png)

6. <span data-ttu-id="d5687-182">Execute the following queries to successfully query the SalesLT.ProductCategory table in the sqldbtutorialdb database as **user1**.</span><span class="sxs-lookup"><span data-stu-id="d5687-182">Execute the following queries to successfully query the SalesLT.ProductCategory table in the sqldbtutorialdb database as **user1**.</span></span>

   ```
   EXECUTE AS USER = 'user1';  
   SELECT * FROM [SalesLT].[ProductCategory];
   REVERT;
   ```

   ![select permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/select_permissions.png)

## <a name="create-a-database-level-firewall-rule-using-t-sql"></a><span data-ttu-id="d5687-184">Create a database-level firewall rule using T-SQL</span><span class="sxs-lookup"><span data-stu-id="d5687-184">Create a database-level firewall rule using T-SQL</span></span>

<span data-ttu-id="d5687-185">The steps in this procedure show you how to create a database-level firewall rule using the [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) system stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d5687-185">The steps in this procedure show you how to create a database-level firewall rule using the [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) system stored procedure.</span></span> <span data-ttu-id="d5687-186">A database-level firewall rule allows a server admin to allow users through the Azure SQL Database firewall only for specific databases.</span><span class="sxs-lookup"><span data-stu-id="d5687-186">A database-level firewall rule allows a server admin to allow users through the Azure SQL Database firewall only for specific databases.</span></span>

> [!NOTE]
> <span data-ttu-id="d5687-187">[Database-level firewall rules](sql-database-firewall-configure.md) increase the portability of your database.</span><span class="sxs-lookup"><span data-stu-id="d5687-187">[Database-level firewall rules](sql-database-firewall-configure.md) increase the portability of your database.</span></span> <span data-ttu-id="d5687-188">For information about the benefits of portability, see [Configure and manage Azure SQL Database security for geo-restore or failover to a secondary server](sql-database-geo-replication-security-config.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-188">For information about the benefits of portability, see [Configure and manage Azure SQL Database security for geo-restore or failover to a secondary server](sql-database-geo-replication-security-config.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="d5687-189">To test a database-level firewall rule, connect from another computer (or delete the server-level firewall rule in the Azure portal.)</span><span class="sxs-lookup"><span data-stu-id="d5687-189">To test a database-level firewall rule, connect from another computer (or delete the server-level firewall rule in the Azure portal.)</span></span>
>

1. <span data-ttu-id="d5687-190">Open SQL Server Management Studio on a computer for which you do not have a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="d5687-190">Open SQL Server Management Studio on a computer for which you do not have a server-level firewall rule.</span></span>

2. <span data-ttu-id="d5687-191">In the **Connect to Server** window, enter the server name and authentication information to connect using SQL Server authentication with the **user1** account.</span><span class="sxs-lookup"><span data-stu-id="d5687-191">In the **Connect to Server** window, enter the server name and authentication information to connect using SQL Server authentication with the **user1** account.</span></span> 
    
   ![Connect as user1 without firewall rule1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/connect-user1_no_rule1.png)

3. <span data-ttu-id="d5687-193">Click **Options** in the **Connect to server** dialog box to specify the database to which you want to connect and then type **sqldbtutorialdb** in the **Connect to Database** drop-down box on the **Connection Properties** tab.</span><span class="sxs-lookup"><span data-stu-id="d5687-193">Click **Options** in the **Connect to server** dialog box to specify the database to which you want to connect and then type **sqldbtutorialdb** in the **Connect to Database** drop-down box on the **Connection Properties** tab.</span></span>
   
   ![Connect as user1 without firewall rule2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/connect-user1_no_rule2.png)

4. <span data-ttu-id="d5687-195">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d5687-195">Click **Connect**.</span></span> 

   <span data-ttu-id="d5687-196">A dialog box appears informing you that the computer from which you are attempting to connect to SQL Database does not have a firewall rule enabling access to the database.</span><span class="sxs-lookup"><span data-stu-id="d5687-196">A dialog box appears informing you that the computer from which you are attempting to connect to SQL Database does not have a firewall rule enabling access to the database.</span></span> 

   ![Connect as user1 without firewall rule4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/connect-user1_no_rule4.png)


5. <span data-ttu-id="d5687-198">Copy the client IP address from this dialog box for use in step 8.</span><span class="sxs-lookup"><span data-stu-id="d5687-198">Copy the client IP address from this dialog box for use in step 8.</span></span>
6. <span data-ttu-id="d5687-199">Click **OK** to close the error dialog box, but do not close the **Connect to Server** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d5687-199">Click **OK** to close the error dialog box, but do not close the **Connect to Server** dialog box.</span></span>
7. <span data-ttu-id="d5687-200">Switch back to a computer for which you have already created a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="d5687-200">Switch back to a computer for which you have already created a server-level firewall rule.</span></span> 
8. <span data-ttu-id="d5687-201">Connect to the sqldbtutorialdb database in SSMS as server admin and execute the following statement to create a database-level firewall using the IP address (or address range) from step 5.</span><span class="sxs-lookup"><span data-stu-id="d5687-201">Connect to the sqldbtutorialdb database in SSMS as server admin and execute the following statement to create a database-level firewall using the IP address (or address range) from step 5.</span></span>  

   ```
   EXEC sp_set_database_firewall_rule @name = N'sqldbtutorialdbFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
   ```

   ![add firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/user1_add_rule_aw.png)

9. <span data-ttu-id="d5687-203">Switch computers again and click **Connect** in the **Connect to Server** dialog box to connect to sqldbtutorialdb as user1.</span><span class="sxs-lookup"><span data-stu-id="d5687-203">Switch computers again and click **Connect** in the **Connect to Server** dialog box to connect to sqldbtutorialdb as user1.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="d5687-204">After you create the database-level firewall rule, it may take up to 5 minutes to become active.</span><span class="sxs-lookup"><span data-stu-id="d5687-204">After you create the database-level firewall rule, it may take up to 5 minutes to become active.</span></span>
   >

10. <span data-ttu-id="d5687-205">After you connect successfully, expand **Databases** in Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="d5687-205">After you connect successfully, expand **Databases** in Object Explorer.</span></span> <span data-ttu-id="d5687-206">Notice that **user1** can only view the **sqldbtutorialdb** database.</span><span class="sxs-lookup"><span data-stu-id="d5687-206">Notice that **user1** can only view the **sqldbtutorialdb** database.</span></span>

   ![Connect as user1 with firewall rule1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/connect-user1_rule1.png)

11. <span data-ttu-id="d5687-208">Expand **sqldbtutorialdb**, and then expand **Tables**.</span><span class="sxs-lookup"><span data-stu-id="d5687-208">Expand **sqldbtutorialdb**, and then expand **Tables**.</span></span> <span data-ttu-id="d5687-209">Notice that user1 only has permission to view a single table, the **SalesLT.ProductCategory** table.</span><span class="sxs-lookup"><span data-stu-id="d5687-209">Notice that user1 only has permission to view a single table, the **SalesLT.ProductCategory** table.</span></span> 

   ![Connect as user1 and view objects1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-sql-authentication-get-started/connect-user1_view_objects1.png)

## <a name="create-a-new-user-as-dbowner-and-a-database-level-firewall-rule"></a><span data-ttu-id="d5687-211">Create a new user as db_owner and a database-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="d5687-211">Create a new user as db_owner and a database-level firewall rule</span></span>

<span data-ttu-id="d5687-212">The steps in this procedure show you how to create a user in another database with db_owner database role permissions and create a database-level firewall for this other database.</span><span class="sxs-lookup"><span data-stu-id="d5687-212">The steps in this procedure show you how to create a user in another database with db_owner database role permissions and create a database-level firewall for this other database.</span></span> <span data-ttu-id="d5687-213">This new user with **db_owner** role membership will only be able to connect to and manage this single database.</span><span class="sxs-lookup"><span data-stu-id="d5687-213">This new user with **db_owner** role membership will only be able to connect to and manage this single database.</span></span>

1. <span data-ttu-id="d5687-214">Switch to your computer with a connection to SQL Database using the server admin account.</span><span class="sxs-lookup"><span data-stu-id="d5687-214">Switch to your computer with a connection to SQL Database using the server admin account.</span></span>
2. <span data-ttu-id="d5687-215">Open a query window connected to the **blankdb** database and execute the following statement to create a user called blankdbadmin in the blankdb database.</span><span class="sxs-lookup"><span data-stu-id="d5687-215">Open a query window connected to the **blankdb** database and execute the following statement to create a user called blankdbadmin in the blankdb database.</span></span>

   ```
   CREATE USER blankdbadmin
   WITH PASSWORD = 'p@ssw0rd';
   ```

3. <span data-ttu-id="d5687-216">In the same query window, execute the following statement to add the blankdbadmin user to the db_owner database role.</span><span class="sxs-lookup"><span data-stu-id="d5687-216">In the same query window, execute the following statement to add the blankdbadmin user to the db_owner database role.</span></span> <span data-ttu-id="d5687-217">This user can now perform all actions necessary to manage the blankdb database.</span><span class="sxs-lookup"><span data-stu-id="d5687-217">This user can now perform all actions necessary to manage the blankdb database.</span></span>

   ```
   ALTER ROLE db_owner ADD MEMBER blankdbadmin; 
   ```

4. <span data-ttu-id="d5687-218">In the same query window, execute the following statement to create a database-level firewall by executing [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) using the IP address from step 4 in the previous procedure (or a range of IP addresses for users of this database):</span><span class="sxs-lookup"><span data-stu-id="d5687-218">In the same query window, execute the following statement to create a database-level firewall by executing [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) using the IP address from step 4 in the previous procedure (or a range of IP addresses for users of this database):</span></span>

   ```
   EXEC sp_set_database_firewall_rule @name = N'blankdbFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
   ```

5. <span data-ttu-id="d5687-219">Switch computers (to one for which you have created a database-level firewall rule) and connect to the blankdb database using the blankdbadmin user account.</span><span class="sxs-lookup"><span data-stu-id="d5687-219">Switch computers (to one for which you have created a database-level firewall rule) and connect to the blankdb database using the blankdbadmin user account.</span></span>
6. <span data-ttu-id="d5687-220">Open a query window to the blankdb database and execute the following statement to create a user called blankdbuser1 in the blankdb database.</span><span class="sxs-lookup"><span data-stu-id="d5687-220">Open a query window to the blankdb database and execute the following statement to create a user called blankdbuser1 in the blankdb database.</span></span>

   ```
   CREATE USER blankdbuser1
   WITH PASSWORD = 'p@ssw0rd';
   ```
 
7. <span data-ttu-id="d5687-221">As necessary for your learning environment, create an additional database-level firewall rule for this user.</span><span class="sxs-lookup"><span data-stu-id="d5687-221">As necessary for your learning environment, create an additional database-level firewall rule for this user.</span></span> <span data-ttu-id="d5687-222">However, if you created the database-level firewall rule using an IP address range, this may not be necessary.</span><span class="sxs-lookup"><span data-stu-id="d5687-222">However, if you created the database-level firewall rule using an IP address range, this may not be necessary.</span></span>

## <a name="grant-dbmanager-permissions-and-create-a-server-level-firewall-rule"></a><span data-ttu-id="d5687-223">Grant dbmanager permissions and create a server-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="d5687-223">Grant dbmanager permissions and create a server-level firewall rule</span></span>

<span data-ttu-id="d5687-224">The steps in this procedure show you how to create a login and user in the master database with permissions to create and manage new user databases.</span><span class="sxs-lookup"><span data-stu-id="d5687-224">The steps in this procedure show you how to create a login and user in the master database with permissions to create and manage new user databases.</span></span> <span data-ttu-id="d5687-225">The steps also show you how to create an additional server-level firewall rule using Transact-SQL using [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5687-225">The steps also show you how to create an additional server-level firewall rule using Transact-SQL using [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx).</span></span> 

> [!IMPORTANT]
><span data-ttu-id="d5687-226">The first server-level firewall rule must always be created in Azure (in the Azure portal, using PowerShell, or the REST API).</span><span class="sxs-lookup"><span data-stu-id="d5687-226">The first server-level firewall rule must always be created in Azure (in the Azure portal, using PowerShell, or the REST API).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="d5687-227">Creating logins in the master database and creating a user account from a login is required for the server admin to delegate create database permissions to another user.</span><span class="sxs-lookup"><span data-stu-id="d5687-227">Creating logins in the master database and creating a user account from a login is required for the server admin to delegate create database permissions to another user.</span></span> <span data-ttu-id="d5687-228">However, creating logins and then creating users from logins decreases the portability of your environment.</span><span class="sxs-lookup"><span data-stu-id="d5687-228">However, creating logins and then creating users from logins decreases the portability of your environment.</span></span>
>

1. <span data-ttu-id="d5687-229">Switch to your computer with a connection to SQL Database using the server admin account.</span><span class="sxs-lookup"><span data-stu-id="d5687-229">Switch to your computer with a connection to SQL Database using the server admin account.</span></span>
2. <span data-ttu-id="d5687-230">Open a query window connected to the master database and execute the following statement to create a login called dbcreator in the master database.</span><span class="sxs-lookup"><span data-stu-id="d5687-230">Open a query window connected to the master database and execute the following statement to create a login called dbcreator in the master database.</span></span>

   ```
   CREATE LOGIN dbcreator
   WITH PASSWORD = 'p@ssw0rd';
   ```

3. <span data-ttu-id="d5687-231">In the same query window,</span><span class="sxs-lookup"><span data-stu-id="d5687-231">In the same query window,</span></span> 

   ```
   CREATE USER dbcreator
   FROM LOGIN dbcreator;
   ```

3. <span data-ttu-id="d5687-232">In the same query window, execute the following query to add the dbcreator user to the dbmanager database role.</span><span class="sxs-lookup"><span data-stu-id="d5687-232">In the same query window, execute the following query to add the dbcreator user to the dbmanager database role.</span></span> <span data-ttu-id="d5687-233">This user can now create and manage databases created by the user.</span><span class="sxs-lookup"><span data-stu-id="d5687-233">This user can now create and manage databases created by the user.</span></span>

   ```
   ALTER ROLE dbmanager ADD MEMBER dbcreator; 
   ```

4. <span data-ttu-id="d5687-234">In the same query window, execute the following query to create a server-level firewall by executing [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) using an IP address appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="d5687-234">In the same query window, execute the following query to create a server-level firewall by executing [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) using an IP address appropriate for your environment:</span></span>

   ```
   EXEC sp_set_firewall_rule @name = N'dbcreatorFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
   ```

5. <span data-ttu-id="d5687-235">Switch computers (to one for which you have created a server-level firewall rule) and connect to the master database using the dbcreator user account.</span><span class="sxs-lookup"><span data-stu-id="d5687-235">Switch computers (to one for which you have created a server-level firewall rule) and connect to the master database using the dbcreator user account.</span></span>
6. <span data-ttu-id="d5687-236">Open a query window to the master database and execute the following query to create a database called foo.</span><span class="sxs-lookup"><span data-stu-id="d5687-236">Open a query window to the master database and execute the following query to create a database called foo.</span></span>

   ```
   CREATE DATABASE FOO (EDITION = 'basic');
   ```
 7. <span data-ttu-id="d5687-237">Optionally, delete this database to save money using the following statement:</span><span class="sxs-lookup"><span data-stu-id="d5687-237">Optionally, delete this database to save money using the following statement:</span></span>

   ```
   DROP DATABASE FOO;
   ```

## <a name="complete-script"></a><span data-ttu-id="d5687-238">Complete script</span><span class="sxs-lookup"><span data-stu-id="d5687-238">Complete script</span></span>

<span data-ttu-id="d5687-239">To create the logins and users, add them to roles, grant them permissions, create database-level firewall rules, and create server-level firewall rules, execute the following statements in the appropriate databases on your server.</span><span class="sxs-lookup"><span data-stu-id="d5687-239">To create the logins and users, add them to roles, grant them permissions, create database-level firewall rules, and create server-level firewall rules, execute the following statements in the appropriate databases on your server.</span></span>

### <a name="master-database"></a><span data-ttu-id="d5687-240">master database</span><span class="sxs-lookup"><span data-stu-id="d5687-240">master database</span></span>
<span data-ttu-id="d5687-241">Execute these statements in the master database using the server admin account, adding the appropriate IP addresses or range.</span><span class="sxs-lookup"><span data-stu-id="d5687-241">Execute these statements in the master database using the server admin account, adding the appropriate IP addresses or range.</span></span>

```
CREATE LOGIN dbcreator WITH PASSWORD = 'p@ssw0rd';
CREATE USER dbcreator FROM LOGIN dbcreator;
ALTER ROLE dbmanager ADD MEMBER dbcreator;
EXEC sp_set_firewall_rule @name = N'dbcreatorFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
```

### <a name="sqldbtutorialdb-database"></a><span data-ttu-id="d5687-242">sqldbtutorialdb database</span><span class="sxs-lookup"><span data-stu-id="d5687-242">sqldbtutorialdb database</span></span>
<span data-ttu-id="d5687-243">Execute these statements in the sqldbtutorialdb database using the server admin account, adding the appropriate IP addresses or range.</span><span class="sxs-lookup"><span data-stu-id="d5687-243">Execute these statements in the sqldbtutorialdb database using the server admin account, adding the appropriate IP addresses or range.</span></span>

```
CREATE USER user1 WITH PASSWORD = 'p@ssw0rd';
GRANT SELECT ON OBJECT::[SalesLT].[ProductCategory] to user1;
EXEC sp_set_database_firewall_rule @name = N'sqldbtutorialdbFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
```

### <a name="blankdb-database"></a><span data-ttu-id="d5687-244">blankdb database</span><span class="sxs-lookup"><span data-stu-id="d5687-244">blankdb database</span></span>
<span data-ttu-id="d5687-245">Execute these statements in the blankdb database using the server admin account, adding the appropriate IP addresses or range.</span><span class="sxs-lookup"><span data-stu-id="d5687-245">Execute these statements in the blankdb database using the server admin account, adding the appropriate IP addresses or range.</span></span>

```
CREATE USER blankdbadmin
   WITH PASSWORD = 'p@ssw0rd';
ALTER ROLE db_owner ADD MEMBER blankdbadmin;
EXEC sp_set_database_firewall_rule @name = N'blankdbFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
CREATE USER blankdbuser1
   WITH PASSWORD = 'p@ssw0rd';
```

## <a name="next-steps"></a><span data-ttu-id="d5687-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5687-246">Next steps</span></span>
- <span data-ttu-id="d5687-247">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-247">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span></span>
- <span data-ttu-id="d5687-248">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-248">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span></span>
- <span data-ttu-id="d5687-249">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5687-249">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
- <span data-ttu-id="d5687-250">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5687-250">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span></span>
- <span data-ttu-id="d5687-251">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-251">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span>
- <span data-ttu-id="d5687-252">For a tutorial using Azure Active Directory authentication, see [Azure AD authentication and authorization](sql-database-control-access-aad-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5687-252">For a tutorial using Azure Active Directory authentication, see [Azure AD authentication and authorization](sql-database-control-access-aad-authentication-get-started.md).</span></span>






















