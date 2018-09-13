---
title: Azure Storage Table Design Guide | Microsoft Docs
description: Design Scalable and Performant Tables in Azure Table Storage
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: e815ac38cdff953e1cc16672cbc6e3835ce1d191
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550785"
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a><span data-ttu-id="a595e-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span><span class="sxs-lookup"><span data-stu-id="a595e-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span></span>
## <a name="overview"></a><span data-ttu-id="a595e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a595e-104">Overview</span></span>
<span data-ttu-id="a595e-105">To design scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span><span class="sxs-lookup"><span data-stu-id="a595e-105">To design scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span></span> <span data-ttu-id="a595e-106">If you have previously designed schemas for relational databases, these considerations will be familiar to you, but while there are some similarities between the Azure Table service storage model and relational models, there are also many important differences.</span><span class="sxs-lookup"><span data-stu-id="a595e-106">If you have previously designed schemas for relational databases, these considerations will be familiar to you, but while there are some similarities between the Azure Table service storage model and relational models, there are also many important differences.</span></span> <span data-ttu-id="a595e-107">These differences typically lead to very different designs that may look counter-intuitive or wrong to someone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as the Azure Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-107">These differences typically lead to very different designs that may look counter-intuitive or wrong to someone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as the Azure Table service.</span></span> <span data-ttu-id="a595e-108">Many of your design differences will reflect the fact that the Table service is designed to support cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need to think differently about how you store your data and understand how the Table service works.</span><span class="sxs-lookup"><span data-stu-id="a595e-108">Many of your design differences will reflect the fact that the Table service is designed to support cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need to think differently about how you store your data and understand how the Table service works.</span></span> <span data-ttu-id="a595e-109">A well designed NoSQL data store can enable your solution to scale much further (and at a lower cost) than a solution that uses a relational database.</span><span class="sxs-lookup"><span data-stu-id="a595e-109">A well designed NoSQL data store can enable your solution to scale much further (and at a lower cost) than a solution that uses a relational database.</span></span> <span data-ttu-id="a595e-110">This guide helps you with these topics.</span><span class="sxs-lookup"><span data-stu-id="a595e-110">This guide helps you with these topics.</span></span>  

## <a name="about-the-azure-table-service"></a><span data-ttu-id="a595e-111">About the Azure Table service</span><span class="sxs-lookup"><span data-stu-id="a595e-111">About the Azure Table service</span></span>
<span data-ttu-id="a595e-112">This section highlights some of the key features of the Table service that are especially relevant to designing for performance and scalability.</span><span class="sxs-lookup"><span data-stu-id="a595e-112">This section highlights some of the key features of the Table service that are especially relevant to designing for performance and scalability.</span></span> <span data-ttu-id="a595e-113">If you are new to Azure Storage and the Table service, first read [Introduction to Microsoft Azure Storage](storage-introduction.md) and [Get started with Azure Table Storage using .NET](storage-dotnet-how-to-use-tables.md) before reading the remainder of this article.</span><span class="sxs-lookup"><span data-stu-id="a595e-113">If you are new to Azure Storage and the Table service, first read [Introduction to Microsoft Azure Storage](storage-introduction.md) and [Get started with Azure Table Storage using .NET](storage-dotnet-how-to-use-tables.md) before reading the remainder of this article.</span></span> <span data-ttu-id="a595e-114">Although the focus of this guide is on the Table service, it will include some discussion of the Azure Queue and Blob services, and how you might use them along with the Table service in a solution.</span><span class="sxs-lookup"><span data-stu-id="a595e-114">Although the focus of this guide is on the Table service, it will include some discussion of the Azure Queue and Blob services, and how you might use them along with the Table service in a solution.</span></span>  

<span data-ttu-id="a595e-115">What is the Table service?</span><span class="sxs-lookup"><span data-stu-id="a595e-115">What is the Table service?</span></span> <span data-ttu-id="a595e-116">As you might expect from the name, the Table service uses a tabular format to store data.</span><span class="sxs-lookup"><span data-stu-id="a595e-116">As you might expect from the name, the Table service uses a tabular format to store data.</span></span> <span data-ttu-id="a595e-117">In the standard terminology, each row of the table represents an entity, and the columns store the various properties of that entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-117">In the standard terminology, each row of the table represents an entity, and the columns store the various properties of that entity.</span></span> <span data-ttu-id="a595e-118">Every entity has a pair of keys to uniquely identify it, and a timestamp column that the Table service uses to track when the entity was last updated (this happens automatically and you cannot manually overwrite the timestamp with an arbitrary value).</span><span class="sxs-lookup"><span data-stu-id="a595e-118">Every entity has a pair of keys to uniquely identify it, and a timestamp column that the Table service uses to track when the entity was last updated (this happens automatically and you cannot manually overwrite the timestamp with an arbitrary value).</span></span> <span data-ttu-id="a595e-119">The Table service uses this last-modified timestamp (LMT) to manage optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="a595e-119">The Table service uses this last-modified timestamp (LMT) to manage optimistic concurrency.</span></span>  

> [!NOTE]
> <span data-ttu-id="a595e-120">The Table service REST API operations also return an **ETag** value that it derives from the last-modified timestamp (LMT).</span><span class="sxs-lookup"><span data-stu-id="a595e-120">The Table service REST API operations also return an **ETag** value that it derives from the last-modified timestamp (LMT).</span></span> <span data-ttu-id="a595e-121">In this document we will use the terms ETag and LMT interchangeably because they refer to the same underlying data.</span><span class="sxs-lookup"><span data-stu-id="a595e-121">In this document we will use the terms ETag and LMT interchangeably because they refer to the same underlying data.</span></span>  
> 
> 

<span data-ttu-id="a595e-122">The following example shows a simple table design to store employee and department entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-122">The following example shows a simple table design to store employee and department entities.</span></span> <span data-ttu-id="a595e-123">Many of the examples shown later in this guide are based on this simple design.</span><span class="sxs-lookup"><span data-stu-id="a595e-123">Many of the examples shown later in this guide are based on this simple design.</span></span>  

<table>
<tr>
<th><span data-ttu-id="a595e-124">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a595e-124">PartitionKey</span></span></th>
<th><span data-ttu-id="a595e-125">RowKey</span><span class="sxs-lookup"><span data-stu-id="a595e-125">RowKey</span></span></th>
<th><span data-ttu-id="a595e-126">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a595e-126">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-127">Marketing</span><span class="sxs-lookup"><span data-stu-id="a595e-127">Marketing</span></span></td>
<td><span data-ttu-id="a595e-128">00001</span><span class="sxs-lookup"><span data-stu-id="a595e-128">00001</span></span></td>
<td><span data-ttu-id="a595e-129">2014-08-22T00:50:32Z</span><span class="sxs-lookup"><span data-stu-id="a595e-129">2014-08-22T00:50:32Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-130">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-130">FirstName</span></span></th>
<th><span data-ttu-id="a595e-131">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-131">LastName</span></span></th>
<th><span data-ttu-id="a595e-132">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-132">Age</span></span></th>
<th><span data-ttu-id="a595e-133">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-133">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-134">Don</span><span class="sxs-lookup"><span data-stu-id="a595e-134">Don</span></span></td>
<td><span data-ttu-id="a595e-135">Hall</span><span class="sxs-lookup"><span data-stu-id="a595e-135">Hall</span></span></td>
<td><span data-ttu-id="a595e-136">34</span><span class="sxs-lookup"><span data-stu-id="a595e-136">34</span></span></td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="a595e-137">Marketing</span><span class="sxs-lookup"><span data-stu-id="a595e-137">Marketing</span></span></td>
<td><span data-ttu-id="a595e-138">00002</span><span class="sxs-lookup"><span data-stu-id="a595e-138">00002</span></span></td>
<td><span data-ttu-id="a595e-139">2014-08-22T00:50:34Z</span><span class="sxs-lookup"><span data-stu-id="a595e-139">2014-08-22T00:50:34Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-140">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-140">FirstName</span></span></th>
<th><span data-ttu-id="a595e-141">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-141">LastName</span></span></th>
<th><span data-ttu-id="a595e-142">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-142">Age</span></span></th>
<th><span data-ttu-id="a595e-143">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-143">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-144">Jun</span><span class="sxs-lookup"><span data-stu-id="a595e-144">Jun</span></span></td>
<td><span data-ttu-id="a595e-145">Cao</span><span class="sxs-lookup"><span data-stu-id="a595e-145">Cao</span></span></td>
<td><span data-ttu-id="a595e-146">47</span><span class="sxs-lookup"><span data-stu-id="a595e-146">47</span></span></td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="a595e-147">Marketing</span><span class="sxs-lookup"><span data-stu-id="a595e-147">Marketing</span></span></td>
<td><span data-ttu-id="a595e-148">Department</span><span class="sxs-lookup"><span data-stu-id="a595e-148">Department</span></span></td>
<td><span data-ttu-id="a595e-149">2014-08-22T00:50:30Z</span><span class="sxs-lookup"><span data-stu-id="a595e-149">2014-08-22T00:50:30Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-150">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="a595e-150">DepartmentName</span></span></th>
<th><span data-ttu-id="a595e-151">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="a595e-151">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-152">Marketing</span><span class="sxs-lookup"><span data-stu-id="a595e-152">Marketing</span></span></td>
<td><span data-ttu-id="a595e-153">153</span><span class="sxs-lookup"><span data-stu-id="a595e-153">153</span></span></td>
</tr>
</table>
</td>
</tr>
<tr>
<td><span data-ttu-id="a595e-154">Sales</span><span class="sxs-lookup"><span data-stu-id="a595e-154">Sales</span></span></td>
<td><span data-ttu-id="a595e-155">00010</span><span class="sxs-lookup"><span data-stu-id="a595e-155">00010</span></span></td>
<td><span data-ttu-id="a595e-156">2014-08-22T00:50:44Z</span><span class="sxs-lookup"><span data-stu-id="a595e-156">2014-08-22T00:50:44Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-157">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-157">FirstName</span></span></th>
<th><span data-ttu-id="a595e-158">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-158">LastName</span></span></th>
<th><span data-ttu-id="a595e-159">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-159">Age</span></span></th>
<th><span data-ttu-id="a595e-160">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-160">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-161">Ken</span><span class="sxs-lookup"><span data-stu-id="a595e-161">Ken</span></span></td>
<td><span data-ttu-id="a595e-162">Kwok</span><span class="sxs-lookup"><span data-stu-id="a595e-162">Kwok</span></span></td>
<td><span data-ttu-id="a595e-163">23</span><span class="sxs-lookup"><span data-stu-id="a595e-163">23</span></span></td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


<span data-ttu-id="a595e-164">So far, this looks very similar to a table in a relational database with the key differences being the mandatory columns, and the ability to store multiple entity types in the same table.</span><span class="sxs-lookup"><span data-stu-id="a595e-164">So far, this looks very similar to a table in a relational database with the key differences being the mandatory columns, and the ability to store multiple entity types in the same table.</span></span> <span data-ttu-id="a595e-165">In addition, each of the user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span><span class="sxs-lookup"><span data-stu-id="a595e-165">In addition, each of the user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span></span> <span data-ttu-id="a595e-166">Although unlike in a relational database, the schema-less nature of the Table service means that a property need not have the same data type on each entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-166">Although unlike in a relational database, the schema-less nature of the Table service means that a property need not have the same data type on each entity.</span></span> <span data-ttu-id="a595e-167">To store complex data types in a single property, you must use a serialized format such as JSON or XML.</span><span class="sxs-lookup"><span data-stu-id="a595e-167">To store complex data types in a single property, you must use a serialized format such as JSON or XML.</span></span> <span data-ttu-id="a595e-168">For more information about the table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-168">For more information about the table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="a595e-169">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental to good table design.</span><span class="sxs-lookup"><span data-stu-id="a595e-169">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental to good table design.</span></span> <span data-ttu-id="a595e-170">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-170">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="a595e-171">As with keys in a relational database table, the **PartitionKey** and **RowKey** values are indexed to create a clustered index that enables fast look-ups; however, the Table service does not create any secondary indexes so these are the only two indexed properties (some of the patterns described later show how you can work around this apparent limitation).</span><span class="sxs-lookup"><span data-stu-id="a595e-171">As with keys in a relational database table, the **PartitionKey** and **RowKey** values are indexed to create a clustered index that enables fast look-ups; however, the Table service does not create any secondary indexes so these are the only two indexed properties (some of the patterns described later show how you can work around this apparent limitation).</span></span>  

<span data-ttu-id="a595e-172">A table is made up of one or more partitions, and as you will see, many of the design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** to optimize your solution.</span><span class="sxs-lookup"><span data-stu-id="a595e-172">A table is made up of one or more partitions, and as you will see, many of the design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** to optimize your solution.</span></span> <span data-ttu-id="a595e-173">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span><span class="sxs-lookup"><span data-stu-id="a595e-173">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span></span> <span data-ttu-id="a595e-174">Tables help you to logically organize your entities, help you manage access to the data using access control lists, and you can drop an entire table using a single storage operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-174">Tables help you to logically organize your entities, help you manage access to the data using access control lists, and you can drop an entire table using a single storage operation.</span></span>  

### <a name="table-partitions"></a><span data-ttu-id="a595e-175">Table partitions</span><span class="sxs-lookup"><span data-stu-id="a595e-175">Table partitions</span></span>
<span data-ttu-id="a595e-176">The account name, table name and **PartitionKey** together identify the partition within the storage service where the table service stores the entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-176">The account name, table name and **PartitionKey** together identify the partition within the storage service where the table service stores the entity.</span></span> <span data-ttu-id="a595e-177">As well as being part of the addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form the basis of how the table service scales.</span><span class="sxs-lookup"><span data-stu-id="a595e-177">As well as being part of the addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form the basis of how the table service scales.</span></span> <span data-ttu-id="a595e-178">For more information on partitions see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="a595e-178">For more information on partitions see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span>  

<span data-ttu-id="a595e-179">In the Table service, an individual node services one or more complete partitions and the service scales by dynamically load-balancing partitions across nodes.</span><span class="sxs-lookup"><span data-stu-id="a595e-179">In the Table service, an individual node services one or more complete partitions and the service scales by dynamically load-balancing partitions across nodes.</span></span> <span data-ttu-id="a595e-180">If a node is under load, the table service can *split* the range of partitions serviced by that node onto different nodes; when traffic subsides, the service can *merge* the partition ranges from quiet nodes back onto a single node.</span><span class="sxs-lookup"><span data-stu-id="a595e-180">If a node is under load, the table service can *split* the range of partitions serviced by that node onto different nodes; when traffic subsides, the service can *merge* the partition ranges from quiet nodes back onto a single node.</span></span>  

<span data-ttu-id="a595e-181">For more information about the internal details of the Table service, and in particular how the service manages partitions, see the paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-181">For more information about the internal details of the Table service, and in particular how the service manages partitions, see the paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>  

