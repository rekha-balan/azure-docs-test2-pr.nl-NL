---
title: Using transactions in Azure SQL Data Warehouse | Microsoft Docs
description: Tips for implementing transactions in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: ckarst
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: cakarst
ms.reviewer: igorstan
ms.openlocfilehash: 121fa87cb295799fdcd3de5e627fb894efc24c49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819447"
---
# <a name="using-transactions-in-sql-data-warehouse"></a><span data-ttu-id="e3be8-103">Using transactions in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e3be8-103">Using transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="e3be8-104">Tips for implementing transactions in Azure SQL Data Warehouse for developing solutions.</span><span class="sxs-lookup"><span data-stu-id="e3be8-104">Tips for implementing transactions in Azure SQL Data Warehouse for developing solutions.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="e3be8-105">What to expect</span><span class="sxs-lookup"><span data-stu-id="e3be8-105">What to expect</span></span>
<span data-ttu-id="e3be8-106">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span><span class="sxs-lookup"><span data-stu-id="e3be8-106">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="e3be8-107">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3be8-107">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="e3be8-108">This article highlights the differences and lists the others.</span><span class="sxs-lookup"><span data-stu-id="e3be8-108">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="e3be8-109">Transaction isolation levels</span><span class="sxs-lookup"><span data-stu-id="e3be8-109">Transaction isolation levels</span></span>
<span data-ttu-id="e3be8-110">SQL Data Warehouse implements ACID transactions.</span><span class="sxs-lookup"><span data-stu-id="e3be8-110">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="e3be8-111">However, the isolation level of the transactional support is limited to READ UNCOMMITTED; this level cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="e3be8-111">However, the isolation level of the transactional support is limited to READ UNCOMMITTED; this level cannot be changed.</span></span> <span data-ttu-id="e3be8-112">If READ UNCOMMITTED is a concern, you can implement a number of coding methods to prevent dirty reads of data.</span><span class="sxs-lookup"><span data-stu-id="e3be8-112">If READ UNCOMMITTED is a concern, you can implement a number of coding methods to prevent dirty reads of data.</span></span> <span data-ttu-id="e3be8-113">The most popular methods use both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span><span class="sxs-lookup"><span data-stu-id="e3be8-113">The most popular methods use both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="e3be8-114">Views that pre-filter the data are also a popular approach.</span><span class="sxs-lookup"><span data-stu-id="e3be8-114">Views that pre-filter the data are also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="e3be8-115">Transaction size</span><span class="sxs-lookup"><span data-stu-id="e3be8-115">Transaction size</span></span>
<span data-ttu-id="e3be8-116">A single data modification transaction is limited in size.</span><span class="sxs-lookup"><span data-stu-id="e3be8-116">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="e3be8-117">The limit is applied per distribution.</span><span class="sxs-lookup"><span data-stu-id="e3be8-117">The limit is applied per distribution.</span></span> <span data-ttu-id="e3be8-118">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span><span class="sxs-lookup"><span data-stu-id="e3be8-118">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="e3be8-119">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span><span class="sxs-lookup"><span data-stu-id="e3be8-119">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="e3be8-120">For variable length columns, consider taking an average column length rather than using the maximum size.</span><span class="sxs-lookup"><span data-stu-id="e3be8-120">For variable length columns, consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="e3be8-121">In the table below the following assumptions have been made:</span><span class="sxs-lookup"><span data-stu-id="e3be8-121">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="e3be8-122">An even distribution of data has occurred</span><span class="sxs-lookup"><span data-stu-id="e3be8-122">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="e3be8-123">The average row length is 250 bytes</span><span class="sxs-lookup"><span data-stu-id="e3be8-123">The average row length is 250 bytes</span></span>

