---
title: Data Science Virtual Machine data ingestion tools - Azure | Microsoft Docs
description: Data Science Virtual Machine data ingestion tools
keywords: data science tools, data science virtual machine, tools for data science, linux data science
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2017
ms.author: gokuma
ms.openlocfilehash: 7aeb0476fffb8c9e5cf2b0b5d89a2a387bd6364a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869284"
---
# <a name="data-science-virtual-machine-data-ingestion-tools"></a><span data-ttu-id="976a5-104">Data Science Virtual Machine data ingestion tools</span><span class="sxs-lookup"><span data-stu-id="976a5-104">Data Science Virtual Machine data ingestion tools</span></span>

<span data-ttu-id="976a5-105">One of the first technical steps in a data science or AI project is to identify the datasets to be used and bring them into your analytics environment.</span><span class="sxs-lookup"><span data-stu-id="976a5-105">One of the first technical steps in a data science or AI project is to identify the datasets to be used and bring them into your analytics environment.</span></span> <span data-ttu-id="976a5-106">The Data Science Virtual Machine (DSVM) provides tools and libraries to bring in data from different sources into a analytical data storage locally on the DSVM or in a data platform on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="976a5-106">The Data Science Virtual Machine (DSVM) provides tools and libraries to bring in data from different sources into a analytical data storage locally on the DSVM or in a data platform on the cloud or on-premises.</span></span> 

<span data-ttu-id="976a5-107">Here are some data movement tools we have provided on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="976a5-107">Here are some data movement tools we have provided on the DSVM.</span></span> 

## <a name="adlcopy"></a><span data-ttu-id="976a5-108">AdlCopy</span><span class="sxs-lookup"><span data-stu-id="976a5-108">AdlCopy</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-109">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-109">What is it?</span></span>   | <span data-ttu-id="976a5-110">A tool to copy data from Azure storage blobs into Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="976a5-110">A tool to copy data from Azure storage blobs into Azure Data Lake Store.</span></span> <span data-ttu-id="976a5-111">It can also copy data between two Azure Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="976a5-111">It can also copy data between two Azure Data Lake Store accounts.</span></span>      |
| <span data-ttu-id="976a5-112">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-112">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-113">Windows</span><span class="sxs-lookup"><span data-stu-id="976a5-113">Windows</span></span>      |
| <span data-ttu-id="976a5-114">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-114">Typical Uses</span></span>      | <span data-ttu-id="976a5-115">Importing multiple blobs from Azure storage into Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="976a5-115">Importing multiple blobs from Azure storage into Azure Data Lake Store.</span></span>      |
|  <span data-ttu-id="976a5-116">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-116">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-117">Open a command prompt, then type `adlcopy` to get help.</span><span class="sxs-lookup"><span data-stu-id="976a5-117">Open a command prompt, then type `adlcopy` to get help.</span></span>    |
| <span data-ttu-id="976a5-118">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-118">Links to Samples</span></span>      | [<span data-ttu-id="976a5-119">Using AdlCopy</span><span class="sxs-lookup"><span data-stu-id="976a5-119">Using AdlCopy</span></span>](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob)      |
| <span data-ttu-id="976a5-120">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-120">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-121">AzCopy, Azure Command Line</span><span class="sxs-lookup"><span data-stu-id="976a5-121">AzCopy, Azure Command Line</span></span>     |

## <a name="azure-command-line"></a><span data-ttu-id="976a5-122">Azure Command Line</span><span class="sxs-lookup"><span data-stu-id="976a5-122">Azure Command Line</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-123">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-123">What is it?</span></span>   | <span data-ttu-id="976a5-124">A management tool for Azure.</span><span class="sxs-lookup"><span data-stu-id="976a5-124">A management tool for Azure.</span></span> <span data-ttu-id="976a5-125">It also contains command verbs to move data from Azure data platforms like Azure storage blobs, Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="976a5-125">It also contains command verbs to move data from Azure data platforms like Azure storage blobs, Azure Data Lake Storage</span></span>     |
| <span data-ttu-id="976a5-126">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-126">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-127">Windows, Linux</span><span class="sxs-lookup"><span data-stu-id="976a5-127">Windows, Linux</span></span>     |
| <span data-ttu-id="976a5-128">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-128">Typical Uses</span></span>      | <span data-ttu-id="976a5-129">Importing, exporting data to and from Azure storage, Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="976a5-129">Importing, exporting data to and from Azure storage, Azure Data Lake Store</span></span>      |
|  <span data-ttu-id="976a5-130">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-130">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-131">Open a command prompt, then type `az` to get help.</span><span class="sxs-lookup"><span data-stu-id="976a5-131">Open a command prompt, then type `az` to get help.</span></span>    |
| <span data-ttu-id="976a5-132">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-132">Links to Samples</span></span>      | [<span data-ttu-id="976a5-133">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="976a5-133">Using Azure CLI</span></span>](https://docs.microsoft.com/cli/azure)     |
| <span data-ttu-id="976a5-134">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-134">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-135">AzCopy, AdlCopy</span><span class="sxs-lookup"><span data-stu-id="976a5-135">AzCopy, AdlCopy</span></span>      |


