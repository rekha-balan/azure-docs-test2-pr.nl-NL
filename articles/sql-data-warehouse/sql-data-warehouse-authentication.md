---
title: Authentication to Azure SQL Data Warehouse | Microsoft Docs
description: Azure Active Directory (AAD) and SQL Server authentication to Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: ''
author: byham
manager: jhubbard
editor: ''
tags: ''
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rickbyh;barbkess
ms.openlocfilehash: 2e7249dd94c8e369b2849fc2ae419d4cfd1879b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554954"
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="fbe24-103">Authentication to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fbe24-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [Security Overview](sql-data-warehouse-overview-manage-security.md)
> * [Authentication](sql-data-warehouse-authentication.md)
> * [Encryption (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Encryption (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="fbe24-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span><span class="sxs-lookup"><span data-stu-id="fbe24-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="fbe24-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span><span class="sxs-lookup"><span data-stu-id="fbe24-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="fbe24-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fbe24-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="fbe24-111">SQL authentication</span><span class="sxs-lookup"><span data-stu-id="fbe24-111">SQL authentication</span></span>
<span data-ttu-id="fbe24-112">To connect to SQL Data Warehouse, you must provide the following information:</span><span class="sxs-lookup"><span data-stu-id="fbe24-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="fbe24-113">Fully qualified servername</span><span class="sxs-lookup"><span data-stu-id="fbe24-113">Fully qualified servername</span></span>
* <span data-ttu-id="fbe24-114">Specify SQL authentication</span><span class="sxs-lookup"><span data-stu-id="fbe24-114">Specify SQL authentication</span></span>
* <span data-ttu-id="fbe24-115">Username</span><span class="sxs-lookup"><span data-stu-id="fbe24-115">Username</span></span>
* <span data-ttu-id="fbe24-116">Password</span><span class="sxs-lookup"><span data-stu-id="fbe24-116">Password</span></span>
* <span data-ttu-id="fbe24-117">Default database (optional)</span><span class="sxs-lookup"><span data-stu-id="fbe24-117">Default database (optional)</span></span>

<span data-ttu-id="fbe24-118">By default your connection connects to the *master* database and not your user database.</span><span class="sxs-lookup"><span data-stu-id="fbe24-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="fbe24-119">To connect to your user database, you can choose to do one of two things:</span><span class="sxs-lookup"><span data-stu-id="fbe24-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="fbe24-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span><span class="sxs-lookup"><span data-stu-id="fbe24-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="fbe24-121">For example, include the InitialCatalog parameter for an ODBC connection.</span><span class="sxs-lookup"><span data-stu-id="fbe24-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="fbe24-122">Highlight the user database before creating a session in SSDT.</span><span class="sxs-lookup"><span data-stu-id="fbe24-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection. For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="fbe24-125">Azure Active Directory (AAD) authentication</span><span class="sxs-lookup"><span data-stu-id="fbe24-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="fbe24-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbe24-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fbe24-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span><span class="sxs-lookup"><span data-stu-id="fbe24-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="fbe24-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span><span class="sxs-lookup"><span data-stu-id="fbe24-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="fbe24-129">Benefits</span><span class="sxs-lookup"><span data-stu-id="fbe24-129">Benefits</span></span>
<span data-ttu-id="fbe24-130">Azure Active Directory benefits include:</span><span class="sxs-lookup"><span data-stu-id="fbe24-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="fbe24-131">Provides an alternative to SQL Server authentication.</span><span class="sxs-lookup"><span data-stu-id="fbe24-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="fbe24-132">Helps stop the proliferation of user identities across database servers.</span><span class="sxs-lookup"><span data-stu-id="fbe24-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="fbe24-133">Allows password rotation in a single place</span><span class="sxs-lookup"><span data-stu-id="fbe24-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="fbe24-134">Manage database permissions using external (AAD) groups.</span><span class="sxs-lookup"><span data-stu-id="fbe24-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="fbe24-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbe24-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="fbe24-136">Uses contained database users to authenticate identities at the database level.</span><span class="sxs-lookup"><span data-stu-id="fbe24-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="fbe24-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fbe24-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="fbe24-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="fbe24-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="fbe24-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fbe24-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> Azure Active Directory is still relatively new and has some limitations. To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="fbe24-142">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="fbe24-142">Configuration steps</span></span>
<span data-ttu-id="fbe24-143">Follow these steps to configure Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="fbe24-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="fbe24-144">Create and populate an Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbe24-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="fbe24-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="fbe24-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="fbe24-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fbe24-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="fbe24-147">Configure your client computers</span><span class="sxs-lookup"><span data-stu-id="fbe24-147">Configure your client computers</span></span>
5. <span data-ttu-id="fbe24-148">Create contained database users in your database mapped to Azure AD identities</span><span class="sxs-lookup"><span data-stu-id="fbe24-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="fbe24-149">Connect to your data warehouse by using Azure AD identities</span><span class="sxs-lookup"><span data-stu-id="fbe24-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="fbe24-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="fbe24-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="fbe24-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbe24-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="fbe24-152">Find the details</span><span class="sxs-lookup"><span data-stu-id="fbe24-152">Find the details</span></span>
* <span data-ttu-id="fbe24-153">Complete the detailed steps.</span><span class="sxs-lookup"><span data-stu-id="fbe24-153">Complete the detailed steps.</span></span> <span data-ttu-id="fbe24-154">The detailed steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fbe24-154">The detailed steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="fbe24-155">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fbe24-155">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="fbe24-156">Create custom database roles and add users to the roles.</span><span class="sxs-lookup"><span data-stu-id="fbe24-156">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="fbe24-157">Then grant granular permissions to the roles.</span><span class="sxs-lookup"><span data-stu-id="fbe24-157">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="fbe24-158">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbe24-158">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbe24-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbe24-159">Next steps</span></span>
<span data-ttu-id="fbe24-160">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="fbe24-160">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
