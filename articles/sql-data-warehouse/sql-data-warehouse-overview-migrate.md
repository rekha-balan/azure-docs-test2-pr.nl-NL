---
title: Migrate your solution to SQL Data Warehouse | Microsoft Docs
description: Migration guidance for bringing your solution to Azure SQL Data Warehouse platform.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e5937f8472492cd1dd77c82ed518a665718623a1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660570"
---
# <a name="migrate-your-solution-to-sql-data-warehouse"></a><span data-ttu-id="12a4d-103">Migrate your solution to SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="12a4d-103">Migrate your solution to SQL Data Warehouse</span></span>
<span data-ttu-id="12a4d-104">SQL Data Warehouse is a distributed database system that elastically scales to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="12a4d-104">SQL Data Warehouse is a distributed database system that elastically scales to meet your needs.</span></span> <span data-ttu-id="12a4d-105">To maintain both performance and scale, not all features within SQL Server are implemented inside SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12a4d-105">To maintain both performance and scale, not all features within SQL Server are implemented inside SQL Data Warehouse.</span></span> <span data-ttu-id="12a4d-106">The following migration topics touch on some of the key factors for migrating your solution to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12a4d-106">The following migration topics touch on some of the key factors for migrating your solution to SQL Data Warehouse.</span></span> <span data-ttu-id="12a4d-107">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span><span class="sxs-lookup"><span data-stu-id="12a4d-107">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="12a4d-108">You may therefore find that adapting your existing solution ensures you take full advantage of the distributed platform provided by SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12a4d-108">You may therefore find that adapting your existing solution ensures you take full advantage of the distributed platform provided by SQL Data Warehouse.</span></span>

<span data-ttu-id="12a4d-109">It is also important to remember that SQL Data Warehouse is a platform based in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4d-109">It is also important to remember that SQL Data Warehouse is a platform based in Microsoft Azure.</span></span> <span data-ttu-id="12a4d-110">Therefore part of your migration may well include transferring your data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="12a4d-110">Therefore part of your migration may well include transferring your data to the cloud.</span></span> <span data-ttu-id="12a4d-111">Data transfer is a subject in its own right and should be carefully considered; especially as volumes increase.</span><span class="sxs-lookup"><span data-stu-id="12a4d-111">Data transfer is a subject in its own right and should be carefully considered; especially as volumes increase.</span></span> <span data-ttu-id="12a4d-112">Data transfer and data loading are discrete topics.</span><span class="sxs-lookup"><span data-stu-id="12a4d-112">Data transfer and data loading are discrete topics.</span></span>

## <a name="migration-guidance"></a><span data-ttu-id="12a4d-113">Migration guidance</span><span class="sxs-lookup"><span data-stu-id="12a4d-113">Migration guidance</span></span>
<span data-ttu-id="12a4d-114">Make sure you have read through these articles to ensure you understand some of the product differences and fundamental concepts before embarking on your migration.</span><span class="sxs-lookup"><span data-stu-id="12a4d-114">Make sure you have read through these articles to ensure you understand some of the product differences and fundamental concepts before embarking on your migration.</span></span>

* <span data-ttu-id="12a4d-115">[Migrate your schema][Migrate your schema]</span><span class="sxs-lookup"><span data-stu-id="12a4d-115">[Migrate your schema][Migrate your schema]</span></span>
* <span data-ttu-id="12a4d-116">[Migrate your data][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="12a4d-116">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="12a4d-117">[Migrate your code][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="12a4d-117">[Migrate your code][Migrate your code]</span></span>

## <a name="next-steps"></a><span data-ttu-id="12a4d-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="12a4d-118">Next steps</span></span>
<span data-ttu-id="12a4d-119">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance which they publish through blogs.</span><span class="sxs-lookup"><span data-stu-id="12a4d-119">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance which they publish through blogs.</span></span>  <span data-ttu-id="12a4d-120">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span><span class="sxs-lookup"><span data-stu-id="12a4d-120">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your schema]: sql-data-warehouse-migrate-schema.md
[Migrate your data]: sql-data-warehouse-migrate-data.md
[Migrate your code]: sql-data-warehouse-migrate-code.md


<!--MSDN references-->


<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
