---
title: Azure Cosmos DB feature support for MongoDB | Microsoft Docs
description: Learn about the feature support the Azure Cosmos DB MongoDB API provides for MongoDB 3.4.
services: cosmos-db
author: alekseys
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: overview
ms.date: 11/15/2017
ms.author: alekseys
ms.openlocfilehash: d9616f87e76231c3bb587c2018572b7526b471a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871174"
---
# <a name="mongodb-api-support-for-mongodb-features-and-syntax"></a><span data-ttu-id="2c7ba-103">MongoDB API support for MongoDB features and syntax</span><span class="sxs-lookup"><span data-stu-id="2c7ba-103">MongoDB API support for MongoDB features and syntax</span></span>

<span data-ttu-id="2c7ba-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="2c7ba-105">You can communicate with the database's MongoDB API through any of the open source MongoDB client [drivers](https://docs.mongodb.org/ecosystem/drivers).</span><span class="sxs-lookup"><span data-stu-id="2c7ba-105">You can communicate with the database's MongoDB API through any of the open source MongoDB client [drivers](https://docs.mongodb.org/ecosystem/drivers).</span></span> <span data-ttu-id="2c7ba-106">The MongoDB API enables the use of existing client drivers by adhering to the MongoDB [wire protocol](https://docs.mongodb.org/manual/reference/mongodb-wire-protocol).</span><span class="sxs-lookup"><span data-stu-id="2c7ba-106">The MongoDB API enables the use of existing client drivers by adhering to the MongoDB [wire protocol](https://docs.mongodb.org/manual/reference/mongodb-wire-protocol).</span></span>

<span data-ttu-id="2c7ba-107">By using the Azure Cosmos DB MongoDB API, you can enjoy the benefits of the MongoDB APIs you're used to, with all of the enterprise capabilities Azure Cosmos DB provides: [global distribution](distribute-data-globally.md), [automatic sharding](partition-data.md), availability and latency guarantees, automatic indexing of every field, encryption at rest, backups, and much more.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-107">By using the Azure Cosmos DB MongoDB API, you can enjoy the benefits of the MongoDB APIs you're used to, with all of the enterprise capabilities Azure Cosmos DB provides: [global distribution](distribute-data-globally.md), [automatic sharding](partition-data.md), availability and latency guarantees, automatic indexing of every field, encryption at rest, backups, and much more.</span></span>

## <a name="mongodb-protocol-support"></a><span data-ttu-id="2c7ba-108">MongoDB Protocol Support</span><span class="sxs-lookup"><span data-stu-id="2c7ba-108">MongoDB Protocol Support</span></span>

<span data-ttu-id="2c7ba-109">The Azure Cosmos DB MongoDB API is compatible with MongoDB Server version **3.2** by default.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-109">The Azure Cosmos DB MongoDB API is compatible with MongoDB Server version **3.2** by default.</span></span> <span data-ttu-id="2c7ba-110">The supported operators and any limitations or exceptions are listed below.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-110">The supported operators and any limitations or exceptions are listed below.</span></span> <span data-ttu-id="2c7ba-111">Features or query operators added in MongoDB version **3.4** are currently available as a preview feature.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-111">Features or query operators added in MongoDB version **3.4** are currently available as a preview feature.</span></span> <span data-ttu-id="2c7ba-112">Any client driver that understands these protocols should be able to connect to Cosmos DB using the MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-112">Any client driver that understands these protocols should be able to connect to Cosmos DB using the MongoDB API.</span></span>

