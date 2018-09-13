---
title: How to use batching to improve Azure SQL Database application performance
description: The topic provides evidence that batching database operations greatly imroves the speed and scalability of your Azure SQL Database applications. Although these batching techniques work for any SQL Server database, the focus of the article is on Azure.
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: ''
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: monitor and tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: b62097f945bc5c595c0893d16bb2c1d9bbfd7a07
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552195"
---
# <a name="how-to-use-batching-to-improve-sql-database-application-performance"></a><span data-ttu-id="131f7-104">How to use batching to improve SQL Database application performance</span><span class="sxs-lookup"><span data-stu-id="131f7-104">How to use batching to improve SQL Database application performance</span></span>
<span data-ttu-id="131f7-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span><span class="sxs-lookup"><span data-stu-id="131f7-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span></span> <span data-ttu-id="131f7-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span><span class="sxs-lookup"><span data-stu-id="131f7-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span></span> <span data-ttu-id="131f7-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span><span class="sxs-lookup"><span data-stu-id="131f7-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="131f7-108">Why is batching important for SQL Database?</span><span class="sxs-lookup"><span data-stu-id="131f7-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="131f7-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span><span class="sxs-lookup"><span data-stu-id="131f7-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="131f7-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span><span class="sxs-lookup"><span data-stu-id="131f7-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="131f7-111">Packaging many separate transactions into a single batch minimizes these costs.</span><span class="sxs-lookup"><span data-stu-id="131f7-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="131f7-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span><span class="sxs-lookup"><span data-stu-id="131f7-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="131f7-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span><span class="sxs-lookup"><span data-stu-id="131f7-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span></span>

* <span data-ttu-id="131f7-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="131f7-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="131f7-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span><span class="sxs-lookup"><span data-stu-id="131f7-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span></span> <span data-ttu-id="131f7-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span><span class="sxs-lookup"><span data-stu-id="131f7-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span></span> <span data-ttu-id="131f7-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span><span class="sxs-lookup"><span data-stu-id="131f7-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="131f7-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span><span class="sxs-lookup"><span data-stu-id="131f7-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="131f7-119">Batching is also effective for architectures that use multiple databases (sharding).</span><span class="sxs-lookup"><span data-stu-id="131f7-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="131f7-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span><span class="sxs-lookup"><span data-stu-id="131f7-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="131f7-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span><span class="sxs-lookup"><span data-stu-id="131f7-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span></span> <span data-ttu-id="131f7-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span><span class="sxs-lookup"><span data-stu-id="131f7-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span></span> <span data-ttu-id="131f7-123">You can no longer look to improve the database hardware or network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="131f7-123">You can no longer look to improve the database hardware or network infrastructure.</span></span> <span data-ttu-id="131f7-124">Microsoft Azure controls those environments.</span><span class="sxs-lookup"><span data-stu-id="131f7-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="131f7-125">The main area that you can control is how your application interacts with SQL Database.</span><span class="sxs-lookup"><span data-stu-id="131f7-125">The main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="131f7-126">Batching is one of these optimizations.</span><span class="sxs-lookup"><span data-stu-id="131f7-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="131f7-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span><span class="sxs-lookup"><span data-stu-id="131f7-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="131f7-128">The last two sections cover batching guidelines and scenarios.</span><span class="sxs-lookup"><span data-stu-id="131f7-128">The last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="131f7-129">Batching strategies</span><span class="sxs-lookup"><span data-stu-id="131f7-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="131f7-130">Note about timing results in this topic</span><span class="sxs-lookup"><span data-stu-id="131f7-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="131f7-131">Results are not benchmarks but are meant to show **relative performance**.</span><span class="sxs-lookup"><span data-stu-id="131f7-131">Results are not benchmarks but are meant to show **relative performance**.</span></span> <span data-ttu-id="131f7-132">Timings are based on an average of at least 10 test runs.</span><span class="sxs-lookup"><span data-stu-id="131f7-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="131f7-133">Operations are inserts into an empty table.</span><span class="sxs-lookup"><span data-stu-id="131f7-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="131f7-134">These tests were measured awhile ago, and they do not necessarily correspond to throughput that you might experience today.</span><span class="sxs-lookup"><span data-stu-id="131f7-134">These tests were measured awhile ago, and they do not necessarily correspond to throughput that you might experience today.</span></span> <span data-ttu-id="131f7-135">The relative benefit of the batching technique should be similar.</span><span class="sxs-lookup"><span data-stu-id="131f7-135">The relative benefit of the batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="131f7-136">Transactions</span><span class="sxs-lookup"><span data-stu-id="131f7-136">Transactions</span></span>
<span data-ttu-id="131f7-137">It seems strange to begin a review of batching by discussing transactions.</span><span class="sxs-lookup"><span data-stu-id="131f7-137">It seems strange to begin a review of batching by discussing transactions.</span></span> <span data-ttu-id="131f7-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span><span class="sxs-lookup"><span data-stu-id="131f7-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="131f7-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span><span class="sxs-lookup"><span data-stu-id="131f7-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span></span>

<span data-ttu-id="131f7-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span><span class="sxs-lookup"><span data-stu-id="131f7-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="131f7-141">The following ADO.NET code sequentially performs these operations.</span><span class="sxs-lookup"><span data-stu-id="131f7-141">The following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="131f7-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span><span class="sxs-lookup"><span data-stu-id="131f7-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span></span> <span data-ttu-id="131f7-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span><span class="sxs-lookup"><span data-stu-id="131f7-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span></span> <span data-ttu-id="131f7-144">Here is the same code that uses a transaction.</span><span class="sxs-lookup"><span data-stu-id="131f7-144">Here is the same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="131f7-145">Transactions are actually being used in both of these examples.</span><span class="sxs-lookup"><span data-stu-id="131f7-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="131f7-146">In the first example, each individual call is an implicit transaction.</span><span class="sxs-lookup"><span data-stu-id="131f7-146">In the first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="131f7-147">In the second example, an explicit transaction wraps all of the calls.</span><span class="sxs-lookup"><span data-stu-id="131f7-147">In the second example, an explicit transaction wraps all of the calls.</span></span> <span data-ttu-id="131f7-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span><span class="sxs-lookup"><span data-stu-id="131f7-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span></span> <span data-ttu-id="131f7-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span><span class="sxs-lookup"><span data-stu-id="131f7-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span></span> <span data-ttu-id="131f7-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span><span class="sxs-lookup"><span data-stu-id="131f7-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span></span>