| [<span data-ttu-id="e3be8-124">DWU</span><span class="sxs-lookup"><span data-stu-id="e3be8-124">DWU</span></span>](sql-data-warehouse-overview-what-is.md) | <span data-ttu-id="e3be8-125">Cap per distribution (GiB)</span><span class="sxs-lookup"><span data-stu-id="e3be8-125">Cap per distribution (GiB)</span></span> | <span data-ttu-id="e3be8-126">Number of Distributions</span><span class="sxs-lookup"><span data-stu-id="e3be8-126">Number of Distributions</span></span> | <span data-ttu-id="e3be8-127">MAX transaction size (GiB)</span><span class="sxs-lookup"><span data-stu-id="e3be8-127">MAX transaction size (GiB)</span></span> | <span data-ttu-id="e3be8-128"># Rows per distribution</span><span class="sxs-lookup"><span data-stu-id="e3be8-128"># Rows per distribution</span></span> | <span data-ttu-id="e3be8-129">Max Rows per transaction</span><span class="sxs-lookup"><span data-stu-id="e3be8-129">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e3be8-130">DW100</span><span class="sxs-lookup"><span data-stu-id="e3be8-130">DW100</span></span> |<span data-ttu-id="e3be8-131">1</span><span class="sxs-lookup"><span data-stu-id="e3be8-131">1</span></span> |<span data-ttu-id="e3be8-132">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-132">60</span></span> |<span data-ttu-id="e3be8-133">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-133">60</span></span> |<span data-ttu-id="e3be8-134">4,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-134">4,000,000</span></span> |<span data-ttu-id="e3be8-135">240,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-135">240,000,000</span></span> |
| <span data-ttu-id="e3be8-136">DW200</span><span class="sxs-lookup"><span data-stu-id="e3be8-136">DW200</span></span> |<span data-ttu-id="e3be8-137">1.5</span><span class="sxs-lookup"><span data-stu-id="e3be8-137">1.5</span></span> |<span data-ttu-id="e3be8-138">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-138">60</span></span> |<span data-ttu-id="e3be8-139">90</span><span class="sxs-lookup"><span data-stu-id="e3be8-139">90</span></span> |<span data-ttu-id="e3be8-140">6,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-140">6,000,000</span></span> |<span data-ttu-id="e3be8-141">360,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-141">360,000,000</span></span> |
| <span data-ttu-id="e3be8-142">DW300</span><span class="sxs-lookup"><span data-stu-id="e3be8-142">DW300</span></span> |<span data-ttu-id="e3be8-143">2.25</span><span class="sxs-lookup"><span data-stu-id="e3be8-143">2.25</span></span> |<span data-ttu-id="e3be8-144">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-144">60</span></span> |<span data-ttu-id="e3be8-145">135</span><span class="sxs-lookup"><span data-stu-id="e3be8-145">135</span></span> |<span data-ttu-id="e3be8-146">9,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-146">9,000,000</span></span> |<span data-ttu-id="e3be8-147">540,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-147">540,000,000</span></span> |
| <span data-ttu-id="e3be8-148">DW400</span><span class="sxs-lookup"><span data-stu-id="e3be8-148">DW400</span></span> |<span data-ttu-id="e3be8-149">3</span><span class="sxs-lookup"><span data-stu-id="e3be8-149">3</span></span> |<span data-ttu-id="e3be8-150">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-150">60</span></span> |<span data-ttu-id="e3be8-151">180</span><span class="sxs-lookup"><span data-stu-id="e3be8-151">180</span></span> |<span data-ttu-id="e3be8-152">12,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-152">12,000,000</span></span> |<span data-ttu-id="e3be8-153">720,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-153">720,000,000</span></span> |
| <span data-ttu-id="e3be8-154">DW500</span><span class="sxs-lookup"><span data-stu-id="e3be8-154">DW500</span></span> |<span data-ttu-id="e3be8-155">3.75</span><span class="sxs-lookup"><span data-stu-id="e3be8-155">3.75</span></span> |<span data-ttu-id="e3be8-156">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-156">60</span></span> |<span data-ttu-id="e3be8-157">225</span><span class="sxs-lookup"><span data-stu-id="e3be8-157">225</span></span> |<span data-ttu-id="e3be8-158">15,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-158">15,000,000</span></span> |<span data-ttu-id="e3be8-159">900,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-159">900,000,000</span></span> |
| <span data-ttu-id="e3be8-160">DW600</span><span class="sxs-lookup"><span data-stu-id="e3be8-160">DW600</span></span> |<span data-ttu-id="e3be8-161">4.5</span><span class="sxs-lookup"><span data-stu-id="e3be8-161">4.5</span></span> |<span data-ttu-id="e3be8-162">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-162">60</span></span> |<span data-ttu-id="e3be8-163">270</span><span class="sxs-lookup"><span data-stu-id="e3be8-163">270</span></span> |<span data-ttu-id="e3be8-164">18,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-164">18,000,000</span></span> |<span data-ttu-id="e3be8-165">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-165">1,080,000,000</span></span> |
| <span data-ttu-id="e3be8-166">DW1000</span><span class="sxs-lookup"><span data-stu-id="e3be8-166">DW1000</span></span> |<span data-ttu-id="e3be8-167">7.5</span><span class="sxs-lookup"><span data-stu-id="e3be8-167">7.5</span></span> |<span data-ttu-id="e3be8-168">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-168">60</span></span> |<span data-ttu-id="e3be8-169">450</span><span class="sxs-lookup"><span data-stu-id="e3be8-169">450</span></span> |<span data-ttu-id="e3be8-170">30,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-170">30,000,000</span></span> |<span data-ttu-id="e3be8-171">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-171">1,800,000,000</span></span> |
| <span data-ttu-id="e3be8-172">DW1200</span><span class="sxs-lookup"><span data-stu-id="e3be8-172">DW1200</span></span> |<span data-ttu-id="e3be8-173">9</span><span class="sxs-lookup"><span data-stu-id="e3be8-173">9</span></span> |<span data-ttu-id="e3be8-174">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-174">60</span></span> |<span data-ttu-id="e3be8-175">540</span><span class="sxs-lookup"><span data-stu-id="e3be8-175">540</span></span> |<span data-ttu-id="e3be8-176">36,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-176">36,000,000</span></span> |<span data-ttu-id="e3be8-177">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-177">2,160,000,000</span></span> |
| <span data-ttu-id="e3be8-178">DW1500</span><span class="sxs-lookup"><span data-stu-id="e3be8-178">DW1500</span></span> |<span data-ttu-id="e3be8-179">11.25</span><span class="sxs-lookup"><span data-stu-id="e3be8-179">11.25</span></span> |<span data-ttu-id="e3be8-180">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-180">60</span></span> |<span data-ttu-id="e3be8-181">675</span><span class="sxs-lookup"><span data-stu-id="e3be8-181">675</span></span> |<span data-ttu-id="e3be8-182">45,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-182">45,000,000</span></span> |<span data-ttu-id="e3be8-183">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-183">2,700,000,000</span></span> |
| <span data-ttu-id="e3be8-184">DW2000</span><span class="sxs-lookup"><span data-stu-id="e3be8-184">DW2000</span></span> |<span data-ttu-id="e3be8-185">15</span><span class="sxs-lookup"><span data-stu-id="e3be8-185">15</span></span> |<span data-ttu-id="e3be8-186">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-186">60</span></span> |<span data-ttu-id="e3be8-187">900</span><span class="sxs-lookup"><span data-stu-id="e3be8-187">900</span></span> |<span data-ttu-id="e3be8-188">60,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-188">60,000,000</span></span> |<span data-ttu-id="e3be8-189">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-189">3,600,000,000</span></span> |
| <span data-ttu-id="e3be8-190">DW3000</span><span class="sxs-lookup"><span data-stu-id="e3be8-190">DW3000</span></span> |<span data-ttu-id="e3be8-191">22.5</span><span class="sxs-lookup"><span data-stu-id="e3be8-191">22.5</span></span> |<span data-ttu-id="e3be8-192">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-192">60</span></span> |<span data-ttu-id="e3be8-193">1,350</span><span class="sxs-lookup"><span data-stu-id="e3be8-193">1,350</span></span> |<span data-ttu-id="e3be8-194">90,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-194">90,000,000</span></span> |<span data-ttu-id="e3be8-195">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-195">5,400,000,000</span></span> |
| <span data-ttu-id="e3be8-196">DW6000</span><span class="sxs-lookup"><span data-stu-id="e3be8-196">DW6000</span></span> |<span data-ttu-id="e3be8-197">45</span><span class="sxs-lookup"><span data-stu-id="e3be8-197">45</span></span> |<span data-ttu-id="e3be8-198">60</span><span class="sxs-lookup"><span data-stu-id="e3be8-198">60</span></span> |<span data-ttu-id="e3be8-199">2,700</span><span class="sxs-lookup"><span data-stu-id="e3be8-199">2,700</span></span> |<span data-ttu-id="e3be8-200">180,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-200">180,000,000</span></span> |<span data-ttu-id="e3be8-201">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-201">10,800,000,000</span></span> |

