---
title: Provision throughput for Azure Cosmos DB | Microsoft Docs
description: Learn  how to set provisioned throughput for your Azure Cosmos DB containsers, collections, graphs, and tables.
services: cosmos-db
author: aliuy
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: andrl
ms.openlocfilehash: 2c3e4806aef506ef9016699b46eadd5f8a187224
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869415"
---
# <a name="set-and-get-throughput-for-azure-cosmos-db-containers-and-database"></a><span data-ttu-id="1948c-103">Set and get throughput for Azure Cosmos DB containers and database</span><span class="sxs-lookup"><span data-stu-id="1948c-103">Set and get throughput for Azure Cosmos DB containers and database</span></span>

<span data-ttu-id="1948c-104">You can set throughput for an Azure Cosmos DB container or a set of containers by using Azure portal or by using the client SDKs.</span><span class="sxs-lookup"><span data-stu-id="1948c-104">You can set throughput for an Azure Cosmos DB container or a set of containers by using Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="1948c-105">**Provision throughput for an individual container:** When you provision throughput for a set of containers, all those containers share the provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-105">**Provision throughput for an individual container:** When you provision throughput for a set of containers, all those containers share the provisioned throughput.</span></span> <span data-ttu-id="1948c-106">Provisioning throughput for individual containers will guarantee the reservation of throughput for that specific container.</span><span class="sxs-lookup"><span data-stu-id="1948c-106">Provisioning throughput for individual containers will guarantee the reservation of throughput for that specific container.</span></span> <span data-ttu-id="1948c-107">When assigning RU/sec at the individual container level, the containers can be created as *fixed* or *unlimited*.</span><span class="sxs-lookup"><span data-stu-id="1948c-107">When assigning RU/sec at the individual container level, the containers can be created as *fixed* or *unlimited*.</span></span> <span data-ttu-id="1948c-108">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-108">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span></span> <span data-ttu-id="1948c-109">To create an unlimited container, you must specify a minimum throughput of 1,000 RU/s and a [partition key](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="1948c-109">To create an unlimited container, you must specify a minimum throughput of 1,000 RU/s and a [partition key](partition-data.md).</span></span> <span data-ttu-id="1948c-110">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values).</span><span class="sxs-lookup"><span data-stu-id="1948c-110">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values).</span></span> <span data-ttu-id="1948c-111">By selecting a partition key with many distinct values, you ensure that your container/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1948c-111">By selecting a partition key with many distinct values, you ensure that your container/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

<span data-ttu-id="1948c-112">**Provision throughput for a set of containers or a database:** Provisioning throughput for a database allows you to share the throughput among all the containers that belong to that database.</span><span class="sxs-lookup"><span data-stu-id="1948c-112">**Provision throughput for a set of containers or a database:** Provisioning throughput for a database allows you to share the throughput among all the containers that belong to that database.</span></span> <span data-ttu-id="1948c-113">Within an Azure Cosmos DB database, you can have a set of containers which shares the throughput as well as containers, which have dedicated throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-113">Within an Azure Cosmos DB database, you can have a set of containers which shares the throughput as well as containers, which have dedicated throughput.</span></span> <span data-ttu-id="1948c-114">When assigning RU/sec across a set of containers, the containers belonging to this set are treated as *unlimited* containers and must specify a partition key.</span><span class="sxs-lookup"><span data-stu-id="1948c-114">When assigning RU/sec across a set of containers, the containers belonging to this set are treated as *unlimited* containers and must specify a partition key.</span></span>

