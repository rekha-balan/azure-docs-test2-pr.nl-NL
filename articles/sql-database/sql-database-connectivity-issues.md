---
title: Fix a SQL connection error, transient error | Microsoft Docs
description: 'Learn how to troubleshoot, diagnose, and prevent a SQL connection error or transient error in Azure SQL Database. '
keywords: sql connection,connection string,connectivity issues,transient error,connection error
services: sql-database
documentationcenter: ''
author: dalechen
manager: cshepard
editor: ''
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: troubleshoot
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/20/2017
ms.author: daleche
ms.openlocfilehash: 608cbc0fd1cc1d73d28056909ed06618457bd9c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555578"
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="68f83-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span><span class="sxs-lookup"><span data-stu-id="68f83-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="68f83-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="68f83-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="68f83-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span><span class="sxs-lookup"><span data-stu-id="68f83-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="68f83-107">Transient errors (transient faults)</span><span class="sxs-lookup"><span data-stu-id="68f83-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="68f83-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span><span class="sxs-lookup"><span data-stu-id="68f83-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="68f83-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span><span class="sxs-lookup"><span data-stu-id="68f83-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="68f83-110">Most of these reconfiguration events often complete in less than 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="68f83-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="68f83-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="68f83-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="68f83-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span><span class="sxs-lookup"><span data-stu-id="68f83-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="68f83-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="68f83-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="68f83-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="68f83-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="68f83-115">Connection versus command</span><span class="sxs-lookup"><span data-stu-id="68f83-115">Connection versus command</span></span>
<span data-ttu-id="68f83-116">You'll retry the SQL connection or establish it again, depending on the following:</span><span class="sxs-lookup"><span data-stu-id="68f83-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="68f83-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span><span class="sxs-lookup"><span data-stu-id="68f83-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="68f83-118">**A transient error occurs during an SQL query command**: The command should not be immediately retried.</span><span class="sxs-lookup"><span data-stu-id="68f83-118">**A transient error occurs during an SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="68f83-119">Instead, after a delay, the connection should be freshly established.</span><span class="sxs-lookup"><span data-stu-id="68f83-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="68f83-120">Then the command can be retried.</span><span class="sxs-lookup"><span data-stu-id="68f83-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="68f83-121">Retry logic for transient errors</span><span class="sxs-lookup"><span data-stu-id="68f83-121">Retry logic for transient errors</span></span>
<span data-ttu-id="68f83-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span><span class="sxs-lookup"><span data-stu-id="68f83-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="68f83-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span><span class="sxs-lookup"><span data-stu-id="68f83-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="68f83-124">Principles for retry</span><span class="sxs-lookup"><span data-stu-id="68f83-124">Principles for retry</span></span>
* <span data-ttu-id="68f83-125">An attempt to open a connection should be retried if the error is transient.</span><span class="sxs-lookup"><span data-stu-id="68f83-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="68f83-126">An SQL SELECT statement that fails with a transient error should not be retried directly.</span><span class="sxs-lookup"><span data-stu-id="68f83-126">An SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="68f83-127">Instead, establish a fresh connection, and then retry the SELECT.</span><span class="sxs-lookup"><span data-stu-id="68f83-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="68f83-128">When an SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span><span class="sxs-lookup"><span data-stu-id="68f83-128">When an SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="68f83-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span><span class="sxs-lookup"><span data-stu-id="68f83-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="68f83-130">Other considerations for retry</span><span class="sxs-lookup"><span data-stu-id="68f83-130">Other considerations for retry</span></span>
* <span data-ttu-id="68f83-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span><span class="sxs-lookup"><span data-stu-id="68f83-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="68f83-132">A user interface program should account for the human tendency to give up after too long a wait.</span><span class="sxs-lookup"><span data-stu-id="68f83-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="68f83-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span><span class="sxs-lookup"><span data-stu-id="68f83-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="68f83-134">Interval increase between retries</span><span class="sxs-lookup"><span data-stu-id="68f83-134">Interval increase between retries</span></span>
<span data-ttu-id="68f83-135">We recommend that you delay for 5 seconds before your first retry.</span><span class="sxs-lookup"><span data-stu-id="68f83-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="68f83-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span><span class="sxs-lookup"><span data-stu-id="68f83-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="68f83-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="68f83-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="68f83-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="68f83-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="68f83-139">You might also want to set a maximum number of retries before the program self-terminates.</span><span class="sxs-lookup"><span data-stu-id="68f83-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="68f83-140">Code samples with retry logic</span><span class="sxs-lookup"><span data-stu-id="68f83-140">Code samples with retry logic</span></span>
<span data-ttu-id="68f83-141">Code samples with retry logic, in a variety of programming languages, are available at:</span><span class="sxs-lookup"><span data-stu-id="68f83-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="68f83-142">Connection libraries for SQL Database and SQL Server</span><span class="sxs-lookup"><span data-stu-id="68f83-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="68f83-143">Test your retry logic</span><span class="sxs-lookup"><span data-stu-id="68f83-143">Test your retry logic</span></span>
<span data-ttu-id="68f83-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span><span class="sxs-lookup"><span data-stu-id="68f83-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="68f83-145">Test by disconnecting from the network</span><span class="sxs-lookup"><span data-stu-id="68f83-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="68f83-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span><span class="sxs-lookup"><span data-stu-id="68f83-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="68f83-147">The error will be:</span><span class="sxs-lookup"><span data-stu-id="68f83-147">The error will be:</span></span>