<span data-ttu-id="131f7-151">The following table shows some ad-hoc testing results.</span><span class="sxs-lookup"><span data-stu-id="131f7-151">The following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="131f7-152">The tests performed the same sequential inserts with and without transactions.</span><span class="sxs-lookup"><span data-stu-id="131f7-152">The tests performed the same sequential inserts with and without transactions.</span></span> <span data-ttu-id="131f7-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="131f7-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span></span> <span data-ttu-id="131f7-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span><span class="sxs-lookup"><span data-stu-id="131f7-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="131f7-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span><span class="sxs-lookup"><span data-stu-id="131f7-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="131f7-156">**On-Premises to Azure**:</span><span class="sxs-lookup"><span data-stu-id="131f7-156">**On-Premises to Azure**:</span></span>

| <span data-ttu-id="131f7-157">Operations</span><span class="sxs-lookup"><span data-stu-id="131f7-157">Operations</span></span> | <span data-ttu-id="131f7-158">No Transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-158">No Transaction (ms)</span></span> | <span data-ttu-id="131f7-159">Transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="131f7-160">1</span><span class="sxs-lookup"><span data-stu-id="131f7-160">1</span></span> |<span data-ttu-id="131f7-161">130</span><span class="sxs-lookup"><span data-stu-id="131f7-161">130</span></span> |<span data-ttu-id="131f7-162">402</span><span class="sxs-lookup"><span data-stu-id="131f7-162">402</span></span> |
| <span data-ttu-id="131f7-163">10</span><span class="sxs-lookup"><span data-stu-id="131f7-163">10</span></span> |<span data-ttu-id="131f7-164">1208</span><span class="sxs-lookup"><span data-stu-id="131f7-164">1208</span></span> |<span data-ttu-id="131f7-165">1226</span><span class="sxs-lookup"><span data-stu-id="131f7-165">1226</span></span> |
| <span data-ttu-id="131f7-166">100</span><span class="sxs-lookup"><span data-stu-id="131f7-166">100</span></span> |<span data-ttu-id="131f7-167">12662</span><span class="sxs-lookup"><span data-stu-id="131f7-167">12662</span></span> |<span data-ttu-id="131f7-168">10395</span><span class="sxs-lookup"><span data-stu-id="131f7-168">10395</span></span> |
| <span data-ttu-id="131f7-169">1000</span><span class="sxs-lookup"><span data-stu-id="131f7-169">1000</span></span> |<span data-ttu-id="131f7-170">128852</span><span class="sxs-lookup"><span data-stu-id="131f7-170">128852</span></span> |<span data-ttu-id="131f7-171">102917</span><span class="sxs-lookup"><span data-stu-id="131f7-171">102917</span></span> |

<span data-ttu-id="131f7-172">**Azure to Azure (same datacenter)**:</span><span class="sxs-lookup"><span data-stu-id="131f7-172">**Azure to Azure (same datacenter)**:</span></span>

| <span data-ttu-id="131f7-173">Operations</span><span class="sxs-lookup"><span data-stu-id="131f7-173">Operations</span></span> | <span data-ttu-id="131f7-174">No Transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-174">No Transaction (ms)</span></span> | <span data-ttu-id="131f7-175">Transaction (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="131f7-176">1</span><span class="sxs-lookup"><span data-stu-id="131f7-176">1</span></span> |<span data-ttu-id="131f7-177">21</span><span class="sxs-lookup"><span data-stu-id="131f7-177">21</span></span> |<span data-ttu-id="131f7-178">26</span><span class="sxs-lookup"><span data-stu-id="131f7-178">26</span></span> |
| <span data-ttu-id="131f7-179">10</span><span class="sxs-lookup"><span data-stu-id="131f7-179">10</span></span> |<span data-ttu-id="131f7-180">220</span><span class="sxs-lookup"><span data-stu-id="131f7-180">220</span></span> |<span data-ttu-id="131f7-181">56</span><span class="sxs-lookup"><span data-stu-id="131f7-181">56</span></span> |
| <span data-ttu-id="131f7-182">100</span><span class="sxs-lookup"><span data-stu-id="131f7-182">100</span></span> |<span data-ttu-id="131f7-183">2145</span><span class="sxs-lookup"><span data-stu-id="131f7-183">2145</span></span> |<span data-ttu-id="131f7-184">341</span><span class="sxs-lookup"><span data-stu-id="131f7-184">341</span></span> |
| <span data-ttu-id="131f7-185">1000</span><span class="sxs-lookup"><span data-stu-id="131f7-185">1000</span></span> |<span data-ttu-id="131f7-186">21479</span><span class="sxs-lookup"><span data-stu-id="131f7-186">21479</span></span> |<span data-ttu-id="131f7-187">2756</span><span class="sxs-lookup"><span data-stu-id="131f7-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="131f7-188">Results are not benchmarks.</span><span class="sxs-lookup"><span data-stu-id="131f7-188">Results are not benchmarks.</span></span> <span data-ttu-id="131f7-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="131f7-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="131f7-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span><span class="sxs-lookup"><span data-stu-id="131f7-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="131f7-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span><span class="sxs-lookup"><span data-stu-id="131f7-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span></span> <span data-ttu-id="131f7-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="131f7-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span></span> <span data-ttu-id="131f7-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span><span class="sxs-lookup"><span data-stu-id="131f7-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span></span>

<span data-ttu-id="131f7-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="131f7-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="131f7-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span><span class="sxs-lookup"><span data-stu-id="131f7-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span></span> <span data-ttu-id="131f7-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span><span class="sxs-lookup"><span data-stu-id="131f7-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span></span>

