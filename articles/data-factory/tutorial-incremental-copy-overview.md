---
title: Incrementally copy data by using Azure Data Factory | Microsoft Docs
description: These tutorials show you how to incrementally copy data from a source data store to a destination data store. The first one copies data from one table.
services: data-factory
documentationcenter: ''
author: dearandyxu
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: yexu
ms.openlocfilehash: 5151ef834a35f410d8caf9904cd3c7567a8958ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864964"
---
# <a name="incrementally-load-data-from-a-source-data-store-to-a-destination-data-store"></a><span data-ttu-id="85cd5-104">Incrementally load data from a source data store to a destination data store</span><span class="sxs-lookup"><span data-stu-id="85cd5-104">Incrementally load data from a source data store to a destination data store</span></span>

<span data-ttu-id="85cd5-105">In a data integration solution, incrementally (or delta) loading data after an initial full data load is a widely used scenario.</span><span class="sxs-lookup"><span data-stu-id="85cd5-105">In a data integration solution, incrementally (or delta) loading data after an initial full data load is a widely used scenario.</span></span> <span data-ttu-id="85cd5-106">The tutorials in this section show you different ways of loading data incrementally by using Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="85cd5-106">The tutorials in this section show you different ways of loading data incrementally by using Azure Data Factory.</span></span>

## <a name="delta-data-loading-by-using-a-watermark"></a><span data-ttu-id="85cd5-107">Delta data loading by using a watermark</span><span class="sxs-lookup"><span data-stu-id="85cd5-107">Delta data loading by using a watermark</span></span>
<span data-ttu-id="85cd5-108">In this case, you define a watermark in your source database.</span><span class="sxs-lookup"><span data-stu-id="85cd5-108">In this case, you define a watermark in your source database.</span></span> <span data-ttu-id="85cd5-109">A watermark is a column that has the last updated time stamp or an incrementing key.</span><span class="sxs-lookup"><span data-stu-id="85cd5-109">A watermark is a column that has the last updated time stamp or an incrementing key.</span></span> <span data-ttu-id="85cd5-110">The delta loading solution loads the changed data between an old watermark and a new watermark.</span><span class="sxs-lookup"><span data-stu-id="85cd5-110">The delta loading solution loads the changed data between an old watermark and a new watermark.</span></span> <span data-ttu-id="85cd5-111">The workflow for this approach is depicted in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="85cd5-111">The workflow for this approach is depicted in the following diagram:</span></span> 

![Workflow for using a watermark](media/tutorial-incremental-copy-overview/workflow-using-watermark.png)

<span data-ttu-id="85cd5-113">For step-by-step instructions, see the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="85cd5-113">For step-by-step instructions, see the following tutorials:</span></span> 

- [<span data-ttu-id="85cd5-114">Incrementally copy data from one table in Azure SQL Database to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="85cd5-114">Incrementally copy data from one table in Azure SQL Database to Azure Blob storage</span></span>](tutorial-incremental-copy-powershell.md)
- [<span data-ttu-id="85cd5-115">Incrementally copy data from multiple tables in on-premises SQL Server to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="85cd5-115">Incrementally copy data from multiple tables in on-premises SQL Server to Azure SQL Database</span></span>](tutorial-incremental-copy-multiple-tables-powershell.md)

## <a name="delta-data-loading-by-using-the-change-tracking-technology"></a><span data-ttu-id="85cd5-116">Delta data loading by using the Change Tracking technology</span><span class="sxs-lookup"><span data-stu-id="85cd5-116">Delta data loading by using the Change Tracking technology</span></span>
<span data-ttu-id="85cd5-117">Change Tracking technology is a lightweight solution in SQL Server and Azure SQL Database that provides an efficient change tracking mechanism for applications.</span><span class="sxs-lookup"><span data-stu-id="85cd5-117">Change Tracking technology is a lightweight solution in SQL Server and Azure SQL Database that provides an efficient change tracking mechanism for applications.</span></span> <span data-ttu-id="85cd5-118">It enables an application to easily identify data that was inserted, updated, or deleted.</span><span class="sxs-lookup"><span data-stu-id="85cd5-118">It enables an application to easily identify data that was inserted, updated, or deleted.</span></span> 

<span data-ttu-id="85cd5-119">The workflow for this approach is depicted in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="85cd5-119">The workflow for this approach is depicted in the following diagram:</span></span>

![Workflow for using Change Tracking](media/tutorial-incremental-copy-overview/workflow-using-change-tracking.png)

<span data-ttu-id="85cd5-121">For step-by-step instructions, see the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="85cd5-121">For step-by-step instructions, see the following tutorial:</span></span> <br/>
[<span data-ttu-id="85cd5-122">Incrementally copy data from Azure SQL Database to Azure Blob storage by using Change Tracking technology</span><span class="sxs-lookup"><span data-stu-id="85cd5-122">Incrementally copy data from Azure SQL Database to Azure Blob storage by using Change Tracking technology</span></span>](tutorial-incremental-copy-change-tracking-feature-powershell.md)

## <a name="next-steps"></a><span data-ttu-id="85cd5-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="85cd5-123">Next steps</span></span>
<span data-ttu-id="85cd5-124">Advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="85cd5-124">Advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="85cd5-125">Incrementally copy data from one table in Azure SQL Database to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="85cd5-125">Incrementally copy data from one table in Azure SQL Database to Azure Blob storage</span></span>](tutorial-incremental-copy-powershell.md)
