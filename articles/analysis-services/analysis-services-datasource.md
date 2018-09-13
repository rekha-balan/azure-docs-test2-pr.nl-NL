---
title: Data sources supported in Azure Analysis Services | Microsoft Docs
description: Describes data sources supported for data models in Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: f6ad95eb45cc208fe2289cb2095214f98a0b250b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44778900"
---
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="8966e-103">Data sources supported in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8966e-103">Data sources supported in Azure Analysis Services</span></span>

<span data-ttu-id="8966e-104">Data sources and connectors shown in Get Data or Import Wizard in Visual Studio are shown for both Azure Analysis Services and SQL Server Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="8966e-104">Data sources and connectors shown in Get Data or Import Wizard in Visual Studio are shown for both Azure Analysis Services and SQL Server Analysis Services.</span></span> <span data-ttu-id="8966e-105">However, not all data sources and  connectors shown are supported in Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="8966e-105">However, not all data sources and  connectors shown are supported in Azure Analysis Services.</span></span> <span data-ttu-id="8966e-106">The types of data sources you can connect to depend on many factors such as model compatibility level, available data connectors, authentication type, providers, and On-premises data gateway support.</span><span class="sxs-lookup"><span data-stu-id="8966e-106">The types of data sources you can connect to depend on many factors such as model compatibility level, available data connectors, authentication type, providers, and On-premises data gateway support.</span></span> 

## <a name="azure-data-sources"></a><span data-ttu-id="8966e-107">Azure data sources</span><span class="sxs-lookup"><span data-stu-id="8966e-107">Azure data sources</span></span>

|<span data-ttu-id="8966e-108">Datasource</span><span class="sxs-lookup"><span data-stu-id="8966e-108">Datasource</span></span>  |<span data-ttu-id="8966e-109">In-memory</span><span class="sxs-lookup"><span data-stu-id="8966e-109">In-memory</span></span>  |<span data-ttu-id="8966e-110">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="8966e-110">DirectQuery</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="8966e-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8966e-111">Azure SQL Database</span></span>     |   <span data-ttu-id="8966e-112">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-112">Yes</span></span>      |    <span data-ttu-id="8966e-113">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-113">Yes</span></span>      |
|<span data-ttu-id="8966e-114">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8966e-114">Azure SQL Data Warehouse</span></span>     |   <span data-ttu-id="8966e-115">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-115">Yes</span></span>      |   <span data-ttu-id="8966e-116">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-116">Yes</span></span>       |
|<span data-ttu-id="8966e-117">Azure Blob Storage\*</span><span class="sxs-lookup"><span data-stu-id="8966e-117">Azure Blob Storage\*</span></span>     |   <span data-ttu-id="8966e-118">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-118">Yes</span></span>       |    <span data-ttu-id="8966e-119">No</span><span class="sxs-lookup"><span data-stu-id="8966e-119">No</span></span>      |
|<span data-ttu-id="8966e-120">Azure Table Storage\*</span><span class="sxs-lookup"><span data-stu-id="8966e-120">Azure Table Storage\*</span></span>    |   <span data-ttu-id="8966e-121">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-121">Yes</span></span>       |    <span data-ttu-id="8966e-122">No</span><span class="sxs-lookup"><span data-stu-id="8966e-122">No</span></span>      |
|<span data-ttu-id="8966e-123">Azure Cosmos DB\*</span><span class="sxs-lookup"><span data-stu-id="8966e-123">Azure Cosmos DB\*</span></span>     |  <span data-ttu-id="8966e-124">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-124">Yes</span></span>        |  <span data-ttu-id="8966e-125">No</span><span class="sxs-lookup"><span data-stu-id="8966e-125">No</span></span>        |
|<span data-ttu-id="8966e-126">Azure Data Lake Store\*</span><span class="sxs-lookup"><span data-stu-id="8966e-126">Azure Data Lake Store\*</span></span>     |   <span data-ttu-id="8966e-127">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-127">Yes</span></span>       |    <span data-ttu-id="8966e-128">No</span><span class="sxs-lookup"><span data-stu-id="8966e-128">No</span></span>      |
|<span data-ttu-id="8966e-129">Azure HDInsight HDFS\*</span><span class="sxs-lookup"><span data-stu-id="8966e-129">Azure HDInsight HDFS\*</span></span>     |     <span data-ttu-id="8966e-130">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-130">Yes</span></span>     |   <span data-ttu-id="8966e-131">No</span><span class="sxs-lookup"><span data-stu-id="8966e-131">No</span></span>       |
|<span data-ttu-id="8966e-132">Azure HDInsight Spark\*</span><span class="sxs-lookup"><span data-stu-id="8966e-132">Azure HDInsight Spark\*</span></span>     |   <span data-ttu-id="8966e-133">Yes</span><span class="sxs-lookup"><span data-stu-id="8966e-133">Yes</span></span>       |   <span data-ttu-id="8966e-134">No</span><span class="sxs-lookup"><span data-stu-id="8966e-134">No</span></span>       |
||||

