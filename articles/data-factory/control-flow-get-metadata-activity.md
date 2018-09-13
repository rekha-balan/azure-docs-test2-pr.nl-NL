---
title: Get metadata activity in Azure Data Factory | Microsoft Docs
description: Learn how you can use the SQL Server Stored Procedure Activity to invoke a stored procedure in an Azure SQL Database or Azure SQL Data Warehouse from a Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: shlo
ms.openlocfilehash: c24bec7366ea62b3dd8f7a301c9d2d62c6dd6c7d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856879"
---
# <a name="get-metadata-activity-in-azure-data-factory"></a><span data-ttu-id="db855-103">Get metadata activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="db855-103">Get metadata activity in Azure Data Factory</span></span>
<span data-ttu-id="db855-104">GetMetadata activity can be used to retrieve **metadata** of any data in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="db855-104">GetMetadata activity can be used to retrieve **metadata** of any data in Azure Data Factory.</span></span> <span data-ttu-id="db855-105">This activity can be used in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="db855-105">This activity can be used in the following scenarios:</span></span>

- <span data-ttu-id="db855-106">Validate the metadata information of any data</span><span class="sxs-lookup"><span data-stu-id="db855-106">Validate the metadata information of any data</span></span>
- <span data-ttu-id="db855-107">Trigger a pipeline when data is ready/ available</span><span class="sxs-lookup"><span data-stu-id="db855-107">Trigger a pipeline when data is ready/ available</span></span>

<span data-ttu-id="db855-108">The following functionality is available in the control flow:</span><span class="sxs-lookup"><span data-stu-id="db855-108">The following functionality is available in the control flow:</span></span>

- <span data-ttu-id="db855-109">The output from GetMetadata Activity can be used in conditional expressions to perform validation.</span><span class="sxs-lookup"><span data-stu-id="db855-109">The output from GetMetadata Activity can be used in conditional expressions to perform validation.</span></span>
- <span data-ttu-id="db855-110">A pipeline can be triggered when condition is satisfied via Do-Until looping</span><span class="sxs-lookup"><span data-stu-id="db855-110">A pipeline can be triggered when condition is satisfied via Do-Until looping</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="db855-111">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="db855-111">Supported capabilities</span></span>

<span data-ttu-id="db855-112">The GetMetadata Activity takes a dataset as a required input, and outputs metadata information available as activity output.</span><span class="sxs-lookup"><span data-stu-id="db855-112">The GetMetadata Activity takes a dataset as a required input, and outputs metadata information available as activity output.</span></span> <span data-ttu-id="db855-113">Currently, the following connectors with corresponding retrievable meatadata are supported, and the maximum supported metadata size is up to **1MB**.</span><span class="sxs-lookup"><span data-stu-id="db855-113">Currently, the following connectors with corresponding retrievable meatadata are supported, and the maximum supported metadata size is up to **1MB**.</span></span>

>[!NOTE]
><span data-ttu-id="db855-114">If you run GetMetadata activity on a Self-hosted Integration Runtime, the latest capability is supported on version 3.6 or above.</span><span class="sxs-lookup"><span data-stu-id="db855-114">If you run GetMetadata activity on a Self-hosted Integration Runtime, the latest capability is supported on version 3.6 or above.</span></span> 

### <a name="supported-connectors"></a><span data-ttu-id="db855-115">Supported connectors</span><span class="sxs-lookup"><span data-stu-id="db855-115">Supported connectors</span></span>

<span data-ttu-id="db855-116">**File storage:**</span><span class="sxs-lookup"><span data-stu-id="db855-116">**File storage:**</span></span>