* <span data-ttu-id="68f83-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="68f83-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="68f83-149">Message: "No such host is known"</span><span class="sxs-lookup"><span data-stu-id="68f83-149">Message: "No such host is known"</span></span>

<span data-ttu-id="68f83-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span><span class="sxs-lookup"><span data-stu-id="68f83-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="68f83-151">To make this practical, you unplug your computer from the network before you start your program.</span><span class="sxs-lookup"><span data-stu-id="68f83-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="68f83-152">Then your program recognizes a run time parameter that causes the program to:</span><span class="sxs-lookup"><span data-stu-id="68f83-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="68f83-153">Temporarily add 11001 to its list of errors to consider as transient.</span><span class="sxs-lookup"><span data-stu-id="68f83-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="68f83-154">Attempt its first connection as usual.</span><span class="sxs-lookup"><span data-stu-id="68f83-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="68f83-155">After the error is caught, remove 11001 from the list.</span><span class="sxs-lookup"><span data-stu-id="68f83-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="68f83-156">Display a message telling the user to plug the computer into the network.</span><span class="sxs-lookup"><span data-stu-id="68f83-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="68f83-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span><span class="sxs-lookup"><span data-stu-id="68f83-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="68f83-158">The user presses the Enter key after the computer plugged into the network.</span><span class="sxs-lookup"><span data-stu-id="68f83-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="68f83-159">Attempt again to connect, expecting success.</span><span class="sxs-lookup"><span data-stu-id="68f83-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="68f83-160">Test by misspelling the database name when connecting</span><span class="sxs-lookup"><span data-stu-id="68f83-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="68f83-161">Your program can purposely misspell the user name before the first connection attempt.</span><span class="sxs-lookup"><span data-stu-id="68f83-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="68f83-162">The error will be:</span><span class="sxs-lookup"><span data-stu-id="68f83-162">The error will be:</span></span>

* <span data-ttu-id="68f83-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="68f83-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="68f83-164">Message: "Login failed for user 'WRONG_MyUserName'."</span><span class="sxs-lookup"><span data-stu-id="68f83-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="68f83-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span><span class="sxs-lookup"><span data-stu-id="68f83-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="68f83-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span><span class="sxs-lookup"><span data-stu-id="68f83-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="68f83-167">Temporarily add 18456 to its list of errors to consider as transient.</span><span class="sxs-lookup"><span data-stu-id="68f83-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="68f83-168">Purposely add 'WRONG_' to the user name.</span><span class="sxs-lookup"><span data-stu-id="68f83-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="68f83-169">After the error is caught, remove 18456 from the list.</span><span class="sxs-lookup"><span data-stu-id="68f83-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="68f83-170">Remove 'WRONG_' from the user name.</span><span class="sxs-lookup"><span data-stu-id="68f83-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="68f83-171">Attempt again to connect, expecting success.</span><span class="sxs-lookup"><span data-stu-id="68f83-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="68f83-172">.NET SqlConnection parameters for connection retry</span><span class="sxs-lookup"><span data-stu-id="68f83-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="68f83-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span><span class="sxs-lookup"><span data-stu-id="68f83-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="68f83-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="68f83-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="68f83-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span><span class="sxs-lookup"><span data-stu-id="68f83-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="68f83-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span><span class="sxs-lookup"><span data-stu-id="68f83-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="68f83-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span><span class="sxs-lookup"><span data-stu-id="68f83-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="68f83-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="68f83-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="68f83-179">Specifically, your chosen values should make the following equality true:</span><span class="sxs-lookup"><span data-stu-id="68f83-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="68f83-180">Connection Timeout = ConnectRetryCount \* ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="68f83-180">Connection Timeout = ConnectRetryCount \* ConnectionRetryInterval</span></span>