<span data-ttu-id="1948c-115">Based on the provisioned throughput, Azure Cosmos DB will allocate physical partitions to host your container(s) and splits/rebalances data across partitions as it grows.</span><span class="sxs-lookup"><span data-stu-id="1948c-115">Based on the provisioned throughput, Azure Cosmos DB will allocate physical partitions to host your container(s) and splits/rebalances data across partitions as it grows.</span></span> <span data-ttu-id="1948c-116">Container and database level throughput provisioning are separate offerings and switching between either of these require migrating data from source to destination.</span><span class="sxs-lookup"><span data-stu-id="1948c-116">Container and database level throughput provisioning are separate offerings and switching between either of these require migrating data from source to destination.</span></span> <span data-ttu-id="1948c-117">Which means you need to create a new database or a new collection and then migrate data by using [bulk executor library](bulk-executor-overview.md) or [Azure Data Factory](../data-factory/connector-azure-cosmos-db.md).</span><span class="sxs-lookup"><span data-stu-id="1948c-117">Which means you need to create a new database or a new collection and then migrate data by using [bulk executor library](bulk-executor-overview.md) or [Azure Data Factory](../data-factory/connector-azure-cosmos-db.md).</span></span> <span data-ttu-id="1948c-118">The following image illustrates provisioning throughput at different levels:</span><span class="sxs-lookup"><span data-stu-id="1948c-118">The following image illustrates provisioning throughput at different levels:</span></span>

![Provisioning request units for individual containers and set of containers](./media/request-units/provisioning_set_containers.png)

<span data-ttu-id="1948c-120">In the next sections, you will learn the steps required to configure throughput at different levels for an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="1948c-120">In the next sections, you will learn the steps required to configure throughput at different levels for an Azure Cosmos DB account.</span></span> 

## <a name="provision-throughput-by-using-azure-portal"></a><span data-ttu-id="1948c-121">Provision throughput by using Azure portal</span><span class="sxs-lookup"><span data-stu-id="1948c-121">Provision throughput by using Azure portal</span></span>

### <a name="provision-throughput-for-a-container-collectiongraphtable"></a><span data-ttu-id="1948c-122">Provision throughput for a container (collection/graph/table)</span><span class="sxs-lookup"><span data-stu-id="1948c-122">Provision throughput for a container (collection/graph/table)</span></span>

1. <span data-ttu-id="1948c-123">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1948c-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="1948c-124">From the left nav, select **All resources** and find your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="1948c-124">From the left nav, select **All resources** and find your Azure Cosmos DB account.</span></span>  
3. <span data-ttu-id="1948c-125">You can configure throughput while creating a container (collection, graph, table) or update throughput for an existing container.</span><span class="sxs-lookup"><span data-stu-id="1948c-125">You can configure throughput while creating a container (collection, graph, table) or update throughput for an existing container.</span></span>  
4. <span data-ttu-id="1948c-126">To assign throughput while creating a container, open the **Data Explorer** blade and select **New Collection** (New Graph, New Table for other APIs)</span><span class="sxs-lookup"><span data-stu-id="1948c-126">To assign throughput while creating a container, open the **Data Explorer** blade and select **New Collection** (New Graph, New Table for other APIs)</span></span>  
5. <span data-ttu-id="1948c-127">Fill the form in **Add Collection** blade.</span><span class="sxs-lookup"><span data-stu-id="1948c-127">Fill the form in **Add Collection** blade.</span></span> <span data-ttu-id="1948c-128">Fields in this blade are described in the following table:</span><span class="sxs-lookup"><span data-stu-id="1948c-128">Fields in this blade are described in the following table:</span></span>  

   |<span data-ttu-id="1948c-129">**Setting**</span><span class="sxs-lookup"><span data-stu-id="1948c-129">**Setting**</span></span>  |<span data-ttu-id="1948c-130">**Description**</span><span class="sxs-lookup"><span data-stu-id="1948c-130">**Description**</span></span>  |
   |---------|---------|
   |<span data-ttu-id="1948c-131">Database id</span><span class="sxs-lookup"><span data-stu-id="1948c-131">Database id</span></span>  |  <span data-ttu-id="1948c-132">Provide a unique name to identify your database.</span><span class="sxs-lookup"><span data-stu-id="1948c-132">Provide a unique name to identify your database.</span></span> <span data-ttu-id="1948c-133">Database is a logical container of one or more collections.</span><span class="sxs-lookup"><span data-stu-id="1948c-133">Database is a logical container of one or more collections.</span></span> <span data-ttu-id="1948c-134">Database names must contain from 1 through 255 characters, and they cannot contain /, \\, #, ?, or a trailing space.</span><span class="sxs-lookup"><span data-stu-id="1948c-134">Database names must contain from 1 through 255 characters, and they cannot contain /, \\, #, ?, or a trailing space.</span></span> |
   |<span data-ttu-id="1948c-135">Collection id</span><span class="sxs-lookup"><span data-stu-id="1948c-135">Collection id</span></span>  | <span data-ttu-id="1948c-136">Provide a unique name to identify your collection.</span><span class="sxs-lookup"><span data-stu-id="1948c-136">Provide a unique name to identify your collection.</span></span> <span data-ttu-id="1948c-137">Collection ids have the same character requirements as database names.</span><span class="sxs-lookup"><span data-stu-id="1948c-137">Collection ids have the same character requirements as database names.</span></span> |
   |<span data-ttu-id="1948c-138">Storage capacity</span><span class="sxs-lookup"><span data-stu-id="1948c-138">Storage capacity</span></span>   | <span data-ttu-id="1948c-139">This value represents the storage capacity of the database.</span><span class="sxs-lookup"><span data-stu-id="1948c-139">This value represents the storage capacity of the database.</span></span> <span data-ttu-id="1948c-140">When provisioning throughput for an individual collection, storage capacity can be **Fixed (10 GB)** or **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="1948c-140">When provisioning throughput for an individual collection, storage capacity can be **Fixed (10 GB)** or **Unlimited**.</span></span> <span data-ttu-id="1948c-141">Unlimited storage capacity requires you to set a partition key for your data.</span><span class="sxs-lookup"><span data-stu-id="1948c-141">Unlimited storage capacity requires you to set a partition key for your data.</span></span>  |
   |<span data-ttu-id="1948c-142">Throughput</span><span class="sxs-lookup"><span data-stu-id="1948c-142">Throughput</span></span>   | <span data-ttu-id="1948c-143">Each collection and database can have throughput in request units per second.</span><span class="sxs-lookup"><span data-stu-id="1948c-143">Each collection and database can have throughput in request units per second.</span></span>  <span data-ttu-id="1948c-144">For fixed storage capacity, minimum throughput is 400 request units per second (RU/s), for unlimited storage capacity, minimum throughput is set to 1000 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1948c-144">For fixed storage capacity, minimum throughput is 400 request units per second (RU/s), for unlimited storage capacity, minimum throughput is set to 1000 RU/s.</span></span>|

