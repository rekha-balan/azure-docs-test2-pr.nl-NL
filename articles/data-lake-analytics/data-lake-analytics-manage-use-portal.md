---
title: Manage Azure Data Lake Analytics by using the Azure portal
description: This article describes how to use the Azure portal to manage Data Lake Analytics accounts, data sources, users, & jobs.
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.topic: conceptual
ms.date: 12/05/2016
ms.openlocfilehash: 1d49403ec04b2ec35291869385c316cb5ab3b0da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776236"
---
# <a name="manage-azure-data-lake-analytics-using-the-azure-portal"></a><span data-ttu-id="85853-103">Manage Azure Data Lake Analytics using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="85853-103">Manage Azure Data Lake Analytics using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="85853-104">This article describes how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85853-104">This article describes how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs by using the Azure portal.</span></span>


<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="85853-105">Manage Data Lake Analytics accounts</span><span class="sxs-lookup"><span data-stu-id="85853-105">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="85853-106">Create an account</span><span class="sxs-lookup"><span data-stu-id="85853-106">Create an account</span></span>

1. <span data-ttu-id="85853-107">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85853-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="85853-108">Click **Create a resource** > **Intelligence + analytics** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="85853-108">Click **Create a resource** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="85853-109">Select values for the following items:</span><span class="sxs-lookup"><span data-stu-id="85853-109">Select values for the following items:</span></span> 
   1. <span data-ttu-id="85853-110">**Name**: The name of the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-110">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="85853-111">**Subscription**: The Azure subscription used for the account.</span><span class="sxs-lookup"><span data-stu-id="85853-111">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="85853-112">**Resource Group**: The Azure resource group in which to create the account.</span><span class="sxs-lookup"><span data-stu-id="85853-112">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="85853-113">**Location**: The Azure datacenter for the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-113">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="85853-114">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-114">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="85853-115">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span><span class="sxs-lookup"><span data-stu-id="85853-115">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="85853-116">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="85853-116">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="85853-117">Delete a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="85853-117">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="85853-118">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="85853-118">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="85853-119">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-119">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="85853-120">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="85853-120">Click **Delete**.</span></span>
3. <span data-ttu-id="85853-121">Type the account name.</span><span class="sxs-lookup"><span data-stu-id="85853-121">Type the account name.</span></span>
4. <span data-ttu-id="85853-122">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="85853-122">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="85853-123">Manage data sources</span><span class="sxs-lookup"><span data-stu-id="85853-123">Manage data sources</span></span>

<span data-ttu-id="85853-124">Data Lake Analytics supports the following data sources:</span><span class="sxs-lookup"><span data-stu-id="85853-124">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="85853-125">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="85853-125">Data Lake Store</span></span>
* <span data-ttu-id="85853-126">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="85853-126">Azure Storage</span></span>

<span data-ttu-id="85853-127">You can use Data Explorer to browse data sources and perform basic file management operations.</span><span class="sxs-lookup"><span data-stu-id="85853-127">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="85853-128">Add a data source</span><span class="sxs-lookup"><span data-stu-id="85853-128">Add a data source</span></span>

1. <span data-ttu-id="85853-129">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-129">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="85853-130">Click **Data Sources**.</span><span class="sxs-lookup"><span data-stu-id="85853-130">Click **Data Sources**.</span></span>
3. <span data-ttu-id="85853-131">Click **Add Data Source**.</span><span class="sxs-lookup"><span data-stu-id="85853-131">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="85853-132">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span><span class="sxs-lookup"><span data-stu-id="85853-132">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="85853-133">To add Azure Blob storage, you need the storage account and the account key.</span><span class="sxs-lookup"><span data-stu-id="85853-133">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="85853-134">To find them, go to the storage account in the portal.</span><span class="sxs-lookup"><span data-stu-id="85853-134">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="85853-135">Set up firewall rules</span><span class="sxs-lookup"><span data-stu-id="85853-135">Set up firewall rules</span></span>

