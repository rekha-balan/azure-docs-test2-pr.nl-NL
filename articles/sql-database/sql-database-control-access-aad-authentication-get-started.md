---
title: 'AAD auth: Azure SQL Database firewalls, authentication, access | Microsoft Docs'
description: In this how-to guide, you learn how to use SQL Server Management Studio and Transact-SQL to work with server-level and database-level firewall rules, Azure Active Directory authentication, logins, users, and roles to grant access and control to Azure SQL Database servers and databases.
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
ms.date: 01/17/2017
ms.author: carlrab
ms.openlocfilehash: 14a04dac8211889f2783cf7f4de69cd3239ddb1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549576"
---
# <a name="azure-ad-authentication-access-and-database-level-firewall-rules"></a><span data-ttu-id="08fcb-103">Azure AD authentication, access, and database-level firewall rules</span><span class="sxs-lookup"><span data-stu-id="08fcb-103">Azure AD authentication, access, and database-level firewall rules</span></span>
<span data-ttu-id="08fcb-104">In this how-to guide, you learn how to use SQL Server Management Studio to work with Azure Active Directory authentication, logins, users, and database roles that grant access and permissions to Azure SQL Database servers and databases.</span><span class="sxs-lookup"><span data-stu-id="08fcb-104">In this how-to guide, you learn how to use SQL Server Management Studio to work with Azure Active Directory authentication, logins, users, and database roles that grant access and permissions to Azure SQL Database servers and databases.</span></span> <span data-ttu-id="08fcb-105">You learn to:</span><span class="sxs-lookup"><span data-stu-id="08fcb-105">You learn to:</span></span>

- <span data-ttu-id="08fcb-106">View user permissions in the master database and in user databases</span><span class="sxs-lookup"><span data-stu-id="08fcb-106">View user permissions in the master database and in user databases</span></span>
- <span data-ttu-id="08fcb-107">Create logins and users based on Azure Active Directory authentication</span><span class="sxs-lookup"><span data-stu-id="08fcb-107">Create logins and users based on Azure Active Directory authentication</span></span>
- <span data-ttu-id="08fcb-108">Grant server-wide and database-specific permissions to users</span><span class="sxs-lookup"><span data-stu-id="08fcb-108">Grant server-wide and database-specific permissions to users</span></span>
- <span data-ttu-id="08fcb-109">Log in to a user database as a non-admin user</span><span class="sxs-lookup"><span data-stu-id="08fcb-109">Log in to a user database as a non-admin user</span></span>
- <span data-ttu-id="08fcb-110">Create database-level firewall rules for database users</span><span class="sxs-lookup"><span data-stu-id="08fcb-110">Create database-level firewall rules for database users</span></span>
- <span data-ttu-id="08fcb-111">Create server-level firewall rules for server admins</span><span class="sxs-lookup"><span data-stu-id="08fcb-111">Create server-level firewall rules for server admins</span></span>

<span data-ttu-id="08fcb-112">**Time estimate**: This how-to guide takes approximately 45 minutes to complete (assuming you have already met the prerequisites).</span><span class="sxs-lookup"><span data-stu-id="08fcb-112">**Time estimate**: This how-to guide takes approximately 45 minutes to complete (assuming you have already met the prerequisites).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08fcb-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="08fcb-113">Prerequisites</span></span>

* <span data-ttu-id="08fcb-114">**An Azure account**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-114">**An Azure account**.</span></span> <span data-ttu-id="08fcb-115">You need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="08fcb-115">You need an Azure account.</span></span> <span data-ttu-id="08fcb-116">You can [open a free Azure account](https://azure.microsoft.com/free/) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/).</span><span class="sxs-lookup"><span data-stu-id="08fcb-116">You can [open a free Azure account](https://azure.microsoft.com/free/) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/).</span></span> 

