---
title: Azure Data Catalog supported data sources | Microsoft Docs
description: Specification of the currently supported data sources.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: jstevens
editor: ''
tags: ''
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 03/14/2017
ms.author: maroche
ms.openlocfilehash: 67c2eca1a6619ff695d13cea5d16b529ce64ba30
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555164"
---
# <a name="azure-data-catalog-supported-data-sources"></a><span data-ttu-id="c66d0-103">Azure Data Catalog supported data sources</span><span class="sxs-lookup"><span data-stu-id="c66d0-103">Azure Data Catalog supported data sources</span></span>

<span data-ttu-id="c66d0-104">You can publish meta data using a public API, a click-once registration tool, or by manually entering information directly to the Data Catalog web portal.</span><span class="sxs-lookup"><span data-stu-id="c66d0-104">You can publish meta data using a public API, a click-once registration tool, or by manually entering information directly to the Data Catalog web portal.</span></span> <span data-ttu-id="c66d0-105">The following grid summarizes all sources supported by the catalog today, and the publishing capabilities for each.</span><span class="sxs-lookup"><span data-stu-id="c66d0-105">The following grid summarizes all sources supported by the catalog today, and the publishing capabilities for each.</span></span>  <span data-ttu-id="c66d0-106">Also listed are the external data tools that each source can launch from our portal "open-in" experience.</span><span class="sxs-lookup"><span data-stu-id="c66d0-106">Also listed are the external data tools that each source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="c66d0-107">The second grid has a more technical specification of each data sources connection properties.</span><span class="sxs-lookup"><span data-stu-id="c66d0-107">The second grid has a more technical specification of each data sources connection properties.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="c66d0-108">List of supported data sources</span><span class="sxs-lookup"><span data-stu-id="c66d0-108">List of supported data sources</span></span>

