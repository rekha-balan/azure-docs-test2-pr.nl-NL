---
title: Release notes for Data Management Gateway | Microsoft Docs
description: Data Management Gateway tory release notes
services: data-factory
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: spelluru
published: true
ms.openlocfilehash: 9b8fccdca5d4419a401e7955365107b29728d09b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556200"
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="a1881-103">Release notes for Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="a1881-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="a1881-104">One of the challenges for modern data integration is to seamlessly move data to and from on-premises to cloud.</span><span class="sxs-lookup"><span data-stu-id="a1881-104">One of the challenges for modern data integration is to seamlessly move data to and from on-premises to cloud.</span></span> <span data-ttu-id="a1881-105">Data Factory makes this integration seamless with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span><span class="sxs-lookup"><span data-stu-id="a1881-105">Data Factory makes this integration seamless with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="a1881-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span><span class="sxs-lookup"><span data-stu-id="a1881-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span> 

*  [<span data-ttu-id="a1881-107">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="a1881-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="a1881-108">Move data between on-premises and cloud using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md) 


## <a name="current-version-2762192"></a><span data-ttu-id="a1881-109">CURRENT VERSION (2.7.6219.2)</span><span class="sxs-lookup"><span data-stu-id="a1881-109">CURRENT VERSION (2.7.6219.2)</span></span>

### <a name="whats-new"></a><span data-ttu-id="a1881-110">What’s new</span><span class="sxs-lookup"><span data-stu-id="a1881-110">What’s new</span></span>
- <span data-ttu-id="a1881-111">You can now authenticate into your Azure Data Lake Store using service principal.</span><span class="sxs-lookup"><span data-stu-id="a1881-111">You can now authenticate into your Azure Data Lake Store using service principal.</span></span> <span data-ttu-id="a1881-112">Previous we only supported OAuth.</span><span class="sxs-lookup"><span data-stu-id="a1881-112">Previous we only supported OAuth.</span></span>
- <span data-ttu-id="a1881-113">We have packaged new driver for reading data from Oracle on premise data store in gateway.</span><span class="sxs-lookup"><span data-stu-id="a1881-113">We have packaged new driver for reading data from Oracle on premise data store in gateway.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="a1881-114">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a1881-114">Enhancements-</span></span>
- <span data-ttu-id="a1881-115">Improved data read performance from Oracle data source.</span><span class="sxs-lookup"><span data-stu-id="a1881-115">Improved data read performance from Oracle data source.</span></span>
- <span data-ttu-id="a1881-116">Fixed: OData source OAuth token expiration issue.</span><span class="sxs-lookup"><span data-stu-id="a1881-116">Fixed: OData source OAuth token expiration issue.</span></span>
- <span data-ttu-id="a1881-117">Fixed: Unable to read Oracle decimal over 28 bits issue.</span><span class="sxs-lookup"><span data-stu-id="a1881-117">Fixed: Unable to read Oracle decimal over 28 bits issue.</span></span>


## <a name="earlier-versions"></a><span data-ttu-id="a1881-118">Earlier versions</span><span class="sxs-lookup"><span data-stu-id="a1881-118">Earlier versions</span></span>

## <a name="2661922"></a><span data-ttu-id="a1881-119">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="a1881-119">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="a1881-120">What’s new</span><span class="sxs-lookup"><span data-stu-id="a1881-120">What’s new</span></span>
- <span data-ttu-id="a1881-121">Customers can provide feedback on gateway registering experience.</span><span class="sxs-lookup"><span data-stu-id="a1881-121">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="a1881-122">Support a new compression format: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="a1881-122">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="a1881-123">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a1881-123">Enhancements-</span></span>
- <span data-ttu-id="a1881-124">Performance improvement for Oracle Sink, HDFS source.</span><span class="sxs-lookup"><span data-stu-id="a1881-124">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="a1881-125">Bug fix for gateway auto update, gateway parallel processing capacity.</span><span class="sxs-lookup"><span data-stu-id="a1881-125">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="a1881-126">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="a1881-126">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="a1881-127">Enhancements</span><span class="sxs-lookup"><span data-stu-id="a1881-127">Enhancements</span></span>
- <span data-ttu-id="a1881-128">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span><span class="sxs-lookup"><span data-stu-id="a1881-128">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="a1881-129">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span><span class="sxs-lookup"><span data-stu-id="a1881-129">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="a1881-130">This would require you to reset Linked Service credentials in Portal.</span><span class="sxs-lookup"><span data-stu-id="a1881-130">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="a1881-131">Bug fix.</span><span class="sxs-lookup"><span data-stu-id="a1881-131">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="a1881-132">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="a1881-132">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="a1881-133">What’s new</span><span class="sxs-lookup"><span data-stu-id="a1881-133">What’s new</span></span>

- <span data-ttu-id="a1881-134">You can now store data source credentials locally.</span><span class="sxs-lookup"><span data-stu-id="a1881-134">You can now store data source credentials locally.</span></span> <span data-ttu-id="a1881-135">The credentials are encrypted.</span><span class="sxs-lookup"><span data-stu-id="a1881-135">The credentials are encrypted.</span></span> <span data-ttu-id="a1881-136">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on premise.</span><span class="sxs-lookup"><span data-stu-id="a1881-136">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on premise.</span></span> 

### <a name="enhancements-"></a><span data-ttu-id="a1881-137">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a1881-137">Enhancements-</span></span>

- <span data-ttu-id="a1881-138">Improved and more robust Gateway registration experience.</span><span class="sxs-lookup"><span data-stu-id="a1881-138">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="a1881-139">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span><span class="sxs-lookup"><span data-stu-id="a1881-139">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="a1881-140">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="a1881-140">2.3.6100.2</span></span>

- <span data-ttu-id="a1881-141">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span><span class="sxs-lookup"><span data-stu-id="a1881-141">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="a1881-142">Enhance the stability of network connection between gateway and Service Bus</span><span class="sxs-lookup"><span data-stu-id="a1881-142">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="a1881-143">A few bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-143">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="a1881-144">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="a1881-144">2.2.6072.1</span></span>

*  <span data-ttu-id="a1881-145">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a1881-145">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="a1881-146">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span><span class="sxs-lookup"><span data-stu-id="a1881-146">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="a1881-147">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span><span class="sxs-lookup"><span data-stu-id="a1881-147">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="a1881-148">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span><span class="sxs-lookup"><span data-stu-id="a1881-148">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="a1881-149">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="a1881-149">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="a1881-150">Enhances the robustness of gateway registration using registration key.</span><span class="sxs-lookup"><span data-stu-id="a1881-150">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="a1881-151">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="a1881-151">2.1.6040.</span></span>

*  <span data-ttu-id="a1881-152">DB2 driver is included in the gateway installation package now.</span><span class="sxs-lookup"><span data-stu-id="a1881-152">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="a1881-153">You do not need to install it separately.</span><span class="sxs-lookup"><span data-stu-id="a1881-153">You do not need to install it separately.</span></span> 
*  <span data-ttu-id="a1881-154">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span><span class="sxs-lookup"><span data-stu-id="a1881-154">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span> 
*  <span data-ttu-id="a1881-155">Supports using DocumentDB as a source or destination for on-premises data stores</span><span class="sxs-lookup"><span data-stu-id="a1881-155">Supports using DocumentDB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="a1881-156">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span><span class="sxs-lookup"><span data-stu-id="a1881-156">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span> 
*  <span data-ttu-id="a1881-157">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span><span class="sxs-lookup"><span data-stu-id="a1881-157">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="a1881-158">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="a1881-158">2.0.6013.1</span></span>

*  <span data-ttu-id="a1881-159">You can select the language/culture to be used by a gateway during manual installation.</span><span class="sxs-lookup"><span data-stu-id="a1881-159">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="a1881-160">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span><span class="sxs-lookup"><span data-stu-id="a1881-160">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="a1881-161">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span><span class="sxs-lookup"><span data-stu-id="a1881-161">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="a1881-162">User interface improvements for gateway configuration manager:</span><span class="sxs-lookup"><span data-stu-id="a1881-162">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="a1881-163">Make gateway status more visible on the Home tab.</span><span class="sxs-lookup"><span data-stu-id="a1881-163">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="a1881-164">Reorganized and simplified controls.</span><span class="sxs-lookup"><span data-stu-id="a1881-164">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="a1881-165">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a1881-165">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="a1881-166">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span><span class="sxs-lookup"><span data-stu-id="a1881-166">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span> 
*  <span data-ttu-id="a1881-167">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a1881-167">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="a1881-168">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-168">Performance improvements</span></span>

    * <span data-ttu-id="a1881-169">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span><span class="sxs-lookup"><span data-stu-id="a1881-169">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="a1881-170">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="a1881-170">1.12.5953.1</span></span>

*  <span data-ttu-id="a1881-171">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-171">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="a1881-172">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="a1881-172">1.11.5918.1</span></span>

*  <span data-ttu-id="a1881-173">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span><span class="sxs-lookup"><span data-stu-id="a1881-173">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="a1881-174">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span><span class="sxs-lookup"><span data-stu-id="a1881-174">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="a1881-175">You can choose to restart right then or later.</span><span class="sxs-lookup"><span data-stu-id="a1881-175">You can choose to restart right then or later.</span></span> 

*  <span data-ttu-id="a1881-176">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span><span class="sxs-lookup"><span data-stu-id="a1881-176">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="a1881-177">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-177">Performance improvements</span></span>

    * <span data-ttu-id="a1881-178">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span><span class="sxs-lookup"><span data-stu-id="a1881-178">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="a1881-179">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-179">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="a1881-180">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="a1881-180">1.10.5892.1</span></span>

*  <span data-ttu-id="a1881-181">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-181">Performance improvements</span></span>

*  <span data-ttu-id="a1881-182">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-182">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="a1881-183">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="a1881-183">1.9.5865.2</span></span>

*  <span data-ttu-id="a1881-184">Zero touch auto update capability</span><span class="sxs-lookup"><span data-stu-id="a1881-184">Zero touch auto update capability</span></span>
*  <span data-ttu-id="a1881-185">New tray icon with gateway status indicators</span><span class="sxs-lookup"><span data-stu-id="a1881-185">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="a1881-186">Ability to “Update now” from the client</span><span class="sxs-lookup"><span data-stu-id="a1881-186">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="a1881-187">Ability to set update schedule time</span><span class="sxs-lookup"><span data-stu-id="a1881-187">Ability to set update schedule time</span></span>
*  <span data-ttu-id="a1881-188">PowerShell script for toggling auto-update on/off</span><span class="sxs-lookup"><span data-stu-id="a1881-188">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="a1881-189">Support for JSON format</span><span class="sxs-lookup"><span data-stu-id="a1881-189">Support for JSON format</span></span>  
*  <span data-ttu-id="a1881-190">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-190">Performance improvements</span></span>
*  <span data-ttu-id="a1881-191">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-191">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="a1881-192">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="a1881-192">1.8.5822.1</span></span>

*  <span data-ttu-id="a1881-193">Improve troubleshooting experience</span><span class="sxs-lookup"><span data-stu-id="a1881-193">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="a1881-194">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-194">Performance improvements</span></span>
*  <span data-ttu-id="a1881-195">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-195">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="a1881-196">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="a1881-196">1.7.5795.1</span></span>

*  <span data-ttu-id="a1881-197">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-197">Performance improvements</span></span>
*  <span data-ttu-id="a1881-198">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-198">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="a1881-199">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="a1881-199">1.7.5764.1</span></span>

*  <span data-ttu-id="a1881-200">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-200">Performance improvements</span></span>
*  <span data-ttu-id="a1881-201">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-201">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="a1881-202">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="a1881-202">1.6.5735.1</span></span>

*  <span data-ttu-id="a1881-203">Support on-premises HDFS Source/Sink</span><span class="sxs-lookup"><span data-stu-id="a1881-203">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="a1881-204">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-204">Performance improvements</span></span>
*  <span data-ttu-id="a1881-205">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-205">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="a1881-206">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="a1881-206">1.6.5696.1</span></span>

*  <span data-ttu-id="a1881-207">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-207">Performance improvements</span></span>
*  <span data-ttu-id="a1881-208">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-208">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="a1881-209">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="a1881-209">1.6.5676.1</span></span>

*  <span data-ttu-id="a1881-210">Support diagnostic tools on Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a1881-210">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="a1881-211">Support table columns for tabular data sources for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-211">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-212">Support SQL DW for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-212">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-213">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-213">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-214">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-214">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-215">Support Copy Activity reporting progress for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-215">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-216">Support Data Source Connectivity Validation for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-216">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-217">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-217">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="a1881-218">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="a1881-218">1.6.5672.1</span></span>

*  <span data-ttu-id="a1881-219">Support table name for ODBC data source for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-219">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-220">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-220">Performance improvements</span></span>
*  <span data-ttu-id="a1881-221">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-221">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="a1881-222">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="a1881-222">1.6.5658.1</span></span>

*  <span data-ttu-id="a1881-223">Support File Sink for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-223">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-224">Support preserving hierarchy in binary copy for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-224">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-225">Support Copy Activity Idempotency for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-225">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-226">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-226">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="a1881-227">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="a1881-227">1.6.5640.1</span></span>

*  <span data-ttu-id="a1881-228">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="a1881-228">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="a1881-229">Support quote character in csv parser for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-229">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-230">Compression support (BZip2)</span><span class="sxs-lookup"><span data-stu-id="a1881-230">Compression support (BZip2)</span></span>
*  <span data-ttu-id="a1881-231">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-231">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="a1881-232">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="a1881-232">1.5.5612.1</span></span>

*  <span data-ttu-id="a1881-233">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span><span class="sxs-lookup"><span data-stu-id="a1881-233">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="a1881-234">Compression support (Gzip and Deflate)</span><span class="sxs-lookup"><span data-stu-id="a1881-234">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="a1881-235">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-235">Performance improvements</span></span>
*  <span data-ttu-id="a1881-236">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-236">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="a1881-237">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="a1881-237">1.4.5549.1</span></span>

*  <span data-ttu-id="a1881-238">Add Oracle data source support for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1881-238">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="a1881-239">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a1881-239">Performance improvements</span></span>
*  <span data-ttu-id="a1881-240">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a1881-240">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="a1881-241">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="a1881-241">1.4.5492.1</span></span>

*  <span data-ttu-id="a1881-242">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span><span class="sxs-lookup"><span data-stu-id="a1881-242">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="a1881-243">Refine the Configuration UI and registration process</span><span class="sxs-lookup"><span data-stu-id="a1881-243">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="a1881-244">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span><span class="sxs-lookup"><span data-stu-id="a1881-244">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="a1881-245">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="a1881-245">1.2.5303.1</span></span>

*  <span data-ttu-id="a1881-246">Fix timeout issue to support more time-consuming data source connections.</span><span class="sxs-lookup"><span data-stu-id="a1881-246">Fix timeout issue to support more time-consuming data source connections.</span></span> 

### <a name="1155268"></a><span data-ttu-id="a1881-247">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="a1881-247">1.1.5526.8</span></span>

*  <span data-ttu-id="a1881-248">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span><span class="sxs-lookup"><span data-stu-id="a1881-248">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="a1881-249">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="a1881-249">1.0.5144.2</span></span>

*  <span data-ttu-id="a1881-250">No changes that affect Azure Data Factory scenarios.</span><span class="sxs-lookup"><span data-stu-id="a1881-250">No changes that affect Azure Data Factory scenarios.</span></span>