<span data-ttu-id="e3be8-202">The transaction size limit is applied per transaction or operation.</span><span class="sxs-lookup"><span data-stu-id="e3be8-202">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="e3be8-203">It is not applied across all concurrent transactions.</span><span class="sxs-lookup"><span data-stu-id="e3be8-203">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="e3be8-204">Therefore each transaction is permitted to write this amount of data to the log.</span><span class="sxs-lookup"><span data-stu-id="e3be8-204">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="e3be8-205">To optimize and minimize the amount of data written to the log, please refer to the [Transactions best practices](sql-data-warehouse-develop-best-practices-transactions.md) article.</span><span class="sxs-lookup"><span data-stu-id="e3be8-205">To optimize and minimize the amount of data written to the log, please refer to the [Transactions best practices](sql-data-warehouse-develop-best-practices-transactions.md) article.</span></span>

> [!WARNING]
> <span data-ttu-id="e3be8-206">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span><span class="sxs-lookup"><span data-stu-id="e3be8-206">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="e3be8-207">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span><span class="sxs-lookup"><span data-stu-id="e3be8-207">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="e3be8-208">Transaction state</span><span class="sxs-lookup"><span data-stu-id="e3be8-208">Transaction state</span></span>
<span data-ttu-id="e3be8-209">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span><span class="sxs-lookup"><span data-stu-id="e3be8-209">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="e3be8-210">This value means the transaction has failed and is marked for rollback only.</span><span class="sxs-lookup"><span data-stu-id="e3be8-210">This value means the transaction has failed and is marked for rollback only.</span></span>

