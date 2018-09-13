---
title: Transactions in SQL Data Warehouse | Microsoft Docs
description: Tips for implementing transactions in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556312"
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="1ccc9-103">Transactions in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1ccc9-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="1ccc9-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="1ccc9-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="1ccc9-106">This article highlights the differences and lists the others.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="1ccc9-107">Transaction isolation levels</span><span class="sxs-lookup"><span data-stu-id="1ccc9-107">Transaction isolation levels</span></span>
<span data-ttu-id="1ccc9-108">SQL Data Warehouse implements ACID transactions.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="1ccc9-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="1ccc9-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="1ccc9-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="1ccc9-112">Views that pre-filter the data is also a popular approach.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="1ccc9-113">Transaction size</span><span class="sxs-lookup"><span data-stu-id="1ccc9-113">Transaction size</span></span>
<span data-ttu-id="1ccc9-114">A single data modification transaction is limited in size.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="1ccc9-115">The limit today is applied "per distribution".</span><span class="sxs-lookup"><span data-stu-id="1ccc9-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="1ccc9-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="1ccc9-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="1ccc9-118">For variable length columns consider taking an average column length rather than using the maximum size.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="1ccc9-119">In the table below the following assumptions have been made:</span><span class="sxs-lookup"><span data-stu-id="1ccc9-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="1ccc9-120">An even distribution of data has occurred</span><span class="sxs-lookup"><span data-stu-id="1ccc9-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="1ccc9-121">The average row length is 250 bytes</span><span class="sxs-lookup"><span data-stu-id="1ccc9-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="1ccc9-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="1ccc9-122">[DWU][DWU]</span></span> | <span data-ttu-id="1ccc9-123">Cap per distribution (GiB)</span><span class="sxs-lookup"><span data-stu-id="1ccc9-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="1ccc9-124">Number of Distributions</span><span class="sxs-lookup"><span data-stu-id="1ccc9-124">Number of Distributions</span></span> | <span data-ttu-id="1ccc9-125">MAX transaction size (GiB)</span><span class="sxs-lookup"><span data-stu-id="1ccc9-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="1ccc9-126"># Rows per distribution</span><span class="sxs-lookup"><span data-stu-id="1ccc9-126"># Rows per distribution</span></span> | <span data-ttu-id="1ccc9-127">Max Rows per transaction</span><span class="sxs-lookup"><span data-stu-id="1ccc9-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1ccc9-128">DW100</span><span class="sxs-lookup"><span data-stu-id="1ccc9-128">DW100</span></span> |<span data-ttu-id="1ccc9-129">1</span><span class="sxs-lookup"><span data-stu-id="1ccc9-129">1</span></span> |<span data-ttu-id="1ccc9-130">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-130">60</span></span> |<span data-ttu-id="1ccc9-131">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-131">60</span></span> |<span data-ttu-id="1ccc9-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-132">4,000,000</span></span> |<span data-ttu-id="1ccc9-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-133">240,000,000</span></span> |
| <span data-ttu-id="1ccc9-134">DW200</span><span class="sxs-lookup"><span data-stu-id="1ccc9-134">DW200</span></span> |<span data-ttu-id="1ccc9-135">1.5</span><span class="sxs-lookup"><span data-stu-id="1ccc9-135">1.5</span></span> |<span data-ttu-id="1ccc9-136">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-136">60</span></span> |<span data-ttu-id="1ccc9-137">90</span><span class="sxs-lookup"><span data-stu-id="1ccc9-137">90</span></span> |<span data-ttu-id="1ccc9-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-138">6,000,000</span></span> |<span data-ttu-id="1ccc9-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-139">360,000,000</span></span> |
| <span data-ttu-id="1ccc9-140">DW300</span><span class="sxs-lookup"><span data-stu-id="1ccc9-140">DW300</span></span> |<span data-ttu-id="1ccc9-141">2.25</span><span class="sxs-lookup"><span data-stu-id="1ccc9-141">2.25</span></span> |<span data-ttu-id="1ccc9-142">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-142">60</span></span> |<span data-ttu-id="1ccc9-143">135</span><span class="sxs-lookup"><span data-stu-id="1ccc9-143">135</span></span> |<span data-ttu-id="1ccc9-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-144">9,000,000</span></span> |<span data-ttu-id="1ccc9-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-145">540,000,000</span></span> |
| <span data-ttu-id="1ccc9-146">DW400</span><span class="sxs-lookup"><span data-stu-id="1ccc9-146">DW400</span></span> |<span data-ttu-id="1ccc9-147">3</span><span class="sxs-lookup"><span data-stu-id="1ccc9-147">3</span></span> |<span data-ttu-id="1ccc9-148">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-148">60</span></span> |<span data-ttu-id="1ccc9-149">180</span><span class="sxs-lookup"><span data-stu-id="1ccc9-149">180</span></span> |<span data-ttu-id="1ccc9-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-150">12,000,000</span></span> |<span data-ttu-id="1ccc9-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-151">720,000,000</span></span> |
| <span data-ttu-id="1ccc9-152">DW500</span><span class="sxs-lookup"><span data-stu-id="1ccc9-152">DW500</span></span> |<span data-ttu-id="1ccc9-153">3.75</span><span class="sxs-lookup"><span data-stu-id="1ccc9-153">3.75</span></span> |<span data-ttu-id="1ccc9-154">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-154">60</span></span> |<span data-ttu-id="1ccc9-155">225</span><span class="sxs-lookup"><span data-stu-id="1ccc9-155">225</span></span> |<span data-ttu-id="1ccc9-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-156">15,000,000</span></span> |<span data-ttu-id="1ccc9-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-157">900,000,000</span></span> |
| <span data-ttu-id="1ccc9-158">DW600</span><span class="sxs-lookup"><span data-stu-id="1ccc9-158">DW600</span></span> |<span data-ttu-id="1ccc9-159">4.5</span><span class="sxs-lookup"><span data-stu-id="1ccc9-159">4.5</span></span> |<span data-ttu-id="1ccc9-160">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-160">60</span></span> |<span data-ttu-id="1ccc9-161">270</span><span class="sxs-lookup"><span data-stu-id="1ccc9-161">270</span></span> |<span data-ttu-id="1ccc9-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-162">18,000,000</span></span> |<span data-ttu-id="1ccc9-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-163">1,080,000,000</span></span> |
| <span data-ttu-id="1ccc9-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-164">DW1000</span></span> |<span data-ttu-id="1ccc9-165">7.5</span><span class="sxs-lookup"><span data-stu-id="1ccc9-165">7.5</span></span> |<span data-ttu-id="1ccc9-166">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-166">60</span></span> |<span data-ttu-id="1ccc9-167">450</span><span class="sxs-lookup"><span data-stu-id="1ccc9-167">450</span></span> |<span data-ttu-id="1ccc9-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-168">30,000,000</span></span> |<span data-ttu-id="1ccc9-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-169">1,800,000,000</span></span> |
| <span data-ttu-id="1ccc9-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="1ccc9-170">DW1200</span></span> |<span data-ttu-id="1ccc9-171">9</span><span class="sxs-lookup"><span data-stu-id="1ccc9-171">9</span></span> |<span data-ttu-id="1ccc9-172">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-172">60</span></span> |<span data-ttu-id="1ccc9-173">540</span><span class="sxs-lookup"><span data-stu-id="1ccc9-173">540</span></span> |<span data-ttu-id="1ccc9-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-174">36,000,000</span></span> |<span data-ttu-id="1ccc9-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-175">2,160,000,000</span></span> |
| <span data-ttu-id="1ccc9-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="1ccc9-176">DW1500</span></span> |<span data-ttu-id="1ccc9-177">11.25</span><span class="sxs-lookup"><span data-stu-id="1ccc9-177">11.25</span></span> |<span data-ttu-id="1ccc9-178">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-178">60</span></span> |<span data-ttu-id="1ccc9-179">675</span><span class="sxs-lookup"><span data-stu-id="1ccc9-179">675</span></span> |<span data-ttu-id="1ccc9-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-180">45,000,000</span></span> |<span data-ttu-id="1ccc9-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-181">2,700,000,000</span></span> |
| <span data-ttu-id="1ccc9-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-182">DW2000</span></span> |<span data-ttu-id="1ccc9-183">15</span><span class="sxs-lookup"><span data-stu-id="1ccc9-183">15</span></span> |<span data-ttu-id="1ccc9-184">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-184">60</span></span> |<span data-ttu-id="1ccc9-185">900</span><span class="sxs-lookup"><span data-stu-id="1ccc9-185">900</span></span> |<span data-ttu-id="1ccc9-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-186">60,000,000</span></span> |<span data-ttu-id="1ccc9-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-187">3,600,000,000</span></span> |
| <span data-ttu-id="1ccc9-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-188">DW3000</span></span> |<span data-ttu-id="1ccc9-189">22.5</span><span class="sxs-lookup"><span data-stu-id="1ccc9-189">22.5</span></span> |<span data-ttu-id="1ccc9-190">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-190">60</span></span> |<span data-ttu-id="1ccc9-191">1,350</span><span class="sxs-lookup"><span data-stu-id="1ccc9-191">1,350</span></span> |<span data-ttu-id="1ccc9-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-192">90,000,000</span></span> |<span data-ttu-id="1ccc9-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-193">5,400,000,000</span></span> |
| <span data-ttu-id="1ccc9-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-194">DW6000</span></span> |<span data-ttu-id="1ccc9-195">45</span><span class="sxs-lookup"><span data-stu-id="1ccc9-195">45</span></span> |<span data-ttu-id="1ccc9-196">60</span><span class="sxs-lookup"><span data-stu-id="1ccc9-196">60</span></span> |<span data-ttu-id="1ccc9-197">2,700</span><span class="sxs-lookup"><span data-stu-id="1ccc9-197">2,700</span></span> |<span data-ttu-id="1ccc9-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-198">180,000,000</span></span> |<span data-ttu-id="1ccc9-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-199">10,800,000,000</span></span> |

