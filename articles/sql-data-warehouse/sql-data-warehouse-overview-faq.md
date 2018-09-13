---
title: Azure SQL Data Warehouse Frequently Asked Questions | Microsoft Docs
description: This article lists out frequently asked questions about Azure SQL Data Warehouse from customers and developers
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: ''
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter
ms.openlocfilehash: 49cbfca4f733356548b6c8f491fead9e2d7fdf5c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548996"
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="6870f-103">SQL Data Warehouse Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="6870f-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="6870f-104">General</span><span class="sxs-lookup"><span data-stu-id="6870f-104">General</span></span>

<span data-ttu-id="6870f-105">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-105">Q.</span></span> <span data-ttu-id="6870f-106">What does SQL DW offer for data security?</span><span class="sxs-lookup"><span data-stu-id="6870f-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="6870f-107">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-107">A.</span></span> <span data-ttu-id="6870f-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span><span class="sxs-lookup"><span data-stu-id="6870f-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="6870f-109">For more information, see [Security].</span><span class="sxs-lookup"><span data-stu-id="6870f-109">For more information, see [Security].</span></span>

<span data-ttu-id="6870f-110">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-110">Q.</span></span> <span data-ttu-id="6870f-111">Where can I find out what legal or business standards is SQL DW compliant with?</span><span class="sxs-lookup"><span data-stu-id="6870f-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="6870f-112">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-112">A.</span></span> <span data-ttu-id="6870f-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span><span class="sxs-lookup"><span data-stu-id="6870f-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="6870f-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span><span class="sxs-lookup"><span data-stu-id="6870f-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="6870f-115">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-115">Q.</span></span> <span data-ttu-id="6870f-116">Can I connect PowerBI?</span><span class="sxs-lookup"><span data-stu-id="6870f-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="6870f-117">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-117">A.</span></span> <span data-ttu-id="6870f-118">Yes!</span><span class="sxs-lookup"><span data-stu-id="6870f-118">Yes!</span></span> <span data-ttu-id="6870f-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span><span class="sxs-lookup"><span data-stu-id="6870f-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="6870f-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span><span class="sxs-lookup"><span data-stu-id="6870f-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="6870f-121">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-121">Q.</span></span> <span data-ttu-id="6870f-122">What are SQL Data Warehouse Capacity Limits?</span><span class="sxs-lookup"><span data-stu-id="6870f-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="6870f-123">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-123">A.</span></span> <span data-ttu-id="6870f-124">See our current [capacity limits] page.</span><span class="sxs-lookup"><span data-stu-id="6870f-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="6870f-125">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-125">Q.</span></span> <span data-ttu-id="6870f-126">Why is my Scale/Pause/Resume taking so long?</span><span class="sxs-lookup"><span data-stu-id="6870f-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="6870f-127">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-127">A.</span></span> <span data-ttu-id="6870f-128">A variety of factors can influence the time for compute management operations.</span><span class="sxs-lookup"><span data-stu-id="6870f-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="6870f-129">A common case for  long running operations is transactional rollback.</span><span class="sxs-lookup"><span data-stu-id="6870f-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="6870f-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span><span class="sxs-lookup"><span data-stu-id="6870f-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="6870f-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span><span class="sxs-lookup"><span data-stu-id="6870f-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="6870f-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span><span class="sxs-lookup"><span data-stu-id="6870f-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="6870f-133">User support</span><span class="sxs-lookup"><span data-stu-id="6870f-133">User support</span></span>

<span data-ttu-id="6870f-134">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-134">Q.</span></span> <span data-ttu-id="6870f-135">I have a feature request, where do I submit it?</span><span class="sxs-lookup"><span data-stu-id="6870f-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="6870f-136">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-136">A.</span></span> <span data-ttu-id="6870f-137">If you have a feature request, submit it on our [UserVoice] page</span><span class="sxs-lookup"><span data-stu-id="6870f-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="6870f-138">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-138">Q.</span></span> <span data-ttu-id="6870f-139">How can I do x?</span><span class="sxs-lookup"><span data-stu-id="6870f-139">How can I do x?</span></span>