<span data-ttu-id="8966e-135">\* Tabular 1400 models only.</span><span class="sxs-lookup"><span data-stu-id="8966e-135">\* Tabular 1400 models only.</span></span>

<span data-ttu-id="8966e-136">**Provider** </span><span class="sxs-lookup"><span data-stu-id="8966e-136">**Provider** </span></span>  
<span data-ttu-id="8966e-137">In-memory and DirectQuery models connecting to Azure data sources use .NET Framework Data Provider for SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8966e-137">In-memory and DirectQuery models connecting to Azure data sources use .NET Framework Data Provider for SQL Server.</span></span>

## <a name="on-premises-data-sources"></a><span data-ttu-id="8966e-138">On-premises data sources</span><span class="sxs-lookup"><span data-stu-id="8966e-138">On-premises data sources</span></span>

<span data-ttu-id="8966e-139">Connecting to on-premises data sources from and Azure AS server require an On-premises gateway.</span><span class="sxs-lookup"><span data-stu-id="8966e-139">Connecting to on-premises data sources from and Azure AS server require an On-premises gateway.</span></span> <span data-ttu-id="8966e-140">When using a gateway, 64-bit providers are required.</span><span class="sxs-lookup"><span data-stu-id="8966e-140">When using a gateway, 64-bit providers are required.</span></span>

### <a name="in-memory-and-directquery"></a><span data-ttu-id="8966e-141">In-memory and DirectQuery</span><span class="sxs-lookup"><span data-stu-id="8966e-141">In-memory and DirectQuery</span></span>

|<span data-ttu-id="8966e-142">Datasource</span><span class="sxs-lookup"><span data-stu-id="8966e-142">Datasource</span></span> | <span data-ttu-id="8966e-143">In-memory provider</span><span class="sxs-lookup"><span data-stu-id="8966e-143">In-memory provider</span></span> | <span data-ttu-id="8966e-144">DirectQuery provider</span><span class="sxs-lookup"><span data-stu-id="8966e-144">DirectQuery provider</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="8966e-145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8966e-145">SQL Server</span></span> |<span data-ttu-id="8966e-146">SQL Server Native Client 11.0, Microsoft OLE DB Provider for SQL Server, .NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="8966e-146">SQL Server Native Client 11.0, Microsoft OLE DB Provider for SQL Server, .NET Framework Data Provider for SQL Server</span></span> | <span data-ttu-id="8966e-147">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="8966e-147">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="8966e-148">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8966e-148">SQL Server Data Warehouse</span></span> |<span data-ttu-id="8966e-149">SQL Server Native Client 11.0, Microsoft OLE DB Provider for SQL Server, .NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="8966e-149">SQL Server Native Client 11.0, Microsoft OLE DB Provider for SQL Server, .NET Framework Data Provider for SQL Server</span></span> | <span data-ttu-id="8966e-150">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="8966e-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="8966e-151">Oracle</span><span class="sxs-lookup"><span data-stu-id="8966e-151">Oracle</span></span> |<span data-ttu-id="8966e-152">Microsoft OLE DB Provider for Oracle, Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="8966e-152">Microsoft OLE DB Provider for Oracle, Oracle Data Provider for .NET</span></span> |<span data-ttu-id="8966e-153">Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="8966e-153">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="8966e-154">Teradata</span><span class="sxs-lookup"><span data-stu-id="8966e-154">Teradata</span></span> |<span data-ttu-id="8966e-155">OLE DB Provider for Teradata, Teradata Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="8966e-155">OLE DB Provider for Teradata, Teradata Data Provider for .NET</span></span> |<span data-ttu-id="8966e-156">Teradata Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="8966e-156">Teradata Data Provider for .NET</span></span> | |
| | | |

