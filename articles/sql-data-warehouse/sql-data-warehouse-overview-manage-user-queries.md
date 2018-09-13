---
title: Monitor user queries in Azure SQL Data Warehouse | Microsoft Docs
description: Overview of the considerations, best practices, and tasks for monitoring user queries in Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 54346a8e6f42fc81cd727db03c02f0e935db07d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563465"
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="80f4f-103">Monitor user queries in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="80f4f-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="80f4f-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="80f4f-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="80f4f-105">Category</span><span class="sxs-lookup"><span data-stu-id="80f4f-105">Category</span></span> | <span data-ttu-id="80f4f-106">Task or consideration</span><span class="sxs-lookup"><span data-stu-id="80f4f-106">Task or consideration</span></span> | <span data-ttu-id="80f4f-107">Description</span><span class="sxs-lookup"><span data-stu-id="80f4f-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="80f4f-108">Slow performance</span><span class="sxs-lookup"><span data-stu-id="80f4f-108">Slow performance</span></span> |<span data-ttu-id="80f4f-109">Find a long-running user query</span><span class="sxs-lookup"><span data-stu-id="80f4f-109">Find a long-running user query</span></span> |<span data-ttu-id="80f4f-110">[Find long-running queries][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="80f4f-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="80f4f-111">Concurrency</span><span class="sxs-lookup"><span data-stu-id="80f4f-111">Concurrency</span></span> |<span data-ttu-id="80f4f-112">Assign concurrent resources to user queries</span><span class="sxs-lookup"><span data-stu-id="80f4f-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="80f4f-113">[Concurrency and workload management][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="80f4f-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80f4f-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="80f4f-114">Next steps</span></span>
<span data-ttu-id="80f4f-115">For more management tips, head over to the [Management overview][Management overview].</span><span class="sxs-lookup"><span data-stu-id="80f4f-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