<span data-ttu-id="131f7-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span><span class="sxs-lookup"><span data-stu-id="131f7-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span></span> <span data-ttu-id="131f7-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span><span class="sxs-lookup"><span data-stu-id="131f7-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="131f7-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="131f7-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="131f7-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://msdn.microsoft.com/library/vstudio/2k2hy99x.aspx).</span><span class="sxs-lookup"><span data-stu-id="131f7-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://msdn.microsoft.com/library/vstudio/2k2hy99x.aspx).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="131f7-201">Table-valued parameters</span><span class="sxs-lookup"><span data-stu-id="131f7-201">Table-valued parameters</span></span>
<span data-ttu-id="131f7-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span><span class="sxs-lookup"><span data-stu-id="131f7-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="131f7-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span><span class="sxs-lookup"><span data-stu-id="131f7-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span></span> <span data-ttu-id="131f7-204">To use table-valued parameters, first define a table type.</span><span class="sxs-lookup"><span data-stu-id="131f7-204">To use table-valued parameters, first define a table type.</span></span> <span data-ttu-id="131f7-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="131f7-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="131f7-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span><span class="sxs-lookup"><span data-stu-id="131f7-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span></span> <span data-ttu-id="131f7-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span><span class="sxs-lookup"><span data-stu-id="131f7-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="131f7-208">The following example shows this technique:</span><span class="sxs-lookup"><span data-stu-id="131f7-208">The following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. The following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="131f7-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span><span class="sxs-lookup"><span data-stu-id="131f7-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="131f7-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span><span class="sxs-lookup"><span data-stu-id="131f7-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="131f7-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span><span class="sxs-lookup"><span data-stu-id="131f7-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span></span>