## <a name="azcopy"></a><span data-ttu-id="976a5-136">AzCopy</span><span class="sxs-lookup"><span data-stu-id="976a5-136">AzCopy</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-137">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-137">What is it?</span></span>   | <span data-ttu-id="976a5-138">A tool to copy data to and from local files, Azure storage blobs, files, and tables.</span><span class="sxs-lookup"><span data-stu-id="976a5-138">A tool to copy data to and from local files, Azure storage blobs, files, and tables.</span></span>      |
| <span data-ttu-id="976a5-139">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-139">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-140">Windows</span><span class="sxs-lookup"><span data-stu-id="976a5-140">Windows</span></span>      |
| <span data-ttu-id="976a5-141">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-141">Typical Uses</span></span>      | <span data-ttu-id="976a5-142">Copying files to blob storage, copying blobs between accounts.</span><span class="sxs-lookup"><span data-stu-id="976a5-142">Copying files to blob storage, copying blobs between accounts.</span></span>      |
|  <span data-ttu-id="976a5-143">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-143">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-144">Open a command prompt, then type `azcopy` to get help.</span><span class="sxs-lookup"><span data-stu-id="976a5-144">Open a command prompt, then type `azcopy` to get help.</span></span>    |
| <span data-ttu-id="976a5-145">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-145">Links to Samples</span></span>      | [<span data-ttu-id="976a5-146">AzCopy on Windows</span><span class="sxs-lookup"><span data-stu-id="976a5-146">AzCopy on Windows</span></span>](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy)      |
| <span data-ttu-id="976a5-147">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-147">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-148">AdlCopy</span><span class="sxs-lookup"><span data-stu-id="976a5-148">AdlCopy</span></span>     |


## <a name="azure-cosmos-db-data-migration-tool"></a><span data-ttu-id="976a5-149">Azure Cosmos DB Data Migration tool</span><span class="sxs-lookup"><span data-stu-id="976a5-149">Azure Cosmos DB Data Migration tool</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-150">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-150">What is it?</span></span>   | <span data-ttu-id="976a5-151">Tool to import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB, and Azure Cosmos DB SQL API collections into Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="976a5-151">Tool to import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB, and Azure Cosmos DB SQL API collections into Azure Cosmos DB.</span></span>      |
| <span data-ttu-id="976a5-152">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-152">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-153">Windows</span><span class="sxs-lookup"><span data-stu-id="976a5-153">Windows</span></span>      |
| <span data-ttu-id="976a5-154">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-154">Typical Uses</span></span>      | <span data-ttu-id="976a5-155">Importing files from a VM to CosmosDB, importing data from Azure table storage to CosmosDB, or importing data from a SQL Server database to CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="976a5-155">Importing files from a VM to CosmosDB, importing data from Azure table storage to CosmosDB, or importing data from a SQL Server database to CosmosDB.</span></span>     |
|  <span data-ttu-id="976a5-156">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-156">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-157">To use the command line version, Open a command prompt, then type `dt`.</span><span class="sxs-lookup"><span data-stu-id="976a5-157">To use the command line version, Open a command prompt, then type `dt`.</span></span> <span data-ttu-id="976a5-158">To use the GUI tool, open a command prompt, then type `dtui`.</span><span class="sxs-lookup"><span data-stu-id="976a5-158">To use the GUI tool, open a command prompt, then type `dtui`.</span></span>    |
| <span data-ttu-id="976a5-159">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-159">Links to Samples</span></span>      | [<span data-ttu-id="976a5-160">CosmosDB Import Data</span><span class="sxs-lookup"><span data-stu-id="976a5-160">CosmosDB Import Data</span></span>](https://docs.microsoft.com/azure/cosmos-db/import-data)      |
| <span data-ttu-id="976a5-161">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-161">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-162">AzCopy, AdlCopy</span><span class="sxs-lookup"><span data-stu-id="976a5-162">AzCopy, AdlCopy</span></span>      |


## <a name="bcp"></a><span data-ttu-id="976a5-163">bcp</span><span class="sxs-lookup"><span data-stu-id="976a5-163">bcp</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-164">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-164">What is it?</span></span>   | <span data-ttu-id="976a5-165">SQL Server tool to copy data between SQL Server and a data file.</span><span class="sxs-lookup"><span data-stu-id="976a5-165">SQL Server tool to copy data between SQL Server and a data file.</span></span>      |
| <span data-ttu-id="976a5-166">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-166">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-167">Windows</span><span class="sxs-lookup"><span data-stu-id="976a5-167">Windows</span></span>      |
| <span data-ttu-id="976a5-168">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-168">Typical Uses</span></span>      | <span data-ttu-id="976a5-169">Importing a CSV file into a SQL Server table, exporting a SQL Server table to a file.</span><span class="sxs-lookup"><span data-stu-id="976a5-169">Importing a CSV file into a SQL Server table, exporting a SQL Server table to a file.</span></span>      |
|  <span data-ttu-id="976a5-170">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-170">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-171">Open a command prompt, then type `bcp` to get help.</span><span class="sxs-lookup"><span data-stu-id="976a5-171">Open a command prompt, then type `bcp` to get help.</span></span>    |
| <span data-ttu-id="976a5-172">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-172">Links to Samples</span></span>      | [<span data-ttu-id="976a5-173">Bulk Copy Utility</span><span class="sxs-lookup"><span data-stu-id="976a5-173">Bulk Copy Utility</span></span>](https://docs.microsoft.com/sql/tools/bcp-utility)      |
| <span data-ttu-id="976a5-174">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-174">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-175">SQL Server, sqlcmd</span><span class="sxs-lookup"><span data-stu-id="976a5-175">SQL Server, sqlcmd</span></span>      |

