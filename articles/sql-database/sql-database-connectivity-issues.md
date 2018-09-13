---
title: Fix a SQL connection error, transient error | Microsoft Docs
description: Learn how to troubleshoot, diagnose, and prevent a SQL connection error or transient error in Azure SQL Database.
keywords: sql connection,connection string,connectivity issues,transient error,connection error
services: sql-database
author: dalechen
manager: craigg
ms.service: sql-database
ms.custom: develop apps
ms.topic: conceptual
ms.date: 08/01/2018
ms.author: ninarn
ms.openlocfilehash: 1da4e8d94007653a43f187322c1d0e4077e337fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810315"
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="0cd51-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span><span class="sxs-lookup"><span data-stu-id="0cd51-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="0cd51-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0cd51-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="0cd51-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span><span class="sxs-lookup"><span data-stu-id="0cd51-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="0cd51-107">Transient errors (transient faults)</span><span class="sxs-lookup"><span data-stu-id="0cd51-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="0cd51-108">A transient error, also known as a transient fault, has an underlying cause that soon resolves itself.</span><span class="sxs-lookup"><span data-stu-id="0cd51-108">A transient error, also known as a transient fault, has an underlying cause that soon resolves itself.</span></span> <span data-ttu-id="0cd51-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span><span class="sxs-lookup"><span data-stu-id="0cd51-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="0cd51-110">Most of these reconfiguration events finish in less than 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="0cd51-110">Most of these reconfiguration events finish in less than 60 seconds.</span></span> <span data-ttu-id="0cd51-111">During this reconfiguration time span, you might have connectivity issues to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0cd51-111">During this reconfiguration time span, you might have connectivity issues to SQL Database.</span></span> <span data-ttu-id="0cd51-112">Applications that connect to SQL Database should be built to expect these transient errors.</span><span class="sxs-lookup"><span data-stu-id="0cd51-112">Applications that connect to SQL Database should be built to expect these transient errors.</span></span> <span data-ttu-id="0cd51-113">To handle them, implement retry logic in their code instead of surfacing them to users as application errors.</span><span class="sxs-lookup"><span data-stu-id="0cd51-113">To handle them, implement retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="0cd51-114">If your client program uses ADO.NET, your program is told about the transient error by the throw of **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="0cd51-114">If your client program uses ADO.NET, your program is told about the transient error by the throw of **SqlException**.</span></span> <span data-ttu-id="0cd51-115">Compare the **Number** property against the list of transient errors that are found near the top of the article [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="0cd51-115">Compare the **Number** property against the list of transient errors that are found near the top of the article [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-vs-command"></a><span data-ttu-id="0cd51-116">Connection vs. command</span><span class="sxs-lookup"><span data-stu-id="0cd51-116">Connection vs. command</span></span>
<span data-ttu-id="0cd51-117">Retry the SQL connection or establish it again, depending on the following:</span><span class="sxs-lookup"><span data-stu-id="0cd51-117">Retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="0cd51-118">**A transient error occurs during a connection try**: After a delay of several seconds, retry the connection.</span><span class="sxs-lookup"><span data-stu-id="0cd51-118">**A transient error occurs during a connection try**: After a delay of several seconds, retry the connection.</span></span>
* <span data-ttu-id="0cd51-119">**A transient error occurs during a SQL query command**: Do not immediately retry the command.</span><span class="sxs-lookup"><span data-stu-id="0cd51-119">**A transient error occurs during a SQL query command**: Do not immediately retry the command.</span></span> <span data-ttu-id="0cd51-120">Instead, after a delay, freshly establish the connection.</span><span class="sxs-lookup"><span data-stu-id="0cd51-120">Instead, after a delay, freshly establish the connection.</span></span> <span data-ttu-id="0cd51-121">Then retry the command.</span><span class="sxs-lookup"><span data-stu-id="0cd51-121">Then retry the command.</span></span>


<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

## <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="0cd51-122">Retry logic for transient errors</span><span class="sxs-lookup"><span data-stu-id="0cd51-122">Retry logic for transient errors</span></span>
<span data-ttu-id="0cd51-123">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span><span class="sxs-lookup"><span data-stu-id="0cd51-123">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="0cd51-124">When your program communicates with SQL Database through third-party middleware, ask the vendor whether the middleware contains retry logic for transient errors.</span><span class="sxs-lookup"><span data-stu-id="0cd51-124">When your program communicates with SQL Database through third-party middleware, ask the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