6. <span data-ttu-id="1948c-145">After you enter values for these fields, select **OK** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="1948c-145">After you enter values for these fields, select **OK** to save the settings.</span></span>  

   ![Set throughput for a collection](./media/set-throughput/set-throughput-for-container.png)

7. <span data-ttu-id="1948c-147">To update throughput for an existing container, expand your database and the container and then click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1948c-147">To update throughput for an existing container, expand your database and the container and then click **Settings**.</span></span> <span data-ttu-id="1948c-148">In the new window, type the new throughput value and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="1948c-148">In the new window, type the new throughput value and then select **Save**.</span></span>  

   ![Update throughput for a collection](./media/set-throughput/update-throughput-for-container.png)

### <a name="provision-throughput-for-a-set-of-containers-or-at-the-database-level"></a><span data-ttu-id="1948c-150">Provision throughput for a set of containers or at the database level</span><span class="sxs-lookup"><span data-stu-id="1948c-150">Provision throughput for a set of containers or at the database level</span></span>

1. <span data-ttu-id="1948c-151">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1948c-151">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="1948c-152">From the left nav, select **All resources** and find your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="1948c-152">From the left nav, select **All resources** and find your Azure Cosmos DB account.</span></span>  
3. <span data-ttu-id="1948c-153">You can configure throughput while creating a database or update throughput for an existing database.</span><span class="sxs-lookup"><span data-stu-id="1948c-153">You can configure throughput while creating a database or update throughput for an existing database.</span></span>  
4. <span data-ttu-id="1948c-154">To assign throughput while creating a database, open the **Data Explorer** blade and select **New Database**</span><span class="sxs-lookup"><span data-stu-id="1948c-154">To assign throughput while creating a database, open the **Data Explorer** blade and select **New Database**</span></span>  
5. <span data-ttu-id="1948c-155">Fill the **Database id** value, check **Provision throughput** option, and configure throughput value.</span><span class="sxs-lookup"><span data-stu-id="1948c-155">Fill the **Database id** value, check **Provision throughput** option, and configure throughput value.</span></span> <span data-ttu-id="1948c-156">A database can be provisioned with minimum throughput value 50,000 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1948c-156">A database can be provisioned with minimum throughput value 50,000 RU/s.</span></span>  

   ![Set throughput with new database option](./media/set-throughput/set-throughput-with-new-database-option.png)