<span data-ttu-id="131f7-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span><span class="sxs-lookup"><span data-stu-id="131f7-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="131f7-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span><span class="sxs-lookup"><span data-stu-id="131f7-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="131f7-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span><span class="sxs-lookup"><span data-stu-id="131f7-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="131f7-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span><span class="sxs-lookup"><span data-stu-id="131f7-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="131f7-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span><span class="sxs-lookup"><span data-stu-id="131f7-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="131f7-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span></span> <span data-ttu-id="131f7-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span><span class="sxs-lookup"><span data-stu-id="131f7-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span></span> <span data-ttu-id="131f7-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span><span class="sxs-lookup"><span data-stu-id="131f7-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="131f7-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="131f7-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="131f7-221">Operations</span><span class="sxs-lookup"><span data-stu-id="131f7-221">Operations</span></span> | <span data-ttu-id="131f7-222">On-Premises to Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-222">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="131f7-223">Azure same datacenter (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="131f7-224">1</span><span class="sxs-lookup"><span data-stu-id="131f7-224">1</span></span> |<span data-ttu-id="131f7-225">124</span><span class="sxs-lookup"><span data-stu-id="131f7-225">124</span></span> |<span data-ttu-id="131f7-226">32</span><span class="sxs-lookup"><span data-stu-id="131f7-226">32</span></span> |
| <span data-ttu-id="131f7-227">10</span><span class="sxs-lookup"><span data-stu-id="131f7-227">10</span></span> |<span data-ttu-id="131f7-228">131</span><span class="sxs-lookup"><span data-stu-id="131f7-228">131</span></span> |<span data-ttu-id="131f7-229">25</span><span class="sxs-lookup"><span data-stu-id="131f7-229">25</span></span> |
| <span data-ttu-id="131f7-230">100</span><span class="sxs-lookup"><span data-stu-id="131f7-230">100</span></span> |<span data-ttu-id="131f7-231">338</span><span class="sxs-lookup"><span data-stu-id="131f7-231">338</span></span> |<span data-ttu-id="131f7-232">51</span><span class="sxs-lookup"><span data-stu-id="131f7-232">51</span></span> |
| <span data-ttu-id="131f7-233">1000</span><span class="sxs-lookup"><span data-stu-id="131f7-233">1000</span></span> |<span data-ttu-id="131f7-234">2615</span><span class="sxs-lookup"><span data-stu-id="131f7-234">2615</span></span> |<span data-ttu-id="131f7-235">382</span><span class="sxs-lookup"><span data-stu-id="131f7-235">382</span></span> |
| <span data-ttu-id="131f7-236">10000</span><span class="sxs-lookup"><span data-stu-id="131f7-236">10000</span></span> |<span data-ttu-id="131f7-237">23830</span><span class="sxs-lookup"><span data-stu-id="131f7-237">23830</span></span> |<span data-ttu-id="131f7-238">3586</span><span class="sxs-lookup"><span data-stu-id="131f7-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="131f7-239">Results are not benchmarks.</span><span class="sxs-lookup"><span data-stu-id="131f7-239">Results are not benchmarks.</span></span> <span data-ttu-id="131f7-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="131f7-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="131f7-241">The performance gain from batching is immediately apparent.</span><span class="sxs-lookup"><span data-stu-id="131f7-241">The performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="131f7-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span><span class="sxs-lookup"><span data-stu-id="131f7-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span></span> <span data-ttu-id="131f7-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span><span class="sxs-lookup"><span data-stu-id="131f7-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span></span>

<span data-ttu-id="131f7-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="131f7-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="131f7-245">SQL bulk copy</span><span class="sxs-lookup"><span data-stu-id="131f7-245">SQL bulk copy</span></span>
<span data-ttu-id="131f7-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span><span class="sxs-lookup"><span data-stu-id="131f7-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span></span> <span data-ttu-id="131f7-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span><span class="sxs-lookup"><span data-stu-id="131f7-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span></span> <span data-ttu-id="131f7-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="131f7-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="131f7-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="131f7-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="131f7-250">There are some cases where bulk copy is preferred over table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="131f7-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="131f7-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="131f7-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="131f7-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="131f7-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="131f7-253">Operations</span><span class="sxs-lookup"><span data-stu-id="131f7-253">Operations</span></span> | <span data-ttu-id="131f7-254">On-Premises to Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-254">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="131f7-255">Azure same datacenter (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="131f7-256">1</span><span class="sxs-lookup"><span data-stu-id="131f7-256">1</span></span> |<span data-ttu-id="131f7-257">433</span><span class="sxs-lookup"><span data-stu-id="131f7-257">433</span></span> |<span data-ttu-id="131f7-258">57</span><span class="sxs-lookup"><span data-stu-id="131f7-258">57</span></span> |
| <span data-ttu-id="131f7-259">10</span><span class="sxs-lookup"><span data-stu-id="131f7-259">10</span></span> |<span data-ttu-id="131f7-260">441</span><span class="sxs-lookup"><span data-stu-id="131f7-260">441</span></span> |<span data-ttu-id="131f7-261">32</span><span class="sxs-lookup"><span data-stu-id="131f7-261">32</span></span> |
| <span data-ttu-id="131f7-262">100</span><span class="sxs-lookup"><span data-stu-id="131f7-262">100</span></span> |<span data-ttu-id="131f7-263">636</span><span class="sxs-lookup"><span data-stu-id="131f7-263">636</span></span> |<span data-ttu-id="131f7-264">53</span><span class="sxs-lookup"><span data-stu-id="131f7-264">53</span></span> |
| <span data-ttu-id="131f7-265">1000</span><span class="sxs-lookup"><span data-stu-id="131f7-265">1000</span></span> |<span data-ttu-id="131f7-266">2535</span><span class="sxs-lookup"><span data-stu-id="131f7-266">2535</span></span> |<span data-ttu-id="131f7-267">341</span><span class="sxs-lookup"><span data-stu-id="131f7-267">341</span></span> |
| <span data-ttu-id="131f7-268">10000</span><span class="sxs-lookup"><span data-stu-id="131f7-268">10000</span></span> |<span data-ttu-id="131f7-269">21605</span><span class="sxs-lookup"><span data-stu-id="131f7-269">21605</span></span> |<span data-ttu-id="131f7-270">2737</span><span class="sxs-lookup"><span data-stu-id="131f7-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="131f7-271">Results are not benchmarks.</span><span class="sxs-lookup"><span data-stu-id="131f7-271">Results are not benchmarks.</span></span> <span data-ttu-id="131f7-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="131f7-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="131f7-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span><span class="sxs-lookup"><span data-stu-id="131f7-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span></span> <span data-ttu-id="131f7-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="131f7-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span><span class="sxs-lookup"><span data-stu-id="131f7-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span></span>

<span data-ttu-id="131f7-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="131f7-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="131f7-277">Multiple-row Parameterized INSERT statements</span><span class="sxs-lookup"><span data-stu-id="131f7-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="131f7-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="131f7-279">The following code example demonstrates this technique.</span><span class="sxs-lookup"><span data-stu-id="131f7-279">The following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="131f7-280">This example is meant to show the basic concept.</span><span class="sxs-lookup"><span data-stu-id="131f7-280">This example is meant to show the basic concept.</span></span> <span data-ttu-id="131f7-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span><span class="sxs-lookup"><span data-stu-id="131f7-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span></span> <span data-ttu-id="131f7-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span><span class="sxs-lookup"><span data-stu-id="131f7-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="131f7-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="131f7-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="131f7-284">Operations</span><span class="sxs-lookup"><span data-stu-id="131f7-284">Operations</span></span> | <span data-ttu-id="131f7-285">Table-valued parameters (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="131f7-286">Single-statement INSERT (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="131f7-287">1</span><span class="sxs-lookup"><span data-stu-id="131f7-287">1</span></span> |<span data-ttu-id="131f7-288">32</span><span class="sxs-lookup"><span data-stu-id="131f7-288">32</span></span> |<span data-ttu-id="131f7-289">20</span><span class="sxs-lookup"><span data-stu-id="131f7-289">20</span></span> |
| <span data-ttu-id="131f7-290">10</span><span class="sxs-lookup"><span data-stu-id="131f7-290">10</span></span> |<span data-ttu-id="131f7-291">30</span><span class="sxs-lookup"><span data-stu-id="131f7-291">30</span></span> |<span data-ttu-id="131f7-292">25</span><span class="sxs-lookup"><span data-stu-id="131f7-292">25</span></span> |
| <span data-ttu-id="131f7-293">100</span><span class="sxs-lookup"><span data-stu-id="131f7-293">100</span></span> |<span data-ttu-id="131f7-294">33</span><span class="sxs-lookup"><span data-stu-id="131f7-294">33</span></span> |<span data-ttu-id="131f7-295">51</span><span class="sxs-lookup"><span data-stu-id="131f7-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="131f7-296">Results are not benchmarks.</span><span class="sxs-lookup"><span data-stu-id="131f7-296">Results are not benchmarks.</span></span> <span data-ttu-id="131f7-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="131f7-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="131f7-298">This approach can be slightly faster for batches that are less than 100 rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="131f7-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span><span class="sxs-lookup"><span data-stu-id="131f7-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="131f7-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="131f7-300">DataAdapter</span></span>
<span data-ttu-id="131f7-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span><span class="sxs-lookup"><span data-stu-id="131f7-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="131f7-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span><span class="sxs-lookup"><span data-stu-id="131f7-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="131f7-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span><span class="sxs-lookup"><span data-stu-id="131f7-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span></span> <span data-ttu-id="131f7-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="131f7-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="131f7-305">Entity framework</span><span class="sxs-lookup"><span data-stu-id="131f7-305">Entity framework</span></span>
<span data-ttu-id="131f7-306">Entity Framework does not currently support batching.</span><span class="sxs-lookup"><span data-stu-id="131f7-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="131f7-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span><span class="sxs-lookup"><span data-stu-id="131f7-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span></span> <span data-ttu-id="131f7-308">But the solutions are typically complex and customized to the application and data model.</span><span class="sxs-lookup"><span data-stu-id="131f7-308">But the solutions are typically complex and customized to the application and data model.</span></span> <span data-ttu-id="131f7-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span><span class="sxs-lookup"><span data-stu-id="131f7-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="131f7-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="131f7-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="131f7-311">XML</span><span class="sxs-lookup"><span data-stu-id="131f7-311">XML</span></span>
<span data-ttu-id="131f7-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span><span class="sxs-lookup"><span data-stu-id="131f7-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span></span> <span data-ttu-id="131f7-313">However, the use of XML has no advantages over other methods and several disadvantages.</span><span class="sxs-lookup"><span data-stu-id="131f7-313">However, the use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="131f7-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span><span class="sxs-lookup"><span data-stu-id="131f7-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="131f7-315">The stored procedure parses the commands in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="131f7-315">The stored procedure parses the commands in the stored procedure.</span></span>

<span data-ttu-id="131f7-316">There are several disadvantages to this approach:</span><span class="sxs-lookup"><span data-stu-id="131f7-316">There are several disadvantages to this approach:</span></span>

* <span data-ttu-id="131f7-317">Working with XML can be cumbersome and error prone.</span><span class="sxs-lookup"><span data-stu-id="131f7-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="131f7-318">Parsing the XML on the database can be CPU-intensive.</span><span class="sxs-lookup"><span data-stu-id="131f7-318">Parsing the XML on the database can be CPU-intensive.</span></span>
* <span data-ttu-id="131f7-319">In most cases, this method is slower than table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="131f7-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="131f7-320">For these reasons, the use of XML for batch queries is not recommended.</span><span class="sxs-lookup"><span data-stu-id="131f7-320">For these reasons, the use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="131f7-321">Batching considerations</span><span class="sxs-lookup"><span data-stu-id="131f7-321">Batching considerations</span></span>
<span data-ttu-id="131f7-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span><span class="sxs-lookup"><span data-stu-id="131f7-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="131f7-323">Tradeoffs</span><span class="sxs-lookup"><span data-stu-id="131f7-323">Tradeoffs</span></span>
<span data-ttu-id="131f7-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span><span class="sxs-lookup"><span data-stu-id="131f7-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="131f7-325">For example, consider the scenario where your role unexpectedly goes down.</span><span class="sxs-lookup"><span data-stu-id="131f7-325">For example, consider the scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="131f7-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="131f7-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span><span class="sxs-lookup"><span data-stu-id="131f7-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span></span>

<span data-ttu-id="131f7-328">Because of this tradeoff, evaluate the type of operations that you batch.</span><span class="sxs-lookup"><span data-stu-id="131f7-328">Because of this tradeoff, evaluate the type of operations that you batch.</span></span> <span data-ttu-id="131f7-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span><span class="sxs-lookup"><span data-stu-id="131f7-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="131f7-330">Batch size</span><span class="sxs-lookup"><span data-stu-id="131f7-330">Batch size</span></span>
<span data-ttu-id="131f7-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span><span class="sxs-lookup"><span data-stu-id="131f7-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span></span> <span data-ttu-id="131f7-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span><span class="sxs-lookup"><span data-stu-id="131f7-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="131f7-333">For example, consider a scenario where you want to insert 1000 rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-333">For example, consider a scenario where you want to insert 1000 rows.</span></span> <span data-ttu-id="131f7-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span><span class="sxs-lookup"><span data-stu-id="131f7-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="131f7-335">Batch size</span><span class="sxs-lookup"><span data-stu-id="131f7-335">Batch size</span></span> | <span data-ttu-id="131f7-336">Iterations</span><span class="sxs-lookup"><span data-stu-id="131f7-336">Iterations</span></span> | <span data-ttu-id="131f7-337">Table-valued parameters (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="131f7-338">1000</span><span class="sxs-lookup"><span data-stu-id="131f7-338">1000</span></span> |<span data-ttu-id="131f7-339">1</span><span class="sxs-lookup"><span data-stu-id="131f7-339">1</span></span> |<span data-ttu-id="131f7-340">347</span><span class="sxs-lookup"><span data-stu-id="131f7-340">347</span></span> |
| <span data-ttu-id="131f7-341">500</span><span class="sxs-lookup"><span data-stu-id="131f7-341">500</span></span> |<span data-ttu-id="131f7-342">2</span><span class="sxs-lookup"><span data-stu-id="131f7-342">2</span></span> |<span data-ttu-id="131f7-343">355</span><span class="sxs-lookup"><span data-stu-id="131f7-343">355</span></span> |
| <span data-ttu-id="131f7-344">100</span><span class="sxs-lookup"><span data-stu-id="131f7-344">100</span></span> |<span data-ttu-id="131f7-345">10</span><span class="sxs-lookup"><span data-stu-id="131f7-345">10</span></span> |<span data-ttu-id="131f7-346">465</span><span class="sxs-lookup"><span data-stu-id="131f7-346">465</span></span> |
| <span data-ttu-id="131f7-347">50</span><span class="sxs-lookup"><span data-stu-id="131f7-347">50</span></span> |<span data-ttu-id="131f7-348">20</span><span class="sxs-lookup"><span data-stu-id="131f7-348">20</span></span> |<span data-ttu-id="131f7-349">630</span><span class="sxs-lookup"><span data-stu-id="131f7-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="131f7-350">Results are not benchmarks.</span><span class="sxs-lookup"><span data-stu-id="131f7-350">Results are not benchmarks.</span></span> <span data-ttu-id="131f7-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="131f7-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="131f7-352">You can see that the best performance for 1000 rows is to submit them all at once.</span><span class="sxs-lookup"><span data-stu-id="131f7-352">You can see that the best performance for 1000 rows is to submit them all at once.</span></span> <span data-ttu-id="131f7-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span><span class="sxs-lookup"><span data-stu-id="131f7-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="131f7-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span><span class="sxs-lookup"><span data-stu-id="131f7-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span></span>

<span data-ttu-id="131f7-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span><span class="sxs-lookup"><span data-stu-id="131f7-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span></span> <span data-ttu-id="131f7-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span><span class="sxs-lookup"><span data-stu-id="131f7-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span></span> <span data-ttu-id="131f7-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span><span class="sxs-lookup"><span data-stu-id="131f7-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="131f7-358">Finally, balance the size of the batch with the risks associated with batching.</span><span class="sxs-lookup"><span data-stu-id="131f7-358">Finally, balance the size of the batch with the risks associated with batching.</span></span> <span data-ttu-id="131f7-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span><span class="sxs-lookup"><span data-stu-id="131f7-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="131f7-360">Parallel processing</span><span class="sxs-lookup"><span data-stu-id="131f7-360">Parallel processing</span></span>
<span data-ttu-id="131f7-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span><span class="sxs-lookup"><span data-stu-id="131f7-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span></span> <span data-ttu-id="131f7-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span><span class="sxs-lookup"><span data-stu-id="131f7-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="131f7-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span><span class="sxs-lookup"><span data-stu-id="131f7-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="131f7-364">This test shows how more simultaneous batches actually decreased performance.</span><span class="sxs-lookup"><span data-stu-id="131f7-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="131f7-365">Batch size [Iterations]</span><span class="sxs-lookup"><span data-stu-id="131f7-365">Batch size [Iterations]</span></span> | <span data-ttu-id="131f7-366">Two threads (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-366">Two threads (ms)</span></span> | <span data-ttu-id="131f7-367">Four threads (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-367">Four threads (ms)</span></span> | <span data-ttu-id="131f7-368">Six threads (ms)</span><span class="sxs-lookup"><span data-stu-id="131f7-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="131f7-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="131f7-369">1000 [1]</span></span> |<span data-ttu-id="131f7-370">277</span><span class="sxs-lookup"><span data-stu-id="131f7-370">277</span></span> |<span data-ttu-id="131f7-371">315</span><span class="sxs-lookup"><span data-stu-id="131f7-371">315</span></span> |<span data-ttu-id="131f7-372">266</span><span class="sxs-lookup"><span data-stu-id="131f7-372">266</span></span> |
| <span data-ttu-id="131f7-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="131f7-373">500 [2]</span></span> |<span data-ttu-id="131f7-374">548</span><span class="sxs-lookup"><span data-stu-id="131f7-374">548</span></span> |<span data-ttu-id="131f7-375">278</span><span class="sxs-lookup"><span data-stu-id="131f7-375">278</span></span> |<span data-ttu-id="131f7-376">256</span><span class="sxs-lookup"><span data-stu-id="131f7-376">256</span></span> |
| <span data-ttu-id="131f7-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="131f7-377">250 [4]</span></span> |<span data-ttu-id="131f7-378">405</span><span class="sxs-lookup"><span data-stu-id="131f7-378">405</span></span> |<span data-ttu-id="131f7-379">329</span><span class="sxs-lookup"><span data-stu-id="131f7-379">329</span></span> |<span data-ttu-id="131f7-380">265</span><span class="sxs-lookup"><span data-stu-id="131f7-380">265</span></span> |
| <span data-ttu-id="131f7-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="131f7-381">100 [10]</span></span> |<span data-ttu-id="131f7-382">488</span><span class="sxs-lookup"><span data-stu-id="131f7-382">488</span></span> |<span data-ttu-id="131f7-383">439</span><span class="sxs-lookup"><span data-stu-id="131f7-383">439</span></span> |<span data-ttu-id="131f7-384">391</span><span class="sxs-lookup"><span data-stu-id="131f7-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="131f7-385">Results are not benchmarks.</span><span class="sxs-lookup"><span data-stu-id="131f7-385">Results are not benchmarks.</span></span> <span data-ttu-id="131f7-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="131f7-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="131f7-387">There are several potential reasons for the degradation in performance due to parallelism:</span><span class="sxs-lookup"><span data-stu-id="131f7-387">There are several potential reasons for the degradation in performance due to parallelism:</span></span>

* <span data-ttu-id="131f7-388">There are multiple simultaneous network calls instead of one.</span><span class="sxs-lookup"><span data-stu-id="131f7-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="131f7-389">Multiple operations against a single table can result in contention and blocking.</span><span class="sxs-lookup"><span data-stu-id="131f7-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="131f7-390">There are overheads associated with multithreading.</span><span class="sxs-lookup"><span data-stu-id="131f7-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="131f7-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span><span class="sxs-lookup"><span data-stu-id="131f7-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span></span>

<span data-ttu-id="131f7-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span><span class="sxs-lookup"><span data-stu-id="131f7-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span></span> <span data-ttu-id="131f7-393">Database sharding or federations would be a scenario for this approach.</span><span class="sxs-lookup"><span data-stu-id="131f7-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="131f7-394">Sharding uses multiple databases and routes different data to each database.</span><span class="sxs-lookup"><span data-stu-id="131f7-394">Sharding uses multiple databases and routes different data to each database.</span></span> <span data-ttu-id="131f7-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span><span class="sxs-lookup"><span data-stu-id="131f7-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span></span> <span data-ttu-id="131f7-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span><span class="sxs-lookup"><span data-stu-id="131f7-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span></span>

<span data-ttu-id="131f7-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span><span class="sxs-lookup"><span data-stu-id="131f7-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="131f7-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span><span class="sxs-lookup"><span data-stu-id="131f7-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="131f7-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span><span class="sxs-lookup"><span data-stu-id="131f7-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span></span> <span data-ttu-id="131f7-400">A smaller number might result in less contention and a faster execution time.</span><span class="sxs-lookup"><span data-stu-id="131f7-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="131f7-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span><span class="sxs-lookup"><span data-stu-id="131f7-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="131f7-402">Related performance factors</span><span class="sxs-lookup"><span data-stu-id="131f7-402">Related performance factors</span></span>
<span data-ttu-id="131f7-403">Typical guidance on database performance also affects batching.</span><span class="sxs-lookup"><span data-stu-id="131f7-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="131f7-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span><span class="sxs-lookup"><span data-stu-id="131f7-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="131f7-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span><span class="sxs-lookup"><span data-stu-id="131f7-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span></span> <span data-ttu-id="131f7-406">This statement suppresses the return of the count of the affected rows in the procedure.</span><span class="sxs-lookup"><span data-stu-id="131f7-406">This statement suppresses the return of the count of the affected rows in the procedure.</span></span> <span data-ttu-id="131f7-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span><span class="sxs-lookup"><span data-stu-id="131f7-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="131f7-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span><span class="sxs-lookup"><span data-stu-id="131f7-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span></span> <span data-ttu-id="131f7-409">It is possible that more complex stored procedures would benefit from this statement.</span><span class="sxs-lookup"><span data-stu-id="131f7-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="131f7-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span><span class="sxs-lookup"><span data-stu-id="131f7-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span></span> <span data-ttu-id="131f7-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span><span class="sxs-lookup"><span data-stu-id="131f7-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="131f7-412">Batching scenarios</span><span class="sxs-lookup"><span data-stu-id="131f7-412">Batching scenarios</span></span>
<span data-ttu-id="131f7-413">The following sections describe how to use table-valued parameters in three application scenarios.</span><span class="sxs-lookup"><span data-stu-id="131f7-413">The following sections describe how to use table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="131f7-414">The first scenario shows how buffering and batching can work together.</span><span class="sxs-lookup"><span data-stu-id="131f7-414">The first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="131f7-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span><span class="sxs-lookup"><span data-stu-id="131f7-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="131f7-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span><span class="sxs-lookup"><span data-stu-id="131f7-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="131f7-417">Buffering</span><span class="sxs-lookup"><span data-stu-id="131f7-417">Buffering</span></span>
<span data-ttu-id="131f7-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span><span class="sxs-lookup"><span data-stu-id="131f7-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="131f7-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span><span class="sxs-lookup"><span data-stu-id="131f7-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span></span> <span data-ttu-id="131f7-420">It is important to understand this risk and consider the consequences.</span><span class="sxs-lookup"><span data-stu-id="131f7-420">It is important to understand this risk and consider the consequences.</span></span>

<span data-ttu-id="131f7-421">For example, consider a web application that tracks the navigation history of each user.</span><span class="sxs-lookup"><span data-stu-id="131f7-421">For example, consider a web application that tracks the navigation history of each user.</span></span> <span data-ttu-id="131f7-422">On each page request, the application could make a database call to record the user’s page view.</span><span class="sxs-lookup"><span data-stu-id="131f7-422">On each page request, the application could make a database call to record the user’s page view.</span></span> <span data-ttu-id="131f7-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span><span class="sxs-lookup"><span data-stu-id="131f7-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span></span> <span data-ttu-id="131f7-424">You can trigger the database update by elapsed time and/or buffer size.</span><span class="sxs-lookup"><span data-stu-id="131f7-424">You can trigger the database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="131f7-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span><span class="sxs-lookup"><span data-stu-id="131f7-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span></span>

<span data-ttu-id="131f7-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span><span class="sxs-lookup"><span data-stu-id="131f7-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span></span> <span data-ttu-id="131f7-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span><span class="sxs-lookup"><span data-stu-id="131f7-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span></span>

<span data-ttu-id="131f7-428">The following NavHistoryData class models the user navigation details.</span><span class="sxs-lookup"><span data-stu-id="131f7-428">The following NavHistoryData class models the user navigation details.</span></span> <span data-ttu-id="131f7-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span><span class="sxs-lookup"><span data-stu-id="131f7-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="131f7-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span><span class="sxs-lookup"><span data-stu-id="131f7-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span></span> <span data-ttu-id="131f7-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span><span class="sxs-lookup"><span data-stu-id="131f7-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="131f7-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span><span class="sxs-lookup"><span data-stu-id="131f7-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span></span> <span data-ttu-id="131f7-433">It then subscribes to this observable collection with the Buffer method.</span><span class="sxs-lookup"><span data-stu-id="131f7-433">It then subscribes to this observable collection with the Buffer method.</span></span> <span data-ttu-id="131f7-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span><span class="sxs-lookup"><span data-stu-id="131f7-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="131f7-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span><span class="sxs-lookup"><span data-stu-id="131f7-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span></span> <span data-ttu-id="131f7-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span><span class="sxs-lookup"><span data-stu-id="131f7-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="131f7-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span><span class="sxs-lookup"><span data-stu-id="131f7-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="131f7-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span><span class="sxs-lookup"><span data-stu-id="131f7-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="131f7-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span><span class="sxs-lookup"><span data-stu-id="131f7-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="131f7-440">Master detail</span><span class="sxs-lookup"><span data-stu-id="131f7-440">Master detail</span></span>
<span data-ttu-id="131f7-441">Table-valued parameters are useful for simple INSERT scenarios.</span><span class="sxs-lookup"><span data-stu-id="131f7-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="131f7-442">However, it can be more challenging to batch inserts that involve more than one table.</span><span class="sxs-lookup"><span data-stu-id="131f7-442">However, it can be more challenging to batch inserts that involve more than one table.</span></span> <span data-ttu-id="131f7-443">The “master/detail” scenario is a good example.</span><span class="sxs-lookup"><span data-stu-id="131f7-443">The “master/detail” scenario is a good example.</span></span> <span data-ttu-id="131f7-444">The master table identifies the primary entity.</span><span class="sxs-lookup"><span data-stu-id="131f7-444">The master table identifies the primary entity.</span></span> <span data-ttu-id="131f7-445">One or more detail tables store more data about the entity.</span><span class="sxs-lookup"><span data-stu-id="131f7-445">One or more detail tables store more data about the entity.</span></span> <span data-ttu-id="131f7-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span><span class="sxs-lookup"><span data-stu-id="131f7-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span></span> <span data-ttu-id="131f7-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span><span class="sxs-lookup"><span data-stu-id="131f7-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="131f7-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span><span class="sxs-lookup"><span data-stu-id="131f7-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="131f7-449">Each order contains one or more product purchases.</span><span class="sxs-lookup"><span data-stu-id="131f7-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="131f7-450">This information is captured in the PurchaseOrderDetail table.</span><span class="sxs-lookup"><span data-stu-id="131f7-450">This information is captured in the PurchaseOrderDetail table.</span></span> <span data-ttu-id="131f7-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span><span class="sxs-lookup"><span data-stu-id="131f7-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="131f7-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span><span class="sxs-lookup"><span data-stu-id="131f7-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span></span> <span data-ttu-id="131f7-453">The following definition of a foreign key enforces this constraint.</span><span class="sxs-lookup"><span data-stu-id="131f7-453">The following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="131f7-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span><span class="sxs-lookup"><span data-stu-id="131f7-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="131f7-455">Then define a stored procedure that accepts tables of these types.</span><span class="sxs-lookup"><span data-stu-id="131f7-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="131f7-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span><span class="sxs-lookup"><span data-stu-id="131f7-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="131f7-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span><span class="sxs-lookup"><span data-stu-id="131f7-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects the order identifiers in the @orders
    -- table with the actual order identifiers in the PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders to the PurchaseOrder table, storing the actual
    -- order identifiers in the @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match the passed-in order identifiers with the actual identifiers
    -- and complete the @IdentityLink table for use with inserting the details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert the order details into the PurchaseOrderDetail table, 
          -- using the actual order identifiers of the master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="131f7-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span></span> <span data-ttu-id="131f7-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="131f7-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span></span> <span data-ttu-id="131f7-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span><span class="sxs-lookup"><span data-stu-id="131f7-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span></span> <span data-ttu-id="131f7-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span><span class="sxs-lookup"><span data-stu-id="131f7-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span></span>

<span data-ttu-id="131f7-462">This stored procedure can be used from code or from other Transact-SQL calls.</span><span class="sxs-lookup"><span data-stu-id="131f7-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="131f7-463">See the table-valued parameters section of this paper for a code example.</span><span class="sxs-lookup"><span data-stu-id="131f7-463">See the table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="131f7-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="131f7-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="131f7-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span><span class="sxs-lookup"><span data-stu-id="131f7-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="131f7-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span><span class="sxs-lookup"><span data-stu-id="131f7-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span></span> <span data-ttu-id="131f7-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span><span class="sxs-lookup"><span data-stu-id="131f7-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span></span> <span data-ttu-id="131f7-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span><span class="sxs-lookup"><span data-stu-id="131f7-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="131f7-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="131f7-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="131f7-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="131f7-470">UPSERT</span></span>
<span data-ttu-id="131f7-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span><span class="sxs-lookup"><span data-stu-id="131f7-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="131f7-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span><span class="sxs-lookup"><span data-stu-id="131f7-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="131f7-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span><span class="sxs-lookup"><span data-stu-id="131f7-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span></span> <span data-ttu-id="131f7-474">The MERGE statement can perform both insert and update operations in a single call.</span><span class="sxs-lookup"><span data-stu-id="131f7-474">The MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="131f7-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span><span class="sxs-lookup"><span data-stu-id="131f7-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span></span> <span data-ttu-id="131f7-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="131f7-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="131f7-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span><span class="sxs-lookup"><span data-stu-id="131f7-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span></span> <span data-ttu-id="131f7-478">First, create the user-defined table type:</span><span class="sxs-lookup"><span data-stu-id="131f7-478">First, create the user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="131f7-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span><span class="sxs-lookup"><span data-stu-id="131f7-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span></span> <span data-ttu-id="131f7-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="131f7-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="131f7-481">The contents of the @employees table are not shown here.</span><span class="sxs-lookup"><span data-stu-id="131f7-481">The contents of the @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="131f7-482">For more information, see the documentation and examples for the MERGE statement.</span><span class="sxs-lookup"><span data-stu-id="131f7-482">For more information, see the documentation and examples for the MERGE statement.</span></span> <span data-ttu-id="131f7-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span><span class="sxs-lookup"><span data-stu-id="131f7-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span></span> <span data-ttu-id="131f7-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span><span class="sxs-lookup"><span data-stu-id="131f7-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="131f7-485">Recommendation summary</span><span class="sxs-lookup"><span data-stu-id="131f7-485">Recommendation summary</span></span>
<span data-ttu-id="131f7-486">The following list provides a summary of the batching recommendations discussed in this topic:</span><span class="sxs-lookup"><span data-stu-id="131f7-486">The following list provides a summary of the batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="131f7-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span><span class="sxs-lookup"><span data-stu-id="131f7-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="131f7-488">Understand the tradeoffs between batching/buffering and resiliency.</span><span class="sxs-lookup"><span data-stu-id="131f7-488">Understand the tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="131f7-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span><span class="sxs-lookup"><span data-stu-id="131f7-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span></span>
* <span data-ttu-id="131f7-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span><span class="sxs-lookup"><span data-stu-id="131f7-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span></span>
* <span data-ttu-id="131f7-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span><span class="sxs-lookup"><span data-stu-id="131f7-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span></span>
* <span data-ttu-id="131f7-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span><span class="sxs-lookup"><span data-stu-id="131f7-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="131f7-493">For < 100 rows, use a single parameterized INSERT command.</span><span class="sxs-lookup"><span data-stu-id="131f7-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="131f7-494">For < 1000 rows, use table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="131f7-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="131f7-495">For >= 1000 rows, use SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="131f7-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="131f7-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span><span class="sxs-lookup"><span data-stu-id="131f7-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span></span>
* <span data-ttu-id="131f7-497">Batch size guidelines:</span><span class="sxs-lookup"><span data-stu-id="131f7-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="131f7-498">Use the largest batch sizes that make sense for your application and business requirements.</span><span class="sxs-lookup"><span data-stu-id="131f7-498">Use the largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="131f7-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span><span class="sxs-lookup"><span data-stu-id="131f7-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="131f7-500">What is the consequence of retries or loss of the data in the batch?</span><span class="sxs-lookup"><span data-stu-id="131f7-500">What is the consequence of retries or loss of the data in the batch?</span></span> 
  * <span data-ttu-id="131f7-501">Test the largest batch size to verify that SQL Database does not reject it.</span><span class="sxs-lookup"><span data-stu-id="131f7-501">Test the largest batch size to verify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="131f7-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span><span class="sxs-lookup"><span data-stu-id="131f7-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span></span> <span data-ttu-id="131f7-503">These settings provide flexibility.</span><span class="sxs-lookup"><span data-stu-id="131f7-503">These settings provide flexibility.</span></span> <span data-ttu-id="131f7-504">You can change the batching behavior in production without redeploying the cloud service.</span><span class="sxs-lookup"><span data-stu-id="131f7-504">You can change the batching behavior in production without redeploying the cloud service.</span></span>
* <span data-ttu-id="131f7-505">Avoid parallel execution of batches that operate on a single table in one database.</span><span class="sxs-lookup"><span data-stu-id="131f7-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="131f7-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span><span class="sxs-lookup"><span data-stu-id="131f7-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span></span> <span data-ttu-id="131f7-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span><span class="sxs-lookup"><span data-stu-id="131f7-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="131f7-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span><span class="sxs-lookup"><span data-stu-id="131f7-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="131f7-509">Next steps</span><span class="sxs-lookup"><span data-stu-id="131f7-509">Next steps</span></span>
<span data-ttu-id="131f7-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span><span class="sxs-lookup"><span data-stu-id="131f7-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span></span> <span data-ttu-id="131f7-511">But this is just one factor in your overall strategy.</span><span class="sxs-lookup"><span data-stu-id="131f7-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="131f7-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="131f7-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool.md).</span></span>