### <a name="principles-for-retry"></a><span data-ttu-id="0cd51-125">Principles for retry</span><span class="sxs-lookup"><span data-stu-id="0cd51-125">Principles for retry</span></span>
* <span data-ttu-id="0cd51-126">If the error is transient, retry to open a connection.</span><span class="sxs-lookup"><span data-stu-id="0cd51-126">If the error is transient, retry to open a connection.</span></span>
* <span data-ttu-id="0cd51-127">Do not directly retry a SQL SELECT statement that failed with a transient error.</span><span class="sxs-lookup"><span data-stu-id="0cd51-127">Do not directly retry a SQL SELECT statement that failed with a transient error.</span></span>
  * <span data-ttu-id="0cd51-128">Instead, establish a fresh connection, and then retry the SELECT.</span><span class="sxs-lookup"><span data-stu-id="0cd51-128">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="0cd51-129">When a SQL UPDATE statement fails with a transient error, establish a fresh connection before you retry the UPDATE.</span><span class="sxs-lookup"><span data-stu-id="0cd51-129">When a SQL UPDATE statement fails with a transient error, establish a fresh connection before you retry the UPDATE.</span></span>
  * <span data-ttu-id="0cd51-130">The retry logic must ensure that either the entire database transaction finished or that the entire transaction is rolled back.</span><span class="sxs-lookup"><span data-stu-id="0cd51-130">The retry logic must ensure that either the entire database transaction finished or that the entire transaction is rolled back.</span></span>

### <a name="other-considerations-for-retry"></a><span data-ttu-id="0cd51-131">Other considerations for retry</span><span class="sxs-lookup"><span data-stu-id="0cd51-131">Other considerations for retry</span></span>
* <span data-ttu-id="0cd51-132">A batch program that automatically starts after work hours and finishes before morning can afford to be very patient with long time intervals between its retry attempts.</span><span class="sxs-lookup"><span data-stu-id="0cd51-132">A batch program that automatically starts after work hours and finishes before morning can afford to be very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="0cd51-133">A user interface program should account for the human tendency to give up after too long a wait.</span><span class="sxs-lookup"><span data-stu-id="0cd51-133">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  * <span data-ttu-id="0cd51-134">The solution must not retry every few seconds, because that policy can flood the system with requests.</span><span class="sxs-lookup"><span data-stu-id="0cd51-134">The solution must not retry every few seconds, because that policy can flood the system with requests.</span></span>