<span data-ttu-id="85853-136">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span><span class="sxs-lookup"><span data-stu-id="85853-136">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="85853-137">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span><span class="sxs-lookup"><span data-stu-id="85853-137">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="85853-138">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span><span class="sxs-lookup"><span data-stu-id="85853-138">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="85853-139">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span><span class="sxs-lookup"><span data-stu-id="85853-139">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="85853-140">Set up a firewall rule</span><span class="sxs-lookup"><span data-stu-id="85853-140">Set up a firewall rule</span></span>

1. <span data-ttu-id="85853-141">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-141">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="85853-142">On the menu on the left, click **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="85853-142">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="85853-143">Add a new user</span><span class="sxs-lookup"><span data-stu-id="85853-143">Add a new user</span></span>

<span data-ttu-id="85853-144">You can use the **Add User Wizard** to easily provision new Data Lake users.</span><span class="sxs-lookup"><span data-stu-id="85853-144">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="85853-145">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-145">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="85853-146">On the left, under **Getting Started**, click **Add User Wizard**.</span><span class="sxs-lookup"><span data-stu-id="85853-146">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="85853-147">Select a user, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="85853-147">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="85853-148">Select a role, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="85853-148">Select a role, and then click **Select**.</span></span> <span data-ttu-id="85853-149">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span><span class="sxs-lookup"><span data-stu-id="85853-149">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="85853-150">Select the access control lists (ACLs) for the U-SQL databases.</span><span class="sxs-lookup"><span data-stu-id="85853-150">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="85853-151">When you're satisfied with your choices, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="85853-151">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="85853-152">Select the ACLs for files.</span><span class="sxs-lookup"><span data-stu-id="85853-152">Select the ACLs for files.</span></span> <span data-ttu-id="85853-153">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span><span class="sxs-lookup"><span data-stu-id="85853-153">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="85853-154">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="85853-154">Click **Select**.</span></span>
7. <span data-ttu-id="85853-155">Review all your selected changes, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="85853-155">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="85853-156">When the wizard is finished, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="85853-156">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="85853-157">Manage Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="85853-157">Manage Role-Based Access Control</span></span>

<span data-ttu-id="85853-158">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span><span class="sxs-lookup"><span data-stu-id="85853-158">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="85853-159">The standard RBAC roles have the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="85853-159">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="85853-160">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span><span class="sxs-lookup"><span data-stu-id="85853-160">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="85853-161">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span><span class="sxs-lookup"><span data-stu-id="85853-161">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="85853-162">**Reader**: Can monitor jobs.</span><span class="sxs-lookup"><span data-stu-id="85853-162">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="85853-163">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="85853-163">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="85853-164">You can use the Data Lake Analytics Developer role to:</span><span class="sxs-lookup"><span data-stu-id="85853-164">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="85853-165">Submit jobs.</span><span class="sxs-lookup"><span data-stu-id="85853-165">Submit jobs.</span></span>
* <span data-ttu-id="85853-166">Monitor job status and the progress of jobs submitted by any user.</span><span class="sxs-lookup"><span data-stu-id="85853-166">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="85853-167">See the U-SQL scripts from jobs submitted by any user.</span><span class="sxs-lookup"><span data-stu-id="85853-167">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="85853-168">Cancel only your own jobs.</span><span class="sxs-lookup"><span data-stu-id="85853-168">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="85853-169">Add users or security groups to a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="85853-169">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="85853-170">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-170">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="85853-171">Click **Access control (IAM)** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="85853-171">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="85853-172">Select a role.</span><span class="sxs-lookup"><span data-stu-id="85853-172">Select a role.</span></span>
4. <span data-ttu-id="85853-173">Add a user.</span><span class="sxs-lookup"><span data-stu-id="85853-173">Add a user.</span></span>
5. <span data-ttu-id="85853-174">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="85853-174">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="85853-175">If a user or a security group needs to submit jobs, they also need permission on the store account.</span><span class="sxs-lookup"><span data-stu-id="85853-175">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="85853-176">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="85853-176">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="85853-177">Manage jobs</span><span class="sxs-lookup"><span data-stu-id="85853-177">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="85853-178">Submit a job</span><span class="sxs-lookup"><span data-stu-id="85853-178">Submit a job</span></span>