<span data-ttu-id="1ccc9-200">The transaction size limit is applied per transaction or operation.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="1ccc9-201">It is not applied across all concurrent transactions.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="1ccc9-202">Therefore each transaction is permitted to write this amount of data to the log.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="1ccc9-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="1ccc9-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="1ccc9-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="1ccc9-206">Transaction state</span><span class="sxs-lookup"><span data-stu-id="1ccc9-206">Transaction state</span></span>
<span data-ttu-id="1ccc9-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="1ccc9-208">This means that the transaction has failed and is marked for rollback only</span><span class="sxs-lookup"><span data-stu-id="1ccc9-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="1ccc9-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="1ccc9-210">SQL Server uses the value -1 to represent an un-committable transaction.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="1ccc9-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="1ccc9-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="1ccc9-213">SQL Server also permits reads in the un-committable transaction.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="1ccc9-214">However, SQL Data Warehouse does not let you do this.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="1ccc9-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="1ccc9-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="1ccc9-217">For example, in SQL Server you might see a transaction that looks like this:</span><span class="sxs-lookup"><span data-stu-id="1ccc9-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="1ccc9-218">If you leave your code as it is above then you will get the following error message:</span><span class="sxs-lookup"><span data-stu-id="1ccc9-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="1ccc9-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="1ccc9-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="1ccc9-221">You will also not get the output of the ERROR_\* functions.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-221">You will also not get the output of the ERROR_\* functions.</span></span>