### <a name="in-memory-only"></a><span data-ttu-id="8966e-157">In-memory only</span><span class="sxs-lookup"><span data-stu-id="8966e-157">In-memory only</span></span>

|<span data-ttu-id="8966e-158">Datasource</span><span class="sxs-lookup"><span data-stu-id="8966e-158">Datasource</span></span>  |  
|---------|---------|
|<span data-ttu-id="8966e-159">Access Database</span><span class="sxs-lookup"><span data-stu-id="8966e-159">Access Database</span></span>     |  
|<span data-ttu-id="8966e-160">Active Directory\*</span><span class="sxs-lookup"><span data-stu-id="8966e-160">Active Directory\*</span></span>     |  
|<span data-ttu-id="8966e-161">Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8966e-161">Analysis Services</span></span>     |  
|<span data-ttu-id="8966e-162">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="8966e-162">Analytics Platform System</span></span>     |  
|<span data-ttu-id="8966e-163">Dynamics CRM\*</span><span class="sxs-lookup"><span data-stu-id="8966e-163">Dynamics CRM\*</span></span>     |  
|<span data-ttu-id="8966e-164">Excel workbook</span><span class="sxs-lookup"><span data-stu-id="8966e-164">Excel workbook</span></span>     |  
|<span data-ttu-id="8966e-165">Exchange\*</span><span class="sxs-lookup"><span data-stu-id="8966e-165">Exchange\*</span></span>     |  
|<span data-ttu-id="8966e-166">Folder\*</span><span class="sxs-lookup"><span data-stu-id="8966e-166">Folder\*</span></span>     |
|<span data-ttu-id="8966e-167">IBM Informix\* (Beta)</span><span class="sxs-lookup"><span data-stu-id="8966e-167">IBM Informix\* (Beta)</span></span> |
|<span data-ttu-id="8966e-168">JSON document\*</span><span class="sxs-lookup"><span data-stu-id="8966e-168">JSON document\*</span></span>     |  
|<span data-ttu-id="8966e-169">Lines from binary\*</span><span class="sxs-lookup"><span data-stu-id="8966e-169">Lines from binary\*</span></span>     | 
|<span data-ttu-id="8966e-170">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="8966e-170">MySQL Database</span></span>     | 
|<span data-ttu-id="8966e-171">OData Feed\*</span><span class="sxs-lookup"><span data-stu-id="8966e-171">OData Feed\*</span></span>     |  
|<span data-ttu-id="8966e-172">ODBC query</span><span class="sxs-lookup"><span data-stu-id="8966e-172">ODBC query</span></span>     | 
|<span data-ttu-id="8966e-173">OLE DB</span><span class="sxs-lookup"><span data-stu-id="8966e-173">OLE DB</span></span>     |   
|<span data-ttu-id="8966e-174">Postgre SQL Database\*</span><span class="sxs-lookup"><span data-stu-id="8966e-174">Postgre SQL Database\*</span></span>    | 
|<span data-ttu-id="8966e-175">Salesforce Objects\*</span><span class="sxs-lookup"><span data-stu-id="8966e-175">Salesforce Objects\*</span></span> |  
|<span data-ttu-id="8966e-176">Salesforce Reports\*</span><span class="sxs-lookup"><span data-stu-id="8966e-176">Salesforce Reports\*</span></span> |
|<span data-ttu-id="8966e-177">SAP HANA\*</span><span class="sxs-lookup"><span data-stu-id="8966e-177">SAP HANA\*</span></span>    |  
|<span data-ttu-id="8966e-178">SAP Business Warehouse\*</span><span class="sxs-lookup"><span data-stu-id="8966e-178">SAP Business Warehouse\*</span></span>    |  
|<span data-ttu-id="8966e-179">SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="8966e-179">SharePoint\*</span></span>     |   
|<span data-ttu-id="8966e-180">Sybase Database</span><span class="sxs-lookup"><span data-stu-id="8966e-180">Sybase Database</span></span>     |  
|<span data-ttu-id="8966e-181">XML table\*</span><span class="sxs-lookup"><span data-stu-id="8966e-181">XML table\*</span></span>    |  
|||
 
