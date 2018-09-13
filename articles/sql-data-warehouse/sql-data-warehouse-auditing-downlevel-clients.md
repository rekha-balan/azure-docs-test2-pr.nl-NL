---
title: SQL Data Warehouse downlevel clients support for data auditing | Microsoft Docs
description: Learn about SQL Data Warehouse downlevel clients support for data auditing
services: sql-data-warehouse
documentationcenter: ''
author: ronortloff
manager: jhubbard
editor: ''
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555395"
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="70ec3-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span><span class="sxs-lookup"><span data-stu-id="70ec3-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="70ec3-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span><span class="sxs-lookup"><span data-stu-id="70ec3-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="70ec3-105">Any client which implements TDS 7.4 should also support redirection.</span><span class="sxs-lookup"><span data-stu-id="70ec3-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="70ec3-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span><span class="sxs-lookup"><span data-stu-id="70ec3-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="70ec3-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span><span class="sxs-lookup"><span data-stu-id="70ec3-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="70ec3-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="70ec3-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="70ec3-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="70ec3-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="70ec3-110">A partial list of "Downlevel clients" includes:</span><span class="sxs-lookup"><span data-stu-id="70ec3-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="70ec3-111">.NET 4.0 and below,</span><span class="sxs-lookup"><span data-stu-id="70ec3-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="70ec3-112">ODBC 10.0 and below.</span><span class="sxs-lookup"><span data-stu-id="70ec3-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="70ec3-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span><span class="sxs-lookup"><span data-stu-id="70ec3-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="70ec3-114">Tedious (for Node.JS)</span><span class="sxs-lookup"><span data-stu-id="70ec3-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="70ec3-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span><span class="sxs-lookup"><span data-stu-id="70ec3-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