6. <span data-ttu-id="1948c-158">To update throughput for an existing database, expand your database and the container and then click **Scale**.</span><span class="sxs-lookup"><span data-stu-id="1948c-158">To update throughput for an existing database, expand your database and the container and then click **Scale**.</span></span> <span data-ttu-id="1948c-159">In the new window, type the new throughput value and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="1948c-159">In the new window, type the new throughput value and then select **Save**.</span></span>  

   ![Update throughput for a database](./media/set-throughput/update-throughput-for-database.png)

### <a name="provision-throughput-for-a-set-of-containers-as-well-as-for-an-individual-container-in-a-database"></a><span data-ttu-id="1948c-161">Provision throughput for a set of containers as well as for an individual container in a database</span><span class="sxs-lookup"><span data-stu-id="1948c-161">Provision throughput for a set of containers as well as for an individual container in a database</span></span>

1. <span data-ttu-id="1948c-162">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1948c-162">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="1948c-163">From the left nav, select **All resources** and find your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="1948c-163">From the left nav, select **All resources** and find your Azure Cosmos DB account.</span></span>  
3. <span data-ttu-id="1948c-164">Create a database and assign throughput to it.</span><span class="sxs-lookup"><span data-stu-id="1948c-164">Create a database and assign throughput to it.</span></span> <span data-ttu-id="1948c-165">Open the **Data Explorer** blade and select **New Database**</span><span class="sxs-lookup"><span data-stu-id="1948c-165">Open the **Data Explorer** blade and select **New Database**</span></span>  
4. <span data-ttu-id="1948c-166">Fill the **Database id** value, check **Provision throughput** option, and configure throughput value.</span><span class="sxs-lookup"><span data-stu-id="1948c-166">Fill the **Database id** value, check **Provision throughput** option, and configure throughput value.</span></span> <span data-ttu-id="1948c-167">A database can be provisioned with minimum throughput value 50,000 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1948c-167">A database can be provisioned with minimum throughput value 50,000 RU/s.</span></span>  

   ![Set throughput with new database option](./media/set-throughput/set-throughput-with-new-database-option.png)

5. <span data-ttu-id="1948c-169">Next create a collection within the database you created in above step.</span><span class="sxs-lookup"><span data-stu-id="1948c-169">Next create a collection within the database you created in above step.</span></span> <span data-ttu-id="1948c-170">To create a collection, right-click on the database and select **New Collection**.</span><span class="sxs-lookup"><span data-stu-id="1948c-170">To create a collection, right-click on the database and select **New Collection**.</span></span>  

6. <span data-ttu-id="1948c-171">In the **Add Collection** blade, enter a name for the collection, and partition key.</span><span class="sxs-lookup"><span data-stu-id="1948c-171">In the **Add Collection** blade, enter a name for the collection, and partition key.</span></span> <span data-ttu-id="1948c-172">Optionally, you can provision throughput for that specific container if you choose not to assign a throughput value, the throughput assigned to the database is shared to the collection.</span><span class="sxs-lookup"><span data-stu-id="1948c-172">Optionally, you can provision throughput for that specific container if you choose not to assign a throughput value, the throughput assigned to the database is shared to the collection.</span></span>  

   ![Optionally set throughput for the container](./media/set-throughput/optionally-set-throughput-for-the-container.png)

## <a name="considerations-when-provisioning-throughput"></a><span data-ttu-id="1948c-174">Considerations when provisioning throughput</span><span class="sxs-lookup"><span data-stu-id="1948c-174">Considerations when provisioning throughput</span></span>