<table>

    <tr>
       <td><span data-ttu-id="c66d0-109"><b>Data Source Object</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-109"><b>Data Source Object</b></span></span></td>
       <td><span data-ttu-id="c66d0-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="c66d0-111"><b>Manual Entry</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-111"><b>Manual Entry</b></span></span></td>
       <td><span data-ttu-id="c66d0-112"><b>Registration Tool</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-112"><b>Registration Tool</b></span></span></td>
       <td><span data-ttu-id="c66d0-113"><b>Open-In Tools</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-113"><b>Open-In Tools</b></span></span></td>
       <td><span data-ttu-id="c66d0-114"><b>Notes</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-114"><b>Notes</b></span></span></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-115">Azure Data Lake Store Directory</span><span class="sxs-lookup"><span data-stu-id="c66d0-115">Azure Data Lake Store Directory</span></span></td>
      <td><span data-ttu-id="c66d0-116">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-116">✓</span></span></td>
      <td><span data-ttu-id="c66d0-117">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-117">✓</span></span></td>
      <td><span data-ttu-id="c66d0-118">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-119">Azure Data Lake Store File</span><span class="sxs-lookup"><span data-stu-id="c66d0-119">Azure Data Lake Store File</span></span></td>
      <td><span data-ttu-id="c66d0-120">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-120">✓</span></span></td>
      <td><span data-ttu-id="c66d0-121">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-121">✓</span></span></td>
      <td><span data-ttu-id="c66d0-122">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-123">Azure Storage Blob</span><span class="sxs-lookup"><span data-stu-id="c66d0-123">Azure Storage Blob</span></span></td>
      <td><span data-ttu-id="c66d0-124">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-124">✓</span></span></td>
      <td><span data-ttu-id="c66d0-125">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-125">✓</span></span></td>
      <td><span data-ttu-id="c66d0-126">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-126">✓</span></span></td>
      <td><span data-ttu-id="c66d0-127"><font size=2>PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-127"><font size=2>PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-128">Azure Storage Directory</span><span class="sxs-lookup"><span data-stu-id="c66d0-128">Azure Storage Directory</span></span></td>
      <td><span data-ttu-id="c66d0-129">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-129">✓</span></span></td>
      <td><span data-ttu-id="c66d0-130">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-130">✓</span></span></td>
      <td><span data-ttu-id="c66d0-131">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-131">✓</span></span></td>
      <td><span data-ttu-id="c66d0-132"><font size=2>PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-132"><font size=2>PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-133">Azure Storage Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-133">Azure Storage Table</span></span></td>
      <td><span data-ttu-id="c66d0-134">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-134">✓</span></span></td>
      <td><span data-ttu-id="c66d0-135">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-135">✓</span></span></td>
      <td><span data-ttu-id="c66d0-136">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-137">HDFS Directory</span><span class="sxs-lookup"><span data-stu-id="c66d0-137">HDFS Directory</span></span></td>
      <td><span data-ttu-id="c66d0-138">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-138">✓</span></span></td>
      <td><span data-ttu-id="c66d0-139">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-139">✓</span></span></td>
      <td><span data-ttu-id="c66d0-140">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-141">HDFS File</span><span class="sxs-lookup"><span data-stu-id="c66d0-141">HDFS File</span></span></td>
      <td><span data-ttu-id="c66d0-142">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-142">✓</span></span></td>
      <td><span data-ttu-id="c66d0-143">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-143">✓</span></span></td>
      <td><span data-ttu-id="c66d0-144">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-145">Hive Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-145">Hive Table</span></span></td>
      <td><span data-ttu-id="c66d0-146">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-146">✓</span></span></td>
      <td><span data-ttu-id="c66d0-147">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-147">✓</span></span></td>
      <td><span data-ttu-id="c66d0-148">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-148">✓</span></span></td>
      <td><span data-ttu-id="c66d0-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-150">Hive View</span><span class="sxs-lookup"><span data-stu-id="c66d0-150">Hive View</span></span></td>
      <td><span data-ttu-id="c66d0-151">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-151">✓</span></span></td>
      <td><span data-ttu-id="c66d0-152">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-152">✓</span></span></td>
      <td><span data-ttu-id="c66d0-153">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-153">✓</span></span></td>
      <td><span data-ttu-id="c66d0-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-155">MySQL Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-155">MySQL Table</span></span></td>
      <td><span data-ttu-id="c66d0-156">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-156">✓</span></span></td>
      <td><span data-ttu-id="c66d0-157">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-157">✓</span></span></td>
      <td><span data-ttu-id="c66d0-158">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-158">✓</span></span></td>
      <td><span data-ttu-id="c66d0-159"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-159"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-160">MySQL View</span><span class="sxs-lookup"><span data-stu-id="c66d0-160">MySQL View</span></span></td>
      <td><span data-ttu-id="c66d0-161">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-161">✓</span></span></td>
      <td><span data-ttu-id="c66d0-162">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-162">✓</span></span></td>
      <td><span data-ttu-id="c66d0-163">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-163">✓</span></span></td>
      <td><span data-ttu-id="c66d0-164"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-164"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-165">Oracle Database Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-165">Oracle Database Table</span></span></td>
      <td><span data-ttu-id="c66d0-166">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-166">✓</span></span></td>
      <td><span data-ttu-id="c66d0-167">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-167">✓</span></span></td>
      <td><span data-ttu-id="c66d0-168">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-168">✓</span></span></td>
      <td><span data-ttu-id="c66d0-169"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-169"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-170">Oracle Database View</span><span class="sxs-lookup"><span data-stu-id="c66d0-170">Oracle Database View</span></span></td>
      <td><span data-ttu-id="c66d0-171">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-171">✓</span></span></td>
      <td><span data-ttu-id="c66d0-172">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-172">✓</span></span></td>
      <td><span data-ttu-id="c66d0-173">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-173">✓</span></span></td>
      <td><span data-ttu-id="c66d0-174"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-174"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-175">Other (Generic Asset)</span><span class="sxs-lookup"><span data-stu-id="c66d0-175">Other (Generic Asset)</span></span></td>
      <td><span data-ttu-id="c66d0-176">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-176">✓</span></span></td>
      <td><span data-ttu-id="c66d0-177">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-178">SQL Data Warehouse Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-178">SQL Data Warehouse Table</span></span></td>
      <td><span data-ttu-id="c66d0-179">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-179">✓</span></span></td>
      <td><span data-ttu-id="c66d0-180">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-180">✓</span></span></td>
      <td><span data-ttu-id="c66d0-181">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-181">✓</span></span></td>
      <td><span data-ttu-id="c66d0-182"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-182"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-183">SQL Data Warehouse View</span><span class="sxs-lookup"><span data-stu-id="c66d0-183">SQL Data Warehouse View</span></span></td>
      <td><span data-ttu-id="c66d0-184">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-184">✓</span></span></td>
      <td><span data-ttu-id="c66d0-185">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-185">✓</span></span></td>
      <td><span data-ttu-id="c66d0-186">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-186">✓</span></span></td>
      <td><span data-ttu-id="c66d0-187"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-187"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-188">SQL Server Analysis Services Dimension</span><span class="sxs-lookup"><span data-stu-id="c66d0-188">SQL Server Analysis Services Dimension</span></span></td>
      <td><span data-ttu-id="c66d0-189">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-189">✓</span></span></td>
      <td><span data-ttu-id="c66d0-190">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-190">✓</span></span></td>
      <td><span data-ttu-id="c66d0-191">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-191">✓</span></span></td>
      <td><span data-ttu-id="c66d0-192"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-192"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-193">SQL Server Analysis Services KPI</span><span class="sxs-lookup"><span data-stu-id="c66d0-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="c66d0-194">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-194">✓</span></span></td>
      <td><span data-ttu-id="c66d0-195">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-195">✓</span></span></td>
      <td><span data-ttu-id="c66d0-196">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-196">✓</span></span></td>
      <td><span data-ttu-id="c66d0-197"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-197"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-198">SQL Server Analysis Services Measure</span><span class="sxs-lookup"><span data-stu-id="c66d0-198">SQL Server Analysis Services Measure</span></span></td>
      <td><span data-ttu-id="c66d0-199">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-199">✓</span></span></td>
      <td><span data-ttu-id="c66d0-200">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-200">✓</span></span></td>
      <td><span data-ttu-id="c66d0-201">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-201">✓</span></span></td>
      <td><span data-ttu-id="c66d0-202"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-202"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-203">SQL Server Analysis Services Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-203">SQL Server Analysis Services Table</span></span></td>
      <td><span data-ttu-id="c66d0-204">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-204">✓</span></span></td>
      <td><span data-ttu-id="c66d0-205">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-205">✓</span></span></td>
      <td><span data-ttu-id="c66d0-206">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-206">✓</span></span></td>
      <td><span data-ttu-id="c66d0-207"><font size=2>Excel, PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-207"><font size=2>Excel, PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-208">SQL Server Reporting Services Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-208">SQL Server Reporting Services Report</span></span></td>
      <td><span data-ttu-id="c66d0-209">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-209">✓</span></span></td>
      <td><span data-ttu-id="c66d0-210">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-210">✓</span></span></td>
      <td><span data-ttu-id="c66d0-211">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-211">✓</span></span></td>
      <td><span data-ttu-id="c66d0-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="c66d0-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-214">SQL Server Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-214">SQL Server Table</span></span></td>
      <td><span data-ttu-id="c66d0-215">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-215">✓</span></span></td>
      <td><span data-ttu-id="c66d0-216">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-216">✓</span></span></td>
      <td><span data-ttu-id="c66d0-217">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-217">✓</span></span></td>
      <td><span data-ttu-id="c66d0-218"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-218"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-219">SQL Server View</span><span class="sxs-lookup"><span data-stu-id="c66d0-219">SQL Server View</span></span></td>
      <td><span data-ttu-id="c66d0-220">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-220">✓</span></span></td>
      <td><span data-ttu-id="c66d0-221">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-221">✓</span></span></td>
      <td><span data-ttu-id="c66d0-222">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-222">✓</span></span></td>
      <td><span data-ttu-id="c66d0-223"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-223"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-224">Teradata Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-224">Teradata Table</span></span></td>
      <td><span data-ttu-id="c66d0-225">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-225">✓</span></span></td>
      <td><span data-ttu-id="c66d0-226">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-226">✓</span></span></td>
      <td><span data-ttu-id="c66d0-227">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-227">✓</span></span></td>
      <td><span data-ttu-id="c66d0-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-229">Teradata View</span><span class="sxs-lookup"><span data-stu-id="c66d0-229">Teradata View</span></span></td>
      <td><span data-ttu-id="c66d0-230">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-230">✓</span></span></td>
      <td><span data-ttu-id="c66d0-231">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-231">✓</span></span></td>
      <td><span data-ttu-id="c66d0-232">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-232">✓</span></span></td>
      <td><span data-ttu-id="c66d0-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-234">SAP Hana View</span><span class="sxs-lookup"><span data-stu-id="c66d0-234">SAP Hana View</span></span></td>
      <td><span data-ttu-id="c66d0-235">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-235">✓</span></span></td>
      <td><span data-ttu-id="c66d0-236">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-236">✓</span></span></td>
      <td><span data-ttu-id="c66d0-237">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-237">✓</span></span></td>
      <td><span data-ttu-id="c66d0-238"><font size=2>PowerBI</font></span><span class="sxs-lookup"><span data-stu-id="c66d0-238"><font size=2>PowerBI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-239">Db2 Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-239">Db2 Table</span></span></td>
      <td><span data-ttu-id="c66d0-240">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-240">✓</span></span></td>
      <td><span data-ttu-id="c66d0-241">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-241">✓</span></span></td>
      <td><span data-ttu-id="c66d0-242">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-243">Db2 View</span><span class="sxs-lookup"><span data-stu-id="c66d0-243">Db2 View</span></span></td>
      <td><span data-ttu-id="c66d0-244">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-244">✓</span></span></td>
      <td><span data-ttu-id="c66d0-245">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-245">✓</span></span></td>
      <td><span data-ttu-id="c66d0-246">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-247">File System File</span><span class="sxs-lookup"><span data-stu-id="c66d0-247">File System File</span></span></td>
      <td><span data-ttu-id="c66d0-248">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-249">Ftp Directory</span><span class="sxs-lookup"><span data-stu-id="c66d0-249">Ftp Directory</span></span></td>
      <td><span data-ttu-id="c66d0-250">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-250">✓</span></span></td>
      <td><span data-ttu-id="c66d0-251">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-251">✓</span></span></td>
      <td><span data-ttu-id="c66d0-252">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-253">Ftp File</span><span class="sxs-lookup"><span data-stu-id="c66d0-253">Ftp File</span></span></td>
      <td><span data-ttu-id="c66d0-254">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-254">✓</span></span></td>
      <td><span data-ttu-id="c66d0-255">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-255">✓</span></span></td>
      <td><span data-ttu-id="c66d0-256">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-257">Http Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-257">Http Report</span></span></td>
      <td><span data-ttu-id="c66d0-258">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-259">Http End Point</span><span class="sxs-lookup"><span data-stu-id="c66d0-259">Http End Point</span></span></td>
      <td><span data-ttu-id="c66d0-260">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-261">Http File</span><span class="sxs-lookup"><span data-stu-id="c66d0-261">Http File</span></span></td>
      <td><span data-ttu-id="c66d0-262">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-263">Odata Entity Set</span><span class="sxs-lookup"><span data-stu-id="c66d0-263">Odata Entity Set</span></span></td>
      <td><span data-ttu-id="c66d0-264">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-265">Odata Function</span><span class="sxs-lookup"><span data-stu-id="c66d0-265">Odata Function</span></span></td>
      <td><span data-ttu-id="c66d0-266">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-267">Postgresql Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-267">Postgresql Table</span></span></td>
      <td><span data-ttu-id="c66d0-268">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-268">✓</span></span></td>
      <td><span data-ttu-id="c66d0-269">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-269">✓</span></span></td>
      <td><span data-ttu-id="c66d0-270">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-271">Postgresql View</span><span class="sxs-lookup"><span data-stu-id="c66d0-271">Postgresql View</span></span></td>
      <td><span data-ttu-id="c66d0-272">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-272">✓</span></span></td>
      <td><span data-ttu-id="c66d0-273">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-273">✓</span></span></td>
      <td><span data-ttu-id="c66d0-274">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-275">SAP Hana View</span><span class="sxs-lookup"><span data-stu-id="c66d0-275">SAP Hana View</span></span></td>
      <td><span data-ttu-id="c66d0-276">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td> <span data-ttu-id="c66d0-277">Salesforce Object</span><span class="sxs-lookup"><span data-stu-id="c66d0-277">Salesforce Object</span></span></td>
      <td><span data-ttu-id="c66d0-278">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-278">✓</span></span></td>
      <td><span data-ttu-id="c66d0-279">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-279">✓</span></span></td>
      <td><span data-ttu-id="c66d0-280">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-281">Sharepoint List</span><span class="sxs-lookup"><span data-stu-id="c66d0-281">Sharepoint List</span></span> </td>
      <td><span data-ttu-id="c66d0-282">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
  
    <tr>
      <td><span data-ttu-id="c66d0-283">Azure DocumentDB Collection</span><span class="sxs-lookup"><span data-stu-id="c66d0-283">Azure DocumentDB Collection</span></span></td>
      <td><span data-ttu-id="c66d0-284">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-284">✓</span></span></td>
      <td><span data-ttu-id="c66d0-285">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-285">✓</span></span></td>
      <td><span data-ttu-id="c66d0-286">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-287">Generic ODBC Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-287">Generic ODBC Table</span></span></td>
      <td><span data-ttu-id="c66d0-288">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-288">✓</span></span></td>
      <td><span data-ttu-id="c66d0-289">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-289">✓</span></span></td>
      <td><span data-ttu-id="c66d0-290">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

    <tr>
      <td><span data-ttu-id="c66d0-291">Generic ODBC View</span><span class="sxs-lookup"><span data-stu-id="c66d0-291">Generic ODBC View</span></span></td>
      <td><span data-ttu-id="c66d0-292">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-292">✓</span></span></td>
      <td><span data-ttu-id="c66d0-293">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-293">✓</span></span></td>
      <td><span data-ttu-id="c66d0-294">✓</span><span class="sxs-lookup"><span data-stu-id="c66d0-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>