<span data-ttu-id="2c7ba-113">The [MongoDB aggregation pipeline](#aggregation-pipeline) is also currently available as a separate preview feature.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-113">The [MongoDB aggregation pipeline](#aggregation-pipeline) is also currently available as a separate preview feature.</span></span>

## <a name="mongodb-query-language-support"></a><span data-ttu-id="2c7ba-114">MongoDB query language support</span><span class="sxs-lookup"><span data-stu-id="2c7ba-114">MongoDB query language support</span></span>

<span data-ttu-id="2c7ba-115">Azure Cosmos DB MongoDB API provides comprehensive support for MongoDB query language constructs.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-115">Azure Cosmos DB MongoDB API provides comprehensive support for MongoDB query language constructs.</span></span> <span data-ttu-id="2c7ba-116">Below you can find the detailed list of currently supported operations, operators, stages, commands and options.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-116">Below you can find the detailed list of currently supported operations, operators, stages, commands and options.</span></span>

## <a name="database-commands"></a><span data-ttu-id="2c7ba-117">Database commands</span><span class="sxs-lookup"><span data-stu-id="2c7ba-117">Database commands</span></span>

<span data-ttu-id="2c7ba-118">Azure Cosmos DB supports the following database commands on all MongoDB API accounts.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-118">Azure Cosmos DB supports the following database commands on all MongoDB API accounts.</span></span>

### <a name="query-and-write-operation-commands"></a><span data-ttu-id="2c7ba-119">Query and write operation commands</span><span class="sxs-lookup"><span data-stu-id="2c7ba-119">Query and write operation commands</span></span>
- <span data-ttu-id="2c7ba-120">delete</span><span class="sxs-lookup"><span data-stu-id="2c7ba-120">delete</span></span>
- <span data-ttu-id="2c7ba-121">find</span><span class="sxs-lookup"><span data-stu-id="2c7ba-121">find</span></span>
- <span data-ttu-id="2c7ba-122">findAndModify</span><span class="sxs-lookup"><span data-stu-id="2c7ba-122">findAndModify</span></span>
- <span data-ttu-id="2c7ba-123">getLastError</span><span class="sxs-lookup"><span data-stu-id="2c7ba-123">getLastError</span></span>
- <span data-ttu-id="2c7ba-124">getMore</span><span class="sxs-lookup"><span data-stu-id="2c7ba-124">getMore</span></span>
- <span data-ttu-id="2c7ba-125">insert</span><span class="sxs-lookup"><span data-stu-id="2c7ba-125">insert</span></span>
- <span data-ttu-id="2c7ba-126">update</span><span class="sxs-lookup"><span data-stu-id="2c7ba-126">update</span></span>

### <a name="authentication-commands"></a><span data-ttu-id="2c7ba-127">Authentication commands</span><span class="sxs-lookup"><span data-stu-id="2c7ba-127">Authentication commands</span></span>
- <span data-ttu-id="2c7ba-128">logout</span><span class="sxs-lookup"><span data-stu-id="2c7ba-128">logout</span></span>
- <span data-ttu-id="2c7ba-129">authenticate</span><span class="sxs-lookup"><span data-stu-id="2c7ba-129">authenticate</span></span>
- <span data-ttu-id="2c7ba-130">getnonce</span><span class="sxs-lookup"><span data-stu-id="2c7ba-130">getnonce</span></span>

### <a name="administration-commands"></a><span data-ttu-id="2c7ba-131">Administration commands</span><span class="sxs-lookup"><span data-stu-id="2c7ba-131">Administration commands</span></span>
- <span data-ttu-id="2c7ba-132">dropDatabase</span><span class="sxs-lookup"><span data-stu-id="2c7ba-132">dropDatabase</span></span>
- <span data-ttu-id="2c7ba-133">listCollections</span><span class="sxs-lookup"><span data-stu-id="2c7ba-133">listCollections</span></span>
- <span data-ttu-id="2c7ba-134">drop</span><span class="sxs-lookup"><span data-stu-id="2c7ba-134">drop</span></span>
- <span data-ttu-id="2c7ba-135">create</span><span class="sxs-lookup"><span data-stu-id="2c7ba-135">create</span></span>
- <span data-ttu-id="2c7ba-136">filemd5</span><span class="sxs-lookup"><span data-stu-id="2c7ba-136">filemd5</span></span>
- <span data-ttu-id="2c7ba-137">createIndexes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-137">createIndexes</span></span>
- <span data-ttu-id="2c7ba-138">listIndexes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-138">listIndexes</span></span>
- <span data-ttu-id="2c7ba-139">dropIndexes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-139">dropIndexes</span></span>
- <span data-ttu-id="2c7ba-140">connectionStatus</span><span class="sxs-lookup"><span data-stu-id="2c7ba-140">connectionStatus</span></span>
- <span data-ttu-id="2c7ba-141">reIndex</span><span class="sxs-lookup"><span data-stu-id="2c7ba-141">reIndex</span></span>

### <a name="diagnostics-commands"></a><span data-ttu-id="2c7ba-142">Diagnostics commands</span><span class="sxs-lookup"><span data-stu-id="2c7ba-142">Diagnostics commands</span></span>
- <span data-ttu-id="2c7ba-143">buildInfo</span><span class="sxs-lookup"><span data-stu-id="2c7ba-143">buildInfo</span></span>
- <span data-ttu-id="2c7ba-144">collStats</span><span class="sxs-lookup"><span data-stu-id="2c7ba-144">collStats</span></span>
- <span data-ttu-id="2c7ba-145">dbStats</span><span class="sxs-lookup"><span data-stu-id="2c7ba-145">dbStats</span></span>
- <span data-ttu-id="2c7ba-146">hostInfo</span><span class="sxs-lookup"><span data-stu-id="2c7ba-146">hostInfo</span></span>
- <span data-ttu-id="2c7ba-147">listDatabases</span><span class="sxs-lookup"><span data-stu-id="2c7ba-147">listDatabases</span></span>
- <span data-ttu-id="2c7ba-148">whatsmyuri</span><span class="sxs-lookup"><span data-stu-id="2c7ba-148">whatsmyuri</span></span>

<a name="aggregation-pipeline"/>

## <a name="aggregation-pipelinea"></a><span data-ttu-id="2c7ba-149">Aggregation pipeline</a></span><span class="sxs-lookup"><span data-stu-id="2c7ba-149">Aggregation pipeline</a></span></span>

<span data-ttu-id="2c7ba-150">Azure Cosmos DB supports aggregation pipeline in public preview.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-150">Azure Cosmos DB supports aggregation pipeline in public preview.</span></span> <span data-ttu-id="2c7ba-151">See the [Azure blog](https://aka.ms/mongodb-aggregation) for instructions on how to onboard to the public preview.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-151">See the [Azure blog](https://aka.ms/mongodb-aggregation) for instructions on how to onboard to the public preview.</span></span>

### <a name="aggregation-commands"></a><span data-ttu-id="2c7ba-152">Aggregation commands</span><span class="sxs-lookup"><span data-stu-id="2c7ba-152">Aggregation commands</span></span>
- <span data-ttu-id="2c7ba-153">aggregate</span><span class="sxs-lookup"><span data-stu-id="2c7ba-153">aggregate</span></span>
- <span data-ttu-id="2c7ba-154">count</span><span class="sxs-lookup"><span data-stu-id="2c7ba-154">count</span></span>
- <span data-ttu-id="2c7ba-155">distinct</span><span class="sxs-lookup"><span data-stu-id="2c7ba-155">distinct</span></span>

### <a name="aggregation-stages"></a><span data-ttu-id="2c7ba-156">Aggregation stages</span><span class="sxs-lookup"><span data-stu-id="2c7ba-156">Aggregation stages</span></span>
- <span data-ttu-id="2c7ba-157">$project</span><span class="sxs-lookup"><span data-stu-id="2c7ba-157">$project</span></span>
- <span data-ttu-id="2c7ba-158">$match</span><span class="sxs-lookup"><span data-stu-id="2c7ba-158">$match</span></span>
- <span data-ttu-id="2c7ba-159">$limit</span><span class="sxs-lookup"><span data-stu-id="2c7ba-159">$limit</span></span>
- <span data-ttu-id="2c7ba-160">$skip</span><span class="sxs-lookup"><span data-stu-id="2c7ba-160">$skip</span></span>
- <span data-ttu-id="2c7ba-161">$unwind</span><span class="sxs-lookup"><span data-stu-id="2c7ba-161">$unwind</span></span>
- <span data-ttu-id="2c7ba-162">$group</span><span class="sxs-lookup"><span data-stu-id="2c7ba-162">$group</span></span>
- <span data-ttu-id="2c7ba-163">$sample</span><span class="sxs-lookup"><span data-stu-id="2c7ba-163">$sample</span></span>
- <span data-ttu-id="2c7ba-164">$sort</span><span class="sxs-lookup"><span data-stu-id="2c7ba-164">$sort</span></span>
- <span data-ttu-id="2c7ba-165">$lookup</span><span class="sxs-lookup"><span data-stu-id="2c7ba-165">$lookup</span></span>
- <span data-ttu-id="2c7ba-166">$out</span><span class="sxs-lookup"><span data-stu-id="2c7ba-166">$out</span></span>
- <span data-ttu-id="2c7ba-167">$count</span><span class="sxs-lookup"><span data-stu-id="2c7ba-167">$count</span></span>
- <span data-ttu-id="2c7ba-168">$addFields</span><span class="sxs-lookup"><span data-stu-id="2c7ba-168">$addFields</span></span>

### <a name="aggregation-expressions"></a><span data-ttu-id="2c7ba-169">Aggregation expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-169">Aggregation expressions</span></span>

#### <a name="boolean-expressions"></a><span data-ttu-id="2c7ba-170">Boolean expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-170">Boolean expressions</span></span>
- <span data-ttu-id="2c7ba-171">$and</span><span class="sxs-lookup"><span data-stu-id="2c7ba-171">$and</span></span>
- <span data-ttu-id="2c7ba-172">$or</span><span class="sxs-lookup"><span data-stu-id="2c7ba-172">$or</span></span>
- <span data-ttu-id="2c7ba-173">$not</span><span class="sxs-lookup"><span data-stu-id="2c7ba-173">$not</span></span>

#### <a name="set-expressions"></a><span data-ttu-id="2c7ba-174">Set expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-174">Set expressions</span></span>
- <span data-ttu-id="2c7ba-175">$setEquals</span><span class="sxs-lookup"><span data-stu-id="2c7ba-175">$setEquals</span></span>
- <span data-ttu-id="2c7ba-176">$setIntersection</span><span class="sxs-lookup"><span data-stu-id="2c7ba-176">$setIntersection</span></span>
- <span data-ttu-id="2c7ba-177">$setUnion</span><span class="sxs-lookup"><span data-stu-id="2c7ba-177">$setUnion</span></span>
- <span data-ttu-id="2c7ba-178">$setDifference</span><span class="sxs-lookup"><span data-stu-id="2c7ba-178">$setDifference</span></span>
- <span data-ttu-id="2c7ba-179">$setIsSubset</span><span class="sxs-lookup"><span data-stu-id="2c7ba-179">$setIsSubset</span></span>
- <span data-ttu-id="2c7ba-180">$anyElementTrue</span><span class="sxs-lookup"><span data-stu-id="2c7ba-180">$anyElementTrue</span></span>
- <span data-ttu-id="2c7ba-181">$allElementsTrue</span><span class="sxs-lookup"><span data-stu-id="2c7ba-181">$allElementsTrue</span></span>

#### <a name="comparison-expressions"></a><span data-ttu-id="2c7ba-182">Comparison expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-182">Comparison expressions</span></span>
- <span data-ttu-id="2c7ba-183">$cmp</span><span class="sxs-lookup"><span data-stu-id="2c7ba-183">$cmp</span></span>
- <span data-ttu-id="2c7ba-184">$eq</span><span class="sxs-lookup"><span data-stu-id="2c7ba-184">$eq</span></span>
- <span data-ttu-id="2c7ba-185">$gt</span><span class="sxs-lookup"><span data-stu-id="2c7ba-185">$gt</span></span>
- <span data-ttu-id="2c7ba-186">$gte</span><span class="sxs-lookup"><span data-stu-id="2c7ba-186">$gte</span></span>
- <span data-ttu-id="2c7ba-187">$lt</span><span class="sxs-lookup"><span data-stu-id="2c7ba-187">$lt</span></span>
- <span data-ttu-id="2c7ba-188">$lte</span><span class="sxs-lookup"><span data-stu-id="2c7ba-188">$lte</span></span>
- <span data-ttu-id="2c7ba-189">$ne</span><span class="sxs-lookup"><span data-stu-id="2c7ba-189">$ne</span></span>

#### <a name="arithmetic-expressions"></a><span data-ttu-id="2c7ba-190">Arithmetic expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-190">Arithmetic expressions</span></span>
- <span data-ttu-id="2c7ba-191">$abs</span><span class="sxs-lookup"><span data-stu-id="2c7ba-191">$abs</span></span>
- <span data-ttu-id="2c7ba-192">$add</span><span class="sxs-lookup"><span data-stu-id="2c7ba-192">$add</span></span>
- <span data-ttu-id="2c7ba-193">$ceil</span><span class="sxs-lookup"><span data-stu-id="2c7ba-193">$ceil</span></span>
- <span data-ttu-id="2c7ba-194">$divide</span><span class="sxs-lookup"><span data-stu-id="2c7ba-194">$divide</span></span>
- <span data-ttu-id="2c7ba-195">$exp</span><span class="sxs-lookup"><span data-stu-id="2c7ba-195">$exp</span></span>
- <span data-ttu-id="2c7ba-196">$floor</span><span class="sxs-lookup"><span data-stu-id="2c7ba-196">$floor</span></span>
- <span data-ttu-id="2c7ba-197">$ln</span><span class="sxs-lookup"><span data-stu-id="2c7ba-197">$ln</span></span>
- <span data-ttu-id="2c7ba-198">$log</span><span class="sxs-lookup"><span data-stu-id="2c7ba-198">$log</span></span>
- <span data-ttu-id="2c7ba-199">$log10</span><span class="sxs-lookup"><span data-stu-id="2c7ba-199">$log10</span></span>
- <span data-ttu-id="2c7ba-200">$mod</span><span class="sxs-lookup"><span data-stu-id="2c7ba-200">$mod</span></span>
- <span data-ttu-id="2c7ba-201">$multiply</span><span class="sxs-lookup"><span data-stu-id="2c7ba-201">$multiply</span></span>
- <span data-ttu-id="2c7ba-202">$pow</span><span class="sxs-lookup"><span data-stu-id="2c7ba-202">$pow</span></span>
- <span data-ttu-id="2c7ba-203">$sqrt</span><span class="sxs-lookup"><span data-stu-id="2c7ba-203">$sqrt</span></span>
- <span data-ttu-id="2c7ba-204">$subtract</span><span class="sxs-lookup"><span data-stu-id="2c7ba-204">$subtract</span></span>
- <span data-ttu-id="2c7ba-205">$trunc</span><span class="sxs-lookup"><span data-stu-id="2c7ba-205">$trunc</span></span>

#### <a name="string-expressions"></a><span data-ttu-id="2c7ba-206">String expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-206">String expressions</span></span>
- <span data-ttu-id="2c7ba-207">$concat</span><span class="sxs-lookup"><span data-stu-id="2c7ba-207">$concat</span></span>
- <span data-ttu-id="2c7ba-208">$indexOfBytes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-208">$indexOfBytes</span></span>
- <span data-ttu-id="2c7ba-209">$indexOfCP</span><span class="sxs-lookup"><span data-stu-id="2c7ba-209">$indexOfCP</span></span>
- <span data-ttu-id="2c7ba-210">$split</span><span class="sxs-lookup"><span data-stu-id="2c7ba-210">$split</span></span>
- <span data-ttu-id="2c7ba-211">$strLenBytes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-211">$strLenBytes</span></span>
- <span data-ttu-id="2c7ba-212">$strLenCP</span><span class="sxs-lookup"><span data-stu-id="2c7ba-212">$strLenCP</span></span>
- <span data-ttu-id="2c7ba-213">$strcasecmp</span><span class="sxs-lookup"><span data-stu-id="2c7ba-213">$strcasecmp</span></span>
- <span data-ttu-id="2c7ba-214">$substr</span><span class="sxs-lookup"><span data-stu-id="2c7ba-214">$substr</span></span>
- <span data-ttu-id="2c7ba-215">$substrBytes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-215">$substrBytes</span></span>
- <span data-ttu-id="2c7ba-216">$substrCP</span><span class="sxs-lookup"><span data-stu-id="2c7ba-216">$substrCP</span></span>
- <span data-ttu-id="2c7ba-217">$toLower</span><span class="sxs-lookup"><span data-stu-id="2c7ba-217">$toLower</span></span>
- <span data-ttu-id="2c7ba-218">$toUpper</span><span class="sxs-lookup"><span data-stu-id="2c7ba-218">$toUpper</span></span>

#### <a name="array-expressions"></a><span data-ttu-id="2c7ba-219">Array expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-219">Array expressions</span></span>
- <span data-ttu-id="2c7ba-220">$arrayElemAt</span><span class="sxs-lookup"><span data-stu-id="2c7ba-220">$arrayElemAt</span></span>
- <span data-ttu-id="2c7ba-221">$concatArrays</span><span class="sxs-lookup"><span data-stu-id="2c7ba-221">$concatArrays</span></span>
- <span data-ttu-id="2c7ba-222">$filter</span><span class="sxs-lookup"><span data-stu-id="2c7ba-222">$filter</span></span>
- <span data-ttu-id="2c7ba-223">$indexOfArray</span><span class="sxs-lookup"><span data-stu-id="2c7ba-223">$indexOfArray</span></span>
- <span data-ttu-id="2c7ba-224">$isArray</span><span class="sxs-lookup"><span data-stu-id="2c7ba-224">$isArray</span></span>
- <span data-ttu-id="2c7ba-225">$range</span><span class="sxs-lookup"><span data-stu-id="2c7ba-225">$range</span></span>
- <span data-ttu-id="2c7ba-226">$reverseArray</span><span class="sxs-lookup"><span data-stu-id="2c7ba-226">$reverseArray</span></span>
- <span data-ttu-id="2c7ba-227">$size</span><span class="sxs-lookup"><span data-stu-id="2c7ba-227">$size</span></span>
- <span data-ttu-id="2c7ba-228">$slice</span><span class="sxs-lookup"><span data-stu-id="2c7ba-228">$slice</span></span>
- <span data-ttu-id="2c7ba-229">$in</span><span class="sxs-lookup"><span data-stu-id="2c7ba-229">$in</span></span>

#### <a name="date-expressions"></a><span data-ttu-id="2c7ba-230">Date expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-230">Date expressions</span></span>
- <span data-ttu-id="2c7ba-231">$dayOfYear</span><span class="sxs-lookup"><span data-stu-id="2c7ba-231">$dayOfYear</span></span>
- <span data-ttu-id="2c7ba-232">$dayOfMonth</span><span class="sxs-lookup"><span data-stu-id="2c7ba-232">$dayOfMonth</span></span>
- <span data-ttu-id="2c7ba-233">$dayOfWeek</span><span class="sxs-lookup"><span data-stu-id="2c7ba-233">$dayOfWeek</span></span>
- <span data-ttu-id="2c7ba-234">$year</span><span class="sxs-lookup"><span data-stu-id="2c7ba-234">$year</span></span>
- <span data-ttu-id="2c7ba-235">$month</span><span class="sxs-lookup"><span data-stu-id="2c7ba-235">$month</span></span>
- <span data-ttu-id="2c7ba-236">$week</span><span class="sxs-lookup"><span data-stu-id="2c7ba-236">$week</span></span>
- <span data-ttu-id="2c7ba-237">$hour</span><span class="sxs-lookup"><span data-stu-id="2c7ba-237">$hour</span></span>
- <span data-ttu-id="2c7ba-238">$minute</span><span class="sxs-lookup"><span data-stu-id="2c7ba-238">$minute</span></span>
- <span data-ttu-id="2c7ba-239">$second</span><span class="sxs-lookup"><span data-stu-id="2c7ba-239">$second</span></span>
- <span data-ttu-id="2c7ba-240">$millisecond</span><span class="sxs-lookup"><span data-stu-id="2c7ba-240">$millisecond</span></span>
- <span data-ttu-id="2c7ba-241">$isoDayOfWeek</span><span class="sxs-lookup"><span data-stu-id="2c7ba-241">$isoDayOfWeek</span></span>
- <span data-ttu-id="2c7ba-242">$isoWeek</span><span class="sxs-lookup"><span data-stu-id="2c7ba-242">$isoWeek</span></span>

#### <a name="conditional-expressions"></a><span data-ttu-id="2c7ba-243">Conditional expressions</span><span class="sxs-lookup"><span data-stu-id="2c7ba-243">Conditional expressions</span></span>
- <span data-ttu-id="2c7ba-244">$cond</span><span class="sxs-lookup"><span data-stu-id="2c7ba-244">$cond</span></span>
- <span data-ttu-id="2c7ba-245">$ifNull</span><span class="sxs-lookup"><span data-stu-id="2c7ba-245">$ifNull</span></span>

## <a name="aggregation-accumulators"></a><span data-ttu-id="2c7ba-246">Aggregation accumulators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-246">Aggregation accumulators</span></span>
- <span data-ttu-id="2c7ba-247">$sum</span><span class="sxs-lookup"><span data-stu-id="2c7ba-247">$sum</span></span>
- <span data-ttu-id="2c7ba-248">$avg</span><span class="sxs-lookup"><span data-stu-id="2c7ba-248">$avg</span></span>
- <span data-ttu-id="2c7ba-249">$first</span><span class="sxs-lookup"><span data-stu-id="2c7ba-249">$first</span></span>
- <span data-ttu-id="2c7ba-250">$last</span><span class="sxs-lookup"><span data-stu-id="2c7ba-250">$last</span></span>
- <span data-ttu-id="2c7ba-251">$max</span><span class="sxs-lookup"><span data-stu-id="2c7ba-251">$max</span></span>
- <span data-ttu-id="2c7ba-252">$min</span><span class="sxs-lookup"><span data-stu-id="2c7ba-252">$min</span></span>
- <span data-ttu-id="2c7ba-253">$push</span><span class="sxs-lookup"><span data-stu-id="2c7ba-253">$push</span></span>
- <span data-ttu-id="2c7ba-254">$addToSet</span><span class="sxs-lookup"><span data-stu-id="2c7ba-254">$addToSet</span></span>

## <a name="operators"></a><span data-ttu-id="2c7ba-255">Operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-255">Operators</span></span>

<span data-ttu-id="2c7ba-256">Following operators are supported with corresponding examples of their use.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-256">Following operators are supported with corresponding examples of their use.</span></span> <span data-ttu-id="2c7ba-257">Consider this sample document used in the queries below:</span><span class="sxs-lookup"><span data-stu-id="2c7ba-257">Consider this sample document used in the queries below:</span></span>

```json
{
  "Volcano Name": "Rainier",
  "Country": "United States",
  "Region": "US-Washington",
  "Location": {
    "type": "Point",
    "coordinates": [
      -121.758,
      46.87
    ]
  },
  "Elevation": 4392,
  "Type": "Stratovolcano",
  "Status": "Dendrochronology",
  "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
}
```

<span data-ttu-id="2c7ba-258">Operator</span><span class="sxs-lookup"><span data-stu-id="2c7ba-258">Operator</span></span> | <span data-ttu-id="2c7ba-259">Example</span><span class="sxs-lookup"><span data-stu-id="2c7ba-259">Example</span></span> |
--- | --- |
<span data-ttu-id="2c7ba-260">$eq</span><span class="sxs-lookup"><span data-stu-id="2c7ba-260">$eq</span></span> | ``` { "Volcano Name": { $eq: "Rainier" } } ``` |  | -
<span data-ttu-id="2c7ba-261">$gt</span><span class="sxs-lookup"><span data-stu-id="2c7ba-261">$gt</span></span> | ``` { "Elevation": { $gt: 4000 } } ``` |  | -
<span data-ttu-id="2c7ba-262">$gte</span><span class="sxs-lookup"><span data-stu-id="2c7ba-262">$gte</span></span> | ``` { "Elevation": { $gte: 4392 } } ``` |  | -
<span data-ttu-id="2c7ba-263">$lt</span><span class="sxs-lookup"><span data-stu-id="2c7ba-263">$lt</span></span> | ``` { "Elevation": { $lt: 5000 } } ``` |  | -
<span data-ttu-id="2c7ba-264">$lte</span><span class="sxs-lookup"><span data-stu-id="2c7ba-264">$lte</span></span> | ``` { "Elevation": { $lte: 5000 } } ``` | | -
<span data-ttu-id="2c7ba-265">$ne</span><span class="sxs-lookup"><span data-stu-id="2c7ba-265">$ne</span></span> | ``` { "Elevation": { $ne: 1 } } ``` |  | -
<span data-ttu-id="2c7ba-266">$in</span><span class="sxs-lookup"><span data-stu-id="2c7ba-266">$in</span></span> | ``` { "Volcano Name": { $in: ["St. Helens", "Rainier", "Glacier Peak"] } } ``` |  | -
<span data-ttu-id="2c7ba-267">$nin</span><span class="sxs-lookup"><span data-stu-id="2c7ba-267">$nin</span></span> | ``` { "Volcano Name": { $nin: ["Lassen Peak", "Hood", "Baker"] } } ``` | | -
<span data-ttu-id="2c7ba-268">$or</span><span class="sxs-lookup"><span data-stu-id="2c7ba-268">$or</span></span> | ``` { $or: [ { Elevation: { $lt: 4000 } }, { "Volcano Name": "Rainier" } ] } ``` |  | -
<span data-ttu-id="2c7ba-269">$and</span><span class="sxs-lookup"><span data-stu-id="2c7ba-269">$and</span></span> | ``` { $and: [ { Elevation: { $gt: 4000 } }, { "Volcano Name": "Rainier" } ] } ``` |  | -
<span data-ttu-id="2c7ba-270">$not</span><span class="sxs-lookup"><span data-stu-id="2c7ba-270">$not</span></span> | ``` { "Elevation": { $not: { $gt: 5000 } } } ```|  | -
<span data-ttu-id="2c7ba-271">$nor</span><span class="sxs-lookup"><span data-stu-id="2c7ba-271">$nor</span></span> | ``` { $nor: [ { "Elevation": { $lt: 4000 } }, { "Volcano Name": "Baker" } ] } ``` |  | -
<span data-ttu-id="2c7ba-272">$exists</span><span class="sxs-lookup"><span data-stu-id="2c7ba-272">$exists</span></span> | ``` { "Status": { $exists: true } } ```|  | -
<span data-ttu-id="2c7ba-273">$type</span><span class="sxs-lookup"><span data-stu-id="2c7ba-273">$type</span></span> | ``` { "Status": { $type: "string" } } ```|  | -
<span data-ttu-id="2c7ba-274">$mod</span><span class="sxs-lookup"><span data-stu-id="2c7ba-274">$mod</span></span> | ``` { "Elevation": { $mod: [ 4, 0 ] } } ``` |  | -
<span data-ttu-id="2c7ba-275">$regex</span><span class="sxs-lookup"><span data-stu-id="2c7ba-275">$regex</span></span> | ``` { "Volcano Name": { $regex: "^Rain"} } ```|  | -

### <a name="notes"></a><span data-ttu-id="2c7ba-276">Notes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-276">Notes</span></span>

<span data-ttu-id="2c7ba-277">In $regex queries, Left-anchored expressions allow index search.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-277">In $regex queries, Left-anchored expressions allow index search.</span></span> <span data-ttu-id="2c7ba-278">However, using 'i' modifier (case-insensitivity) and 'm' modifier (multiline) causes the collection scan in all expressions.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-278">However, using 'i' modifier (case-insensitivity) and 'm' modifier (multiline) causes the collection scan in all expressions.</span></span>
<span data-ttu-id="2c7ba-279">When there's a need to include '$' or '|', it is best to create two (or more) regex queries.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-279">When there's a need to include '$' or '|', it is best to create two (or more) regex queries.</span></span> <span data-ttu-id="2c7ba-280">For example, given the following original query: ```find({x:{$regex: /^abc$/})```, it has to be modified as follows: ```find({x:{$regex: /^abc/, x:{$regex:/^abc$/}})```.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-280">For example, given the following original query: ```find({x:{$regex: /^abc$/})```, it has to be modified as follows: ```find({x:{$regex: /^abc/, x:{$regex:/^abc$/}})```.</span></span>
<span data-ttu-id="2c7ba-281">The first part will use the index to restrict the search to those documents beginning with ^abc and the second part will match the exact entries.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-281">The first part will use the index to restrict the search to those documents beginning with ^abc and the second part will match the exact entries.</span></span> <span data-ttu-id="2c7ba-282">The bar operator '|' acts as an "or" function - the query ```find({x:{$regex: /^abc|^def/})``` matches the documents in which field 'x' has values that begin with "abc" or "def".</span><span class="sxs-lookup"><span data-stu-id="2c7ba-282">The bar operator '|' acts as an "or" function - the query ```find({x:{$regex: /^abc|^def/})``` matches the documents in which field 'x' has values that begin with "abc" or "def".</span></span> <span data-ttu-id="2c7ba-283">To utilize the index, it's recommended to break the query into two different queries joined by the $or operator: ```find( {$or : [{x: $regex: /^abc/}, {$regex: /^def/}] })```.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-283">To utilize the index, it's recommended to break the query into two different queries joined by the $or operator: ```find( {$or : [{x: $regex: /^abc/}, {$regex: /^def/}] })```.</span></span>

### <a name="update-operators"></a><span data-ttu-id="2c7ba-284">Update operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-284">Update operators</span></span>

#### <a name="field-update-operators"></a><span data-ttu-id="2c7ba-285">Field update operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-285">Field update operators</span></span>
- <span data-ttu-id="2c7ba-286">$inc</span><span class="sxs-lookup"><span data-stu-id="2c7ba-286">$inc</span></span>
- <span data-ttu-id="2c7ba-287">$mul</span><span class="sxs-lookup"><span data-stu-id="2c7ba-287">$mul</span></span>
- <span data-ttu-id="2c7ba-288">$rename</span><span class="sxs-lookup"><span data-stu-id="2c7ba-288">$rename</span></span>
- <span data-ttu-id="2c7ba-289">$setOnInsert</span><span class="sxs-lookup"><span data-stu-id="2c7ba-289">$setOnInsert</span></span>
- <span data-ttu-id="2c7ba-290">$set</span><span class="sxs-lookup"><span data-stu-id="2c7ba-290">$set</span></span>
- <span data-ttu-id="2c7ba-291">$unset</span><span class="sxs-lookup"><span data-stu-id="2c7ba-291">$unset</span></span>
- <span data-ttu-id="2c7ba-292">$min</span><span class="sxs-lookup"><span data-stu-id="2c7ba-292">$min</span></span>
- <span data-ttu-id="2c7ba-293">$max</span><span class="sxs-lookup"><span data-stu-id="2c7ba-293">$max</span></span>
- <span data-ttu-id="2c7ba-294">$currentDate</span><span class="sxs-lookup"><span data-stu-id="2c7ba-294">$currentDate</span></span>

#### <a name="array-update-operators"></a><span data-ttu-id="2c7ba-295">Array update operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-295">Array update operators</span></span>
- <span data-ttu-id="2c7ba-296">$addToSet</span><span class="sxs-lookup"><span data-stu-id="2c7ba-296">$addToSet</span></span>
- <span data-ttu-id="2c7ba-297">$pop</span><span class="sxs-lookup"><span data-stu-id="2c7ba-297">$pop</span></span>
- <span data-ttu-id="2c7ba-298">$pullAll</span><span class="sxs-lookup"><span data-stu-id="2c7ba-298">$pullAll</span></span>
- <span data-ttu-id="2c7ba-299">$pull  (Note: $pull with condition is not supported)</span><span class="sxs-lookup"><span data-stu-id="2c7ba-299">$pull  (Note: $pull with condition is not supported)</span></span>
- <span data-ttu-id="2c7ba-300">$pushAll</span><span class="sxs-lookup"><span data-stu-id="2c7ba-300">$pushAll</span></span>
- <span data-ttu-id="2c7ba-301">$push</span><span class="sxs-lookup"><span data-stu-id="2c7ba-301">$push</span></span>
- <span data-ttu-id="2c7ba-302">$each</span><span class="sxs-lookup"><span data-stu-id="2c7ba-302">$each</span></span>
- <span data-ttu-id="2c7ba-303">$slice</span><span class="sxs-lookup"><span data-stu-id="2c7ba-303">$slice</span></span>
- <span data-ttu-id="2c7ba-304">$sort</span><span class="sxs-lookup"><span data-stu-id="2c7ba-304">$sort</span></span>
- <span data-ttu-id="2c7ba-305">$position</span><span class="sxs-lookup"><span data-stu-id="2c7ba-305">$position</span></span>

#### <a name="bitwise-update-operator"></a><span data-ttu-id="2c7ba-306">Bitwise update operator</span><span class="sxs-lookup"><span data-stu-id="2c7ba-306">Bitwise update operator</span></span>
- <span data-ttu-id="2c7ba-307">$bit</span><span class="sxs-lookup"><span data-stu-id="2c7ba-307">$bit</span></span>

### <a name="geospatial-operators"></a><span data-ttu-id="2c7ba-308">Geospatial operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-308">Geospatial operators</span></span>

<span data-ttu-id="2c7ba-309">Operator</span><span class="sxs-lookup"><span data-stu-id="2c7ba-309">Operator</span></span> | <span data-ttu-id="2c7ba-310">Example</span><span class="sxs-lookup"><span data-stu-id="2c7ba-310">Example</span></span> 
--- | --- |
<span data-ttu-id="2c7ba-311">$geoWithin</span><span class="sxs-lookup"><span data-stu-id="2c7ba-311">$geoWithin</span></span> | ```{ "Location.coordinates": { $geoWithin: { $centerSphere: [ [ -121, 46 ], 5 ] } } }``` | <span data-ttu-id="2c7ba-312">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-312">Yes</span></span>
<span data-ttu-id="2c7ba-313">$geoIntersects</span><span class="sxs-lookup"><span data-stu-id="2c7ba-313">$geoIntersects</span></span> |  ```{ "Location.coordinates": { $geoIntersects: { $geometry: { type: "Polygon", coordinates: [ [ [ -121.9, 46.7 ], [ -121.5, 46.7 ], [ -121.5, 46.9 ], [ -121.9, 46.9 ], [ -121.9, 46.7 ] ] ] } } } }``` | <span data-ttu-id="2c7ba-314">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-314">Yes</span></span>
<span data-ttu-id="2c7ba-315">$near</span><span class="sxs-lookup"><span data-stu-id="2c7ba-315">$near</span></span> | ```{ "Location.coordinates": { $near: { $geometry: { type: "Polygon", coordinates: [ [ [ -121.9, 46.7 ], [ -121.5, 46.7 ], [ -121.5, 46.9 ], [ -121.9, 46.9 ], [ -121.9, 46.7 ] ] ] } } } }``` | <span data-ttu-id="2c7ba-316">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-316">Yes</span></span>
<span data-ttu-id="2c7ba-317">$nearSphere</span><span class="sxs-lookup"><span data-stu-id="2c7ba-317">$nearSphere</span></span> | ```{ "Location.coordinates": { $nearSphere : [ -121, 46  ], $maxDistance: 0.50 } }``` | <span data-ttu-id="2c7ba-318">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-318">Yes</span></span>
<span data-ttu-id="2c7ba-319">$geometry</span><span class="sxs-lookup"><span data-stu-id="2c7ba-319">$geometry</span></span> | ```{ "Location.coordinates": { $geoWithin: { $geometry: { type: "Polygon", coordinates: [ [ [ -121.9, 46.7 ], [ -121.5, 46.7 ], [ -121.5, 46.9 ], [ -121.9, 46.9 ], [ -121.9, 46.7 ] ] ] } } } }``` | <span data-ttu-id="2c7ba-320">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-320">Yes</span></span>
<span data-ttu-id="2c7ba-321">$minDistance</span><span class="sxs-lookup"><span data-stu-id="2c7ba-321">$minDistance</span></span> | ```{ "Location.coordinates": { $nearSphere : { $geometry: {type: "Point", coordinates: [ -121, 46 ]}, $minDistance: 1000, $maxDistance: 1000000 } } }``` | <span data-ttu-id="2c7ba-322">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-322">Yes</span></span>
<span data-ttu-id="2c7ba-323">$maxDistance</span><span class="sxs-lookup"><span data-stu-id="2c7ba-323">$maxDistance</span></span> | ```{ "Location.coordinates": { $nearSphere : [ -121, 46  ], $maxDistance: 0.50 } }``` | <span data-ttu-id="2c7ba-324">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-324">Yes</span></span>
<span data-ttu-id="2c7ba-325">$center</span><span class="sxs-lookup"><span data-stu-id="2c7ba-325">$center</span></span> | ```{ "Location.coordinates": { $geoWithin: { $center: [ [-121, 46], 1 ] } } }``` | <span data-ttu-id="2c7ba-326">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-326">Yes</span></span>
<span data-ttu-id="2c7ba-327">$centerSphere</span><span class="sxs-lookup"><span data-stu-id="2c7ba-327">$centerSphere</span></span> | ```{ "Location.coordinates": { $geoWithin: { $centerSphere: [ [ -121, 46 ], 5 ] } } }``` | <span data-ttu-id="2c7ba-328">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-328">Yes</span></span>
<span data-ttu-id="2c7ba-329">$box</span><span class="sxs-lookup"><span data-stu-id="2c7ba-329">$box</span></span> | ```{ "Location.coordinates": { $geoWithin: { $box:  [ [ 0, 0 ], [ -122, 47 ] ] } } }``` | <span data-ttu-id="2c7ba-330">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-330">Yes</span></span>
<span data-ttu-id="2c7ba-331">$polygon</span><span class="sxs-lookup"><span data-stu-id="2c7ba-331">$polygon</span></span> | ```{ "Location.coordinates": { $near: { $geometry: { type: "Polygon", coordinates: [ [ [ -121.9, 46.7 ], [ -121.5, 46.7 ], [ -121.5, 46.9 ], [ -121.9, 46.9 ], [ -121.9, 46.7 ] ] ] } } } }``` | <span data-ttu-id="2c7ba-332">Yes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-332">Yes</span></span>

## <a name="additional-operators"></a><span data-ttu-id="2c7ba-333">Additional operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-333">Additional operators</span></span>

<span data-ttu-id="2c7ba-334">Operator</span><span class="sxs-lookup"><span data-stu-id="2c7ba-334">Operator</span></span> | <span data-ttu-id="2c7ba-335">Example</span><span class="sxs-lookup"><span data-stu-id="2c7ba-335">Example</span></span> | <span data-ttu-id="2c7ba-336">Notes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-336">Notes</span></span> 
--- | --- | --- |
<span data-ttu-id="2c7ba-337">$all</span><span class="sxs-lookup"><span data-stu-id="2c7ba-337">$all</span></span> | ```{ "Location.coordinates": { $all: [-121.758, 46.87] } }``` | 
<span data-ttu-id="2c7ba-338">$elemMatch</span><span class="sxs-lookup"><span data-stu-id="2c7ba-338">$elemMatch</span></span> | ```{ "Location.coordinates": { $elemMatch: {  $lt: 0 } } }``` |  
<span data-ttu-id="2c7ba-339">$size</span><span class="sxs-lookup"><span data-stu-id="2c7ba-339">$size</span></span> | ```{ "Location.coordinates": { $size: 2 } }``` | 
<span data-ttu-id="2c7ba-340">$comment</span><span class="sxs-lookup"><span data-stu-id="2c7ba-340">$comment</span></span> |  ```{ "Location.coordinates": { $elemMatch: {  $lt: 0 } }, $comment: "Negative values"}``` | 
<span data-ttu-id="2c7ba-341">$text</span><span class="sxs-lookup"><span data-stu-id="2c7ba-341">$text</span></span> |  | <span data-ttu-id="2c7ba-342">Not supported.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-342">Not supported.</span></span> <span data-ttu-id="2c7ba-343">Use $regex instead.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-343">Use $regex instead.</span></span>

## <a name="unsupported-operators"></a><span data-ttu-id="2c7ba-344">Unsupported operators</span><span class="sxs-lookup"><span data-stu-id="2c7ba-344">Unsupported operators</span></span>

<span data-ttu-id="2c7ba-345">The ```$where``` and the ```$eval``` operators are not supported by Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-345">The ```$where``` and the ```$eval``` operators are not supported by Azure Cosmos DB.</span></span>

### <a name="methods"></a><span data-ttu-id="2c7ba-346">Methods</span><span class="sxs-lookup"><span data-stu-id="2c7ba-346">Methods</span></span>

<span data-ttu-id="2c7ba-347">Following methods are supported:</span><span class="sxs-lookup"><span data-stu-id="2c7ba-347">Following methods are supported:</span></span>

#### <a name="cursor-methods"></a><span data-ttu-id="2c7ba-348">Cursor methods</span><span class="sxs-lookup"><span data-stu-id="2c7ba-348">Cursor methods</span></span>

<span data-ttu-id="2c7ba-349">Method</span><span class="sxs-lookup"><span data-stu-id="2c7ba-349">Method</span></span> | <span data-ttu-id="2c7ba-350">Example</span><span class="sxs-lookup"><span data-stu-id="2c7ba-350">Example</span></span> | <span data-ttu-id="2c7ba-351">Notes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-351">Notes</span></span> 
--- | --- | --- |
<span data-ttu-id="2c7ba-352">cursor.sort()</span><span class="sxs-lookup"><span data-stu-id="2c7ba-352">cursor.sort()</span></span> | ```cursor.sort({ "Elevation": -1 })``` | <span data-ttu-id="2c7ba-353">Documents without sort key do not get returned</span><span class="sxs-lookup"><span data-stu-id="2c7ba-353">Documents without sort key do not get returned</span></span>

## <a name="unique-indexes"></a><span data-ttu-id="2c7ba-354">Unique indexes</span><span class="sxs-lookup"><span data-stu-id="2c7ba-354">Unique indexes</span></span>

<span data-ttu-id="2c7ba-355">Azure Cosmos DB indexes every field in documents that are written to the database by default.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-355">Azure Cosmos DB indexes every field in documents that are written to the database by default.</span></span> <span data-ttu-id="2c7ba-356">Unique indexes ensure that a specific field doesn’t have duplicate values across all documents in a collection, similar to the way uniqueness is preserved on the default "_id" key.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-356">Unique indexes ensure that a specific field doesn’t have duplicate values across all documents in a collection, similar to the way uniqueness is preserved on the default "_id" key.</span></span> <span data-ttu-id="2c7ba-357">Now you can create custom indexes in Azure Cosmos DB by using the createIndex command, including the 'unique’ constraint.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-357">Now you can create custom indexes in Azure Cosmos DB by using the createIndex command, including the 'unique’ constraint.</span></span>

<span data-ttu-id="2c7ba-358">Unique indexes are available for all MongoDB API accounts.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-358">Unique indexes are available for all MongoDB API accounts.</span></span>

## <a name="time-to-live-ttl"></a><span data-ttu-id="2c7ba-359">Time-to-live (TTL)</span><span class="sxs-lookup"><span data-stu-id="2c7ba-359">Time-to-live (TTL)</span></span>

<span data-ttu-id="2c7ba-360">Azure Cosmos DB supports a relative time-to-live (TTL) based on the timestamp of the document.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-360">Azure Cosmos DB supports a relative time-to-live (TTL) based on the timestamp of the document.</span></span> <span data-ttu-id="2c7ba-361">TTL can be enabled for MongoDB API collections through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c7ba-361">TTL can be enabled for MongoDB API collections through the [Azure portal](https://portal.azure.com).</span></span>

## <a name="user-and-role-management"></a><span data-ttu-id="2c7ba-362">User and role management</span><span class="sxs-lookup"><span data-stu-id="2c7ba-362">User and role management</span></span>

<span data-ttu-id="2c7ba-363">Azure Cosmos DB does not yet support users and roles.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-363">Azure Cosmos DB does not yet support users and roles.</span></span> <span data-ttu-id="2c7ba-364">Azure Cosmos DB supports role based access control (RBAC) and read-write and read-only passwords/keys that can be obtained through the [Azure portal](https://portal.azure.com) (Connection String page).</span><span class="sxs-lookup"><span data-stu-id="2c7ba-364">Azure Cosmos DB supports role based access control (RBAC) and read-write and read-only passwords/keys that can be obtained through the [Azure portal](https://portal.azure.com) (Connection String page).</span></span>

## <a name="replication"></a><span data-ttu-id="2c7ba-365">Replication</span><span class="sxs-lookup"><span data-stu-id="2c7ba-365">Replication</span></span>

<span data-ttu-id="2c7ba-366">Azure Cosmos DB supports automatic, native replication at the lowest layers.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-366">Azure Cosmos DB supports automatic, native replication at the lowest layers.</span></span> <span data-ttu-id="2c7ba-367">This logic is extended out to achieve low-latency, global replication as well.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-367">This logic is extended out to achieve low-latency, global replication as well.</span></span> <span data-ttu-id="2c7ba-368">Azure Cosmos DB does not support manual replication commands.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-368">Azure Cosmos DB does not support manual replication commands.</span></span>

## <a name="write-concern"></a><span data-ttu-id="2c7ba-369">Write Concern</span><span class="sxs-lookup"><span data-stu-id="2c7ba-369">Write Concern</span></span>

<span data-ttu-id="2c7ba-370">Certain MongoDB Apis support specifying a [Write Concern](https://docs.mongodb.com/manual/reference/write-concern/) which specifies the number of responses required during a write operation.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-370">Certain MongoDB Apis support specifying a [Write Concern](https://docs.mongodb.com/manual/reference/write-concern/) which specifies the number of responses required during a write operation.</span></span> <span data-ttu-id="2c7ba-371">Due to how Cosmos DB handles replication in the background all writes are all automatically Quorum by default.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-371">Due to how Cosmos DB handles replication in the background all writes are all automatically Quorum by default.</span></span> <span data-ttu-id="2c7ba-372">Any write concern specified by client code is ignored.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-372">Any write concern specified by client code is ignored.</span></span> <span data-ttu-id="2c7ba-373">Learn more in [Using consistency levels to maximize availability and performance](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2c7ba-373">Learn more in [Using consistency levels to maximize availability and performance](consistency-levels.md).</span></span>

## <a name="sharding"></a><span data-ttu-id="2c7ba-374">Sharding</span><span class="sxs-lookup"><span data-stu-id="2c7ba-374">Sharding</span></span>

<span data-ttu-id="2c7ba-375">Azure Cosmos DB supports automatic, server-side sharding.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-375">Azure Cosmos DB supports automatic, server-side sharding.</span></span> <span data-ttu-id="2c7ba-376">Azure Cosmos DB does not support manual sharding commands.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-376">Azure Cosmos DB does not support manual sharding commands.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c7ba-377">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c7ba-377">Next steps</span></span>

- <span data-ttu-id="2c7ba-378">Learn how to [use Studio 3T](mongodb-mongochef.md) with an API for MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-378">Learn how to [use Studio 3T](mongodb-mongochef.md) with an API for MongoDB database.</span></span>
- <span data-ttu-id="2c7ba-379">Learn how to [use Robo 3T](mongodb-robomongo.md) with an API for MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="2c7ba-379">Learn how to [use Robo 3T](mongodb-robomongo.md) with an API for MongoDB database.</span></span>
- <span data-ttu-id="2c7ba-380">Explore Azure Cosmos DB with protocol support for MongoDB [samples](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2c7ba-380">Explore Azure Cosmos DB with protocol support for MongoDB [samples](mongodb-samples.md).</span></span>