| <span data-ttu-id="db855-117">Connector/Metadata</span><span class="sxs-lookup"><span data-stu-id="db855-117">Connector/Metadata</span></span> | <span data-ttu-id="db855-118">itemName</span><span class="sxs-lookup"><span data-stu-id="db855-118">itemName</span></span><br><span data-ttu-id="db855-119">(file/folder)</span><span class="sxs-lookup"><span data-stu-id="db855-119">(file/folder)</span></span> | <span data-ttu-id="db855-120">itemType</span><span class="sxs-lookup"><span data-stu-id="db855-120">itemType</span></span><br><span data-ttu-id="db855-121">(file/folder)</span><span class="sxs-lookup"><span data-stu-id="db855-121">(file/folder)</span></span> | <span data-ttu-id="db855-122">size</span><span class="sxs-lookup"><span data-stu-id="db855-122">size</span></span><br><span data-ttu-id="db855-123">(file)</span><span class="sxs-lookup"><span data-stu-id="db855-123">(file)</span></span> | <span data-ttu-id="db855-124">created</span><span class="sxs-lookup"><span data-stu-id="db855-124">created</span></span><br><span data-ttu-id="db855-125">(file/folder)</span><span class="sxs-lookup"><span data-stu-id="db855-125">(file/folder)</span></span> | <span data-ttu-id="db855-126">lastModified</span><span class="sxs-lookup"><span data-stu-id="db855-126">lastModified</span></span><br><span data-ttu-id="db855-127">(file/folder)</span><span class="sxs-lookup"><span data-stu-id="db855-127">(file/folder)</span></span> |<span data-ttu-id="db855-128">childItems</span><span class="sxs-lookup"><span data-stu-id="db855-128">childItems</span></span><br><span data-ttu-id="db855-129">(folder)</span><span class="sxs-lookup"><span data-stu-id="db855-129">(folder)</span></span> |<span data-ttu-id="db855-130">contentMD5</span><span class="sxs-lookup"><span data-stu-id="db855-130">contentMD5</span></span><br><span data-ttu-id="db855-131">(file)</span><span class="sxs-lookup"><span data-stu-id="db855-131">(file)</span></span> | <span data-ttu-id="db855-132">structure</span><span class="sxs-lookup"><span data-stu-id="db855-132">structure</span></span><br/><span data-ttu-id="db855-133">(file)</span><span class="sxs-lookup"><span data-stu-id="db855-133">(file)</span></span> | <span data-ttu-id="db855-134">columnCount</span><span class="sxs-lookup"><span data-stu-id="db855-134">columnCount</span></span><br><span data-ttu-id="db855-135">(file)</span><span class="sxs-lookup"><span data-stu-id="db855-135">(file)</span></span> | <span data-ttu-id="db855-136">exists</span><span class="sxs-lookup"><span data-stu-id="db855-136">exists</span></span><br><span data-ttu-id="db855-137">(file/folder)</span><span class="sxs-lookup"><span data-stu-id="db855-137">(file/folder)</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="db855-138">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="db855-138">Amazon S3</span></span> | <span data-ttu-id="db855-139">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-139">√/√</span></span> | <span data-ttu-id="db855-140">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-140">√/√</span></span> | <span data-ttu-id="db855-141">√</span><span class="sxs-lookup"><span data-stu-id="db855-141">√</span></span> | <span data-ttu-id="db855-142">x/x</span><span class="sxs-lookup"><span data-stu-id="db855-142">x/x</span></span> | <span data-ttu-id="db855-143">√/√\*</span><span class="sxs-lookup"><span data-stu-id="db855-143">√/√\*</span></span> | <span data-ttu-id="db855-144">√</span><span class="sxs-lookup"><span data-stu-id="db855-144">√</span></span> | <span data-ttu-id="db855-145">x</span><span class="sxs-lookup"><span data-stu-id="db855-145">x</span></span> | <span data-ttu-id="db855-146">√</span><span class="sxs-lookup"><span data-stu-id="db855-146">√</span></span> | <span data-ttu-id="db855-147">√</span><span class="sxs-lookup"><span data-stu-id="db855-147">√</span></span> | <span data-ttu-id="db855-148">√/√\*</span><span class="sxs-lookup"><span data-stu-id="db855-148">√/√\*</span></span> |
| <span data-ttu-id="db855-149">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="db855-149">Azure Blob</span></span> | <span data-ttu-id="db855-150">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-150">√/√</span></span> | <span data-ttu-id="db855-151">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-151">√/√</span></span> | <span data-ttu-id="db855-152">√</span><span class="sxs-lookup"><span data-stu-id="db855-152">√</span></span> | <span data-ttu-id="db855-153">x/x</span><span class="sxs-lookup"><span data-stu-id="db855-153">x/x</span></span> | <span data-ttu-id="db855-154">√/√\*</span><span class="sxs-lookup"><span data-stu-id="db855-154">√/√\*</span></span> | <span data-ttu-id="db855-155">√</span><span class="sxs-lookup"><span data-stu-id="db855-155">√</span></span> | <span data-ttu-id="db855-156">√</span><span class="sxs-lookup"><span data-stu-id="db855-156">√</span></span> | <span data-ttu-id="db855-157">√</span><span class="sxs-lookup"><span data-stu-id="db855-157">√</span></span> | <span data-ttu-id="db855-158">√</span><span class="sxs-lookup"><span data-stu-id="db855-158">√</span></span> | <span data-ttu-id="db855-159">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-159">√/√</span></span> |
| <span data-ttu-id="db855-160">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="db855-160">Azure Data Lake Store</span></span> | <span data-ttu-id="db855-161">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-161">√/√</span></span> | <span data-ttu-id="db855-162">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-162">√/√</span></span> | <span data-ttu-id="db855-163">√</span><span class="sxs-lookup"><span data-stu-id="db855-163">√</span></span> | <span data-ttu-id="db855-164">x/x</span><span class="sxs-lookup"><span data-stu-id="db855-164">x/x</span></span> | <span data-ttu-id="db855-165">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-165">√/√</span></span> | <span data-ttu-id="db855-166">√</span><span class="sxs-lookup"><span data-stu-id="db855-166">√</span></span> | <span data-ttu-id="db855-167">x</span><span class="sxs-lookup"><span data-stu-id="db855-167">x</span></span> | <span data-ttu-id="db855-168">√</span><span class="sxs-lookup"><span data-stu-id="db855-168">√</span></span> | <span data-ttu-id="db855-169">√</span><span class="sxs-lookup"><span data-stu-id="db855-169">√</span></span> | <span data-ttu-id="db855-170">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-170">√/√</span></span> |
| <span data-ttu-id="db855-171">Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="db855-171">Azure File Storage</span></span> | <span data-ttu-id="db855-172">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-172">√/√</span></span> | <span data-ttu-id="db855-173">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-173">√/√</span></span> | <span data-ttu-id="db855-174">√</span><span class="sxs-lookup"><span data-stu-id="db855-174">√</span></span> | <span data-ttu-id="db855-175">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-175">√/√</span></span> | <span data-ttu-id="db855-176">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-176">√/√</span></span> | <span data-ttu-id="db855-177">√</span><span class="sxs-lookup"><span data-stu-id="db855-177">√</span></span> | <span data-ttu-id="db855-178">x</span><span class="sxs-lookup"><span data-stu-id="db855-178">x</span></span> | <span data-ttu-id="db855-179">√</span><span class="sxs-lookup"><span data-stu-id="db855-179">√</span></span> | <span data-ttu-id="db855-180">√</span><span class="sxs-lookup"><span data-stu-id="db855-180">√</span></span> | <span data-ttu-id="db855-181">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-181">√/√</span></span> |
| <span data-ttu-id="db855-182">File System</span><span class="sxs-lookup"><span data-stu-id="db855-182">File System</span></span> | <span data-ttu-id="db855-183">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-183">√/√</span></span> | <span data-ttu-id="db855-184">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-184">√/√</span></span> | <span data-ttu-id="db855-185">√</span><span class="sxs-lookup"><span data-stu-id="db855-185">√</span></span> | <span data-ttu-id="db855-186">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-186">√/√</span></span> | <span data-ttu-id="db855-187">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-187">√/√</span></span> | <span data-ttu-id="db855-188">√</span><span class="sxs-lookup"><span data-stu-id="db855-188">√</span></span> | <span data-ttu-id="db855-189">x</span><span class="sxs-lookup"><span data-stu-id="db855-189">x</span></span> | <span data-ttu-id="db855-190">√</span><span class="sxs-lookup"><span data-stu-id="db855-190">√</span></span> | <span data-ttu-id="db855-191">√</span><span class="sxs-lookup"><span data-stu-id="db855-191">√</span></span> | <span data-ttu-id="db855-192">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-192">√/√</span></span> |
| <span data-ttu-id="db855-193">SFTP</span><span class="sxs-lookup"><span data-stu-id="db855-193">SFTP</span></span> | <span data-ttu-id="db855-194">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-194">√/√</span></span> | <span data-ttu-id="db855-195">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-195">√/√</span></span> | <span data-ttu-id="db855-196">√</span><span class="sxs-lookup"><span data-stu-id="db855-196">√</span></span> | <span data-ttu-id="db855-197">x/x</span><span class="sxs-lookup"><span data-stu-id="db855-197">x/x</span></span> | <span data-ttu-id="db855-198">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-198">√/√</span></span> | <span data-ttu-id="db855-199">√</span><span class="sxs-lookup"><span data-stu-id="db855-199">√</span></span> | <span data-ttu-id="db855-200">x</span><span class="sxs-lookup"><span data-stu-id="db855-200">x</span></span> | <span data-ttu-id="db855-201">√</span><span class="sxs-lookup"><span data-stu-id="db855-201">√</span></span> | <span data-ttu-id="db855-202">√</span><span class="sxs-lookup"><span data-stu-id="db855-202">√</span></span> | <span data-ttu-id="db855-203">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-203">√/√</span></span> |
| <span data-ttu-id="db855-204">FTP</span><span class="sxs-lookup"><span data-stu-id="db855-204">FTP</span></span> | <span data-ttu-id="db855-205">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-205">√/√</span></span> | <span data-ttu-id="db855-206">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-206">√/√</span></span> | <span data-ttu-id="db855-207">√</span><span class="sxs-lookup"><span data-stu-id="db855-207">√</span></span> | <span data-ttu-id="db855-208">x/x</span><span class="sxs-lookup"><span data-stu-id="db855-208">x/x</span></span> | <span data-ttu-id="db855-209">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-209">√/√</span></span> | <span data-ttu-id="db855-210">√</span><span class="sxs-lookup"><span data-stu-id="db855-210">√</span></span> | <span data-ttu-id="db855-211">x</span><span class="sxs-lookup"><span data-stu-id="db855-211">x</span></span> | <span data-ttu-id="db855-212">√</span><span class="sxs-lookup"><span data-stu-id="db855-212">√</span></span> | <span data-ttu-id="db855-213">√</span><span class="sxs-lookup"><span data-stu-id="db855-213">√</span></span> | <span data-ttu-id="db855-214">√/√</span><span class="sxs-lookup"><span data-stu-id="db855-214">√/√</span></span> |

