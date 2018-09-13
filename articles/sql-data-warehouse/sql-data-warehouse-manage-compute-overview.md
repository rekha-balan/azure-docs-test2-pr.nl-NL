---
title: Manage compute power in Azure SQL Data Warehouse (Overview) | Microsoft Docs
description: Performance scale out capabilities in Azure SQL Data Warehouse. Scale out by adjusting DWUs or pause and resume compute resources to save costs.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: ''
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564025"
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="f5b82-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span><span class="sxs-lookup"><span data-stu-id="f5b82-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [Overview](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="f5b82-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span><span class="sxs-lookup"><span data-stu-id="f5b82-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="f5b82-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span><span class="sxs-lookup"><span data-stu-id="f5b82-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="f5b82-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span><span class="sxs-lookup"><span data-stu-id="f5b82-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="f5b82-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f5b82-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="f5b82-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span><span class="sxs-lookup"><span data-stu-id="f5b82-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="f5b82-115">How compute management operations work in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f5b82-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="f5b82-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="f5b82-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="f5b82-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span><span class="sxs-lookup"><span data-stu-id="f5b82-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="f5b82-118">Beneath this head node are your compute nodes and your storage layer.</span><span class="sxs-lookup"><span data-stu-id="f5b82-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="f5b82-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="f5b82-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="f5b82-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span><span class="sxs-lookup"><span data-stu-id="f5b82-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="f5b82-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span><span class="sxs-lookup"><span data-stu-id="f5b82-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="f5b82-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span><span class="sxs-lookup"><span data-stu-id="f5b82-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="f5b82-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span><span class="sxs-lookup"><span data-stu-id="f5b82-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="f5b82-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span><span class="sxs-lookup"><span data-stu-id="f5b82-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="f5b82-125">DWU</span><span class="sxs-lookup"><span data-stu-id="f5b82-125">DWU</span></span>  | <span data-ttu-id="f5b82-126">\#of compute nodes</span><span class="sxs-lookup"><span data-stu-id="f5b82-126">\#of compute nodes</span></span> | <span data-ttu-id="f5b82-127">\# of distributions per node</span><span class="sxs-lookup"><span data-stu-id="f5b82-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="f5b82-128">100</span><span class="sxs-lookup"><span data-stu-id="f5b82-128">100</span></span>  | <span data-ttu-id="f5b82-129">1</span><span class="sxs-lookup"><span data-stu-id="f5b82-129">1</span></span>                  | <span data-ttu-id="f5b82-130">60</span><span class="sxs-lookup"><span data-stu-id="f5b82-130">60</span></span>                           |
| <span data-ttu-id="f5b82-131">200</span><span class="sxs-lookup"><span data-stu-id="f5b82-131">200</span></span>  | <span data-ttu-id="f5b82-132">2</span><span class="sxs-lookup"><span data-stu-id="f5b82-132">2</span></span>                  | <span data-ttu-id="f5b82-133">30</span><span class="sxs-lookup"><span data-stu-id="f5b82-133">30</span></span>                           |
| <span data-ttu-id="f5b82-134">300</span><span class="sxs-lookup"><span data-stu-id="f5b82-134">300</span></span>  | <span data-ttu-id="f5b82-135">3</span><span class="sxs-lookup"><span data-stu-id="f5b82-135">3</span></span>                  | <span data-ttu-id="f5b82-136">20</span><span class="sxs-lookup"><span data-stu-id="f5b82-136">20</span></span>                           |
| <span data-ttu-id="f5b82-137">400</span><span class="sxs-lookup"><span data-stu-id="f5b82-137">400</span></span>  | <span data-ttu-id="f5b82-138">4</span><span class="sxs-lookup"><span data-stu-id="f5b82-138">4</span></span>                  | <span data-ttu-id="f5b82-139">15</span><span class="sxs-lookup"><span data-stu-id="f5b82-139">15</span></span>                           |
| <span data-ttu-id="f5b82-140">500</span><span class="sxs-lookup"><span data-stu-id="f5b82-140">500</span></span>  | <span data-ttu-id="f5b82-141">5</span><span class="sxs-lookup"><span data-stu-id="f5b82-141">5</span></span>                  | <span data-ttu-id="f5b82-142">12</span><span class="sxs-lookup"><span data-stu-id="f5b82-142">12</span></span>                           |
| <span data-ttu-id="f5b82-143">600</span><span class="sxs-lookup"><span data-stu-id="f5b82-143">600</span></span>  | <span data-ttu-id="f5b82-144">6</span><span class="sxs-lookup"><span data-stu-id="f5b82-144">6</span></span>                  | <span data-ttu-id="f5b82-145">10</span><span class="sxs-lookup"><span data-stu-id="f5b82-145">10</span></span>                           |
| <span data-ttu-id="f5b82-146">1000</span><span class="sxs-lookup"><span data-stu-id="f5b82-146">1000</span></span> | <span data-ttu-id="f5b82-147">10</span><span class="sxs-lookup"><span data-stu-id="f5b82-147">10</span></span>                 | <span data-ttu-id="f5b82-148">6</span><span class="sxs-lookup"><span data-stu-id="f5b82-148">6</span></span>                            |
| <span data-ttu-id="f5b82-149">1200</span><span class="sxs-lookup"><span data-stu-id="f5b82-149">1200</span></span> | <span data-ttu-id="f5b82-150">12</span><span class="sxs-lookup"><span data-stu-id="f5b82-150">12</span></span>                 | <span data-ttu-id="f5b82-151">5</span><span class="sxs-lookup"><span data-stu-id="f5b82-151">5</span></span>                            |
| <span data-ttu-id="f5b82-152">1500</span><span class="sxs-lookup"><span data-stu-id="f5b82-152">1500</span></span> | <span data-ttu-id="f5b82-153">15</span><span class="sxs-lookup"><span data-stu-id="f5b82-153">15</span></span>                 | <span data-ttu-id="f5b82-154">4</span><span class="sxs-lookup"><span data-stu-id="f5b82-154">4</span></span>                            |
| <span data-ttu-id="f5b82-155">2000</span><span class="sxs-lookup"><span data-stu-id="f5b82-155">2000</span></span> | <span data-ttu-id="f5b82-156">20</span><span class="sxs-lookup"><span data-stu-id="f5b82-156">20</span></span>                 | <span data-ttu-id="f5b82-157">3</span><span class="sxs-lookup"><span data-stu-id="f5b82-157">3</span></span>                            |
| <span data-ttu-id="f5b82-158">3000</span><span class="sxs-lookup"><span data-stu-id="f5b82-158">3000</span></span> | <span data-ttu-id="f5b82-159">30</span><span class="sxs-lookup"><span data-stu-id="f5b82-159">30</span></span>                 | <span data-ttu-id="f5b82-160">2</span><span class="sxs-lookup"><span data-stu-id="f5b82-160">2</span></span>                            |
| <span data-ttu-id="f5b82-161">6000</span><span class="sxs-lookup"><span data-stu-id="f5b82-161">6000</span></span> | <span data-ttu-id="f5b82-162">60</span><span class="sxs-lookup"><span data-stu-id="f5b82-162">60</span></span>                 | <span data-ttu-id="f5b82-163">1</span><span class="sxs-lookup"><span data-stu-id="f5b82-163">1</span></span>                            |

<span data-ttu-id="f5b82-164">The three primary functions for managing compute are:</span><span class="sxs-lookup"><span data-stu-id="f5b82-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="f5b82-165">Pause</span><span class="sxs-lookup"><span data-stu-id="f5b82-165">Pause</span></span>
2. <span data-ttu-id="f5b82-166">Resume</span><span class="sxs-lookup"><span data-stu-id="f5b82-166">Resume</span></span>
3. <span data-ttu-id="f5b82-167">Scale</span><span class="sxs-lookup"><span data-stu-id="f5b82-167">Scale</span></span>

<span data-ttu-id="f5b82-168">Each of these operations may take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="f5b82-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="f5b82-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span><span class="sxs-lookup"><span data-stu-id="f5b82-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="f5b82-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span><span class="sxs-lookup"><span data-stu-id="f5b82-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="f5b82-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span><span class="sxs-lookup"><span data-stu-id="f5b82-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  Compute management functionality does not exist across all endpoints.
>
>  

|              | <span data-ttu-id="f5b82-173">Pause/Resume</span><span class="sxs-lookup"><span data-stu-id="f5b82-173">Pause/Resume</span></span> | <span data-ttu-id="f5b82-174">Scale</span><span class="sxs-lookup"><span data-stu-id="f5b82-174">Scale</span></span> | <span data-ttu-id="f5b82-175">Check database state</span><span class="sxs-lookup"><span data-stu-id="f5b82-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="f5b82-176">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f5b82-176">Azure portal</span></span> | <span data-ttu-id="f5b82-177">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-177">Yes</span></span>          | <span data-ttu-id="f5b82-178">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-178">Yes</span></span>   | <span data-ttu-id="f5b82-179">**No**</span><span class="sxs-lookup"><span data-stu-id="f5b82-179">**No**</span></span>               |
| <span data-ttu-id="f5b82-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b82-180">PowerShell</span></span>   | <span data-ttu-id="f5b82-181">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-181">Yes</span></span>          | <span data-ttu-id="f5b82-182">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-182">Yes</span></span>   | <span data-ttu-id="f5b82-183">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-183">Yes</span></span>                  |
| <span data-ttu-id="f5b82-184">REST API</span><span class="sxs-lookup"><span data-stu-id="f5b82-184">REST API</span></span>     | <span data-ttu-id="f5b82-185">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-185">Yes</span></span>          | <span data-ttu-id="f5b82-186">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-186">Yes</span></span>   | <span data-ttu-id="f5b82-187">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-187">Yes</span></span>                  |
| <span data-ttu-id="f5b82-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="f5b82-188">T-SQL</span></span>        | <span data-ttu-id="f5b82-189">**No**</span><span class="sxs-lookup"><span data-stu-id="f5b82-189">**No**</span></span>       | <span data-ttu-id="f5b82-190">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-190">Yes</span></span>   | <span data-ttu-id="f5b82-191">Yes</span><span class="sxs-lookup"><span data-stu-id="f5b82-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="f5b82-192">Scale compute</span><span class="sxs-lookup"><span data-stu-id="f5b82-192">Scale compute</span></span>

<span data-ttu-id="f5b82-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span><span class="sxs-lookup"><span data-stu-id="f5b82-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="f5b82-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span><span class="sxs-lookup"><span data-stu-id="f5b82-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="f5b82-195">How do I scale compute?</span><span class="sxs-lookup"><span data-stu-id="f5b82-195">How do I scale compute?</span></span>
<span data-ttu-id="f5b82-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span><span class="sxs-lookup"><span data-stu-id="f5b82-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="f5b82-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span><span class="sxs-lookup"><span data-stu-id="f5b82-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="f5b82-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span><span class="sxs-lookup"><span data-stu-id="f5b82-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="f5b82-199">To adjust DWUs, you can use any of these individual methods.</span><span class="sxs-lookup"><span data-stu-id="f5b82-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="f5b82-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f5b82-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="f5b82-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f5b82-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="f5b82-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f5b82-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="f5b82-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="f5b82-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="f5b82-204">How many DWUs should I use?</span><span class="sxs-lookup"><span data-stu-id="f5b82-204">How many DWUs should I use?</span></span>

<span data-ttu-id="f5b82-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span><span class="sxs-lookup"><span data-stu-id="f5b82-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="f5b82-206">Since scaling is quick, you can try various performance levels in an hour or less.</span><span class="sxs-lookup"><span data-stu-id="f5b82-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> SQL Data Warehouse is designed to process large amounts of data. To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.

<span data-ttu-id="f5b82-209">Recommendations for finding the best DWU for your workload:</span><span class="sxs-lookup"><span data-stu-id="f5b82-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="f5b82-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span><span class="sxs-lookup"><span data-stu-id="f5b82-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="f5b82-211">A good starting point is DW400 or DW200.</span><span class="sxs-lookup"><span data-stu-id="f5b82-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="f5b82-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span><span class="sxs-lookup"><span data-stu-id="f5b82-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="f5b82-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span><span class="sxs-lookup"><span data-stu-id="f5b82-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="f5b82-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span><span class="sxs-lookup"><span data-stu-id="f5b82-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="f5b82-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span><span class="sxs-lookup"><span data-stu-id="f5b82-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> Query performance only increases with more parallelization if the work can be split between compute nodes. If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement. 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="f5b82-218">When should I scale DWUs?</span><span class="sxs-lookup"><span data-stu-id="f5b82-218">When should I scale DWUs?</span></span>
<span data-ttu-id="f5b82-219">Scaling DWUs alters the following important scenarios:</span><span class="sxs-lookup"><span data-stu-id="f5b82-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="f5b82-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span><span class="sxs-lookup"><span data-stu-id="f5b82-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="f5b82-221">Increasing the number of readers and writers when loading with PolyBase</span><span class="sxs-lookup"><span data-stu-id="f5b82-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="f5b82-222">Maximum number of concurrent queries and concurrency slots</span><span class="sxs-lookup"><span data-stu-id="f5b82-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="f5b82-223">Recommendations for when to scale DWUs:</span><span class="sxs-lookup"><span data-stu-id="f5b82-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="f5b82-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span><span class="sxs-lookup"><span data-stu-id="f5b82-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="f5b82-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span><span class="sxs-lookup"><span data-stu-id="f5b82-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="f5b82-226">Pause compute</span><span class="sxs-lookup"><span data-stu-id="f5b82-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="f5b82-227">To pause a database, use any of these individual methods.</span><span class="sxs-lookup"><span data-stu-id="f5b82-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="f5b82-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f5b82-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="f5b82-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f5b82-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="f5b82-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f5b82-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="f5b82-231">Resume compute</span><span class="sxs-lookup"><span data-stu-id="f5b82-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="f5b82-232">To resume a database, use any of these individual methods.</span><span class="sxs-lookup"><span data-stu-id="f5b82-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="f5b82-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f5b82-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="f5b82-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f5b82-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="f5b82-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f5b82-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="f5b82-236">Check database state</span><span class="sxs-lookup"><span data-stu-id="f5b82-236">Check database state</span></span> 

<span data-ttu-id="f5b82-237">To resume a database, use any of these individual methods.</span><span class="sxs-lookup"><span data-stu-id="f5b82-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="f5b82-238">[Check database state with T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="f5b82-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="f5b82-239">[Check database state with PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f5b82-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="f5b82-240">[Check database state with REST APIs][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f5b82-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="f5b82-241">Permissions</span><span class="sxs-lookup"><span data-stu-id="f5b82-241">Permissions</span></span>

<span data-ttu-id="f5b82-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="f5b82-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="f5b82-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="f5b82-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="f5b82-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5b82-244">Next steps</span></span>
<span data-ttu-id="f5b82-245">Refer to the following articles to help you understand some additional key performance concepts:</span><span class="sxs-lookup"><span data-stu-id="f5b82-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="f5b82-246">[Workload and concurrency management][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="f5b82-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="f5b82-247">[Table design overview][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="f5b82-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="f5b82-248">[Table distribution][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="f5b82-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="f5b82-249">[Table indexing][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="f5b82-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="f5b82-250">[Table partitioning][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="f5b82-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="f5b82-251">[Table statistics][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="f5b82-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="f5b82-252">[Best practices][Best practices]</span><span class="sxs-lookup"><span data-stu-id="f5b82-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