<span data-ttu-id="1ccc9-222">In SQL Data Warehouse the code needs to be slightly altered:</span><span class="sxs-lookup"><span data-stu-id="1ccc9-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

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

<span data-ttu-id="1ccc9-223">The expected behavior is now observed.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-223">The expected behavior is now observed.</span></span> <span data-ttu-id="1ccc9-224">The error in the transaction is managed and the ERROR_\* functions provide values as expected.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-224">The error in the transaction is managed and the ERROR_\* functions provide values as expected.</span></span>

<span data-ttu-id="1ccc9-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="1ccc9-226">Error_Line() function</span><span class="sxs-lookup"><span data-stu-id="1ccc9-226">Error_Line() function</span></span>
<span data-ttu-id="1ccc9-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="1ccc9-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="1ccc9-229">Use query labels in your code instead to implement equivalent functionality.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="1ccc9-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="1ccc9-231">Using THROW and RAISERROR</span><span class="sxs-lookup"><span data-stu-id="1ccc9-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="1ccc9-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="1ccc9-233">There are a few differences that are worth paying attention to however.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="1ccc9-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span><span class="sxs-lookup"><span data-stu-id="1ccc9-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="1ccc9-235">RAISERROR error messages are fixed at 50,000</span><span class="sxs-lookup"><span data-stu-id="1ccc9-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="1ccc9-236">Use of sys.messages is not supported</span><span class="sxs-lookup"><span data-stu-id="1ccc9-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="1ccc9-237">Limitiations</span><span class="sxs-lookup"><span data-stu-id="1ccc9-237">Limitiations</span></span>
<span data-ttu-id="1ccc9-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span><span class="sxs-lookup"><span data-stu-id="1ccc9-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="1ccc9-239">They are as follows:</span><span class="sxs-lookup"><span data-stu-id="1ccc9-239">They are as follows:</span></span>

* <span data-ttu-id="1ccc9-240">No distributed transactions</span><span class="sxs-lookup"><span data-stu-id="1ccc9-240">No distributed transactions</span></span>
* <span data-ttu-id="1ccc9-241">No nested transactions permitted</span><span class="sxs-lookup"><span data-stu-id="1ccc9-241">No nested transactions permitted</span></span>
* <span data-ttu-id="1ccc9-242">No save points allowed</span><span class="sxs-lookup"><span data-stu-id="1ccc9-242">No save points allowed</span></span>
* <span data-ttu-id="1ccc9-243">No named transactions</span><span class="sxs-lookup"><span data-stu-id="1ccc9-243">No named transactions</span></span>
* <span data-ttu-id="1ccc9-244">No marked transactions</span><span class="sxs-lookup"><span data-stu-id="1ccc9-244">No marked transactions</span></span>
* <span data-ttu-id="1ccc9-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span><span class="sxs-lookup"><span data-stu-id="1ccc9-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ccc9-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ccc9-246">Next steps</span></span>
<span data-ttu-id="1ccc9-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="1ccc9-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="1ccc9-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="1ccc9-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