## <a name="blobfuse"></a><span data-ttu-id="976a5-176">blobfuse</span><span class="sxs-lookup"><span data-stu-id="976a5-176">blobfuse</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-177">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-177">What is it?</span></span>   | <span data-ttu-id="976a5-178">A tool to mount an Azure blob container in the Linux file system.</span><span class="sxs-lookup"><span data-stu-id="976a5-178">A tool to mount an Azure blob container in the Linux file system.</span></span>      |
| <span data-ttu-id="976a5-179">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-179">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-180">Linux</span><span class="sxs-lookup"><span data-stu-id="976a5-180">Linux</span></span>      |
| <span data-ttu-id="976a5-181">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-181">Typical Uses</span></span>      | <span data-ttu-id="976a5-182">Reading and writing to blobs in a container</span><span class="sxs-lookup"><span data-stu-id="976a5-182">Reading and writing to blobs in a container</span></span>      |
|  <span data-ttu-id="976a5-183">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-183">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-184">Run _blobfuse_ at a terminal.</span><span class="sxs-lookup"><span data-stu-id="976a5-184">Run _blobfuse_ at a terminal.</span></span>    |
| <span data-ttu-id="976a5-185">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-185">Links to Samples</span></span>      | [<span data-ttu-id="976a5-186">blobfuse on GitHub</span><span class="sxs-lookup"><span data-stu-id="976a5-186">blobfuse on GitHub</span></span>](https://github.com/Azure/azure-storage-fuse)      |
| <span data-ttu-id="976a5-187">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-187">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-188">Azure Command Line</span><span class="sxs-lookup"><span data-stu-id="976a5-188">Azure Command Line</span></span>      |


## <a name="microsoft-data-management-gateway"></a><span data-ttu-id="976a5-189">Microsoft Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="976a5-189">Microsoft Data Management Gateway</span></span>

|    |           |
| ------------- | ------------- |
| <span data-ttu-id="976a5-190">What is it?</span><span class="sxs-lookup"><span data-stu-id="976a5-190">What is it?</span></span>   | <span data-ttu-id="976a5-191">A tool to connect on-premises data sources to cloud services for consumption.</span><span class="sxs-lookup"><span data-stu-id="976a5-191">A tool to connect on-premises data sources to cloud services for consumption.</span></span>      |
| <span data-ttu-id="976a5-192">Supported DSVM Versions</span><span class="sxs-lookup"><span data-stu-id="976a5-192">Supported DSVM Versions</span></span>      | <span data-ttu-id="976a5-193">Windows</span><span class="sxs-lookup"><span data-stu-id="976a5-193">Windows</span></span>      |
| <span data-ttu-id="976a5-194">Typical Uses</span><span class="sxs-lookup"><span data-stu-id="976a5-194">Typical Uses</span></span>      | <span data-ttu-id="976a5-195">Connecting a VM to an on-premises data source.</span><span class="sxs-lookup"><span data-stu-id="976a5-195">Connecting a VM to an on-premises data source.</span></span>      |
|  <span data-ttu-id="976a5-196">How to use / run it?</span><span class="sxs-lookup"><span data-stu-id="976a5-196">How to use / run it?</span></span>    |   <span data-ttu-id="976a5-197">Start "Microsoft Data Management Gateway" from the Start Menu.</span><span class="sxs-lookup"><span data-stu-id="976a5-197">Start "Microsoft Data Management Gateway" from the Start Menu.</span></span>    |
| <span data-ttu-id="976a5-198">Links to Samples</span><span class="sxs-lookup"><span data-stu-id="976a5-198">Links to Samples</span></span>      | [<span data-ttu-id="976a5-199">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="976a5-199">Data Management Gateway</span></span>](https://msdn.microsoft.com/library/dn879362.aspx)      |
| <span data-ttu-id="976a5-200">Related Tools on the DSVM</span><span class="sxs-lookup"><span data-stu-id="976a5-200">Related Tools on the DSVM</span></span>      | <span data-ttu-id="976a5-201">AzCopy, AdlCopy, bcp</span><span class="sxs-lookup"><span data-stu-id="976a5-201">AzCopy, AdlCopy, bcp</span></span>    |