<span data-ttu-id="6870f-140">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-140">A.</span></span> <span data-ttu-id="6870f-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span><span class="sxs-lookup"><span data-stu-id="6870f-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="6870f-142">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-142">Q.</span></span> <span data-ttu-id="6870f-143">How do I submit a support ticket?</span><span class="sxs-lookup"><span data-stu-id="6870f-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="6870f-144">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-144">A.</span></span> <span data-ttu-id="6870f-145">[Support Tickets] can be filed through Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6870f-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="6870f-146">SQL language/feature support</span><span class="sxs-lookup"><span data-stu-id="6870f-146">SQL language/feature support</span></span> 

<span data-ttu-id="6870f-147">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-147">Q.</span></span> <span data-ttu-id="6870f-148">What datatypes does SQL Data Warehouse support?</span><span class="sxs-lookup"><span data-stu-id="6870f-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="6870f-149">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-149">A.</span></span> <span data-ttu-id="6870f-150">See SQL Data Warehouse [data types].</span><span class="sxs-lookup"><span data-stu-id="6870f-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="6870f-151">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-151">Q.</span></span> <span data-ttu-id="6870f-152">What table features do you support?</span><span class="sxs-lookup"><span data-stu-id="6870f-152">What table features do you support?</span></span>

<span data-ttu-id="6870f-153">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-153">A.</span></span> <span data-ttu-id="6870f-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span><span class="sxs-lookup"><span data-stu-id="6870f-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="6870f-155">Tooling and administration</span><span class="sxs-lookup"><span data-stu-id="6870f-155">Tooling and administration</span></span>

<span data-ttu-id="6870f-156">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-156">Q.</span></span> <span data-ttu-id="6870f-157">Do you support Database projects in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6870f-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="6870f-158">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-158">A.</span></span> <span data-ttu-id="6870f-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6870f-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="6870f-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span><span class="sxs-lookup"><span data-stu-id="6870f-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="6870f-161">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-161">Q.</span></span> <span data-ttu-id="6870f-162">Does SQL Data Warehouse support REST APIs?</span><span class="sxs-lookup"><span data-stu-id="6870f-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="6870f-163">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-163">A.</span></span> <span data-ttu-id="6870f-164">Yes.</span><span class="sxs-lookup"><span data-stu-id="6870f-164">Yes.</span></span> <span data-ttu-id="6870f-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6870f-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="6870f-166">You can find API information within REST documentation pages or [MSDN].</span><span class="sxs-lookup"><span data-stu-id="6870f-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="6870f-167">Loading</span><span class="sxs-lookup"><span data-stu-id="6870f-167">Loading</span></span>

<span data-ttu-id="6870f-168">Q.</span><span class="sxs-lookup"><span data-stu-id="6870f-168">Q.</span></span> <span data-ttu-id="6870f-169">What client drivers do you support?</span><span class="sxs-lookup"><span data-stu-id="6870f-169">What client drivers do you support?</span></span>

<span data-ttu-id="6870f-170">A.</span><span class="sxs-lookup"><span data-stu-id="6870f-170">A.</span></span> <span data-ttu-id="6870f-171">Driver support for DW can be found on the [Connection Strings] page</span><span class="sxs-lookup"><span data-stu-id="6870f-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="6870f-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="6870f-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="6870f-173">A: Orc, RC, Parquet, and flat delimited text</span><span class="sxs-lookup"><span data-stu-id="6870f-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="6870f-174">Q: What can I connect to from SQL DW using PolyBase?</span><span class="sxs-lookup"><span data-stu-id="6870f-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="6870f-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span><span class="sxs-lookup"><span data-stu-id="6870f-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="6870f-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span><span class="sxs-lookup"><span data-stu-id="6870f-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="6870f-177">A: No, SQL DW PolyBase only interacts the storage components.</span><span class="sxs-lookup"><span data-stu-id="6870f-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="6870f-178">Q: Can I connect to HDI?</span><span class="sxs-lookup"><span data-stu-id="6870f-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="6870f-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span><span class="sxs-lookup"><span data-stu-id="6870f-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="6870f-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span><span class="sxs-lookup"><span data-stu-id="6870f-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="6870f-181">However, you cannot generate pushdown computation to the HDI instance.</span><span class="sxs-lookup"><span data-stu-id="6870f-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6870f-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="6870f-182">Next steps</span></span>
<span data-ttu-id="6870f-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span><span class="sxs-lookup"><span data-stu-id="6870f-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Connection Strings]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Security]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[data types]: ./sql-data-warehouse-tables-data-types.md
[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Overview]: ./sql-data-warehouse-overview-faq.md