> [!NOTE]
> <span data-ttu-id="e3be8-211">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3be8-211">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="e3be8-212">SQL Server uses the value -1 to represent an uncommittable transaction.</span><span class="sxs-lookup"><span data-stu-id="e3be8-212">SQL Server uses the value -1 to represent an uncommittable transaction.</span></span> <span data-ttu-id="e3be8-213">SQL Server can tolerate some errors inside a transaction without it having to be marked as uncommittable.</span><span class="sxs-lookup"><span data-stu-id="e3be8-213">SQL Server can tolerate some errors inside a transaction without it having to be marked as uncommittable.</span></span> <span data-ttu-id="e3be8-214">For example `SELECT 1/0` would cause an error but not force a transaction into an uncommittable state.</span><span class="sxs-lookup"><span data-stu-id="e3be8-214">For example `SELECT 1/0` would cause an error but not force a transaction into an uncommittable state.</span></span> <span data-ttu-id="e3be8-215">SQL Server also permits reads in the uncommittable transaction.</span><span class="sxs-lookup"><span data-stu-id="e3be8-215">SQL Server also permits reads in the uncommittable transaction.</span></span> <span data-ttu-id="e3be8-216">However, SQL Data Warehouse does not let you do this.</span><span class="sxs-lookup"><span data-stu-id="e3be8-216">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="e3be8-217">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span><span class="sxs-lookup"><span data-stu-id="e3be8-217">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="e3be8-218">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span><span class="sxs-lookup"><span data-stu-id="e3be8-218">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="e3be8-219">For example, in SQL Server you might see a transaction that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="e3be8-219">For example, in SQL Server you might see a transaction that looks like the following:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="e3be8-220">The preceding code gives the following error message:</span><span class="sxs-lookup"><span data-stu-id="e3be8-220">The preceding code gives the following error message:</span></span>

<span data-ttu-id="e3be8-221">Msg 111233, Level 16, State 1, Line 1 111233; The current transaction has aborted, and any pending changes have been rolled back.</span><span class="sxs-lookup"><span data-stu-id="e3be8-221">Msg 111233, Level 16, State 1, Line 1 111233; The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="e3be8-222">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML, or SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="e3be8-222">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML, or SELECT statement.</span></span>

<span data-ttu-id="e3be8-223">You won't get the output of the ERROR_\* functions.</span><span class="sxs-lookup"><span data-stu-id="e3be8-223">You won't get the output of the ERROR_\* functions.</span></span>

<span data-ttu-id="e3be8-224">In SQL Data Warehouse the code needs to be slightly altered:</span><span class="sxs-lookup"><span data-stu-id="e3be8-224">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="e3be8-225">The expected behavior is now observed.</span><span class="sxs-lookup"><span data-stu-id="e3be8-225">The expected behavior is now observed.</span></span> <span data-ttu-id="e3be8-226">The error in the transaction is managed and the ERROR_\* functions provide values as expected.</span><span class="sxs-lookup"><span data-stu-id="e3be8-226">The error in the transaction is managed and the ERROR_\* functions provide values as expected.</span></span>