1. <span data-ttu-id="85853-179">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-179">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="85853-180">Click **New Job**.</span><span class="sxs-lookup"><span data-stu-id="85853-180">Click **New Job**.</span></span> <span data-ttu-id="85853-181">For each job,  configure:</span><span class="sxs-lookup"><span data-stu-id="85853-181">For each job,  configure:</span></span>

    1. <span data-ttu-id="85853-182">**Job Name**: The name of the job.</span><span class="sxs-lookup"><span data-stu-id="85853-182">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="85853-183">**Priority**: Lower numbers have higher priority.</span><span class="sxs-lookup"><span data-stu-id="85853-183">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="85853-184">If two jobs are queued, the one with lower priority value runs first.</span><span class="sxs-lookup"><span data-stu-id="85853-184">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="85853-185">**Parallelism**: The maximum number of compute processes to reserve for this job.</span><span class="sxs-lookup"><span data-stu-id="85853-185">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="85853-186">Click **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="85853-186">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="85853-187">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="85853-187">Monitor jobs</span></span>

1. <span data-ttu-id="85853-188">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="85853-188">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="85853-189">Click **View All Jobs**.</span><span class="sxs-lookup"><span data-stu-id="85853-189">Click **View All Jobs**.</span></span> <span data-ttu-id="85853-190">A list of all the active and recently finished jobs in the account is shown.</span><span class="sxs-lookup"><span data-stu-id="85853-190">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="85853-191">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span><span class="sxs-lookup"><span data-stu-id="85853-191">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="85853-192">Monitoring pipeline jobs</span><span class="sxs-lookup"><span data-stu-id="85853-192">Monitoring pipeline jobs</span></span>
<span data-ttu-id="85853-193">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span><span class="sxs-lookup"><span data-stu-id="85853-193">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="85853-194">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span><span class="sxs-lookup"><span data-stu-id="85853-194">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="85853-195">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span><span class="sxs-lookup"><span data-stu-id="85853-195">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="85853-196">Jobs scheduled using ADF V2 will automatically have this property populated.</span><span class="sxs-lookup"><span data-stu-id="85853-196">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="85853-197">To view a list of U-SQL jobs that are part of pipelines:</span><span class="sxs-lookup"><span data-stu-id="85853-197">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="85853-198">In the Azure portal, go to your Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="85853-198">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="85853-199">Click **Job Insights**.</span><span class="sxs-lookup"><span data-stu-id="85853-199">Click **Job Insights**.</span></span> <span data-ttu-id="85853-200">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span><span class="sxs-lookup"><span data-stu-id="85853-200">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="85853-201">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span><span class="sxs-lookup"><span data-stu-id="85853-201">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="85853-202">Monitoring recurring jobs</span><span class="sxs-lookup"><span data-stu-id="85853-202">Monitoring recurring jobs</span></span>
<span data-ttu-id="85853-203">A recurring job is one that has the same business logic but uses different input data every time it runs.</span><span class="sxs-lookup"><span data-stu-id="85853-203">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="85853-204">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span><span class="sxs-lookup"><span data-stu-id="85853-204">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="85853-205">Recurring jobs are identified using the "Recurrence" property.</span><span class="sxs-lookup"><span data-stu-id="85853-205">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="85853-206">Jobs scheduled using ADF V2 will automatically have this property populated.</span><span class="sxs-lookup"><span data-stu-id="85853-206">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="85853-207">To view a list of U-SQL jobs that are recurring:</span><span class="sxs-lookup"><span data-stu-id="85853-207">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="85853-208">In the Azure portal, go to your Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="85853-208">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="85853-209">Click **Job Insights**.</span><span class="sxs-lookup"><span data-stu-id="85853-209">Click **Job Insights**.</span></span> <span data-ttu-id="85853-210">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span><span class="sxs-lookup"><span data-stu-id="85853-210">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="85853-211">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span><span class="sxs-lookup"><span data-stu-id="85853-211">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85853-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="85853-212">Next steps</span></span>

* [<span data-ttu-id="85853-213">Overview of Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="85853-213">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="85853-214">Manage Azure Data Lake Analytics by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="85853-214">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="85853-215">Manage Azure Data Lake Analytics using policies</span><span class="sxs-lookup"><span data-stu-id="85853-215">Manage Azure Data Lake Analytics using policies</span></span>](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-policies)