<span data-ttu-id="1948c-175">Below are some considerations that help you decide on a throughput reservation strategy.</span><span class="sxs-lookup"><span data-stu-id="1948c-175">Below are some considerations that help you decide on a throughput reservation strategy.</span></span>

### <a name="considerations-when-provisioning-throughput-at-the-database-level"></a><span data-ttu-id="1948c-176">Considerations when provisioning throughput at the database level</span><span class="sxs-lookup"><span data-stu-id="1948c-176">Considerations when provisioning throughput at the database level</span></span>

<span data-ttu-id="1948c-177">Consider provisioning throughput at database level (that is for a set of containers) in the following cases:</span><span class="sxs-lookup"><span data-stu-id="1948c-177">Consider provisioning throughput at database level (that is for a set of containers) in the following cases:</span></span>

* <span data-ttu-id="1948c-178">If you have a dozen or more number of containers that could share throughput across some or all of them.</span><span class="sxs-lookup"><span data-stu-id="1948c-178">If you have a dozen or more number of containers that could share throughput across some or all of them.</span></span>  

* <span data-ttu-id="1948c-179">When you are migrating from a single-tenant database that is designed to run on IaaS-hosted VMs or on-premises (for example, NoSQL or relational databases) to Azure Cosmos DB and have many containers.</span><span class="sxs-lookup"><span data-stu-id="1948c-179">When you are migrating from a single-tenant database that is designed to run on IaaS-hosted VMs or on-premises (for example, NoSQL or relational databases) to Azure Cosmos DB and have many containers.</span></span>  

* <span data-ttu-id="1948c-180">If you want to consider unplanned spikes in workloads by using pooled throughput at the database level.</span><span class="sxs-lookup"><span data-stu-id="1948c-180">If you want to consider unplanned spikes in workloads by using pooled throughput at the database level.</span></span>  

* <span data-ttu-id="1948c-181">Instead of setting throughput on an individual container, you are interested in getting the aggregate throughput across a set of containers within the database.</span><span class="sxs-lookup"><span data-stu-id="1948c-181">Instead of setting throughput on an individual container, you are interested in getting the aggregate throughput across a set of containers within the database.</span></span>

### <a name="considerations-when-provisioning-throughput-at-the-container-level"></a><span data-ttu-id="1948c-182">Considerations when provisioning throughput at the container level</span><span class="sxs-lookup"><span data-stu-id="1948c-182">Considerations when provisioning throughput at the container level</span></span>

<span data-ttu-id="1948c-183">Consider provisioning throughput at an individual container in the following cases:</span><span class="sxs-lookup"><span data-stu-id="1948c-183">Consider provisioning throughput at an individual container in the following cases:</span></span>

* <span data-ttu-id="1948c-184">If you have less number of Azure Cosmos DB containers.</span><span class="sxs-lookup"><span data-stu-id="1948c-184">If you have less number of Azure Cosmos DB containers.</span></span>  

* <span data-ttu-id="1948c-185">If you want to get the guaranteed throughput on a given container backed by SLA.</span><span class="sxs-lookup"><span data-stu-id="1948c-185">If you want to get the guaranteed throughput on a given container backed by SLA.</span></span>

## <a name="throughput-ranges"></a><span data-ttu-id="1948c-186">Throughput ranges</span><span class="sxs-lookup"><span data-stu-id="1948c-186">Throughput ranges</span></span>

