---
title: 'Azure portal: Create & manage a SQL Database elastic pool | Microsoft Docs'
description: Learn how to use the Azure portal and SQL Database's built-in intelligence to manage, monitor, and right-size a scalable elastic pool to optimize database performance and manage cost.
keywords: ''
services: sql-database
documentationcenter: ''
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: multiple databases
ms.devlang: NA
ms.date: 04/18/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 00087ce1a972d0d7204b1d78330c8da7b3067f01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551183"
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="9e15b-103">Create and manage an elastic pool with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9e15b-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="9e15b-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e15b-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="9e15b-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="9e15b-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="9e15b-107">Create an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-107">Create an elastic pool</span></span> 

<span data-ttu-id="9e15b-108">There are two ways you can create an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="9e15b-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span><span class="sxs-lookup"><span data-stu-id="9e15b-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="9e15b-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span><span class="sxs-lookup"><span data-stu-id="9e15b-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="9e15b-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="9e15b-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="9e15b-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="9e15b-113">GA of elastic pools in this region will occur as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="9e15b-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="9e15b-114">Step 1: Create an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="9e15b-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span><span class="sxs-lookup"><span data-stu-id="9e15b-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="9e15b-117">You are able to specify a new or existing server through this pool provisioning workflow.</span><span class="sxs-lookup"><span data-stu-id="9e15b-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="9e15b-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="9e15b-119">Click **New pool**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-119">Click **New pool**.</span></span>

    ![Add pool to a server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="9e15b-121">**-OR-**</span><span class="sxs-lookup"><span data-stu-id="9e15b-121">**-OR-**</span></span>

    <span data-ttu-id="9e15b-122">You may see a message saying there are recommended elastic pools for the server.</span><span class="sxs-lookup"><span data-stu-id="9e15b-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="9e15b-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="9e15b-124">See [Understand pool recommendations](#understand-pool-recommendations) later in this topic for how the recommendation is made.</span><span class="sxs-lookup"><span data-stu-id="9e15b-124">See [Understand pool recommendations](#understand-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![recommended pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="9e15b-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="9e15b-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span><span class="sxs-lookup"><span data-stu-id="9e15b-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="9e15b-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="9e15b-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span><span class="sxs-lookup"><span data-stu-id="9e15b-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configure elastic pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="9e15b-131">Specify a name for the elastic pool, or leave it as the default.</span><span class="sxs-lookup"><span data-stu-id="9e15b-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="9e15b-132">Step 2: Choose a pricing tier</span><span class="sxs-lookup"><span data-stu-id="9e15b-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="9e15b-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span><span class="sxs-lookup"><span data-stu-id="9e15b-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="9e15b-134">For details, see Service Tiers.</span><span class="sxs-lookup"><span data-stu-id="9e15b-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="9e15b-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e15b-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="9e15b-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>
>

![Select a pricing tier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="9e15b-139">Step 3: Configure the pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="9e15b-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="9e15b-141">Click **Configure pool**</span><span class="sxs-lookup"><span data-stu-id="9e15b-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="9e15b-142">Select the databases you want to add to the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="9e15b-143">This step is optional while creating the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="9e15b-144">Databases can be added after the pool has been created.</span><span class="sxs-lookup"><span data-stu-id="9e15b-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="9e15b-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="9e15b-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![Add databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="9e15b-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span><span class="sxs-lookup"><span data-stu-id="9e15b-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="9e15b-148">Also, the service may give you a recommendation message to help you right-size the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="9e15b-149">See [Dynamic Recommendations](#dynamic-recommendations).</span><span class="sxs-lookup"><span data-stu-id="9e15b-149">See [Dynamic Recommendations](#dynamic-recommendations).</span></span>

3. <span data-ttu-id="9e15b-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="9e15b-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="9e15b-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="9e15b-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configure Elastic Pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="9e15b-154">Click **Select** in the **Configure Pool** blade after changing settings.</span><span class="sxs-lookup"><span data-stu-id="9e15b-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="9e15b-155">Click **OK** to create the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="9e15b-156">Understand elastic pool recommendations</span><span class="sxs-lookup"><span data-stu-id="9e15b-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="9e15b-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span><span class="sxs-lookup"><span data-stu-id="9e15b-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="9e15b-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![recommended pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="9e15b-160">The pool recommendation comprises:</span><span class="sxs-lookup"><span data-stu-id="9e15b-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="9e15b-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span><span class="sxs-lookup"><span data-stu-id="9e15b-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="9e15b-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span><span class="sxs-lookup"><span data-stu-id="9e15b-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="9e15b-163">The **eDTU MAX** and **eDTU Min** per database</span><span class="sxs-lookup"><span data-stu-id="9e15b-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="9e15b-164">The list of recommended databases for the pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e15b-165">The service takes the last 30 days of telemetry into account when recommending pools.</span><span class="sxs-lookup"><span data-stu-id="9e15b-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="9e15b-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span><span class="sxs-lookup"><span data-stu-id="9e15b-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="9e15b-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span><span class="sxs-lookup"><span data-stu-id="9e15b-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="9e15b-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span><span class="sxs-lookup"><span data-stu-id="9e15b-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="9e15b-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="9e15b-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="9e15b-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span><span class="sxs-lookup"><span data-stu-id="9e15b-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="9e15b-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span><span class="sxs-lookup"><span data-stu-id="9e15b-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="9e15b-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span><span class="sxs-lookup"><span data-stu-id="9e15b-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![dynamic recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="9e15b-175">Manage and monitor an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="9e15b-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="9e15b-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="9e15b-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span><span class="sxs-lookup"><span data-stu-id="9e15b-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="9e15b-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span><span class="sxs-lookup"><span data-stu-id="9e15b-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="9e15b-180">The following graphic shows an example elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="9e15b-181">The view includes:</span><span class="sxs-lookup"><span data-stu-id="9e15b-181">The view includes:</span></span>

*  <span data-ttu-id="9e15b-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="9e15b-183">The **Configure** pool button to make changes to the elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="9e15b-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="9e15b-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span><span class="sxs-lookup"><span data-stu-id="9e15b-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Pool view][2]

<span data-ttu-id="9e15b-187">You can go to a particular pool to see its resource utilization.</span><span class="sxs-lookup"><span data-stu-id="9e15b-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="9e15b-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span><span class="sxs-lookup"><span data-stu-id="9e15b-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="9e15b-189">The chart can be configured to show different metrics over various time windows.</span><span class="sxs-lookup"><span data-stu-id="9e15b-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="9e15b-190">Select an elastic pool to work with.</span><span class="sxs-lookup"><span data-stu-id="9e15b-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="9e15b-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="9e15b-192">Click the chart.</span><span class="sxs-lookup"><span data-stu-id="9e15b-192">Click the chart.</span></span>

    ![Elastic pool monitoring][3]

    <span data-ttu-id="9e15b-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span><span class="sxs-lookup"><span data-stu-id="9e15b-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![Metric blade][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="9e15b-196">To customize the chart display</span><span class="sxs-lookup"><span data-stu-id="9e15b-196">To customize the chart display</span></span>

<span data-ttu-id="9e15b-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span><span class="sxs-lookup"><span data-stu-id="9e15b-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="9e15b-198">On the metric blade, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-198">On the metric blade, click **Edit**.</span></span>

    ![Click edit][6]

2. <span data-ttu-id="9e15b-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span><span class="sxs-lookup"><span data-stu-id="9e15b-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="9e15b-201">Select the chart type (bar or line), then select the resources to monitor.</span><span class="sxs-lookup"><span data-stu-id="9e15b-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="9e15b-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span><span class="sxs-lookup"><span data-stu-id="9e15b-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="9e15b-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![Click edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/edit-chart.png)

    

3. <span data-ttu-id="9e15b-205">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="9e15b-206">Manage and monitor databases in an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="9e15b-207">Individual databases can also be monitored for potential trouble.</span><span class="sxs-lookup"><span data-stu-id="9e15b-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="9e15b-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span><span class="sxs-lookup"><span data-stu-id="9e15b-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="9e15b-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span><span class="sxs-lookup"><span data-stu-id="9e15b-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="9e15b-210">Click the chart.</span><span class="sxs-lookup"><span data-stu-id="9e15b-210">Click the chart.</span></span>

    ![Elastic pool monitoring][4]

2. <span data-ttu-id="9e15b-212">The **Database Resource Utilization** blade appears.</span><span class="sxs-lookup"><span data-stu-id="9e15b-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="9e15b-213">This provides a detailed view of the database usage in the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="9e15b-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span><span class="sxs-lookup"><span data-stu-id="9e15b-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="9e15b-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![Database resource utilization blade][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="9e15b-217">To customize the view</span><span class="sxs-lookup"><span data-stu-id="9e15b-217">To customize the view</span></span>

1. <span data-ttu-id="9e15b-218">In the **Database resource utilization** blade, click **Edit chart**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Click Edit chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="9e15b-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span><span class="sxs-lookup"><span data-stu-id="9e15b-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![Click Custom](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="9e15b-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span><span class="sxs-lookup"><span data-stu-id="9e15b-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![Edit the chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="9e15b-224">To select databases to monitor</span><span class="sxs-lookup"><span data-stu-id="9e15b-224">To select databases to monitor</span></span>

<span data-ttu-id="9e15b-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span><span class="sxs-lookup"><span data-stu-id="9e15b-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="9e15b-226">Use the checkbox to select the database.</span><span class="sxs-lookup"><span data-stu-id="9e15b-226">Use the checkbox to select the database.</span></span>

![Search for databases to monitor][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="9e15b-228">Add an alert to an elastic pool resource</span><span class="sxs-lookup"><span data-stu-id="9e15b-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="9e15b-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span><span class="sxs-lookup"><span data-stu-id="9e15b-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e15b-230">Resource utilization monitoring for elastic pools has a lag of at least 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-230">Resource utilization monitoring for elastic pools has a lag of at least 20 minutes.</span></span> <span data-ttu-id="9e15b-231">Setting alerts of less than 30 minutes for elastic pools is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="9e15b-231">Setting alerts of less than 30 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="9e15b-232">Any alerts set for Elastic Pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered.</span><span class="sxs-lookup"><span data-stu-id="9e15b-232">Any alerts set for Elastic Pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 30 minutes may not be triggered.</span></span> <span data-ttu-id="9e15b-233">Make sure that any alerts you define for Elastic Pools use a period (WindowSize) of 30 minutes or more.</span><span class="sxs-lookup"><span data-stu-id="9e15b-233">Make sure that any alerts you define for Elastic Pools use a period (WindowSize) of 30 minutes or more.</span></span>
>
>

<span data-ttu-id="9e15b-234">**To add an alert to any resource:**</span><span class="sxs-lookup"><span data-stu-id="9e15b-234">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="9e15b-235">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span><span class="sxs-lookup"><span data-stu-id="9e15b-235">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="9e15b-236">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span><span class="sxs-lookup"><span data-stu-id="9e15b-236">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="9e15b-237">Choose a **Metric** that you want to alert from the list.</span><span class="sxs-lookup"><span data-stu-id="9e15b-237">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="9e15b-238">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span><span class="sxs-lookup"><span data-stu-id="9e15b-238">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="9e15b-239">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-239">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="9e15b-240">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-240">Click **OK**.</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="9e15b-241">Move a database into an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-241">Move a database into an elastic pool</span></span>

<span data-ttu-id="9e15b-242">You can add or remove databases from an existing pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-242">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="9e15b-243">The databases can be in other pools.</span><span class="sxs-lookup"><span data-stu-id="9e15b-243">The databases can be in other pools.</span></span> <span data-ttu-id="9e15b-244">However, you can only add databases that are on the same logical server.</span><span class="sxs-lookup"><span data-stu-id="9e15b-244">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="9e15b-245">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-245">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Click Configure pool][1]

2. <span data-ttu-id="9e15b-247">In the **Configure pool** blade, click **Add to pool**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-247">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![Click Add to pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="9e15b-249">In the **Add databases** blade, select the database or databases to add to the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-249">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="9e15b-250">Then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-250">Then click **Select**.</span></span>

    ![Select databases to add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="9e15b-252">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-252">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![Pending pool additions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="9e15b-254">In the **Configure pool blade**, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-254">In the **Configure pool blade**, click **Save**.</span></span>

    ![Click Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="9e15b-256">Move a database out of an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-256">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="9e15b-257">In the **Configure pool** blade, select the database or databases to remove.</span><span class="sxs-lookup"><span data-stu-id="9e15b-257">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![databases listing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="9e15b-259">Click **Remove from pool**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-259">Click **Remove from pool**.</span></span>

    ![databases listing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="9e15b-261">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-261">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![preview database addition and removal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="9e15b-263">In the **Configure pool blade**, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-263">In the **Configure pool blade**, click **Save**.</span></span>

    ![Click Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="9e15b-265">Change performance settings of an elastic pool</span><span class="sxs-lookup"><span data-stu-id="9e15b-265">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="9e15b-266">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span><span class="sxs-lookup"><span data-stu-id="9e15b-266">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="9e15b-267">Maybe the pool needs a change in the performance or storage limits.</span><span class="sxs-lookup"><span data-stu-id="9e15b-267">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="9e15b-268">Possibly you want to change the database settings in the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-268">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="9e15b-269">You can change the setup of the pool at any time to get the best balance of performance and cost.</span><span class="sxs-lookup"><span data-stu-id="9e15b-269">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="9e15b-270">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="9e15b-270">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="9e15b-271">To change the eDTUs or storage limits per pool, and eDTUs per database:</span><span class="sxs-lookup"><span data-stu-id="9e15b-271">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="9e15b-272">Open the **Configure pool** blade.</span><span class="sxs-lookup"><span data-stu-id="9e15b-272">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="9e15b-273">Under **elastic pool settings**, use either slider to change the pool settings.</span><span class="sxs-lookup"><span data-stu-id="9e15b-273">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![Elastic pool resource utilization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="9e15b-275">When the setting changes, the display shows the estimated monthly cost of the change.</span><span class="sxs-lookup"><span data-stu-id="9e15b-275">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![Updating an elastic pool and new monthly cost](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="9e15b-277">Latency of elastic pool operations</span><span class="sxs-lookup"><span data-stu-id="9e15b-277">Latency of elastic pool operations</span></span>
* <span data-ttu-id="9e15b-278">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span><span class="sxs-lookup"><span data-stu-id="9e15b-278">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="9e15b-279">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="9e15b-279">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="9e15b-280">Changes average 90 minutes or less per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="9e15b-280">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="9e15b-281">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span><span class="sxs-lookup"><span data-stu-id="9e15b-281">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e15b-282">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e15b-282">Next steps</span></span>

- <span data-ttu-id="9e15b-283">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-283">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="9e15b-284">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-284">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="9e15b-285">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-285">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="9e15b-286">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-286">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="9e15b-287">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e15b-287">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/basic.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-pool-manage-portal/metric.png































