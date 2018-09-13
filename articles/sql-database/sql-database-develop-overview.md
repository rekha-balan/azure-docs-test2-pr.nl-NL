---
title: SQL Database Application Development Overview | Microsoft Docs
description: Learn about available connectivity libraries and best practices for applications connecting to SQL Database.
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: development
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 338fa476377e9ff04c9a1f4e585f790b92a59f87
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550419"
---
# <a name="sql-database-application-development-overview"></a><span data-ttu-id="447ed-103">SQL Database Application Development Overview</span><span class="sxs-lookup"><span data-stu-id="447ed-103">SQL Database Application Development Overview</span></span>
<span data-ttu-id="447ed-104">This article walks through the basic considerations that a developer should be aware of when writing code to connect to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="447ed-104">This article walks through the basic considerations that a developer should be aware of when writing code to connect to Azure SQL Database.</span></span>

> [!TIP]
> <span data-ttu-id="447ed-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, connect using SQL Server Management Studio, query the master database, create a sample database and a blank database, query database properties, connect using SQL Server Management Studio, and query the sample database, see [Get Started Tutorial](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="447ed-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, connect using SQL Server Management Studio, query the master database, create a sample database and a blank database, query database properties, connect using SQL Server Management Studio, and query the sample database, see [Get Started Tutorial](sql-database-get-started-portal.md).</span></span>
>

## <a name="language-and-platform"></a><span data-ttu-id="447ed-106">Language and platform</span><span class="sxs-lookup"><span data-stu-id="447ed-106">Language and platform</span></span>
<span data-ttu-id="447ed-107">There are code samples available for various programming languages and platforms.</span><span class="sxs-lookup"><span data-stu-id="447ed-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="447ed-108">You can find links to the code samples at:</span><span class="sxs-lookup"><span data-stu-id="447ed-108">You can find links to the code samples at:</span></span> 

