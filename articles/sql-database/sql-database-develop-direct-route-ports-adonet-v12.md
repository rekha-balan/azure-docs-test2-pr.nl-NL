---
title: Ports beyond 1433 for SQL Database | Microsoft Docs
description: Client connections from ADO.NET to Azure SQL Database sometimes bypass the proxy and interact directly with the database. Ports other than 1433 become important.
services: sql-database
documentationcenter: ''
author: MightyPen
manager: jhubbard
editor: ''
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: development
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: e47d8f71fbfe95027e1fbfebb0b7e91ffe653c62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662623"
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="4f295-104">Ports beyond 1433 for ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="4f295-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="4f295-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span><span class="sxs-lookup"><span data-stu-id="4f295-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span>

## <a name="outside-vs-inside"></a><span data-ttu-id="4f295-106">Outside vs inside</span><span class="sxs-lookup"><span data-stu-id="4f295-106">Outside vs inside</span></span>
<span data-ttu-id="4f295-107">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span><span class="sxs-lookup"><span data-stu-id="4f295-107">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="4f295-108">The subsections discuss two common scenarios.</span><span class="sxs-lookup"><span data-stu-id="4f295-108">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="4f295-109">*Outside:* Client runs on your desktop computer</span><span class="sxs-lookup"><span data-stu-id="4f295-109">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="4f295-110">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span><span class="sxs-lookup"><span data-stu-id="4f295-110">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="4f295-111">*Inside:* Client runs on Azure</span><span class="sxs-lookup"><span data-stu-id="4f295-111">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="4f295-112">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="4f295-112">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="4f295-113">After a connection is established, further interactions between the client and database involve no middleware proxy.</span><span class="sxs-lookup"><span data-stu-id="4f295-113">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="4f295-114">The sequence is as follows:</span><span class="sxs-lookup"><span data-stu-id="4f295-114">The sequence is as follows:</span></span>

1. <span data-ttu-id="4f295-115">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span><span class="sxs-lookup"><span data-stu-id="4f295-115">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="4f295-116">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span><span class="sxs-lookup"><span data-stu-id="4f295-116">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="4f295-117">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span><span class="sxs-lookup"><span data-stu-id="4f295-117">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="4f295-118">Queries are sent directly to the database, and results are returned directly to the client.</span><span class="sxs-lookup"><span data-stu-id="4f295-118">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="4f295-119">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4f295-119">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="4f295-120">In particular, ports in the range must be free of any other outbound blockers.</span><span class="sxs-lookup"><span data-stu-id="4f295-120">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="4f295-121">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span><span class="sxs-lookup"><span data-stu-id="4f295-121">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="4f295-122">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span><span class="sxs-lookup"><span data-stu-id="4f295-122">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="4f295-123">Version clarifications</span><span class="sxs-lookup"><span data-stu-id="4f295-123">Version clarifications</span></span>
<span data-ttu-id="4f295-124">This section clarifies the monikers that refer to product versions.</span><span class="sxs-lookup"><span data-stu-id="4f295-124">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="4f295-125">It also lists some pairings of versions between products.</span><span class="sxs-lookup"><span data-stu-id="4f295-125">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="4f295-126">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="4f295-126">ADO.NET</span></span>
* <span data-ttu-id="4f295-127">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span><span class="sxs-lookup"><span data-stu-id="4f295-127">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="4f295-128">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span><span class="sxs-lookup"><span data-stu-id="4f295-128">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="4f295-129">Related links</span><span class="sxs-lookup"><span data-stu-id="4f295-129">Related links</span></span>
* <span data-ttu-id="4f295-130">ADO.NET 4.6 was released on July 20, 2015.</span><span class="sxs-lookup"><span data-stu-id="4f295-130">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="4f295-131">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f295-131">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="4f295-132">ADO.NET 4.5 was released on August 15, 2012.</span><span class="sxs-lookup"><span data-stu-id="4f295-132">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="4f295-133">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f295-133">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="4f295-134">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f295-134">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="4f295-135">TDS protocol version list</span><span class="sxs-lookup"><span data-stu-id="4f295-135">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="4f295-136">SQL Database Development Overview</span><span class="sxs-lookup"><span data-stu-id="4f295-136">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="4f295-137">Azure SQL Database firewall</span><span class="sxs-lookup"><span data-stu-id="4f295-137">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="4f295-138">How to: Configure firewall settings on SQL Database</span><span class="sxs-lookup"><span data-stu-id="4f295-138">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

