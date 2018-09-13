---
title: Migrate your data to SQL Data Warehouse | Microsoft Docs
description: Tips for migrating your data to Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: f2fbb90fedb303febbb9663b898640428f92b572
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554956"
---
# <a name="migrate-your-data"></a><span data-ttu-id="4eae9-103">Migrate Your Data</span><span class="sxs-lookup"><span data-stu-id="4eae9-103">Migrate Your Data</span></span>
<span data-ttu-id="4eae9-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span><span class="sxs-lookup"><span data-stu-id="4eae9-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="4eae9-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span><span class="sxs-lookup"><span data-stu-id="4eae9-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="4eae9-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span><span class="sxs-lookup"><span data-stu-id="4eae9-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="4eae9-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span><span class="sxs-lookup"><span data-stu-id="4eae9-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="4eae9-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span><span class="sxs-lookup"><span data-stu-id="4eae9-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="4eae9-109">It then look a little deeper into how the migration can be optimized.</span><span class="sxs-lookup"><span data-stu-id="4eae9-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="4eae9-110">Azure Data Factory (ADF) copy</span><span class="sxs-lookup"><span data-stu-id="4eae9-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="4eae9-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="4eae9-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="4eae9-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4eae9-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="4eae9-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4eae9-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="4eae9-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4eae9-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="4eae9-115">PolyBase also provides a high-performance option for loading the data.</span><span class="sxs-lookup"><span data-stu-id="4eae9-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="4eae9-116">However, that does mean using two tools instead of one.</span><span class="sxs-lookup"><span data-stu-id="4eae9-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="4eae9-117">If you need the best performance then use PolyBase.</span><span class="sxs-lookup"><span data-stu-id="4eae9-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="4eae9-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span><span class="sxs-lookup"><span data-stu-id="4eae9-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="4eae9-119">Head over to the following article for some great [ADF samples][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="4eae9-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="4eae9-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="4eae9-120">Integration Services</span></span>
<span data-ttu-id="4eae9-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span><span class="sxs-lookup"><span data-stu-id="4eae9-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="4eae9-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span><span class="sxs-lookup"><span data-stu-id="4eae9-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="4eae9-123">SSIS can export to UTF-8 without the byte order mark in the file.</span><span class="sxs-lookup"><span data-stu-id="4eae9-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="4eae9-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span><span class="sxs-lookup"><span data-stu-id="4eae9-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="4eae9-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span><span class="sxs-lookup"><span data-stu-id="4eae9-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="4eae9-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span><span class="sxs-lookup"><span data-stu-id="4eae9-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="4eae9-127">However, your connections will need to be using an ADO.NET connection manager.</span><span class="sxs-lookup"><span data-stu-id="4eae9-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="4eae9-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span><span class="sxs-lookup"><span data-stu-id="4eae9-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="4eae9-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span><span class="sxs-lookup"><span data-stu-id="4eae9-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="4eae9-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span><span class="sxs-lookup"><span data-stu-id="4eae9-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="4eae9-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span><span class="sxs-lookup"><span data-stu-id="4eae9-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="4eae9-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span><span class="sxs-lookup"><span data-stu-id="4eae9-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="4eae9-133">For more information consult the [SSIS documentation][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="4eae9-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="4eae9-134">bcp</span><span class="sxs-lookup"><span data-stu-id="4eae9-134">bcp</span></span>
<span data-ttu-id="4eae9-135">bcp is a command-line utility that is designed for flat file data import and export.</span><span class="sxs-lookup"><span data-stu-id="4eae9-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="4eae9-136">Some transformation can take place during data export.</span><span class="sxs-lookup"><span data-stu-id="4eae9-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="4eae9-137">To perform simple transformations use a query to select and transform the data.</span><span class="sxs-lookup"><span data-stu-id="4eae9-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="4eae9-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="4eae9-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="4eae9-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span><span class="sxs-lookup"><span data-stu-id="4eae9-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="4eae9-140">This ensures that the logic is retained and the process is repeatable.</span><span class="sxs-lookup"><span data-stu-id="4eae9-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="4eae9-141">Advantages of bcp are:</span><span class="sxs-lookup"><span data-stu-id="4eae9-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="4eae9-142">Simplicity.</span><span class="sxs-lookup"><span data-stu-id="4eae9-142">Simplicity.</span></span> <span data-ttu-id="4eae9-143">bcp commands are simple to build and execute</span><span class="sxs-lookup"><span data-stu-id="4eae9-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="4eae9-144">Re-startable load process.</span><span class="sxs-lookup"><span data-stu-id="4eae9-144">Re-startable load process.</span></span> <span data-ttu-id="4eae9-145">Once exported the load can be executed any number of times</span><span class="sxs-lookup"><span data-stu-id="4eae9-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="4eae9-146">Limitations of bcp are:</span><span class="sxs-lookup"><span data-stu-id="4eae9-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="4eae9-147">bcp works with tabulated flat files only.</span><span class="sxs-lookup"><span data-stu-id="4eae9-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="4eae9-148">It does not work with files such as xml or JSON</span><span class="sxs-lookup"><span data-stu-id="4eae9-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="4eae9-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span><span class="sxs-lookup"><span data-stu-id="4eae9-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="4eae9-150">bcp has not been adapted to be robust when loading data over the internet.</span><span class="sxs-lookup"><span data-stu-id="4eae9-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="4eae9-151">Any network instability may cause a load error.</span><span class="sxs-lookup"><span data-stu-id="4eae9-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="4eae9-152">bcp relies on the schema being present in the target database prior to the load</span><span class="sxs-lookup"><span data-stu-id="4eae9-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="4eae9-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4eae9-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="4eae9-154">Optimizing data migration</span><span class="sxs-lookup"><span data-stu-id="4eae9-154">Optimizing data migration</span></span>
<span data-ttu-id="4eae9-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span><span class="sxs-lookup"><span data-stu-id="4eae9-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="4eae9-156">Export of source data</span><span class="sxs-lookup"><span data-stu-id="4eae9-156">Export of source data</span></span>
2. <span data-ttu-id="4eae9-157">Transfer of data to Azure</span><span class="sxs-lookup"><span data-stu-id="4eae9-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="4eae9-158">Load into the target SQLDW database</span><span class="sxs-lookup"><span data-stu-id="4eae9-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="4eae9-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span><span class="sxs-lookup"><span data-stu-id="4eae9-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="4eae9-160">Optimizing data load</span><span class="sxs-lookup"><span data-stu-id="4eae9-160">Optimizing data load</span></span>
<span data-ttu-id="4eae9-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="4eae9-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="4eae9-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span><span class="sxs-lookup"><span data-stu-id="4eae9-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="4eae9-163">They are:</span><span class="sxs-lookup"><span data-stu-id="4eae9-163">They are:</span></span>

1. <span data-ttu-id="4eae9-164">Encoding of data files</span><span class="sxs-lookup"><span data-stu-id="4eae9-164">Encoding of data files</span></span>
2. <span data-ttu-id="4eae9-165">Format of data files</span><span class="sxs-lookup"><span data-stu-id="4eae9-165">Format of data files</span></span>
3. <span data-ttu-id="4eae9-166">Location of data files</span><span class="sxs-lookup"><span data-stu-id="4eae9-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="4eae9-167">Encoding</span><span class="sxs-lookup"><span data-stu-id="4eae9-167">Encoding</span></span>
<span data-ttu-id="4eae9-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="4eae9-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="4eae9-169">Format of data files</span><span class="sxs-lookup"><span data-stu-id="4eae9-169">Format of data files</span></span>
<span data-ttu-id="4eae9-170">PolyBase mandates a fixed row terminator of \n or newline.</span><span class="sxs-lookup"><span data-stu-id="4eae9-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="4eae9-171">Your data files must conform to this standard.</span><span class="sxs-lookup"><span data-stu-id="4eae9-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="4eae9-172">There aren't any restrictions on string or column terminators.</span><span class="sxs-lookup"><span data-stu-id="4eae9-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="4eae9-173">You will have to define every column in the file as part of your external table in PolyBase.</span><span class="sxs-lookup"><span data-stu-id="4eae9-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="4eae9-174">Make sure that all exported columns are required and that the types conform to the required standards.</span><span class="sxs-lookup"><span data-stu-id="4eae9-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="4eae9-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span><span class="sxs-lookup"><span data-stu-id="4eae9-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="4eae9-176">Location of data files</span><span class="sxs-lookup"><span data-stu-id="4eae9-176">Location of data files</span></span>
<span data-ttu-id="4eae9-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span><span class="sxs-lookup"><span data-stu-id="4eae9-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="4eae9-178">Consequently, the data must have been first transferred into blob storage.</span><span class="sxs-lookup"><span data-stu-id="4eae9-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="4eae9-179">Optimizing data transfer</span><span class="sxs-lookup"><span data-stu-id="4eae9-179">Optimizing data transfer</span></span>
<span data-ttu-id="4eae9-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span><span class="sxs-lookup"><span data-stu-id="4eae9-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="4eae9-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span><span class="sxs-lookup"><span data-stu-id="4eae9-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="4eae9-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span><span class="sxs-lookup"><span data-stu-id="4eae9-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="4eae9-183">However, these errors may require data to be re-sent either in whole or in part.</span><span class="sxs-lookup"><span data-stu-id="4eae9-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="4eae9-184">Fortunately you have several options to improve the speed and resilience of this process:</span><span class="sxs-lookup"><span data-stu-id="4eae9-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="4eae9-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="4eae9-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="4eae9-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span><span class="sxs-lookup"><span data-stu-id="4eae9-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="4eae9-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span><span class="sxs-lookup"><span data-stu-id="4eae9-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="4eae9-188">This is by no means a mandatory step.</span><span class="sxs-lookup"><span data-stu-id="4eae9-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="4eae9-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span><span class="sxs-lookup"><span data-stu-id="4eae9-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="4eae9-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span><span class="sxs-lookup"><span data-stu-id="4eae9-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="4eae9-191">Increased reliability</span><span class="sxs-lookup"><span data-stu-id="4eae9-191">Increased reliability</span></span>
2. <span data-ttu-id="4eae9-192">Faster network speed</span><span class="sxs-lookup"><span data-stu-id="4eae9-192">Faster network speed</span></span>
3. <span data-ttu-id="4eae9-193">Lower network latency</span><span class="sxs-lookup"><span data-stu-id="4eae9-193">Lower network latency</span></span>
4. <span data-ttu-id="4eae9-194">higher network security</span><span class="sxs-lookup"><span data-stu-id="4eae9-194">higher network security</span></span>

<span data-ttu-id="4eae9-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span><span class="sxs-lookup"><span data-stu-id="4eae9-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="4eae9-196">Interested?</span><span class="sxs-lookup"><span data-stu-id="4eae9-196">Interested?</span></span> <span data-ttu-id="4eae9-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="4eae9-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="4eae9-198">Azure Import and Export Service</span><span class="sxs-lookup"><span data-stu-id="4eae9-198">Azure Import and Export Service</span></span>
<span data-ttu-id="4eae9-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span><span class="sxs-lookup"><span data-stu-id="4eae9-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="4eae9-200">It involves writing your data to disks and shipping them to an Azure data center.</span><span class="sxs-lookup"><span data-stu-id="4eae9-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="4eae9-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span><span class="sxs-lookup"><span data-stu-id="4eae9-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="4eae9-202">A high-level view of the import export process is as follows:</span><span class="sxs-lookup"><span data-stu-id="4eae9-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="4eae9-203">Configure an Azure Blob Storage container to receive the data</span><span class="sxs-lookup"><span data-stu-id="4eae9-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="4eae9-204">Export your data to local storage</span><span class="sxs-lookup"><span data-stu-id="4eae9-204">Export your data to local storage</span></span>
3. <span data-ttu-id="4eae9-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span><span class="sxs-lookup"><span data-stu-id="4eae9-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="4eae9-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span><span class="sxs-lookup"><span data-stu-id="4eae9-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="4eae9-207">Ship the disks your nominated Azure data center</span><span class="sxs-lookup"><span data-stu-id="4eae9-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="4eae9-208">Your data is transferred to your Azure Blob Storage container</span><span class="sxs-lookup"><span data-stu-id="4eae9-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="4eae9-209">Load the data into SQLDW using PolyBase</span><span class="sxs-lookup"><span data-stu-id="4eae9-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="4eae9-210">[AZCopy][AZCopy] utility</span><span class="sxs-lookup"><span data-stu-id="4eae9-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="4eae9-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span><span class="sxs-lookup"><span data-stu-id="4eae9-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="4eae9-212">It is designed for small (MB++) to very large (GB++) data transfers.</span><span class="sxs-lookup"><span data-stu-id="4eae9-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="4eae9-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span><span class="sxs-lookup"><span data-stu-id="4eae9-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="4eae9-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4eae9-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="4eae9-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span><span class="sxs-lookup"><span data-stu-id="4eae9-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="4eae9-216">To use AZCopy you will first need to download and install it.</span><span class="sxs-lookup"><span data-stu-id="4eae9-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="4eae9-217">There is a [production version][production version] and a [preview version][preview version] available.</span><span class="sxs-lookup"><span data-stu-id="4eae9-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="4eae9-218">To upload a file from your file system you will need a command like the one below:</span><span class="sxs-lookup"><span data-stu-id="4eae9-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="4eae9-219">A high-level process summary could be:</span><span class="sxs-lookup"><span data-stu-id="4eae9-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="4eae9-220">Configure an Azure storage blob container to receive the data</span><span class="sxs-lookup"><span data-stu-id="4eae9-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="4eae9-221">Export your data to local storage</span><span class="sxs-lookup"><span data-stu-id="4eae9-221">Export your data to local storage</span></span>
3. <span data-ttu-id="4eae9-222">AZCopy your data in the Azure Blob Storage container</span><span class="sxs-lookup"><span data-stu-id="4eae9-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="4eae9-223">Load the data into SQL Data Warehouse using PolyBase</span><span class="sxs-lookup"><span data-stu-id="4eae9-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="4eae9-224">Full documentation available: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="4eae9-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="4eae9-225">Optimizing data export</span><span class="sxs-lookup"><span data-stu-id="4eae9-225">Optimizing data export</span></span>
<span data-ttu-id="4eae9-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span><span class="sxs-lookup"><span data-stu-id="4eae9-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="4eae9-227">Data compression</span><span class="sxs-lookup"><span data-stu-id="4eae9-227">Data compression</span></span>
<span data-ttu-id="4eae9-228">PolyBase can read gzip compressed data.</span><span class="sxs-lookup"><span data-stu-id="4eae9-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="4eae9-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span><span class="sxs-lookup"><span data-stu-id="4eae9-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="4eae9-230">Multiple files</span><span class="sxs-lookup"><span data-stu-id="4eae9-230">Multiple files</span></span>
<span data-ttu-id="4eae9-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4eae9-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="4eae9-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span><span class="sxs-lookup"><span data-stu-id="4eae9-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="4eae9-233">It is therefore a good idea to isolate the files for each table into its own folder.</span><span class="sxs-lookup"><span data-stu-id="4eae9-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="4eae9-234">PolyBase also supports a feature known as "recursive folder traversal".</span><span class="sxs-lookup"><span data-stu-id="4eae9-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="4eae9-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span><span class="sxs-lookup"><span data-stu-id="4eae9-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="4eae9-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4eae9-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4eae9-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="4eae9-237">Next steps</span></span>
<span data-ttu-id="4eae9-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4eae9-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="4eae9-239">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="4eae9-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]: ../storage/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
