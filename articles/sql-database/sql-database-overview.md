---
title: What is an Azure SQL database? | Microsoft Docs
description: This article provides an overview of Azure SQL databases.
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: DBs and servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 11/28/2016
ms.author: carlrab
ms.openlocfilehash: ebfc2a6a2e16140953abbb9da3b81702fcc26e60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552275"
---
# <a name="azure-sql-database-overview"></a><span data-ttu-id="7294d-104">Azure SQL database overview</span><span class="sxs-lookup"><span data-stu-id="7294d-104">Azure SQL database overview</span></span>
<span data-ttu-id="7294d-105">This topic provides an overview of Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="7294d-105">This topic provides an overview of Azure SQL databases.</span></span> <span data-ttu-id="7294d-106">For information about Azure SQL logical servers, see [Logical servers](sql-database-server-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-106">For information about Azure SQL logical servers, see [Logical servers](sql-database-server-overview.md).</span></span>

## <a name="what-is-azure-sql-database"></a><span data-ttu-id="7294d-107">What is Azure SQL database?</span><span class="sxs-lookup"><span data-stu-id="7294d-107">What is Azure SQL database?</span></span>
<span data-ttu-id="7294d-108">Each database in Azure SQL Database is associated with a logical server.</span><span class="sxs-lookup"><span data-stu-id="7294d-108">Each database in Azure SQL Database is associated with a logical server.</span></span> <span data-ttu-id="7294d-109">The database can be:</span><span class="sxs-lookup"><span data-stu-id="7294d-109">The database can be:</span></span>

- <span data-ttu-id="7294d-110">A single database with its [own set of resources](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTUs)</span><span class="sxs-lookup"><span data-stu-id="7294d-110">A single database with its [own set of resources](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTUs)</span></span>
- <span data-ttu-id="7294d-111">Part of an [elastic pool](sql-database-elastic-pool.md) that [shares a set of resources](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (eDTUs)</span><span class="sxs-lookup"><span data-stu-id="7294d-111">Part of an [elastic pool](sql-database-elastic-pool.md) that [shares a set of resources](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (eDTUs)</span></span>
- <span data-ttu-id="7294d-112">Part of a [scaled-out set of sharded databases](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), which can be either single or pooled databases</span><span class="sxs-lookup"><span data-stu-id="7294d-112">Part of a [scaled-out set of sharded databases](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), which can be either single or pooled databases</span></span>
- <span data-ttu-id="7294d-113">Part of a set of databases participating in a [multitenant SaaS design pattern](sql-database-design-patterns-multi-tenancy-saas-applications.md), and whose databases can either be single or pooled databases (or both)</span><span class="sxs-lookup"><span data-stu-id="7294d-113">Part of a set of databases participating in a [multitenant SaaS design pattern](sql-database-design-patterns-multi-tenancy-saas-applications.md), and whose databases can either be single or pooled databases (or both)</span></span> 

## <a name="how-do-i-connect-and-authenticate-to-an-azure-sql-database"></a><span data-ttu-id="7294d-114">How do I connect and authenticate to an Azure SQL database?</span><span class="sxs-lookup"><span data-stu-id="7294d-114">How do I connect and authenticate to an Azure SQL database?</span></span>

- <span data-ttu-id="7294d-115">**Authentication and authorization**: Azure SQL Database supports SQL authentication and Azure Active Directory Authentication (with certain limitations - see [Connect to SQL Database with Azure Active Directory Authentication](sql-database-aad-authentication.md) for authentication.</span><span class="sxs-lookup"><span data-stu-id="7294d-115">**Authentication and authorization**: Azure SQL Database supports SQL authentication and Azure Active Directory Authentication (with certain limitations - see [Connect to SQL Database with Azure Active Directory Authentication](sql-database-aad-authentication.md) for authentication.</span></span> <span data-ttu-id="7294d-116">You can connect and authenticate to Azure SQL databases through the server's master database or directly to a user database.</span><span class="sxs-lookup"><span data-stu-id="7294d-116">You can connect and authenticate to Azure SQL databases through the server's master database or directly to a user database.</span></span> <span data-ttu-id="7294d-117">For more information, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-117">For more information, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> <span data-ttu-id="7294d-118">Windows Authentication is not supported.</span><span class="sxs-lookup"><span data-stu-id="7294d-118">Windows Authentication is not supported.</span></span> 
- <span data-ttu-id="7294d-119">**TDS**: Microsoft Azure SQL Database supports tabular data stream (TDS) protocol client version 7.3 or later.</span><span class="sxs-lookup"><span data-stu-id="7294d-119">**TDS**: Microsoft Azure SQL Database supports tabular data stream (TDS) protocol client version 7.3 or later.</span></span>
- <span data-ttu-id="7294d-120">**TCP/IP**: Only TCP/IP connections are allowed.</span><span class="sxs-lookup"><span data-stu-id="7294d-120">**TCP/IP**: Only TCP/IP connections are allowed.</span></span>
- <span data-ttu-id="7294d-121">**SQL Database firewall**: To help protect your data, a SQL Database firewall prevents all access to your database server or its databases until you specify which computers have permission.</span><span class="sxs-lookup"><span data-stu-id="7294d-121">**SQL Database firewall**: To help protect your data, a SQL Database firewall prevents all access to your database server or its databases until you specify which computers have permission.</span></span> <span data-ttu-id="7294d-122">See [Firewalls](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="7294d-122">See [Firewalls](sql-database-firewall-configure.md)</span></span>

## <a name="what-collations-are-supported"></a><span data-ttu-id="7294d-123">What collations are supported?</span><span class="sxs-lookup"><span data-stu-id="7294d-123">What collations are supported?</span></span>
<span data-ttu-id="7294d-124">The default database collation used by Microsoft Azure SQL Database is **SQL_LATIN1_GENERAL_CP1_CI_AS**, where **LATIN1_GENERAL** is English (United States), **CP1** is code page 1252, **CI** is case-insensitive, and **AS** is accent-sensitive.</span><span class="sxs-lookup"><span data-stu-id="7294d-124">The default database collation used by Microsoft Azure SQL Database is **SQL_LATIN1_GENERAL_CP1_CI_AS**, where **LATIN1_GENERAL** is English (United States), **CP1** is code page 1252, **CI** is case-insensitive, and **AS** is accent-sensitive.</span></span> <span data-ttu-id="7294d-125">For more information about how to set the collation, see [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).</span><span class="sxs-lookup"><span data-stu-id="7294d-125">For more information about how to set the collation, see [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).</span></span>

## <a name="what-are-the-naming-requirements-for-database-objects"></a><span data-ttu-id="7294d-126">What are the naming requirements for database objects?</span><span class="sxs-lookup"><span data-stu-id="7294d-126">What are the naming requirements for database objects?</span></span>

<span data-ttu-id="7294d-127">Names for all new objects must comply with the SQL Server rules for identifiers.</span><span class="sxs-lookup"><span data-stu-id="7294d-127">Names for all new objects must comply with the SQL Server rules for identifiers.</span></span> <span data-ttu-id="7294d-128">For more information, see [Identifiers](https://msdn.microsoft.com/library/ms175874.aspx).</span><span class="sxs-lookup"><span data-stu-id="7294d-128">For more information, see [Identifiers](https://msdn.microsoft.com/library/ms175874.aspx).</span></span>

## <a name="what-features-are-supported-by-azure-sql-databases"></a><span data-ttu-id="7294d-129">What features are supported by Azure SQL databases?</span><span class="sxs-lookup"><span data-stu-id="7294d-129">What features are supported by Azure SQL databases?</span></span>

<span data-ttu-id="7294d-130">For information about supported features, see [Features](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-130">For information about supported features, see [Features](sql-database-features.md).</span></span> <span data-ttu-id="7294d-131">See also [Azure SQL Database Transact-SQL differences](sql-database-transact-sql-information.md) for more background on the reasons for lack of support for certain types of features.</span><span class="sxs-lookup"><span data-stu-id="7294d-131">See also [Azure SQL Database Transact-SQL differences](sql-database-transact-sql-information.md) for more background on the reasons for lack of support for certain types of features.</span></span>

## <a name="how-do-i-manage-an-azure-sql-database"></a><span data-ttu-id="7294d-132">How do I manage an Azure SQL database?</span><span class="sxs-lookup"><span data-stu-id="7294d-132">How do I manage an Azure SQL database?</span></span>

<span data-ttu-id="7294d-133">You can manage Azure SQL Database logical servers using several methods:</span><span class="sxs-lookup"><span data-stu-id="7294d-133">You can manage Azure SQL Database logical servers using several methods:</span></span>
- [<span data-ttu-id="7294d-134">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7294d-134">Azure portal</span></span>](sql-database-manage-overview.md)
- [<span data-ttu-id="7294d-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7294d-135">PowerShell</span></span>](sql-database-manage-overview.md)
- [<span data-ttu-id="7294d-136">Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="7294d-136">Transact-SQL</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="7294d-137">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7294d-137">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="7294d-138">REST</span><span class="sxs-lookup"><span data-stu-id="7294d-138">REST</span></span>](/rest/api/sql/)

## <a name="next-steps"></a><span data-ttu-id="7294d-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="7294d-139">Next steps</span></span>

- <span data-ttu-id="7294d-140">For information about the Azure SQL Database service, see [What is SQL Database?](sql-database-technical-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7294d-140">For information about the Azure SQL Database service, see [What is SQL Database?](sql-database-technical-overview.md)</span></span>
- <span data-ttu-id="7294d-141">For information about supported features, see [Features](sql-database-features.md)</span><span class="sxs-lookup"><span data-stu-id="7294d-141">For information about supported features, see [Features](sql-database-features.md)</span></span>
- <span data-ttu-id="7294d-142">For an overview of Azure SQL logical servers, see [SQL Database logical server overview](sql-database-server-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7294d-142">For an overview of Azure SQL logical servers, see [SQL Database logical server overview](sql-database-server-overview.md)</span></span>
- <span data-ttu-id="7294d-143">For information about Transact-SQL support and differences, see [Azure SQL Database Transact-SQL differences](sql-database-transact-sql-information.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-143">For information about Transact-SQL support and differences, see [Azure SQL Database Transact-SQL differences](sql-database-transact-sql-information.md).</span></span>
- <span data-ttu-id="7294d-144">For information about specific resource quotas and limitations based on your **service tier**.</span><span class="sxs-lookup"><span data-stu-id="7294d-144">For information about specific resource quotas and limitations based on your **service tier**.</span></span> <span data-ttu-id="7294d-145">For an overview of service tiers, see [SQL Database service tiers](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-145">For an overview of service tiers, see [SQL Database service tiers](sql-database-service-tiers.md).</span></span>
- <span data-ttu-id="7294d-146">For an overview of security, see [Azure SQL Database Security Overview](sql-database-security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-146">For an overview of security, see [Azure SQL Database Security Overview](sql-database-security-overview.md).</span></span>
- <span data-ttu-id="7294d-147">For information on driver availability and support for SQL Database, see [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="7294d-147">For information on driver availability and support for SQL Database, see [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md).</span></span>

