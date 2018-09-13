---
title: 'Stream Analytics: Rotate log-in credentials for inputs and outputs | Microsoft Docs'
description: Learn how to update the credentials for Stream Analytics inputs and outputs.
keywords: login credentials
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d6b0d6b0d319e5a1e4716c6c239d7d196c0cd386
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554711"
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="48bc0-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span><span class="sxs-lookup"><span data-stu-id="48bc0-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="48bc0-105">Abstract</span><span class="sxs-lookup"><span data-stu-id="48bc0-105">Abstract</span></span>
<span data-ttu-id="48bc0-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span><span class="sxs-lookup"><span data-stu-id="48bc0-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="48bc0-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span><span class="sxs-lookup"><span data-stu-id="48bc0-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="48bc0-108">Part 1 - Prepare the new set of credentials:</span><span class="sxs-lookup"><span data-stu-id="48bc0-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="48bc0-109">This part is applicable to the following inputs/outputs:</span><span class="sxs-lookup"><span data-stu-id="48bc0-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="48bc0-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-110">Blob Storage</span></span>
* <span data-ttu-id="48bc0-111">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="48bc0-111">Event Hubs</span></span>
* <span data-ttu-id="48bc0-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="48bc0-112">SQL Database</span></span>
* <span data-ttu-id="48bc0-113">Table Storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-113">Table Storage</span></span>