<span data-ttu-id="68f83-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 \* 10.</span><span class="sxs-lookup"><span data-stu-id="68f83-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 \* 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="68f83-182">Connection versus command</span><span class="sxs-lookup"><span data-stu-id="68f83-182">Connection versus command</span></span>
<span data-ttu-id="68f83-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span><span class="sxs-lookup"><span data-stu-id="68f83-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="68f83-184">The retries can occur in the following situations:</span><span class="sxs-lookup"><span data-stu-id="68f83-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="68f83-185">mySqlConnection.Open method call</span><span class="sxs-lookup"><span data-stu-id="68f83-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="68f83-186">mySqlConnection.Execute method call</span><span class="sxs-lookup"><span data-stu-id="68f83-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="68f83-187">There is a subtlety.</span><span class="sxs-lookup"><span data-stu-id="68f83-187">There is a subtlety.</span></span> <span data-ttu-id="68f83-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span><span class="sxs-lookup"><span data-stu-id="68f83-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="68f83-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span><span class="sxs-lookup"><span data-stu-id="68f83-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="68f83-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span><span class="sxs-lookup"><span data-stu-id="68f83-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="68f83-191">If the retry succeeds, you query is sent for execution.</span><span class="sxs-lookup"><span data-stu-id="68f83-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="68f83-192">Should ConnectRetryCount be combined with application retry logic?</span><span class="sxs-lookup"><span data-stu-id="68f83-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="68f83-193">Suppose your application has robust custom retry logic.</span><span class="sxs-lookup"><span data-stu-id="68f83-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="68f83-194">It might retry the connect operation 4 times.</span><span class="sxs-lookup"><span data-stu-id="68f83-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="68f83-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 \* 3 = 12 retries.</span><span class="sxs-lookup"><span data-stu-id="68f83-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 \* 3 = 12 retries.</span></span> <span data-ttu-id="68f83-196">You might not intend such a high number of retries.</span><span class="sxs-lookup"><span data-stu-id="68f83-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="68f83-197">Connections to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="68f83-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="68f83-198">Connection: Connection string</span><span class="sxs-lookup"><span data-stu-id="68f83-198">Connection: Connection string</span></span>
<span data-ttu-id="68f83-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="68f83-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="68f83-200">You can copy the connection string for your database from the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68f83-200">You can copy the connection string for your database from the [Azure Portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="68f83-201">Connection: IP address</span><span class="sxs-lookup"><span data-stu-id="68f83-201">Connection: IP address</span></span>
<span data-ttu-id="68f83-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span><span class="sxs-lookup"><span data-stu-id="68f83-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="68f83-203">You do this by editing the firewall settings through the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68f83-203">You do this by editing the firewall settings through the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="68f83-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span><span class="sxs-lookup"><span data-stu-id="68f83-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="68f83-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="68f83-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="68f83-206">Connection: Ports</span><span class="sxs-lookup"><span data-stu-id="68f83-206">Connection: Ports</span></span>
<span data-ttu-id="68f83-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span><span class="sxs-lookup"><span data-stu-id="68f83-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="68f83-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span><span class="sxs-lookup"><span data-stu-id="68f83-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="68f83-209">Open the Control Panel</span><span class="sxs-lookup"><span data-stu-id="68f83-209">Open the Control Panel</span></span>
2. <span data-ttu-id="68f83-210">&gt; All Control Panel Items</span><span class="sxs-lookup"><span data-stu-id="68f83-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="68f83-211">&gt; Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="68f83-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="68f83-212">&gt; Advanced Settings</span><span class="sxs-lookup"><span data-stu-id="68f83-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="68f83-213">&gt; Outbound Rules</span><span class="sxs-lookup"><span data-stu-id="68f83-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="68f83-214">&gt; Actions</span><span class="sxs-lookup"><span data-stu-id="68f83-214">&gt; Actions</span></span>
7. <span data-ttu-id="68f83-215">&gt; New Rule</span><span class="sxs-lookup"><span data-stu-id="68f83-215">&gt; New Rule</span></span>

