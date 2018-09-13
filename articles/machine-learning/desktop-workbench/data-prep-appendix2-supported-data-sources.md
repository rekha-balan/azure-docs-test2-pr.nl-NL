---
title: Supported data sources available with Azure Machine Learning data preparation  | Microsoft Docs
description: This document provides a complete list of supported data sources available for Azure Machine Learning data preparation.
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 88ed4fa43e5724cfe1d6f1555db947d77045cd2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865724"
---
# <a name="supported-data-sources-for-azure-machine-learning-data-preparation"></a><span data-ttu-id="cfe7d-103">Supported data sources for Azure Machine Learning data preparation</span><span class="sxs-lookup"><span data-stu-id="cfe7d-103">Supported data sources for Azure Machine Learning data preparation</span></span> 
<span data-ttu-id="cfe7d-104">This article outlines the currently supported data sources for Azure Machine Learning data preparation.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-104">This article outlines the currently supported data sources for Azure Machine Learning data preparation.</span></span>

<span data-ttu-id="cfe7d-105">The supported data sources for this release are as follows.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-105">The supported data sources for this release are as follows.</span></span>

## <a name="types"></a><span data-ttu-id="cfe7d-106">Types</span><span class="sxs-lookup"><span data-stu-id="cfe7d-106">Types</span></span> 

### <a name="sql-server"></a><span data-ttu-id="cfe7d-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cfe7d-107">SQL Server</span></span>
<span data-ttu-id="cfe7d-108">Read from on-prem SQL server or Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-108">Read from on-prem SQL server or Azure SQL database.</span></span>