- <span data-ttu-id="db855-215">For Amazon S3, the `lastModified` applies to bucket and key but not virtual folder; ; and the `exists` applies to bucket and key but not prefix or virtual folder.</span><span class="sxs-lookup"><span data-stu-id="db855-215">For Amazon S3, the `lastModified` applies to bucket and key but not virtual folder; ; and the `exists` applies to bucket and key but not prefix or virtual folder.</span></span>
- <span data-ttu-id="db855-216">For Azure Blob, the `lastModified` applies to container and blob but not virtual folder.</span><span class="sxs-lookup"><span data-stu-id="db855-216">For Azure Blob, the `lastModified` applies to container and blob but not virtual folder.</span></span>

<span data-ttu-id="db855-217">**Relational database:**</span><span class="sxs-lookup"><span data-stu-id="db855-217">**Relational database:**</span></span>

| <span data-ttu-id="db855-218">Connector/Metadata</span><span class="sxs-lookup"><span data-stu-id="db855-218">Connector/Metadata</span></span> | <span data-ttu-id="db855-219">structure</span><span class="sxs-lookup"><span data-stu-id="db855-219">structure</span></span> | <span data-ttu-id="db855-220">columnCount</span><span class="sxs-lookup"><span data-stu-id="db855-220">columnCount</span></span> | <span data-ttu-id="db855-221">exists</span><span class="sxs-lookup"><span data-stu-id="db855-221">exists</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="db855-222">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="db855-222">Azure SQL Database</span></span> | <span data-ttu-id="db855-223">√</span><span class="sxs-lookup"><span data-stu-id="db855-223">√</span></span> | <span data-ttu-id="db855-224">√</span><span class="sxs-lookup"><span data-stu-id="db855-224">√</span></span> | <span data-ttu-id="db855-225">√</span><span class="sxs-lookup"><span data-stu-id="db855-225">√</span></span> |
| <span data-ttu-id="db855-226">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="db855-226">Azure SQL Data Warehouse</span></span> | <span data-ttu-id="db855-227">√</span><span class="sxs-lookup"><span data-stu-id="db855-227">√</span></span> | <span data-ttu-id="db855-228">√</span><span class="sxs-lookup"><span data-stu-id="db855-228">√</span></span> | <span data-ttu-id="db855-229">√</span><span class="sxs-lookup"><span data-stu-id="db855-229">√</span></span> |
| <span data-ttu-id="db855-230">SQL Server</span><span class="sxs-lookup"><span data-stu-id="db855-230">SQL Server</span></span> | <span data-ttu-id="db855-231">√</span><span class="sxs-lookup"><span data-stu-id="db855-231">√</span></span> | <span data-ttu-id="db855-232">√</span><span class="sxs-lookup"><span data-stu-id="db855-232">√</span></span> | <span data-ttu-id="db855-233">√</span><span class="sxs-lookup"><span data-stu-id="db855-233">√</span></span> |