<span data-ttu-id="1948c-187">The following table lists the throughput available for containers:</span><span class="sxs-lookup"><span data-stu-id="1948c-187">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-188"><strong>Single Partition Container</strong></span><span class="sxs-lookup"><span data-stu-id="1948c-188"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-189"><strong>Partitioned Container</strong></span><span class="sxs-lookup"><span data-stu-id="1948c-189"><strong>Partitioned Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-190"><strong>Set of Containers</strong></span><span class="sxs-lookup"><span data-stu-id="1948c-190"><strong>Set of Containers</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1948c-191">Minimum Throughput</span><span class="sxs-lookup"><span data-stu-id="1948c-191">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-192">400 request units per second</span><span class="sxs-lookup"><span data-stu-id="1948c-192">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-193">1,000 request units per second</span><span class="sxs-lookup"><span data-stu-id="1948c-193">1,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-194">50,000 request units per second</span><span class="sxs-lookup"><span data-stu-id="1948c-194">50,000 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1948c-195">Maximum Throughput</span><span class="sxs-lookup"><span data-stu-id="1948c-195">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-196">10,000 request units per second</span><span class="sxs-lookup"><span data-stu-id="1948c-196">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-197">Unlimited</span><span class="sxs-lookup"><span data-stu-id="1948c-197">Unlimited</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1948c-198">Unlimited</span><span class="sxs-lookup"><span data-stu-id="1948c-198">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

<a id="set-throughput-sdk"></a>

## <a name="set-throughput-by-using-sql-api-for-net"></a><span data-ttu-id="1948c-199">Set throughput by using SQL API for .NET</span><span class="sxs-lookup"><span data-stu-id="1948c-199">Set throughput by using SQL API for .NET</span></span>

### <a name="set-throughput-at-the-container-level"></a><span data-ttu-id="1948c-200">Set throughput at the container level</span><span class="sxs-lookup"><span data-stu-id="1948c-200">Set throughput at the container level</span></span>
<span data-ttu-id="1948c-201">Here is a code snippet for creating a container with 3,000 request units per second for an individual container using the SQL API's .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="1948c-201">Here is a code snippet for creating a container with 3,000 request units per second for an individual container using the SQL API's .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

### <a name="set-throughput-for-a-set-of-containers-at-the-database-level"></a><span data-ttu-id="1948c-202">Set throughput for a set of containers at the database level</span><span class="sxs-lookup"><span data-stu-id="1948c-202">Set throughput for a set of containers at the database level</span></span>

<span data-ttu-id="1948c-203">Here is a code snippet for provisioning 100,000 request units per second across a set of containers using the SQL API's .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="1948c-203">Here is a code snippet for provisioning 100,000 request units per second across a set of containers using the SQL API's .NET SDK:</span></span>

```csharp
// Provision 100,000 RU/sec at the database level. 
// sharedCollection1 and sharedCollection2 will share the 100,000 RU/sec from the parent database
// dedicatedCollection will have its own dedicated 4,000 RU/sec, independant of the 100,000 RU/sec provisioned from the parent database
Database database = await client.CreateDatabaseAsync(new Database { Id = "myDb" }, new RequestOptions { OfferThroughput = 100000 });

DocumentCollection sharedCollection1 = new DocumentCollection();
sharedCollection1.Id = "sharedCollection1";
sharedCollection1.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(database.SelfLink, sharedCollection1, new RequestOptions())

DocumentCollection sharedCollection2 = new DocumentCollection();
sharedCollection2.Id = "sharedCollection2";
sharedCollection2.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(database.SelfLink, sharedCollection2, new RequestOptions())

DocumentCollection dedicatedCollection = new DocumentCollection();
dedicatedCollection.Id = "dedicatedCollection";
dedicatedCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(database.SelfLink, dedicatedCollection, new RequestOptions { OfferThroughput = 4000 )
```

<span data-ttu-id="1948c-204">Azure Cosmos DB operates on a reservation model for throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-204">Azure Cosmos DB operates on a reservation model for throughput.</span></span> <span data-ttu-id="1948c-205">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span><span class="sxs-lookup"><span data-stu-id="1948c-205">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="1948c-206">As your application's load, data, and usage patterns change you can easily scale up and down the number of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1948c-206">As your application's load, data, and usage patterns change you can easily scale up and down the number of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="1948c-207">Each container, or set of containers, is mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-207">Each container, or set of containers, is mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="1948c-208">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span><span class="sxs-lookup"><span data-stu-id="1948c-208">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="1948c-209">Here is a code snippet for changing the throughput of a container to 5,000 request units per second using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="1948c-209">Here is a code snippet for changing the throughput of a container to 5,000 request units per second using the .NET SDK.</span></span> <span data-ttu-id="1948c-210">After changing the throughput, you should refresh any existing Azure portal windows for the changed throughput to show up.</span><span class="sxs-lookup"><span data-stu-id="1948c-210">After changing the throughput, you should refresh any existing Azure portal windows for the changed throughput to show up.</span></span> 