<span data-ttu-id="e3be8-227">All that has changed is that the ROLLBACK of the transaction had to happen before the read of the error information in the CATCH block.</span><span class="sxs-lookup"><span data-stu-id="e3be8-227">All that has changed is that the ROLLBACK of the transaction had to happen before the read of the error information in the CATCH block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="e3be8-228">Error_Line() function</span><span class="sxs-lookup"><span data-stu-id="e3be8-228">Error_Line() function</span></span>
<span data-ttu-id="e3be8-229">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span><span class="sxs-lookup"><span data-stu-id="e3be8-229">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="e3be8-230">If you have this in your code, you need to remove it to be compliant with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e3be8-230">If you have this in your code, you need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="e3be8-231">Use query labels in your code instead to implement equivalent functionality.</span><span class="sxs-lookup"><span data-stu-id="e3be8-231">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="e3be8-232">For more details, see the [LABEL](sql-data-warehouse-develop-label.md) article.</span><span class="sxs-lookup"><span data-stu-id="e3be8-232">For more details, see the [LABEL](sql-data-warehouse-develop-label.md) article.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="e3be8-233">Using THROW and RAISERROR</span><span class="sxs-lookup"><span data-stu-id="e3be8-233">Using THROW and RAISERROR</span></span>
<span data-ttu-id="e3be8-234">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span><span class="sxs-lookup"><span data-stu-id="e3be8-234">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="e3be8-235">There are a few differences that are worth paying attention to however.</span><span class="sxs-lookup"><span data-stu-id="e3be8-235">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="e3be8-236">User-defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span><span class="sxs-lookup"><span data-stu-id="e3be8-236">User-defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="e3be8-237">RAISERROR error messages are fixed at 50,000</span><span class="sxs-lookup"><span data-stu-id="e3be8-237">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="e3be8-238">Use of sys.messages is not supported</span><span class="sxs-lookup"><span data-stu-id="e3be8-238">Use of sys.messages is not supported</span></span>

## <a name="limitations"></a><span data-ttu-id="e3be8-239">Limitations</span><span class="sxs-lookup"><span data-stu-id="e3be8-239">Limitations</span></span>
<span data-ttu-id="e3be8-240">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span><span class="sxs-lookup"><span data-stu-id="e3be8-240">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="e3be8-241">They are as follows:</span><span class="sxs-lookup"><span data-stu-id="e3be8-241">They are as follows:</span></span>

* <span data-ttu-id="e3be8-242">No distributed transactions</span><span class="sxs-lookup"><span data-stu-id="e3be8-242">No distributed transactions</span></span>
* <span data-ttu-id="e3be8-243">No nested transactions permitted</span><span class="sxs-lookup"><span data-stu-id="e3be8-243">No nested transactions permitted</span></span>
* <span data-ttu-id="e3be8-244">No save points allowed</span><span class="sxs-lookup"><span data-stu-id="e3be8-244">No save points allowed</span></span>
* <span data-ttu-id="e3be8-245">No named transactions</span><span class="sxs-lookup"><span data-stu-id="e3be8-245">No named transactions</span></span>
* <span data-ttu-id="e3be8-246">No marked transactions</span><span class="sxs-lookup"><span data-stu-id="e3be8-246">No marked transactions</span></span>
* <span data-ttu-id="e3be8-247">No support for DDL such as CREATE TABLE inside a user-defined transaction</span><span class="sxs-lookup"><span data-stu-id="e3be8-247">No support for DDL such as CREATE TABLE inside a user-defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3be8-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3be8-248">Next steps</span></span>
<span data-ttu-id="e3be8-249">To learn more about optimizing transactions, see [Transactions best practices](sql-data-warehouse-develop-best-practices-transactions.md).</span><span class="sxs-lookup"><span data-stu-id="e3be8-249">To learn more about optimizing transactions, see [Transactions best practices](sql-data-warehouse-develop-best-practices-transactions.md).</span></span> <span data-ttu-id="e3be8-250">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices](sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="e3be8-250">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices](sql-data-warehouse-best-practices.md).</span></span>