### <a name="metadata-options"></a><span data-ttu-id="db855-234">Metadata options</span><span class="sxs-lookup"><span data-stu-id="db855-234">Metadata options</span></span>

<span data-ttu-id="db855-235">The following metadata types can be specified in the GetMetadata activity field list to retrieve:</span><span class="sxs-lookup"><span data-stu-id="db855-235">The following metadata types can be specified in the GetMetadata activity field list to retrieve:</span></span>

| <span data-ttu-id="db855-236">Metadata type</span><span class="sxs-lookup"><span data-stu-id="db855-236">Metadata type</span></span> | <span data-ttu-id="db855-237">Description</span><span class="sxs-lookup"><span data-stu-id="db855-237">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="db855-238">itemName</span><span class="sxs-lookup"><span data-stu-id="db855-238">itemName</span></span> | <span data-ttu-id="db855-239">Name of the file or folder.</span><span class="sxs-lookup"><span data-stu-id="db855-239">Name of the file or folder.</span></span> |
| <span data-ttu-id="db855-240">itemType</span><span class="sxs-lookup"><span data-stu-id="db855-240">itemType</span></span> | <span data-ttu-id="db855-241">Type of the file or folder.</span><span class="sxs-lookup"><span data-stu-id="db855-241">Type of the file or folder.</span></span> <span data-ttu-id="db855-242">Output value is `File` or `Folder`.</span><span class="sxs-lookup"><span data-stu-id="db855-242">Output value is `File` or `Folder`.</span></span> |
| <span data-ttu-id="db855-243">size</span><span class="sxs-lookup"><span data-stu-id="db855-243">size</span></span> | <span data-ttu-id="db855-244">Size of the file in byte.</span><span class="sxs-lookup"><span data-stu-id="db855-244">Size of the file in byte.</span></span> <span data-ttu-id="db855-245">Applicable to file only.</span><span class="sxs-lookup"><span data-stu-id="db855-245">Applicable to file only.</span></span> |
| <span data-ttu-id="db855-246">created</span><span class="sxs-lookup"><span data-stu-id="db855-246">created</span></span> | <span data-ttu-id="db855-247">Created datetime of the file or folder.</span><span class="sxs-lookup"><span data-stu-id="db855-247">Created datetime of the file or folder.</span></span> |
| <span data-ttu-id="db855-248">lastModified</span><span class="sxs-lookup"><span data-stu-id="db855-248">lastModified</span></span> | <span data-ttu-id="db855-249">Last modified datetime of the file or folder.</span><span class="sxs-lookup"><span data-stu-id="db855-249">Last modified datetime of the file or folder.</span></span> |
| <span data-ttu-id="db855-250">childItems</span><span class="sxs-lookup"><span data-stu-id="db855-250">childItems</span></span> | <span data-ttu-id="db855-251">List of sub-folders and files inside the given folder.</span><span class="sxs-lookup"><span data-stu-id="db855-251">List of sub-folders and files inside the given folder.</span></span> <span data-ttu-id="db855-252">Applicable to folder only.</span><span class="sxs-lookup"><span data-stu-id="db855-252">Applicable to folder only.</span></span> <span data-ttu-id="db855-253">Output value is a list of name and type of each child item.</span><span class="sxs-lookup"><span data-stu-id="db855-253">Output value is a list of name and type of each child item.</span></span> |
| <span data-ttu-id="db855-254">contentMD5</span><span class="sxs-lookup"><span data-stu-id="db855-254">contentMD5</span></span> | <span data-ttu-id="db855-255">MD5 of the file.</span><span class="sxs-lookup"><span data-stu-id="db855-255">MD5 of the file.</span></span> <span data-ttu-id="db855-256">Applicable to file only.</span><span class="sxs-lookup"><span data-stu-id="db855-256">Applicable to file only.</span></span> |
| <span data-ttu-id="db855-257">structure</span><span class="sxs-lookup"><span data-stu-id="db855-257">structure</span></span> | <span data-ttu-id="db855-258">Data structure inside the file or relational database table.</span><span class="sxs-lookup"><span data-stu-id="db855-258">Data structure inside the file or relational database table.</span></span> <span data-ttu-id="db855-259">Output value is a list of column name and column type.</span><span class="sxs-lookup"><span data-stu-id="db855-259">Output value is a list of column name and column type.</span></span> |
| <span data-ttu-id="db855-260">columnCount</span><span class="sxs-lookup"><span data-stu-id="db855-260">columnCount</span></span> | <span data-ttu-id="db855-261">Number of columns inside the file or relational table.</span><span class="sxs-lookup"><span data-stu-id="db855-261">Number of columns inside the file or relational table.</span></span> |
| <span data-ttu-id="db855-262">exists</span><span class="sxs-lookup"><span data-stu-id="db855-262">exists</span></span>| <span data-ttu-id="db855-263">Whether a file/folder/table exists or not.</span><span class="sxs-lookup"><span data-stu-id="db855-263">Whether a file/folder/table exists or not.</span></span> <span data-ttu-id="db855-264">Note if "exists" is specified in the GetaMetadata field list, the activity won't fail even when the item (file/folder/table) doesn't exists; instead, it returns `exists: false` in the output.</span><span class="sxs-lookup"><span data-stu-id="db855-264">Note if "exists" is specified in the GetaMetadata field list, the activity won't fail even when the item (file/folder/table) doesn't exists; instead, it returns `exists: false` in the output.</span></span> |