* <span data-ttu-id="447ed-109">More Information: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-109">More Information: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="447ed-110">Tools</span><span class="sxs-lookup"><span data-stu-id="447ed-110">Tools</span></span> 
<span data-ttu-id="447ed-111">You can leverage open source tools like [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="447ed-111">You can leverage open source tools like [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="447ed-112">Additionally, Azure SQL Database works with Microsoft tools like [Visual Studio](https://www.visualstudio.com/visual-studio-homepage-vs.aspx) and  [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="447ed-112">Additionally, Azure SQL Database works with Microsoft tools like [Visual Studio](https://www.visualstudio.com/visual-studio-homepage-vs.aspx) and  [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>  <span data-ttu-id="447ed-113">You can also use the Azure Management Portal, PowerShell, and REST APIs help you gain additional productivity.</span><span class="sxs-lookup"><span data-stu-id="447ed-113">You can also use the Azure Management Portal, PowerShell, and REST APIs help you gain additional productivity.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="447ed-114">Resource limitations</span><span class="sxs-lookup"><span data-stu-id="447ed-114">Resource limitations</span></span>
<span data-ttu-id="447ed-115">Azure SQL Database manages the resources available to a database using two different mechanisms: Resources Governance and Enforcement of Limits.</span><span class="sxs-lookup"><span data-stu-id="447ed-115">Azure SQL Database manages the resources available to a database using two different mechanisms: Resources Governance and Enforcement of Limits.</span></span>

* <span data-ttu-id="447ed-116">More Information: [Azure SQL Database resource limits](sql-database-resource-limits.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-116">More Information: [Azure SQL Database resource limits](sql-database-resource-limits.md)</span></span>

## <a name="security"></a><span data-ttu-id="447ed-117">Security</span><span class="sxs-lookup"><span data-stu-id="447ed-117">Security</span></span>
<span data-ttu-id="447ed-118">Azure SQL Database provides resources for limiting access, protecting data, and monitoring activities on a SQL Database.</span><span class="sxs-lookup"><span data-stu-id="447ed-118">Azure SQL Database provides resources for limiting access, protecting data, and monitoring activities on a SQL Database.</span></span>

* <span data-ttu-id="447ed-119">More Information: [Securing your SQL Database](sql-database-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-119">More Information: [Securing your SQL Database](sql-database-security-overview.md)</span></span>

## <a name="authentication"></a><span data-ttu-id="447ed-120">Authentication</span><span class="sxs-lookup"><span data-stu-id="447ed-120">Authentication</span></span>
* <span data-ttu-id="447ed-121">Azure SQL Database supports both SQL Server authentication users and logins, as well as [Azure Active Directory authentication](sql-database-aad-authentication.md) users and logins.</span><span class="sxs-lookup"><span data-stu-id="447ed-121">Azure SQL Database supports both SQL Server authentication users and logins, as well as [Azure Active Directory authentication](sql-database-aad-authentication.md) users and logins.</span></span>
* <span data-ttu-id="447ed-122">You need to specify a particular database, instead of defaulting to the *master* database.</span><span class="sxs-lookup"><span data-stu-id="447ed-122">You need to specify a particular database, instead of defaulting to the *master* database.</span></span>
* <span data-ttu-id="447ed-123">You cannot use the Transact-SQL **USE myDatabaseName;** statement on SQL Database to switch to another database.</span><span class="sxs-lookup"><span data-stu-id="447ed-123">You cannot use the Transact-SQL **USE myDatabaseName;** statement on SQL Database to switch to another database.</span></span>
* <span data-ttu-id="447ed-124">More information: [SQL Database security: Manage database access and login security](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-124">More information: [SQL Database security: Manage database access and login security](sql-database-manage-logins.md)</span></span>

## <a name="resiliency"></a><span data-ttu-id="447ed-125">Resiliency</span><span class="sxs-lookup"><span data-stu-id="447ed-125">Resiliency</span></span>
<span data-ttu-id="447ed-126">When a transient error occurs while connecting to SQL Database, your code should retry the call.</span><span class="sxs-lookup"><span data-stu-id="447ed-126">When a transient error occurs while connecting to SQL Database, your code should retry the call.</span></span>  <span data-ttu-id="447ed-127">We recommend that retry logic use backoff logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span><span class="sxs-lookup"><span data-stu-id="447ed-127">We recommend that retry logic use backoff logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

* <span data-ttu-id="447ed-128">Code samples:  For code samples that illustrate retry logic, see samples for the language of your choice at: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-128">Code samples:  For code samples that illustrate retry logic, see samples for the language of your choice at: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span></span>
* <span data-ttu-id="447ed-129">More information: [Error messages for SQL Database client programs](sql-database-develop-error-messages.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-129">More information: [Error messages for SQL Database client programs](sql-database-develop-error-messages.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="447ed-130">Managing Connections</span><span class="sxs-lookup"><span data-stu-id="447ed-130">Managing Connections</span></span>
* <span data-ttu-id="447ed-131">In your client connection logic, override the default timeout to be 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="447ed-131">In your client connection logic, override the default timeout to be 30 seconds.</span></span>  <span data-ttu-id="447ed-132">The default of 15 seconds is too short for connections that depend on the internet.</span><span class="sxs-lookup"><span data-stu-id="447ed-132">The default of 15 seconds is too short for connections that depend on the internet.</span></span>
* <span data-ttu-id="447ed-133">If you are using a [connection pool](http://msdn.microsoft.com/library/8xx3tyca.aspx), be sure to close the connection the instant your program is not actively using it, and is not preparing to reuse it.</span><span class="sxs-lookup"><span data-stu-id="447ed-133">If you are using a [connection pool](http://msdn.microsoft.com/library/8xx3tyca.aspx), be sure to close the connection the instant your program is not actively using it, and is not preparing to reuse it.</span></span>

## <a name="network-considerations"></a><span data-ttu-id="447ed-134">Network Considerations</span><span class="sxs-lookup"><span data-stu-id="447ed-134">Network Considerations</span></span>
* <span data-ttu-id="447ed-135">On the computer that hosts your client program, ensure the firewall allows outgoing TCP communication on port 1433.</span><span class="sxs-lookup"><span data-stu-id="447ed-135">On the computer that hosts your client program, ensure the firewall allows outgoing TCP communication on port 1433.</span></span>  <span data-ttu-id="447ed-136">More information: [Configure an Azure SQL Database firewall](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-136">More information: [Configure an Azure SQL Database firewall](sql-database-configure-firewall-settings.md)</span></span>
* <span data-ttu-id="447ed-137">If your client program connects to SQL Database while your client runs on an Azure virtual machine (VM), you must open certain port ranges on the VM.</span><span class="sxs-lookup"><span data-stu-id="447ed-137">If your client program connects to SQL Database while your client runs on an Azure virtual machine (VM), you must open certain port ranges on the VM.</span></span> <span data-ttu-id="447ed-138">More information: [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-138">More information: [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span></span>
* <span data-ttu-id="447ed-139">Client connections to Azure SQL Database sometimes bypass the proxy and interact directly with the database.</span><span class="sxs-lookup"><span data-stu-id="447ed-139">Client connections to Azure SQL Database sometimes bypass the proxy and interact directly with the database.</span></span> <span data-ttu-id="447ed-140">Ports other than 1433 become important.</span><span class="sxs-lookup"><span data-stu-id="447ed-140">Ports other than 1433 become important.</span></span> <span data-ttu-id="447ed-141">More information:  [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-141">More information:  [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span></span>

## <a name="data-sharding-with-elastic-scale"></a><span data-ttu-id="447ed-142">Data Sharding with Elastic Scale</span><span class="sxs-lookup"><span data-stu-id="447ed-142">Data Sharding with Elastic Scale</span></span>
<span data-ttu-id="447ed-143">Elastic Scale simplifies the process of scaling out (and in).</span><span class="sxs-lookup"><span data-stu-id="447ed-143">Elastic Scale simplifies the process of scaling out (and in).</span></span> 

* [<span data-ttu-id="447ed-144">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="447ed-144">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="447ed-145">Data dependent routing</span><span class="sxs-lookup"><span data-stu-id="447ed-145">Data dependent routing</span></span>](sql-database-elastic-scale-data-dependent-routing.md)
* [<span data-ttu-id="447ed-146">Get Started with Azure SQL Database Elastic Scale Preview</span><span class="sxs-lookup"><span data-stu-id="447ed-146">Get Started with Azure SQL Database Elastic Scale Preview</span></span>](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a><span data-ttu-id="447ed-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="447ed-147">Next steps</span></span>
<span data-ttu-id="447ed-148">Explore all the [capabilities of SQL Database](sql-database-technical-overview.md)</span><span class="sxs-lookup"><span data-stu-id="447ed-148">Explore all the [capabilities of SQL Database](sql-database-technical-overview.md)</span></span>