</table>

<span data-ttu-id="c66d0-295">If you need support for additional sources, submit a feature request using the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="c66d0-295">If you need support for additional sources, submit a feature request using the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


<br>
<br>
## <a name="data-source-reference-specification"></a><span data-ttu-id="c66d0-296">Data source reference specification</span><span class="sxs-lookup"><span data-stu-id="c66d0-296">Data source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="c66d0-297">"DSL Structure" column in the following table only lists connection properties for "address" property bag that are used by Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="c66d0-297">"DSL Structure" column in the following table only lists connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="c66d0-298">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span><span class="sxs-lookup"><span data-stu-id="c66d0-298">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>
<table>
    <tr>
       <td><span data-ttu-id="c66d0-299"><b>Source Type</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-299"><b>Source Type</b></span></span></td>
       <td><span data-ttu-id="c66d0-300"><b>Asset Type</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-300"><b>Asset Type</b></span></span></td>
       <td><span data-ttu-id="c66d0-301"><b>Object Types</b></span><span class="sxs-lookup"><span data-stu-id="c66d0-301"><b>Object Types</b></span></span></td>
       <td><span data-ttu-id="c66d0-302"><b>DSL Structure<b></span><span class="sxs-lookup"><span data-stu-id="c66d0-302"><b>DSL Structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-303">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c66d0-303">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="c66d0-304">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-304">Container</span></span></td>
      <td><span data-ttu-id="c66d0-305">Data Lake</span><span class="sxs-lookup"><span data-stu-id="c66d0-305">Data Lake</span></span></td>
      <td><span data-ttu-id="c66d0-306">
        <font size=2> protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="c66d0-306">
        <font size=2> protocol: webhdfs</span></span> <br><span data-ttu-id="c66d0-307">authentication: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-307">authentication: {basic, oauth}</span></span> <br><span data-ttu-id="c66d0-308">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-308">address:</span></span> <br><span data-ttu-id="c66d0-309">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-309">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-310">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c66d0-310">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="c66d0-311">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-311">Table</span></span></td>
      <td><span data-ttu-id="c66d0-312">Directory, File</span><span class="sxs-lookup"><span data-stu-id="c66d0-312">Directory, File</span></span></td>
      <td><span data-ttu-id="c66d0-313">
        <font size=2> protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="c66d0-313">
        <font size=2> protocol: webhdfs</span></span> <br><span data-ttu-id="c66d0-314">authentication: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-314">authentication: {basic, oauth}</span></span> <br><span data-ttu-id="c66d0-315">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-315">address:</span></span> <br><span data-ttu-id="c66d0-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-317">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c66d0-317">Azure Storage</span></span></td>
      <td><span data-ttu-id="c66d0-318">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-318">Container</span></span></td>
      <td><span data-ttu-id="c66d0-319">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-319">Container</span></span></td>
      <td><span data-ttu-id="c66d0-320">
        <font size=2> protocol: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="c66d0-320">
        <font size=2> protocol: azure-blobs</span></span> <br><span data-ttu-id="c66d0-321">authentication: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="c66d0-321">authentication: {azure-access-key}</span></span> <br><span data-ttu-id="c66d0-322">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-322">address:</span></span> <br><span data-ttu-id="c66d0-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="c66d0-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="c66d0-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="c66d0-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="c66d0-325">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-325">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-326">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c66d0-326">Azure Storage</span></span></td>
      <td><span data-ttu-id="c66d0-327">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-327">Table</span></span></td>
      <td><span data-ttu-id="c66d0-328">Blob, Directory</span><span class="sxs-lookup"><span data-stu-id="c66d0-328">Blob, Directory</span></span></td>
      <td><span data-ttu-id="c66d0-329">
        <font size=2> protocol: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="c66d0-329">
        <font size=2> protocol: azure-blobs</span></span> <br><span data-ttu-id="c66d0-330">authentication: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="c66d0-330">authentication: {azure-access-key}</span></span> <br><span data-ttu-id="c66d0-331">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-331">address:</span></span> <br><span data-ttu-id="c66d0-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="c66d0-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="c66d0-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="c66d0-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="c66d0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span><span class="sxs-lookup"><span data-stu-id="c66d0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="c66d0-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-336">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c66d0-336">Azure Storage</span></span></td>
      <td><span data-ttu-id="c66d0-337">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-337">Container</span></span></td>
      <td><span data-ttu-id="c66d0-338">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-338">Container</span></span></td>
      <td><span data-ttu-id="c66d0-339">
        <font size=2> protocol: azure-tables</span><span class="sxs-lookup"><span data-stu-id="c66d0-339">
        <font size=2> protocol: azure-tables</span></span> <br><span data-ttu-id="c66d0-340">authentication: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="c66d0-340">authentication: {azure-access-key}</span></span> <br><span data-ttu-id="c66d0-341">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-341">address:</span></span> <br><span data-ttu-id="c66d0-342">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="c66d0-342">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="c66d0-343">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-343">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-344">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c66d0-344">Azure Storage</span></span></td>
      <td><span data-ttu-id="c66d0-345">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-345">Table</span></span></td>
      <td><span data-ttu-id="c66d0-346">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-346">Table</span></span></td>
      <td><span data-ttu-id="c66d0-347">
        <font size=2> protocol: azure-tables</span><span class="sxs-lookup"><span data-stu-id="c66d0-347">
        <font size=2> protocol: azure-tables</span></span> <br><span data-ttu-id="c66d0-348">authentication: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="c66d0-348">authentication: {azure-access-key}</span></span> <br><span data-ttu-id="c66d0-349">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-349">address:</span></span> <br><span data-ttu-id="c66d0-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="c66d0-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="c66d0-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="c66d0-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="c66d0-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-353">Cosmos</span><span class="sxs-lookup"><span data-stu-id="c66d0-353">Cosmos</span></span></td>
      <td><span data-ttu-id="c66d0-354">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-354">Container</span></span></td>
      <td><span data-ttu-id="c66d0-355">Virtual Cluster</span><span class="sxs-lookup"><span data-stu-id="c66d0-355">Virtual Cluster</span></span></td>
      <td><span data-ttu-id="c66d0-356">
        <font size=2> protocol: cosmos</span><span class="sxs-lookup"><span data-stu-id="c66d0-356">
        <font size=2> protocol: cosmos</span></span> <br><span data-ttu-id="c66d0-357">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-357">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-358">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-358">address:</span></span> <br><span data-ttu-id="c66d0-359">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-359">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-360">Cosmos</span><span class="sxs-lookup"><span data-stu-id="c66d0-360">Cosmos</span></span></td>
      <td><span data-ttu-id="c66d0-361">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-361">Table</span></span></td>
      <td><span data-ttu-id="c66d0-362">Stream, Stream Set, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-362">Stream, Stream Set, View</span></span></td>
      <td><span data-ttu-id="c66d0-363">
        <font size=2> protocol: cosmos</span><span class="sxs-lookup"><span data-stu-id="c66d0-363">
        <font size=2> protocol: cosmos</span></span> <br><span data-ttu-id="c66d0-364">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-364">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-365">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-365">address:</span></span> <br><span data-ttu-id="c66d0-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-367">DataZen</span><span class="sxs-lookup"><span data-stu-id="c66d0-367">DataZen</span></span></td>
      <td><span data-ttu-id="c66d0-368">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-368">Container</span></span></td>
      <td><span data-ttu-id="c66d0-369">Site</span><span class="sxs-lookup"><span data-stu-id="c66d0-369">Site</span></span></td>
      <td><span data-ttu-id="c66d0-370">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-370">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-371">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-371">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-372">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-372">address:</span></span> <br><span data-ttu-id="c66d0-373">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-373">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-374">DataZen</span><span class="sxs-lookup"><span data-stu-id="c66d0-374">DataZen</span></span></td>
      <td><span data-ttu-id="c66d0-375">Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-375">Report</span></span></td>
      <td><span data-ttu-id="c66d0-376">Report, Dashboard</span><span class="sxs-lookup"><span data-stu-id="c66d0-376">Report, Dashboard</span></span></td>
      <td><span data-ttu-id="c66d0-377">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-377">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-378">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-378">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-379">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-379">address:</span></span> <br><span data-ttu-id="c66d0-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-381">Db2</span><span class="sxs-lookup"><span data-stu-id="c66d0-381">Db2</span></span></td>
      <td><span data-ttu-id="c66d0-382">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-382">Container</span></span></td>
      <td><span data-ttu-id="c66d0-383">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-383">Database</span></span></td>
      <td><span data-ttu-id="c66d0-384">
        <font size=2> protocol: db2</span><span class="sxs-lookup"><span data-stu-id="c66d0-384">
        <font size=2> protocol: db2</span></span> <br><span data-ttu-id="c66d0-385">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-385">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-386">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-386">address:</span></span> <br><span data-ttu-id="c66d0-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-388">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-388">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-389">Db2</span><span class="sxs-lookup"><span data-stu-id="c66d0-389">Db2</span></span></td>
      <td><span data-ttu-id="c66d0-390">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-390">Table</span></span></td>
      <td><span data-ttu-id="c66d0-391">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-391">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-392">
        <font size=2> protocol: db2</span><span class="sxs-lookup"><span data-stu-id="c66d0-392">
        <font size=2> protocol: db2</span></span> <br><span data-ttu-id="c66d0-393">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-393">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-394">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-394">address:</span></span> <br><span data-ttu-id="c66d0-395">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-395">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-396">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-396">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-397">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-397">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-398">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-398">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-399">File System</span><span class="sxs-lookup"><span data-stu-id="c66d0-399">File System</span></span></td>
      <td><span data-ttu-id="c66d0-400">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-400">Table</span></span></td>
      <td><span data-ttu-id="c66d0-401">File</span><span class="sxs-lookup"><span data-stu-id="c66d0-401">File</span></span></td>
      <td><span data-ttu-id="c66d0-402">
        <font size=2> protocol: file</span><span class="sxs-lookup"><span data-stu-id="c66d0-402">
        <font size=2> protocol: file</span></span> <br><span data-ttu-id="c66d0-403">authentication: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-403">authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="c66d0-404">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-404">address:</span></span> <br><span data-ttu-id="c66d0-405">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-405">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-406">Ftp</span><span class="sxs-lookup"><span data-stu-id="c66d0-406">Ftp</span></span></td>
      <td><span data-ttu-id="c66d0-407">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-407">Table</span></span></td>
      <td><span data-ttu-id="c66d0-408">Directory, File</span><span class="sxs-lookup"><span data-stu-id="c66d0-408">Directory, File</span></span></td>
      <td><span data-ttu-id="c66d0-409">
        <font size=2> protocol: ftp</span><span class="sxs-lookup"><span data-stu-id="c66d0-409">
        <font size=2> protocol: ftp</span></span> <br><span data-ttu-id="c66d0-410">authentication: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-410">authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="c66d0-411">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-411">address:</span></span> <br><span data-ttu-id="c66d0-412">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-412">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-413">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="c66d0-413">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="c66d0-414">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-414">Container</span></span></td>
      <td><span data-ttu-id="c66d0-415">Cluster</span><span class="sxs-lookup"><span data-stu-id="c66d0-415">Cluster</span></span></td>
      <td><span data-ttu-id="c66d0-416">
        <font size=2> protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="c66d0-416">
        <font size=2> protocol: webhdfs</span></span> <br><span data-ttu-id="c66d0-417">authentication: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-417">authentication: {basic, oauth}</span></span> <br><span data-ttu-id="c66d0-418">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-418">address:</span></span> <br><span data-ttu-id="c66d0-419">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-419">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-420">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="c66d0-420">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="c66d0-421">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-421">Table</span></span></td>
      <td><span data-ttu-id="c66d0-422">Directory, File</span><span class="sxs-lookup"><span data-stu-id="c66d0-422">Directory, File</span></span></td>
      <td><span data-ttu-id="c66d0-423">
        <font size=2> protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="c66d0-423">
        <font size=2> protocol: webhdfs</span></span> <br><span data-ttu-id="c66d0-424">authentication: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-424">authentication: {basic, oauth}</span></span> <br><span data-ttu-id="c66d0-425">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-425">address:</span></span> <br><span data-ttu-id="c66d0-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-427">Hive</span><span class="sxs-lookup"><span data-stu-id="c66d0-427">Hive</span></span></td>
      <td><span data-ttu-id="c66d0-428">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-428">Container</span></span></td>
      <td><span data-ttu-id="c66d0-429">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-429">Database</span></span></td>
      <td><span data-ttu-id="c66d0-430">
        <font size=2> protocol: hive</span><span class="sxs-lookup"><span data-stu-id="c66d0-430">
        <font size=2> protocol: hive</span></span> <br><span data-ttu-id="c66d0-431">authentication: {hdinsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-431">authentication: {hdinsight, basic, username, none}</span></span> <br><span data-ttu-id="c66d0-432">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-432">address:</span></span> <br><span data-ttu-id="c66d0-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-434">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-434">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-435">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="c66d0-435">connectionProperties:</span></span> <br><span data-ttu-id="c66d0-436">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-436">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-437">Hive</span><span class="sxs-lookup"><span data-stu-id="c66d0-437">Hive</span></span></td>
      <td><span data-ttu-id="c66d0-438">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-438">Table</span></span></td>
      <td><span data-ttu-id="c66d0-439">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-439">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-440">
        <font size=2> protocol: hive</span><span class="sxs-lookup"><span data-stu-id="c66d0-440">
        <font size=2> protocol: hive</span></span> <br><span data-ttu-id="c66d0-441">authentication: {hdinsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-441">authentication: {hdinsight, basic, username, none}</span></span> <br><span data-ttu-id="c66d0-442">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-442">address:</span></span> <br><span data-ttu-id="c66d0-443">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-443">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-444">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-444">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-445">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-445">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-446">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="c66d0-446">connectionProperties:</span></span> <br><span data-ttu-id="c66d0-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-448">Http</span><span class="sxs-lookup"><span data-stu-id="c66d0-448">Http</span></span></td>
      <td><span data-ttu-id="c66d0-449">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-449">Container</span></span></td>
      <td><span data-ttu-id="c66d0-450">Site</span><span class="sxs-lookup"><span data-stu-id="c66d0-450">Site</span></span></td>
      <td><span data-ttu-id="c66d0-451">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-451">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-452">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-452">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-453">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-453">address:</span></span> <br><span data-ttu-id="c66d0-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-455">Http</span><span class="sxs-lookup"><span data-stu-id="c66d0-455">Http</span></span></td>
      <td><span data-ttu-id="c66d0-456">Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-456">Report</span></span></td>
      <td><span data-ttu-id="c66d0-457">Report, Dashboard</span><span class="sxs-lookup"><span data-stu-id="c66d0-457">Report, Dashboard</span></span></td>
      <td><span data-ttu-id="c66d0-458">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-458">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-459">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-459">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-460">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-460">address:</span></span> <br><span data-ttu-id="c66d0-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-462">Http</span><span class="sxs-lookup"><span data-stu-id="c66d0-462">Http</span></span></td>
      <td><span data-ttu-id="c66d0-463">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-463">Table</span></span></td>
      <td><span data-ttu-id="c66d0-464">End Point, File</span><span class="sxs-lookup"><span data-stu-id="c66d0-464">End Point, File</span></span></td>
      <td><span data-ttu-id="c66d0-465">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-465">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-466">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-466">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-467">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-467">address:</span></span> <br><span data-ttu-id="c66d0-468">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-468">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-469">MySQL</span><span class="sxs-lookup"><span data-stu-id="c66d0-469">MySQL</span></span></td>
      <td><span data-ttu-id="c66d0-470">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-470">Container</span></span></td>
      <td><span data-ttu-id="c66d0-471">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-471">Database</span></span></td>
      <td><span data-ttu-id="c66d0-472">
        <font size=2> protocol: mysql</span><span class="sxs-lookup"><span data-stu-id="c66d0-472">
        <font size=2> protocol: mysql</span></span> <br><span data-ttu-id="c66d0-473">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-473">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-474">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-474">address:</span></span> <br><span data-ttu-id="c66d0-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-476">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-476">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-477">MySQL</span><span class="sxs-lookup"><span data-stu-id="c66d0-477">MySQL</span></span></td>
      <td><span data-ttu-id="c66d0-478">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-478">Table</span></span></td>
      <td><span data-ttu-id="c66d0-479">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-479">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-480">
        <font size=2> protocol: mysql</span><span class="sxs-lookup"><span data-stu-id="c66d0-480">
        <font size=2> protocol: mysql</span></span> <br><span data-ttu-id="c66d0-481">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-481">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-482">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-482">address:</span></span> <br><span data-ttu-id="c66d0-483">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-483">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-484">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-484">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-485">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-485">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-486">Odata</span><span class="sxs-lookup"><span data-stu-id="c66d0-486">Odata</span></span></td>
      <td><span data-ttu-id="c66d0-487">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-487">Container</span></span></td>
      <td><span data-ttu-id="c66d0-488">Entity Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-488">Entity Container</span></span></td>
      <td><span data-ttu-id="c66d0-489">
        <font size=2> protocol: odata</span><span class="sxs-lookup"><span data-stu-id="c66d0-489">
        <font size=2> protocol: odata</span></span> <br><span data-ttu-id="c66d0-490">authentication: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-490">authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="c66d0-491">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-491">address:</span></span> <br><span data-ttu-id="c66d0-492">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-492">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-493">Odata</span><span class="sxs-lookup"><span data-stu-id="c66d0-493">Odata</span></span></td>
      <td><span data-ttu-id="c66d0-494">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-494">Table</span></span></td>
      <td><span data-ttu-id="c66d0-495">Entity Set, Function</span><span class="sxs-lookup"><span data-stu-id="c66d0-495">Entity Set, Function</span></span></td>
      <td><span data-ttu-id="c66d0-496">
        <font size=2> protocol: odata</span><span class="sxs-lookup"><span data-stu-id="c66d0-496">
        <font size=2> protocol: odata</span></span> <br><span data-ttu-id="c66d0-497">authentication: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-497">authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="c66d0-498">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-498">address:</span></span> <br><span data-ttu-id="c66d0-499">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="c66d0-499">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="c66d0-500">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-500">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-501">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-501">Oracle Database</span></span></td>
      <td><span data-ttu-id="c66d0-502">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-502">Container</span></span></td>
      <td><span data-ttu-id="c66d0-503">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-503">Database</span></span></td>
      <td><span data-ttu-id="c66d0-504">
        <font size=2> protocol: oracle</span><span class="sxs-lookup"><span data-stu-id="c66d0-504">
        <font size=2> protocol: oracle</span></span> <br><span data-ttu-id="c66d0-505">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-505">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-506">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-506">address:</span></span> <br><span data-ttu-id="c66d0-507">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-507">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-508">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-508">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-509">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-509">Oracle Database</span></span></td>
      <td><span data-ttu-id="c66d0-510">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-510">Table</span></span></td>
      <td><span data-ttu-id="c66d0-511">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-511">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-512">
        <font size=2> protocol: oracle</span><span class="sxs-lookup"><span data-stu-id="c66d0-512">
        <font size=2> protocol: oracle</span></span> <br><span data-ttu-id="c66d0-513">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-513">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-514">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-514">address:</span></span> <br><span data-ttu-id="c66d0-515">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-515">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-516">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-516">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-517">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-517">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-518">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-518">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-519">Postgresql</span><span class="sxs-lookup"><span data-stu-id="c66d0-519">Postgresql</span></span></td>
      <td><span data-ttu-id="c66d0-520">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-520">Container</span></span></td>
      <td><span data-ttu-id="c66d0-521">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-521">Database</span></span></td>
      <td><span data-ttu-id="c66d0-522">
        <font size=2> protocol: postgresql</span><span class="sxs-lookup"><span data-stu-id="c66d0-522">
        <font size=2> protocol: postgresql</span></span> <br><span data-ttu-id="c66d0-523">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-523">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-524">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-524">address:</span></span> <br><span data-ttu-id="c66d0-525">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-525">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-526">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-526">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-527">Postgresql</span><span class="sxs-lookup"><span data-stu-id="c66d0-527">Postgresql</span></span></td>
      <td><span data-ttu-id="c66d0-528">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-528">Table</span></span></td>
      <td><span data-ttu-id="c66d0-529">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-529">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-530">
        <font size=2> protocol: postgresql</span><span class="sxs-lookup"><span data-stu-id="c66d0-530">
        <font size=2> protocol: postgresql</span></span> <br><span data-ttu-id="c66d0-531">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-531">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-532">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-532">address:</span></span> <br><span data-ttu-id="c66d0-533">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-533">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-534">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-534">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-537">Power BI</span><span class="sxs-lookup"><span data-stu-id="c66d0-537">Power BI</span></span></td>
      <td><span data-ttu-id="c66d0-538">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-538">Container</span></span></td>
      <td><span data-ttu-id="c66d0-539">Site</span><span class="sxs-lookup"><span data-stu-id="c66d0-539">Site</span></span></td>
      <td><span data-ttu-id="c66d0-540">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-540">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-541">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-541">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-542">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-542">address:</span></span> <br><span data-ttu-id="c66d0-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-544">Power BI</span><span class="sxs-lookup"><span data-stu-id="c66d0-544">Power BI</span></span></td>
      <td><span data-ttu-id="c66d0-545">Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-545">Report</span></span></td>
      <td><span data-ttu-id="c66d0-546">Report, Dashboard</span><span class="sxs-lookup"><span data-stu-id="c66d0-546">Report, Dashboard</span></span></td>
      <td><span data-ttu-id="c66d0-547">
        <font size=2> protocol: http</span><span class="sxs-lookup"><span data-stu-id="c66d0-547">
        <font size=2> protocol: http</span></span> <br><span data-ttu-id="c66d0-548">authentication: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-548">authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="c66d0-549">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-549">address:</span></span> <br><span data-ttu-id="c66d0-550">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-550">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-551">Power Query</span><span class="sxs-lookup"><span data-stu-id="c66d0-551">Power Query</span></span></td>
      <td><span data-ttu-id="c66d0-552">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-552">Table</span></span></td>
      <td><span data-ttu-id="c66d0-553">Data Mashup</span><span class="sxs-lookup"><span data-stu-id="c66d0-553">Data Mashup</span></span></td>
      <td><span data-ttu-id="c66d0-554">
        <font size=2> protocol: power-query</span><span class="sxs-lookup"><span data-stu-id="c66d0-554">
        <font size=2> protocol: power-query</span></span> <br><span data-ttu-id="c66d0-555">authentication: {oauth}</span><span class="sxs-lookup"><span data-stu-id="c66d0-555">authentication: {oauth}</span></span> <br><span data-ttu-id="c66d0-556">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-556">address:</span></span> <br><span data-ttu-id="c66d0-557">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-557">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-558">Salesforce</span><span class="sxs-lookup"><span data-stu-id="c66d0-558">Salesforce</span></span></td>
      <td><span data-ttu-id="c66d0-559">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-559">Table</span></span></td>
      <td><span data-ttu-id="c66d0-560">Object</span><span class="sxs-lookup"><span data-stu-id="c66d0-560">Object</span></span></td>
      <td><span data-ttu-id="c66d0-561">
        <font size=2> protocol: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="c66d0-561">
        <font size=2> protocol: salesforce-com</span></span> <br><span data-ttu-id="c66d0-562">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-562">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-563">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-563">address:</span></span> <br><span data-ttu-id="c66d0-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="c66d0-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="c66d0-565">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="c66d0-565">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="c66d0-566">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-566">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-567">SAP Hana</span><span class="sxs-lookup"><span data-stu-id="c66d0-567">SAP Hana</span></span></td>
      <td><span data-ttu-id="c66d0-568">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-568">Container</span></span></td>
      <td><span data-ttu-id="c66d0-569">Server</span><span class="sxs-lookup"><span data-stu-id="c66d0-569">Server</span></span></td>
      <td><span data-ttu-id="c66d0-570">
        <font size=2> protocol: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="c66d0-570">
        <font size=2> protocol: sap-hana-sql</span></span> <br><span data-ttu-id="c66d0-571">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-571">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-572">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-572">address:</span></span> <br><span data-ttu-id="c66d0-573">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-573">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-574">SAP Hana</span><span class="sxs-lookup"><span data-stu-id="c66d0-574">SAP Hana</span></span></td>
      <td><span data-ttu-id="c66d0-575">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-575">Table</span></span></td>
      <td><span data-ttu-id="c66d0-576">View</span><span class="sxs-lookup"><span data-stu-id="c66d0-576">View</span></span></td>
      <td><span data-ttu-id="c66d0-577">
        <font size=2> protocol: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="c66d0-577">
        <font size=2> protocol: sap-hana-sql</span></span> <br><span data-ttu-id="c66d0-578">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-578">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-579">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-579">address:</span></span> <br><span data-ttu-id="c66d0-580">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-580">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-581">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-581">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-582">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-582">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-583">SharePoint</span><span class="sxs-lookup"><span data-stu-id="c66d0-583">SharePoint</span></span></td>
      <td><span data-ttu-id="c66d0-584">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-584">Table</span></span></td>
      <td><span data-ttu-id="c66d0-585">List</span><span class="sxs-lookup"><span data-stu-id="c66d0-585">List</span></span></td>
      <td><span data-ttu-id="c66d0-586">
        <font size=2> protocol: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="c66d0-586">
        <font size=2> protocol: sharepoint-list</span></span> <br><span data-ttu-id="c66d0-587">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-587">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-588">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-588">address:</span></span> <br><span data-ttu-id="c66d0-589">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-589">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-590">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c66d0-590">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="c66d0-591">Command</span><span class="sxs-lookup"><span data-stu-id="c66d0-591">Command</span></span></td>
      <td><span data-ttu-id="c66d0-592">Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="c66d0-592">Stored Procedure</span></span></td>
      <td><span data-ttu-id="c66d0-593">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-593">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-594">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-594">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-595">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-595">address:</span></span> <br><span data-ttu-id="c66d0-596">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-596">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-597">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-597">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-598">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-598">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-599">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-599">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-600">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c66d0-600">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="c66d0-601">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="c66d0-601">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="c66d0-602">Table-valued Function</span><span class="sxs-lookup"><span data-stu-id="c66d0-602">Table-valued Function</span></span></td>
      <td><span data-ttu-id="c66d0-603">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-603">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-604">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-604">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-605">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-605">address:</span></span> <br><span data-ttu-id="c66d0-606">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-606">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-607">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-607">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-610">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c66d0-610">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="c66d0-611">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-611">Container</span></span></td>
      <td><span data-ttu-id="c66d0-612">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-612">Database</span></span></td>
      <td><span data-ttu-id="c66d0-613">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-613">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-614">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-614">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-615">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-615">address:</span></span> <br><span data-ttu-id="c66d0-616">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-616">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-618">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c66d0-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="c66d0-619">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-619">Table</span></span></td>
      <td><span data-ttu-id="c66d0-620">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-620">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-621">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-621">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-622">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-622">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-623">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-623">address:</span></span> <br><span data-ttu-id="c66d0-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-628">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c66d0-628">SQL Server</span></span></td>
      <td><span data-ttu-id="c66d0-629">Command</span><span class="sxs-lookup"><span data-stu-id="c66d0-629">Command</span></span></td>
      <td><span data-ttu-id="c66d0-630">Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="c66d0-630">Stored Procedure</span></span></td>
      <td><span data-ttu-id="c66d0-631">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-631">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-632">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-632">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-633">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-633">address:</span></span> <br><span data-ttu-id="c66d0-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-638">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c66d0-638">SQL Server</span></span></td>
      <td><span data-ttu-id="c66d0-639">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="c66d0-639">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="c66d0-640">Table-valued Function</span><span class="sxs-lookup"><span data-stu-id="c66d0-640">Table-valued Function</span></span></td>
      <td><span data-ttu-id="c66d0-641">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-641">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-642">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-642">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-643">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-643">address:</span></span> <br><span data-ttu-id="c66d0-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-646">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-646">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-647">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-647">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-648">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c66d0-648">SQL Server</span></span></td>
      <td><span data-ttu-id="c66d0-649">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-649">Container</span></span></td>
      <td><span data-ttu-id="c66d0-650">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-650">Database</span></span></td>
      <td><span data-ttu-id="c66d0-651">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-651">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-652">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-652">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-653">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-653">address:</span></span> <br><span data-ttu-id="c66d0-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c66d0-656">SQL Server</span></span></td>
      <td><span data-ttu-id="c66d0-657">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-657">Table</span></span></td>
      <td><span data-ttu-id="c66d0-658">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-658">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-659">
        <font size=2> protocol: tds</span><span class="sxs-lookup"><span data-stu-id="c66d0-659">
        <font size=2> protocol: tds</span></span> <br><span data-ttu-id="c66d0-660">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-660">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-661">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-661">address:</span></span> <br><span data-ttu-id="c66d0-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="c66d0-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="c66d0-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-666">SQL Server Analysis Services Multidimensional</span><span class="sxs-lookup"><span data-stu-id="c66d0-666">SQL Server Analysis Services Multidimensional</span></span></td>
      <td><span data-ttu-id="c66d0-667">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-667">Container</span></span></td>
      <td><span data-ttu-id="c66d0-668">Model</span><span class="sxs-lookup"><span data-stu-id="c66d0-668">Model</span></span></td>
      <td><span data-ttu-id="c66d0-669">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-669">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-670">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-670">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-671">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-671">address:</span></span> <br><span data-ttu-id="c66d0-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-675">SQL Server Analysis Services Multidimensional</span><span class="sxs-lookup"><span data-stu-id="c66d0-675">SQL Server Analysis Services Multidimensional</span></span></td>
      <td><span data-ttu-id="c66d0-676">KPI</span><span class="sxs-lookup"><span data-stu-id="c66d0-676">KPI</span></span></td>
      <td><span data-ttu-id="c66d0-677">KPI</span><span class="sxs-lookup"><span data-stu-id="c66d0-677">KPI</span></span></td>
      <td><span data-ttu-id="c66d0-678">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-678">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-679">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-679">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-680">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-680">address:</span></span> <br><span data-ttu-id="c66d0-681">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-681">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-684">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-684">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-685">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-685">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-686">SQL Server Analysis Services Multidimensional</span><span class="sxs-lookup"><span data-stu-id="c66d0-686">SQL Server Analysis Services Multidimensional</span></span></td>
      <td><span data-ttu-id="c66d0-687">Measure</span><span class="sxs-lookup"><span data-stu-id="c66d0-687">Measure</span></span></td>
      <td><span data-ttu-id="c66d0-688">Measure</span><span class="sxs-lookup"><span data-stu-id="c66d0-688">Measure</span></span></td>
      <td><span data-ttu-id="c66d0-689">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-689">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-690">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-690">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-691">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-691">address:</span></span> <br><span data-ttu-id="c66d0-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-694">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-694">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-695">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-695">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-696">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-696">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-697">SQL Server Analysis Services Multidimensional</span><span class="sxs-lookup"><span data-stu-id="c66d0-697">SQL Server Analysis Services Multidimensional</span></span></td>
      <td><span data-ttu-id="c66d0-698">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-698">Table</span></span></td>
      <td><span data-ttu-id="c66d0-699">Dimension</span><span class="sxs-lookup"><span data-stu-id="c66d0-699">Dimension</span></span></td>
      <td><span data-ttu-id="c66d0-700">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-700">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-701">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-701">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-702">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-702">address:</span></span> <br><span data-ttu-id="c66d0-703">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-703">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-704">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-704">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-705">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-705">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-706">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-706">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-707">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-707">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-708">SQL Server Analysis Services Tabular</span><span class="sxs-lookup"><span data-stu-id="c66d0-708">SQL Server Analysis Services Tabular</span></span></td>
      <td><span data-ttu-id="c66d0-709">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-709">Container</span></span></td>
      <td><span data-ttu-id="c66d0-710">Model</span><span class="sxs-lookup"><span data-stu-id="c66d0-710">Model</span></span></td>
      <td><span data-ttu-id="c66d0-711">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-711">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-712">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-712">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-713">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-713">address:</span></span> <br><span data-ttu-id="c66d0-714">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-714">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-715">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-715">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-716">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-716">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-717">SQL Server Analysis Services Tabular</span><span class="sxs-lookup"><span data-stu-id="c66d0-717">SQL Server Analysis Services Tabular</span></span></td>
      <td><span data-ttu-id="c66d0-718">KPI</span><span class="sxs-lookup"><span data-stu-id="c66d0-718">KPI</span></span></td>
      <td><span data-ttu-id="c66d0-719">KPI</span><span class="sxs-lookup"><span data-stu-id="c66d0-719">KPI</span></span></td>
      <td><span data-ttu-id="c66d0-720">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-720">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-721">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-721">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-722">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-722">address:</span></span> <br><span data-ttu-id="c66d0-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-725">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-725">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-726">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-726">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-727">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-727">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-728">SQL Server Analysis Services Tabular</span><span class="sxs-lookup"><span data-stu-id="c66d0-728">SQL Server Analysis Services Tabular</span></span></td>
      <td><span data-ttu-id="c66d0-729">Measure</span><span class="sxs-lookup"><span data-stu-id="c66d0-729">Measure</span></span></td>
      <td><span data-ttu-id="c66d0-730">Measure</span><span class="sxs-lookup"><span data-stu-id="c66d0-730">Measure</span></span></td>
      <td><span data-ttu-id="c66d0-731">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-731">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-732">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-732">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-733">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-733">address:</span></span> <br><span data-ttu-id="c66d0-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-736">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-736">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-737">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-737">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-738">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-738">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-739">SQL Server Analysis Services Tabular</span><span class="sxs-lookup"><span data-stu-id="c66d0-739">SQL Server Analysis Services Tabular</span></span></td>
      <td><span data-ttu-id="c66d0-740">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-740">Table</span></span></td>
      <td><span data-ttu-id="c66d0-741">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-741">Table</span></span></td>
      <td><span data-ttu-id="c66d0-742">
        <font size=2> protocol: analysis-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-742">
        <font size=2> protocol: analysis-services</span></span> <br><span data-ttu-id="c66d0-743">authentication: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="c66d0-743">authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="c66d0-744">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-744">address:</span></span> <br><span data-ttu-id="c66d0-745">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-745">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-746">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-746">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-747">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-747">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-748">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-748">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-749">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-749">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-750">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="c66d0-750">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="c66d0-751">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-751">Container</span></span></td>
      <td><span data-ttu-id="c66d0-752">Server</span><span class="sxs-lookup"><span data-stu-id="c66d0-752">Server</span></span></td>
      <td><span data-ttu-id="c66d0-753">
        <font size=2> protocol: reporting-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-753">
        <font size=2> protocol: reporting-services</span></span> <br><span data-ttu-id="c66d0-754">authentication: {windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-754">authentication: {windows}</span></span> <br><span data-ttu-id="c66d0-755">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-755">address:</span></span> <br><span data-ttu-id="c66d0-756">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-756">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-757">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-757">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-758">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="c66d0-758">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="c66d0-759">Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-759">Report</span></span></td>
      <td><span data-ttu-id="c66d0-760">Report</span><span class="sxs-lookup"><span data-stu-id="c66d0-760">Report</span></span></td>
      <td><span data-ttu-id="c66d0-761">
        <font size=2> protocol: reporting-services</span><span class="sxs-lookup"><span data-stu-id="c66d0-761">
        <font size=2> protocol: reporting-services</span></span> <br><span data-ttu-id="c66d0-762">authentication: {windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-762">authentication: {windows}</span></span> <br><span data-ttu-id="c66d0-763">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-763">address:</span></span> <br><span data-ttu-id="c66d0-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span><span class="sxs-lookup"><span data-stu-id="c66d0-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="c66d0-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-767">Teradata</span><span class="sxs-lookup"><span data-stu-id="c66d0-767">Teradata</span></span></td>
      <td><span data-ttu-id="c66d0-768">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-768">Container</span></span></td>
      <td><span data-ttu-id="c66d0-769">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-769">Database</span></span></td>
      <td><span data-ttu-id="c66d0-770">
        <font size=2> protocol: teradata</span><span class="sxs-lookup"><span data-stu-id="c66d0-770">
        <font size=2> protocol: teradata</span></span> <br><span data-ttu-id="c66d0-771">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-771">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-772">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-772">address:</span></span> <br><span data-ttu-id="c66d0-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-775">Teradata</span><span class="sxs-lookup"><span data-stu-id="c66d0-775">Teradata</span></span></td>
      <td><span data-ttu-id="c66d0-776">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-776">Table</span></span></td>
      <td><span data-ttu-id="c66d0-777">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-777">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-778">
        <font size=2> protocol: teradata</span><span class="sxs-lookup"><span data-stu-id="c66d0-778">
        <font size=2> protocol: teradata</span></span> <br><span data-ttu-id="c66d0-779">authentication: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-779">authentication: {protocol, windows}</span></span> <br><span data-ttu-id="c66d0-780">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-780">address:</span></span> <br><span data-ttu-id="c66d0-781">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="c66d0-781">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="c66d0-782">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-782">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-783">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-783">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-784">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="c66d0-784">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="c66d0-785">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-785">Container</span></span></td>
      <td><span data-ttu-id="c66d0-786">Model</span><span class="sxs-lookup"><span data-stu-id="c66d0-786">Model</span></span></td>
      <td><span data-ttu-id="c66d0-787">
        <font size="2"> protocol: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="c66d0-787">
        <font size="2"> protocol: mssql-mds</span></span> <br><span data-ttu-id="c66d0-788">authentication: {windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-788">authentication: {windows}</span></span> <br><span data-ttu-id="c66d0-789">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-789">address:</span></span> <br><span data-ttu-id="c66d0-790">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="c66d0-790">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="c66d0-791">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-791">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-793">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="c66d0-793">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="c66d0-794">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-794">Table</span></span></td>
      <td><span data-ttu-id="c66d0-795">Entity</span><span class="sxs-lookup"><span data-stu-id="c66d0-795">Entity</span></span></td>
      <td><span data-ttu-id="c66d0-796">
        <font size="2"> protocol: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="c66d0-796">
        <font size="2"> protocol: mssql-mds</span></span> <br><span data-ttu-id="c66d0-797">authentication: {windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-797">authentication: {windows}</span></span> <br><span data-ttu-id="c66d0-798">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-798">address:</span></span> <br><span data-ttu-id="c66d0-799">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="c66d0-799">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="c66d0-800">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="c66d0-800">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="c66d0-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span><span class="sxs-lookup"><span data-stu-id="c66d0-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="c66d0-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-803">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c66d0-803">Azure DocumentDB</span></span></td>
      <td><span data-ttu-id="c66d0-804">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-804">Container</span></span></td>
      <td><span data-ttu-id="c66d0-805">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-805">Database</span></span></td>
      <td><span data-ttu-id="c66d0-806">
        <font size=2> protocol: document-db</span><span class="sxs-lookup"><span data-stu-id="c66d0-806">
        <font size=2> protocol: document-db</span></span> <br><span data-ttu-id="c66d0-807">authentication: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="c66d0-807">authentication: {azure-access-key}</span></span> <br><span data-ttu-id="c66d0-808">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-808">address:</span></span> <br><span data-ttu-id="c66d0-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="c66d0-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="c66d0-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-811">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c66d0-811">Azure DocumentDB</span></span></td>
      <td><span data-ttu-id="c66d0-812">Collection</span><span class="sxs-lookup"><span data-stu-id="c66d0-812">Collection</span></span></td>
      <td><span data-ttu-id="c66d0-813">Collection</span><span class="sxs-lookup"><span data-stu-id="c66d0-813">Collection</span></span></td>
      <td><span data-ttu-id="c66d0-814">
        <font size=2> protocol: document-db</span><span class="sxs-lookup"><span data-stu-id="c66d0-814">
        <font size=2> protocol: document-db</span></span> <br><span data-ttu-id="c66d0-815">authentication: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="c66d0-815">authentication: {azure-access-key}</span></span> <br><span data-ttu-id="c66d0-816">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-816">address:</span></span> <br><span data-ttu-id="c66d0-817">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="c66d0-817">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="c66d0-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-820">Generic ODBC</span><span class="sxs-lookup"><span data-stu-id="c66d0-820">Generic ODBC</span></span></td>
      <td><span data-ttu-id="c66d0-821">Container</span><span class="sxs-lookup"><span data-stu-id="c66d0-821">Container</span></span></td>
      <td><span data-ttu-id="c66d0-822">Database</span><span class="sxs-lookup"><span data-stu-id="c66d0-822">Database</span></span></td>
      <td><span data-ttu-id="c66d0-823">
        <font size=2> protocol: odbc</span><span class="sxs-lookup"><span data-stu-id="c66d0-823">
        <font size=2> protocol: odbc</span></span> <br><span data-ttu-id="c66d0-824">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-824">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-825">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-825">address:</span></span> <br><span data-ttu-id="c66d0-826">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="c66d0-826">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="c66d0-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-828">Generic ODBC</span><span class="sxs-lookup"><span data-stu-id="c66d0-828">Generic ODBC</span></span></td>
      <td><span data-ttu-id="c66d0-829">Table</span><span class="sxs-lookup"><span data-stu-id="c66d0-829">Table</span></span></td>
      <td><span data-ttu-id="c66d0-830">Table, View</span><span class="sxs-lookup"><span data-stu-id="c66d0-830">Table, View</span></span></td>
      <td><span data-ttu-id="c66d0-831">
        <font size=2> protocol: odbc</span><span class="sxs-lookup"><span data-stu-id="c66d0-831">
        <font size=2> protocol: odbc</span></span> <br><span data-ttu-id="c66d0-832">authentication: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="c66d0-832">authentication: {basic, windows}</span></span> <br><span data-ttu-id="c66d0-833">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-833">address:</span></span> <br><span data-ttu-id="c66d0-834">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="c66d0-834">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="c66d0-835">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="c66d0-835">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="c66d0-836">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="c66d0-836">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="c66d0-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="c66d0-838">Other (None of the above)</span><span class="sxs-lookup"><span data-stu-id="c66d0-838">Other (None of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="c66d0-839">
        <font size=2> protocol: generic-asset</span><span class="sxs-lookup"><span data-stu-id="c66d0-839">
        <font size=2> protocol: generic-asset</span></span> <br><span data-ttu-id="c66d0-840">address:</span><span class="sxs-lookup"><span data-stu-id="c66d0-840">address:</span></span> <br><span data-ttu-id="c66d0-841">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="c66d0-841">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