#### <a name="options"></a><span data-ttu-id="cfe7d-109">Options</span><span class="sxs-lookup"><span data-stu-id="cfe7d-109">Options</span></span>
- <span data-ttu-id="cfe7d-110">Server Address</span><span class="sxs-lookup"><span data-stu-id="cfe7d-110">Server Address</span></span>
- <span data-ttu-id="cfe7d-111">Trust Server (Even when the certificate on the server is not valid.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-111">Trust Server (Even when the certificate on the server is not valid.</span></span> <span data-ttu-id="cfe7d-112">Use with caution)</span><span class="sxs-lookup"><span data-stu-id="cfe7d-112">Use with caution)</span></span>
- <span data-ttu-id="cfe7d-113">Authentication Type (Windows, Server)</span><span class="sxs-lookup"><span data-stu-id="cfe7d-113">Authentication Type (Windows, Server)</span></span>
- <span data-ttu-id="cfe7d-114">User Name</span><span class="sxs-lookup"><span data-stu-id="cfe7d-114">User Name</span></span>
- <span data-ttu-id="cfe7d-115">Password</span><span class="sxs-lookup"><span data-stu-id="cfe7d-115">Password</span></span>
- <span data-ttu-id="cfe7d-116">Database to connect to</span><span class="sxs-lookup"><span data-stu-id="cfe7d-116">Database to connect to</span></span>
- <span data-ttu-id="cfe7d-117">SQL Query</span><span class="sxs-lookup"><span data-stu-id="cfe7d-117">SQL Query</span></span>

#### <a name="notes"></a><span data-ttu-id="cfe7d-118">Notes</span><span class="sxs-lookup"><span data-stu-id="cfe7d-118">Notes</span></span>
- <span data-ttu-id="cfe7d-119">Sql-variant columns are not supported</span><span class="sxs-lookup"><span data-stu-id="cfe7d-119">Sql-variant columns are not supported</span></span>
- <span data-ttu-id="cfe7d-120">Time column is converted to datetime by appending time from database to date 1970/1/1</span><span class="sxs-lookup"><span data-stu-id="cfe7d-120">Time column is converted to datetime by appending time from database to date 1970/1/1</span></span>
- <span data-ttu-id="cfe7d-121">When executed on Spark cluster, all data related columns (date, datetime, datetime2, datetimeoffset) will evaluate incorrect values for dates before 1583</span><span class="sxs-lookup"><span data-stu-id="cfe7d-121">When executed on Spark cluster, all data related columns (date, datetime, datetime2, datetimeoffset) will evaluate incorrect values for dates before 1583</span></span>
- <span data-ttu-id="cfe7d-122">Values in decimal columns may lose precision due to conversion to decimal</span><span class="sxs-lookup"><span data-stu-id="cfe7d-122">Values in decimal columns may lose precision due to conversion to decimal</span></span>

### <a name="directory-vs-file"></a><span data-ttu-id="cfe7d-123">Directory vs. file</span><span class="sxs-lookup"><span data-stu-id="cfe7d-123">Directory vs. file</span></span>
<span data-ttu-id="cfe7d-124">Choose a single file and read it into data preparation.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-124">Choose a single file and read it into data preparation.</span></span> <span data-ttu-id="cfe7d-125">The file type is parsed to determine the default parameters for the file connection shown on the next screen.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-125">The file type is parsed to determine the default parameters for the file connection shown on the next screen.</span></span>

<span data-ttu-id="cfe7d-126">Choose a directory or a set of files within a directory (the file picker is multiselect).</span><span class="sxs-lookup"><span data-stu-id="cfe7d-126">Choose a directory or a set of files within a directory (the file picker is multiselect).</span></span> <span data-ttu-id="cfe7d-127">With either approach, the files are read in as a single data flow and are appended to each other, with headers stripped out if needed.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-127">With either approach, the files are read in as a single data flow and are appended to each other, with headers stripped out if needed.</span></span>

<span data-ttu-id="cfe7d-128">The supported file types are:</span><span class="sxs-lookup"><span data-stu-id="cfe7d-128">The supported file types are:</span></span>
- <span data-ttu-id="cfe7d-129">Delimited (.csv, .tsv, .txt, etc.)</span><span class="sxs-lookup"><span data-stu-id="cfe7d-129">Delimited (.csv, .tsv, .txt, etc.)</span></span>
- <span data-ttu-id="cfe7d-130">Fixed width</span><span class="sxs-lookup"><span data-stu-id="cfe7d-130">Fixed width</span></span>
- <span data-ttu-id="cfe7d-131">Plain text</span><span class="sxs-lookup"><span data-stu-id="cfe7d-131">Plain text</span></span>
- <span data-ttu-id="cfe7d-132">JSON file</span><span class="sxs-lookup"><span data-stu-id="cfe7d-132">JSON file</span></span>

### <a name="csv-file"></a><span data-ttu-id="cfe7d-133">CSV file</span><span class="sxs-lookup"><span data-stu-id="cfe7d-133">CSV file</span></span>
<span data-ttu-id="cfe7d-134">Read a comma-separated-value file from storage.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-134">Read a comma-separated-value file from storage.</span></span>

#### <a name="options"></a><span data-ttu-id="cfe7d-135">Options</span><span class="sxs-lookup"><span data-stu-id="cfe7d-135">Options</span></span>
- <span data-ttu-id="cfe7d-136">Separator</span><span class="sxs-lookup"><span data-stu-id="cfe7d-136">Separator</span></span>
- <span data-ttu-id="cfe7d-137">Comment</span><span class="sxs-lookup"><span data-stu-id="cfe7d-137">Comment</span></span>
- <span data-ttu-id="cfe7d-138">Headers</span><span class="sxs-lookup"><span data-stu-id="cfe7d-138">Headers</span></span>
- <span data-ttu-id="cfe7d-139">Decimal symbol</span><span class="sxs-lookup"><span data-stu-id="cfe7d-139">Decimal symbol</span></span>
- <span data-ttu-id="cfe7d-140">File encoding</span><span class="sxs-lookup"><span data-stu-id="cfe7d-140">File encoding</span></span>
- <span data-ttu-id="cfe7d-141">Lines to skip</span><span class="sxs-lookup"><span data-stu-id="cfe7d-141">Lines to skip</span></span>

### <a name="tsv-file"></a><span data-ttu-id="cfe7d-142">TSV file</span><span class="sxs-lookup"><span data-stu-id="cfe7d-142">TSV file</span></span>
<span data-ttu-id="cfe7d-143">Read a tab-separated-value file from storage.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-143">Read a tab-separated-value file from storage.</span></span>

#### <a name="options"></a><span data-ttu-id="cfe7d-144">Options</span><span class="sxs-lookup"><span data-stu-id="cfe7d-144">Options</span></span>
- <span data-ttu-id="cfe7d-145">Comment</span><span class="sxs-lookup"><span data-stu-id="cfe7d-145">Comment</span></span>
- <span data-ttu-id="cfe7d-146">Headers</span><span class="sxs-lookup"><span data-stu-id="cfe7d-146">Headers</span></span>
- <span data-ttu-id="cfe7d-147">File encoding</span><span class="sxs-lookup"><span data-stu-id="cfe7d-147">File encoding</span></span>
- <span data-ttu-id="cfe7d-148">Lines to skip</span><span class="sxs-lookup"><span data-stu-id="cfe7d-148">Lines to skip</span></span>

### <a name="excel-xlsxlsx"></a><span data-ttu-id="cfe7d-149">Excel (.xls/.xlsx)</span><span class="sxs-lookup"><span data-stu-id="cfe7d-149">Excel (.xls/.xlsx)</span></span>
<span data-ttu-id="cfe7d-150">Read an Excel file one sheet at a time by specifying sheet name or number.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-150">Read an Excel file one sheet at a time by specifying sheet name or number.</span></span>

#### <a name="options"></a><span data-ttu-id="cfe7d-151">Options</span><span class="sxs-lookup"><span data-stu-id="cfe7d-151">Options</span></span>
- <span data-ttu-id="cfe7d-152">Sheet name or number</span><span class="sxs-lookup"><span data-stu-id="cfe7d-152">Sheet name or number</span></span>
- <span data-ttu-id="cfe7d-153">Headers</span><span class="sxs-lookup"><span data-stu-id="cfe7d-153">Headers</span></span>
- <span data-ttu-id="cfe7d-154">Lines to skip</span><span class="sxs-lookup"><span data-stu-id="cfe7d-154">Lines to skip</span></span>

### <a name="json-file"></a><span data-ttu-id="cfe7d-155">JSON file</span><span class="sxs-lookup"><span data-stu-id="cfe7d-155">JSON file</span></span>
<span data-ttu-id="cfe7d-156">Read a JSON file from storage.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-156">Read a JSON file from storage.</span></span> <span data-ttu-id="cfe7d-157">The file is "flattened" on read.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-157">The file is "flattened" on read.</span></span>

#### <a name="options"></a><span data-ttu-id="cfe7d-158">Options</span><span class="sxs-lookup"><span data-stu-id="cfe7d-158">Options</span></span>
- <span data-ttu-id="cfe7d-159">None</span><span class="sxs-lookup"><span data-stu-id="cfe7d-159">None</span></span>

### <a name="parquet"></a><span data-ttu-id="cfe7d-160">Parquet</span><span class="sxs-lookup"><span data-stu-id="cfe7d-160">Parquet</span></span>
<span data-ttu-id="cfe7d-161">Read a Parquet data set, either a single file or a folder.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-161">Read a Parquet data set, either a single file or a folder.</span></span>

<span data-ttu-id="cfe7d-162">Parquet as a format can take various forms in storage.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-162">Parquet as a format can take various forms in storage.</span></span> <span data-ttu-id="cfe7d-163">For smaller data sets, a single .parquet file is sometimes used.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-163">For smaller data sets, a single .parquet file is sometimes used.</span></span> <span data-ttu-id="cfe7d-164">Various Python libraries support reading or writing to single .parquet files.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-164">Various Python libraries support reading or writing to single .parquet files.</span></span> <span data-ttu-id="cfe7d-165">For the moment, Azure Machine Learning data preparation relies on the PyArrow Python library for reading Parquet during local interactive use.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-165">For the moment, Azure Machine Learning data preparation relies on the PyArrow Python library for reading Parquet during local interactive use.</span></span> <span data-ttu-id="cfe7d-166">It supports single .parquet files (as long as they were written as such, and not as part of a larger data set), as well as Parquet data sets.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-166">It supports single .parquet files (as long as they were written as such, and not as part of a larger data set), as well as Parquet data sets.</span></span>

<span data-ttu-id="cfe7d-167">A Parquet data set is a collection of more than one .parquet file, each of which represents a smaller partition of a larger data set.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-167">A Parquet data set is a collection of more than one .parquet file, each of which represents a smaller partition of a larger data set.</span></span> <span data-ttu-id="cfe7d-168">Data sets are usually contained in a folder and are the default parquet output format for platforms such as Spark and Hive.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-168">Data sets are usually contained in a folder and are the default parquet output format for platforms such as Spark and Hive.</span></span>

>[!NOTE]
><span data-ttu-id="cfe7d-169">When you're reading Parquet data that's in a folder with multiple .parquet files, it's safest to select the directory for reading, and the **Parquet data set** option.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-169">When you're reading Parquet data that's in a folder with multiple .parquet files, it's safest to select the directory for reading, and the **Parquet data set** option.</span></span> <span data-ttu-id="cfe7d-170">This makes PyArrow read the whole folder instead of the individual files.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-170">This makes PyArrow read the whole folder instead of the individual files.</span></span> <span data-ttu-id="cfe7d-171">This ensures support for reading more complicated ways of storing Parquet on disk, such as folder partitioning.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-171">This ensures support for reading more complicated ways of storing Parquet on disk, such as folder partitioning.</span></span>

<span data-ttu-id="cfe7d-172">Scale-out execution relies on Spark's Parquet reading capabilities and supports single files as well as folders, similar to local interactive use.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-172">Scale-out execution relies on Spark's Parquet reading capabilities and supports single files as well as folders, similar to local interactive use.</span></span>

#### <a name="options"></a><span data-ttu-id="cfe7d-173">Options</span><span class="sxs-lookup"><span data-stu-id="cfe7d-173">Options</span></span>
- <span data-ttu-id="cfe7d-174">Parquet data set.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-174">Parquet data set.</span></span> <span data-ttu-id="cfe7d-175">This option determines whether Azure Machine Learning data preparation expands a given directory and attempts to read each file individually (the unselected mode), or whether it treats the directory as the whole data set (the selected mode).</span><span class="sxs-lookup"><span data-stu-id="cfe7d-175">This option determines whether Azure Machine Learning data preparation expands a given directory and attempts to read each file individually (the unselected mode), or whether it treats the directory as the whole data set (the selected mode).</span></span> <span data-ttu-id="cfe7d-176">With the selected mode, PyArrow chooses the best way to interpret the files.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-176">With the selected mode, PyArrow chooses the best way to interpret the files.</span></span>


## <a name="locations"></a><span data-ttu-id="cfe7d-177">Locations</span><span class="sxs-lookup"><span data-stu-id="cfe7d-177">Locations</span></span>
### <a name="local"></a><span data-ttu-id="cfe7d-178">Local</span><span class="sxs-lookup"><span data-stu-id="cfe7d-178">Local</span></span>
<span data-ttu-id="cfe7d-179">A local hard drive or a mapped network storage location.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-179">A local hard drive or a mapped network storage location.</span></span>

### <a name="sql-server"></a><span data-ttu-id="cfe7d-180">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cfe7d-180">SQL Server</span></span>
<span data-ttu-id="cfe7d-181">On-prem SQL sever, or Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-181">On-prem SQL sever, or Azure SQL database.</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="cfe7d-182">Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="cfe7d-182">Azure Blob storage</span></span>
<span data-ttu-id="cfe7d-183">Azure Blob storage, which requires an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cfe7d-183">Azure Blob storage, which requires an Azure subscription.</span></span>