>[!TIP]
><span data-ttu-id="db855-265">When you want to validate if a file/folder/table exists or not, specify `exists` in the GetMetadata activity field list, then you can check the `exists: true/false` result from the activity output.</span><span class="sxs-lookup"><span data-stu-id="db855-265">When you want to validate if a file/folder/table exists or not, specify `exists` in the GetMetadata activity field list, then you can check the `exists: true/false` result from the activity output.</span></span> <span data-ttu-id="db855-266">If `exists` is not configured in the field list, the GetMetadata activity will fail when the object is not found.</span><span class="sxs-lookup"><span data-stu-id="db855-266">If `exists` is not configured in the field list, the GetMetadata activity will fail when the object is not found.</span></span>

## <a name="syntax"></a><span data-ttu-id="db855-267">Syntax</span><span class="sxs-lookup"><span data-stu-id="db855-267">Syntax</span></span>

<span data-ttu-id="db855-268">**GetMetadata activity:**</span><span class="sxs-lookup"><span data-stu-id="db855-268">**GetMetadata activity:**</span></span>

```json
{
    "name": "MyActivity",
    "type": "GetMetadata",
    "typeProperties": {
        "fieldList" : ["size", "lastModified", "structure"],
        "dataset": {
            "referenceName": "MyDataset",
            "type": "DatasetReference"
        }
    }
}
```

