---
title: Authenticate to Azure SQL Data Warehouse | Microsoft Docs
description: Learn how to authenticate to Azure SQL Data Warehouse by using Azure Active Directory (AAD) or SQL Server authentication.
services: sql-data-warehouse
author: kavithaj
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/12/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: d082ba8bd2819450609a8a6e4ab41b4320158d4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789235"
---
# <a name="authenticate-to-azure-sql-data-warehouse"></a><span data-ttu-id="799d9-103">Authenticate to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="799d9-103">Authenticate to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="799d9-104">Learn how to authenticate to Azure SQL Data Warehouse by using Azure Active Directory (AAD) or SQL Server authentication.</span><span class="sxs-lookup"><span data-stu-id="799d9-104">Learn how to authenticate to Azure SQL Data Warehouse by using Azure Active Directory (AAD) or SQL Server authentication.</span></span>

<span data-ttu-id="799d9-105">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span><span class="sxs-lookup"><span data-stu-id="799d9-105">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="799d9-106">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span><span class="sxs-lookup"><span data-stu-id="799d9-106">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="799d9-107">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="799d9-107">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="799d9-108">SQL authentication</span><span class="sxs-lookup"><span data-stu-id="799d9-108">SQL authentication</span></span>
<span data-ttu-id="799d9-109">To connect to SQL Data Warehouse, you must provide the following information:</span><span class="sxs-lookup"><span data-stu-id="799d9-109">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="799d9-110">Fully qualified servername</span><span class="sxs-lookup"><span data-stu-id="799d9-110">Fully qualified servername</span></span>
* <span data-ttu-id="799d9-111">Specify SQL authentication</span><span class="sxs-lookup"><span data-stu-id="799d9-111">Specify SQL authentication</span></span>
* <span data-ttu-id="799d9-112">Username</span><span class="sxs-lookup"><span data-stu-id="799d9-112">Username</span></span>
* <span data-ttu-id="799d9-113">Password</span><span class="sxs-lookup"><span data-stu-id="799d9-113">Password</span></span>
* <span data-ttu-id="799d9-114">Default database (optional)</span><span class="sxs-lookup"><span data-stu-id="799d9-114">Default database (optional)</span></span>

<span data-ttu-id="799d9-115">By default your connection connects to the *master* database and not your user database.</span><span class="sxs-lookup"><span data-stu-id="799d9-115">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="799d9-116">To connect to your user database, you can choose to do one of two things:</span><span class="sxs-lookup"><span data-stu-id="799d9-116">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="799d9-117">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span><span class="sxs-lookup"><span data-stu-id="799d9-117">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="799d9-118">For example, include the InitialCatalog parameter for an ODBC connection.</span><span class="sxs-lookup"><span data-stu-id="799d9-118">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="799d9-119">Highlight the user database before creating a session in SSDT.</span><span class="sxs-lookup"><span data-stu-id="799d9-119">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="799d9-120">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span><span class="sxs-lookup"><span data-stu-id="799d9-120">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="799d9-121">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span><span class="sxs-lookup"><span data-stu-id="799d9-121">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="799d9-122">Azure Active Directory (AAD) authentication</span><span class="sxs-lookup"><span data-stu-id="799d9-122">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="799d9-123">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="799d9-123">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="799d9-124">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span><span class="sxs-lookup"><span data-stu-id="799d9-124">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="799d9-125">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span><span class="sxs-lookup"><span data-stu-id="799d9-125">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="799d9-126">Benefits</span><span class="sxs-lookup"><span data-stu-id="799d9-126">Benefits</span></span>
<span data-ttu-id="799d9-127">Azure Active Directory benefits include:</span><span class="sxs-lookup"><span data-stu-id="799d9-127">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="799d9-128">Provides an alternative to SQL Server authentication.</span><span class="sxs-lookup"><span data-stu-id="799d9-128">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="799d9-129">Helps stop the proliferation of user identities across database servers.</span><span class="sxs-lookup"><span data-stu-id="799d9-129">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="799d9-130">Allows password rotation in a single place</span><span class="sxs-lookup"><span data-stu-id="799d9-130">Allows password rotation in a single place</span></span>
* <span data-ttu-id="799d9-131">Manage database permissions using external (AAD) groups.</span><span class="sxs-lookup"><span data-stu-id="799d9-131">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="799d9-132">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="799d9-132">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="799d9-133">Uses contained database users to authenticate identities at the database level.</span><span class="sxs-lookup"><span data-stu-id="799d9-133">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="799d9-134">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="799d9-134">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="799d9-135">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="799d9-135">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="799d9-136">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="799d9-136">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="799d9-137">Azure Active Directory is still relatively new and has some limitations.</span><span class="sxs-lookup"><span data-stu-id="799d9-137">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="799d9-138">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span><span class="sxs-lookup"><span data-stu-id="799d9-138">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="799d9-139">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="799d9-139">Configuration steps</span></span>
<span data-ttu-id="799d9-140">Follow these steps to configure Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="799d9-140">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="799d9-141">Create and populate an Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="799d9-141">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="799d9-142">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="799d9-142">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="799d9-143">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="799d9-143">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="799d9-144">Configure your client computers</span><span class="sxs-lookup"><span data-stu-id="799d9-144">Configure your client computers</span></span>
5. <span data-ttu-id="799d9-145">Create contained database users in your database mapped to Azure AD identities</span><span class="sxs-lookup"><span data-stu-id="799d9-145">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="799d9-146">Connect to your data warehouse by using Azure AD identities</span><span class="sxs-lookup"><span data-stu-id="799d9-146">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="799d9-147">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="799d9-147">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="799d9-148">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="799d9-148">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="799d9-149">Find the details</span><span class="sxs-lookup"><span data-stu-id="799d9-149">Find the details</span></span>
* <span data-ttu-id="799d9-150">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="799d9-150">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="799d9-151">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="799d9-151">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="799d9-152">Create custom database roles and add users to the roles.</span><span class="sxs-lookup"><span data-stu-id="799d9-152">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="799d9-153">Then grant granular permissions to the roles.</span><span class="sxs-lookup"><span data-stu-id="799d9-153">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="799d9-154">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="799d9-154">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="799d9-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="799d9-155">Next steps</span></span>
<span data-ttu-id="799d9-156">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="799d9-156">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]:../active-directory/fundamentals/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