<span data-ttu-id="68f83-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span><span class="sxs-lookup"><span data-stu-id="68f83-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="68f83-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="68f83-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="68f83-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="68f83-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="68f83-219">Connection: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="68f83-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="68f83-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span><span class="sxs-lookup"><span data-stu-id="68f83-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="68f83-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="68f83-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="68f83-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span><span class="sxs-lookup"><span data-stu-id="68f83-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="68f83-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span><span class="sxs-lookup"><span data-stu-id="68f83-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="68f83-224">Supports connection pooling.</span><span class="sxs-lookup"><span data-stu-id="68f83-224">Supports connection pooling.</span></span> <span data-ttu-id="68f83-225">This includes an efficient verification that the connection object it gives your program is functioning.</span><span class="sxs-lookup"><span data-stu-id="68f83-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="68f83-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span><span class="sxs-lookup"><span data-stu-id="68f83-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="68f83-227">Re-opening a connection is not expensive the way creating a new connection is.</span><span class="sxs-lookup"><span data-stu-id="68f83-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="68f83-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="68f83-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="68f83-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="68f83-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="68f83-230">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="68f83-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="68f83-231">Diagnostics: Test whether utilities can connect</span><span class="sxs-lookup"><span data-stu-id="68f83-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="68f83-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span><span class="sxs-lookup"><span data-stu-id="68f83-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="68f83-233">Ideally the utility would connect by using the same library that your program uses.</span><span class="sxs-lookup"><span data-stu-id="68f83-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="68f83-234">On any Windows computer, you can try these utilities:</span><span class="sxs-lookup"><span data-stu-id="68f83-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="68f83-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="68f83-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="68f83-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="68f83-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="68f83-237">Once connected, test whether a short SQL SELECT query works.</span><span class="sxs-lookup"><span data-stu-id="68f83-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="68f83-238">Diagnostics: Check the open ports</span><span class="sxs-lookup"><span data-stu-id="68f83-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="68f83-239">Suppose you suspect that connection attempts are failing due to port issues.</span><span class="sxs-lookup"><span data-stu-id="68f83-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="68f83-240">On your computer you can run a utility that reports on the port configurations.</span><span class="sxs-lookup"><span data-stu-id="68f83-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="68f83-241">On Linux the following utilities might be helpful:</span><span class="sxs-lookup"><span data-stu-id="68f83-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="68f83-242">(Change the example value to be your IP address.)</span><span class="sxs-lookup"><span data-stu-id="68f83-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="68f83-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span><span class="sxs-lookup"><span data-stu-id="68f83-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="68f83-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span><span class="sxs-lookup"><span data-stu-id="68f83-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

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

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="68f83-245">Diagnostics: Log your errors</span><span class="sxs-lookup"><span data-stu-id="68f83-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="68f83-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span><span class="sxs-lookup"><span data-stu-id="68f83-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="68f83-247">Your client can assist in a diagnosis by logging all errors it encounters.</span><span class="sxs-lookup"><span data-stu-id="68f83-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="68f83-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span><span class="sxs-lookup"><span data-stu-id="68f83-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="68f83-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span><span class="sxs-lookup"><span data-stu-id="68f83-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="68f83-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span><span class="sxs-lookup"><span data-stu-id="68f83-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="68f83-251">Diagnostics: Examine system logs for errors</span><span class="sxs-lookup"><span data-stu-id="68f83-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="68f83-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span><span class="sxs-lookup"><span data-stu-id="68f83-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="68f83-253">Query of log</span><span class="sxs-lookup"><span data-stu-id="68f83-253">Query of log</span></span> | <span data-ttu-id="68f83-254">Description</span><span class="sxs-lookup"><span data-stu-id="68f83-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="68f83-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span><span class="sxs-lookup"><span data-stu-id="68f83-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="68f83-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span><span class="sxs-lookup"><span data-stu-id="68f83-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="68f83-257">**TIP:** You must connect to the **master** database to run this.</span><span class="sxs-lookup"><span data-stu-id="68f83-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="68f83-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span><span class="sxs-lookup"><span data-stu-id="68f83-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="68f83-259">**TIP:** You must connect to the **master** database to run this.</span><span class="sxs-lookup"><span data-stu-id="68f83-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="68f83-260">Diagnostics: Search for problem events in the SQL Database log</span><span class="sxs-lookup"><span data-stu-id="68f83-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="68f83-261">You can search for entries about problem events in the log of Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="68f83-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="68f83-262">Try the following Transact-SQL SELECT statement in the **master** database:</span><span class="sxs-lookup"><span data-stu-id="68f83-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="68f83-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="68f83-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="68f83-264">Next is what a returned row might look like.</span><span class="sxs-lookup"><span data-stu-id="68f83-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="68f83-265">The null values shown are often not null in other rows.</span><span class="sxs-lookup"><span data-stu-id="68f83-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="68f83-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="68f83-266">Enterprise Library 6</span></span>
<span data-ttu-id="68f83-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span><span class="sxs-lookup"><span data-stu-id="68f83-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="68f83-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span><span class="sxs-lookup"><span data-stu-id="68f83-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="68f83-269">Enterprise Library 6 - April 2013</span><span class="sxs-lookup"><span data-stu-id="68f83-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="68f83-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span><span class="sxs-lookup"><span data-stu-id="68f83-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="68f83-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span><span class="sxs-lookup"><span data-stu-id="68f83-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="68f83-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="68f83-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="68f83-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span><span class="sxs-lookup"><span data-stu-id="68f83-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="68f83-274">EntLib60 classes for transient errors and retry</span><span class="sxs-lookup"><span data-stu-id="68f83-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="68f83-275">The following EntLib60 classes are particularly useful for retry logic.</span><span class="sxs-lookup"><span data-stu-id="68f83-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="68f83-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="68f83-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="68f83-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="68f83-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="68f83-278">**RetryPolicy** class</span><span class="sxs-lookup"><span data-stu-id="68f83-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="68f83-279">**ExecuteAction** method</span><span class="sxs-lookup"><span data-stu-id="68f83-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="68f83-280">**ExponentialBackoff** class</span><span class="sxs-lookup"><span data-stu-id="68f83-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="68f83-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span><span class="sxs-lookup"><span data-stu-id="68f83-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="68f83-282">**ReliableSqlConnection** class</span><span class="sxs-lookup"><span data-stu-id="68f83-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="68f83-283">**ExecuteCommand** method</span><span class="sxs-lookup"><span data-stu-id="68f83-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="68f83-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="68f83-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="68f83-285">**AlwaysTransientErrorDetectionStrategy** class</span><span class="sxs-lookup"><span data-stu-id="68f83-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="68f83-286">**NeverTransientErrorDetectionStrategy** class</span><span class="sxs-lookup"><span data-stu-id="68f83-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="68f83-287">Here are links to information about EntLib60:</span><span class="sxs-lookup"><span data-stu-id="68f83-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="68f83-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="68f83-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="68f83-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span><span class="sxs-lookup"><span data-stu-id="68f83-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="68f83-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="68f83-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="68f83-291">EntLib60: The logging block</span><span class="sxs-lookup"><span data-stu-id="68f83-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="68f83-292">The Logging block is a highly flexible and configurable solution that allows you to:</span><span class="sxs-lookup"><span data-stu-id="68f83-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="68f83-293">Create and store log messages in a wide variety of locations.</span><span class="sxs-lookup"><span data-stu-id="68f83-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="68f83-294">Categorize and filter messages.</span><span class="sxs-lookup"><span data-stu-id="68f83-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="68f83-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span><span class="sxs-lookup"><span data-stu-id="68f83-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="68f83-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span><span class="sxs-lookup"><span data-stu-id="68f83-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="68f83-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="68f83-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="68f83-298">EntLib60 IsTransient method source code</span><span class="sxs-lookup"><span data-stu-id="68f83-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="68f83-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span><span class="sxs-lookup"><span data-stu-id="68f83-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="68f83-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span><span class="sxs-lookup"><span data-stu-id="68f83-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="68f83-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span><span class="sxs-lookup"><span data-stu-id="68f83-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
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


## <a name="next-steps"></a><span data-ttu-id="68f83-302">Next steps</span><span class="sxs-lookup"><span data-stu-id="68f83-302">Next steps</span></span>
* <span data-ttu-id="68f83-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="68f83-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="68f83-304">SQL Server Connection Pooling (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="68f83-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="68f83-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span><span class="sxs-lookup"><span data-stu-id="68f83-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)