<span data-ttu-id="8966e-182">\* Tabular 1400 models only.</span><span class="sxs-lookup"><span data-stu-id="8966e-182">\* Tabular 1400 models only.</span></span>

## <a name="specifying-a-different-provider"></a><span data-ttu-id="8966e-183">Specifying a different provider</span><span class="sxs-lookup"><span data-stu-id="8966e-183">Specifying a different provider</span></span>

<span data-ttu-id="8966e-184">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span><span class="sxs-lookup"><span data-stu-id="8966e-184">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="8966e-185">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span><span class="sxs-lookup"><span data-stu-id="8966e-185">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span> <span data-ttu-id="8966e-186">If using native providers other than SQLOLEDB, you may see error message: **The provider 'SQLNCLI11.1' is not registered**.</span><span class="sxs-lookup"><span data-stu-id="8966e-186">If using native providers other than SQLOLEDB, you may see error message: **The provider 'SQLNCLI11.1' is not registered**.</span></span> <span data-ttu-id="8966e-187">Or, if you have a DirectQuery model connecting to on-premises data sources and you use native providers, you may see error message: **Error creating OLE DB row set. Incorrect syntax near 'LIMIT'**.</span><span class="sxs-lookup"><span data-stu-id="8966e-187">Or, if you have a DirectQuery model connecting to on-premises data sources and you use native providers, you may see error message: **Error creating OLE DB row set. Incorrect syntax near 'LIMIT'**.</span></span>

<span data-ttu-id="8966e-188">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span><span class="sxs-lookup"><span data-stu-id="8966e-188">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="8966e-189">**To specify a provider**</span><span class="sxs-lookup"><span data-stu-id="8966e-189">**To specify a provider**</span></span>

1. <span data-ttu-id="8966e-190">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span><span class="sxs-lookup"><span data-stu-id="8966e-190">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="8966e-191">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span><span class="sxs-lookup"><span data-stu-id="8966e-191">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="8966e-192">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span><span class="sxs-lookup"><span data-stu-id="8966e-192">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="8966e-193">Impersonation</span><span class="sxs-lookup"><span data-stu-id="8966e-193">Impersonation</span></span>
<span data-ttu-id="8966e-194">In some cases, it may be necessary to specify a different impersonation account.</span><span class="sxs-lookup"><span data-stu-id="8966e-194">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="8966e-195">Impersonation account can be specified in Visual Studio (SSDT) or SSMS.</span><span class="sxs-lookup"><span data-stu-id="8966e-195">Impersonation account can be specified in Visual Studio (SSDT) or SSMS.</span></span>

<span data-ttu-id="8966e-196">For on-premises data sources:</span><span class="sxs-lookup"><span data-stu-id="8966e-196">For on-premises data sources:</span></span>

* <span data-ttu-id="8966e-197">If using SQL authentication, impersonation should be Service Account.</span><span class="sxs-lookup"><span data-stu-id="8966e-197">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="8966e-198">If using Windows authentication, set Windows user/password.</span><span class="sxs-lookup"><span data-stu-id="8966e-198">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="8966e-199">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span><span class="sxs-lookup"><span data-stu-id="8966e-199">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="8966e-200">For cloud data sources:</span><span class="sxs-lookup"><span data-stu-id="8966e-200">For cloud data sources:</span></span>

* <span data-ttu-id="8966e-201">If using SQL authentication, impersonation should be Service Account.</span><span class="sxs-lookup"><span data-stu-id="8966e-201">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8966e-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="8966e-202">Next steps</span></span>
<span data-ttu-id="8966e-203">[On-premises gateway](analysis-services-gateway.md) </span><span class="sxs-lookup"><span data-stu-id="8966e-203">[On-premises gateway](analysis-services-gateway.md) </span></span>  
[<span data-ttu-id="8966e-204">Manage your server</span><span class="sxs-lookup"><span data-stu-id="8966e-204">Manage your server</span></span>](analysis-services-manage.md)   