<span data-ttu-id="db855-269">**Dataset:**</span><span class="sxs-lookup"><span data-stu-id="db855-269">**Dataset:**</span></span>

```json
{
    "name": "MyDataset",
    "properties": {
    "type": "AzureBlob",
        "linkedService": {
            "referenceName": "StorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath":"container/folder",
            "filename": "file.json",
            "format":{
                "type":"JsonFormat"
            }
        }
    }
}
```

## <a name="type-properties"></a><span data-ttu-id="db855-270">Type properties</span><span class="sxs-lookup"><span data-stu-id="db855-270">Type properties</span></span>

<span data-ttu-id="db855-271">Currently GetMetadata activity can fetch the following types of metadata information.</span><span class="sxs-lookup"><span data-stu-id="db855-271">Currently GetMetadata activity can fetch the following types of metadata information.</span></span>

<span data-ttu-id="db855-272">Property</span><span class="sxs-lookup"><span data-stu-id="db855-272">Property</span></span> | <span data-ttu-id="db855-273">Description</span><span class="sxs-lookup"><span data-stu-id="db855-273">Description</span></span> | <span data-ttu-id="db855-274">Required</span><span class="sxs-lookup"><span data-stu-id="db855-274">Required</span></span>
-------- | ----------- | --------
<span data-ttu-id="db855-275">fieldList</span><span class="sxs-lookup"><span data-stu-id="db855-275">fieldList</span></span> | <span data-ttu-id="db855-276">Lists the types of metadata information required.</span><span class="sxs-lookup"><span data-stu-id="db855-276">Lists the types of metadata information required.</span></span> <span data-ttu-id="db855-277">See details in [Metadata options](#metadata-options) section on supported metadata.</span><span class="sxs-lookup"><span data-stu-id="db855-277">See details in [Metadata options](#metadata-options) section on supported metadata.</span></span> | <span data-ttu-id="db855-278">Yes</span><span class="sxs-lookup"><span data-stu-id="db855-278">Yes</span></span> 
<span data-ttu-id="db855-279">dataset</span><span class="sxs-lookup"><span data-stu-id="db855-279">dataset</span></span> | <span data-ttu-id="db855-280">The reference dataset whose metadata activity is to be retrieved by the GetMetadata Activity.</span><span class="sxs-lookup"><span data-stu-id="db855-280">The reference dataset whose metadata activity is to be retrieved by the GetMetadata Activity.</span></span> <span data-ttu-id="db855-281">See [Supported capabilities](#supported-capabilities) section on supported connectors, and refer to connector topic on dataset syntax details.</span><span class="sxs-lookup"><span data-stu-id="db855-281">See [Supported capabilities](#supported-capabilities) section on supported connectors, and refer to connector topic on dataset syntax details.</span></span> | <span data-ttu-id="db855-282">Yes</span><span class="sxs-lookup"><span data-stu-id="db855-282">Yes</span></span>

## <a name="sample-output"></a><span data-ttu-id="db855-283">Sample output</span><span class="sxs-lookup"><span data-stu-id="db855-283">Sample output</span></span>

<span data-ttu-id="db855-284">The GetMetadata result is shown in activity output.</span><span class="sxs-lookup"><span data-stu-id="db855-284">The GetMetadata result is shown in activity output.</span></span> <span data-ttu-id="db855-285">Below are two samples with exhaustive metadata options selected in field list as reference.</span><span class="sxs-lookup"><span data-stu-id="db855-285">Below are two samples with exhaustive metadata options selected in field list as reference.</span></span> <span data-ttu-id="db855-286">To use the result in subsequent activity, use the pattern of `@{activity('MyGetMetadataActivity').output.itemName}`.</span><span class="sxs-lookup"><span data-stu-id="db855-286">To use the result in subsequent activity, use the pattern of `@{activity('MyGetMetadataActivity').output.itemName}`.</span></span>

### <a name="get-a-files-metadata"></a><span data-ttu-id="db855-287">Get a file's metadata</span><span class="sxs-lookup"><span data-stu-id="db855-287">Get a file's metadata</span></span>

```json
{
  "exists": true,
  "itemName": "test.csv",
  "itemType": "File",
  "size": 104857600,
  "lastModified": "2017-02-23T06:17:09Z",
  "created": "2017-02-23T06:17:09Z",
  "contentMD5": "cMauY+Kz5zDm3eWa9VpoyQ==",
  "structure": [
    {
        "name": "id",
        "type": "Int64"
    },
    {
        "name": "name",
        "type": "String"
    }
  ],
  "columnCount": 2
}
```

### <a name="get-a-folders-metadata"></a><span data-ttu-id="db855-288">Get a folder's metadata</span><span class="sxs-lookup"><span data-stu-id="db855-288">Get a folder's metadata</span></span>

```json
{
  "exists": true,
  "itemName": "testFolder",
  "itemType": "Folder",
  "lastModified": "2017-02-23T06:17:09Z",
  "created": "2017-02-23T06:17:09Z",
  "childItems": [
    {
      "name": "test.avro",
      "type": "File"
    },
    {
      "name": "folder hello",
      "type": "Folder"
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="db855-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="db855-289">Next steps</span></span>
<span data-ttu-id="db855-290">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="db855-290">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="db855-291">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="db855-291">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="db855-292">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="db855-292">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="db855-293">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="db855-293">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="db855-294">Web Activity</span><span class="sxs-lookup"><span data-stu-id="db855-294">Web Activity</span></span>](control-flow-web-activity.md)