```csharp
// Fetch the resource to be updated
// For a updating throughput for a set of containers, replace the collection's self link with the database's self link
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="1948c-211">There is no impact to the availability of your container, or set of containers, when you change the throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-211">There is no impact to the availability of your container, or set of containers, when you change the throughput.</span></span> <span data-ttu-id="1948c-212">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-212">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

<a id="set-throughput-java"></a>

## <a name="to-set-the-throughput-by-using-the-sql-api-for-java"></a><span data-ttu-id="1948c-213">To set the throughput by using the SQL API for Java</span><span class="sxs-lookup"><span data-stu-id="1948c-213">To set the throughput by using the SQL API for Java</span></span>

<span data-ttu-id="1948c-214">The following code snippet retrieves the current throughput and changes it to 500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1948c-214">The following code snippet retrieves the current throughput and changes it to 500 RU/s.</span></span> <span data-ttu-id="1948c-215">For a complete code sample, see the [OfferCrudSamples.java](https://github.com/Azure/azure-documentdb-java/blob/master/documentdb-examples/src/test/java/com/microsoft/azure/documentdb/examples/OfferCrudSamples.java) file on GitHub.</span><span class="sxs-lookup"><span data-stu-id="1948c-215">For a complete code sample, see the [OfferCrudSamples.java](https://github.com/Azure/azure-documentdb-java/blob/master/documentdb-examples/src/test/java/com/microsoft/azure/documentdb/examples/OfferCrudSamples.java) file on GitHub.</span></span> 

```Java
// find offer associated with this collection
// To change the throughput for a set of containers, use the database's resource id instead of the collection's resource id
Iterator < Offer > it = client.queryOffers(
    String.format("SELECT * FROM r where r.offerResourceId = '%s'", collectionResourceId), null).getQueryIterator();
assertThat(it.hasNext(), equalTo(true));

Offer offer = it.next();
assertThat(offer.getString("offerResourceId"), equalTo(collectionResourceId));
assertThat(offer.getContent().getInt("offerThroughput"), equalTo(throughput));

// update the offer
int newThroughput = 500;
offer.getContent().put("offerThroughput", newThroughput);
client.replaceOffer(offer);
```

## <a name="get-throughput-by-using-mongodb-api-portal-metrics"></a><span data-ttu-id="1948c-216">Get throughput by using MongoDB API portal metrics</span><span class="sxs-lookup"><span data-stu-id="1948c-216">Get throughput by using MongoDB API portal metrics</span></span>

<span data-ttu-id="1948c-217">The simplest way to get a good estimate of request unit charges for your MongoDB API database is to use the [Azure portal](https://portal.azure.com) metrics.</span><span class="sxs-lookup"><span data-stu-id="1948c-217">The simplest way to get a good estimate of request unit charges for your MongoDB API database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="1948c-218">With the *Number of requests* and *Request Charge* charts, you can get an estimate of how many request units each operation is consuming and how many request units they consume relative to one another.</span><span class="sxs-lookup"><span data-stu-id="1948c-218">With the *Number of requests* and *Request Charge* charts, you can get an estimate of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![MongoDB API portal metrics][1]

### <a id="RequestRateTooLargeAPIforMongoDB"></a> <span data-ttu-id="1948c-220">Exceeding reserved throughput limits in the MongoDB API</span><span class="sxs-lookup"><span data-stu-id="1948c-220">Exceeding reserved throughput limits in the MongoDB API</span></span>
<span data-ttu-id="1948c-221">Applications that exceed the provisioned throughput for a container or a set of containers will be rate-limited until the consumption rate drops below the provisioned throughput rate.</span><span class="sxs-lookup"><span data-stu-id="1948c-221">Applications that exceed the provisioned throughput for a container or a set of containers will be rate-limited until the consumption rate drops below the provisioned throughput rate.</span></span> <span data-ttu-id="1948c-222">When a rate-limitation occurs, the backend will end the request with a `16500` error code - `Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="1948c-222">When a rate-limitation occurs, the backend will end the request with a `16500` error code - `Too Many Requests`.</span></span> <span data-ttu-id="1948c-223">By default, the MongoDB API automatically retries up to 10 times before returning a `Too Many Requests` error code.</span><span class="sxs-lookup"><span data-stu-id="1948c-223">By default, the MongoDB API automatically retries up to 10 times before returning a `Too Many Requests` error code.</span></span> <span data-ttu-id="1948c-224">If you are receiving many `Too Many Requests` error codes, you may want to consider either adding a retry logic in your application's error handling routines or [increase provisioned throughput for the container](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="1948c-224">If you are receiving many `Too Many Requests` error codes, you may want to consider either adding a retry logic in your application's error handling routines or [increase provisioned throughput for the container](set-throughput.md).</span></span>