* <span data-ttu-id="08fcb-117">**Azure create permissions**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-117">**Azure create permissions**.</span></span> <span data-ttu-id="08fcb-118">You must be able to connect to the Azure portal using an account that is a member of either the subscription owner or contributor role.</span><span class="sxs-lookup"><span data-stu-id="08fcb-118">You must be able to connect to the Azure portal using an account that is a member of either the subscription owner or contributor role.</span></span> <span data-ttu-id="08fcb-119">For more information on role-based access control (RBAC), see [Getting started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-119">For more information on role-based access control (RBAC), see [Getting started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

* <span data-ttu-id="08fcb-120">**SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-120">**SQL Server Management Studio**.</span></span> <span data-ttu-id="08fcb-121">You can download and install the latest version of SQL Server Management Studio (SSMS) at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="08fcb-121">You can download and install the latest version of SQL Server Management Studio (SSMS) at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> <span data-ttu-id="08fcb-122">Always use the latest version of SSMS when connecting to Azure SQL Database as new capabilities are continually being released.</span><span class="sxs-lookup"><span data-stu-id="08fcb-122">Always use the latest version of SSMS when connecting to Azure SQL Database as new capabilities are continually being released.</span></span>

* <span data-ttu-id="08fcb-123">**Base server and databases** To install and configure a server and the two databases used in this how-to guide, click the **Deploy to Azure** button.</span><span class="sxs-lookup"><span data-stu-id="08fcb-123">**Base server and databases** To install and configure a server and the two databases used in this how-to guide, click the **Deploy to Azure** button.</span></span> <span data-ttu-id="08fcb-124">Clicking the button opens the **Deploy from a template** blade; create a new resource group, and provide the **Admin Login Password** for the new server that will be created:</span><span class="sxs-lookup"><span data-stu-id="08fcb-124">Clicking the button opens the **Deploy from a template** blade; create a new resource group, and provide the **Admin Login Password** for the new server that will be created:</span></span>

   <span data-ttu-id="08fcb-125">[![download](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fsqldbtutorial.blob.core.windows.net%2Ftemplates%2Fsqldbgetstarted.json)</span><span class="sxs-lookup"><span data-stu-id="08fcb-125">[![download](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fsqldbtutorial.blob.core.windows.net%2Ftemplates%2Fsqldbgetstarted.json)</span></span>

   > [!NOTE]
   > <span data-ttu-id="08fcb-126">The completion of the related how-to guide for SQL Server authentication, [SQL authentication, logins and user accounts, database roles, permissions, server-level firewall rules, and database-level firewall rules](sql-database-control-access-sql-authentication-get-started.md), is optional - however, there are concepts covered in that how-to guide that are not repeated here.</span><span class="sxs-lookup"><span data-stu-id="08fcb-126">The completion of the related how-to guide for SQL Server authentication, [SQL authentication, logins and user accounts, database roles, permissions, server-level firewall rules, and database-level firewall rules](sql-database-control-access-sql-authentication-get-started.md), is optional - however, there are concepts covered in that how-to guide that are not repeated here.</span></span> <span data-ttu-id="08fcb-127">The procedures in this how-to guide related to server and database level firewalls are not required if you completed this related how-to guide on the same computers (with the same IP addresses) and are marked as optional for that reason.</span><span class="sxs-lookup"><span data-stu-id="08fcb-127">The procedures in this how-to guide related to server and database level firewalls are not required if you completed this related how-to guide on the same computers (with the same IP addresses) and are marked as optional for that reason.</span></span> <span data-ttu-id="08fcb-128">Also, the screenshots in this how-to guide assume that you have completed of this related how-to guide.</span><span class="sxs-lookup"><span data-stu-id="08fcb-128">Also, the screenshots in this how-to guide assume that you have completed of this related how-to guide.</span></span> 
   >

* <span data-ttu-id="08fcb-129">You have created and populated an Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08fcb-129">You have created and populated an Azure Active Directory.</span></span> <span data-ttu-id="08fcb-130">For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx), and [Hybrid Identity Required Ports and Protocols](../active-directory/active-directory-aadconnect-ports.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-130">For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx), and [Hybrid Identity Required Ports and Protocols](../active-directory/active-directory-aadconnect-ports.md).</span></span>

> [!NOTE]
> <span data-ttu-id="08fcb-131">This how-to guide helps you to learn the content of these learn topics: [SQL Database access and control](sql-database-control-access.md), [Logins, users, and database roles](sql-database-manage-logins.md), [Principals](https://msdn.microsoft.com/library/ms181127.aspx), [Database roles](https://msdn.microsoft.com/library/ms189121.aspx), [SQL Database firewall rules](sql-database-firewall-configure.md), and [Azure Active Directory authentication](sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-131">This how-to guide helps you to learn the content of these learn topics: [SQL Database access and control](sql-database-control-access.md), [Logins, users, and database roles](sql-database-manage-logins.md), [Principals](https://msdn.microsoft.com/library/ms181127.aspx), [Database roles](https://msdn.microsoft.com/library/ms189121.aspx), [SQL Database firewall rules](sql-database-firewall-configure.md), and [Azure Active Directory authentication](sql-database-aad-authentication.md).</span></span> 
>  

## <a name="sign-in-to-the-azure-portal-using-your-azure-account"></a><span data-ttu-id="08fcb-132">Sign in to the Azure portal using your Azure account</span><span class="sxs-lookup"><span data-stu-id="08fcb-132">Sign in to the Azure portal using your Azure account</span></span>
<span data-ttu-id="08fcb-133">Using your [existing subscription](https://account.windowsazure.com/Home/Index), follow these steps to connect to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="08fcb-133">Using your [existing subscription](https://account.windowsazure.com/Home/Index), follow these steps to connect to the Azure portal.</span></span>

1. <span data-ttu-id="08fcb-134">Open your browser of choice and connect to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="08fcb-134">Open your browser of choice and connect to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="08fcb-135">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="08fcb-135">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
3. <span data-ttu-id="08fcb-136">On the **Sign in** page, provide the credentials for your subscription.</span><span class="sxs-lookup"><span data-stu-id="08fcb-136">On the **Sign in** page, provide the credentials for your subscription.</span></span>
   
## <a name="provision-an-azure-active-directory-admin-for-your-sql-logical-server"></a><span data-ttu-id="08fcb-137">Provision an Azure Active Directory admin for your SQL logical server</span><span class="sxs-lookup"><span data-stu-id="08fcb-137">Provision an Azure Active Directory admin for your SQL logical server</span></span>

<span data-ttu-id="08fcb-138">In this section of the how-to guide, you view information about the security configuration for your logical server in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="08fcb-138">In this section of the how-to guide, you view information about the security configuration for your logical server in the Azure portal.</span></span>

1. <span data-ttu-id="08fcb-139">Open the **SQL Server** blade for your logical server and view the information in the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="08fcb-139">Open the **SQL Server** blade for your logical server and view the information in the **Overview** page.</span></span> <span data-ttu-id="08fcb-140">Notice that an Azure Active Directory admin has not been configured.</span><span class="sxs-lookup"><span data-stu-id="08fcb-140">Notice that an Azure Active Directory admin has not been configured.</span></span>

   ![Server admin account in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/sql_admin_portal.png)

2. <span data-ttu-id="08fcb-142">Click **Not configured** in the **Essentials** pane to open the **Active Directory admin** blade.</span><span class="sxs-lookup"><span data-stu-id="08fcb-142">Click **Not configured** in the **Essentials** pane to open the **Active Directory admin** blade.</span></span>

   ![AAD blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/aad_blade.png)

3. <span data-ttu-id="08fcb-144">Click **Set admin** to open the **Add admin** blade and then select an Active Directory user or group account as the Active Directory admin for your server.</span><span class="sxs-lookup"><span data-stu-id="08fcb-144">Click **Set admin** to open the **Add admin** blade and then select an Active Directory user or group account as the Active Directory admin for your server.</span></span>

   ![Select AAD admin account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/aad_admin.png)

4. <span data-ttu-id="08fcb-146">Click **Select** and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-146">Click **Select** and then click **Save**.</span></span>

   ![Save selected AAD admin account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/aad_admin_save.png)

> [!NOTE]
> <span data-ttu-id="08fcb-148">To review connection information for this server, go to [Connect with SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-148">To review connection information for this server, go to [Connect with SSMS](sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="08fcb-149">For this how-to guide series, the fully qualified server name is 'sqldbtutorialserver.database.windows.net'.</span><span class="sxs-lookup"><span data-stu-id="08fcb-149">For this how-to guide series, the fully qualified server name is 'sqldbtutorialserver.database.windows.net'.</span></span>
>

## <a name="connect-to-sql-server-using-sql-server-management-studio-ssms"></a><span data-ttu-id="08fcb-150">Connect to SQL server using SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="08fcb-150">Connect to SQL server using SQL Server Management Studio (SSMS)</span></span>

1. <span data-ttu-id="08fcb-151">If you have not already done so, download and install the latest version of SSMS at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="08fcb-151">If you have not already done so, download and install the latest version of SSMS at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> <span data-ttu-id="08fcb-152">To stay up-to-date, the latest version of SSMS prompts you when there is a new version available to download.</span><span class="sxs-lookup"><span data-stu-id="08fcb-152">To stay up-to-date, the latest version of SSMS prompts you when there is a new version available to download.</span></span>

2. <span data-ttu-id="08fcb-153">After installing, type **Microsoft SQL Server Management Studio** in the Windows search box and click **Enter** to open SSMS.</span><span class="sxs-lookup"><span data-stu-id="08fcb-153">After installing, type **Microsoft SQL Server Management Studio** in the Windows search box and click **Enter** to open SSMS.</span></span>

   ![SQL Server Management Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/ssms.png)

3. <span data-ttu-id="08fcb-155">In the **Connect to Server** dialog box, select one of the Active Directory authentication methods and then provide the appropriate authentication information.</span><span class="sxs-lookup"><span data-stu-id="08fcb-155">In the **Connect to Server** dialog box, select one of the Active Directory authentication methods and then provide the appropriate authentication information.</span></span> <span data-ttu-id="08fcb-156">For information on choosing a method, see [Azure Active Directory authentication](sql-database-aad-authentication.md) and [SSMS support for Azure AD MFA](sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-156">For information on choosing a method, see [Azure Active Directory authentication](sql-database-aad-authentication.md) and [SSMS support for Azure AD MFA](sql-database-ssms-mfa-authentication.md).</span></span>

   ![connect to server with aad](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/connect_to_server_with_aad.png)

4. <span data-ttu-id="08fcb-158">Enter the necessary information to connect to your SQL server using SQL Server Authentication and the Server admin account.</span><span class="sxs-lookup"><span data-stu-id="08fcb-158">Enter the necessary information to connect to your SQL server using SQL Server Authentication and the Server admin account.</span></span>

5. <span data-ttu-id="08fcb-159">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-159">Click **Connect**.</span></span>

   ![connected to server with aad](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/connected_to_server_with_aad.png)

## <a name="view-the-server-admin-account-and-its-permissions"></a><span data-ttu-id="08fcb-161">View the Server admin account and its permissions</span><span class="sxs-lookup"><span data-stu-id="08fcb-161">View the Server admin account and its permissions</span></span> 
<span data-ttu-id="08fcb-162">In this section of the how-to guide, you view information about the server admin account and its permissions in the master database and in user databases.</span><span class="sxs-lookup"><span data-stu-id="08fcb-162">In this section of the how-to guide, you view information about the server admin account and its permissions in the master database and in user databases.</span></span>

1. <span data-ttu-id="08fcb-163">In Object Explorer, expand **Databases**, expand **System databases**, expand **master**, expand **Security**, and then expand **Users**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-163">In Object Explorer, expand **Databases**, expand **System databases**, expand **master**, expand **Security**, and then expand **Users**.</span></span> <span data-ttu-id="08fcb-164">Notice that a user account has been created in the master database for the Active Directory admin. Notice also that a login was not created for Active Directory admin user account.</span><span class="sxs-lookup"><span data-stu-id="08fcb-164">Notice that a user account has been created in the master database for the Active Directory admin. Notice also that a login was not created for Active Directory admin user account.</span></span>

   ![master database user account for AAD admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/master_database_user_account_for_AAD_admin.png)

   > [!NOTE]
   > <span data-ttu-id="08fcb-166">For information about the other user accounts that appear, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span><span class="sxs-lookup"><span data-stu-id="08fcb-166">For information about the other user accounts that appear, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
   >

2. <span data-ttu-id="08fcb-167">In Object Explorer, right-click **master** and then click **New Query** to open a query window connected to the master database.</span><span class="sxs-lookup"><span data-stu-id="08fcb-167">In Object Explorer, right-click **master** and then click **New Query** to open a query window connected to the master database.</span></span>
3. <span data-ttu-id="08fcb-168">In the query window, execute the following query to return information about the user executing the query.</span><span class="sxs-lookup"><span data-stu-id="08fcb-168">In the query window, execute the following query to return information about the user executing the query.</span></span> <span data-ttu-id="08fcb-169">Notice that user@microsoft.com is returned for the user account executing this query (we see a different result when we query a user database later in this procedure).</span><span class="sxs-lookup"><span data-stu-id="08fcb-169">Notice that user@microsoft.com is returned for the user account executing this query (we see a different result when we query a user database later in this procedure).</span></span>

   ```
   SELECT USER;
   ```

   ![select user query in the master database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/select_user_query_in_master_database.png)

4. <span data-ttu-id="08fcb-171">In the query window, execute the following query to return information about the permissions of the Active Directory admin user.</span><span class="sxs-lookup"><span data-stu-id="08fcb-171">In the query window, execute the following query to return information about the permissions of the Active Directory admin user.</span></span> <span data-ttu-id="08fcb-172">Notice that the Active Directory admin user has permissions to connect to the master database, create logins and users, select information from the sys.sql_logins table, and add users to the dbmanager and dbcreator database roles.</span><span class="sxs-lookup"><span data-stu-id="08fcb-172">Notice that the Active Directory admin user has permissions to connect to the master database, create logins and users, select information from the sys.sql_logins table, and add users to the dbmanager and dbcreator database roles.</span></span> <span data-ttu-id="08fcb-173">These permissions are in addition to permissions granted to the public role from which all users inherit permissions (such as permissions to select information from certain tables).</span><span class="sxs-lookup"><span data-stu-id="08fcb-173">These permissions are in addition to permissions granted to the public role from which all users inherit permissions (such as permissions to select information from certain tables).</span></span> <span data-ttu-id="08fcb-174">See [Permissions](https://msdn.microsoft.com/library/ms191291.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="08fcb-174">See [Permissions](https://msdn.microsoft.com/library/ms191291.aspx) for more information.</span></span>

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
   WHERE p.name = 'user@microsoft.com';
   ```

   ![aad admin permissions in the master database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/aad_admin_permissions_in_master_database.png)

6. <span data-ttu-id="08fcb-176">In Object Explorer, expand **blankdb**, expand **Security**, and then expand **Users**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-176">In Object Explorer, expand **blankdb**, expand **Security**, and then expand **Users**.</span></span> <span data-ttu-id="08fcb-177">Notice that there is no user account called user@microsoft.com in this database.</span><span class="sxs-lookup"><span data-stu-id="08fcb-177">Notice that there is no user account called user@microsoft.com in this database.</span></span>

   ![user accounts in blankdb](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/user_accounts_in_blankdb.png)

7. <span data-ttu-id="08fcb-179">In Object Explorer, right-click **blankdb** and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-179">In Object Explorer, right-click **blankdb** and then click **New Query**.</span></span>

8. <span data-ttu-id="08fcb-180">In the query window, execute the following query to return information about the user executing the query.</span><span class="sxs-lookup"><span data-stu-id="08fcb-180">In the query window, execute the following query to return information about the user executing the query.</span></span> <span data-ttu-id="08fcb-181">Notice that dbo is returned for the user account executing this query (by default, the Server admin login is mapped to the dbo user account in each user database).</span><span class="sxs-lookup"><span data-stu-id="08fcb-181">Notice that dbo is returned for the user account executing this query (by default, the Server admin login is mapped to the dbo user account in each user database).</span></span>

   ```
   SELECT USER;
   ```

   ![select user query in the blankdb database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/select_user_query_in_blankdb_database.png)

9. <span data-ttu-id="08fcb-183">In the query window, execute the following query to return information about the permissions of the dbo user.</span><span class="sxs-lookup"><span data-stu-id="08fcb-183">In the query window, execute the following query to return information about the permissions of the dbo user.</span></span> <span data-ttu-id="08fcb-184">Notice that dbo is a member of the public role and also a member of the db_owner fixed database role.</span><span class="sxs-lookup"><span data-stu-id="08fcb-184">Notice that dbo is a member of the public role and also a member of the db_owner fixed database role.</span></span> <span data-ttu-id="08fcb-185">See [Database-Level Roles](https://msdn.microsoft.com/library/ms189121.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="08fcb-185">See [Database-Level Roles](https://msdn.microsoft.com/library/ms189121.aspx) for more information.</span></span>

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

   ![server admin permissions in the blankdb database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/aad_admin_permissions_in_blankdb_database.png)

10. <span data-ttu-id="08fcb-187">Optionally, repeat the previous three steps for the AdventureWorksLT user database.</span><span class="sxs-lookup"><span data-stu-id="08fcb-187">Optionally, repeat the previous three steps for the AdventureWorksLT user database.</span></span>

## <a name="create-a-new-user-in-the-adventureworkslt-database-with-select-permissions"></a><span data-ttu-id="08fcb-188">Create a new user in the AdventureWorksLT database with SELECT permissions</span><span class="sxs-lookup"><span data-stu-id="08fcb-188">Create a new user in the AdventureWorksLT database with SELECT permissions</span></span>

<span data-ttu-id="08fcb-189">In this section of the how-to guide, you create a user account in the AdventureWorksLT database based on a user's principal name of an Azure AD user or display name for an Azure AD group, test this user's permissions as member of the public role, grant this user SELECT permissions, and then test this user's permissions again.</span><span class="sxs-lookup"><span data-stu-id="08fcb-189">In this section of the how-to guide, you create a user account in the AdventureWorksLT database based on a user's principal name of an Azure AD user or display name for an Azure AD group, test this user's permissions as member of the public role, grant this user SELECT permissions, and then test this user's permissions again.</span></span>

> [!NOTE]
> <span data-ttu-id="08fcb-190">Database-level users ([contained users](https://msdn.microsoft.com/library/ff929188.aspx)) increase the portability of your database, a capability that we explore in later how-to guides.</span><span class="sxs-lookup"><span data-stu-id="08fcb-190">Database-level users ([contained users](https://msdn.microsoft.com/library/ff929188.aspx)) increase the portability of your database, a capability that we explore in later how-to guides.</span></span>
>

1. <span data-ttu-id="08fcb-191">In Object Explorer, right-click **AdventureWorksLT** and then click **New Query** to open a query window connected to the AdventureWorksLT database.</span><span class="sxs-lookup"><span data-stu-id="08fcb-191">In Object Explorer, right-click **AdventureWorksLT** and then click **New Query** to open a query window connected to the AdventureWorksLT database.</span></span>
2. <span data-ttu-id="08fcb-192">Execute the following statement to create a user account in the AdventureWorksLT database for a user in the Microsoft domain called aaduser1.</span><span class="sxs-lookup"><span data-stu-id="08fcb-192">Execute the following statement to create a user account in the AdventureWorksLT database for a user in the Microsoft domain called aaduser1.</span></span>

   ```
   CREATE USER [aaduser1@microsoft.com]
   FROM EXTERNAL PROVIDER;
   ```
   ![new user aaduser1@microsoft.com AdventureWorksLT](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/new_user_aaduser1@microsoft.com_aw.png)

3. <span data-ttu-id="08fcb-194">In the query window, execute the following query to return information about the permissions of user1.</span><span class="sxs-lookup"><span data-stu-id="08fcb-194">In the query window, execute the following query to return information about the permissions of user1.</span></span> <span data-ttu-id="08fcb-195">Notice that the only permissions that user1 has are the permissions inherited from the public role.</span><span class="sxs-lookup"><span data-stu-id="08fcb-195">Notice that the only permissions that user1 has are the permissions inherited from the public role.</span></span>

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
   WHERE p.name = 'aaduser1@microsoft.com';
   ```

   ![new user permissions in a user database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/new_user_permissions_in_user_database.png)

4. <span data-ttu-id="08fcb-197">Execute the following queries to attempt to query a table in the AdventureWorksLT database as user1.</span><span class="sxs-lookup"><span data-stu-id="08fcb-197">Execute the following queries to attempt to query a table in the AdventureWorksLT database as user1.</span></span>

   ```
   EXECUTE AS USER = 'aaduser1@microsoft.com';  
   SELECT * FROM [SalesLT].[ProductCategory];
   REVERT;
   ```

   ![no select permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/no_select_permissions.png)

5. <span data-ttu-id="08fcb-199">Execute the following statement to grant SELECT permissions on the ProductCategory table in the SalesLT schema to user1.</span><span class="sxs-lookup"><span data-stu-id="08fcb-199">Execute the following statement to grant SELECT permissions on the ProductCategory table in the SalesLT schema to user1.</span></span>

   ```
   GRANT SELECT ON OBJECT::[SalesLT].[ProductCategory] to [aaduser1@microsoft.com];
   ```

   ![grant select permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/grant_select_permissions.png)

6. <span data-ttu-id="08fcb-201">Execute the following queries to attempt to query a table in the AdventureWorksLT database as user1.</span><span class="sxs-lookup"><span data-stu-id="08fcb-201">Execute the following queries to attempt to query a table in the AdventureWorksLT database as user1.</span></span>

   ```
   EXECUTE AS USER = 'aaduser1@microsoft.com';  
   SELECT * FROM [SalesLT].[ProductCategory];
   REVERT;
   ```

   ![select permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/select_permissions.png)

## <a name="create-a-database-level-firewall-rule-for-adventureworkslt-database-users"></a><span data-ttu-id="08fcb-203">Create a database-level firewall rule for AdventureWorksLT database users</span><span class="sxs-lookup"><span data-stu-id="08fcb-203">Create a database-level firewall rule for AdventureWorksLT database users</span></span>

> [!NOTE]
> <span data-ttu-id="08fcb-204">You do not need to complete this procedure if you completed the equivalent procedure in the related how-to guide for SQL Server authentication, [SQL authentication and authorization](sql-database-control-access-sql-authentication-get-started.md) and are learning using the same computer with the same IP address.</span><span class="sxs-lookup"><span data-stu-id="08fcb-204">You do not need to complete this procedure if you completed the equivalent procedure in the related how-to guide for SQL Server authentication, [SQL authentication and authorization](sql-database-control-access-sql-authentication-get-started.md) and are learning using the same computer with the same IP address.</span></span>
>

<span data-ttu-id="08fcb-205">In this section of the how-to guide, you attempt to log in using the new user account from a computer with a different IP address, create a database-level firewall rule as the Server admin, and then successfully log in using this new database-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="08fcb-205">In this section of the how-to guide, you attempt to log in using the new user account from a computer with a different IP address, create a database-level firewall rule as the Server admin, and then successfully log in using this new database-level firewall rule.</span></span> 

> [!NOTE]
> <span data-ttu-id="08fcb-206">[Database-level firewall rules](sql-database-firewall-configure.md) increase the portability of your database, a capability that we explore in later how-to guides.</span><span class="sxs-lookup"><span data-stu-id="08fcb-206">[Database-level firewall rules](sql-database-firewall-configure.md) increase the portability of your database, a capability that we explore in later how-to guides.</span></span>
>

1. <span data-ttu-id="08fcb-207">On another computer for which you have not already created a server-level firewall rule, open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="08fcb-207">On another computer for which you have not already created a server-level firewall rule, open SQL Server Management Studio.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="08fcb-208">Always use the latest version of SSMS at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="08fcb-208">Always use the latest version of SSMS at [Download SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 
   >

2. <span data-ttu-id="08fcb-209">In the **Connect to Server** window, enter the server name and authentication information to connect using SQL Server authentication with the aaduser1@microsoft.com account.</span><span class="sxs-lookup"><span data-stu-id="08fcb-209">In the **Connect to Server** window, enter the server name and authentication information to connect using SQL Server authentication with the aaduser1@microsoft.com account.</span></span> 
    
   ![Connect as aaduser1@microsoft.com without firewall rule1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/connect_aaduser1_no_rule1.png)

3. <span data-ttu-id="08fcb-211">Click **Options** in the **Connect to server** dialog box to specify the database to which you want to connect and then type **AdventureWorksLT** in the **Connect to Database** drop-down box on the **Connection Properties** tab.</span><span class="sxs-lookup"><span data-stu-id="08fcb-211">Click **Options** in the **Connect to server** dialog box to specify the database to which you want to connect and then type **AdventureWorksLT** in the **Connect to Database** drop-down box on the **Connection Properties** tab.</span></span>
   
   ![Connect as aaduser1 without firewall rule2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/connect_aaduser1_no_rule2.png)

4. <span data-ttu-id="08fcb-213">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-213">Click **Connect**.</span></span> <span data-ttu-id="08fcb-214">A dialog box appears informing you that the computer from which you are attempting to connect to SQL Database does not have a firewall rule enabling access to the database.</span><span class="sxs-lookup"><span data-stu-id="08fcb-214">A dialog box appears informing you that the computer from which you are attempting to connect to SQL Database does not have a firewall rule enabling access to the database.</span></span> <span data-ttu-id="08fcb-215">The dialog box that you receive has two variations depending upon steps you have previously taken with firewalls, but you usually get the first dialog box shown.</span><span class="sxs-lookup"><span data-stu-id="08fcb-215">The dialog box that you receive has two variations depending upon steps you have previously taken with firewalls, but you usually get the first dialog box shown.</span></span>

   ![Connect as user1 without firewall rule3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/connect_aaduser1_no_rule3.png)

   ![Connect as user1 without firewall rule4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/connect_aaduser1_no_rule4.png)

   > [!NOTE]
   > <span data-ttu-id="08fcb-218">The newest versions of SSMS include the functionality to allow subscription owners and contributors to sign in to Microsoft Azure and create a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="08fcb-218">The newest versions of SSMS include the functionality to allow subscription owners and contributors to sign in to Microsoft Azure and create a server-level firewall rule.</span></span>
   > 

4. <span data-ttu-id="08fcb-219">Copy the client IP address from this dialog box for use in step 7.</span><span class="sxs-lookup"><span data-stu-id="08fcb-219">Copy the client IP address from this dialog box for use in step 7.</span></span>
5. <span data-ttu-id="08fcb-220">Click **Cancel** but do not close the **Connect to Server** dialog box.</span><span class="sxs-lookup"><span data-stu-id="08fcb-220">Click **Cancel** but do not close the **Connect to Server** dialog box.</span></span>
6. <span data-ttu-id="08fcb-221">Switch back to a computer for which you have already created a server-level firewall rule and connect to your server using the Server admin account.</span><span class="sxs-lookup"><span data-stu-id="08fcb-221">Switch back to a computer for which you have already created a server-level firewall rule and connect to your server using the Server admin account.</span></span>
7. <span data-ttu-id="08fcb-222">In a new query window connected to the AdventureWorksLT database as Server admin, execute the following statement to create a database-level firewall by executing [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) using the IP address from step 4:</span><span class="sxs-lookup"><span data-stu-id="08fcb-222">In a new query window connected to the AdventureWorksLT database as Server admin, execute the following statement to create a database-level firewall by executing [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) using the IP address from step 4:</span></span>

   ```
   EXEC sp_set_database_firewall_rule @name = N'AdventureWorksLTFirewallRule', 
     @start_ip_address = 'x.x.x.x', @end_ip_address = 'x.x.x.x';
   ```

   ![add database level firewall rule4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-control-access-aad-authentication-get-started/aaduser1_add_rule_aw.png)

8. <span data-ttu-id="08fcb-224">Switch computers again and click **Connect** in the **Connect to Server** dialog box to connect to AdventureWorksLT as aaduser1.</span><span class="sxs-lookup"><span data-stu-id="08fcb-224">Switch computers again and click **Connect** in the **Connect to Server** dialog box to connect to AdventureWorksLT as aaduser1.</span></span> 

9. <span data-ttu-id="08fcb-225">In Object Explorer, expand **Databases**, expand **AdventureWorksLT**, and then expand **Tables**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-225">In Object Explorer, expand **Databases**, expand **AdventureWorksLT**, and then expand **Tables**.</span></span> <span data-ttu-id="08fcb-226">Notice that user1 only has permission to view a single table, the **SalesLT.ProductCategory** table.</span><span class="sxs-lookup"><span data-stu-id="08fcb-226">Notice that user1 only has permission to view a single table, the **SalesLT.ProductCategory** table.</span></span> 

10. <span data-ttu-id="08fcb-227">In Object Explorer, right-click **SalesLT.ProductCategory** and click **Select Top 1000 Rows**.</span><span class="sxs-lookup"><span data-stu-id="08fcb-227">In Object Explorer, right-click **SalesLT.ProductCategory** and click **Select Top 1000 Rows**.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="08fcb-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="08fcb-228">Next steps</span></span>
- <span data-ttu-id="08fcb-229">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-229">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span></span>
- <span data-ttu-id="08fcb-230">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-230">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span></span>
- <span data-ttu-id="08fcb-231">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span><span class="sxs-lookup"><span data-stu-id="08fcb-231">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
- <span data-ttu-id="08fcb-232">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span><span class="sxs-lookup"><span data-stu-id="08fcb-232">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span></span>
- <span data-ttu-id="08fcb-233">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="08fcb-233">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span>
