<span data-ttu-id="48bc0-114">For other inputs/outputs, proceed with Part 2.</span><span class="sxs-lookup"><span data-stu-id="48bc0-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="48bc0-115">Blob storage/Table storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="48bc0-116">Go to the Storage extention on the Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="48bc0-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="48bc0-118">Locate the storage used by your job and go into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="48bc0-120">Click the Manage Access Keys command:</span><span class="sxs-lookup"><span data-stu-id="48bc0-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="48bc0-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span><span class="sxs-lookup"><span data-stu-id="48bc0-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="48bc0-123">Hit regenerate:</span><span class="sxs-lookup"><span data-stu-id="48bc0-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="48bc0-125">Copy the newly generated key:</span><span class="sxs-lookup"><span data-stu-id="48bc0-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="48bc0-127">Continue to Part 2.</span><span class="sxs-lookup"><span data-stu-id="48bc0-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="48bc0-128">Event hubs</span><span class="sxs-lookup"><span data-stu-id="48bc0-128">Event hubs</span></span>
1. <span data-ttu-id="48bc0-129">Go to the Service Bus extension on the Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="48bc0-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="48bc0-131">Locate the Service Bus Namespace used by your job and go into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="48bc0-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span><span class="sxs-lookup"><span data-stu-id="48bc0-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="48bc0-134">Go to the Event Hubs tab:</span><span class="sxs-lookup"><span data-stu-id="48bc0-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="48bc0-136">Locate the Event Hub used by your job and go into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="48bc0-138">Go to the Configure Tab:</span><span class="sxs-lookup"><span data-stu-id="48bc0-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="48bc0-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span><span class="sxs-lookup"><span data-stu-id="48bc0-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="48bc0-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span><span class="sxs-lookup"><span data-stu-id="48bc0-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="48bc0-143">Hit regenerate:</span><span class="sxs-lookup"><span data-stu-id="48bc0-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="48bc0-145">Copy the newly generated key:</span><span class="sxs-lookup"><span data-stu-id="48bc0-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="48bc0-147">Continue to Part 2.</span><span class="sxs-lookup"><span data-stu-id="48bc0-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="48bc0-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="48bc0-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="48bc0-149">Note: you will need to connect to the SQL Database Service.</span><span class="sxs-lookup"><span data-stu-id="48bc0-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="48bc0-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span><span class="sxs-lookup"><span data-stu-id="48bc0-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="48bc0-151">Go to the SQL Databases extension on the Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="48bc0-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="48bc0-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span><span class="sxs-lookup"><span data-stu-id="48bc0-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="48bc0-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="48bc0-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="48bc0-155">Click the Manage command:</span><span class="sxs-lookup"><span data-stu-id="48bc0-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="48bc0-157">Type Database Master:</span><span class="sxs-lookup"><span data-stu-id="48bc0-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="48bc0-159">Type in your User Name, Password, and click Log on:</span><span class="sxs-lookup"><span data-stu-id="48bc0-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="48bc0-161">Click New Query:</span><span class="sxs-lookup"><span data-stu-id="48bc0-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="48bc0-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span><span class="sxs-lookup"><span data-stu-id="48bc0-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="48bc0-164">Click Run:</span><span class="sxs-lookup"><span data-stu-id="48bc0-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="48bc0-166">Go back to step 2 and this time click the database:</span><span class="sxs-lookup"><span data-stu-id="48bc0-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="48bc0-168">Click the Manage command:</span><span class="sxs-lookup"><span data-stu-id="48bc0-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="48bc0-170">type in your User Name, Password, and click Logon:</span><span class="sxs-lookup"><span data-stu-id="48bc0-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="48bc0-172">Click New Query:</span><span class="sxs-lookup"><span data-stu-id="48bc0-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="48bc0-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span><span class="sxs-lookup"><span data-stu-id="48bc0-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="48bc0-175">Click Run:</span><span class="sxs-lookup"><span data-stu-id="48bc0-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="48bc0-177">You should now provide your new user with the same roles and privileges your original user had.</span><span class="sxs-lookup"><span data-stu-id="48bc0-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="48bc0-178">Continue to Part 2.</span><span class="sxs-lookup"><span data-stu-id="48bc0-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="48bc0-179">Part 2: Stopping the Stream Analytics Job</span><span class="sxs-lookup"><span data-stu-id="48bc0-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="48bc0-180">Go to the Stream Analytics extension on the Azure Management portal:</span><span class="sxs-lookup"><span data-stu-id="48bc0-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="48bc0-182">Locate your job and go into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="48bc0-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span><span class="sxs-lookup"><span data-stu-id="48bc0-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="48bc0-186">Click the Stop command and confirm the job has stopped:</span><span class="sxs-lookup"><span data-stu-id="48bc0-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="48bc0-187">![graphic29][graphic29] Wait for the job to stop.</span><span class="sxs-lookup"><span data-stu-id="48bc0-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="48bc0-188">Locate the input/output you want to rotate credentials on and go into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="48bc0-190">Proceed to Part 3.</span><span class="sxs-lookup"><span data-stu-id="48bc0-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="48bc0-191">Part 3: Editing the credentials on the Stream Analytics Job</span><span class="sxs-lookup"><span data-stu-id="48bc0-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="48bc0-192">Blob storage/Table storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="48bc0-193">Find the Storage Account Key field and paste your newly generated key into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="48bc0-195">Click the Save command and confirm saving your changes:</span><span class="sxs-lookup"><span data-stu-id="48bc0-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="48bc0-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span><span class="sxs-lookup"><span data-stu-id="48bc0-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="48bc0-198">Proceed to Part 4.</span><span class="sxs-lookup"><span data-stu-id="48bc0-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="48bc0-199">Event hubs</span><span class="sxs-lookup"><span data-stu-id="48bc0-199">Event hubs</span></span>
1. <span data-ttu-id="48bc0-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span><span class="sxs-lookup"><span data-stu-id="48bc0-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="48bc0-202">Click the Save command and confirm saving your changes:</span><span class="sxs-lookup"><span data-stu-id="48bc0-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="48bc0-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span><span class="sxs-lookup"><span data-stu-id="48bc0-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="48bc0-205">Proceed to Part 4.</span><span class="sxs-lookup"><span data-stu-id="48bc0-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="48bc0-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="48bc0-206">Power BI</span></span>
1. <span data-ttu-id="48bc0-207">Click the Renew authorization:</span><span class="sxs-lookup"><span data-stu-id="48bc0-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="48bc0-209">You will get the following confirmation:</span><span class="sxs-lookup"><span data-stu-id="48bc0-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="48bc0-211">Click the Save command and confirm saving your changes:</span><span class="sxs-lookup"><span data-stu-id="48bc0-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="48bc0-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span><span class="sxs-lookup"><span data-stu-id="48bc0-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="48bc0-214">Proceed to Part 4.</span><span class="sxs-lookup"><span data-stu-id="48bc0-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="48bc0-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="48bc0-215">SQL Database</span></span>
1. <span data-ttu-id="48bc0-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span><span class="sxs-lookup"><span data-stu-id="48bc0-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="48bc0-218">Click the Save command and confirm saving your changes:</span><span class="sxs-lookup"><span data-stu-id="48bc0-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="48bc0-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span><span class="sxs-lookup"><span data-stu-id="48bc0-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="48bc0-221">Proceed to Part 4.</span><span class="sxs-lookup"><span data-stu-id="48bc0-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="48bc0-222">Part 4: Starting your job from last stopped time</span><span class="sxs-lookup"><span data-stu-id="48bc0-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="48bc0-223">Navigate away from the Input/Output:</span><span class="sxs-lookup"><span data-stu-id="48bc0-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="48bc0-225">Click the Start command:</span><span class="sxs-lookup"><span data-stu-id="48bc0-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="48bc0-227">Pick the Last Stopped Time and click OK:</span><span class="sxs-lookup"><span data-stu-id="48bc0-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="48bc0-229">Proceed to Part 5.</span><span class="sxs-lookup"><span data-stu-id="48bc0-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="48bc0-230">Part 5: Removing the old set of credentials</span><span class="sxs-lookup"><span data-stu-id="48bc0-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="48bc0-231">This part is applicable to the following inputs/outputs:</span><span class="sxs-lookup"><span data-stu-id="48bc0-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="48bc0-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-232">Blob Storage</span></span>
* <span data-ttu-id="48bc0-233">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="48bc0-233">Event Hubs</span></span>
* <span data-ttu-id="48bc0-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="48bc0-234">SQL Database</span></span>
* <span data-ttu-id="48bc0-235">Table Storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="48bc0-236">Blob storage/Table storage</span><span class="sxs-lookup"><span data-stu-id="48bc0-236">Blob storage/Table storage</span></span>
<span data-ttu-id="48bc0-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span><span class="sxs-lookup"><span data-stu-id="48bc0-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="48bc0-238">Event hubs</span><span class="sxs-lookup"><span data-stu-id="48bc0-238">Event hubs</span></span>
<span data-ttu-id="48bc0-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span><span class="sxs-lookup"><span data-stu-id="48bc0-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="48bc0-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="48bc0-240">SQL Database</span></span>
1. <span data-ttu-id="48bc0-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span><span class="sxs-lookup"><span data-stu-id="48bc0-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="48bc0-242">Click Run:</span><span class="sxs-lookup"><span data-stu-id="48bc0-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="48bc0-244">You should get the following confirmation:</span><span class="sxs-lookup"><span data-stu-id="48bc0-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="48bc0-245">Get help</span><span class="sxs-lookup"><span data-stu-id="48bc0-245">Get help</span></span>
<span data-ttu-id="48bc0-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="48bc0-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="48bc0-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="48bc0-247">Next steps</span></span>
* [<span data-ttu-id="48bc0-248">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="48bc0-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="48bc0-249">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="48bc0-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="48bc0-250">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="48bc0-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="48bc0-251">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="48bc0-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="48bc0-252">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="48bc0-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png












































