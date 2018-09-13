---
title: Release notes for Data Management Gateway | Microsoft Docs
description: Data Management Gateway tory release notes
services: data-factory
author: nabhishek
manager: craigg
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: abnarain
robots: noindex
ms.openlocfilehash: ac0e1945e75ee7aea346c103a671b4a47b9e5994
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864588"
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="a329c-103">Release notes for Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="a329c-103">Release notes for Data Management Gateway</span></span>
> [!NOTE]
> <span data-ttu-id="a329c-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a329c-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="a329c-105">If you are using the current version of the Data Factory service, see [self-hosted integration runtime in V2](../create-self-hosted-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="a329c-105">If you are using the current version of the Data Factory service, see [self-hosted integration runtime in V2](../create-self-hosted-integration-runtime.md).</span></span>

<span data-ttu-id="a329c-106">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span><span class="sxs-lookup"><span data-stu-id="a329c-106">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span></span> <span data-ttu-id="a329c-107">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span><span class="sxs-lookup"><span data-stu-id="a329c-107">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="a329c-108">See the following articles for detailed information about Data Management Gateway and how to use it:</span><span class="sxs-lookup"><span data-stu-id="a329c-108">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span>

*  [<span data-ttu-id="a329c-109">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="a329c-109">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="a329c-110">Move data between on-premises and cloud using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-110">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version"></a><span data-ttu-id="a329c-111">CURRENT VERSION</span><span class="sxs-lookup"><span data-stu-id="a329c-111">CURRENT VERSION</span></span> 
<span data-ttu-id="a329c-112">We no more maintain the Release notes here.</span><span class="sxs-lookup"><span data-stu-id="a329c-112">We no more maintain the Release notes here.</span></span> <span data-ttu-id="a329c-113">Get latest release notes [here](https://go.microsoft.com/fwlink/?linkid=853077)</span><span class="sxs-lookup"><span data-stu-id="a329c-113">Get latest release notes [here](https://go.microsoft.com/fwlink/?linkid=853077)</span></span>




## <a name="earlier-versions"></a><span data-ttu-id="a329c-114">Earlier versions</span><span class="sxs-lookup"><span data-stu-id="a329c-114">Earlier versions</span></span>
## <a name="21063477"></a><span data-ttu-id="a329c-115">2.10.6347.7</span><span class="sxs-lookup"><span data-stu-id="a329c-115">2.10.6347.7</span></span>
### <a name="enhancements-"></a><span data-ttu-id="a329c-116">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a329c-116">Enhancements-</span></span>
- <span data-ttu-id="a329c-117">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span><span class="sxs-lookup"><span data-stu-id="a329c-117">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="a329c-118">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span><span class="sxs-lookup"><span data-stu-id="a329c-118">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="a329c-119">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span><span class="sxs-lookup"><span data-stu-id="a329c-119">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="a329c-120">Fixed: Issue with gateway offline during update (due to clock skew)</span><span class="sxs-lookup"><span data-stu-id="a329c-120">Fixed: Issue with gateway offline during update (due to clock skew)</span></span>


## <a name="2963132"></a><span data-ttu-id="a329c-121">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="a329c-121">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="a329c-122">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a329c-122">Enhancements-</span></span>
-   <span data-ttu-id="a329c-123">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span><span class="sxs-lookup"><span data-stu-id="a329c-123">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="a329c-124">More details here.</span><span class="sxs-lookup"><span data-stu-id="a329c-124">More details here.</span></span>
-   <span data-ttu-id="a329c-125">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span><span class="sxs-lookup"><span data-stu-id="a329c-125">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span></span> <span data-ttu-id="a329c-126">(earlier limit was 195 GB).</span><span class="sxs-lookup"><span data-stu-id="a329c-126">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="a329c-127">Fixed: Out of memory issue while unzipping several small files during copy activity.</span><span class="sxs-lookup"><span data-stu-id="a329c-127">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="a329c-128">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span><span class="sxs-lookup"><span data-stu-id="a329c-128">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="a329c-129">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="a329c-129">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="a329c-130">Fixed: Column name with space at the end does not work in copy activity.</span><span class="sxs-lookup"><span data-stu-id="a329c-130">Fixed: Column name with space at the end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="a329c-131">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="a329c-131">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="a329c-132">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a329c-132">Enhancements-</span></span>
- <span data-ttu-id="a329c-133">Fixed: Issue with missing credentials on gateway machine reboot.</span><span class="sxs-lookup"><span data-stu-id="a329c-133">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="a329c-134">Fixed: Issue with registration during gateway restore using a backup file.</span><span class="sxs-lookup"><span data-stu-id="a329c-134">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="a329c-135">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="a329c-135">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="a329c-136">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a329c-136">Enhancements-</span></span>
- <span data-ttu-id="a329c-137">Fixed: Incorrect read of Decimal null value from Oracle as source.</span><span class="sxs-lookup"><span data-stu-id="a329c-137">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="a329c-138">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="a329c-138">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="a329c-139">What’s new</span><span class="sxs-lookup"><span data-stu-id="a329c-139">What’s new</span></span>
- <span data-ttu-id="a329c-140">Customers can provide feedback on gateway registering experience.</span><span class="sxs-lookup"><span data-stu-id="a329c-140">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="a329c-141">Support a new compression format: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="a329c-141">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="a329c-142">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a329c-142">Enhancements-</span></span>
- <span data-ttu-id="a329c-143">Performance improvement for Oracle Sink, HDFS source.</span><span class="sxs-lookup"><span data-stu-id="a329c-143">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="a329c-144">Bug fix for gateway auto update, gateway parallel processing capacity.</span><span class="sxs-lookup"><span data-stu-id="a329c-144">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="a329c-145">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="a329c-145">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="a329c-146">Enhancements</span><span class="sxs-lookup"><span data-stu-id="a329c-146">Enhancements</span></span>
- <span data-ttu-id="a329c-147">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span><span class="sxs-lookup"><span data-stu-id="a329c-147">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="a329c-148">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span><span class="sxs-lookup"><span data-stu-id="a329c-148">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="a329c-149">This would require you to reset Linked Service credentials in Portal.</span><span class="sxs-lookup"><span data-stu-id="a329c-149">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="a329c-150">Bug fix.</span><span class="sxs-lookup"><span data-stu-id="a329c-150">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="a329c-151">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="a329c-151">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="a329c-152">What’s new</span><span class="sxs-lookup"><span data-stu-id="a329c-152">What’s new</span></span>

- <span data-ttu-id="a329c-153">You can now store data source credentials locally.</span><span class="sxs-lookup"><span data-stu-id="a329c-153">You can now store data source credentials locally.</span></span> <span data-ttu-id="a329c-154">The credentials are encrypted.</span><span class="sxs-lookup"><span data-stu-id="a329c-154">The credentials are encrypted.</span></span> <span data-ttu-id="a329c-155">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span><span class="sxs-lookup"><span data-stu-id="a329c-155">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="a329c-156">Enhancements-</span><span class="sxs-lookup"><span data-stu-id="a329c-156">Enhancements-</span></span>

- <span data-ttu-id="a329c-157">Improved and more robust Gateway registration experience.</span><span class="sxs-lookup"><span data-stu-id="a329c-157">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="a329c-158">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span><span class="sxs-lookup"><span data-stu-id="a329c-158">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="a329c-159">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="a329c-159">2.3.6100.2</span></span>

- <span data-ttu-id="a329c-160">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span><span class="sxs-lookup"><span data-stu-id="a329c-160">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="a329c-161">Enhance the stability of network connection between gateway and Service Bus</span><span class="sxs-lookup"><span data-stu-id="a329c-161">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="a329c-162">A few bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-162">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="a329c-163">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="a329c-163">2.2.6072.1</span></span>

*  <span data-ttu-id="a329c-164">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a329c-164">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="a329c-165">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span><span class="sxs-lookup"><span data-stu-id="a329c-165">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="a329c-166">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span><span class="sxs-lookup"><span data-stu-id="a329c-166">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="a329c-167">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span><span class="sxs-lookup"><span data-stu-id="a329c-167">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="a329c-168">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="a329c-168">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="a329c-169">Enhances the robustness of gateway registration using registration key.</span><span class="sxs-lookup"><span data-stu-id="a329c-169">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="a329c-170">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="a329c-170">2.1.6040.</span></span>

*  <span data-ttu-id="a329c-171">DB2 driver is included in the gateway installation package now.</span><span class="sxs-lookup"><span data-stu-id="a329c-171">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="a329c-172">You do not need to install it separately.</span><span class="sxs-lookup"><span data-stu-id="a329c-172">You do not need to install it separately.</span></span>
*  <span data-ttu-id="a329c-173">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span><span class="sxs-lookup"><span data-stu-id="a329c-173">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="a329c-174">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span><span class="sxs-lookup"><span data-stu-id="a329c-174">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="a329c-175">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span><span class="sxs-lookup"><span data-stu-id="a329c-175">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="a329c-176">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span><span class="sxs-lookup"><span data-stu-id="a329c-176">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="a329c-177">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="a329c-177">2.0.6013.1</span></span>

*  <span data-ttu-id="a329c-178">You can select the language/culture to be used by a gateway during manual installation.</span><span class="sxs-lookup"><span data-stu-id="a329c-178">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="a329c-179">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span><span class="sxs-lookup"><span data-stu-id="a329c-179">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="a329c-180">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span><span class="sxs-lookup"><span data-stu-id="a329c-180">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="a329c-181">User interface improvements for gateway configuration manager:</span><span class="sxs-lookup"><span data-stu-id="a329c-181">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="a329c-182">Make gateway status more visible on the Home tab.</span><span class="sxs-lookup"><span data-stu-id="a329c-182">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="a329c-183">Reorganized and simplified controls.</span><span class="sxs-lookup"><span data-stu-id="a329c-183">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="a329c-184">You can copy data from a storage using the [code-free copy tool](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a329c-184">You can copy data from a storage using the [code-free copy tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="a329c-185">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span><span class="sxs-lookup"><span data-stu-id="a329c-185">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="a329c-186">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a329c-186">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="a329c-187">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-187">Performance improvements</span></span>

    * <span data-ttu-id="a329c-188">Improve performance on viewing Schema/Preview against SQL Server in code-free copy tool.</span><span class="sxs-lookup"><span data-stu-id="a329c-188">Improve performance on viewing Schema/Preview against SQL Server in code-free copy tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="a329c-189">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="a329c-189">1.12.5953.1</span></span>

*  <span data-ttu-id="a329c-190">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-190">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="a329c-191">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="a329c-191">1.11.5918.1</span></span>

*  <span data-ttu-id="a329c-192">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span><span class="sxs-lookup"><span data-stu-id="a329c-192">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="a329c-193">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span><span class="sxs-lookup"><span data-stu-id="a329c-193">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="a329c-194">You can choose to restart right then or later.</span><span class="sxs-lookup"><span data-stu-id="a329c-194">You can choose to restart right then or later.</span></span>

*  <span data-ttu-id="a329c-195">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span><span class="sxs-lookup"><span data-stu-id="a329c-195">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="a329c-196">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-196">Performance improvements</span></span>

    * <span data-ttu-id="a329c-197">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span><span class="sxs-lookup"><span data-stu-id="a329c-197">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="a329c-198">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-198">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="a329c-199">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="a329c-199">1.10.5892.1</span></span>

*  <span data-ttu-id="a329c-200">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-200">Performance improvements</span></span>

*  <span data-ttu-id="a329c-201">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-201">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="a329c-202">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="a329c-202">1.9.5865.2</span></span>

*  <span data-ttu-id="a329c-203">Zero touch auto update capability</span><span class="sxs-lookup"><span data-stu-id="a329c-203">Zero touch auto update capability</span></span>
*  <span data-ttu-id="a329c-204">New tray icon with gateway status indicators</span><span class="sxs-lookup"><span data-stu-id="a329c-204">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="a329c-205">Ability to “Update now” from the client</span><span class="sxs-lookup"><span data-stu-id="a329c-205">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="a329c-206">Ability to set update schedule time</span><span class="sxs-lookup"><span data-stu-id="a329c-206">Ability to set update schedule time</span></span>
*  <span data-ttu-id="a329c-207">PowerShell script for toggling auto-update on/off</span><span class="sxs-lookup"><span data-stu-id="a329c-207">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="a329c-208">Support for JSON format</span><span class="sxs-lookup"><span data-stu-id="a329c-208">Support for JSON format</span></span>  
*  <span data-ttu-id="a329c-209">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-209">Performance improvements</span></span>
*  <span data-ttu-id="a329c-210">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-210">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="a329c-211">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="a329c-211">1.8.5822.1</span></span>

*  <span data-ttu-id="a329c-212">Improve troubleshooting experience</span><span class="sxs-lookup"><span data-stu-id="a329c-212">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="a329c-213">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-213">Performance improvements</span></span>
*  <span data-ttu-id="a329c-214">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-214">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="a329c-215">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="a329c-215">1.7.5795.1</span></span>

*  <span data-ttu-id="a329c-216">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-216">Performance improvements</span></span>
*  <span data-ttu-id="a329c-217">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-217">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="a329c-218">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="a329c-218">1.7.5764.1</span></span>

*  <span data-ttu-id="a329c-219">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-219">Performance improvements</span></span>
*  <span data-ttu-id="a329c-220">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-220">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="a329c-221">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="a329c-221">1.6.5735.1</span></span>

*  <span data-ttu-id="a329c-222">Support on-premises HDFS Source/Sink</span><span class="sxs-lookup"><span data-stu-id="a329c-222">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="a329c-223">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-223">Performance improvements</span></span>
*  <span data-ttu-id="a329c-224">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-224">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="a329c-225">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="a329c-225">1.6.5696.1</span></span>

*  <span data-ttu-id="a329c-226">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-226">Performance improvements</span></span>
*  <span data-ttu-id="a329c-227">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-227">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="a329c-228">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="a329c-228">1.6.5676.1</span></span>

*  <span data-ttu-id="a329c-229">Support diagnostic tools on Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a329c-229">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="a329c-230">Support table columns for tabular data sources for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-230">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-231">Support SQL DW for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-231">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-232">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-232">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-233">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-233">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-234">Support Copy Activity reporting progress for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-234">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-235">Support Data Source Connectivity Validation for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-235">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-236">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-236">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="a329c-237">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="a329c-237">1.6.5672.1</span></span>

*  <span data-ttu-id="a329c-238">Support table name for ODBC data source for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-238">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-239">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-239">Performance improvements</span></span>
*  <span data-ttu-id="a329c-240">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-240">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="a329c-241">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="a329c-241">1.6.5658.1</span></span>

*  <span data-ttu-id="a329c-242">Support File Sink for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-242">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-243">Support preserving hierarchy in binary copy for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-243">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-244">Support Copy Activity Idempotency for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-244">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-245">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-245">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="a329c-246">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="a329c-246">1.6.5640.1</span></span>

*  <span data-ttu-id="a329c-247">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="a329c-247">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="a329c-248">Support quote character in csv parser for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-248">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-249">Compression support (BZip2)</span><span class="sxs-lookup"><span data-stu-id="a329c-249">Compression support (BZip2)</span></span>
*  <span data-ttu-id="a329c-250">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-250">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="a329c-251">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="a329c-251">1.5.5612.1</span></span>

*  <span data-ttu-id="a329c-252">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span><span class="sxs-lookup"><span data-stu-id="a329c-252">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="a329c-253">Compression support (Gzip and Deflate)</span><span class="sxs-lookup"><span data-stu-id="a329c-253">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="a329c-254">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-254">Performance improvements</span></span>
*  <span data-ttu-id="a329c-255">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-255">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="a329c-256">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="a329c-256">1.4.5549.1</span></span>

*  <span data-ttu-id="a329c-257">Add Oracle data source support for Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a329c-257">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="a329c-258">Performance improvements</span><span class="sxs-lookup"><span data-stu-id="a329c-258">Performance improvements</span></span>
*  <span data-ttu-id="a329c-259">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="a329c-259">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="a329c-260">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="a329c-260">1.4.5492.1</span></span>

*  <span data-ttu-id="a329c-261">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span><span class="sxs-lookup"><span data-stu-id="a329c-261">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="a329c-262">Refine the Configuration UI and registration process</span><span class="sxs-lookup"><span data-stu-id="a329c-262">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="a329c-263">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span><span class="sxs-lookup"><span data-stu-id="a329c-263">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="a329c-264">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="a329c-264">1.2.5303.1</span></span>

*  <span data-ttu-id="a329c-265">Fix timeout issue to support more time-consuming data source connections.</span><span class="sxs-lookup"><span data-stu-id="a329c-265">Fix timeout issue to support more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="a329c-266">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="a329c-266">1.1.5526.8</span></span>

*  <span data-ttu-id="a329c-267">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span><span class="sxs-lookup"><span data-stu-id="a329c-267">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="a329c-268">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="a329c-268">1.0.5144.2</span></span>

*  <span data-ttu-id="a329c-269">No changes that affect Azure Data Factory scenarios.</span><span class="sxs-lookup"><span data-stu-id="a329c-269">No changes that affect Azure Data Factory scenarios.</span></span>
