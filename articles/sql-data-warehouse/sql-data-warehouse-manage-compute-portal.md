---
title: Manage compute power in Azure SQL Data Warehouse (Azure portal) | Microsoft Docs
description: Azure portal tasks to manage compute power. Scale compute resources by adjusting DWUs. Or, pause and resume compute resources to save costs.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: a2df07a6713dd0f35ce657a0ab9d5d20dacb1278
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554703"
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="15dec-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span><span class="sxs-lookup"><span data-stu-id="15dec-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [Overview](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="15dec-111">Scale compute power</span><span class="sxs-lookup"><span data-stu-id="15dec-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="15dec-112">To change compute resources:</span><span class="sxs-lookup"><span data-stu-id="15dec-112">To change compute resources:</span></span>

1. <span data-ttu-id="15dec-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="15dec-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Click Scale][1]
2. <span data-ttu-id="15dec-115">In the Scale blade, move the slider left or right to change the DWU setting.</span><span class="sxs-lookup"><span data-stu-id="15dec-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Move Slider][2]
3. <span data-ttu-id="15dec-117">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="15dec-117">Click **Save**.</span></span> <span data-ttu-id="15dec-118">A confirmation message appears.</span><span class="sxs-lookup"><span data-stu-id="15dec-118">A confirmation message appears.</span></span> <span data-ttu-id="15dec-119">Click **yes** to confirm or **no** to cancel.</span><span class="sxs-lookup"><span data-stu-id="15dec-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Click Save][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="15dec-121">Pause compute</span><span class="sxs-lookup"><span data-stu-id="15dec-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="15dec-122">To pause a database:</span><span class="sxs-lookup"><span data-stu-id="15dec-122">To pause a database:</span></span>

1. <span data-ttu-id="15dec-123">Open the [Azure portal][Azure portal] and open your database.</span><span class="sxs-lookup"><span data-stu-id="15dec-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="15dec-124">Notice that the Status is **Online**.</span><span class="sxs-lookup"><span data-stu-id="15dec-124">Notice that the Status is **Online**.</span></span>

    ![Online status][6]
2. <span data-ttu-id="15dec-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span><span class="sxs-lookup"><span data-stu-id="15dec-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="15dec-127">Click **yes** to confirm or **no** to cancel.</span><span class="sxs-lookup"><span data-stu-id="15dec-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirm pause][7]
3. <span data-ttu-id="15dec-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span><span class="sxs-lookup"><span data-stu-id="15dec-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="15dec-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span><span class="sxs-lookup"><span data-stu-id="15dec-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Pause status][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="15dec-132">Resume compute</span><span class="sxs-lookup"><span data-stu-id="15dec-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="15dec-133">To resume a database:</span><span class="sxs-lookup"><span data-stu-id="15dec-133">To resume a database:</span></span>

1. <span data-ttu-id="15dec-134">Open the [Azure portal][Azure portal] and open your database.</span><span class="sxs-lookup"><span data-stu-id="15dec-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="15dec-135">Notice that the Status is **Paused**.</span><span class="sxs-lookup"><span data-stu-id="15dec-135">Notice that the Status is **Paused**.</span></span>

    ![Pause database][4]
2. <span data-ttu-id="15dec-137">To resume the database click **Start**, and then a confirmation message appears.</span><span class="sxs-lookup"><span data-stu-id="15dec-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="15dec-138">Click **yes** to confirm or **no** to cancel.</span><span class="sxs-lookup"><span data-stu-id="15dec-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirm resume][5]
3. <span data-ttu-id="15dec-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span><span class="sxs-lookup"><span data-stu-id="15dec-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="15dec-141">When the status is **online**, the database is ready.</span><span class="sxs-lookup"><span data-stu-id="15dec-141">When the status is **online**, the database is ready.</span></span>

    ![Online status][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="15dec-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="15dec-143">Next steps</span></span>
<span data-ttu-id="15dec-144">For more information, see [Management overview][Management overview].</span><span class="sxs-lookup"><span data-stu-id="15dec-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/