### <a name="interval-increase-between-retries"></a><span data-ttu-id="0cd51-135">Interval increase between retries</span><span class="sxs-lookup"><span data-stu-id="0cd51-135">Interval increase between retries</span></span>
<span data-ttu-id="0cd51-136">We recommend that you wait for 5 seconds before your first retry.</span><span class="sxs-lookup"><span data-stu-id="0cd51-136">We recommend that you wait for 5 seconds before your first retry.</span></span> <span data-ttu-id="0cd51-137">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span><span class="sxs-lookup"><span data-stu-id="0cd51-137">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="0cd51-138">For each subsequent retry, the delay should grow exponentially, up to a maximum of 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="0cd51-138">For each subsequent retry, the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="0cd51-139">For a discussion of the blocking period for clients that use ADO.NET, see [SQL Server connection pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cd51-139">For a discussion of the blocking period for clients that use ADO.NET, see [SQL Server connection pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="0cd51-140">You also might want to set a maximum number of retries before the program self-terminates.</span><span class="sxs-lookup"><span data-stu-id="0cd51-140">You also might want to set a maximum number of retries before the program self-terminates.</span></span>

### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="0cd51-141">Code samples with retry logic</span><span class="sxs-lookup"><span data-stu-id="0cd51-141">Code samples with retry logic</span></span>
<span data-ttu-id="0cd51-142">Code examples with retry logic are available at:</span><span class="sxs-lookup"><span data-stu-id="0cd51-142">Code examples with retry logic are available at:</span></span>

- <span data-ttu-id="0cd51-143">[Connect resiliently to SQL with ADO.NET][step-4-connect-resiliently-to-sql-with-ado-net-a78n]</span><span class="sxs-lookup"><span data-stu-id="0cd51-143">[Connect resiliently to SQL with ADO.NET][step-4-connect-resiliently-to-sql-with-ado-net-a78n]</span></span>
- <span data-ttu-id="0cd51-144">[Connect resiliently to SQL with PHP][step-4-connect-resiliently-to-sql-with-php-p42h]</span><span class="sxs-lookup"><span data-stu-id="0cd51-144">[Connect resiliently to SQL with PHP][step-4-connect-resiliently-to-sql-with-php-p42h]</span></span>

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

### <a name="test-your-retry-logic"></a><span data-ttu-id="0cd51-145">Test your retry logic</span><span class="sxs-lookup"><span data-stu-id="0cd51-145">Test your retry logic</span></span>
<span data-ttu-id="0cd51-146">To test your retry logic, you must simulate or cause an error that can be corrected while your program is still running.</span><span class="sxs-lookup"><span data-stu-id="0cd51-146">To test your retry logic, you must simulate or cause an error that can be corrected while your program is still running.</span></span>

#### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="0cd51-147">Test by disconnecting from the network</span><span class="sxs-lookup"><span data-stu-id="0cd51-147">Test by disconnecting from the network</span></span>
<span data-ttu-id="0cd51-148">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span><span class="sxs-lookup"><span data-stu-id="0cd51-148">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="0cd51-149">The error is:</span><span class="sxs-lookup"><span data-stu-id="0cd51-149">The error is:</span></span>

* <span data-ttu-id="0cd51-150">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="0cd51-150">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="0cd51-151">Message: "No such host is known"</span><span class="sxs-lookup"><span data-stu-id="0cd51-151">Message: "No such host is known"</span></span>

<span data-ttu-id="0cd51-152">As part of the first retry attempt, your program can correct the misspelling and then attempt to connect.</span><span class="sxs-lookup"><span data-stu-id="0cd51-152">As part of the first retry attempt, your program can correct the misspelling and then attempt to connect.</span></span>

<span data-ttu-id="0cd51-153">To make this test practical, unplug your computer from the network before you start your program.</span><span class="sxs-lookup"><span data-stu-id="0cd51-153">To make this test practical, unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="0cd51-154">Then your program recognizes a runtime parameter that causes the program to:</span><span class="sxs-lookup"><span data-stu-id="0cd51-154">Then your program recognizes a runtime parameter that causes the program to:</span></span>

* <span data-ttu-id="0cd51-155">Temporarily add 11001 to its list of errors to consider as transient.</span><span class="sxs-lookup"><span data-stu-id="0cd51-155">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
* <span data-ttu-id="0cd51-156">Attempt its first connection as usual.</span><span class="sxs-lookup"><span data-stu-id="0cd51-156">Attempt its first connection as usual.</span></span>
* <span data-ttu-id="0cd51-157">After the error is caught, remove 11001 from the list.</span><span class="sxs-lookup"><span data-stu-id="0cd51-157">After the error is caught, remove 11001 from the list.</span></span>
* <span data-ttu-id="0cd51-158">Display a message that tells the user to plug the computer into the network.</span><span class="sxs-lookup"><span data-stu-id="0cd51-158">Display a message that tells the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="0cd51-159">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span><span class="sxs-lookup"><span data-stu-id="0cd51-159">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="0cd51-160">The user presses the Enter key after the computer is plugged into the network.</span><span class="sxs-lookup"><span data-stu-id="0cd51-160">The user presses the Enter key after the computer is plugged into the network.</span></span>
* <span data-ttu-id="0cd51-161">Attempt again to connect, expecting success.</span><span class="sxs-lookup"><span data-stu-id="0cd51-161">Attempt again to connect, expecting success.</span></span>

#### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="0cd51-162">Test by misspelling the database name when connecting</span><span class="sxs-lookup"><span data-stu-id="0cd51-162">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="0cd51-163">Your program can purposely misspell the user name before the first connection attempt.</span><span class="sxs-lookup"><span data-stu-id="0cd51-163">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="0cd51-164">The error is:</span><span class="sxs-lookup"><span data-stu-id="0cd51-164">The error is:</span></span>

* <span data-ttu-id="0cd51-165">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="0cd51-165">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="0cd51-166">Message: "Login failed for user 'WRONG_MyUserName'."</span><span class="sxs-lookup"><span data-stu-id="0cd51-166">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="0cd51-167">As part of the first retry attempt, your program can correct the misspelling and then attempt to connect.</span><span class="sxs-lookup"><span data-stu-id="0cd51-167">As part of the first retry attempt, your program can correct the misspelling and then attempt to connect.</span></span>

<span data-ttu-id="0cd51-168">To make this test practical, your program recognizes a runtime parameter that causes the program to:</span><span class="sxs-lookup"><span data-stu-id="0cd51-168">To make this test practical, your program recognizes a runtime parameter that causes the program to:</span></span>

* <span data-ttu-id="0cd51-169">Temporarily add 18456 to its list of errors to consider as transient.</span><span class="sxs-lookup"><span data-stu-id="0cd51-169">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
* <span data-ttu-id="0cd51-170">Purposely add 'WRONG_' to the user name.</span><span class="sxs-lookup"><span data-stu-id="0cd51-170">Purposely add 'WRONG_' to the user name.</span></span>
* <span data-ttu-id="0cd51-171">After the error is caught, remove 18456 from the list.</span><span class="sxs-lookup"><span data-stu-id="0cd51-171">After the error is caught, remove 18456 from the list.</span></span>
* <span data-ttu-id="0cd51-172">Remove 'WRONG_' from the user name.</span><span class="sxs-lookup"><span data-stu-id="0cd51-172">Remove 'WRONG_' from the user name.</span></span>
* <span data-ttu-id="0cd51-173">Attempt again to connect, expecting success.</span><span class="sxs-lookup"><span data-stu-id="0cd51-173">Attempt again to connect, expecting success.</span></span>


<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

## <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="0cd51-174">.NET SqlConnection parameters for connection retry</span><span class="sxs-lookup"><span data-stu-id="0cd51-174">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="0cd51-175">If your client program connects to SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, use .NET 4.6.1 or later (or .NET Core) so that you can use its connection retry feature.</span><span class="sxs-lookup"><span data-stu-id="0cd51-175">If your client program connects to SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, use .NET 4.6.1 or later (or .NET Core) so that you can use its connection retry feature.</span></span> <span data-ttu-id="0cd51-176">For more information on the feature, see [this webpage](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="0cd51-176">For more information on the feature, see [this webpage](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->

<span data-ttu-id="0cd51-177">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, coordinate the values among the following parameters:</span><span class="sxs-lookup"><span data-stu-id="0cd51-177">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="0cd51-178">**ConnectRetryCount**:&nbsp;&nbsp;Default is 1.</span><span class="sxs-lookup"><span data-stu-id="0cd51-178">**ConnectRetryCount**:&nbsp;&nbsp;Default is 1.</span></span> <span data-ttu-id="0cd51-179">Range is 0 through 255.</span><span class="sxs-lookup"><span data-stu-id="0cd51-179">Range is 0 through 255.</span></span>
* <span data-ttu-id="0cd51-180">**ConnectRetryInterval**:&nbsp;&nbsp;Default is 1 second.</span><span class="sxs-lookup"><span data-stu-id="0cd51-180">**ConnectRetryInterval**:&nbsp;&nbsp;Default is 1 second.</span></span> <span data-ttu-id="0cd51-181">Range is 1 through 60.</span><span class="sxs-lookup"><span data-stu-id="0cd51-181">Range is 1 through 60.</span></span>
* <span data-ttu-id="0cd51-182">**Connection Timeout**:&nbsp;&nbsp;Default is 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="0cd51-182">**Connection Timeout**:&nbsp;&nbsp;Default is 15 seconds.</span></span> <span data-ttu-id="0cd51-183">Range is 0 through 2147483647.</span><span class="sxs-lookup"><span data-stu-id="0cd51-183">Range is 0 through 2147483647.</span></span>

<span data-ttu-id="0cd51-184">Specifically, your chosen values should make the following equality true:</span><span class="sxs-lookup"><span data-stu-id="0cd51-184">Specifically, your chosen values should make the following equality true:</span></span>

<span data-ttu-id="0cd51-185">Connection Timeout = ConnectRetryCount \* ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="0cd51-185">Connection Timeout = ConnectRetryCount \* ConnectionRetryInterval</span></span>

<span data-ttu-id="0cd51-186">For example, if the count equals 3 and the interval equals 10 seconds, a timeout of only 29 seconds doesn't give the system enough time for its third and final retry to connect: 29 < 3 \* 10.</span><span class="sxs-lookup"><span data-stu-id="0cd51-186">For example, if the count equals 3 and the interval equals 10 seconds, a timeout of only 29 seconds doesn't give the system enough time for its third and final retry to connect: 29 < 3 \* 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

## <a name="connection-vs-command"></a><span data-ttu-id="0cd51-187">Connection vs. command</span><span class="sxs-lookup"><span data-stu-id="0cd51-187">Connection vs. command</span></span>
<span data-ttu-id="0cd51-188">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span><span class="sxs-lookup"><span data-stu-id="0cd51-188">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="0cd51-189">The retries can occur in the following situations:</span><span class="sxs-lookup"><span data-stu-id="0cd51-189">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="0cd51-190">mySqlConnection.Open method call</span><span class="sxs-lookup"><span data-stu-id="0cd51-190">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="0cd51-191">mySqlConnection.Execute method call</span><span class="sxs-lookup"><span data-stu-id="0cd51-191">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="0cd51-192">There is a subtlety.</span><span class="sxs-lookup"><span data-stu-id="0cd51-192">There is a subtlety.</span></span> <span data-ttu-id="0cd51-193">If a transient error occurs while your *query* is being executed, your **SqlConnection** object doesn't retry the connect operation.</span><span class="sxs-lookup"><span data-stu-id="0cd51-193">If a transient error occurs while your *query* is being executed, your **SqlConnection** object doesn't retry the connect operation.</span></span> <span data-ttu-id="0cd51-194">It certainly doesn't retry your query.</span><span class="sxs-lookup"><span data-stu-id="0cd51-194">It certainly doesn't retry your query.</span></span> <span data-ttu-id="0cd51-195">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span><span class="sxs-lookup"><span data-stu-id="0cd51-195">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="0cd51-196">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span><span class="sxs-lookup"><span data-stu-id="0cd51-196">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="0cd51-197">If the retry succeeds, your query is sent for execution.</span><span class="sxs-lookup"><span data-stu-id="0cd51-197">If the retry succeeds, your query is sent for execution.</span></span>

### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="0cd51-198">Should ConnectRetryCount be combined with application retry logic?</span><span class="sxs-lookup"><span data-stu-id="0cd51-198">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="0cd51-199">Suppose your application has robust custom retry logic.</span><span class="sxs-lookup"><span data-stu-id="0cd51-199">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="0cd51-200">It might retry the connect operation four times.</span><span class="sxs-lookup"><span data-stu-id="0cd51-200">It might retry the connect operation four times.</span></span> <span data-ttu-id="0cd51-201">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 \* 3 = 12 retries.</span><span class="sxs-lookup"><span data-stu-id="0cd51-201">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 \* 3 = 12 retries.</span></span> <span data-ttu-id="0cd51-202">You might not intend such a high number of retries.</span><span class="sxs-lookup"><span data-stu-id="0cd51-202">You might not intend such a high number of retries.</span></span>


<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-sql-database"></a><span data-ttu-id="0cd51-203">Connections to SQL Database</span><span class="sxs-lookup"><span data-stu-id="0cd51-203">Connections to SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="0cd51-204">Connection: Connection string</span><span class="sxs-lookup"><span data-stu-id="0cd51-204">Connection: Connection string</span></span>
<span data-ttu-id="0cd51-205">The connection string that's necessary to connect to SQL Database is slightly different from the string used to connect to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cd51-205">The connection string that's necessary to connect to SQL Database is slightly different from the string used to connect to SQL Server.</span></span> <span data-ttu-id="0cd51-206">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0cd51-206">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="0cd51-207">Connection: IP address</span><span class="sxs-lookup"><span data-stu-id="0cd51-207">Connection: IP address</span></span>
<span data-ttu-id="0cd51-208">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span><span class="sxs-lookup"><span data-stu-id="0cd51-208">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="0cd51-209">To set up this configuration, edit the firewall settings through the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0cd51-209">To set up this configuration, edit the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="0cd51-210">If you forget to configure the IP address, your program fails with a handy error message that states the necessary IP address.</span><span class="sxs-lookup"><span data-stu-id="0cd51-210">If you forget to configure the IP address, your program fails with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="0cd51-211">For more information, see [Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md).</span><span class="sxs-lookup"><span data-stu-id="0cd51-211">For more information, see [Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md).</span></span>
<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="0cd51-212">Connection: Ports</span><span class="sxs-lookup"><span data-stu-id="0cd51-212">Connection: Ports</span></span>
<span data-ttu-id="0cd51-213">Typically, you need to ensure that only port 1433 is open for outbound communication on the computer that hosts your client program.</span><span class="sxs-lookup"><span data-stu-id="0cd51-213">Typically, you need to ensure that only port 1433 is open for outbound communication on the computer that hosts your client program.</span></span>

<span data-ttu-id="0cd51-214">For example, when your client program is hosted on a Windows computer, you can use Windows Firewall on the host to open port 1433.</span><span class="sxs-lookup"><span data-stu-id="0cd51-214">For example, when your client program is hosted on a Windows computer, you can use Windows Firewall on the host to open port 1433.</span></span>

1. <span data-ttu-id="0cd51-215">Open Control Panel.</span><span class="sxs-lookup"><span data-stu-id="0cd51-215">Open Control Panel.</span></span>

2. <span data-ttu-id="0cd51-216">Select **All Control Panel Items** > **Windows Firewall** > **Advanced Settings** > **Outbound Rules** > **Actions** > **New Rule**.</span><span class="sxs-lookup"><span data-stu-id="0cd51-216">Select **All Control Panel Items** > **Windows Firewall** > **Advanced Settings** > **Outbound Rules** > **Actions** > **New Rule**.</span></span>

<span data-ttu-id="0cd51-217">If your client program is hosted on an Azure virtual machine (VM), read [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="0cd51-217">If your client program is hosted on an Azure virtual machine (VM), read [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="0cd51-218">For background information about configuration of ports and IP addresses, see [Azure SQL Database firewall](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0cd51-218">For background information about configuration of ports and IP addresses, see [Azure SQL Database firewall](sql-database-firewall-configure.md).</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-462-or-later"></a><span data-ttu-id="0cd51-219">Connection: ADO.NET 4.6.2 or later</span><span class="sxs-lookup"><span data-stu-id="0cd51-219">Connection: ADO.NET 4.6.2 or later</span></span>
<span data-ttu-id="0cd51-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to SQL Database, we recommend that you use .NET Framework version 4.6.2 or later.</span><span class="sxs-lookup"><span data-stu-id="0cd51-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to SQL Database, we recommend that you use .NET Framework version 4.6.2 or later.</span></span>

<span data-ttu-id="0cd51-221">Starting with ADO.NET 4.6.2:</span><span class="sxs-lookup"><span data-stu-id="0cd51-221">Starting with ADO.NET 4.6.2:</span></span>

- <span data-ttu-id="0cd51-222">The connection open attempt to be retried immediately for Azure SQL databases, thereby improving the performance of cloud-enabled apps.</span><span class="sxs-lookup"><span data-stu-id="0cd51-222">The connection open attempt to be retried immediately for Azure SQL databases, thereby improving the performance of cloud-enabled apps.</span></span>

<span data-ttu-id="0cd51-223">Starting with ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="0cd51-223">Starting with ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="0cd51-224">For SQL Database, reliability is improved when you open a connection by using the **SqlConnection.Open** method.</span><span class="sxs-lookup"><span data-stu-id="0cd51-224">For SQL Database, reliability is improved when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="0cd51-225">The **Open** method now incorporates best-effort retry mechanisms in response to transient faults for certain errors within the connection timeout period.</span><span class="sxs-lookup"><span data-stu-id="0cd51-225">The **Open** method now incorporates best-effort retry mechanisms in response to transient faults for certain errors within the connection timeout period.</span></span>
* <span data-ttu-id="0cd51-226">Connection pooling is supported, which includes an efficient verification that the connection object it gives your program is functioning.</span><span class="sxs-lookup"><span data-stu-id="0cd51-226">Connection pooling is supported, which includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="0cd51-227">When you use a connection object from a connection pool, we recommend that your program temporarily closes the connection when it's not immediately in use.</span><span class="sxs-lookup"><span data-stu-id="0cd51-227">When you use a connection object from a connection pool, we recommend that your program temporarily closes the connection when it's not immediately in use.</span></span> <span data-ttu-id="0cd51-228">It's not expensive to reopen a connection, but it is to create a new connection.</span><span class="sxs-lookup"><span data-stu-id="0cd51-228">It's not expensive to reopen a connection, but it is to create a new connection.</span></span>

<span data-ttu-id="0cd51-229">If you use ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="0cd51-229">If you use ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span> <span data-ttu-id="0cd51-230">As of August 2018, you can [download ADO.NET 4.6.2](https://blogs.msdn.microsoft.com/dotnet/2018/04/30/announcing-the-net-framework-4-7-2/).</span><span class="sxs-lookup"><span data-stu-id="0cd51-230">As of August 2018, you can [download ADO.NET 4.6.2](https://blogs.msdn.microsoft.com/dotnet/2018/04/30/announcing-the-net-framework-4-7-2/).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="0cd51-231">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="0cd51-231">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="0cd51-232">Diagnostics: Test whether utilities can connect</span><span class="sxs-lookup"><span data-stu-id="0cd51-232">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="0cd51-233">If your program fails to connect to SQL Database, one diagnostic option is to try to connect with a utility program.</span><span class="sxs-lookup"><span data-stu-id="0cd51-233">If your program fails to connect to SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="0cd51-234">Ideally, the utility connects by using the same library that your program uses.</span><span class="sxs-lookup"><span data-stu-id="0cd51-234">Ideally, the utility connects by using the same library that your program uses.</span></span>

<span data-ttu-id="0cd51-235">On any Windows computer, you can try these utilities:</span><span class="sxs-lookup"><span data-stu-id="0cd51-235">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="0cd51-236">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET</span><span class="sxs-lookup"><span data-stu-id="0cd51-236">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET</span></span>
* <span data-ttu-id="0cd51-237">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx)</span><span class="sxs-lookup"><span data-stu-id="0cd51-237">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx)</span></span>

<span data-ttu-id="0cd51-238">After your program is connected, test whether a short SQL SELECT query works.</span><span class="sxs-lookup"><span data-stu-id="0cd51-238">After your program is connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="0cd51-239">Diagnostics: Check the open ports</span><span class="sxs-lookup"><span data-stu-id="0cd51-239">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="0cd51-240">If you suspect that connection attempts fail due to port issues, you can run a utility on your computer that reports on the port configurations.</span><span class="sxs-lookup"><span data-stu-id="0cd51-240">If you suspect that connection attempts fail due to port issues, you can run a utility on your computer that reports on the port configurations.</span></span>

<span data-ttu-id="0cd51-241">On Linux, the following utilities might be helpful:</span><span class="sxs-lookup"><span data-stu-id="0cd51-241">On Linux, the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="0cd51-242">Change the example value to be your IP address.</span><span class="sxs-lookup"><span data-stu-id="0cd51-242">Change the example value to be your IP address.</span></span>

<span data-ttu-id="0cd51-243">On Windows, the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span><span class="sxs-lookup"><span data-stu-id="0cd51-243">On Windows, the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="0cd51-244">Here's an example execution that queried the port situation on a SQL Database server and that was run on a laptop computer:</span><span class="sxs-lookup"><span data-stu-id="0cd51-244">Here's an example execution that queried the port situation on a SQL Database server and that was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="0cd51-245">Diagnostics: Log your errors</span><span class="sxs-lookup"><span data-stu-id="0cd51-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="0cd51-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span><span class="sxs-lookup"><span data-stu-id="0cd51-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="0cd51-247">Your client can assist in a diagnosis by logging all errors it encounters.</span><span class="sxs-lookup"><span data-stu-id="0cd51-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="0cd51-248">You might be able to correlate the log entries with error data that SQL Database logs itself internally.</span><span class="sxs-lookup"><span data-stu-id="0cd51-248">You might be able to correlate the log entries with error data that SQL Database logs itself internally.</span></span>

<span data-ttu-id="0cd51-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging.</span><span class="sxs-lookup"><span data-stu-id="0cd51-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging.</span></span> <span data-ttu-id="0cd51-250">For more information, see [5 - As easy as falling off a log: Use the Logging Application Block](http://msdn.microsoft.com/library/dn440731.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cd51-250">For more information, see [5 - As easy as falling off a log: Use the Logging Application Block](http://msdn.microsoft.com/library/dn440731.aspx).</span></span>

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="0cd51-251">Diagnostics: Examine system logs for errors</span><span class="sxs-lookup"><span data-stu-id="0cd51-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="0cd51-252">Here are some Transact-SQL SELECT statements that query error logs and other information.</span><span class="sxs-lookup"><span data-stu-id="0cd51-252">Here are some Transact-SQL SELECT statements that query error logs and other information.</span></span>

| <span data-ttu-id="0cd51-253">Query of log</span><span class="sxs-lookup"><span data-stu-id="0cd51-253">Query of log</span></span> | <span data-ttu-id="0cd51-254">Description</span><span class="sxs-lookup"><span data-stu-id="0cd51-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="0cd51-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, which includes some that can cause transient errors or connectivity failures.</span><span class="sxs-lookup"><span data-stu-id="0cd51-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, which includes some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="0cd51-256">Ideally, you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span><span class="sxs-lookup"><span data-stu-id="0cd51-256">Ideally, you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="0cd51-257">You must connect to the *master* database to run this query.</span><span class="sxs-lookup"><span data-stu-id="0cd51-257">You must connect to the *master* database to run this query.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="0cd51-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types for additional diagnostics.</span><span class="sxs-lookup"><span data-stu-id="0cd51-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types for additional diagnostics.</span></span><br/><br/><span data-ttu-id="0cd51-259">You must connect to the *master* database to run this query.</span><span class="sxs-lookup"><span data-stu-id="0cd51-259">You must connect to the *master* database to run this query.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="0cd51-260">Diagnostics: Search for problem events in the SQL Database log</span><span class="sxs-lookup"><span data-stu-id="0cd51-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="0cd51-261">You can search for entries about problem events in the SQL Database log.</span><span class="sxs-lookup"><span data-stu-id="0cd51-261">You can search for entries about problem events in the SQL Database log.</span></span> <span data-ttu-id="0cd51-262">Try the following Transact-SQL SELECT statement in the *master* database:</span><span class="sxs-lookup"><span data-stu-id="0cd51-262">Try the following Transact-SQL SELECT statement in the *master* database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="0cd51-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="0cd51-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="0cd51-264">The following example shows what a returned row might look like.</span><span class="sxs-lookup"><span data-stu-id="0cd51-264">The following example shows what a returned row might look like.</span></span> <span data-ttu-id="0cd51-265">The null values shown are often not null in other rows.</span><span class="sxs-lookup"><span data-stu-id="0cd51-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="0cd51-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="0cd51-266">Enterprise Library 6</span></span>
<span data-ttu-id="0cd51-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the SQL Database service.</span><span class="sxs-lookup"><span data-stu-id="0cd51-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the SQL Database service.</span></span> <span data-ttu-id="0cd51-268">To locate topics dedicated to each area in which EntLib60 can assist, see [Enterprise Library 6 - April 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cd51-268">To locate topics dedicated to each area in which EntLib60 can assist, see [Enterprise Library 6 - April 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx).</span></span>

<span data-ttu-id="0cd51-269">Retry logic for handling transient errors is one area in which EntLib60 can assist.</span><span class="sxs-lookup"><span data-stu-id="0cd51-269">Retry logic for handling transient errors is one area in which EntLib60 can assist.</span></span> <span data-ttu-id="0cd51-270">For more information, see [4 - Perseverance, secret of all triumphs: Use the Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cd51-270">For more information, see [4 - Perseverance, secret of all triumphs: Use the Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0cd51-271">The source code for EntLib60 is available for public download from the [Download Center](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="0cd51-271">The source code for EntLib60 is available for public download from the [Download Center](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="0cd51-272">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span><span class="sxs-lookup"><span data-stu-id="0cd51-272">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
>
>

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="0cd51-273">EntLib60 classes for transient errors and retry</span><span class="sxs-lookup"><span data-stu-id="0cd51-273">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="0cd51-274">The following EntLib60 classes are particularly useful for retry logic.</span><span class="sxs-lookup"><span data-stu-id="0cd51-274">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="0cd51-275">All these classes are found in or under the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**.</span><span class="sxs-lookup"><span data-stu-id="0cd51-275">All these classes are found in or under the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**.</span></span>

<span data-ttu-id="0cd51-276">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="0cd51-276">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

* <span data-ttu-id="0cd51-277">**RetryPolicy** class</span><span class="sxs-lookup"><span data-stu-id="0cd51-277">**RetryPolicy** class</span></span>

  * <span data-ttu-id="0cd51-278">**ExecuteAction** method</span><span class="sxs-lookup"><span data-stu-id="0cd51-278">**ExecuteAction** method</span></span>
* <span data-ttu-id="0cd51-279">**ExponentialBackoff** class</span><span class="sxs-lookup"><span data-stu-id="0cd51-279">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="0cd51-280">**SqlDatabaseTransientErrorDetectionStrategy** class</span><span class="sxs-lookup"><span data-stu-id="0cd51-280">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="0cd51-281">**ReliableSqlConnection** class</span><span class="sxs-lookup"><span data-stu-id="0cd51-281">**ReliableSqlConnection** class</span></span>

  * <span data-ttu-id="0cd51-282">**ExecuteCommand** method</span><span class="sxs-lookup"><span data-stu-id="0cd51-282">**ExecuteCommand** method</span></span>

<span data-ttu-id="0cd51-283">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="0cd51-283">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="0cd51-284">**AlwaysTransientErrorDetectionStrategy** class</span><span class="sxs-lookup"><span data-stu-id="0cd51-284">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="0cd51-285">**NeverTransientErrorDetectionStrategy** class</span><span class="sxs-lookup"><span data-stu-id="0cd51-285">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="0cd51-286">Here are some links to information about EntLib60:</span><span class="sxs-lookup"><span data-stu-id="0cd51-286">Here are some links to information about EntLib60:</span></span>

* <span data-ttu-id="0cd51-287">Free book download: [Developer's Guide to Microsoft Enterprise Library, 2nd edition](http://www.microsoft.com/download/details.aspx?id=41145).</span><span class="sxs-lookup"><span data-stu-id="0cd51-287">Free book download: [Developer's Guide to Microsoft Enterprise Library, 2nd edition](http://www.microsoft.com/download/details.aspx?id=41145).</span></span>
* <span data-ttu-id="0cd51-288">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span><span class="sxs-lookup"><span data-stu-id="0cd51-288">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="0cd51-289">NuGet download: [Enterprise Library - Transient Fault Handling Application Block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="0cd51-289">NuGet download: [Enterprise Library - Transient Fault Handling Application Block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="0cd51-290">EntLib60: The logging block</span><span class="sxs-lookup"><span data-stu-id="0cd51-290">EntLib60: The logging block</span></span>
* <span data-ttu-id="0cd51-291">The logging block is a highly flexible and configurable solution that you can use to:</span><span class="sxs-lookup"><span data-stu-id="0cd51-291">The logging block is a highly flexible and configurable solution that you can use to:</span></span>

  * <span data-ttu-id="0cd51-292">Create and store log messages in a wide variety of locations.</span><span class="sxs-lookup"><span data-stu-id="0cd51-292">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="0cd51-293">Categorize and filter messages.</span><span class="sxs-lookup"><span data-stu-id="0cd51-293">Categorize and filter messages.</span></span>
  * <span data-ttu-id="0cd51-294">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span><span class="sxs-lookup"><span data-stu-id="0cd51-294">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="0cd51-295">The logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span><span class="sxs-lookup"><span data-stu-id="0cd51-295">The logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="0cd51-296">For more information, see [5 - As easy as falling off a log: Use the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cd51-296">For more information, see [5 - As easy as falling off a log: Use the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx).</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="0cd51-297">EntLib60 IsTransient method source code</span><span class="sxs-lookup"><span data-stu-id="0cd51-297">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="0cd51-298">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span><span class="sxs-lookup"><span data-stu-id="0cd51-298">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="0cd51-299">The source code clarifies which errors were considered transient and worthy of retry, as of April 2013.</span><span class="sxs-lookup"><span data-stu-id="0cd51-299">The source code clarifies which errors were considered transient and worthy of retry, as of April 2013.</span></span>

```csharp
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // The instance of SQL Server you attempted to connect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="0cd51-300">Next steps</span><span class="sxs-lookup"><span data-stu-id="0cd51-300">Next steps</span></span>
* <span data-ttu-id="0cd51-301">For more information on troubleshooting other common SQL Database connection issues, see [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="0cd51-301">For more information on troubleshooting other common SQL Database connection issues, see [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="0cd51-302">Connection libraries for SQL Database and SQL Server</span><span class="sxs-lookup"><span data-stu-id="0cd51-302">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)
* [<span data-ttu-id="0cd51-303">SQL Server connection pooling (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="0cd51-303">SQL Server connection pooling (ADO.NET)</span></span>](https://docs.microsoft.com/dotnet/framework/data/adonet/sql-server-connection-pooling)
* <span data-ttu-id="0cd51-304">[*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in Python,](https://pypi.python.org/pypi/retrying) to simplify the task of adding retry behavior to just about anything.</span><span class="sxs-lookup"><span data-stu-id="0cd51-304">[*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in Python,](https://pypi.python.org/pypi/retrying) to simplify the task of adding retry behavior to just about anything.</span></span>


<!-- Link references. -->

[step-4-connect-resiliently-to-sql-with-ado-net-a78n]: https://docs.microsoft.com/sql/connect/ado-net/step-4-connect-resiliently-to-sql-with-ado-net

[step-4-connect-resiliently-to-sql-with-php-p42h]: https://docs.microsoft.com/sql/connect/php/step-4-connect-resiliently-to-sql-with-php