### <a name="entity-group-transactions"></a><span data-ttu-id="a595e-182">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-182">Entity Group Transactions</span></span>
<span data-ttu-id="a595e-183">In the Table service, Entity Group Transactions (EGTs) are the only built-in mechanism for performing atomic updates across multiple entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-183">In the Table service, Entity Group Transactions (EGTs) are the only built-in mechanism for performing atomic updates across multiple entities.</span></span> <span data-ttu-id="a595e-184">EGTs are also referred to as *batch transactions* in some documentation.</span><span class="sxs-lookup"><span data-stu-id="a595e-184">EGTs are also referred to as *batch transactions* in some documentation.</span></span> <span data-ttu-id="a595e-185">EGTs can only operate on entities stored in the same partition (share the same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need to ensure that those entities are in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-185">EGTs can only operate on entities stored in the same partition (share the same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need to ensure that those entities are in the same partition.</span></span> <span data-ttu-id="a595e-186">This is often a reason for keeping multiple entity types in the same table (and partition) and not using multiple tables for different entity types.</span><span class="sxs-lookup"><span data-stu-id="a595e-186">This is often a reason for keeping multiple entity types in the same table (and partition) and not using multiple tables for different entity types.</span></span> <span data-ttu-id="a595e-187">A single EGT can operate on at most 100 entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-187">A single EGT can operate on at most 100 entities.</span></span>  <span data-ttu-id="a595e-188">If you submit multiple concurrent EGTs for processing it is important to ensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span><span class="sxs-lookup"><span data-stu-id="a595e-188">If you submit multiple concurrent EGTs for processing it is important to ensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span></span>

<span data-ttu-id="a595e-189">EGTs also introduce a potential trade-off for you to evaluate in your design: using more partitions will increase the scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit the ability of your application to perform atomic transactions and maintain strong consistency for your data.</span><span class="sxs-lookup"><span data-stu-id="a595e-189">EGTs also introduce a potential trade-off for you to evaluate in your design: using more partitions will increase the scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit the ability of your application to perform atomic transactions and maintain strong consistency for your data.</span></span> <span data-ttu-id="a595e-190">Furthermore, there are specific scalability targets at the level of a partition that might limit the throughput of transactions you can expect for a single node: for more information about the scalability targets for Azure storage accounts and the table service, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="a595e-190">Furthermore, there are specific scalability targets at the level of a partition that might limit the throughput of transactions you can expect for a single node: for more information about the scalability targets for Azure storage accounts and the table service, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="a595e-191">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best to choose your partition key based on the specific requirements of your client application.</span><span class="sxs-lookup"><span data-stu-id="a595e-191">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best to choose your partition key based on the specific requirements of your client application.</span></span>  

### <a name="capacity-considerations"></a><span data-ttu-id="a595e-192">Capacity considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-192">Capacity considerations</span></span>
<span data-ttu-id="a595e-193">The following table includes some of the key values to be aware of when you are designing a Table service solution:</span><span class="sxs-lookup"><span data-stu-id="a595e-193">The following table includes some of the key values to be aware of when you are designing a Table service solution:</span></span>  

| <span data-ttu-id="a595e-194">Total capacity of an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="a595e-194">Total capacity of an Azure storage account</span></span> | <span data-ttu-id="a595e-195">500 TB</span><span class="sxs-lookup"><span data-stu-id="a595e-195">500 TB</span></span> |
| --- | --- |
| <span data-ttu-id="a595e-196">Number of tables in an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="a595e-196">Number of tables in an Azure storage account</span></span> |<span data-ttu-id="a595e-197">Limited only by the capacity of the storage account</span><span class="sxs-lookup"><span data-stu-id="a595e-197">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="a595e-198">Number of partitions in a table</span><span class="sxs-lookup"><span data-stu-id="a595e-198">Number of partitions in a table</span></span> |<span data-ttu-id="a595e-199">Limited only by the capacity of the storage account</span><span class="sxs-lookup"><span data-stu-id="a595e-199">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="a595e-200">Number of entities in a partition</span><span class="sxs-lookup"><span data-stu-id="a595e-200">Number of entities in a partition</span></span> |<span data-ttu-id="a595e-201">Limited only by the capacity of the storage account</span><span class="sxs-lookup"><span data-stu-id="a595e-201">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="a595e-202">Size of an individual entity</span><span class="sxs-lookup"><span data-stu-id="a595e-202">Size of an individual entity</span></span> |<span data-ttu-id="a595e-203">Up to 1 MB with a maximum of 255 properties (including the **PartitionKey**, **RowKey**, and **Timestamp**)</span><span class="sxs-lookup"><span data-stu-id="a595e-203">Up to 1 MB with a maximum of 255 properties (including the **PartitionKey**, **RowKey**, and **Timestamp**)</span></span> |
| <span data-ttu-id="a595e-204">Size of the **PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="a595e-204">Size of the **PartitionKey**</span></span> |<span data-ttu-id="a595e-205">A string up to 1 KB in size</span><span class="sxs-lookup"><span data-stu-id="a595e-205">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="a595e-206">Size of the **RowKey**</span><span class="sxs-lookup"><span data-stu-id="a595e-206">Size of the **RowKey**</span></span> |<span data-ttu-id="a595e-207">A string up to 1 KB in size</span><span class="sxs-lookup"><span data-stu-id="a595e-207">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="a595e-208">Size of an Entity Group Transaction</span><span class="sxs-lookup"><span data-stu-id="a595e-208">Size of an Entity Group Transaction</span></span> |<span data-ttu-id="a595e-209">A transaction can include at most 100 entities and the payload must be less than 4 MB in size.</span><span class="sxs-lookup"><span data-stu-id="a595e-209">A transaction can include at most 100 entities and the payload must be less than 4 MB in size.</span></span> <span data-ttu-id="a595e-210">An EGT can only update an entity once.</span><span class="sxs-lookup"><span data-stu-id="a595e-210">An EGT can only update an entity once.</span></span> |

<span data-ttu-id="a595e-211">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-211">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>  

### <a name="cost-considerations"></a><span data-ttu-id="a595e-212">Cost considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-212">Cost considerations</span></span>
<span data-ttu-id="a595e-213">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and the quantity of transactions as part of your evaluation of any solution that uses the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-213">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and the quantity of transactions as part of your evaluation of any solution that uses the Table service.</span></span> <span data-ttu-id="a595e-214">However, in many scenarios storing denormalized or duplicate data in order to improve the performance or scalability of your solution is a valid approach to take.</span><span class="sxs-lookup"><span data-stu-id="a595e-214">However, in many scenarios storing denormalized or duplicate data in order to improve the performance or scalability of your solution is a valid approach to take.</span></span> <span data-ttu-id="a595e-215">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="a595e-215">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>  

## <a name="guidelines-for-table-design"></a><span data-ttu-id="a595e-216">Guidelines for table design</span><span class="sxs-lookup"><span data-stu-id="a595e-216">Guidelines for table design</span></span>
<span data-ttu-id="a595e-217">These lists summarize some of the key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span><span class="sxs-lookup"><span data-stu-id="a595e-217">These lists summarize some of the key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span></span> <span data-ttu-id="a595e-218">These guidelines are very different from the guidelines you would typically follow for relational database design.</span><span class="sxs-lookup"><span data-stu-id="a595e-218">These guidelines are very different from the guidelines you would typically follow for relational database design.</span></span>  

<span data-ttu-id="a595e-219">Designing your Table service solution to be *read* efficient:</span><span class="sxs-lookup"><span data-stu-id="a595e-219">Designing your Table service solution to be *read* efficient:</span></span>

* <span data-ttu-id="a595e-220">***Design for querying in read-heavy applications.***</span><span class="sxs-lookup"><span data-stu-id="a595e-220">***Design for querying in read-heavy applications.***</span></span> <span data-ttu-id="a595e-221">When you are designing your tables, think about the queries (especially the latency sensitive ones) that you will execute before you think about how you will update your entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-221">When you are designing your tables, think about the queries (especially the latency sensitive ones) that you will execute before you think about how you will update your entities.</span></span> <span data-ttu-id="a595e-222">This typically results in an efficient and performant solution.</span><span class="sxs-lookup"><span data-stu-id="a595e-222">This typically results in an efficient and performant solution.</span></span>  
* <span data-ttu-id="a595e-223">***Specify both PartitionKey and RowKey in your queries.***</span><span class="sxs-lookup"><span data-stu-id="a595e-223">***Specify both PartitionKey and RowKey in your queries.***</span></span> <span data-ttu-id="a595e-224">*Point queries* such as these are the most efficient table service queries.</span><span class="sxs-lookup"><span data-stu-id="a595e-224">*Point queries* such as these are the most efficient table service queries.</span></span>  
* <span data-ttu-id="a595e-225">***Consider storing duplicate copies of entities.***</span><span class="sxs-lookup"><span data-stu-id="a595e-225">***Consider storing duplicate copies of entities.***</span></span> <span data-ttu-id="a595e-226">Table storage is cheap so consider storing the same entity multiple times (with different keys) to enable more efficient queries.</span><span class="sxs-lookup"><span data-stu-id="a595e-226">Table storage is cheap so consider storing the same entity multiple times (with different keys) to enable more efficient queries.</span></span>  
* <span data-ttu-id="a595e-227">***Consider denormalizing your data.***</span><span class="sxs-lookup"><span data-stu-id="a595e-227">***Consider denormalizing your data.***</span></span> <span data-ttu-id="a595e-228">Table storage is cheap so consider denormalizing your data.</span><span class="sxs-lookup"><span data-stu-id="a595e-228">Table storage is cheap so consider denormalizing your data.</span></span> <span data-ttu-id="a595e-229">For example, store summary entities so that queries for aggregate data only need to access a single entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-229">For example, store summary entities so that queries for aggregate data only need to access a single entity.</span></span>  
* <span data-ttu-id="a595e-230">***Use compound key values.***</span><span class="sxs-lookup"><span data-stu-id="a595e-230">***Use compound key values.***</span></span> <span data-ttu-id="a595e-231">The only keys you have are **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-231">The only keys you have are **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="a595e-232">For example, use compound key values to enable alternate keyed access paths to entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-232">For example, use compound key values to enable alternate keyed access paths to entities.</span></span>  
* <span data-ttu-id="a595e-233">***Use query projection.***</span><span class="sxs-lookup"><span data-stu-id="a595e-233">***Use query projection.***</span></span> <span data-ttu-id="a595e-234">You can reduce the amount of data that you transfer over the network by using queries that select just the fields you need.</span><span class="sxs-lookup"><span data-stu-id="a595e-234">You can reduce the amount of data that you transfer over the network by using queries that select just the fields you need.</span></span>  

<span data-ttu-id="a595e-235">Designing your Table service solution to be *write* efficient:</span><span class="sxs-lookup"><span data-stu-id="a595e-235">Designing your Table service solution to be *write* efficient:</span></span>  

* <span data-ttu-id="a595e-236">***Do not create hot partitions.***</span><span class="sxs-lookup"><span data-stu-id="a595e-236">***Do not create hot partitions.***</span></span> <span data-ttu-id="a595e-237">Choose keys that enable you to spread your requests across multiple partitions at any point of time.</span><span class="sxs-lookup"><span data-stu-id="a595e-237">Choose keys that enable you to spread your requests across multiple partitions at any point of time.</span></span>  
* <span data-ttu-id="a595e-238">***Avoid spikes in traffic.***</span><span class="sxs-lookup"><span data-stu-id="a595e-238">***Avoid spikes in traffic.***</span></span> <span data-ttu-id="a595e-239">Smooth the traffic over a reasonable period of time and avoid spikes in traffic.</span><span class="sxs-lookup"><span data-stu-id="a595e-239">Smooth the traffic over a reasonable period of time and avoid spikes in traffic.</span></span>
* <span data-ttu-id="a595e-240">***Don't necessarily create a separate table for each type of entity.***</span><span class="sxs-lookup"><span data-stu-id="a595e-240">***Don't necessarily create a separate table for each type of entity.***</span></span> <span data-ttu-id="a595e-241">When you require atomic transactions across entity types, you can store these multiple entity types in the same partition in the same table.</span><span class="sxs-lookup"><span data-stu-id="a595e-241">When you require atomic transactions across entity types, you can store these multiple entity types in the same partition in the same table.</span></span>
* <span data-ttu-id="a595e-242">***Consider the maximum throughput you must achieve.***</span><span class="sxs-lookup"><span data-stu-id="a595e-242">***Consider the maximum throughput you must achieve.***</span></span> <span data-ttu-id="a595e-243">You must be aware of the scalability targets for the Table service and ensure that your design will not cause you to exceed them.</span><span class="sxs-lookup"><span data-stu-id="a595e-243">You must be aware of the scalability targets for the Table service and ensure that your design will not cause you to exceed them.</span></span>  

<span data-ttu-id="a595e-244">As you read this guide, you will see examples that put all of these principles into practice.</span><span class="sxs-lookup"><span data-stu-id="a595e-244">As you read this guide, you will see examples that put all of these principles into practice.</span></span>  

## <a name="design-for-querying"></a><span data-ttu-id="a595e-245">Design for querying</span><span class="sxs-lookup"><span data-stu-id="a595e-245">Design for querying</span></span>
<span data-ttu-id="a595e-246">Table service solutions may be read intensive, write intensive, or a mix of the two.</span><span class="sxs-lookup"><span data-stu-id="a595e-246">Table service solutions may be read intensive, write intensive, or a mix of the two.</span></span> <span data-ttu-id="a595e-247">This section focuses on the things to bear in mind when you are designing your Table service to support read operations efficiently.</span><span class="sxs-lookup"><span data-stu-id="a595e-247">This section focuses on the things to bear in mind when you are designing your Table service to support read operations efficiently.</span></span> <span data-ttu-id="a595e-248">Typically, a design that supports read operations efficiently is also efficient for write operations.</span><span class="sxs-lookup"><span data-stu-id="a595e-248">Typically, a design that supports read operations efficiently is also efficient for write operations.</span></span> <span data-ttu-id="a595e-249">However, there are additional considerations to bear in mind when designing to support write operations, discussed in the next section, [Design for data modification](#design-for-data-modification).</span><span class="sxs-lookup"><span data-stu-id="a595e-249">However, there are additional considerations to bear in mind when designing to support write operations, discussed in the next section, [Design for data modification](#design-for-data-modification).</span></span>

<span data-ttu-id="a595e-250">A good starting point for designing your Table service solution to enable you to read data efficiently is to ask "What queries will my application need to execute to retrieve the data it needs from the Table service?"</span><span class="sxs-lookup"><span data-stu-id="a595e-250">A good starting point for designing your Table service solution to enable you to read data efficiently is to ask "What queries will my application need to execute to retrieve the data it needs from the Table service?"</span></span>  

> [!NOTE]
> <span data-ttu-id="a595e-251">With the Table service, it's important to get the design correct up front because it's difficult and expensive to change it later.</span><span class="sxs-lookup"><span data-stu-id="a595e-251">With the Table service, it's important to get the design correct up front because it's difficult and expensive to change it later.</span></span> <span data-ttu-id="a595e-252">For example, in a relational database it's often possible to address performance issues simply by adding indexes to an existing database: this is not an option with the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-252">For example, in a relational database it's often possible to address performance issues simply by adding indexes to an existing database: this is not an option with the Table service.</span></span>  
> 
> 

<span data-ttu-id="a595e-253">This section focuses on the key issues you must address when you design your tables for querying.</span><span class="sxs-lookup"><span data-stu-id="a595e-253">This section focuses on the key issues you must address when you design your tables for querying.</span></span> <span data-ttu-id="a595e-254">The topics covered in this section include:</span><span class="sxs-lookup"><span data-stu-id="a595e-254">The topics covered in this section include:</span></span>

* [<span data-ttu-id="a595e-255">How your choice of PartitionKey and RowKey impacts query performance</span><span class="sxs-lookup"><span data-stu-id="a595e-255">How your choice of PartitionKey and RowKey impacts query performance</span></span>](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [<span data-ttu-id="a595e-256">Choosing an appropriate PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a595e-256">Choosing an appropriate PartitionKey</span></span>](#choosing-an-appropriate-partitionkey)
* [<span data-ttu-id="a595e-257">Optimizing queries for the Table service</span><span class="sxs-lookup"><span data-stu-id="a595e-257">Optimizing queries for the Table service</span></span>](#optimizing-queries-for-the-table-service)
* [<span data-ttu-id="a595e-258">Sorting data in the Table service</span><span class="sxs-lookup"><span data-stu-id="a595e-258">Sorting data in the Table service</span></span>](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a><span data-ttu-id="a595e-259">How your choice of PartitionKey and RowKey impacts query performance</span><span class="sxs-lookup"><span data-stu-id="a595e-259">How your choice of PartitionKey and RowKey impacts query performance</span></span>
<span data-ttu-id="a595e-260">The following examples assume the table service is storing employee entities with the following structure (most of the examples omit the **Timestamp** property for clarity):</span><span class="sxs-lookup"><span data-stu-id="a595e-260">The following examples assume the table service is storing employee entities with the following structure (most of the examples omit the **Timestamp** property for clarity):</span></span>  

| <span data-ttu-id="a595e-261">*Column name*</span><span class="sxs-lookup"><span data-stu-id="a595e-261">*Column name*</span></span> | <span data-ttu-id="a595e-262">*Data type*</span><span class="sxs-lookup"><span data-stu-id="a595e-262">*Data type*</span></span> |
| --- | --- |
| <span data-ttu-id="a595e-263">**PartitionKey** (Department Name)</span><span class="sxs-lookup"><span data-stu-id="a595e-263">**PartitionKey** (Department Name)</span></span> |<span data-ttu-id="a595e-264">String</span><span class="sxs-lookup"><span data-stu-id="a595e-264">String</span></span> |
| <span data-ttu-id="a595e-265">**RowKey** (Employee Id)</span><span class="sxs-lookup"><span data-stu-id="a595e-265">**RowKey** (Employee Id)</span></span> |<span data-ttu-id="a595e-266">String</span><span class="sxs-lookup"><span data-stu-id="a595e-266">String</span></span> |
| <span data-ttu-id="a595e-267">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="a595e-267">**FirstName**</span></span> |<span data-ttu-id="a595e-268">String</span><span class="sxs-lookup"><span data-stu-id="a595e-268">String</span></span> |
| <span data-ttu-id="a595e-269">**LastName**</span><span class="sxs-lookup"><span data-stu-id="a595e-269">**LastName**</span></span> |<span data-ttu-id="a595e-270">String</span><span class="sxs-lookup"><span data-stu-id="a595e-270">String</span></span> |
| <span data-ttu-id="a595e-271">**Age**</span><span class="sxs-lookup"><span data-stu-id="a595e-271">**Age**</span></span> |<span data-ttu-id="a595e-272">Integer</span><span class="sxs-lookup"><span data-stu-id="a595e-272">Integer</span></span> |
| <span data-ttu-id="a595e-273">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="a595e-273">**EmailAddress**</span></span> |<span data-ttu-id="a595e-274">String</span><span class="sxs-lookup"><span data-stu-id="a595e-274">String</span></span> |

<span data-ttu-id="a595e-275">The earlier section [Azure Table service overview](#overview) describes some of the key features of the Azure Table service that have a direct influence on designing for query.</span><span class="sxs-lookup"><span data-stu-id="a595e-275">The earlier section [Azure Table service overview](#overview) describes some of the key features of the Azure Table service that have a direct influence on designing for query.</span></span> <span data-ttu-id="a595e-276">These result in the following general guidelines for designing Table service queries.</span><span class="sxs-lookup"><span data-stu-id="a595e-276">These result in the following general guidelines for designing Table service queries.</span></span> <span data-ttu-id="a595e-277">Note that the filter syntax used in the examples below is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-277">Note that the filter syntax used in the examples below is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

* <span data-ttu-id="a595e-278">A ***Point Query*** is the most efficient lookup to use and is recommended to be used for high-volume lookups or lookups requiring lowest latency.</span><span class="sxs-lookup"><span data-stu-id="a595e-278">A ***Point Query*** is the most efficient lookup to use and is recommended to be used for high-volume lookups or lookups requiring lowest latency.</span></span> <span data-ttu-id="a595e-279">Such a query can use the indexes to locate an individual entity very efficiently by specifying both the **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-279">Such a query can use the indexes to locate an individual entity very efficiently by specifying both the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-280">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span><span class="sxs-lookup"><span data-stu-id="a595e-280">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span></span>  
* <span data-ttu-id="a595e-281">Second best is a ***Range Query*** that uses the **PartitionKey** and filters on a range of **RowKey** values to return more than one entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-281">Second best is a ***Range Query*** that uses the **PartitionKey** and filters on a range of **RowKey** values to return more than one entity.</span></span> <span data-ttu-id="a595e-282">The **PartitionKey** value identifies a specific partition, and the **RowKey** values identify a subset of the entities in that partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-282">The **PartitionKey** value identifies a specific partition, and the **RowKey** values identify a subset of the entities in that partition.</span></span> <span data-ttu-id="a595e-283">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span><span class="sxs-lookup"><span data-stu-id="a595e-283">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span></span>  
* <span data-ttu-id="a595e-284">Third best is a ***Partition Scan*** that uses the **PartitionKey** and filters on another non-key property and that may return more than one entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-284">Third best is a ***Partition Scan*** that uses the **PartitionKey** and filters on another non-key property and that may return more than one entity.</span></span> <span data-ttu-id="a595e-285">The **PartitionKey** value identifies a specific partition, and the property values select for a subset of the entities in that partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-285">The **PartitionKey** value identifies a specific partition, and the property values select for a subset of the entities in that partition.</span></span> <span data-ttu-id="a595e-286">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span><span class="sxs-lookup"><span data-stu-id="a595e-286">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span></span>  
* <span data-ttu-id="a595e-287">A ***Table Scan*** does not include the **PartitionKey** and is very inefficient because it searches all of the partitions that make up your table in turn for any matching entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-287">A ***Table Scan*** does not include the **PartitionKey** and is very inefficient because it searches all of the partitions that make up your table in turn for any matching entities.</span></span> <span data-ttu-id="a595e-288">It will perform a table scan regardless of whether or not your filter uses the **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-288">It will perform a table scan regardless of whether or not your filter uses the **RowKey**.</span></span> <span data-ttu-id="a595e-289">For example: $filter=LastName eq 'Jones'</span><span class="sxs-lookup"><span data-stu-id="a595e-289">For example: $filter=LastName eq 'Jones'</span></span>  
* <span data-ttu-id="a595e-290">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span><span class="sxs-lookup"><span data-stu-id="a595e-290">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span></span> <span data-ttu-id="a595e-291">To avoid resorting the entities in the client, choose a **RowKey** that defines the most common sort order.</span><span class="sxs-lookup"><span data-stu-id="a595e-291">To avoid resorting the entities in the client, choose a **RowKey** that defines the most common sort order.</span></span>  

<span data-ttu-id="a595e-292">Note that using an "**or**" to specify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span><span class="sxs-lookup"><span data-stu-id="a595e-292">Note that using an "**or**" to specify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span></span> <span data-ttu-id="a595e-293">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span><span class="sxs-lookup"><span data-stu-id="a595e-293">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span></span>  

<span data-ttu-id="a595e-294">For examples of client-side code that use the Storage Client Library to execute efficient queries, see:</span><span class="sxs-lookup"><span data-stu-id="a595e-294">For examples of client-side code that use the Storage Client Library to execute efficient queries, see:</span></span>  

* [<span data-ttu-id="a595e-295">Executing a point query using the Storage Client Library</span><span class="sxs-lookup"><span data-stu-id="a595e-295">Executing a point query using the Storage Client Library</span></span>](#executing-a-point-query-using-the-storage-client-library)
* [<span data-ttu-id="a595e-296">Retrieving multiple entities using LINQ</span><span class="sxs-lookup"><span data-stu-id="a595e-296">Retrieving multiple entities using LINQ</span></span>](#retrieving-multiple-entities-using-linq)
* [<span data-ttu-id="a595e-297">Server-side projection</span><span class="sxs-lookup"><span data-stu-id="a595e-297">Server-side projection</span></span>](#server-side-projection)  

<span data-ttu-id="a595e-298">For examples of client-side code that can handle multiple entity types stored in the same table, see:</span><span class="sxs-lookup"><span data-stu-id="a595e-298">For examples of client-side code that can handle multiple entity types stored in the same table, see:</span></span>  

* [<span data-ttu-id="a595e-299">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-299">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a><span data-ttu-id="a595e-300">Choosing an appropriate PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a595e-300">Choosing an appropriate PartitionKey</span></span>
<span data-ttu-id="a595e-301">Your choice of **PartitionKey** should balance the need to enables the use of EGTs (to ensure consistency) against the requirement to distribute your entities across multiple partitions (to ensure a scalable solution).</span><span class="sxs-lookup"><span data-stu-id="a595e-301">Your choice of **PartitionKey** should balance the need to enables the use of EGTs (to ensure consistency) against the requirement to distribute your entities across multiple partitions (to ensure a scalable solution).</span></span>  

<span data-ttu-id="a595e-302">At one extreme, you could store all your entities in a single partition, but this may limit the scalability of your solution and would prevent the table service from being able to load-balance requests.</span><span class="sxs-lookup"><span data-stu-id="a595e-302">At one extreme, you could store all your entities in a single partition, but this may limit the scalability of your solution and would prevent the table service from being able to load-balance requests.</span></span> <span data-ttu-id="a595e-303">At the other extreme, you could store one entity per partition, which would be highly scalable and which enables the table service to load-balance requests, but which would prevent you from using entity group transactions.</span><span class="sxs-lookup"><span data-stu-id="a595e-303">At the other extreme, you could store one entity per partition, which would be highly scalable and which enables the table service to load-balance requests, but which would prevent you from using entity group transactions.</span></span>  

<span data-ttu-id="a595e-304">An ideal **PartitionKey** is one that enables you to use efficient queries and that has sufficient partitions to ensure your solution is scalable.</span><span class="sxs-lookup"><span data-stu-id="a595e-304">An ideal **PartitionKey** is one that enables you to use efficient queries and that has sufficient partitions to ensure your solution is scalable.</span></span> <span data-ttu-id="a595e-305">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-305">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span></span>

> [!NOTE]
> <span data-ttu-id="a595e-306">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="a595e-306">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span></span> <span data-ttu-id="a595e-307">You may have several entities that use a given UserID as the partition key.</span><span class="sxs-lookup"><span data-stu-id="a595e-307">You may have several entities that use a given UserID as the partition key.</span></span> <span data-ttu-id="a595e-308">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span><span class="sxs-lookup"><span data-stu-id="a595e-308">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span></span>
> 
> 

<span data-ttu-id="a595e-309">There are additional considerations in your choice of **PartitionKey** that relate to how you will insert, update, and delete entities: see the section [Design for data modification](#design-for-data-modification) below.</span><span class="sxs-lookup"><span data-stu-id="a595e-309">There are additional considerations in your choice of **PartitionKey** that relate to how you will insert, update, and delete entities: see the section [Design for data modification](#design-for-data-modification) below.</span></span>  

### <a name="optimizing-queries-for-the-table-service"></a><span data-ttu-id="a595e-310">Optimizing queries for the Table service</span><span class="sxs-lookup"><span data-stu-id="a595e-310">Optimizing queries for the Table service</span></span>
<span data-ttu-id="a595e-311">The Table service automatically indexes your entities using the **PartitionKey** and **RowKey** values in a single clustered index, hence the reason that point queries are the most efficient to use.</span><span class="sxs-lookup"><span data-stu-id="a595e-311">The Table service automatically indexes your entities using the **PartitionKey** and **RowKey** values in a single clustered index, hence the reason that point queries are the most efficient to use.</span></span> <span data-ttu-id="a595e-312">However, there are no indexes other than that on the clustered index on the **PartitionKey** and **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-312">However, there are no indexes other than that on the clustered index on the **PartitionKey** and **RowKey**.</span></span>

<span data-ttu-id="a595e-313">Many designs must meet requirements to enable lookup of entities based on multiple criteria.</span><span class="sxs-lookup"><span data-stu-id="a595e-313">Many designs must meet requirements to enable lookup of entities based on multiple criteria.</span></span> <span data-ttu-id="a595e-314">For example, locating employee entities based on email, employee id, or last name.</span><span class="sxs-lookup"><span data-stu-id="a595e-314">For example, locating employee entities based on email, employee id, or last name.</span></span> <span data-ttu-id="a595e-315">The following patterns in the section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around the fact that the Table service does not provide secondary indexes:</span><span class="sxs-lookup"><span data-stu-id="a595e-315">The following patterns in the section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around the fact that the Table service does not provide secondary indexes:</span></span>  

* <span data-ttu-id="a595e-316">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-316">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a595e-317">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-317">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a595e-318">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-318">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

### <a name="sorting-data-in-the-table-service"></a><span data-ttu-id="a595e-319">Sorting data in the Table service</span><span class="sxs-lookup"><span data-stu-id="a595e-319">Sorting data in the Table service</span></span>
<span data-ttu-id="a595e-320">The Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-320">The Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span></span> <span data-ttu-id="a595e-321">These keys are string values and to ensure that numeric values sort correctly, you should convert them to a fixed length and pad them with zeroes.</span><span class="sxs-lookup"><span data-stu-id="a595e-321">These keys are string values and to ensure that numeric values sort correctly, you should convert them to a fixed length and pad them with zeroes.</span></span> <span data-ttu-id="a595e-322">For example, if the employee id value you use as the **RowKey** is an integer value, you should convert employee id **123** to **00000123**.</span><span class="sxs-lookup"><span data-stu-id="a595e-322">For example, if the employee id value you use as the **RowKey** is an integer value, you should convert employee id **123** to **00000123**.</span></span>  

<span data-ttu-id="a595e-323">Many applications have requirements to use data sorted in different orders: for example, sorting employees by name, or by joining date.</span><span class="sxs-lookup"><span data-stu-id="a595e-323">Many applications have requirements to use data sorted in different orders: for example, sorting employees by name, or by joining date.</span></span> <span data-ttu-id="a595e-324">The following patterns in the section [Table Design Patterns](#table-design-patterns) address how to alternate sort orders for your entities:</span><span class="sxs-lookup"><span data-stu-id="a595e-324">The following patterns in the section [Table Design Patterns](#table-design-patterns) address how to alternate sort orders for your entities:</span></span>  

* <span data-ttu-id="a595e-325">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span><span class="sxs-lookup"><span data-stu-id="a595e-325">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>  
* <span data-ttu-id="a595e-326">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span><span class="sxs-lookup"><span data-stu-id="a595e-326">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>
* <span data-ttu-id="a595e-327">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span><span class="sxs-lookup"><span data-stu-id="a595e-327">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="design-for-data-modification"></a><span data-ttu-id="a595e-328">Design for data modification</span><span class="sxs-lookup"><span data-stu-id="a595e-328">Design for data modification</span></span>
<span data-ttu-id="a595e-329">This section focuses on the design considerations for optimizing inserts, updates, and deletes.</span><span class="sxs-lookup"><span data-stu-id="a595e-329">This section focuses on the design considerations for optimizing inserts, updates, and deletes.</span></span> <span data-ttu-id="a595e-330">In some cases, you will need to evaluate the trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although the techniques for managing the design trade-offs are different in a relational database).</span><span class="sxs-lookup"><span data-stu-id="a595e-330">In some cases, you will need to evaluate the trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although the techniques for managing the design trade-offs are different in a relational database).</span></span> <span data-ttu-id="a595e-331">The section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for the Table service and highlights some these trade-offs.</span><span class="sxs-lookup"><span data-stu-id="a595e-331">The section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for the Table service and highlights some these trade-offs.</span></span> <span data-ttu-id="a595e-332">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-332">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span></span>  

### <a name="optimizing-the-performance-of-insert-update-and-delete-operations"></a><span data-ttu-id="a595e-333">Optimizing the performance of insert, update, and delete operations</span><span class="sxs-lookup"><span data-stu-id="a595e-333">Optimizing the performance of insert, update, and delete operations</span></span>
<span data-ttu-id="a595e-334">To update or delete an entity, you must be able to identify it by using the **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-334">To update or delete an entity, you must be able to identify it by using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-335">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria to your choice to support point queries because you want to identify entities as efficiently as possible.</span><span class="sxs-lookup"><span data-stu-id="a595e-335">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria to your choice to support point queries because you want to identify entities as efficiently as possible.</span></span> <span data-ttu-id="a595e-336">You do not want to use an inefficient partition or table scan to locate an entity in order to discover the **PartitionKey** and **RowKey** values you need to update or delete it.</span><span class="sxs-lookup"><span data-stu-id="a595e-336">You do not want to use an inefficient partition or table scan to locate an entity in order to discover the **PartitionKey** and **RowKey** values you need to update or delete it.</span></span>  

<span data-ttu-id="a595e-337">The following patterns in the section [Table Design Patterns](#table-design-patterns) address optimizing the performance or your insert, update, and delete operations:</span><span class="sxs-lookup"><span data-stu-id="a595e-337">The following patterns in the section [Table Design Patterns](#table-design-patterns) address optimizing the performance or your insert, update, and delete operations:</span></span>  

* <span data-ttu-id="a595e-338">[High volume delete pattern](#high-volume-delete-pattern) - Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span><span class="sxs-lookup"><span data-stu-id="a595e-338">[High volume delete pattern](#high-volume-delete-pattern) - Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  
* <span data-ttu-id="a595e-339">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span><span class="sxs-lookup"><span data-stu-id="a595e-339">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  
* <span data-ttu-id="a595e-340">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities to store logical entities with more than 252 properties.</span><span class="sxs-lookup"><span data-stu-id="a595e-340">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  
* <span data-ttu-id="a595e-341">[Large entities pattern](#large-entities-pattern) - Use blob storage to store large property values.</span><span class="sxs-lookup"><span data-stu-id="a595e-341">[Large entities pattern](#large-entities-pattern) - Use blob storage to store large property values.</span></span>  

### <a name="ensuring-consistency-in-your-stored-entities"></a><span data-ttu-id="a595e-342">Ensuring consistency in your stored entities</span><span class="sxs-lookup"><span data-stu-id="a595e-342">Ensuring consistency in your stored entities</span></span>
<span data-ttu-id="a595e-343">The other key factor that influences your choice of keys for optimizing data modifications is how to ensure consistency by using atomic transactions.</span><span class="sxs-lookup"><span data-stu-id="a595e-343">The other key factor that influences your choice of keys for optimizing data modifications is how to ensure consistency by using atomic transactions.</span></span> <span data-ttu-id="a595e-344">You can only use an EGT to operate on entities stored in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-344">You can only use an EGT to operate on entities stored in the same partition.</span></span>  

<span data-ttu-id="a595e-345">The following patterns in the section [Table Design Patterns](#table-design-patterns) address managing consistency:</span><span class="sxs-lookup"><span data-stu-id="a595e-345">The following patterns in the section [Table Design Patterns](#table-design-patterns) address managing consistency:</span></span>  

* <span data-ttu-id="a595e-346">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-346">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a595e-347">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-347">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a595e-348">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span><span class="sxs-lookup"><span data-stu-id="a595e-348">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>
* <span data-ttu-id="a595e-349">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-349">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  
* <span data-ttu-id="a595e-350">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-350">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  
* <span data-ttu-id="a595e-351">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span><span class="sxs-lookup"><span data-stu-id="a595e-351">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

<span data-ttu-id="a595e-352">For information about entity group transactions, see the section [Entity Group Transactions](#entity-group-transactions).</span><span class="sxs-lookup"><span data-stu-id="a595e-352">For information about entity group transactions, see the section [Entity Group Transactions](#entity-group-transactions).</span></span>  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a><span data-ttu-id="a595e-353">Ensuring your design for efficient modifications facilitates efficient queries</span><span class="sxs-lookup"><span data-stu-id="a595e-353">Ensuring your design for efficient modifications facilitates efficient queries</span></span>
<span data-ttu-id="a595e-354">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is the case for your specific scenario.</span><span class="sxs-lookup"><span data-stu-id="a595e-354">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is the case for your specific scenario.</span></span> <span data-ttu-id="a595e-355">Some of the patterns in the section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account the number of each type of operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-355">Some of the patterns in the section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account the number of each type of operation.</span></span>  

<span data-ttu-id="a595e-356">The following patterns in the section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span><span class="sxs-lookup"><span data-stu-id="a595e-356">The following patterns in the section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span></span>  

* <span data-ttu-id="a595e-357">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-357">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  
* <span data-ttu-id="a595e-358">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span><span class="sxs-lookup"><span data-stu-id="a595e-358">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="encrypting-table-data"></a><span data-ttu-id="a595e-359">Encrypting Table Data</span><span class="sxs-lookup"><span data-stu-id="a595e-359">Encrypting Table Data</span></span>
<span data-ttu-id="a595e-360">The .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span><span class="sxs-lookup"><span data-stu-id="a595e-360">The .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span></span> <span data-ttu-id="a595e-361">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span><span class="sxs-lookup"><span data-stu-id="a595e-361">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>    

<span data-ttu-id="a595e-362">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span><span class="sxs-lookup"><span data-stu-id="a595e-362">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="a595e-363">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span><span class="sxs-lookup"><span data-stu-id="a595e-363">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="a595e-364">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span><span class="sxs-lookup"><span data-stu-id="a595e-364">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="a595e-365">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span><span class="sxs-lookup"><span data-stu-id="a595e-365">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="a595e-366">The delegate also provides for the possibility of logic around how properties are encrypted.</span><span class="sxs-lookup"><span data-stu-id="a595e-366">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="a595e-367">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-367">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

<span data-ttu-id="a595e-368">Note that merge is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="a595e-368">Note that merge is not currently supported.</span></span> <span data-ttu-id="a595e-369">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span><span class="sxs-lookup"><span data-stu-id="a595e-369">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="a595e-370">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span><span class="sxs-lookup"><span data-stu-id="a595e-370">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>     

<span data-ttu-id="a595e-371">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a595e-371">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>  

## <a name="modelling-relationships"></a><span data-ttu-id="a595e-372">Modelling relationships</span><span class="sxs-lookup"><span data-stu-id="a595e-372">Modelling relationships</span></span>
<span data-ttu-id="a595e-373">Building domain models is a key step in the design of complex systems.</span><span class="sxs-lookup"><span data-stu-id="a595e-373">Building domain models is a key step in the design of complex systems.</span></span> <span data-ttu-id="a595e-374">Typically, you use the modelling process to identify entities and the relationships between them as a way to understand the business domain and inform the design of your system.</span><span class="sxs-lookup"><span data-stu-id="a595e-374">Typically, you use the modelling process to identify entities and the relationships between them as a way to understand the business domain and inform the design of your system.</span></span> <span data-ttu-id="a595e-375">This section focuses on how you can translate some of the common relationship types found in domain models to designs for the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-375">This section focuses on how you can translate some of the common relationship types found in domain models to designs for the Table service.</span></span> <span data-ttu-id="a595e-376">The process of mapping from a logical data-model to a physical NoSQL based data-model is very different from that used when designing a relational database.</span><span class="sxs-lookup"><span data-stu-id="a595e-376">The process of mapping from a logical data-model to a physical NoSQL based data-model is very different from that used when designing a relational database.</span></span> <span data-ttu-id="a595e-377">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how the implementation of how the database works.</span><span class="sxs-lookup"><span data-stu-id="a595e-377">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how the implementation of how the database works.</span></span>  

### <a name="one-to-many-relationships"></a><span data-ttu-id="a595e-378">One-to-many relationships</span><span class="sxs-lookup"><span data-stu-id="a595e-378">One-to-many relationships</span></span>
<span data-ttu-id="a595e-379">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span><span class="sxs-lookup"><span data-stu-id="a595e-379">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span></span> <span data-ttu-id="a595e-380">There are several ways to implement one-to-many relationships in the Table service each with pros and cons that may be relevant to the particular scenario.</span><span class="sxs-lookup"><span data-stu-id="a595e-380">There are several ways to implement one-to-many relationships in the Table service each with pros and cons that may be relevant to the particular scenario.</span></span>  

<span data-ttu-id="a595e-381">Consider the example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span><span class="sxs-lookup"><span data-stu-id="a595e-381">Consider the example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span></span> <span data-ttu-id="a595e-382">One approach is to store separate department and employee entities such as these:</span><span class="sxs-lookup"><span data-stu-id="a595e-382">One approach is to store separate department and employee entities such as these:</span></span>  

![][1]

<span data-ttu-id="a595e-383">This example shows an implicit one-to-many relationship between the types based on the **PartitionKey** value.</span><span class="sxs-lookup"><span data-stu-id="a595e-383">This example shows an implicit one-to-many relationship between the types based on the **PartitionKey** value.</span></span> <span data-ttu-id="a595e-384">Each department can have many employees.</span><span class="sxs-lookup"><span data-stu-id="a595e-384">Each department can have many employees.</span></span>  

<span data-ttu-id="a595e-385">This example also shows a department entity and its related employee entities in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-385">This example also shows a department entity and its related employee entities in the same partition.</span></span> <span data-ttu-id="a595e-386">You could choose to use different partitions, tables, or even storage accounts for the different entity types.</span><span class="sxs-lookup"><span data-stu-id="a595e-386">You could choose to use different partitions, tables, or even storage accounts for the different entity types.</span></span>  

<span data-ttu-id="a595e-387">An alternative approach is to denormalize your data and store only employee entities with denormalized department data as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="a595e-387">An alternative approach is to denormalize your data and store only employee entities with denormalized department data as shown in the following example.</span></span> <span data-ttu-id="a595e-388">In this particular scenario, this denormalized approach may not be the best if you have a requirement to be able to change the details of a department manager because to do this you need to update every employee in the department.</span><span class="sxs-lookup"><span data-stu-id="a595e-388">In this particular scenario, this denormalized approach may not be the best if you have a requirement to be able to change the details of a department manager because to do this you need to update every employee in the department.</span></span>  

![][2]

<span data-ttu-id="a595e-389">For more information, see the [Denormalization pattern](#denormalization-pattern) later in this guide.</span><span class="sxs-lookup"><span data-stu-id="a595e-389">For more information, see the [Denormalization pattern](#denormalization-pattern) later in this guide.</span></span>  

<span data-ttu-id="a595e-390">The following table summarizes the pros and cons of each of the approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span><span class="sxs-lookup"><span data-stu-id="a595e-390">The following table summarizes the pros and cons of each of the approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span></span> <span data-ttu-id="a595e-391">You should also consider how often you expect to perform various operations: it may be acceptable to have a design that includes an expensive operation if that operation only happens infrequently.</span><span class="sxs-lookup"><span data-stu-id="a595e-391">You should also consider how often you expect to perform various operations: it may be acceptable to have a design that includes an expensive operation if that operation only happens infrequently.</span></span>  

<table>
<tr>
<th><span data-ttu-id="a595e-392">Approach</span><span class="sxs-lookup"><span data-stu-id="a595e-392">Approach</span></span></th>
<th><span data-ttu-id="a595e-393">Pros</span><span class="sxs-lookup"><span data-stu-id="a595e-393">Pros</span></span></th>
<th><span data-ttu-id="a595e-394">Cons</span><span class="sxs-lookup"><span data-stu-id="a595e-394">Cons</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-395">Separate entity types, same partition, same table</span><span class="sxs-lookup"><span data-stu-id="a595e-395">Separate entity types, same partition, same table</span></span></td>
<td>
<ul>
<li><span data-ttu-id="a595e-396">You can update a department entity with a single operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-396">You can update a department entity with a single operation.</span></span></li>
<li><span data-ttu-id="a595e-397">You can use an EGT to maintain consistency if you have a requirement to modify a department entity whenever you update/insert/delete an employee entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-397">You can use an EGT to maintain consistency if you have a requirement to modify a department entity whenever you update/insert/delete an employee entity.</span></span> <span data-ttu-id="a595e-398">For example if you maintain a departmental employee count for each department.</span><span class="sxs-lookup"><span data-stu-id="a595e-398">For example if you maintain a departmental employee count for each department.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="a595e-399">You may need to retrieve both an employee and a department entity for some client activities.</span><span class="sxs-lookup"><span data-stu-id="a595e-399">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="a595e-400">Storage operations happen in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-400">Storage operations happen in the same partition.</span></span> <span data-ttu-id="a595e-401">At high transaction volumes, this may result in a hotspot.</span><span class="sxs-lookup"><span data-stu-id="a595e-401">At high transaction volumes, this may result in a hotspot.</span></span></li>
<li><span data-ttu-id="a595e-402">You cannot move an employee to a new department using an EGT.</span><span class="sxs-lookup"><span data-stu-id="a595e-402">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="a595e-403">Separate entity types, different partitions or tables or storage accounts</span><span class="sxs-lookup"><span data-stu-id="a595e-403">Separate entity types, different partitions or tables or storage accounts</span></span></td>
<td>
<ul>
<li><span data-ttu-id="a595e-404">You can update a department entity or employee entity with a single operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-404">You can update a department entity or employee entity with a single operation.</span></span></li>
<li><span data-ttu-id="a595e-405">At high transaction volumes, this may help spread the load across more partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-405">At high transaction volumes, this may help spread the load across more partitions.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="a595e-406">You may need to retrieve both an employee and a department entity for some client activities.</span><span class="sxs-lookup"><span data-stu-id="a595e-406">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="a595e-407">You cannot use EGTs to maintain consistency when you update/insert/delete an employee and update a department.</span><span class="sxs-lookup"><span data-stu-id="a595e-407">You cannot use EGTs to maintain consistency when you update/insert/delete an employee and update a department.</span></span> <span data-ttu-id="a595e-408">For example, updating an employee count in a department entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-408">For example, updating an employee count in a department entity.</span></span></li>
<li><span data-ttu-id="a595e-409">You cannot move an employee to a new department using an EGT.</span><span class="sxs-lookup"><span data-stu-id="a595e-409">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="a595e-410">Denormalize into single entity type</span><span class="sxs-lookup"><span data-stu-id="a595e-410">Denormalize into single entity type</span></span></td>
<td>
<ul>
<li><span data-ttu-id="a595e-411">You can retrieve all the information you need with a single request.</span><span class="sxs-lookup"><span data-stu-id="a595e-411">You can retrieve all the information you need with a single request.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="a595e-412">It may be expensive to maintain consistency if you need to update department information (this would require you to update all the employees in a department).</span><span class="sxs-lookup"><span data-stu-id="a595e-412">It may be expensive to maintain consistency if you need to update department information (this would require you to update all the employees in a department).</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="a595e-413">How you choose between these options, and which of the pros and cons are most significant, depends on your specific application scenarios.</span><span class="sxs-lookup"><span data-stu-id="a595e-413">How you choose between these options, and which of the pros and cons are most significant, depends on your specific application scenarios.</span></span> <span data-ttu-id="a595e-414">For example, how often do you modify department entities; do all your employee queries need the additional departmental information; how close are you to the scalability limits on your partitions or your storage account?</span><span class="sxs-lookup"><span data-stu-id="a595e-414">For example, how often do you modify department entities; do all your employee queries need the additional departmental information; how close are you to the scalability limits on your partitions or your storage account?</span></span>  

### <a name="one-to-one-relationships"></a><span data-ttu-id="a595e-415">One-to-one relationships</span><span class="sxs-lookup"><span data-stu-id="a595e-415">One-to-one relationships</span></span>
<span data-ttu-id="a595e-416">Domain models may include one-to-one relationships between entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-416">Domain models may include one-to-one relationships between entities.</span></span> <span data-ttu-id="a595e-417">If you need to implement a one-to-one relationship in the Table service, you must also choose how to link the two related entities when you need to retrieve them both.</span><span class="sxs-lookup"><span data-stu-id="a595e-417">If you need to implement a one-to-one relationship in the Table service, you must also choose how to link the two related entities when you need to retrieve them both.</span></span> <span data-ttu-id="a595e-418">This link can be either implicit, based on a convention in the key values, or explicit by storing a link in the form of **PartitionKey** and **RowKey** values in each entity to its related entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-418">This link can be either implicit, based on a convention in the key values, or explicit by storing a link in the form of **PartitionKey** and **RowKey** values in each entity to its related entity.</span></span> <span data-ttu-id="a595e-419">For a discussion of whether you should store the related entities in the same partition, see the section [One-to-many relationships](#one-to-many-relationships).</span><span class="sxs-lookup"><span data-stu-id="a595e-419">For a discussion of whether you should store the related entities in the same partition, see the section [One-to-many relationships](#one-to-many-relationships).</span></span>  

<span data-ttu-id="a595e-420">Note that there are also implementation considerations that might lead you to implement one-to-one relationships in the Table service:</span><span class="sxs-lookup"><span data-stu-id="a595e-420">Note that there are also implementation considerations that might lead you to implement one-to-one relationships in the Table service:</span></span>  

* <span data-ttu-id="a595e-421">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span><span class="sxs-lookup"><span data-stu-id="a595e-421">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span></span>  
* <span data-ttu-id="a595e-422">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span><span class="sxs-lookup"><span data-stu-id="a595e-422">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span></span>  

### <a name="join-in-the-client"></a><span data-ttu-id="a595e-423">Join in the client</span><span class="sxs-lookup"><span data-stu-id="a595e-423">Join in the client</span></span>
<span data-ttu-id="a595e-424">Although there are ways to model relationships in the Table service, you should not forget that the two prime reasons for using the Table service are scalability and performance.</span><span class="sxs-lookup"><span data-stu-id="a595e-424">Although there are ways to model relationships in the Table service, you should not forget that the two prime reasons for using the Table service are scalability and performance.</span></span> <span data-ttu-id="a595e-425">If you find you are modelling many relationships that compromise the performance and scalability of your solution, you should ask yourself if it is necessary to build all the data relationships into your table design.</span><span class="sxs-lookup"><span data-stu-id="a595e-425">If you find you are modelling many relationships that compromise the performance and scalability of your solution, you should ask yourself if it is necessary to build all the data relationships into your table design.</span></span> <span data-ttu-id="a595e-426">You may be able to simplify the design and improve the scalability and performance of your solution if you let your client application perform any necessary joins.</span><span class="sxs-lookup"><span data-stu-id="a595e-426">You may be able to simplify the design and improve the scalability and performance of your solution if you let your client application perform any necessary joins.</span></span>  

<span data-ttu-id="a595e-427">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on the client.</span><span class="sxs-lookup"><span data-stu-id="a595e-427">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on the client.</span></span> <span data-ttu-id="a595e-428">This can avoid repeated roundtrips to retrieve the same data.</span><span class="sxs-lookup"><span data-stu-id="a595e-428">This can avoid repeated roundtrips to retrieve the same data.</span></span> <span data-ttu-id="a595e-429">In the examples we have looked at in this guide, the set of departments in a small organization is likely to be small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span><span class="sxs-lookup"><span data-stu-id="a595e-429">In the examples we have looked at in this guide, the set of departments in a small organization is likely to be small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span></span>  

### <a name="inheritance-relationships"></a><span data-ttu-id="a595e-430">Inheritance relationships</span><span class="sxs-lookup"><span data-stu-id="a595e-430">Inheritance relationships</span></span>
<span data-ttu-id="a595e-431">If your client application uses a set of classes that form part of an inheritance relationship to represent business entities, you can easily persist those entities in the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-431">If your client application uses a set of classes that form part of an inheritance relationship to represent business entities, you can easily persist those entities in the Table service.</span></span> <span data-ttu-id="a595e-432">For example, you might have the following set of classes defined in your client application where **Person** is an abstract class.</span><span class="sxs-lookup"><span data-stu-id="a595e-432">For example, you might have the following set of classes defined in your client application where **Person** is an abstract class.</span></span>

![][3]

<span data-ttu-id="a595e-433">You can persist instances of the two concrete classes in the Table service using a single Person table using entities in that look like this:</span><span class="sxs-lookup"><span data-stu-id="a595e-433">You can persist instances of the two concrete classes in the Table service using a single Person table using entities in that look like this:</span></span>  

![][4]

<span data-ttu-id="a595e-434">For more information about working with multiple entity types in the same table in client code, see the section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span><span class="sxs-lookup"><span data-stu-id="a595e-434">For more information about working with multiple entity types in the same table in client code, see the section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span></span> <span data-ttu-id="a595e-435">This provides examples of how to recognize the entity type in client code.</span><span class="sxs-lookup"><span data-stu-id="a595e-435">This provides examples of how to recognize the entity type in client code.</span></span>  

## <a name="table-design-patterns"></a><span data-ttu-id="a595e-436">Table Design Patterns</span><span class="sxs-lookup"><span data-stu-id="a595e-436">Table Design Patterns</span></span>
<span data-ttu-id="a595e-437">In previous sections, you have seen some detailed discussions about how to optimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span><span class="sxs-lookup"><span data-stu-id="a595e-437">In previous sections, you have seen some detailed discussions about how to optimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span></span> <span data-ttu-id="a595e-438">This section describes some patterns appropriate for use with Table service solutions.</span><span class="sxs-lookup"><span data-stu-id="a595e-438">This section describes some patterns appropriate for use with Table service solutions.</span></span> <span data-ttu-id="a595e-439">In addition, you will see how you can practically address some of the issues and trade-offs raised previously in this guide.</span><span class="sxs-lookup"><span data-stu-id="a595e-439">In addition, you will see how you can practically address some of the issues and trade-offs raised previously in this guide.</span></span> <span data-ttu-id="a595e-440">The following diagram summarizes the relationships between the different patterns:</span><span class="sxs-lookup"><span data-stu-id="a595e-440">The following diagram summarizes the relationships between the different patterns:</span></span>  

![][5]

<span data-ttu-id="a595e-441">The pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span><span class="sxs-lookup"><span data-stu-id="a595e-441">The pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span></span> <span data-ttu-id="a595e-442">There are of course many other patterns that are worth considering.</span><span class="sxs-lookup"><span data-stu-id="a595e-442">There are of course many other patterns that are worth considering.</span></span> <span data-ttu-id="a595e-443">For example, one of the key scenarios for Table Service is to use the [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from the [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span><span class="sxs-lookup"><span data-stu-id="a595e-443">For example, one of the key scenarios for Table Service is to use the [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from the [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span></span>  

### <a name="intra-partition-secondary-index-pattern"></a><span data-ttu-id="a595e-444">Intra-partition secondary index pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-444">Intra-partition secondary index pattern</span></span>
<span data-ttu-id="a595e-445">Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-445">Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span> <span data-ttu-id="a595e-446">Updates between copies can be kept consistent using EGT's.</span><span class="sxs-lookup"><span data-stu-id="a595e-446">Updates between copies can be kept consistent using EGT's.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-447">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-447">Context and problem</span></span>
<span data-ttu-id="a595e-448">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-448">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-449">This enables a client application to retrieve an entity efficiently using these values.</span><span class="sxs-lookup"><span data-stu-id="a595e-449">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="a595e-450">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span><span class="sxs-lookup"><span data-stu-id="a595e-450">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="a595e-451">A client can also retrieve entities sorted by employee id within each department.</span><span class="sxs-lookup"><span data-stu-id="a595e-451">A client can also retrieve entities sorted by employee id within each department.</span></span>

![][6]

<span data-ttu-id="a595e-452">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span><span class="sxs-lookup"><span data-stu-id="a595e-452">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="a595e-453">This is because the table service does not provide secondary indexes.</span><span class="sxs-lookup"><span data-stu-id="a595e-453">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="a595e-454">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span><span class="sxs-lookup"><span data-stu-id="a595e-454">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-455">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-455">Solution</span></span>
<span data-ttu-id="a595e-456">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span><span class="sxs-lookup"><span data-stu-id="a595e-456">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span></span> <span data-ttu-id="a595e-457">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id. The prefix values for the **RowKey**, "empid_" and "email_" enable you to query for a single employee or a range of employees by using a range of email addresses or employee ids.</span><span class="sxs-lookup"><span data-stu-id="a595e-457">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id. The prefix values for the **RowKey**, "empid_" and "email_" enable you to query for a single employee or a range of employees by using a range of email addresses or employee ids.</span></span>  

![][7]

<span data-ttu-id="a595e-458">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span><span class="sxs-lookup"><span data-stu-id="a595e-458">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="a595e-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span><span class="sxs-lookup"><span data-stu-id="a595e-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span></span>  
* <span data-ttu-id="a595e-460">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="a595e-460">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span></span>  

<span data-ttu-id="a595e-461">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-461">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="a595e-462">To find all the employees in the Sales department with an employee id in the range 000100 to 000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span><span class="sxs-lookup"><span data-stu-id="a595e-462">To find all the employees in the Sales department with an employee id in the range 000100 to 000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span></span>  
* <span data-ttu-id="a595e-463">To find all the employees in the Sales department with an email address starting with the letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span><span class="sxs-lookup"><span data-stu-id="a595e-463">To find all the employees in the Sales department with an email address starting with the letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span></span>  
  
  <span data-ttu-id="a595e-464">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-464">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-465">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-465">Issues and considerations</span></span>
<span data-ttu-id="a595e-466">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-466">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-467">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span><span class="sxs-lookup"><span data-stu-id="a595e-467">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="a595e-468">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span><span class="sxs-lookup"><span data-stu-id="a595e-468">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="a595e-469">Because the secondary index entities are stored in the same partition as the original entities, you should ensure that you do not exceed the scalability targets for an individual partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-469">Because the secondary index entities are stored in the same partition as the original entities, you should ensure that you do not exceed the scalability targets for an individual partition.</span></span>  
* <span data-ttu-id="a595e-470">You can keep your duplicate entities consistent with each other by using EGTs to update the two copies of the entity atomically.</span><span class="sxs-lookup"><span data-stu-id="a595e-470">You can keep your duplicate entities consistent with each other by using EGTs to update the two copies of the entity atomically.</span></span> <span data-ttu-id="a595e-471">This implies that you should store all copies of an entity in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-471">This implies that you should store all copies of an entity in the same partition.</span></span> <span data-ttu-id="a595e-472">For more information, see the section [Using Entity Group Transactions](#entity-group-transactions).</span><span class="sxs-lookup"><span data-stu-id="a595e-472">For more information, see the section [Using Entity Group Transactions](#entity-group-transactions).</span></span>  
* <span data-ttu-id="a595e-473">The value used for the **RowKey** must be unique for each entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-473">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="a595e-474">Consider using compound key values.</span><span class="sxs-lookup"><span data-stu-id="a595e-474">Consider using compound key values.</span></span>  
* <span data-ttu-id="a595e-475">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span><span class="sxs-lookup"><span data-stu-id="a595e-475">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="a595e-476">You do not necessarily need to duplicate all the properties of your entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-476">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="a595e-477">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span><span class="sxs-lookup"><span data-stu-id="a595e-477">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>

![][8]

* <span data-ttu-id="a595e-478">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query, than to use one query to locate an entity and another to lookup the required data.</span><span class="sxs-lookup"><span data-stu-id="a595e-478">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query, than to use one query to locate an entity and another to lookup the required data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-479">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-479">When to use this pattern</span></span>
<span data-ttu-id="a595e-480">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span><span class="sxs-lookup"><span data-stu-id="a595e-480">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="a595e-481">However, you should be sure that you do not exceed the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-481">However, you should be sure that you do not exceed the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-482">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-482">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-483">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-483">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-484">Inter-partition secondary index pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-484">Inter-partition secondary index pattern</span></span>](#inter-partition-secondary-index-pattern)
* [<span data-ttu-id="a595e-485">Compound key pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-485">Compound key pattern</span></span>](#compound-key-pattern)
* [<span data-ttu-id="a595e-486">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-486">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="a595e-487">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-487">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a><span data-ttu-id="a595e-488">Inter-partition secondary index pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-488">Inter-partition secondary index pattern</span></span>
<span data-ttu-id="a595e-489">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-489">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-490">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-490">Context and problem</span></span>
<span data-ttu-id="a595e-491">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-491">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-492">This enables a client application to retrieve an entity efficiently using these values.</span><span class="sxs-lookup"><span data-stu-id="a595e-492">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="a595e-493">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span><span class="sxs-lookup"><span data-stu-id="a595e-493">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="a595e-494">A client can also retrieve entities sorted by employee id within each department.</span><span class="sxs-lookup"><span data-stu-id="a595e-494">A client can also retrieve entities sorted by employee id within each department.</span></span>  

![][9]

<span data-ttu-id="a595e-495">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span><span class="sxs-lookup"><span data-stu-id="a595e-495">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="a595e-496">This is because the table service does not provide secondary indexes.</span><span class="sxs-lookup"><span data-stu-id="a595e-496">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="a595e-497">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span><span class="sxs-lookup"><span data-stu-id="a595e-497">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

<span data-ttu-id="a595e-498">You are anticipating a very high volume of transactions against these entities and want to minimize the risk of the Table service throttling your client.</span><span class="sxs-lookup"><span data-stu-id="a595e-498">You are anticipating a very high volume of transactions against these entities and want to minimize the risk of the Table service throttling your client.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-499">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-499">Solution</span></span>
<span data-ttu-id="a595e-500">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-500">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-501">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id. The prefix values for the **PartitionKey**, "empid_" and "email_" enable you to identify which index you want to use for a query.</span><span class="sxs-lookup"><span data-stu-id="a595e-501">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id. The prefix values for the **PartitionKey**, "empid_" and "email_" enable you to identify which index you want to use for a query.</span></span>  

![][10]

<span data-ttu-id="a595e-502">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span><span class="sxs-lookup"><span data-stu-id="a595e-502">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="a595e-503">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span><span class="sxs-lookup"><span data-stu-id="a595e-503">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span></span>
* <span data-ttu-id="a595e-504">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="a595e-504">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span></span>  

<span data-ttu-id="a595e-505">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-505">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="a595e-506">To find all the employees in the Sales department with an employee id in the range **000100** to **000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span><span class="sxs-lookup"><span data-stu-id="a595e-506">To find all the employees in the Sales department with an employee id in the range **000100** to **000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span></span>  
* <span data-ttu-id="a595e-507">To find all the employees in the Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span><span class="sxs-lookup"><span data-stu-id="a595e-507">To find all the employees in the Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span></span>  

<span data-ttu-id="a595e-508">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-508">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-509">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-509">Issues and considerations</span></span>
<span data-ttu-id="a595e-510">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-510">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-511">You can keep your duplicate entities eventually consistent with each other by using the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain the primary and secondary index entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-511">You can keep your duplicate entities eventually consistent with each other by using the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain the primary and secondary index entities.</span></span>  
* <span data-ttu-id="a595e-512">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span><span class="sxs-lookup"><span data-stu-id="a595e-512">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="a595e-513">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span><span class="sxs-lookup"><span data-stu-id="a595e-513">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="a595e-514">The value used for the **RowKey** must be unique for each entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-514">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="a595e-515">Consider using compound key values.</span><span class="sxs-lookup"><span data-stu-id="a595e-515">Consider using compound key values.</span></span>  
* <span data-ttu-id="a595e-516">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span><span class="sxs-lookup"><span data-stu-id="a595e-516">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="a595e-517">You do not necessarily need to duplicate all the properties of your entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-517">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="a595e-518">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span><span class="sxs-lookup"><span data-stu-id="a595e-518">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>
  
  ![][11]
* <span data-ttu-id="a595e-519">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query than to use one query to locate an entity using the secondary index and another to lookup the required data in the primary index.</span><span class="sxs-lookup"><span data-stu-id="a595e-519">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query than to use one query to locate an entity using the secondary index and another to lookup the required data in the primary index.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-520">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-520">When to use this pattern</span></span>
<span data-ttu-id="a595e-521">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span><span class="sxs-lookup"><span data-stu-id="a595e-521">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="a595e-522">Use this pattern when you want to avoid exceeding the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-522">Use this pattern when you want to avoid exceeding the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-523">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-523">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-524">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-524">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-525">Eventually consistent transactions pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-525">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="a595e-526">Intra-partition secondary index pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-526">Intra-partition secondary index pattern</span></span>](#intra-partition-secondary-index-pattern)  
* [<span data-ttu-id="a595e-527">Compound key pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-527">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a595e-528">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-528">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a595e-529">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-529">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a><span data-ttu-id="a595e-530">Eventually consistent transactions pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-530">Eventually consistent transactions pattern</span></span>
<span data-ttu-id="a595e-531">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span><span class="sxs-lookup"><span data-stu-id="a595e-531">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-532">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-532">Context and problem</span></span>
<span data-ttu-id="a595e-533">EGTs enable atomic transactions across multiple entities that share the same partition key.</span><span class="sxs-lookup"><span data-stu-id="a595e-533">EGTs enable atomic transactions across multiple entities that share the same partition key.</span></span> <span data-ttu-id="a595e-534">For performance and scalability reasons, you might decide to store entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs to maintain consistency.</span><span class="sxs-lookup"><span data-stu-id="a595e-534">For performance and scalability reasons, you might decide to store entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs to maintain consistency.</span></span> <span data-ttu-id="a595e-535">For example, you might have a requirement to maintain eventual consistency between:</span><span class="sxs-lookup"><span data-stu-id="a595e-535">For example, you might have a requirement to maintain eventual consistency between:</span></span>  

* <span data-ttu-id="a595e-536">Entities stored in two different partitions in the same table, in different tables, in in different storage accounts.</span><span class="sxs-lookup"><span data-stu-id="a595e-536">Entities stored in two different partitions in the same table, in different tables, in in different storage accounts.</span></span>  
* <span data-ttu-id="a595e-537">An entity stored in the Table service and a blob stored in the Blob service.</span><span class="sxs-lookup"><span data-stu-id="a595e-537">An entity stored in the Table service and a blob stored in the Blob service.</span></span>  
* <span data-ttu-id="a595e-538">An entity stored in the Table service and a file in a file system.</span><span class="sxs-lookup"><span data-stu-id="a595e-538">An entity stored in the Table service and a file in a file system.</span></span>  
* <span data-ttu-id="a595e-539">An entity store in the Table service yet indexed using the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="a595e-539">An entity store in the Table service yet indexed using the Azure Search service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-540">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-540">Solution</span></span>
<span data-ttu-id="a595e-541">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span><span class="sxs-lookup"><span data-stu-id="a595e-541">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span></span>
<span data-ttu-id="a595e-542">To illustrate this approach, assume you have a requirement to be able to archive old employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-542">To illustrate this approach, assume you have a requirement to be able to archive old employee entities.</span></span> <span data-ttu-id="a595e-543">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span><span class="sxs-lookup"><span data-stu-id="a595e-543">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span></span> <span data-ttu-id="a595e-544">To implement this requirement you store active employees in the **Current** table and old employees in the **Archive** table.</span><span class="sxs-lookup"><span data-stu-id="a595e-544">To implement this requirement you store active employees in the **Current** table and old employees in the **Archive** table.</span></span> <span data-ttu-id="a595e-545">Archiving an employee requires you to delete the entity from the **Current** table and add the entity to the **Archive** table, but you cannot use an EGT to perform these two operations.</span><span class="sxs-lookup"><span data-stu-id="a595e-545">Archiving an employee requires you to delete the entity from the **Current** table and add the entity to the **Archive** table, but you cannot use an EGT to perform these two operations.</span></span> <span data-ttu-id="a595e-546">To avoid the risk that a failure causes an entity to appear in both or neither tables, the archive operation must be eventually consistent.</span><span class="sxs-lookup"><span data-stu-id="a595e-546">To avoid the risk that a failure causes an entity to appear in both or neither tables, the archive operation must be eventually consistent.</span></span> <span data-ttu-id="a595e-547">The following sequence diagram outlines the steps in this operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-547">The following sequence diagram outlines the steps in this operation.</span></span> <span data-ttu-id="a595e-548">More detail is provided for exception paths in the text following.</span><span class="sxs-lookup"><span data-stu-id="a595e-548">More detail is provided for exception paths in the text following.</span></span>  

![][12]

<span data-ttu-id="a595e-549">A client initiates the archive operation by placing a message on an Azure queue, in this example to archive employee #456.</span><span class="sxs-lookup"><span data-stu-id="a595e-549">A client initiates the archive operation by placing a message on an Azure queue, in this example to archive employee #456.</span></span> <span data-ttu-id="a595e-550">A worker role polls the queue for new messages; when it finds one, it reads the message and leaves a hidden copy on the queue.</span><span class="sxs-lookup"><span data-stu-id="a595e-550">A worker role polls the queue for new messages; when it finds one, it reads the message and leaves a hidden copy on the queue.</span></span> <span data-ttu-id="a595e-551">The worker role next fetches a copy of the entity from the **Current** table, inserts a copy in the **Archive** table, and then deletes the original from the **Current** table.</span><span class="sxs-lookup"><span data-stu-id="a595e-551">The worker role next fetches a copy of the entity from the **Current** table, inserts a copy in the **Archive** table, and then deletes the original from the **Current** table.</span></span> <span data-ttu-id="a595e-552">Finally, if there were no errors from the previous steps, the worker role deletes the hidden message from the queue.</span><span class="sxs-lookup"><span data-stu-id="a595e-552">Finally, if there were no errors from the previous steps, the worker role deletes the hidden message from the queue.</span></span>  

<span data-ttu-id="a595e-553">In this example, step 4 inserts the employee into the **Archive** table.</span><span class="sxs-lookup"><span data-stu-id="a595e-553">In this example, step 4 inserts the employee into the **Archive** table.</span></span> <span data-ttu-id="a595e-554">It could add the employee to a blob in the Blob service or a file in a file system.</span><span class="sxs-lookup"><span data-stu-id="a595e-554">It could add the employee to a blob in the Blob service or a file in a file system.</span></span>  

#### <a name="recovering-from-failures"></a><span data-ttu-id="a595e-555">Recovering from failures</span><span class="sxs-lookup"><span data-stu-id="a595e-555">Recovering from failures</span></span>
<span data-ttu-id="a595e-556">It is important that the operations in steps **4** and **5** must be *idempotent* in case the worker role needs to restart the archive operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-556">It is important that the operations in steps **4** and **5** must be *idempotent* in case the worker role needs to restart the archive operation.</span></span> <span data-ttu-id="a595e-557">If you are using the Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in the client library you are using.</span><span class="sxs-lookup"><span data-stu-id="a595e-557">If you are using the Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in the client library you are using.</span></span> <span data-ttu-id="a595e-558">If you are using another storage system, you must use an appropriate idempotent operation.</span><span class="sxs-lookup"><span data-stu-id="a595e-558">If you are using another storage system, you must use an appropriate idempotent operation.</span></span>  

<span data-ttu-id="a595e-559">If the worker role never completes step **6**, then after a timeout the message reappears on the queue ready for the worker role to try to reprocess it.</span><span class="sxs-lookup"><span data-stu-id="a595e-559">If the worker role never completes step **6**, then after a timeout the message reappears on the queue ready for the worker role to try to reprocess it.</span></span> <span data-ttu-id="a595e-560">The worker role can check how many times a message on the queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it to a separate queue.</span><span class="sxs-lookup"><span data-stu-id="a595e-560">The worker role can check how many times a message on the queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it to a separate queue.</span></span> <span data-ttu-id="a595e-561">For more information about reading queue messages and checking the dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-561">For more information about reading queue messages and checking the dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span></span>  

<span data-ttu-id="a595e-562">Some errors from the Table and Queue services are transient errors, and your client application should include suitable retry logic to handle them.</span><span class="sxs-lookup"><span data-stu-id="a595e-562">Some errors from the Table and Queue services are transient errors, and your client application should include suitable retry logic to handle them.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-563">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-563">Issues and considerations</span></span>
<span data-ttu-id="a595e-564">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-564">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-565">This solution does not provide for transaction isolation.</span><span class="sxs-lookup"><span data-stu-id="a595e-565">This solution does not provide for transaction isolation.</span></span> <span data-ttu-id="a595e-566">For example, a client could read the **Current** and **Archive** tables when the worker role was between steps **4** and **5**, and see an inconsistent view of the data.</span><span class="sxs-lookup"><span data-stu-id="a595e-566">For example, a client could read the **Current** and **Archive** tables when the worker role was between steps **4** and **5**, and see an inconsistent view of the data.</span></span> <span data-ttu-id="a595e-567">Note that the data will be consistent eventually.</span><span class="sxs-lookup"><span data-stu-id="a595e-567">Note that the data will be consistent eventually.</span></span>  
* <span data-ttu-id="a595e-568">You must be sure that steps 4 and 5 are idempotent in order to ensure eventual consistency.</span><span class="sxs-lookup"><span data-stu-id="a595e-568">You must be sure that steps 4 and 5 are idempotent in order to ensure eventual consistency.</span></span>  
* <span data-ttu-id="a595e-569">You can scale the solution by using multiple queues and worker role instances.</span><span class="sxs-lookup"><span data-stu-id="a595e-569">You can scale the solution by using multiple queues and worker role instances.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-570">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-570">When to use this pattern</span></span>
<span data-ttu-id="a595e-571">Use this pattern when you want to guarantee eventual consistency between entities that exist in different partitions or tables.</span><span class="sxs-lookup"><span data-stu-id="a595e-571">Use this pattern when you want to guarantee eventual consistency between entities that exist in different partitions or tables.</span></span> <span data-ttu-id="a595e-572">You can extend this pattern to ensure eventual consistency for operations across the Table service and the Blob service and other non-Azure Storage data sources such as database or the file system.</span><span class="sxs-lookup"><span data-stu-id="a595e-572">You can extend this pattern to ensure eventual consistency for operations across the Table service and the Blob service and other non-Azure Storage data sources such as database or the file system.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-573">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-573">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-574">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-574">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-575">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-575">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a595e-576">Merge or replace</span><span class="sxs-lookup"><span data-stu-id="a595e-576">Merge or replace</span></span>](#merge-or-replace)  

> [!NOTE]
> <span data-ttu-id="a595e-577">If transaction isolation is important to your solution, you should consider redesigning your tables to enable you to use EGTs.</span><span class="sxs-lookup"><span data-stu-id="a595e-577">If transaction isolation is important to your solution, you should consider redesigning your tables to enable you to use EGTs.</span></span>  
> 
> 

### <a name="index-entities-pattern"></a><span data-ttu-id="a595e-578">Index Entities Pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-578">Index Entities Pattern</span></span>
<span data-ttu-id="a595e-579">Maintain index entities to enable efficient searches that return lists of entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-579">Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-580">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-580">Context and problem</span></span>
<span data-ttu-id="a595e-581">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-581">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-582">This enables a client application to retrieve an entity efficiently using a point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-582">This enables a client application to retrieve an entity efficiently using a point query.</span></span> <span data-ttu-id="a595e-583">For example, using the table structure shown below, a client application can efficiently retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey**).</span><span class="sxs-lookup"><span data-stu-id="a595e-583">For example, using the table structure shown below, a client application can efficiently retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey**).</span></span>  

![][13]

<span data-ttu-id="a595e-584">If you also want to be able to retrieve a list of employee entities based on the value of another non-unique property, such as their last name, you must use a less efficient partition scan to find matches rather than using an index to look them up directly.</span><span class="sxs-lookup"><span data-stu-id="a595e-584">If you also want to be able to retrieve a list of employee entities based on the value of another non-unique property, such as their last name, you must use a less efficient partition scan to find matches rather than using an index to look them up directly.</span></span> <span data-ttu-id="a595e-585">This is because the table service does not provide secondary indexes.</span><span class="sxs-lookup"><span data-stu-id="a595e-585">This is because the table service does not provide secondary indexes.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-586">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-586">Solution</span></span>
<span data-ttu-id="a595e-587">To enable lookup by last name with the entity structure shown above, you must maintain lists of employee ids.</span><span class="sxs-lookup"><span data-stu-id="a595e-587">To enable lookup by last name with the entity structure shown above, you must maintain lists of employee ids.</span></span> <span data-ttu-id="a595e-588">If you want to retrieve the employee entities with a particular last name, such as Jones, you must first locate the list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-588">If you want to retrieve the employee entities with a particular last name, such as Jones, you must first locate the list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span></span> <span data-ttu-id="a595e-589">There are three main options for storing the lists of employee ids:</span><span class="sxs-lookup"><span data-stu-id="a595e-589">There are three main options for storing the lists of employee ids:</span></span>  

* <span data-ttu-id="a595e-590">Use blob storage.</span><span class="sxs-lookup"><span data-stu-id="a595e-590">Use blob storage.</span></span>  
* <span data-ttu-id="a595e-591">Create index entities in the same partition as the employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-591">Create index entities in the same partition as the employee entities.</span></span>  
* <span data-ttu-id="a595e-592">Create index entities in a separate partition or table.</span><span class="sxs-lookup"><span data-stu-id="a595e-592">Create index entities in a separate partition or table.</span></span>  

<span data-ttu-id="a595e-593"><u>Option #1: Use blob storage</u></span><span class="sxs-lookup"><span data-stu-id="a595e-593"><u>Option #1: Use blob storage</u></span></span>  

<span data-ttu-id="a595e-594">For the first option, you create a blob for every unique last name, and in each blob store a list of the **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span><span class="sxs-lookup"><span data-stu-id="a595e-594">For the first option, you create a blob for every unique last name, and in each blob store a list of the **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span></span> <span data-ttu-id="a595e-595">When you add or delete an employee you should ensure that the content of the relevant blob is eventually consistent with the employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-595">When you add or delete an employee you should ensure that the content of the relevant blob is eventually consistent with the employee entities.</span></span>  

<span data-ttu-id="a595e-596"><u>Option #2:</u> Create index entities in the same partition</span><span class="sxs-lookup"><span data-stu-id="a595e-596"><u>Option #2:</u> Create index entities in the same partition</span></span>  

<span data-ttu-id="a595e-597">For the second option, use index entities that store the following data:</span><span class="sxs-lookup"><span data-stu-id="a595e-597">For the second option, use index entities that store the following data:</span></span>  

![][14]

<span data-ttu-id="a595e-598">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-598">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="a595e-599">The following steps outline the process you should follow when you are adding a new employee if you are using the second option.</span><span class="sxs-lookup"><span data-stu-id="a595e-599">The following steps outline the process you should follow when you are adding a new employee if you are using the second option.</span></span> <span data-ttu-id="a595e-600">In this example, we are adding an employee with Id 000152 and a last name Jones in the Sales department:</span><span class="sxs-lookup"><span data-stu-id="a595e-600">In this example, we are adding an employee with Id 000152 and a last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="a595e-601">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span><span class="sxs-lookup"><span data-stu-id="a595e-601">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span> <span data-ttu-id="a595e-602">Save the ETag of this entity to use in step 2.</span><span class="sxs-lookup"><span data-stu-id="a595e-602">Save the ETag of this entity to use in step 2.</span></span>  
2. <span data-ttu-id="a595e-603">Create an entity group transaction (that is, a batch operation) that inserts the new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates the index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding the new employee id to the list in the EmployeeIDs field.</span><span class="sxs-lookup"><span data-stu-id="a595e-603">Create an entity group transaction (that is, a batch operation) that inserts the new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates the index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding the new employee id to the list in the EmployeeIDs field.</span></span> <span data-ttu-id="a595e-604">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span><span class="sxs-lookup"><span data-stu-id="a595e-604">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span></span>  
3. <span data-ttu-id="a595e-605">If the entity group transaction fails because of an optimistic concurrency error (someone else has just modified the index entity), then you need to start over at step 1 again.</span><span class="sxs-lookup"><span data-stu-id="a595e-605">If the entity group transaction fails because of an optimistic concurrency error (someone else has just modified the index entity), then you need to start over at step 1 again.</span></span>  

<span data-ttu-id="a595e-606">You can use a similar approach to deleting an employee if you are using the second option.</span><span class="sxs-lookup"><span data-stu-id="a595e-606">You can use a similar approach to deleting an employee if you are using the second option.</span></span> <span data-ttu-id="a595e-607">Changing an employee's last name is slightly more complex because you will need to execute an entity group transaction that updates three entities: the employee entity, the index entity for the old last name, and the index entity for the new last name.</span><span class="sxs-lookup"><span data-stu-id="a595e-607">Changing an employee's last name is slightly more complex because you will need to execute an entity group transaction that updates three entities: the employee entity, the index entity for the old last name, and the index entity for the new last name.</span></span> <span data-ttu-id="a595e-608">You must retrieve each entity before making any changes in order to retrieve the ETag values that you can then use to perform the updates using optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="a595e-608">You must retrieve each entity before making any changes in order to retrieve the ETag values that you can then use to perform the updates using optimistic concurrency.</span></span>  

<span data-ttu-id="a595e-609">The following steps outline the process you should follow when you need to look up all the employees with a given last name in a department if you are using the second option.</span><span class="sxs-lookup"><span data-stu-id="a595e-609">The following steps outline the process you should follow when you need to look up all the employees with a given last name in a department if you are using the second option.</span></span> <span data-ttu-id="a595e-610">In this example, we are looking up all the employees with last name Jones in the Sales department:</span><span class="sxs-lookup"><span data-stu-id="a595e-610">In this example, we are looking up all the employees with last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="a595e-611">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span><span class="sxs-lookup"><span data-stu-id="a595e-611">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span>  
2. <span data-ttu-id="a595e-612">Parse the list of employee Ids in the EmployeeIDs field.</span><span class="sxs-lookup"><span data-stu-id="a595e-612">Parse the list of employee Ids in the EmployeeIDs field.</span></span>  
3. <span data-ttu-id="a595e-613">If you need additional information about each of these employees (such as their email addresses), retrieve each of the employee entities using **PartitionKey** value "Sales" and **RowKey** values from the list of employees you obtained in step 2.</span><span class="sxs-lookup"><span data-stu-id="a595e-613">If you need additional information about each of these employees (such as their email addresses), retrieve each of the employee entities using **PartitionKey** value "Sales" and **RowKey** values from the list of employees you obtained in step 2.</span></span>  

<span data-ttu-id="a595e-614"><u>Option #3:</u> Create index entities in a separate partition or table</span><span class="sxs-lookup"><span data-stu-id="a595e-614"><u>Option #3:</u> Create index entities in a separate partition or table</span></span>  

<span data-ttu-id="a595e-615">For the third option, use index entities that store the following data:</span><span class="sxs-lookup"><span data-stu-id="a595e-615">For the third option, use index entities that store the following data:</span></span>  

![][15]

<span data-ttu-id="a595e-616">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="a595e-616">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="a595e-617">With the third option, you cannot use EGTs to maintain consistency because the index entities are in a separate partition from the employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-617">With the third option, you cannot use EGTs to maintain consistency because the index entities are in a separate partition from the employee entities.</span></span> <span data-ttu-id="a595e-618">You should ensure that the index entities are eventually consistent with the employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-618">You should ensure that the index entities are eventually consistent with the employee entities.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-619">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-619">Issues and considerations</span></span>
<span data-ttu-id="a595e-620">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-620">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-621">This solution requires at least two queries to retrieve matching entities: one to query the index entities to obtain the list of **RowKey** values, and then queries to retrieve each entity in the list.</span><span class="sxs-lookup"><span data-stu-id="a595e-621">This solution requires at least two queries to retrieve matching entities: one to query the index entities to obtain the list of **RowKey** values, and then queries to retrieve each entity in the list.</span></span>  
* <span data-ttu-id="a595e-622">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in the solution assume that the list of employee ids for any given last name is never greater than 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a595e-622">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in the solution assume that the list of employee ids for any given last name is never greater than 1 MB.</span></span> <span data-ttu-id="a595e-623">If the list of employee ids is likely to be greater than 1 MB in size, use option #1 and store the index data in blob storage.</span><span class="sxs-lookup"><span data-stu-id="a595e-623">If the list of employee ids is likely to be greater than 1 MB in size, use option #1 and store the index data in blob storage.</span></span>  
* <span data-ttu-id="a595e-624">If you use option #2 (using EGTs to handle adding and deleting employees, and changing an employee's last name) you must evaluate if the volume of transactions will approach the scalability limits in a given partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-624">If you use option #2 (using EGTs to handle adding and deleting employees, and changing an employee's last name) you must evaluate if the volume of transactions will approach the scalability limits in a given partition.</span></span> <span data-ttu-id="a595e-625">If this is the case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues to handle the update requests and enables you to store your index entities in a separate partition from the employee entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-625">If this is the case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues to handle the update requests and enables you to store your index entities in a separate partition from the employee entities.</span></span>  
* <span data-ttu-id="a595e-626">Option #2 in this solution assumes that you want to look up by last name within a department: for example, you want to retrieve a list of employees with a last name Jones in the Sales department.</span><span class="sxs-lookup"><span data-stu-id="a595e-626">Option #2 in this solution assumes that you want to look up by last name within a department: for example, you want to retrieve a list of employees with a last name Jones in the Sales department.</span></span> <span data-ttu-id="a595e-627">If you want to be able to look up all the employees with a last name Jones across the whole organization, use either option #1 or option #3.</span><span class="sxs-lookup"><span data-stu-id="a595e-627">If you want to be able to look up all the employees with a last name Jones across the whole organization, use either option #1 or option #3.</span></span>
* <span data-ttu-id="a595e-628">You can implement a queue-based solution that delivers eventual consistency (see the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span><span class="sxs-lookup"><span data-stu-id="a595e-628">You can implement a queue-based solution that delivers eventual consistency (see the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-629">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-629">When to use this pattern</span></span>
<span data-ttu-id="a595e-630">Use this pattern when you want to lookup a set of entities that all share a common property value, such as all employees with the last name Jones.</span><span class="sxs-lookup"><span data-stu-id="a595e-630">Use this pattern when you want to lookup a set of entities that all share a common property value, such as all employees with the last name Jones.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-631">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-631">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-632">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-632">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-633">Compound key pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-633">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a595e-634">Eventually consistent transactions pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-634">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="a595e-635">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-635">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a595e-636">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-636">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a><span data-ttu-id="a595e-637">Denormalization pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-637">Denormalization pattern</span></span>
<span data-ttu-id="a595e-638">Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-638">Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-639">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-639">Context and problem</span></span>
<span data-ttu-id="a595e-640">In a relational database, you typically normalize data to remove duplication resulting in queries that retrieve data from multiple tables.</span><span class="sxs-lookup"><span data-stu-id="a595e-640">In a relational database, you typically normalize data to remove duplication resulting in queries that retrieve data from multiple tables.</span></span> <span data-ttu-id="a595e-641">If you normalize your data in Azure tables, you must make multiple round trips from the client to the server to retrieve your related data.</span><span class="sxs-lookup"><span data-stu-id="a595e-641">If you normalize your data in Azure tables, you must make multiple round trips from the client to the server to retrieve your related data.</span></span> <span data-ttu-id="a595e-642">For example, with the table structure shown below you need two round trips to retrieve the details for a department: one to fetch the department entity that includes the manager's id, and then another request to fetch the manager's details in an employee entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-642">For example, with the table structure shown below you need two round trips to retrieve the details for a department: one to fetch the department entity that includes the manager's id, and then another request to fetch the manager's details in an employee entity.</span></span>  

![][16]

#### <a name="solution"></a><span data-ttu-id="a595e-643">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-643">Solution</span></span>
<span data-ttu-id="a595e-644">Instead of storing the data in two separate entities, denormalize the data and keep a copy of the manager's details in the department entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-644">Instead of storing the data in two separate entities, denormalize the data and keep a copy of the manager's details in the department entity.</span></span> <span data-ttu-id="a595e-645">For example:</span><span class="sxs-lookup"><span data-stu-id="a595e-645">For example:</span></span>  

![][17]

<span data-ttu-id="a595e-646">With department entities stored with these properties, you can now retrieve all the details you need about a department using a point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-646">With department entities stored with these properties, you can now retrieve all the details you need about a department using a point query.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-647">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-647">Issues and considerations</span></span>
<span data-ttu-id="a595e-648">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-648">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-649">There is some cost overhead associated with storing some data twice.</span><span class="sxs-lookup"><span data-stu-id="a595e-649">There is some cost overhead associated with storing some data twice.</span></span> <span data-ttu-id="a595e-650">The performance benefit (resulting from fewer requests to the storage service) typically outweighs the marginal increase in storage costs (and this cost is partially offset by a reduction in the number of transactions you require to fetch the details of a department).</span><span class="sxs-lookup"><span data-stu-id="a595e-650">The performance benefit (resulting from fewer requests to the storage service) typically outweighs the marginal increase in storage costs (and this cost is partially offset by a reduction in the number of transactions you require to fetch the details of a department).</span></span>  
* <span data-ttu-id="a595e-651">You must maintain the consistency of the two entities that store information about managers.</span><span class="sxs-lookup"><span data-stu-id="a595e-651">You must maintain the consistency of the two entities that store information about managers.</span></span> <span data-ttu-id="a595e-652">You can handle the consistency issue by using EGTs to update multiple entities in a single atomic transaction: in this case, the department entity, and the employee entity for the department manager are stored in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-652">You can handle the consistency issue by using EGTs to update multiple entities in a single atomic transaction: in this case, the department entity, and the employee entity for the department manager are stored in the same partition.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-653">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-653">When to use this pattern</span></span>
<span data-ttu-id="a595e-654">Use this pattern when you frequently need to look up related information.</span><span class="sxs-lookup"><span data-stu-id="a595e-654">Use this pattern when you frequently need to look up related information.</span></span> <span data-ttu-id="a595e-655">This pattern reduces the number of queries your client must make to retrieve the data it requires.</span><span class="sxs-lookup"><span data-stu-id="a595e-655">This pattern reduces the number of queries your client must make to retrieve the data it requires.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-656">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-656">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-657">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-657">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-658">Compound key pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-658">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a595e-659">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-659">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a595e-660">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-660">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a><span data-ttu-id="a595e-661">Compound key pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-661">Compound key pattern</span></span>
<span data-ttu-id="a595e-662">Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-662">Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-663">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-663">Context and problem</span></span>
<span data-ttu-id="a595e-664">In a relational database, it is quite natural to use joins in queries to return related pieces of data to the client in a single query.</span><span class="sxs-lookup"><span data-stu-id="a595e-664">In a relational database, it is quite natural to use joins in queries to return related pieces of data to the client in a single query.</span></span> <span data-ttu-id="a595e-665">For example, you might use the employee id to look up a list of related entities that contain performance and review data for that employee.</span><span class="sxs-lookup"><span data-stu-id="a595e-665">For example, you might use the employee id to look up a list of related entities that contain performance and review data for that employee.</span></span>  

<span data-ttu-id="a595e-666">Assume you are storing employee entities in the Table service using the following structure:</span><span class="sxs-lookup"><span data-stu-id="a595e-666">Assume you are storing employee entities in the Table service using the following structure:</span></span>  

![][18]

<span data-ttu-id="a595e-667">You also need to store historical data relating to reviews and performance for each year the employee has worked for your organization and you need to be able to access this information by year.</span><span class="sxs-lookup"><span data-stu-id="a595e-667">You also need to store historical data relating to reviews and performance for each year the employee has worked for your organization and you need to be able to access this information by year.</span></span> <span data-ttu-id="a595e-668">One option is to create another table that stores entities with the following structure:</span><span class="sxs-lookup"><span data-stu-id="a595e-668">One option is to create another table that stores entities with the following structure:</span></span>  

![][19]

<span data-ttu-id="a595e-669">Notice that with this approach you may decide to duplicate some information (such as first name and last name) in the new entity to enable you to retrieve your data with a single request.</span><span class="sxs-lookup"><span data-stu-id="a595e-669">Notice that with this approach you may decide to duplicate some information (such as first name and last name) in the new entity to enable you to retrieve your data with a single request.</span></span> <span data-ttu-id="a595e-670">However, you cannot maintain strong consistency because you cannot use an EGT to update the two entities atomically.</span><span class="sxs-lookup"><span data-stu-id="a595e-670">However, you cannot maintain strong consistency because you cannot use an EGT to update the two entities atomically.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-671">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-671">Solution</span></span>
<span data-ttu-id="a595e-672">Store a new entity type in your original table using entities with the following structure:</span><span class="sxs-lookup"><span data-stu-id="a595e-672">Store a new entity type in your original table using entities with the following structure:</span></span>  

![][20]

<span data-ttu-id="a595e-673">Notice how the **RowKey** is now a compound key made up of the employee id and the year of the review data that enables you to retrieve the employee's performance and review data with a single request for a single entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-673">Notice how the **RowKey** is now a compound key made up of the employee id and the year of the review data that enables you to retrieve the employee's performance and review data with a single request for a single entity.</span></span>  

<span data-ttu-id="a595e-674">The following example outlines how you can retrieve all the review data for a particular employee (such as employee 000123 in the Sales department):</span><span class="sxs-lookup"><span data-stu-id="a595e-674">The following example outlines how you can retrieve all the review data for a particular employee (such as employee 000123 in the Sales department):</span></span>  

<span data-ttu-id="a595e-675">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span><span class="sxs-lookup"><span data-stu-id="a595e-675">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-676">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-676">Issues and considerations</span></span>
<span data-ttu-id="a595e-677">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-677">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-678">You should use a suitable separator character that makes it easy to parse the **RowKey** value: for example, **000123_2012**.</span><span class="sxs-lookup"><span data-stu-id="a595e-678">You should use a suitable separator character that makes it easy to parse the **RowKey** value: for example, **000123_2012**.</span></span>  
* <span data-ttu-id="a595e-679">You are also storing this entity in the same partition as other entities that contain related data for the same employee, which means you can use EGTs to maintain strong consistency.</span><span class="sxs-lookup"><span data-stu-id="a595e-679">You are also storing this entity in the same partition as other entities that contain related data for the same employee, which means you can use EGTs to maintain strong consistency.</span></span>
* <span data-ttu-id="a595e-680">You should consider how frequently you will query the data to determine whether this pattern is appropriate.</span><span class="sxs-lookup"><span data-stu-id="a595e-680">You should consider how frequently you will query the data to determine whether this pattern is appropriate.</span></span>  <span data-ttu-id="a595e-681">For example, if you will access the review data infrequently and the main employee data often you should keep them as separate entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-681">For example, if you will access the review data infrequently and the main employee data often you should keep them as separate entities.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-682">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-682">When to use this pattern</span></span>
<span data-ttu-id="a595e-683">Use this pattern when you need to store one or more related entities that you query frequently.</span><span class="sxs-lookup"><span data-stu-id="a595e-683">Use this pattern when you need to store one or more related entities that you query frequently.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-684">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-684">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-685">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-685">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-686">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-686">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a595e-687">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-687">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  
* [<span data-ttu-id="a595e-688">Eventually consistent transactions pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-688">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a><span data-ttu-id="a595e-689">Log tail pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-689">Log tail pattern</span></span>
<span data-ttu-id="a595e-690">Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span><span class="sxs-lookup"><span data-stu-id="a595e-690">Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-691">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-691">Context and problem</span></span>
<span data-ttu-id="a595e-692">A common requirement is be able to retrieve the most recently created entities, for example the ten most recent expense claims submitted by an employee.</span><span class="sxs-lookup"><span data-stu-id="a595e-692">A common requirement is be able to retrieve the most recently created entities, for example the ten most recent expense claims submitted by an employee.</span></span> <span data-ttu-id="a595e-693">Table queries support a **$top** query operation to return the first *n* entities from a set: there is no equivalent query operation to return the last n entities in a set.</span><span class="sxs-lookup"><span data-stu-id="a595e-693">Table queries support a **$top** query operation to return the first *n* entities from a set: there is no equivalent query operation to return the last n entities in a set.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-694">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-694">Solution</span></span>
<span data-ttu-id="a595e-695">Store the entities using a **RowKey** that naturally sorts in reverse date/time order by using so the most recent entry is always the first one in the table.</span><span class="sxs-lookup"><span data-stu-id="a595e-695">Store the entities using a **RowKey** that naturally sorts in reverse date/time order by using so the most recent entry is always the first one in the table.</span></span>  

<span data-ttu-id="a595e-696">For example, to be able to retrieve the ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from the current date/time.</span><span class="sxs-lookup"><span data-stu-id="a595e-696">For example, to be able to retrieve the ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from the current date/time.</span></span> <span data-ttu-id="a595e-697">The following C# code sample shows one way to create a suitable "inverted ticks" value for a **RowKey** that sorts from the most recent to the oldest:</span><span class="sxs-lookup"><span data-stu-id="a595e-697">The following C# code sample shows one way to create a suitable "inverted ticks" value for a **RowKey** that sorts from the most recent to the oldest:</span></span>  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

<span data-ttu-id="a595e-698">You can get back to the date time value using the following code:</span><span class="sxs-lookup"><span data-stu-id="a595e-698">You can get back to the date time value using the following code:</span></span>  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

<span data-ttu-id="a595e-699">The table query looks like this:</span><span class="sxs-lookup"><span data-stu-id="a595e-699">The table query looks like this:</span></span>  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-700">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-700">Issues and considerations</span></span>
<span data-ttu-id="a595e-701">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-701">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-702">You must pad the reverse tick value with leading zeroes to ensure the string value sorts as expected.</span><span class="sxs-lookup"><span data-stu-id="a595e-702">You must pad the reverse tick value with leading zeroes to ensure the string value sorts as expected.</span></span>  
* <span data-ttu-id="a595e-703">You must be aware of the scalability targets at the level of a partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-703">You must be aware of the scalability targets at the level of a partition.</span></span> <span data-ttu-id="a595e-704">Be careful not create hot spot partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-704">Be careful not create hot spot partitions.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-705">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-705">When to use this pattern</span></span>
<span data-ttu-id="a595e-706">Use this pattern when you need to access entities in reverse date/time order or when you need to access the most recently added entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-706">Use this pattern when you need to access entities in reverse date/time order or when you need to access the most recently added entities.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-707">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-707">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-708">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-708">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-709">Prepend / append anti-pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-709">Prepend / append anti-pattern</span></span>](#prepend-append-anti-pattern)  
* [<span data-ttu-id="a595e-710">Retrieving entities</span><span class="sxs-lookup"><span data-stu-id="a595e-710">Retrieving entities</span></span>](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a><span data-ttu-id="a595e-711">High volume delete pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-711">High volume delete pattern</span></span>
<span data-ttu-id="a595e-712">Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span><span class="sxs-lookup"><span data-stu-id="a595e-712">Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-713">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-713">Context and problem</span></span>
<span data-ttu-id="a595e-714">Many applications delete old data which no longer needs to be available to a client application, or that the application has archived to another storage medium.</span><span class="sxs-lookup"><span data-stu-id="a595e-714">Many applications delete old data which no longer needs to be available to a client application, or that the application has archived to another storage medium.</span></span> <span data-ttu-id="a595e-715">You typically identify such data by a date: for example, you have a requirement to delete records of all login requests that are more than 60 days old.</span><span class="sxs-lookup"><span data-stu-id="a595e-715">You typically identify such data by a date: for example, you have a requirement to delete records of all login requests that are more than 60 days old.</span></span>  

<span data-ttu-id="a595e-716">One possible design is to use the date and time of the login request in the **RowKey**:</span><span class="sxs-lookup"><span data-stu-id="a595e-716">One possible design is to use the date and time of the login request in the **RowKey**:</span></span>  

![][21]

<span data-ttu-id="a595e-717">This approach avoids partition hotspots because the application can insert and delete login entities for each user in a separate partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-717">This approach avoids partition hotspots because the application can insert and delete login entities for each user in a separate partition.</span></span> <span data-ttu-id="a595e-718">However, this approach may be costly and time consuming if you have a large number of entities because first you need to perform a table scan in order to identify all the entities to delete, and then you must delete each old entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-718">However, this approach may be costly and time consuming if you have a large number of entities because first you need to perform a table scan in order to identify all the entities to delete, and then you must delete each old entity.</span></span> <span data-ttu-id="a595e-719">Note that you can reduce the number of round trips to the server required to delete the old entities by batching multiple delete requests into EGTs.</span><span class="sxs-lookup"><span data-stu-id="a595e-719">Note that you can reduce the number of round trips to the server required to delete the old entities by batching multiple delete requests into EGTs.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-720">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-720">Solution</span></span>
<span data-ttu-id="a595e-721">Use a separate table for each day of login attempts.</span><span class="sxs-lookup"><span data-stu-id="a595e-721">Use a separate table for each day of login attempts.</span></span> <span data-ttu-id="a595e-722">You can use the entity design above to avoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span><span class="sxs-lookup"><span data-stu-id="a595e-722">You can use the entity design above to avoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-723">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-723">Issues and considerations</span></span>
<span data-ttu-id="a595e-724">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-724">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-725">Does your design support other ways your application will use the data such as looking up specific entities, linking with other data, or generating aggregate information?</span><span class="sxs-lookup"><span data-stu-id="a595e-725">Does your design support other ways your application will use the data such as looking up specific entities, linking with other data, or generating aggregate information?</span></span>  
* <span data-ttu-id="a595e-726">Does your design avoid hot spots when you are inserting new entities?</span><span class="sxs-lookup"><span data-stu-id="a595e-726">Does your design avoid hot spots when you are inserting new entities?</span></span>  
* <span data-ttu-id="a595e-727">Expect a delay if you want to reuse the same table name after deleting it.</span><span class="sxs-lookup"><span data-stu-id="a595e-727">Expect a delay if you want to reuse the same table name after deleting it.</span></span> <span data-ttu-id="a595e-728">It's better to always use unique table names.</span><span class="sxs-lookup"><span data-stu-id="a595e-728">It's better to always use unique table names.</span></span>  
* <span data-ttu-id="a595e-729">Expect some throttling when you first use a new table while the Table service learns the access patterns and distributes the partitions across nodes.</span><span class="sxs-lookup"><span data-stu-id="a595e-729">Expect some throttling when you first use a new table while the Table service learns the access patterns and distributes the partitions across nodes.</span></span> <span data-ttu-id="a595e-730">You should consider how frequently you need to create new tables.</span><span class="sxs-lookup"><span data-stu-id="a595e-730">You should consider how frequently you need to create new tables.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-731">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-731">When to use this pattern</span></span>
<span data-ttu-id="a595e-732">Use this pattern when you have a high volume of entities that you must delete at the same time.</span><span class="sxs-lookup"><span data-stu-id="a595e-732">Use this pattern when you have a high volume of entities that you must delete at the same time.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-733">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-733">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-734">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-734">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-735">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-735">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="a595e-736">Modifying entities</span><span class="sxs-lookup"><span data-stu-id="a595e-736">Modifying entities</span></span>](#modifying-entities)  

### <a name="data-series-pattern"></a><span data-ttu-id="a595e-737">Data series pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-737">Data series pattern</span></span>
<span data-ttu-id="a595e-738">Store complete data series in a single entity to minimize the number of requests you make.</span><span class="sxs-lookup"><span data-stu-id="a595e-738">Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-739">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-739">Context and problem</span></span>
<span data-ttu-id="a595e-740">A common scenario is for an application to store a series of data that it typically needs to retrieve all at once.</span><span class="sxs-lookup"><span data-stu-id="a595e-740">A common scenario is for an application to store a series of data that it typically needs to retrieve all at once.</span></span> <span data-ttu-id="a595e-741">For example, your application might record how many IM messages each employee sends every hour, and then use this information to plot how many messages each user sent over the preceding 24 hours.</span><span class="sxs-lookup"><span data-stu-id="a595e-741">For example, your application might record how many IM messages each employee sends every hour, and then use this information to plot how many messages each user sent over the preceding 24 hours.</span></span> <span data-ttu-id="a595e-742">One design might be to store 24 entities for each employee:</span><span class="sxs-lookup"><span data-stu-id="a595e-742">One design might be to store 24 entities for each employee:</span></span>  

![][22]

<span data-ttu-id="a595e-743">With this design, you can easily locate and update the entity to update for each employee whenever the application needs to update the message count value.</span><span class="sxs-lookup"><span data-stu-id="a595e-743">With this design, you can easily locate and update the entity to update for each employee whenever the application needs to update the message count value.</span></span> <span data-ttu-id="a595e-744">However, to retrieve the information to plot a chart of the activity for the preceding 24 hours, you must retrieve 24 entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-744">However, to retrieve the information to plot a chart of the activity for the preceding 24 hours, you must retrieve 24 entities.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-745">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-745">Solution</span></span>
<span data-ttu-id="a595e-746">Use the following design with a separate property to store the message count for each hour:</span><span class="sxs-lookup"><span data-stu-id="a595e-746">Use the following design with a separate property to store the message count for each hour:</span></span>  

![][23]

<span data-ttu-id="a595e-747">With this design, you can use a merge operation to update the message count for an employee for a specific hour.</span><span class="sxs-lookup"><span data-stu-id="a595e-747">With this design, you can use a merge operation to update the message count for an employee for a specific hour.</span></span> <span data-ttu-id="a595e-748">Now, you can retrieve all the information you need to plot the chart using a request for a single entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-748">Now, you can retrieve all the information you need to plot the chart using a request for a single entity.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-749">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-749">Issues and considerations</span></span>
<span data-ttu-id="a595e-750">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-750">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-751">If your complete data series does not fit into a single entity (an entity can have up to 252 properties), use an alternative data store such as a blob.</span><span class="sxs-lookup"><span data-stu-id="a595e-751">If your complete data series does not fit into a single entity (an entity can have up to 252 properties), use an alternative data store such as a blob.</span></span>  
* <span data-ttu-id="a595e-752">If you have multiple clients updating an entity simultaneously, you will need to use the **ETag** to implement optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="a595e-752">If you have multiple clients updating an entity simultaneously, you will need to use the **ETag** to implement optimistic concurrency.</span></span> <span data-ttu-id="a595e-753">If you have many clients, you may experience high contention.</span><span class="sxs-lookup"><span data-stu-id="a595e-753">If you have many clients, you may experience high contention.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-754">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-754">When to use this pattern</span></span>
<span data-ttu-id="a595e-755">Use this pattern when you need to update and retrieve a data series associated with an individual entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-755">Use this pattern when you need to update and retrieve a data series associated with an individual entity.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-756">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-756">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-757">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-757">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-758">Large entities pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-758">Large entities pattern</span></span>](#large-entities-pattern)  
* [<span data-ttu-id="a595e-759">Merge or replace</span><span class="sxs-lookup"><span data-stu-id="a595e-759">Merge or replace</span></span>](#merge-or-replace)  
* <span data-ttu-id="a595e-760">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing the data series in a blob)</span><span class="sxs-lookup"><span data-stu-id="a595e-760">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing the data series in a blob)</span></span>  

### <a name="wide-entities-pattern"></a><span data-ttu-id="a595e-761">Wide entities pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-761">Wide entities pattern</span></span>
<span data-ttu-id="a595e-762">Use multiple physical entities to store logical entities with more than 252 properties.</span><span class="sxs-lookup"><span data-stu-id="a595e-762">Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-763">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-763">Context and problem</span></span>
<span data-ttu-id="a595e-764">An individual entity can have no more than 252 properties (excluding the mandatory system properties) and cannot store more than 1 MB of data in total.</span><span class="sxs-lookup"><span data-stu-id="a595e-764">An individual entity can have no more than 252 properties (excluding the mandatory system properties) and cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="a595e-765">In a relational database, you would typically get round any limits on the size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span><span class="sxs-lookup"><span data-stu-id="a595e-765">In a relational database, you would typically get round any limits on the size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-766">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-766">Solution</span></span>
<span data-ttu-id="a595e-767">Using the Table service, you can store multiple entities to represent a single large business object with more than 252 properties.</span><span class="sxs-lookup"><span data-stu-id="a595e-767">Using the Table service, you can store multiple entities to represent a single large business object with more than 252 properties.</span></span> <span data-ttu-id="a595e-768">For example, if you want to store a count of the number of IM messages sent by each employee for the last 365 days, you could use the following design that uses two entities with different schemas:</span><span class="sxs-lookup"><span data-stu-id="a595e-768">For example, if you want to store a count of the number of IM messages sent by each employee for the last 365 days, you could use the following design that uses two entities with different schemas:</span></span>  

![][24]

<span data-ttu-id="a595e-769">If you need to make a change that requires updating both entities to keep them synchronized with each other you can use an EGT.</span><span class="sxs-lookup"><span data-stu-id="a595e-769">If you need to make a change that requires updating both entities to keep them synchronized with each other you can use an EGT.</span></span> <span data-ttu-id="a595e-770">Otherwise, you can use a single merge operation to update the message count for a specific day.</span><span class="sxs-lookup"><span data-stu-id="a595e-770">Otherwise, you can use a single merge operation to update the message count for a specific day.</span></span> <span data-ttu-id="a595e-771">To retrieve all the data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span><span class="sxs-lookup"><span data-stu-id="a595e-771">To retrieve all the data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-772">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-772">Issues and considerations</span></span>
<span data-ttu-id="a595e-773">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-773">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-774">Retrieving a complete logical entity involves at least two storage transactions: one to retrieve each physical entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-774">Retrieving a complete logical entity involves at least two storage transactions: one to retrieve each physical entity.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-775">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-775">When to use this pattern</span></span>
<span data-ttu-id="a595e-776">Use this pattern when  need to store entities whose size or number of properties exceeds the limits for an individual entity in the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-776">Use this pattern when  need to store entities whose size or number of properties exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-777">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-777">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-778">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-778">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-779">Entity Group Transactions</span><span class="sxs-lookup"><span data-stu-id="a595e-779">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="a595e-780">Merge or replace</span><span class="sxs-lookup"><span data-stu-id="a595e-780">Merge or replace</span></span>](#merge-or-replace)

### <a name="large-entities-pattern"></a><span data-ttu-id="a595e-781">Large entities pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-781">Large entities pattern</span></span>
<span data-ttu-id="a595e-782">Use blob storage to store large property values.</span><span class="sxs-lookup"><span data-stu-id="a595e-782">Use blob storage to store large property values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-783">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-783">Context and problem</span></span>
<span data-ttu-id="a595e-784">An individual entity cannot store more than 1 MB of data in total.</span><span class="sxs-lookup"><span data-stu-id="a595e-784">An individual entity cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="a595e-785">If one or several of your properties store values that cause the total size of your entity to exceed this value, you cannot store the entire entity in the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-785">If one or several of your properties store values that cause the total size of your entity to exceed this value, you cannot store the entire entity in the Table service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a595e-786">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-786">Solution</span></span>
<span data-ttu-id="a595e-787">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in the Blob service and then store the address of the blob in a property in the entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-787">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in the Blob service and then store the address of the blob in a property in the entity.</span></span> <span data-ttu-id="a595e-788">For example, you can store the photo of an employee in blob storage and store a link to the photo in the **Photo** property of your employee entity:</span><span class="sxs-lookup"><span data-stu-id="a595e-788">For example, you can store the photo of an employee in blob storage and store a link to the photo in the **Photo** property of your employee entity:</span></span>  

![][25]

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-789">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-789">Issues and considerations</span></span>
<span data-ttu-id="a595e-790">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-790">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-791">To maintain eventual consistency between the entity in the Table service and the data in the Blob service, use the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain your entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-791">To maintain eventual consistency between the entity in the Table service and the data in the Blob service, use the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain your entities.</span></span>
* <span data-ttu-id="a595e-792">Retrieving a complete entity involves at least two storage transactions: one to retrieve the entity and one to retrieve the blob data.</span><span class="sxs-lookup"><span data-stu-id="a595e-792">Retrieving a complete entity involves at least two storage transactions: one to retrieve the entity and one to retrieve the blob data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-793">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-793">When to use this pattern</span></span>
<span data-ttu-id="a595e-794">Use this pattern when you need to store entities whose size exceeds the limits for an individual entity in the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-794">Use this pattern when you need to store entities whose size exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-795">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-795">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-796">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-796">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-797">Eventually consistent transactions pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-797">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="a595e-798">Wide entities pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-798">Wide entities pattern</span></span>](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a><span data-ttu-id="a595e-799">Prepend/append anti-pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-799">Prepend/append anti-pattern</span></span>
<span data-ttu-id="a595e-800">Increase scalability when you have a high volume of inserts by spreading the inserts across multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-800">Increase scalability when you have a high volume of inserts by spreading the inserts across multiple partitions.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-801">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-801">Context and problem</span></span>
<span data-ttu-id="a595e-802">Prepending or appending entities to your stored entities typically results in the application adding new entities to the first or last partition of a sequence of partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-802">Prepending or appending entities to your stored entities typically results in the application adding new entities to the first or last partition of a sequence of partitions.</span></span> <span data-ttu-id="a595e-803">In this case, all of the inserts at any given time are taking place in the same partition, creating a hotspot that prevents the table service from load balancing inserts across multiple nodes, and possibly causing your application to hit the scalability targets for partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-803">In this case, all of the inserts at any given time are taking place in the same partition, creating a hotspot that prevents the table service from load balancing inserts across multiple nodes, and possibly causing your application to hit the scalability targets for partition.</span></span> <span data-ttu-id="a595e-804">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in the current hour's partition becoming a hotspot if the volume of transactions reaches the scalability target for an individual partition:</span><span class="sxs-lookup"><span data-stu-id="a595e-804">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in the current hour's partition becoming a hotspot if the volume of transactions reaches the scalability target for an individual partition:</span></span>  

![][26]

#### <a name="solution"></a><span data-ttu-id="a595e-805">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-805">Solution</span></span>
<span data-ttu-id="a595e-806">The following alternative entity structure avoids a hotspot on any particular partition as the application logs events:</span><span class="sxs-lookup"><span data-stu-id="a595e-806">The following alternative entity structure avoids a hotspot on any particular partition as the application logs events:</span></span>  

![][27]

<span data-ttu-id="a595e-807">Notice with this example how both the **PartitionKey** and **RowKey** are compound keys.</span><span class="sxs-lookup"><span data-stu-id="a595e-807">Notice with this example how both the **PartitionKey** and **RowKey** are compound keys.</span></span> <span data-ttu-id="a595e-808">The **PartitionKey** uses both the department and employee id to distribute the logging across multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-808">The **PartitionKey** uses both the department and employee id to distribute the logging across multiple partitions.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-809">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-809">Issues and considerations</span></span>
<span data-ttu-id="a595e-810">Consider the following points when deciding how to implement this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-810">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a595e-811">Does the alternative key structure that avoids creating hot partitions on inserts efficiently support the queries your client application makes?</span><span class="sxs-lookup"><span data-stu-id="a595e-811">Does the alternative key structure that avoids creating hot partitions on inserts efficiently support the queries your client application makes?</span></span>  
* <span data-ttu-id="a595e-812">Does your anticipated volume of transactions mean that you are likely to reach the scalability targets for an individual partition and be throttled by the storage service?</span><span class="sxs-lookup"><span data-stu-id="a595e-812">Does your anticipated volume of transactions mean that you are likely to reach the scalability targets for an individual partition and be throttled by the storage service?</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a595e-813">When to use this pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-813">When to use this pattern</span></span>
<span data-ttu-id="a595e-814">Avoid the prepend/append anti-pattern when your volume of transactions is likely to result in throttling by the storage service when you access a hot partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-814">Avoid the prepend/append anti-pattern when your volume of transactions is likely to result in throttling by the storage service when you access a hot partition.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a595e-815">Related patterns and guidance</span><span class="sxs-lookup"><span data-stu-id="a595e-815">Related patterns and guidance</span></span>
<span data-ttu-id="a595e-816">The following patterns and guidance may also be relevant when implementing this pattern:</span><span class="sxs-lookup"><span data-stu-id="a595e-816">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a595e-817">Compound key pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-817">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a595e-818">Log tail pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-818">Log tail pattern</span></span>](#log-tail-pattern)  
* [<span data-ttu-id="a595e-819">Modifying entities</span><span class="sxs-lookup"><span data-stu-id="a595e-819">Modifying entities</span></span>](#modifying-entities)  

### <a name="log-data-anti-pattern"></a><span data-ttu-id="a595e-820">Log data anti-pattern</span><span class="sxs-lookup"><span data-stu-id="a595e-820">Log data anti-pattern</span></span>
<span data-ttu-id="a595e-821">Typically, you should use the Blob service instead of the Table service to store log data.</span><span class="sxs-lookup"><span data-stu-id="a595e-821">Typically, you should use the Blob service instead of the Table service to store log data.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a595e-822">Context and problem</span><span class="sxs-lookup"><span data-stu-id="a595e-822">Context and problem</span></span>
<span data-ttu-id="a595e-823">A common use case for log data is to retrieve a selection of log entries for a specific date/time range: for example, you want to find all the error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span><span class="sxs-lookup"><span data-stu-id="a595e-823">A common use case for log data is to retrieve a selection of log entries for a specific date/time range: for example, you want to find all the error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span></span> <span data-ttu-id="a595e-824">You do not want to use the date and time of the log message to determine the partition you save log entities to: that results in a hot partition because at any given time, all the log entities will share the same **PartitionKey** value (see the section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span><span class="sxs-lookup"><span data-stu-id="a595e-824">You do not want to use the date and time of the log message to determine the partition you save log entities to: that results in a hot partition because at any given time, all the log entities will share the same **PartitionKey** value (see the section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span></span> <span data-ttu-id="a595e-825">For example, the following entity schema for a log message results in a hot partition because the application writes all log messages to the partition for the current date and hour:</span><span class="sxs-lookup"><span data-stu-id="a595e-825">For example, the following entity schema for a log message results in a hot partition because the application writes all log messages to the partition for the current date and hour:</span></span>  

![][28]

<span data-ttu-id="a595e-826">In this example, the **RowKey** includes the date and time of the log message to ensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share the same date and time.</span><span class="sxs-lookup"><span data-stu-id="a595e-826">In this example, the **RowKey** includes the date and time of the log message to ensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share the same date and time.</span></span>  

<span data-ttu-id="a595e-827">Another approach is to use a **PartitionKey** that ensures that the application writes messages across a range of partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-827">Another approach is to use a **PartitionKey** that ensures that the application writes messages across a range of partitions.</span></span> <span data-ttu-id="a595e-828">For example, if the source of the log message provides a way to distribute messages across many partitions, you could use the following entity schema:</span><span class="sxs-lookup"><span data-stu-id="a595e-828">For example, if the source of the log message provides a way to distribute messages across many partitions, you could use the following entity schema:</span></span>  

![][29]

<span data-ttu-id="a595e-829">However, the problem with this schema is that to retrieve all the log messages for a specific time span you must search every partition in the table.</span><span class="sxs-lookup"><span data-stu-id="a595e-829">However, the problem with this schema is that to retrieve all the log messages for a specific time span you must search every partition in the table.</span></span>

#### <a name="solution"></a><span data-ttu-id="a595e-830">Solution</span><span class="sxs-lookup"><span data-stu-id="a595e-830">Solution</span></span>
<span data-ttu-id="a595e-831">The previous section highlighted the problem of trying to use the Table service to store log entries and suggested two, unsatisfactory, designs.</span><span class="sxs-lookup"><span data-stu-id="a595e-831">The previous section highlighted the problem of trying to use the Table service to store log entries and suggested two, unsatisfactory, designs.</span></span> <span data-ttu-id="a595e-832">One solution led to a hot partition with the risk of poor performance writing log messages; the other solution resulted in poor query performance because of the requirement to scan every partition in the table to retrieve log messages for a specific time span.</span><span class="sxs-lookup"><span data-stu-id="a595e-832">One solution led to a hot partition with the risk of poor performance writing log messages; the other solution resulted in poor query performance because of the requirement to scan every partition in the table to retrieve log messages for a specific time span.</span></span> <span data-ttu-id="a595e-833">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores the log data it collects.</span><span class="sxs-lookup"><span data-stu-id="a595e-833">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores the log data it collects.</span></span>  

<span data-ttu-id="a595e-834">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach to storing data that you typically query by range.</span><span class="sxs-lookup"><span data-stu-id="a595e-834">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach to storing data that you typically query by range.</span></span>  

<span data-ttu-id="a595e-835">Storage Analytics stores log messages in a delimited format in multiple blobs.</span><span class="sxs-lookup"><span data-stu-id="a595e-835">Storage Analytics stores log messages in a delimited format in multiple blobs.</span></span> <span data-ttu-id="a595e-836">The delimited format makes it easy for a client application to parse the data in the log message.</span><span class="sxs-lookup"><span data-stu-id="a595e-836">The delimited format makes it easy for a client application to parse the data in the log message.</span></span>  

<span data-ttu-id="a595e-837">Storage Analytics uses a naming convention for blobs that enables you to locate the blob (or blobs) that contain the log messages for which you are searching.</span><span class="sxs-lookup"><span data-stu-id="a595e-837">Storage Analytics uses a naming convention for blobs that enables you to locate the blob (or blobs) that contain the log messages for which you are searching.</span></span> <span data-ttu-id="a595e-838">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate to the queue service for the hour starting at 18:00 on 31 July 2014.</span><span class="sxs-lookup"><span data-stu-id="a595e-838">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate to the queue service for the hour starting at 18:00 on 31 July 2014.</span></span> <span data-ttu-id="a595e-839">The "000001" indicates that this is the first log file for this period.</span><span class="sxs-lookup"><span data-stu-id="a595e-839">The "000001" indicates that this is the first log file for this period.</span></span> <span data-ttu-id="a595e-840">Storage Analytics also records the timestamps of the first and last log messages stored in the file as part of the blob's metadata.</span><span class="sxs-lookup"><span data-stu-id="a595e-840">Storage Analytics also records the timestamps of the first and last log messages stored in the file as part of the blob's metadata.</span></span> <span data-ttu-id="a595e-841">The API for blob storage enables you locate blobs in a container based on a name prefix: to locate all the blobs that contain queue log data for the hour starting at 18:00, you can use the prefix "queue/2014/07/31/1800."</span><span class="sxs-lookup"><span data-stu-id="a595e-841">The API for blob storage enables you locate blobs in a container based on a name prefix: to locate all the blobs that contain queue log data for the hour starting at 18:00, you can use the prefix "queue/2014/07/31/1800."</span></span>  

<span data-ttu-id="a595e-842">Storage Analytics buffers log messages internally and then periodically updates the appropriate blob or creates a new one with the latest batch of log entries.</span><span class="sxs-lookup"><span data-stu-id="a595e-842">Storage Analytics buffers log messages internally and then periodically updates the appropriate blob or creates a new one with the latest batch of log entries.</span></span> <span data-ttu-id="a595e-843">This reduces the number of writes it must perform to the blob service.</span><span class="sxs-lookup"><span data-stu-id="a595e-843">This reduces the number of writes it must perform to the blob service.</span></span>  

<span data-ttu-id="a595e-844">If you are implementing a similar solution in your own application, you must consider how to manage the trade-off between reliability (writing every log entry to blob storage as it happens) and cost and scalability (buffering updates in your application and writing them to blob storage in batches).</span><span class="sxs-lookup"><span data-stu-id="a595e-844">If you are implementing a similar solution in your own application, you must consider how to manage the trade-off between reliability (writing every log entry to blob storage as it happens) and cost and scalability (buffering updates in your application and writing them to blob storage in batches).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a595e-845">Issues and considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-845">Issues and considerations</span></span>
<span data-ttu-id="a595e-846">Consider the following points when deciding how to store log data:</span><span class="sxs-lookup"><span data-stu-id="a595e-846">Consider the following points when deciding how to store log data:</span></span>  

* <span data-ttu-id="a595e-847">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span><span class="sxs-lookup"><span data-stu-id="a595e-847">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span></span>  
* <span data-ttu-id="a595e-848">To process log data, a client often needs to load many records.</span><span class="sxs-lookup"><span data-stu-id="a595e-848">To process log data, a client often needs to load many records.</span></span>  
* <span data-ttu-id="a595e-849">Although log data is often structured, blob storage may be a better solution.</span><span class="sxs-lookup"><span data-stu-id="a595e-849">Although log data is often structured, blob storage may be a better solution.</span></span>  

### <a name="implementation-considerations"></a><span data-ttu-id="a595e-850">Implementation considerations</span><span class="sxs-lookup"><span data-stu-id="a595e-850">Implementation considerations</span></span>
<span data-ttu-id="a595e-851">This section discusses some of the considerations to bear in mind when you implement the patterns described in the previous sections.</span><span class="sxs-lookup"><span data-stu-id="a595e-851">This section discusses some of the considerations to bear in mind when you implement the patterns described in the previous sections.</span></span> <span data-ttu-id="a595e-852">Most of this section uses examples written in C# that use the Storage Client Library (version 4.3.0 at the time of writing).</span><span class="sxs-lookup"><span data-stu-id="a595e-852">Most of this section uses examples written in C# that use the Storage Client Library (version 4.3.0 at the time of writing).</span></span>  

### <a name="retrieving-entities"></a><span data-ttu-id="a595e-853">Retrieving entities</span><span class="sxs-lookup"><span data-stu-id="a595e-853">Retrieving entities</span></span>
<span data-ttu-id="a595e-854">As discussed in the section [Design for querying](#design-for-querying), the most efficient query is a point query.</span><span class="sxs-lookup"><span data-stu-id="a595e-854">As discussed in the section [Design for querying](#design-for-querying), the most efficient query is a point query.</span></span> <span data-ttu-id="a595e-855">However, in some scenarios you may need to retrieve multiple entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-855">However, in some scenarios you may need to retrieve multiple entities.</span></span> <span data-ttu-id="a595e-856">This section describes some common approaches to retrieving entities using the Storage Client Library.</span><span class="sxs-lookup"><span data-stu-id="a595e-856">This section describes some common approaches to retrieving entities using the Storage Client Library.</span></span>  

#### <a name="executing-a-point-query-using-the-storage-client-library"></a><span data-ttu-id="a595e-857">Executing a point query using the Storage Client Library</span><span class="sxs-lookup"><span data-stu-id="a595e-857">Executing a point query using the Storage Client Library</span></span>
<span data-ttu-id="a595e-858">The easiest way to execute a point query is to use the **Retrieve** table operation as shown in the following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span><span class="sxs-lookup"><span data-stu-id="a595e-858">The easiest way to execute a point query is to use the **Retrieve** table operation as shown in the following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span></span>  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

<span data-ttu-id="a595e-859">Notice how this example expects the entity it retrieves to be of type **EmployeeEntity**.</span><span class="sxs-lookup"><span data-stu-id="a595e-859">Notice how this example expects the entity it retrieves to be of type **EmployeeEntity**.</span></span>  

#### <a name="retrieving-multiple-entities-using-linq"></a><span data-ttu-id="a595e-860">Retrieving multiple entities using LINQ</span><span class="sxs-lookup"><span data-stu-id="a595e-860">Retrieving multiple entities using LINQ</span></span>
<span data-ttu-id="a595e-861">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span><span class="sxs-lookup"><span data-stu-id="a595e-861">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span></span> <span data-ttu-id="a595e-862">To avoid a table scan, you should always include the **PartitionKey** value in the where clause, and if possible the **RowKey** value to avoid table and partition scans.</span><span class="sxs-lookup"><span data-stu-id="a595e-862">To avoid a table scan, you should always include the **PartitionKey** value in the where clause, and if possible the **RowKey** value to avoid table and partition scans.</span></span> <span data-ttu-id="a595e-863">The table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) to use in the where clause.</span><span class="sxs-lookup"><span data-stu-id="a595e-863">The table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) to use in the where clause.</span></span> <span data-ttu-id="a595e-864">The following C# code snippet finds all the employees whose last name starts with "B" (assuming that the **RowKey** stores the last name) in the sales department (assuming the **PartitionKey** stores the department name):</span><span class="sxs-lookup"><span data-stu-id="a595e-864">The following C# code snippet finds all the employees whose last name starts with "B" (assuming that the **RowKey** stores the last name) in the sales department (assuming the **PartitionKey** stores the department name):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

<span data-ttu-id="a595e-865">Notice how the query specifies both a **RowKey** and a **PartitionKey** to ensure better performance.</span><span class="sxs-lookup"><span data-stu-id="a595e-865">Notice how the query specifies both a **RowKey** and a **PartitionKey** to ensure better performance.</span></span>  

<span data-ttu-id="a595e-866">The following code sample shows equivalent functionality using the fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span><span class="sxs-lookup"><span data-stu-id="a595e-866">The following code sample shows equivalent functionality using the fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> <span data-ttu-id="a595e-867">The sample nests multiple **CombineFilters** methods to include the three filter conditions.</span><span class="sxs-lookup"><span data-stu-id="a595e-867">The sample nests multiple **CombineFilters** methods to include the three filter conditions.</span></span>  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a><span data-ttu-id="a595e-868">Retrieving large numbers of entities from a query</span><span class="sxs-lookup"><span data-stu-id="a595e-868">Retrieving large numbers of entities from a query</span></span>
<span data-ttu-id="a595e-869">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span><span class="sxs-lookup"><span data-stu-id="a595e-869">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span></span> <span data-ttu-id="a595e-870">However, in some scenarios you may have a requirement to return many entities from the same partition or even from many partitions.</span><span class="sxs-lookup"><span data-stu-id="a595e-870">However, in some scenarios you may have a requirement to return many entities from the same partition or even from many partitions.</span></span>  

<span data-ttu-id="a595e-871">You should always fully test the performance of your application in such scenarios.</span><span class="sxs-lookup"><span data-stu-id="a595e-871">You should always fully test the performance of your application in such scenarios.</span></span>  

<span data-ttu-id="a595e-872">A query against the table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span><span class="sxs-lookup"><span data-stu-id="a595e-872">A query against the table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span></span> <span data-ttu-id="a595e-873">If the result set contains more than 1,000 entities, if the query did not complete within five seconds, or if the query crosses the partition boundary, the Table service returns a continuation token to enable the client application to request the next set of entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-873">If the result set contains more than 1,000 entities, if the query did not complete within five seconds, or if the query crosses the partition boundary, the Table service returns a continuation token to enable the client application to request the next set of entities.</span></span> <span data-ttu-id="a595e-874">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span><span class="sxs-lookup"><span data-stu-id="a595e-874">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span></span>  

<span data-ttu-id="a595e-875">If you are using the Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-875">If you are using the Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from the Table service.</span></span> <span data-ttu-id="a595e-876">The following C# code sample using the Storage Client Library automatically handles continuation tokens if the table service returns them in a response:</span><span class="sxs-lookup"><span data-stu-id="a595e-876">The following C# code sample using the Storage Client Library automatically handles continuation tokens if the table service returns them in a response:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

<span data-ttu-id="a595e-877">The following C# code handles continuation tokens explicitly:</span><span class="sxs-lookup"><span data-stu-id="a595e-877">The following C# code handles continuation tokens explicitly:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

<span data-ttu-id="a595e-878">By using continuation tokens explicitly, you can control when your application retrieves the next segment of data.</span><span class="sxs-lookup"><span data-stu-id="a595e-878">By using continuation tokens explicitly, you can control when your application retrieves the next segment of data.</span></span> <span data-ttu-id="a595e-879">For example, if your client application enables users to page through the entities stored in a table, a user may decide not to page through all the entities retrieved by the query so your application would only use a continuation token to retrieve the next segment when the user had finished paging through all the entities in the current segment.</span><span class="sxs-lookup"><span data-stu-id="a595e-879">For example, if your client application enables users to page through the entities stored in a table, a user may decide not to page through all the entities retrieved by the query so your application would only use a continuation token to retrieve the next segment when the user had finished paging through all the entities in the current segment.</span></span> <span data-ttu-id="a595e-880">This approach has several benefits:</span><span class="sxs-lookup"><span data-stu-id="a595e-880">This approach has several benefits:</span></span>  

* <span data-ttu-id="a595e-881">It enables you to limit the amount of data to retrieve from the Table service and that you move over the network.</span><span class="sxs-lookup"><span data-stu-id="a595e-881">It enables you to limit the amount of data to retrieve from the Table service and that you move over the network.</span></span>  
* <span data-ttu-id="a595e-882">It enables you to perform asynchronous IO in .NET.</span><span class="sxs-lookup"><span data-stu-id="a595e-882">It enables you to perform asynchronous IO in .NET.</span></span>  
* <span data-ttu-id="a595e-883">It enables you to serialize the continuation token to persistent storage so you can continue in the event of an application crash.</span><span class="sxs-lookup"><span data-stu-id="a595e-883">It enables you to serialize the continuation token to persistent storage so you can continue in the event of an application crash.</span></span>  

> [!NOTE]
> <span data-ttu-id="a595e-884">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span><span class="sxs-lookup"><span data-stu-id="a595e-884">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span></span> <span data-ttu-id="a595e-885">This is also the case if you limit the number of entries a query returns by using **Take** to return the first n entities that match your lookup criteria: the table service may return a segment containing fewer than n entities along with a continuation token to enable you to retrieve the remaining entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-885">This is also the case if you limit the number of entries a query returns by using **Take** to return the first n entities that match your lookup criteria: the table service may return a segment containing fewer than n entities along with a continuation token to enable you to retrieve the remaining entities.</span></span>  
> 
> 

<span data-ttu-id="a595e-886">The following C# code shows how to modify the number of entities returned inside a segment:</span><span class="sxs-lookup"><span data-stu-id="a595e-886">The following C# code shows how to modify the number of entities returned inside a segment:</span></span>  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a><span data-ttu-id="a595e-887">Server-side projection</span><span class="sxs-lookup"><span data-stu-id="a595e-887">Server-side projection</span></span>
<span data-ttu-id="a595e-888">A single entity can have up to 255 properties and be up to 1 MB in size.</span><span class="sxs-lookup"><span data-stu-id="a595e-888">A single entity can have up to 255 properties and be up to 1 MB in size.</span></span> <span data-ttu-id="a595e-889">When you query the table and retrieve entities, you may not need all the properties and can avoid transferring data unnecessarily (to help reduce latency and cost).</span><span class="sxs-lookup"><span data-stu-id="a595e-889">When you query the table and retrieve entities, you may not need all the properties and can avoid transferring data unnecessarily (to help reduce latency and cost).</span></span> <span data-ttu-id="a595e-890">You can use server-side projection to transfer just the properties you need.</span><span class="sxs-lookup"><span data-stu-id="a595e-890">You can use server-side projection to transfer just the properties you need.</span></span> <span data-ttu-id="a595e-891">The following example is retrieves just the **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from the entities selected by the query.</span><span class="sxs-lookup"><span data-stu-id="a595e-891">The following example is retrieves just the **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from the entities selected by the query.</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

<span data-ttu-id="a595e-892">Notice how the **RowKey** value is available even though it was not included in the list of properties to retrieve.</span><span class="sxs-lookup"><span data-stu-id="a595e-892">Notice how the **RowKey** value is available even though it was not included in the list of properties to retrieve.</span></span>  

### <a name="modifying-entities"></a><span data-ttu-id="a595e-893">Modifying entities</span><span class="sxs-lookup"><span data-stu-id="a595e-893">Modifying entities</span></span>
<span data-ttu-id="a595e-894">The Storage Client Library enables you to modify your entities stored in the table service by inserting, deleting, and updating entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-894">The Storage Client Library enables you to modify your entities stored in the table service by inserting, deleting, and updating entities.</span></span> <span data-ttu-id="a595e-895">You can use EGTs to batch multiple insert, update, and delete operations together to reduce the number of round trips required and improve the performance of your solution.</span><span class="sxs-lookup"><span data-stu-id="a595e-895">You can use EGTs to batch multiple insert, update, and delete operations together to reduce the number of round trips required and improve the performance of your solution.</span></span>  

<span data-ttu-id="a595e-896">Note that exceptions thrown when the Storage Client Library executes an EGT typically include the index of the entity that caused the batch to fail.</span><span class="sxs-lookup"><span data-stu-id="a595e-896">Note that exceptions thrown when the Storage Client Library executes an EGT typically include the index of the entity that caused the batch to fail.</span></span> <span data-ttu-id="a595e-897">This is helpful when you are debugging code that uses EGTs.</span><span class="sxs-lookup"><span data-stu-id="a595e-897">This is helpful when you are debugging code that uses EGTs.</span></span>  

<span data-ttu-id="a595e-898">You should also consider how your design affects how your client application handles concurrency and update operations.</span><span class="sxs-lookup"><span data-stu-id="a595e-898">You should also consider how your design affects how your client application handles concurrency and update operations.</span></span>  

#### <a name="managing-concurrency"></a><span data-ttu-id="a595e-899">Managing concurrency</span><span class="sxs-lookup"><span data-stu-id="a595e-899">Managing concurrency</span></span>
<span data-ttu-id="a595e-900">By default, the table service implements optimistic concurrency checks at the level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client to force the table service to bypass these checks.</span><span class="sxs-lookup"><span data-stu-id="a595e-900">By default, the table service implements optimistic concurrency checks at the level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client to force the table service to bypass these checks.</span></span> <span data-ttu-id="a595e-901">For more information about how the table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](storage-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="a595e-901">For more information about how the table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](storage-concurrency.md).</span></span>  

#### <a name="merge-or-replace"></a><span data-ttu-id="a595e-902">Merge or replace</span><span class="sxs-lookup"><span data-stu-id="a595e-902">Merge or replace</span></span>
<span data-ttu-id="a595e-903">The **Replace** method of the **TableOperation** class always replaces the complete entity in the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-903">The **Replace** method of the **TableOperation** class always replaces the complete entity in the Table service.</span></span> <span data-ttu-id="a595e-904">If you do not include a property in the request when that property exists in the stored entity, the request removes that property from the stored entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-904">If you do not include a property in the request when that property exists in the stored entity, the request removes that property from the stored entity.</span></span> <span data-ttu-id="a595e-905">Unless you want to remove a property explicitly from a stored entity, you must include every property in the request.</span><span class="sxs-lookup"><span data-stu-id="a595e-905">Unless you want to remove a property explicitly from a stored entity, you must include every property in the request.</span></span>  

<span data-ttu-id="a595e-906">You can use the **Merge** method of the **TableOperation** class to reduce the amount of data that you send to the Table service when you want to update an entity.</span><span class="sxs-lookup"><span data-stu-id="a595e-906">You can use the **Merge** method of the **TableOperation** class to reduce the amount of data that you send to the Table service when you want to update an entity.</span></span> <span data-ttu-id="a595e-907">The **Merge** method replaces any properties in the stored entity with property values from the entity included in the request, but leaves intact any properties in the stored entity that are not included in the request.</span><span class="sxs-lookup"><span data-stu-id="a595e-907">The **Merge** method replaces any properties in the stored entity with property values from the entity included in the request, but leaves intact any properties in the stored entity that are not included in the request.</span></span> <span data-ttu-id="a595e-908">This is useful if you have large entities and only need to update a small number of properties in a request.</span><span class="sxs-lookup"><span data-stu-id="a595e-908">This is useful if you have large entities and only need to update a small number of properties in a request.</span></span>  

> [!NOTE]
> <span data-ttu-id="a595e-909">The **Replace** and **Merge** methods fail if the entity does not exist.</span><span class="sxs-lookup"><span data-stu-id="a595e-909">The **Replace** and **Merge** methods fail if the entity does not exist.</span></span> <span data-ttu-id="a595e-910">As an alternative, you can use the **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="a595e-910">As an alternative, you can use the **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span></span>  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a><span data-ttu-id="a595e-911">Working with heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-911">Working with heterogeneous entity types</span></span>
<span data-ttu-id="a595e-912">The Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span><span class="sxs-lookup"><span data-stu-id="a595e-912">The Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span></span> <span data-ttu-id="a595e-913">The following example illustrates a table storing both employee and department entities:</span><span class="sxs-lookup"><span data-stu-id="a595e-913">The following example illustrates a table storing both employee and department entities:</span></span>  

<table>
<tr>
<th><span data-ttu-id="a595e-914">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a595e-914">PartitionKey</span></span></th>
<th><span data-ttu-id="a595e-915">RowKey</span><span class="sxs-lookup"><span data-stu-id="a595e-915">RowKey</span></span></th>
<th><span data-ttu-id="a595e-916">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a595e-916">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-917">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-917">FirstName</span></span></th>
<th><span data-ttu-id="a595e-918">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-918">LastName</span></span></th>
<th><span data-ttu-id="a595e-919">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-919">Age</span></span></th>
<th><span data-ttu-id="a595e-920">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-920">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-921">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-921">FirstName</span></span></th>
<th><span data-ttu-id="a595e-922">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-922">LastName</span></span></th>
<th><span data-ttu-id="a595e-923">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-923">Age</span></span></th>
<th><span data-ttu-id="a595e-924">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-924">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-925">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="a595e-925">DepartmentName</span></span></th>
<th><span data-ttu-id="a595e-926">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="a595e-926">EmployeeCount</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-927">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-927">FirstName</span></span></th>
<th><span data-ttu-id="a595e-928">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-928">LastName</span></span></th>
<th><span data-ttu-id="a595e-929">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-929">Age</span></span></th>
<th><span data-ttu-id="a595e-930">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-930">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="a595e-931">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span><span class="sxs-lookup"><span data-stu-id="a595e-931">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span></span> <span data-ttu-id="a595e-932">Furthermore, there is nothing to indicate the type of an entity unless you choose to store that information somewhere.</span><span class="sxs-lookup"><span data-stu-id="a595e-932">Furthermore, there is nothing to indicate the type of an entity unless you choose to store that information somewhere.</span></span> <span data-ttu-id="a595e-933">There are two options for identifying the entity type:</span><span class="sxs-lookup"><span data-stu-id="a595e-933">There are two options for identifying the entity type:</span></span>  

* <span data-ttu-id="a595e-934">Prepend the entity type to the **RowKey** (or possibly the **PartitionKey**).</span><span class="sxs-lookup"><span data-stu-id="a595e-934">Prepend the entity type to the **RowKey** (or possibly the **PartitionKey**).</span></span> <span data-ttu-id="a595e-935">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-935">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span></span>  
* <span data-ttu-id="a595e-936">Use a separate property to record the entity type as shown in the table below.</span><span class="sxs-lookup"><span data-stu-id="a595e-936">Use a separate property to record the entity type as shown in the table below.</span></span>  

<table>
<tr>
<th><span data-ttu-id="a595e-937">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a595e-937">PartitionKey</span></span></th>
<th><span data-ttu-id="a595e-938">RowKey</span><span class="sxs-lookup"><span data-stu-id="a595e-938">RowKey</span></span></th>
<th><span data-ttu-id="a595e-939">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a595e-939">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-940">EntityType</span><span class="sxs-lookup"><span data-stu-id="a595e-940">EntityType</span></span></th>
<th><span data-ttu-id="a595e-941">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-941">FirstName</span></span></th>
<th><span data-ttu-id="a595e-942">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-942">LastName</span></span></th>
<th><span data-ttu-id="a595e-943">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-943">Age</span></span></th>
<th><span data-ttu-id="a595e-944">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-944">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-945">Employee</span><span class="sxs-lookup"><span data-stu-id="a595e-945">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-946">EntityType</span><span class="sxs-lookup"><span data-stu-id="a595e-946">EntityType</span></span></th>
<th><span data-ttu-id="a595e-947">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-947">FirstName</span></span></th>
<th><span data-ttu-id="a595e-948">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-948">LastName</span></span></th>
<th><span data-ttu-id="a595e-949">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-949">Age</span></span></th>
<th><span data-ttu-id="a595e-950">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-950">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-951">Employee</span><span class="sxs-lookup"><span data-stu-id="a595e-951">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-952">EntityType</span><span class="sxs-lookup"><span data-stu-id="a595e-952">EntityType</span></span></th>
<th><span data-ttu-id="a595e-953">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="a595e-953">DepartmentName</span></span></th>
<th><span data-ttu-id="a595e-954">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="a595e-954">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-955">Department</span><span class="sxs-lookup"><span data-stu-id="a595e-955">Department</span></span></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a595e-956">EntityType</span><span class="sxs-lookup"><span data-stu-id="a595e-956">EntityType</span></span></th>
<th><span data-ttu-id="a595e-957">FirstName</span><span class="sxs-lookup"><span data-stu-id="a595e-957">FirstName</span></span></th>
<th><span data-ttu-id="a595e-958">LastName</span><span class="sxs-lookup"><span data-stu-id="a595e-958">LastName</span></span></th>
<th><span data-ttu-id="a595e-959">Age</span><span class="sxs-lookup"><span data-stu-id="a595e-959">Age</span></span></th>
<th><span data-ttu-id="a595e-960">Email</span><span class="sxs-lookup"><span data-stu-id="a595e-960">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a595e-961">Employee</span><span class="sxs-lookup"><span data-stu-id="a595e-961">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="a595e-962">The first option, prepending the entity type to the **RowKey**, is useful if there is a possibility that two entities of different types might have the same key value.</span><span class="sxs-lookup"><span data-stu-id="a595e-962">The first option, prepending the entity type to the **RowKey**, is useful if there is a possibility that two entities of different types might have the same key value.</span></span> <span data-ttu-id="a595e-963">It also groups entities of the same type together in the partition.</span><span class="sxs-lookup"><span data-stu-id="a595e-963">It also groups entities of the same type together in the partition.</span></span>  

<span data-ttu-id="a595e-964">The techniques discussed in this section are especially relevant to the discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in the section [Modelling relationships](#modelling-relationships).</span><span class="sxs-lookup"><span data-stu-id="a595e-964">The techniques discussed in this section are especially relevant to the discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in the section [Modelling relationships](#modelling-relationships).</span></span>  

> [!NOTE]
> <span data-ttu-id="a595e-965">You should consider including a version number in the entity type value to enable client applications to evolve POCO objects and work with different versions.</span><span class="sxs-lookup"><span data-stu-id="a595e-965">You should consider including a version number in the entity type value to enable client applications to evolve POCO objects and work with different versions.</span></span>  
> 
> 

<span data-ttu-id="a595e-966">The remainder of this section describes some of the features in the Storage Client Library that facilitate working with multiple entity types in the same table.</span><span class="sxs-lookup"><span data-stu-id="a595e-966">The remainder of this section describes some of the features in the Storage Client Library that facilitate working with multiple entity types in the same table.</span></span>  

#### <a name="retrieving-heterogeneous-entity-types"></a><span data-ttu-id="a595e-967">Retrieving heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-967">Retrieving heterogeneous entity types</span></span>
<span data-ttu-id="a595e-968">If you are using the Storage Client Library, you have three options for working with multiple entity types.</span><span class="sxs-lookup"><span data-stu-id="a595e-968">If you are using the Storage Client Library, you have three options for working with multiple entity types.</span></span>  

<span data-ttu-id="a595e-969">If you know the type of the entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify the entity type when you retrieve the entity as shown in the previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using the Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span><span class="sxs-lookup"><span data-stu-id="a595e-969">If you know the type of the entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify the entity type when you retrieve the entity as shown in the previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using the Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span></span>  

<span data-ttu-id="a595e-970">The second option is to use the **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need to serialize and deserialize the entity to .NET types).</span><span class="sxs-lookup"><span data-stu-id="a595e-970">The second option is to use the **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need to serialize and deserialize the entity to .NET types).</span></span> <span data-ttu-id="a595e-971">The following C# code potentially retrieves multiple entities of different types from the table, but returns all entities as **DynamicTableEntity** instances.</span><span class="sxs-lookup"><span data-stu-id="a595e-971">The following C# code potentially retrieves multiple entities of different types from the table, but returns all entities as **DynamicTableEntity** instances.</span></span> <span data-ttu-id="a595e-972">It then uses the **EntityType** property to determine the type of each entity:</span><span class="sxs-lookup"><span data-stu-id="a595e-972">It then uses the **EntityType** property to determine the type of each entity:</span></span>  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

<span data-ttu-id="a595e-973">Note that to retrieve other properties you must use the **TryGetValue** method on the **Properties** property of the **DynamicTableEntity** class.</span><span class="sxs-lookup"><span data-stu-id="a595e-973">Note that to retrieve other properties you must use the **TryGetValue** method on the **Properties** property of the **DynamicTableEntity** class.</span></span>  

<span data-ttu-id="a595e-974">A third option is to combine using the **DynamicTableEntity** type and an **EntityResolver** instance.</span><span class="sxs-lookup"><span data-stu-id="a595e-974">A third option is to combine using the **DynamicTableEntity** type and an **EntityResolver** instance.</span></span> <span data-ttu-id="a595e-975">This enables you to resolve to multiple POCO types in the same query.</span><span class="sxs-lookup"><span data-stu-id="a595e-975">This enables you to resolve to multiple POCO types in the same query.</span></span> <span data-ttu-id="a595e-976">In this example, the **EntityResolver** delegate is using the **EntityType** property to distinguish between the two types of entity that the query returns.</span><span class="sxs-lookup"><span data-stu-id="a595e-976">In this example, the **EntityResolver** delegate is using the **EntityType** property to distinguish between the two types of entity that the query returns.</span></span> <span data-ttu-id="a595e-977">The **Resolve** method uses the **resolver** delegate to resolve **DynamicTableEntity** instances to **TableEntity** instances.</span><span class="sxs-lookup"><span data-stu-id="a595e-977">The **Resolve** method uses the **resolver** delegate to resolve **DynamicTableEntity** instances to **TableEntity** instances.</span></span>  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a><span data-ttu-id="a595e-978">Modifying heterogeneous entity types</span><span class="sxs-lookup"><span data-stu-id="a595e-978">Modifying heterogeneous entity types</span></span>
<span data-ttu-id="a595e-979">You do not need to know the type of an entity to delete it, and you always know the type of an entity when you insert it.</span><span class="sxs-lookup"><span data-stu-id="a595e-979">You do not need to know the type of an entity to delete it, and you always know the type of an entity when you insert it.</span></span> <span data-ttu-id="a595e-980">However, you can use **DynamicTableEntity** type to update an entity without knowing its type and without using a POCO entity class.</span><span class="sxs-lookup"><span data-stu-id="a595e-980">However, you can use **DynamicTableEntity** type to update an entity without knowing its type and without using a POCO entity class.</span></span> <span data-ttu-id="a595e-981">The following code sample retrieves a single entity, and checks the **EmployeeCount** property exists before updating it.</span><span class="sxs-lookup"><span data-stu-id="a595e-981">The following code sample retrieves a single entity, and checks the **EmployeeCount** property exists before updating it.</span></span>  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a><span data-ttu-id="a595e-982">Controlling access with Shared Access Signatures</span><span class="sxs-lookup"><span data-stu-id="a595e-982">Controlling access with Shared Access Signatures</span></span>
<span data-ttu-id="a595e-983">You can use Shared Access Signature (SAS) tokens to enable client applications to modify (and query) table entities directly without the need to authenticate directly with the table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-983">You can use Shared Access Signature (SAS) tokens to enable client applications to modify (and query) table entities directly without the need to authenticate directly with the table service.</span></span> <span data-ttu-id="a595e-984">Typically, there are three main benefits to using SAS in your application:</span><span class="sxs-lookup"><span data-stu-id="a595e-984">Typically, there are three main benefits to using SAS in your application:</span></span>  

* <span data-ttu-id="a595e-985">You do not need to distribute your storage account key to an insecure platform (such as a mobile device) in order to allow that device to access and modify entities in the Table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-985">You do not need to distribute your storage account key to an insecure platform (such as a mobile device) in order to allow that device to access and modify entities in the Table service.</span></span>  
* <span data-ttu-id="a595e-986">You can offload some of the work that web and worker roles perform in managing your entities to client devices such as end-user computers and mobile devices.</span><span class="sxs-lookup"><span data-stu-id="a595e-986">You can offload some of the work that web and worker roles perform in managing your entities to client devices such as end-user computers and mobile devices.</span></span>  
* <span data-ttu-id="a595e-987">You can assign a constrained and time limited set of permissions to a client (such as allowing read-only access to specific resources).</span><span class="sxs-lookup"><span data-stu-id="a595e-987">You can assign a constrained and time limited set of permissions to a client (such as allowing read-only access to specific resources).</span></span>  

<span data-ttu-id="a595e-988">For more information about using SAS tokens with the Table service, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="a595e-988">For more information about using SAS tokens with the Table service, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>  

<span data-ttu-id="a595e-989">However, you must still generate the SAS tokens that grant a client application to the entities in the table service: you should do this in an environment that has secure access to your storage account keys.</span><span class="sxs-lookup"><span data-stu-id="a595e-989">However, you must still generate the SAS tokens that grant a client application to the entities in the table service: you should do this in an environment that has secure access to your storage account keys.</span></span> <span data-ttu-id="a595e-990">Typically, you use a web or worker role to generate the SAS tokens and deliver them to the client applications that need access to your entities.</span><span class="sxs-lookup"><span data-stu-id="a595e-990">Typically, you use a web or worker role to generate the SAS tokens and deliver them to the client applications that need access to your entities.</span></span> <span data-ttu-id="a595e-991">Because there is still an overhead involved in generating and delivering SAS tokens to clients, you should consider how best to reduce this overhead, especially in high-volume scenarios.</span><span class="sxs-lookup"><span data-stu-id="a595e-991">Because there is still an overhead involved in generating and delivering SAS tokens to clients, you should consider how best to reduce this overhead, especially in high-volume scenarios.</span></span>  

<span data-ttu-id="a595e-992">It is possible to generate a SAS token that grants access to a subset of the entities in a table.</span><span class="sxs-lookup"><span data-stu-id="a595e-992">It is possible to generate a SAS token that grants access to a subset of the entities in a table.</span></span> <span data-ttu-id="a595e-993">By default, you create a SAS token for an entire table, but it is also possible to specify that the SAS token grant access to either a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span><span class="sxs-lookup"><span data-stu-id="a595e-993">By default, you create a SAS token for an entire table, but it is also possible to specify that the SAS token grant access to either a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a595e-994">You might choose to generate SAS tokens for individual users of your system such that each user's SAS token only allows them access to their own entities in the table service.</span><span class="sxs-lookup"><span data-stu-id="a595e-994">You might choose to generate SAS tokens for individual users of your system such that each user's SAS token only allows them access to their own entities in the table service.</span></span>  

### <a name="asynchronous-and-parallel-operations"></a><span data-ttu-id="a595e-995">Asynchronous and parallel operations</span><span class="sxs-lookup"><span data-stu-id="a595e-995">Asynchronous and parallel operations</span></span>
<span data-ttu-id="a595e-996">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span><span class="sxs-lookup"><span data-stu-id="a595e-996">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span></span>
<span data-ttu-id="a595e-997">For example, you might have two or more worker role instances accessing your tables in parallel.</span><span class="sxs-lookup"><span data-stu-id="a595e-997">For example, you might have two or more worker role instances accessing your tables in parallel.</span></span> <span data-ttu-id="a595e-998">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able to access all the partitions in a table.</span><span class="sxs-lookup"><span data-stu-id="a595e-998">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able to access all the partitions in a table.</span></span>  

<span data-ttu-id="a595e-999">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span><span class="sxs-lookup"><span data-stu-id="a595e-999">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span></span> <span data-ttu-id="a595e-1000">The Storage Client Library makes it easy to write asynchronous queries and modifications.</span><span class="sxs-lookup"><span data-stu-id="a595e-1000">The Storage Client Library makes it easy to write asynchronous queries and modifications.</span></span> <span data-ttu-id="a595e-1001">For example, you might start with the synchronous method that retrieves all the entities in a partition as shown in the following C# code:</span><span class="sxs-lookup"><span data-stu-id="a595e-1001">For example, you might start with the synchronous method that retrieves all the entities in a partition as shown in the following C# code:</span></span>  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

<span data-ttu-id="a595e-1002">You can easily modify this code so that the query runs asynchronously as follows:</span><span class="sxs-lookup"><span data-stu-id="a595e-1002">You can easily modify this code so that the query runs asynchronously as follows:</span></span>  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

<span data-ttu-id="a595e-1003">In this asynchronous example, you can see the following changes from the synchronous version:</span><span class="sxs-lookup"><span data-stu-id="a595e-1003">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="a595e-1004">The method signature now includes the **async** modifier and returns a **Task** instance.</span><span class="sxs-lookup"><span data-stu-id="a595e-1004">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="a595e-1005">Instead of calling the **ExecuteSegmented** method to retrieve results, the method now calls the **ExecuteSegmentedAsync** method and uses the **await** modifier to retrieve results asynchronously.</span><span class="sxs-lookup"><span data-stu-id="a595e-1005">Instead of calling the **ExecuteSegmented** method to retrieve results, the method now calls the **ExecuteSegmentedAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="a595e-1006">The client application can call this method multiple times (with different values for the **department** parameter), and each query will run on a separate thread.</span><span class="sxs-lookup"><span data-stu-id="a595e-1006">The client application can call this method multiple times (with different values for the **department** parameter), and each query will run on a separate thread.</span></span>  

<span data-ttu-id="a595e-1007">Note that there is no asynchronous version of the **Execute** method in the **TableQuery** class because the **IEnumerable** interface does not support asynchronous enumeration.</span><span class="sxs-lookup"><span data-stu-id="a595e-1007">Note that there is no asynchronous version of the **Execute** method in the **TableQuery** class because the **IEnumerable** interface does not support asynchronous enumeration.</span></span>  

<span data-ttu-id="a595e-1008">You can also insert, update, and delete entities asynchronously.</span><span class="sxs-lookup"><span data-stu-id="a595e-1008">You can also insert, update, and delete entities asynchronously.</span></span> <span data-ttu-id="a595e-1009">The following C# example shows a simple, synchronous method to insert or replace an employee entity:</span><span class="sxs-lookup"><span data-stu-id="a595e-1009">The following C# example shows a simple, synchronous method to insert or replace an employee entity:</span></span>  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="a595e-1010">You can easily modify this code so that the update runs asynchronously as follows:</span><span class="sxs-lookup"><span data-stu-id="a595e-1010">You can easily modify this code so that the update runs asynchronously as follows:</span></span>  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="a595e-1011">In this asynchronous example, you can see the following changes from the synchronous version:</span><span class="sxs-lookup"><span data-stu-id="a595e-1011">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="a595e-1012">The method signature now includes the **async** modifier and returns a **Task** instance.</span><span class="sxs-lookup"><span data-stu-id="a595e-1012">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="a595e-1013">Instead of calling the **Execute** method to update the entity, the method now calls the **ExecuteAsync** method and uses the **await** modifier to retrieve results asynchronously.</span><span class="sxs-lookup"><span data-stu-id="a595e-1013">Instead of calling the **Execute** method to update the entity, the method now calls the **ExecuteAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="a595e-1014">The client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span><span class="sxs-lookup"><span data-stu-id="a595e-1014">The client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span></span>  

### <a name="credits"></a><span data-ttu-id="a595e-1015">Credits</span><span class="sxs-lookup"><span data-stu-id="a595e-1015">Credits</span></span>
<span data-ttu-id="a595e-1016">We would like to thank the following members of the Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span><span class="sxs-lookup"><span data-stu-id="a595e-1016">We would like to thank the following members of the Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span></span> 

<span data-ttu-id="a595e-1017">We would also like to thank the following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span><span class="sxs-lookup"><span data-stu-id="a595e-1017">We would also like to thank the following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-table-design-guide/storage-table-design-IMAGE29.png






