## <a id="GetLastRequestStatistics"></a><span data-ttu-id="1948c-225">Get request charge by using MongoDB API's GetLastRequestStatistics command</span><span class="sxs-lookup"><span data-stu-id="1948c-225">Get request charge by using MongoDB API's GetLastRequestStatistics command</span></span>

<span data-ttu-id="1948c-226">The MongoDB API supports a custom command, *getLastRequestStatistics*, for retrieving the request charges for a given operation.</span><span class="sxs-lookup"><span data-stu-id="1948c-226">The MongoDB API supports a custom command, *getLastRequestStatistics*, for retrieving the request charges for a given operation.</span></span>

<span data-ttu-id="1948c-227">For example, in the Mongo shell, execute the operation that you want to verify the request charge for.</span><span class="sxs-lookup"><span data-stu-id="1948c-227">For example, in the Mongo shell, execute the operation that you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="1948c-228">Next, execute the command *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="1948c-228">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="1948c-229">One method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimate the number of operations you anticipate to perform each second.</span><span class="sxs-lookup"><span data-stu-id="1948c-229">One method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimate the number of operations you anticipate to perform each second.</span></span>

> [!NOTE]
> <span data-ttu-id="1948c-230">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span><span class="sxs-lookup"><span data-stu-id="1948c-230">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="throughput-faq"></a><span data-ttu-id="1948c-231">Throughput FAQ</span><span class="sxs-lookup"><span data-stu-id="1948c-231">Throughput FAQ</span></span>

<span data-ttu-id="1948c-232">**Can I set my throughput to less than 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="1948c-232">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="1948c-233">400 RU/s is the minimum throughput available on Cosmos DB single partition containers (1000 RU/s is the minimum for partitioned containers).</span><span class="sxs-lookup"><span data-stu-id="1948c-233">400 RU/s is the minimum throughput available on Cosmos DB single partition containers (1000 RU/s is the minimum for partitioned containers).</span></span> <span data-ttu-id="1948c-234">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1948c-234">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="1948c-235">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span><span class="sxs-lookup"><span data-stu-id="1948c-235">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="1948c-236">**How do I set throughput using the MongoDB API?**</span><span class="sxs-lookup"><span data-stu-id="1948c-236">**How do I set throughput using the MongoDB API?**</span></span>

<span data-ttu-id="1948c-237">There's no MongoDB API extension to set throughput.</span><span class="sxs-lookup"><span data-stu-id="1948c-237">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="1948c-238">The recommendation is to use the SQL API, as shown in [To set the throughput by using the SQL API for .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="1948c-238">The recommendation is to use the SQL API, as shown in [To set the throughput by using the SQL API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1948c-239">Next steps</span><span class="sxs-lookup"><span data-stu-id="1948c-239">Next steps</span></span>

* <span data-ttu-id="1948c-240">To learn about estimating throughput and request units, see [Request units & estimating throughput in Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="1948c-240">To learn about estimating throughput and request units, see [Request units & estimating throughput in Azure Cosmos DB](request-units.md)</span></span>

* <span data-ttu-id="1948c-241">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="1948c-241">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>

[1]: ./media/set-throughput/api-for-mongodb-metrics.png
